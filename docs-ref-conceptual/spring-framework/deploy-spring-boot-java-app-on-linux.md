---
title: Déployer une application web Spring Boot sur Azure App Service pour conteneur
description: Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot en tant qu’application web Linux sur Microsoft Azure.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270865"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a><span data-ttu-id="d1f8f-103">Déployer une application Spring Boot sur Azure App Service pour conteneur</span><span class="sxs-lookup"><span data-stu-id="d1f8f-103">Deploy a Spring Boot application on Azure App Service for Container</span></span>

<span data-ttu-id="d1f8f-104">Ce tutoriel vous guide dans l’utilisation de [Docker] pour conteneuriser votre application [Spring Boot] et déployer votre propre image docker sur un hôte Linux dans [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span><span class="sxs-lookup"><span data-stu-id="d1f8f-104">This tutorial walks you through using [Docker] to containerize your [Spring Boot] application and deploy your own docker image to a Linux host in the [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1f8f-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d1f8f-105">Prerequisites</span></span>

<span data-ttu-id="d1f8f-106">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-106">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="d1f8f-107">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d1f8f-108">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-108">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="d1f8f-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="d1f8f-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="d1f8f-111">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="d1f8f-112">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-112">A [Git] client.</span></span>
* <span data-ttu-id="d1f8f-113">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d1f8f-114">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="d1f8f-115">Créer l’application web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="d1f8f-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="d1f8f-116">La procédure suivante vous guide à travers les étapes nécessaires pour créer une application web Spring Boot simple et pour la tester localement.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-116">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="d1f8f-117">Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="d1f8f-118">- ou -</span><span class="sxs-lookup"><span data-stu-id="d1f8f-118">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="d1f8f-119">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="d1f8f-120">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-120">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="d1f8f-121">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-121">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="d1f8f-122">Une fois l’application web créée, accédez au répertoire `target` où se trouve fichier JAR et démarrez l’application web. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-122">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="d1f8f-123">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-123">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="d1f8f-124">Par exemple, si curl est disponible et que vous configuré le serveur Tomcat pour s’exécuter sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-124">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="d1f8f-125">Vous devriez voir le message suivant : **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="d1f8f-125">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="d1f8f-127">Créer un registre de conteneurs Azure à utiliser comme registre Docker privé</span><span class="sxs-lookup"><span data-stu-id="d1f8f-127">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="d1f8f-128">Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-128">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d1f8f-129">Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d1f8f-129">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
>

1. <span data-ttu-id="d1f8f-130">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-130">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="d1f8f-131">Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créer un registre de conteneurs Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-131">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="d1f8f-132">Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Conteneurs** puis cliquez sur **Registre de conteneurs Azure**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-132">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Créer un registre de conteneurs Azure][AR01]

1. <span data-ttu-id="d1f8f-134">Quand la page d’informations pour le modèle de registre de conteneurs Azure s’affiche, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-134">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Créer un registre de conteneurs Azure][AR02]

1. <span data-ttu-id="d1f8f-136">Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-136">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. <span data-ttu-id="d1f8f-138">Une fois votre registre de conteneurs créé, accédez à celui-ci dans le portail Azure puis cliquez sur **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-138">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="d1f8f-139">Notez le nom d’utilisateur et le mot de passe pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-139">Take note of the username and password for the next steps.</span></span>

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="d1f8f-141">Configurer Maven pour utiliser les clés d’accès de votre registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="d1f8f-141">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="d1f8f-142">Accédez au répertoire du projet terminé pour votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-142">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="d1f8f-143">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la dernière version de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) ainsi que la valeur du serveur de connexion et les paramètres d’accès pour votre registre de conteneurs Azure obtenus à la section précédente de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-143">Update the `<properties>` collection in the *pom.xml* file with the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) and login server value and access settings for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="d1f8f-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-144">For example:</span></span>

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. <span data-ttu-id="d1f8f-145">Ajoutez [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) à la collection `<plugins>` dans le fichier *pom.xml*, spécifiez l’image de base à `<from>/<image>` et le nom de l’image finale `<to>/<image>`, puis spécifiez le nom d’utilisateur et le mot de passe de la section précédente à `<to>/<auth>`.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-145">Add [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) to the `<plugins>` collection in the *pom.xml* file, specify the base image at `<from>/<image>` and  final image name `<to>/<image>`, specify the username and password from previous section at `<to>/<auth>`.</span></span> <span data-ttu-id="d1f8f-146">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-146">For example:</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="d1f8f-147">Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-147">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="d1f8f-148">Quand vous utilisez Jib pour envoyer votre image à Azure Container Registry, l’image ne respecte pas *Dockerfile*. Pour plus d’informations, consultez [ce](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-148">When you are using Jib to push your image to the Azure Container Registry, the image will not honor *Dockerfile*, see [this](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document for details.</span></span>
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="d1f8f-149">Créer une application web sur Linux sur Azure App Service en utilisant votre image de conteneur</span><span class="sxs-lookup"><span data-stu-id="d1f8f-149">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="d1f8f-150">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-150">Browse to the [Azure portal] and sign in.</span></span>

2. <span data-ttu-id="d1f8f-151">Cliquez sur l’icône de menu pour **+ Créer une ressource**, cliquez sur **Web**, puis sur **Web App pour conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-151">Click the menu icon for **+ Create a resource**, then click **Web**, and then click **Web App for Containers**.</span></span>
   
   ![Créer une application web dans le portail Azure][LX01]

3. <span data-ttu-id="d1f8f-153">Quand la page **Application web sur Linux** s’affiche, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-153">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="d1f8f-154">a.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-154">a.</span></span> <span data-ttu-id="d1f8f-155">Entrez un nom unique pour le **Nom de l’application**, par exemple « *wingtiptoyslinux* ».</span><span class="sxs-lookup"><span data-stu-id="d1f8f-155">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*"</span></span>

   <span data-ttu-id="d1f8f-156">b.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-156">b.</span></span> <span data-ttu-id="d1f8f-157">Choisissez votre **abonnement** dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-157">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="d1f8f-158">c.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-158">c.</span></span> <span data-ttu-id="d1f8f-159">Choisissez un **Groupe de ressources** existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-159">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="d1f8f-160">d.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-160">d.</span></span> <span data-ttu-id="d1f8f-161">Choisissez *Linux* comme **Système d’exploitation**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-161">Choose *Linux* as the **OS**.</span></span>

   <span data-ttu-id="d1f8f-162">e.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-162">e.</span></span> <span data-ttu-id="d1f8f-163">Cliquez sur **Plan App Service/Emplacement** et choisissez un plan App Service existant, ou cliquez sur **Créer** pour créer un nouveau plan App Service.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-163">Click **App Service plan/Location** and choose an existing app service plan, or click **Create new** to create a new app service plan.</span></span>

   <span data-ttu-id="d1f8f-164">f.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-164">f.</span></span> <span data-ttu-id="d1f8f-165">Cliquez sur **Configurer le conteneur** et entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-165">Click **Configure container** and enter the following information:</span></span>

   * <span data-ttu-id="d1f8f-166">Choisissez **Conteneur unique** et **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-166">Choose **Single Container** and  **Azure Container Registry**.</span></span>

   * <span data-ttu-id="d1f8f-167">**Registry** : choisissez le nom du conteneur que vous avez créé, par exemple « *wingtiptoysregistry* ».</span><span class="sxs-lookup"><span data-stu-id="d1f8f-167">**Registry**: Choose your container name created earlier; for example: "*wingtiptoysregistry*"</span></span>

   * <span data-ttu-id="d1f8f-168">**Image** : choisissez le nom de l’image, par exemple « *gs-spring-boot-docker* ».</span><span class="sxs-lookup"><span data-stu-id="d1f8f-168">**Image**: Choose the image name; for example: "*gs-spring-boot-docker*"</span></span>
   
   * <span data-ttu-id="d1f8f-169">**Balise** : choisissez l’étiquette de l’image, par exemple « *latest* ».</span><span class="sxs-lookup"><span data-stu-id="d1f8f-169">**Tag**: Choose the tag for the image; for example: "*latest*"</span></span>
   
   * <span data-ttu-id="d1f8f-170">**Fichier de démarrage** : laissez vide, car l’image a déjà la commande de démarrage.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-170">**Startup File**: Keep it blank since the image already has the start up command</span></span>
   
   <span data-ttu-id="d1f8f-171">e.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-171">e.</span></span> <span data-ttu-id="d1f8f-172">Après avoir entré toutes les informations ci-dessus, cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-172">Once you have entered all of the above information, click **Apply**.</span></span>

   ![Configurer les paramètres de l’application web][LX02]

4. <span data-ttu-id="d1f8f-174">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d1f8f-175">Azure mappera automatiquement les demandes Internet au serveur Tomcat incorporé qui s’exécute sur les ports standard 80 ou 8080.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="d1f8f-176">Cependant, si vous avez configuré votre serveur Tomcat incorporé pour qu’il s’exécute sur un port personnalisé, vous devez ajouter une variable d’environnement à votre application web qui définit le port pour votre serveur Tomcat incorporé.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="d1f8f-177">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="d1f8f-178">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="d1f8f-179">Cliquez sur l’icône pour **App Services**, puis sélectionnez votre application web dans la liste.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-179">Click the icon for **App Services**, and select your web app from the list.</span></span>
>
> 4. <span data-ttu-id="d1f8f-180">Cliquez sur **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-180">Click **Configuration**.</span></span> <span data-ttu-id="d1f8f-181">(Élément 1 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="d1f8f-181">(Item #1 in the image below.)</span></span>
>
> 5. <span data-ttu-id="d1f8f-182">Dans la section **Paramètres de l’application**, ajoutez un nouveau paramètre nommé **PORT** et entrez comme valeur votre numéro de port personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-182">In the **Application settings** section, add a new setting named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="d1f8f-183">(Éléments 2, 3 et 4 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="d1f8f-183">(Item #2, #3, #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="d1f8f-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-184">Click **Save**.</span></span> <span data-ttu-id="d1f8f-185">(Élément 5 de l’image ci-dessous.)</span><span class="sxs-lookup"><span data-stu-id="d1f8f-185">(Item #5 in the image below.)</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="d1f8f-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1f8f-187">Next steps</span></span>

<span data-ttu-id="d1f8f-188">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-188">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1f8f-189">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="d1f8f-189">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="d1f8f-190">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d1f8f-190">Additional Resources</span></span>

<span data-ttu-id="d1f8f-191">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d1f8f-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="d1f8f-192">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d1f8f-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="d1f8f-193">Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d1f8f-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="d1f8f-194">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-194">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="d1f8f-195">Pour plus d’informations sur l’exemple de projet Spring Boot on Docker, consultez [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="d1f8f-196">Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="d1f8f-197">Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="d1f8f-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="d1f8f-198">Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].</span><span class="sxs-lookup"><span data-stu-id="d1f8f-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Utilisation d’Azure DevOps et Java]: /azure/devops/java/
[Working with Azure DevOps and Java]: /azure/devops/java/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

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
