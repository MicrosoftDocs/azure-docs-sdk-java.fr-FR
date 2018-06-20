---
title: Déployer une application web Spring Boot sur Linux dans Azure Container Service
description: Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot en tant qu’application web Linux sur Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: container-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: c3a10a0d6029ba31b13f82907311d9182f98acb6
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954750"
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="2dda8-103">Déployer une application Spring Boot sur Linux dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="2dda8-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="2dda8-104">Ce didacticiel vous guide dans l’utilisation de [client Docker] pour développer et déployer une application [Spring Boot] sur un hôte Linux dans [Azure Container Service (AKS)].</span><span class="sxs-lookup"><span data-stu-id="2dda8-104">This tutorial walks you through using [Docker] to develop and deploy a [Spring Boot] application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2dda8-105">configuration requise</span><span class="sxs-lookup"><span data-stu-id="2dda8-105">Prerequisites</span></span>

<span data-ttu-id="2dda8-106">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2dda8-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="2dda8-107">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="2dda8-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="2dda8-108">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="2dda8-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="2dda8-109">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="2dda8-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="2dda8-110">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="2dda8-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="2dda8-111">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="2dda8-111">A [Git] client.</span></span>
* <span data-ttu-id="2dda8-112">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="2dda8-112">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2dda8-113">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="2dda8-113">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="2dda8-114">Créer l’application web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="2dda8-114">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="2dda8-115">La procédure suivante vous guide à travers les étapes nécessaires pour créer une application web Spring Boot simple et pour la tester localement.</span><span class="sxs-lookup"><span data-stu-id="2dda8-115">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="2dda8-116">Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-116">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="2dda8-117">- ou -</span><span class="sxs-lookup"><span data-stu-id="2dda8-117">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="2dda8-118">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-118">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="2dda8-119">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-119">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="2dda8-120">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-120">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="2dda8-121">Une fois l’application web créée, accédez au répertoire `target` où se trouve fichier JAR et démarrez l’application web. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-121">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="2dda8-122">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="2dda8-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="2dda8-123">Par exemple, si curl est disponible et que vous configuré le serveur Tomcat pour s’exécuter sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="2dda8-123">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="2dda8-124">Vous devez normalement voir le message suivant : **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="2dda8-124">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="2dda8-126">Créer un registre de conteneurs Azure à utiliser comme registre Docker privé</span><span class="sxs-lookup"><span data-stu-id="2dda8-126">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="2dda8-127">Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="2dda8-127">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2dda8-128">Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2dda8-128">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="2dda8-129">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="2dda8-129">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="2dda8-130">Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créer un registre de conteneurs Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.</span><span class="sxs-lookup"><span data-stu-id="2dda8-130">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="2dda8-131">Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Conteneurs** puis cliquez sur **Registre de conteneurs Azure**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-131">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Créer un registre de conteneurs Azure][AR01]

1. <span data-ttu-id="2dda8-133">Quand la page d’informations pour le modèle de registre de conteneurs Azure s’affiche, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-133">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Créer un registre de conteneurs Azure][AR02]

1. <span data-ttu-id="2dda8-135">Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-135">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. <span data-ttu-id="2dda8-137">Une fois votre registre de conteneurs créé, accédez à celui-ci dans le portail Azure puis cliquez sur **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-137">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="2dda8-138">Notez le nom d’utilisateur et le mot de passe pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="2dda8-138">Take note of the username and password for the next steps.</span></span>

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="2dda8-140">Configurer Maven pour utiliser les clés d’accès de votre registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="2dda8-140">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="2dda8-141">Accédez au répertoire de configuration de votre installation de Maven et ouvrez le fichier *settings.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="2dda8-141">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="2dda8-142">Ajoutez les paramètres d’accès de votre registre de conteneurs Azure de la section précédente de ce didacticiel à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-142">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="2dda8-143">Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou «  */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="2dda8-143">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="2dda8-144">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion pour votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-144">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="2dda8-145">Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* de façon à ce que le `<plugin>` contienne l’adresse du serveur de connexion et le nom de registre de votre registre de conteneurs Azure de la section précédente de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2dda8-145">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="2dda8-146">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="2dda8-146">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="2dda8-147">Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :</span><span class="sxs-lookup"><span data-stu-id="2dda8-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="2dda8-148">Quand vous placez votre conteneur Docker dans Azure, vous pouvez recevoir un message d’erreur similaire à un de ceux-ci, même si votre conteneur Docker a été créé correctement :</span><span class="sxs-lookup"><span data-stu-id="2dda8-148">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="2dda8-149">Dans ce cas, vous pouvez être amené à vous connecter à votre compte Azure à partir de la ligne de commande de Docker. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-149">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="2dda8-150">Vous pouvez ensuite placer votre conteneur à partir de la ligne de commande. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2dda8-150">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="2dda8-151">Créer une application web sur Linux sur Azure App Service en utilisant votre image de conteneur</span><span class="sxs-lookup"><span data-stu-id="2dda8-151">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="2dda8-152">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="2dda8-152">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="2dda8-153">Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Web + Mobile** puis cliquez sur **Application web sur Linux**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-153">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Créer une application web dans le portail Azure][LX01]

1. <span data-ttu-id="2dda8-155">Quand la page **Application web sur Linux** s’affiche, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2dda8-155">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="2dda8-156">a.</span><span class="sxs-lookup"><span data-stu-id="2dda8-156">a.</span></span> <span data-ttu-id="2dda8-157">Entrez un nom unique pour le **Nom de l’application**, par exemple : « *wingtiptoyslinux* ».</span><span class="sxs-lookup"><span data-stu-id="2dda8-157">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="2dda8-158">b.</span><span class="sxs-lookup"><span data-stu-id="2dda8-158">b.</span></span> <span data-ttu-id="2dda8-159">Choisissez votre **abonnement** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="2dda8-159">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="2dda8-160">c.</span><span class="sxs-lookup"><span data-stu-id="2dda8-160">c.</span></span> <span data-ttu-id="2dda8-161">Choisissez un **Groupe de ressources** existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="2dda8-161">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="2dda8-162">d.</span><span class="sxs-lookup"><span data-stu-id="2dda8-162">d.</span></span> <span data-ttu-id="2dda8-163">Cliquez sur **Configurer le conteneur** et entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2dda8-163">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="2dda8-164">Choisissez **Registre privé**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-164">Choose **Private registry**.</span></span>

      * <span data-ttu-id="2dda8-165">**Image et étiquette facultative** : spécifiez le nom de votre conteneur utilisé plus haut, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* »</span><span class="sxs-lookup"><span data-stu-id="2dda8-165">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="2dda8-166">**URL du serveur**: spécifiez l’URL du registre déclaré plus haut, par exemple : « *https://wingtiptoysregistry.azurecr.io* »</span><span class="sxs-lookup"><span data-stu-id="2dda8-166">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="2dda8-167">**Nom d’utilisateur de connexion** et **Mot de passe** : spécifiez vos informations d’identification de connexion des **clés d’accès** que vous avez utilisées dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="2dda8-167">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="2dda8-168">e.</span><span class="sxs-lookup"><span data-stu-id="2dda8-168">e.</span></span> <span data-ttu-id="2dda8-169">Après avoir entré toutes les informations ci-dessus, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-169">Once you have entered all of the above information, click **OK**.</span></span>

   ![Configurer les paramètres de l’application web][LX02]

1. <span data-ttu-id="2dda8-171">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-171">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2dda8-172">Azure mappera automatiquement les demandes Internet au serveur Tomcat incorporé qui s’exécute sur les ports standard 80 ou 8080.</span><span class="sxs-lookup"><span data-stu-id="2dda8-172">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="2dda8-173">Cependant, si vous avez configuré votre serveur Tomcat incorporé pour qu’il s’exécute sur un port personnalisé, vous devez ajouter une variable d’environnement à votre application web qui définit le port pour votre serveur Tomcat incorporé.</span><span class="sxs-lookup"><span data-stu-id="2dda8-173">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="2dda8-174">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2dda8-174">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="2dda8-175">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="2dda8-175">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="2dda8-176">Cliquez sur l’icône pour **App Services**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-176">Click the icon for **App Services**.</span></span> <span data-ttu-id="2dda8-177">(Voir l’élément 1 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="2dda8-177">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="2dda8-178">Sélectionnez votre application web dans la liste.</span><span class="sxs-lookup"><span data-stu-id="2dda8-178">Select your web app from the list.</span></span> <span data-ttu-id="2dda8-179">(Élément 2 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="2dda8-179">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="2dda8-180">Cliquez sur **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-180">Click **Application Settings**.</span></span> <span data-ttu-id="2dda8-181">(Élément 3 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="2dda8-181">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="2dda8-182">Dans la section **Paramètres de l’application**, ajoutez une nouvelle variable d’environnement nommée **PORT** et entrez comme valeur votre numéro de port personnalisé.</span><span class="sxs-lookup"><span data-stu-id="2dda8-182">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="2dda8-183">(Élément 4 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="2dda8-183">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="2dda8-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2dda8-184">Click **Save**.</span></span> <span data-ttu-id="2dda8-185">(Élément 5 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="2dda8-185">(Item #5 in the image below.)</span></span>
>
> ![Enregistrement d’un numéro de port personnalisé dans le portail Azure][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="2dda8-187">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2dda8-187">Next steps</span></span>

<span data-ttu-id="2dda8-188">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="2dda8-188">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="2dda8-189">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2dda8-189">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="2dda8-190">Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="2dda8-190">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="2dda8-191">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="2dda8-191">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="2dda8-192">Pour plus d’informations sur l’exemple de projet Spring Boot on Docker, consultez [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="2dda8-192">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="2dda8-193">Pour de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="2dda8-193">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="2dda8-194">Pour plus d’informations sur la création d’une application Spring Boot simple, consultez « Spring Initializr » à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="2dda8-194">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="2dda8-195">Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].</span><span class="sxs-lookup"><span data-stu-id="2dda8-195">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
