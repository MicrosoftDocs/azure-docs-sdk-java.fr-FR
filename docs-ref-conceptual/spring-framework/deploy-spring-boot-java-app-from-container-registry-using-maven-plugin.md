---
title: Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service
description: Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service à l’aide d’un plug-in Maven.
services: container-registry
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: abe73f46e3b5a3b85a9f0272c12539d230c1a879
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991373"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="01dd9-103">Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="01dd9-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="01dd9-104">Cet article explique comment déployer un exemple d’application [Spring Boot] dans Azure Container Registry, puis utiliser le plug-in Maven pour Azure Web Apps pour déployer votre application dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="01dd9-104">This article demonstrates how to deploy a sample [Spring Boot] application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="01dd9-105">Le plug-in Maven pour Azure Web Apps pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web dans Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="01dd9-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="01dd9-106">Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="01dd9-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="01dd9-107">Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.</span><span class="sxs-lookup"><span data-stu-id="01dd9-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="01dd9-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="01dd9-108">Prerequisites</span></span>

<span data-ttu-id="01dd9-109">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="01dd9-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="01dd9-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="01dd9-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="01dd9-111">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="01dd9-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="01dd9-112">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="01dd9-112">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="01dd9-113">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="01dd9-113">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="01dd9-114">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="01dd9-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="01dd9-115">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="01dd9-115">A [Git] client.</span></span>
* <span data-ttu-id="01dd9-116">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="01dd9-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="01dd9-117">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="01dd9-117">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="01dd9-118">Cloner l’exemple Spring Boot sur l’application web Docker</span><span class="sxs-lookup"><span data-stu-id="01dd9-118">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="01dd9-119">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="01dd9-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="01dd9-120">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="01dd9-121">- ou -</span><span class="sxs-lookup"><span data-stu-id="01dd9-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="01dd9-122">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-122">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. <span data-ttu-id="01dd9-123">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="01dd9-124">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="01dd9-125">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="01dd9-126">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="01dd9-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="01dd9-127">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="01dd9-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="01dd9-128">Vous devriez voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="01dd9-128">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

> [!NOTE]
>
> <span data-ttu-id="01dd9-130">Lorsque vous utilisez Docker en local, vous pouvez rencontrer une erreur indiquant que la connexion à l’hôte local sur le port 2375 est impossible.</span><span class="sxs-lookup"><span data-stu-id="01dd9-130">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="01dd9-131">Si cela se produit, autorisez l’utilisation de Docker en local sans TLS.</span><span class="sxs-lookup"><span data-stu-id="01dd9-131">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="01dd9-132">Pour ce faire, ouvrez les paramètres de Docker et cochez l’option **Exposer Docker Daemon sur le port TCP://localhost:2375 sans TLS**.</span><span class="sxs-lookup"><span data-stu-id="01dd9-132">To do so, open your Docker settings and check the option to **Expose daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Exposer Docker Daemon sur le port TCP local 2375][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="01dd9-134">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="01dd9-134">Create an Azure service principal</span></span>

<span data-ttu-id="01dd9-135">Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="01dd9-135">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="01dd9-136">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="01dd9-136">Open a command prompt.</span></span>

2. <span data-ttu-id="01dd9-137">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="01dd9-137">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="01dd9-138">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="01dd9-138">Follow the instructions to complete the sign-in process.</span></span>

3. <span data-ttu-id="01dd9-139">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="01dd9-139">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="01dd9-140">Où :</span><span class="sxs-lookup"><span data-stu-id="01dd9-140">Where:</span></span>

   | <span data-ttu-id="01dd9-141">Paramètre</span><span class="sxs-lookup"><span data-stu-id="01dd9-141">Parameter</span></span>  |                    <span data-ttu-id="01dd9-142">Description</span><span class="sxs-lookup"><span data-stu-id="01dd9-142">Description</span></span>                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | <span data-ttu-id="01dd9-143">Spécifie le nom d’utilisateur pour le principal de service.</span><span class="sxs-lookup"><span data-stu-id="01dd9-143">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="01dd9-144">Spécifie le mot de passe pour le principal de service.</span><span class="sxs-lookup"><span data-stu-id="01dd9-144">Specifies the password for the service principal.</span></span>  |


4. <span data-ttu-id="01dd9-145">Azure répond avec un texte JSON similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="01dd9-145">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="01dd9-146">Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="01dd9-146">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="01dd9-147">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="01dd9-147">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="01dd9-148">Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="01dd9-148">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="01dd9-149">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="01dd9-149">Open a command prompt.</span></span>

1. <span data-ttu-id="01dd9-150">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="01dd9-150">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="01dd9-151">Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans cet article :</span><span class="sxs-lookup"><span data-stu-id="01dd9-151">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="01dd9-152">Remplacez `wingtiptoysresources` dans cet exemple par un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="01dd9-152">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="01dd9-153">Créez un registre de conteneurs Azure privé dans le groupe de ressources pour votre application Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="01dd9-153">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="01dd9-154">Remplacez `wingtiptoysregistry` dans cet exemple par un nom unique pour votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="01dd9-154">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="01dd9-155">Récupérez le mot de passe pour votre registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="01dd9-155">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="01dd9-156">Azure répond avec votre mot de passe ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-156">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="01dd9-157">Ajouter votre registre de conteneurs Azure et votre principal du service Azure à vos paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="01dd9-157">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="01dd9-158">Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="01dd9-158">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. <span data-ttu-id="01dd9-159">Ajoutez les paramètres d’accès de votre registre de conteneurs Azure de la section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-159">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="01dd9-160">Où :</span><span class="sxs-lookup"><span data-stu-id="01dd9-160">Where:</span></span>

   |   <span data-ttu-id="01dd9-161">Élément</span><span class="sxs-lookup"><span data-stu-id="01dd9-161">Element</span></span>    |                                 <span data-ttu-id="01dd9-162">Description</span><span class="sxs-lookup"><span data-stu-id="01dd9-162">Description</span></span>                                  |
   |--------------|------------------------------------------------------------------------------|
   |    `<id>`    |         <span data-ttu-id="01dd9-163">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="01dd9-163">Contains the name of your private Azure container registry.</span></span>          |
   | `<username>` |         <span data-ttu-id="01dd9-164">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="01dd9-164">Contains the name of your private Azure container registry.</span></span>          |
   | `<password>` | <span data-ttu-id="01dd9-165">Contient le mot de passe que vous avez récupéré dans la section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="01dd9-165">Contains the password you retrieved in the previous section of this article.</span></span> |


3. <span data-ttu-id="01dd9-166">Ajoutez vos paramètres du principal de service Azure d’une section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-166">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="01dd9-167">Où :</span><span class="sxs-lookup"><span data-stu-id="01dd9-167">Where:</span></span>

   |     <span data-ttu-id="01dd9-168">Élément</span><span class="sxs-lookup"><span data-stu-id="01dd9-168">Element</span></span>     |                                                                                   <span data-ttu-id="01dd9-169">Description</span><span class="sxs-lookup"><span data-stu-id="01dd9-169">Description</span></span>                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                <span data-ttu-id="01dd9-170">Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="01dd9-170">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>                                |
   |   `<client>`    |                                                             <span data-ttu-id="01dd9-171">Contient la valeur `appId` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="01dd9-171">Contains the `appId` value from your service principal.</span></span>                                                             |
   |   `<tenant>`    |                                                            <span data-ttu-id="01dd9-172">Contient la valeur `tenant` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="01dd9-172">Contains the `tenant` value from your service principal.</span></span>                                                             |
   |     `<key>`     |                                                           <span data-ttu-id="01dd9-173">Contient la valeur `password` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="01dd9-173">Contains the `password` value from your service principal.</span></span>                                                            |
   | `<environment>` | <span data-ttu-id="01dd9-174">Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="01dd9-174">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="01dd9-175">(Une liste complète des environnements est disponible dans la documentation [Plug-in Maven pour Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="01dd9-175">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |


4. <span data-ttu-id="01dd9-176">Enregistrez et fermez le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="01dd9-176">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="01dd9-177">Créer votre image conteneur Docker et la placer dans votre registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="01dd9-177">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="01dd9-178">Accédez au répertoire du projet terminé pour votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="01dd9-178">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

2. <span data-ttu-id="01dd9-179">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion pour votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-179">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="01dd9-180">Où :</span><span class="sxs-lookup"><span data-stu-id="01dd9-180">Where:</span></span>

   |           <span data-ttu-id="01dd9-181">Élément</span><span class="sxs-lookup"><span data-stu-id="01dd9-181">Element</span></span>           |                                                                       <span data-ttu-id="01dd9-182">Description</span><span class="sxs-lookup"><span data-stu-id="01dd9-182">Description</span></span>                                                                       |
   |-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
   | `<azure.containerRegistry>` |                                              <span data-ttu-id="01dd9-183">Spécifie le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="01dd9-183">Specifies the name of your private Azure container registry.</span></span>                                               |
   |   `<docker.image.prefix>`   | <span data-ttu-id="01dd9-184">Spécifie l’URL de votre registre de conteneurs Azure privé qui est obtenue en ajoutant « .azurecr.io » au nom de votre registre de conteneurs privé.</span><span class="sxs-lookup"><span data-stu-id="01dd9-184">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span> |


3. <span data-ttu-id="01dd9-185">Vérifiez que `<plugin>` pour le plug-in Docker dans votre fichier *pom.xml* contient les propriétés appropriées de connexion pour l’adresse du serveur et le nom du registre mentionnées à l’étape précédente de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="01dd9-185">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="01dd9-186">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="01dd9-186">For example:</span></span>

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
   <span data-ttu-id="01dd9-187">Où :</span><span class="sxs-lookup"><span data-stu-id="01dd9-187">Where:</span></span>

   |     <span data-ttu-id="01dd9-188">Élément</span><span class="sxs-lookup"><span data-stu-id="01dd9-188">Element</span></span>     |                                       <span data-ttu-id="01dd9-189">Description</span><span class="sxs-lookup"><span data-stu-id="01dd9-189">Description</span></span>                                       |
   |-----------------|-----------------------------------------------------------------------------------------|
   |  `<serverId>`   |  <span data-ttu-id="01dd9-190">Spécifie la propriété contenant le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="01dd9-190">Specifies the property which contains name of your private Azure container registry.</span></span>   |
   | `<registryUrl>` | <span data-ttu-id="01dd9-191">Spécifie la propriété contenant l’URL de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="01dd9-191">Specifies the property which contains the URL of your private Azure container registry.</span></span> |


4. <span data-ttu-id="01dd9-192">Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :</span><span class="sxs-lookup"><span data-stu-id="01dd9-192">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

5. <span data-ttu-id="01dd9-193">FACULTATIF : accédez au [portail Azure] et vérifiez qu’il existe une image de conteneur Docker nommée **gs-spring-boot-docker** dans le registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="01dd9-193">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Vérification du conteneur dans le portail Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="01dd9-195">Personnaliser votre pom.xml, puis créer et déployer votre conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="01dd9-195">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="01dd9-196">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="01dd9-196">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="01dd9-197">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="01dd9-197">This element should resemble the following example:</span></span>

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

<span data-ttu-id="01dd9-198">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="01dd9-198">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="01dd9-199">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="01dd9-199">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="01dd9-200">Élément</span><span class="sxs-lookup"><span data-stu-id="01dd9-200">Element</span></span> | <span data-ttu-id="01dd9-201">Description</span><span class="sxs-lookup"><span data-stu-id="01dd9-201">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="01dd9-202">Spécifie la version du [Plug-in Maven pour Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="01dd9-202">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="01dd9-203">Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="01dd9-203">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="01dd9-204">Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="01dd9-204">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="01dd9-205">Spécifie le groupe de ressources cible, qui est `wingtiptoysresources` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="01dd9-205">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="01dd9-206">Il sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="01dd9-206">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="01dd9-207">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="01dd9-207">Specifies the target name for your web app.</span></span> <span data-ttu-id="01dd9-208">Dans cet exemple, le nom cible est `maven-linux-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="01dd9-208">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="01dd9-209">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="01dd9-209">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="01dd9-210">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="01dd9-210">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="01dd9-211">(Une liste complète est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="01dd9-211">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<containerSettings>` | <span data-ttu-id="01dd9-212">Spécifie les propriétés qui contiennent le nom et l’URL de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="01dd9-212">Specifies the properties which contain the name and URL of your container.</span></span> |
| `<appSettings>` | <span data-ttu-id="01dd9-213">Spécifie des paramètres uniques que Maven utilisera lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="01dd9-213">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="01dd9-214">Dans cet exemple, un élément `<property>` contient une paire nom/valeur d’éléments enfants qui spécifie le port pour votre application.</span><span class="sxs-lookup"><span data-stu-id="01dd9-214">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="01dd9-215">Les paramètres de modification du numéro de port fournis dans cet exemple sont nécessaires uniquement lorsque vous modifiez le port à partir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="01dd9-215">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="01dd9-216">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-216">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="01dd9-217">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="01dd9-217">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="01dd9-218">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="01dd9-218">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="01dd9-219">Si la région que vous spécifiez dans l’élément `<region>` de votre fichier *pom.xml* n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un message d’erreur similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="01dd9-219">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="01dd9-220">Dans ce cas, vous pouvez spécifier une autre région et ré-exécuter la commande Maven pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="01dd9-220">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="01dd9-221">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="01dd9-221">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="01dd9-222">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="01dd9-222">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="01dd9-224">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="01dd9-224">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

## <a name="next-steps"></a><span data-ttu-id="01dd9-226">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01dd9-226">Next steps</span></span>

<span data-ttu-id="01dd9-227">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="01dd9-227">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01dd9-228">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="01dd9-228">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="01dd9-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="01dd9-229">Additional Resources</span></span>

<span data-ttu-id="01dd9-230">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="01dd9-230">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="01dd9-231">[Plug-in Maven pour Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="01dd9-231">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="01dd9-232">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="01dd9-232">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="01dd9-233">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="01dd9-233">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="01dd9-234">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="01dd9-234">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="01dd9-235">[Plug-in Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="01dd9-235">[Docker plugin for Maven]</span></span>

<span data-ttu-id="01dd9-236">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="01dd9-236">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Plug-in Maven pour Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service/containers/tutorial-custom-docker-image
[Docker]: https://www.docker.com/
[Plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin
[Docker plugin for Maven]: https://github.com/spotify/docker-maven-plugin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/AP02.png
[TL01]: ./media/deploy-spring-boot-java-app-from-container-registry-using-maven-plugin/TL01.png
