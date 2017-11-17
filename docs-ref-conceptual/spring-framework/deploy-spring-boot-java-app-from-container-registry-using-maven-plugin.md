---
title: "Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service"
description: "Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service à l’aide d’un plug-in Maven."
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: multiple
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: b7c2735cdcdeb3dcbfe91fad6c57616e4e5c620c
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="eea19-104">Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="eea19-104">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="eea19-105">Le **[Spring Framework]** est une infrastructure open source populaire qui aide les développeurs Java à créer des applications web, mobiles et API.</span><span class="sxs-lookup"><span data-stu-id="eea19-105">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="eea19-106">Ce didacticiel utilise un exemple d’application créé à l’aide de [Spring Boot], une approche orientée par une convention permettant de prendre en main et d’utiliser Spring rapidement.</span><span class="sxs-lookup"><span data-stu-id="eea19-106">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="eea19-107">Cet article explique comment déployer un exemple d’application Spring Boot dans Azure Container Registry, puis utiliser le plug-in Maven pour Azure Web Apps pour déployer votre application dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="eea19-107">This article demonstrates how to deploy a sample Spring Boot application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="eea19-108">Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="eea19-108">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="eea19-109">Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.</span><span class="sxs-lookup"><span data-stu-id="eea19-109">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="eea19-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="eea19-110">Prerequisites</span></span>

<span data-ttu-id="eea19-111">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eea19-111">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="eea19-112">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="eea19-112">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="eea19-113">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="eea19-113">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="eea19-114">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="eea19-114">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="eea19-115">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="eea19-115">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="eea19-116">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="eea19-116">A [Git] client.</span></span>
* <span data-ttu-id="eea19-117">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="eea19-117">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="eea19-118">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="eea19-118">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="eea19-119">Cloner l’exemple Spring Boot sur l’application web Docker</span><span class="sxs-lookup"><span data-stu-id="eea19-119">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="eea19-120">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="eea19-120">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="eea19-121">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-121">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="eea19-122">- ou -</span><span class="sxs-lookup"><span data-stu-id="eea19-122">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="eea19-123">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-123">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="eea19-124">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-124">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="eea19-125">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-125">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="eea19-126">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-126">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="eea19-127">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="eea19-127">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="eea19-128">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="eea19-128">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="eea19-129">Vous devez normalement voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="eea19-129">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

> [!NOTE]
>
> <span data-ttu-id="eea19-131">Lorsque vous utilisez Docker en local, vous pouvez rencontrer une erreur indiquant que la connexion à l’hôte local sur le port 2375 est impossible.</span><span class="sxs-lookup"><span data-stu-id="eea19-131">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="eea19-132">Si cela se produit, autorisez l’utilisation de Docker en local sans TLS.</span><span class="sxs-lookup"><span data-stu-id="eea19-132">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="eea19-133">Pour ce faire, ouvrez les paramètres de Docker et cochez l’option **Exposer Docker Daemon sur le port TCP://localhost:2375 sans TLS**.</span><span class="sxs-lookup"><span data-stu-id="eea19-133">To do so, open your Docker settings and check the option to **Expose Docker Daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Exposer Docker Daemon sur le port TCP local 2375][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="eea19-135">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="eea19-135">Create an Azure service principal</span></span>

<span data-ttu-id="eea19-136">Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eea19-136">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="eea19-137">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="eea19-137">Open a command prompt.</span></span>

1. <span data-ttu-id="eea19-138">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="eea19-138">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="eea19-139">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="eea19-139">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="eea19-140">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="eea19-140">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="eea19-141">Où `uuuuuuuu` est le nom d’utilisateur et `pppppppp` est le mot de passe du principal du service.</span><span class="sxs-lookup"><span data-stu-id="eea19-141">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="eea19-142">Azure répond avec un texte JSON similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="eea19-142">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="eea19-143">Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eea19-143">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="eea19-144">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="eea19-144">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="eea19-145">Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="eea19-145">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="eea19-146">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="eea19-146">Open a command prompt.</span></span>

1. <span data-ttu-id="eea19-147">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="eea19-147">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="eea19-148">Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans cet article :</span><span class="sxs-lookup"><span data-stu-id="eea19-148">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="eea19-149">Remplacez `wingtiptoysresources` dans cet exemple par un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="eea19-149">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="eea19-150">Créez un registre de conteneurs Azure privé dans le groupe de ressources pour votre application Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="eea19-150">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="eea19-151">Remplacez `wingtiptoysregistry` dans cet exemple par un nom unique pour votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="eea19-151">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="eea19-152">Récupérez le mot de passe pour votre registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="eea19-152">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="eea19-153">Azure répond avec votre mot de passe ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-153">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="eea19-154">Ajouter votre registre de conteneurs Azure et votre principal du service Azure à vos paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="eea19-154">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="eea19-155">Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="eea19-155">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="eea19-156">Ajoutez les paramètres d’accès de votre registre de conteneurs Azure de la section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-156">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="eea19-157">Où :</span><span class="sxs-lookup"><span data-stu-id="eea19-157">Where:</span></span>
   <span data-ttu-id="eea19-158">Élément</span><span class="sxs-lookup"><span data-stu-id="eea19-158">Element</span></span> | <span data-ttu-id="eea19-159">Description</span><span class="sxs-lookup"><span data-stu-id="eea19-159">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="eea19-160">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="eea19-160">Contains the name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="eea19-161">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="eea19-161">Contains the name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="eea19-162">Contient le mot de passe que vous avez récupéré dans la section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="eea19-162">Contains the password you retrieved in the previous section of this article.</span></span>

1. <span data-ttu-id="eea19-163">Ajoutez vos paramètres du principal de service Azure d’une section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-163">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="eea19-164">Où :</span><span class="sxs-lookup"><span data-stu-id="eea19-164">Where:</span></span>
   <span data-ttu-id="eea19-165">Élément</span><span class="sxs-lookup"><span data-stu-id="eea19-165">Element</span></span> | <span data-ttu-id="eea19-166">Description</span><span class="sxs-lookup"><span data-stu-id="eea19-166">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="eea19-167">Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eea19-167">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="eea19-168">Contient la valeur `appId` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="eea19-168">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="eea19-169">Contient la valeur `tenant` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="eea19-169">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="eea19-170">Contient la valeur `password` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="eea19-170">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="eea19-171">Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="eea19-171">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="eea19-172">(Une liste complète des environnements est disponible dans la documentation [Maven Plugin for Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="eea19-172">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="eea19-173">Enregistrez et fermez le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="eea19-173">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="eea19-174">Créer votre image conteneur Docker et la placer dans votre registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="eea19-174">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="eea19-175">Accédez au répertoire du projet terminé pour votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="eea19-175">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="eea19-176">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion pour votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-176">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="eea19-177">Où :</span><span class="sxs-lookup"><span data-stu-id="eea19-177">Where:</span></span>
   <span data-ttu-id="eea19-178">Élément</span><span class="sxs-lookup"><span data-stu-id="eea19-178">Element</span></span> | <span data-ttu-id="eea19-179">Description</span><span class="sxs-lookup"><span data-stu-id="eea19-179">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="eea19-180">Spécifie le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="eea19-180">Specifies the name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="eea19-181">Spécifie l’URL de votre registre de conteneurs Azure privé qui est obtenue en ajoutant « .azurecr.io » au nom de votre registre de conteneurs privé.</span><span class="sxs-lookup"><span data-stu-id="eea19-181">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span>

1. <span data-ttu-id="eea19-182">Vérifiez que `<plugin>` pour le plug-in Docker dans votre fichier *pom.xml* contient les propriétés appropriées de connexion pour l’adresse du serveur et le nom du registre mentionnées à l’étape précédente de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="eea19-182">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="eea19-183">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-183">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="eea19-184">Où :</span><span class="sxs-lookup"><span data-stu-id="eea19-184">Where:</span></span>
   <span data-ttu-id="eea19-185">Élément</span><span class="sxs-lookup"><span data-stu-id="eea19-185">Element</span></span> | <span data-ttu-id="eea19-186">Description</span><span class="sxs-lookup"><span data-stu-id="eea19-186">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="eea19-187">Spécifie la propriété contenant le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="eea19-187">Specifies the property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="eea19-188">Spécifie la propriété contenant l’URL de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="eea19-188">Specifies the property which contains the URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="eea19-189">Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :</span><span class="sxs-lookup"><span data-stu-id="eea19-189">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="eea19-190">FACULTATIF : accédez au [portail Azure] et vérifiez qu’il existe une image de conteneur Docker nommée **gs-spring-boot-docker** dans le registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="eea19-190">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Vérification du conteneur dans le portail Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="eea19-192">Personnaliser votre pom.xml, puis créer et déployer votre conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="eea19-192">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="eea19-193">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="eea19-193">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="eea19-194">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="eea19-194">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="eea19-195">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Maven Plugin for Azure Web Apps] (Plug-in Maven pour Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="eea19-195">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="eea19-196">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="eea19-196">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="eea19-197">Élément</span><span class="sxs-lookup"><span data-stu-id="eea19-197">Element</span></span> | <span data-ttu-id="eea19-198">Description</span><span class="sxs-lookup"><span data-stu-id="eea19-198">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="eea19-199">Spécifie la version du [Maven Plugin for Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="eea19-199">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="eea19-200">Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="eea19-200">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="eea19-201">Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="eea19-201">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="eea19-202">Spécifie le groupe de ressources cible, qui est `wingtiptoysresources` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="eea19-202">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="eea19-203">Il sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="eea19-203">The resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="eea19-204">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="eea19-204">Specifies the target name for your web app.</span></span> <span data-ttu-id="eea19-205">Dans cet exemple, le nom cible est `maven-linux-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="eea19-205">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="eea19-206">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="eea19-206">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="eea19-207">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="eea19-207">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="eea19-208">(Une liste complète est disponible dans la documentation [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="eea19-208">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="eea19-209">Spécifie les propriétés qui contiennent le nom et l’URL de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="eea19-209">Specifies the properties which contain the name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="eea19-210">Spécifie des paramètres uniques que Maven utilisera lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="eea19-210">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="eea19-211">Dans cet exemple, un élément `<property>` contient une paire nom/valeur d’éléments enfants qui spécifie le port pour votre application.</span><span class="sxs-lookup"><span data-stu-id="eea19-211">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="eea19-212">Les paramètres de modification du numéro de port fournis dans cet exemple sont nécessaires uniquement lorsque vous modifiez le port à partir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="eea19-212">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="eea19-213">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-213">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="eea19-214">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="eea19-214">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="eea19-215">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="eea19-215">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="eea19-216">Si la région que vous spécifiez dans l’élément `<region>` de votre fichier *pom.xml* n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un message d’erreur similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="eea19-216">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="eea19-217">Dans ce cas, vous pouvez spécifier une autre région et ré-exécuter la commande Maven pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="eea19-217">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="eea19-218">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="eea19-218">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="eea19-219">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="eea19-219">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="eea19-221">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="eea19-221">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

## <a name="next-steps"></a><span data-ttu-id="eea19-223">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eea19-223">Next steps</span></span>

<span data-ttu-id="eea19-224">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="eea19-224">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="eea19-225">[Maven Plugin for Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="eea19-225">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="eea19-226">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="eea19-226">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="eea19-227">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="eea19-227">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="eea19-228">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="eea19-228">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="eea19-229">[Plug-in Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="eea19-229">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[client Docker]: https://www.docker.com/
[Plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
