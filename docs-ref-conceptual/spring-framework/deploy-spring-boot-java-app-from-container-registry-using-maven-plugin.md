---
title: "Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service"
description: "Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service à l’aide d’un plug-in Maven."
services: container-registry
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 8e8e1b5d599f77edf227d2c187225f6ac530b62b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-in-azure-container-registry-to-azure-app-service"></a><span data-ttu-id="a3e07-103">Comment utiliser le plug-in Maven pour Azure Web Apps pour déployer une application Spring Boot dans Azure Container Registry dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a3e07-103">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app in Azure Container Registry to Azure App Service</span></span>

<span data-ttu-id="a3e07-104">Cet article explique comment déployer un exemple d’application [Spring Boot] dans Azure Container Registry, puis utiliser le plug-in Maven pour Azure Web Apps pour déployer votre application dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="a3e07-104">This article demonstrates how to deploy a sample [Spring Boot] application to Azure Container Registry, and then use the Maven Plugin for Azure Web Apps to deploy your application to Azure App Service.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="a3e07-105">Le plug-in Maven pour Azure Web Apps pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web dans Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="a3e07-105">The Maven Plugin for Azure Web Apps for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>
> 
> <span data-ttu-id="a3e07-106">Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="a3e07-106">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="a3e07-107">Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.</span><span class="sxs-lookup"><span data-stu-id="a3e07-107">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
> 

## <a name="prerequisites"></a><span data-ttu-id="a3e07-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a3e07-108">Prerequisites</span></span>

<span data-ttu-id="a3e07-109">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a3e07-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="a3e07-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="a3e07-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a3e07-111">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="a3e07-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="a3e07-112">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a3e07-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="a3e07-113">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="a3e07-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="a3e07-114">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="a3e07-114">A [Git] client.</span></span>
* <span data-ttu-id="a3e07-115">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="a3e07-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a3e07-116">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="a3e07-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="a3e07-117">Cloner l’exemple Spring Boot sur l’application web Docker</span><span class="sxs-lookup"><span data-stu-id="a3e07-117">Clone the sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="a3e07-118">Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="a3e07-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="a3e07-119">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-119">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="a3e07-120">- ou -</span><span class="sxs-lookup"><span data-stu-id="a3e07-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="a3e07-121">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="a3e07-122">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-122">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="a3e07-123">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-123">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="a3e07-124">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-124">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="a3e07-125">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="a3e07-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="a3e07-126">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="a3e07-126">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="a3e07-127">Vous devez normalement voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="a3e07-127">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

> [!NOTE]
>
> <span data-ttu-id="a3e07-129">Lorsque vous utilisez Docker en local, vous pouvez rencontrer une erreur indiquant que la connexion à l’hôte local sur le port 2375 est impossible.</span><span class="sxs-lookup"><span data-stu-id="a3e07-129">When you are using Docker locally, you may see an error which states that you cannot connect to localhost on port 2375.</span></span> <span data-ttu-id="a3e07-130">Si cela se produit, autorisez l’utilisation de Docker en local sans TLS.</span><span class="sxs-lookup"><span data-stu-id="a3e07-130">If this happens, you may need to enable using Docker locally without TLS.</span></span> <span data-ttu-id="a3e07-131">Pour ce faire, ouvrez les paramètres de Docker et cochez l’option **Exposer Docker Daemon sur le port TCP://localhost:2375 sans TLS**.</span><span class="sxs-lookup"><span data-stu-id="a3e07-131">To do so, open your Docker settings and check the option to **Expose daemon on TCP://localhost:2375 without TLS**.</span></span>
>
> ![Exposer Docker Daemon sur le port TCP local 2375][TL01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="a3e07-133">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="a3e07-133">Create an Azure service principal</span></span>

<span data-ttu-id="a3e07-134">Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e07-134">In this section, you create an Azure service principal that the Maven plugin uses when deploying your container to Azure.</span></span>

1. <span data-ttu-id="a3e07-135">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="a3e07-135">Open a command prompt.</span></span>

1. <span data-ttu-id="a3e07-136">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="a3e07-136">Sign into your Azure account by using the Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="a3e07-137">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="a3e07-137">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="a3e07-138">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="a3e07-138">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="a3e07-139">Où :</span><span class="sxs-lookup"><span data-stu-id="a3e07-139">Where:</span></span>
   | <span data-ttu-id="a3e07-140">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a3e07-140">Parameter</span></span> | <span data-ttu-id="a3e07-141">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="a3e07-141">Description</span></span> |
   |---|---|
   | `uuuuuuuu` | <span data-ttu-id="a3e07-142">Spécifie le nom d’utilisateur pour le principal de service.</span><span class="sxs-lookup"><span data-stu-id="a3e07-142">Specifies the user name for the service principal.</span></span> |
   | `pppppppp` | <span data-ttu-id="a3e07-143">Spécifie le mot de passe pour le principal de service.</span><span class="sxs-lookup"><span data-stu-id="a3e07-143">Specifies the password for the service principal.</span></span> |

1. <span data-ttu-id="a3e07-144">Azure répond avec un texte JSON similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a3e07-144">Azure responds with JSON that resembles the following example:</span></span>
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
   > <span data-ttu-id="a3e07-145">Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre conteneur dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e07-145">You will use the values from this JSON response when you configure the Maven plugin to deploy your container to Azure.</span></span> <span data-ttu-id="a3e07-146">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="a3e07-146">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="a3e07-147">Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a3e07-147">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="a3e07-148">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="a3e07-148">Open a command prompt.</span></span>

1. <span data-ttu-id="a3e07-149">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="a3e07-149">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="a3e07-150">Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans cet article :</span><span class="sxs-lookup"><span data-stu-id="a3e07-150">Create a resource group for the Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="a3e07-151">Remplacez `wingtiptoysresources` dans cet exemple par un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a3e07-151">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="a3e07-152">Créez un registre de conteneurs Azure privé dans le groupe de ressources pour votre application Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="a3e07-152">Create a private Azure container registry in the resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="a3e07-153">Remplacez `wingtiptoysregistry` dans cet exemple par un nom unique pour votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a3e07-153">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="a3e07-154">Récupérez le mot de passe pour votre registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="a3e07-154">Retrieve the password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="a3e07-155">Azure répond avec votre mot de passe ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-155">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-to-your-maven-settings"></a><span data-ttu-id="a3e07-156">Ajouter votre registre de conteneurs Azure et votre principal du service Azure à vos paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="a3e07-156">Add your Azure container registry and Azure service principal to your Maven settings</span></span>

1. <span data-ttu-id="a3e07-157">Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="a3e07-157">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="a3e07-158">Ajoutez les paramètres d’accès de votre registre de conteneurs Azure de la section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-158">Add your Azure Container Registry access settings from the previous section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="a3e07-159">Où :</span><span class="sxs-lookup"><span data-stu-id="a3e07-159">Where:</span></span>
   | <span data-ttu-id="a3e07-160">Élément</span><span class="sxs-lookup"><span data-stu-id="a3e07-160">Element</span></span> | <span data-ttu-id="a3e07-161">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="a3e07-161">Description</span></span> |
   |---|---|
   | `<id>` | <span data-ttu-id="a3e07-162">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="a3e07-162">Contains the name of your private Azure container registry.</span></span> |
   | `<username>` | <span data-ttu-id="a3e07-163">Contient le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="a3e07-163">Contains the name of your private Azure container registry.</span></span> |
   | `<password>` | <span data-ttu-id="a3e07-164">Contient le mot de passe que vous avez récupéré dans la section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="a3e07-164">Contains the password you retrieved in the previous section of this article.</span></span> |

1. <span data-ttu-id="a3e07-165">Ajoutez vos paramètres du principal de service Azure d’une section précédente de cet article à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-165">Add your Azure service principal settings from an earlier section of this article to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="a3e07-166">Où :</span><span class="sxs-lookup"><span data-stu-id="a3e07-166">Where:</span></span>
   | <span data-ttu-id="a3e07-167">Élément</span><span class="sxs-lookup"><span data-stu-id="a3e07-167">Element</span></span> | <span data-ttu-id="a3e07-168">Description</span><span class="sxs-lookup"><span data-stu-id="a3e07-168">Description</span></span> |
   |---|---|
   | `<id>` | <span data-ttu-id="a3e07-169">Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e07-169">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span> |
   | `<client>` | <span data-ttu-id="a3e07-170">Contient la valeur `appId` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="a3e07-170">Contains the `appId` value from your service principal.</span></span> |
   | `<tenant>` | <span data-ttu-id="a3e07-171">Contient la valeur `tenant` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="a3e07-171">Contains the `tenant` value from your service principal.</span></span> |
   | `<key>` | <span data-ttu-id="a3e07-172">Contient la valeur `password` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="a3e07-172">Contains the `password` value from your service principal.</span></span> |
   | `<environment>` | <span data-ttu-id="a3e07-173">Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a3e07-173">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="a3e07-174">(Une liste complète des environnements est disponible dans la documentation [Maven Plugin for Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="a3e07-174">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span> |

1. <span data-ttu-id="a3e07-175">Enregistrez et fermez le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="a3e07-175">Save and close the *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-to-your-azure-container-registry"></a><span data-ttu-id="a3e07-176">Créer votre image conteneur Docker et la placer dans votre registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="a3e07-176">Build your Docker container image and push it to your Azure container registry</span></span>

1. <span data-ttu-id="a3e07-177">Accédez au répertoire du projet terminé pour votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a3e07-177">Navigate to the completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="a3e07-178">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion pour votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-178">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="a3e07-179">Où :</span><span class="sxs-lookup"><span data-stu-id="a3e07-179">Where:</span></span>
   | <span data-ttu-id="a3e07-180">Élément</span><span class="sxs-lookup"><span data-stu-id="a3e07-180">Element</span></span> | <span data-ttu-id="a3e07-181">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="a3e07-181">Description</span></span> |
   |---|---|
   | `<azure.containerRegistry>` | <span data-ttu-id="a3e07-182">Spécifie le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="a3e07-182">Specifies the name of your private Azure container registry.</span></span> |
   | `<docker.image.prefix>` | <span data-ttu-id="a3e07-183">Spécifie l’URL de votre registre de conteneurs Azure privé qui est obtenue en ajoutant « .azurecr.io » au nom de votre registre de conteneurs privé.</span><span class="sxs-lookup"><span data-stu-id="a3e07-183">Specifies the URL of your private Azure container registry, which is derived by appending ".azurecr.io" to the name of your private container registry.</span></span> |

1. <span data-ttu-id="a3e07-184">Vérifiez que `<plugin>` pour le plug-in Docker dans votre fichier *pom.xml* contient les propriétés appropriées de connexion pour l’adresse du serveur et le nom du registre mentionnées à l’étape précédente de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a3e07-184">Verify that `<plugin>` for the Docker plugin in your *pom.xml* file contains the correct properties for the login server address and registry name from the previous step in this tutorial.</span></span> <span data-ttu-id="a3e07-185">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="a3e07-185">For example:</span></span>

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
   <span data-ttu-id="a3e07-186">Où :</span><span class="sxs-lookup"><span data-stu-id="a3e07-186">Where:</span></span>
   | <span data-ttu-id="a3e07-187">Élément</span><span class="sxs-lookup"><span data-stu-id="a3e07-187">Element</span></span> | <span data-ttu-id="a3e07-188">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="a3e07-188">Description</span></span> |
   |---|---|
   | `<serverId>` | <span data-ttu-id="a3e07-189">Spécifie la propriété contenant le nom de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="a3e07-189">Specifies the property which contains name of your private Azure container registry.</span></span> |
   | `<registryUrl>` | <span data-ttu-id="a3e07-190">Spécifie la propriété contenant l’URL de votre registre de conteneurs Azure privé.</span><span class="sxs-lookup"><span data-stu-id="a3e07-190">Specifies the property which contains the URL of your private Azure container registry.</span></span> |

1. <span data-ttu-id="a3e07-191">Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :</span><span class="sxs-lookup"><span data-stu-id="a3e07-191">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="a3e07-192">FACULTATIF : accédez au [portail Azure] et vérifiez qu’il existe une image de conteneur Docker nommée **gs-spring-boot-docker** dans le registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a3e07-192">OPTIONAL: Browse to the [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Vérification du conteneur dans le portail Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-to-azure"></a><span data-ttu-id="a3e07-194">Personnaliser votre pom.xml, puis créer et déployer votre conteneur dans Azure</span><span class="sxs-lookup"><span data-stu-id="a3e07-194">Customize your pom.xml, then build and deploy your container to Azure</span></span>

<span data-ttu-id="a3e07-195">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="a3e07-195">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="a3e07-196">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a3e07-196">This element should resemble the following example:</span></span>

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

<span data-ttu-id="a3e07-197">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Maven Plugin for Azure Web Apps] (Plug-in Maven pour Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="a3e07-197">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="a3e07-198">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="a3e07-198">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="a3e07-199">Élément</span><span class="sxs-lookup"><span data-stu-id="a3e07-199">Element</span></span> | <span data-ttu-id="a3e07-200">Description</span><span class="sxs-lookup"><span data-stu-id="a3e07-200">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="a3e07-201">Spécifie la version du [Maven Plugin for Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="a3e07-201">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="a3e07-202">Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="a3e07-202">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<authentication>` | <span data-ttu-id="a3e07-203">Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="a3e07-203">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="a3e07-204">Spécifie le groupe de ressources cible, qui est `wingtiptoysresources` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a3e07-204">Specifies the target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="a3e07-205">Il sera créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="a3e07-205">The resource group will be created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="a3e07-206">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="a3e07-206">Specifies the target name for your web app.</span></span> <span data-ttu-id="a3e07-207">Dans cet exemple, le nom cible est `maven-linux-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="a3e07-207">In this example, the target name is `maven-linux-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="a3e07-208">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="a3e07-208">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="a3e07-209">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="a3e07-209">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="a3e07-210">(Une liste complète est disponible dans la documentation [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="a3e07-210">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<containerSettings>` | <span data-ttu-id="a3e07-211">Spécifie les propriétés qui contiennent le nom et l’URL de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="a3e07-211">Specifies the properties which contain the name and URL of your container.</span></span> |
| `<appSettings>` | <span data-ttu-id="a3e07-212">Spécifie des paramètres uniques que Maven utilisera lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a3e07-212">Specifies any unique settings for Maven to use when deploying your web app to Azure.</span></span> <span data-ttu-id="a3e07-213">Dans cet exemple, un élément `<property>` contient une paire nom/valeur d’éléments enfants qui spécifie le port pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a3e07-213">In this example, a `<property>` element contains a name/value pair of child elements that specify the port for your app.</span></span> |

> [!NOTE]
>
> <span data-ttu-id="a3e07-214">Les paramètres de modification du numéro de port fournis dans cet exemple sont nécessaires uniquement lorsque vous modifiez le port à partir de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="a3e07-214">The settings to change the port number in this example are only necessary when you are changing the port from the default.</span></span>
>

1. <span data-ttu-id="a3e07-215">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-215">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="a3e07-216">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="a3e07-216">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="a3e07-217">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="a3e07-217">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="a3e07-218">Si la région que vous spécifiez dans l’élément `<region>` de votre fichier *pom.xml* n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un message d’erreur similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a3e07-218">If the region which you specify in the `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar to the following example:</span></span>
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
> <span data-ttu-id="a3e07-219">Dans ce cas, vous pouvez spécifier une autre région et ré-exécuter la commande Maven pour déployer votre application.</span><span class="sxs-lookup"><span data-stu-id="a3e07-219">If this happens, you can specify another region and re-run the Maven command to deploy your application.</span></span>
>
>

<span data-ttu-id="a3e07-220">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="a3e07-220">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="a3e07-221">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="a3e07-221">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="a3e07-223">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="a3e07-223">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

## <a name="next-steps"></a><span data-ttu-id="a3e07-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a3e07-225">Next steps</span></span>

<span data-ttu-id="a3e07-226">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a3e07-226">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="a3e07-227">[Maven Plugin for Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="a3e07-227">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="a3e07-228">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="a3e07-228">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="a3e07-229">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a3e07-229">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="a3e07-230">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="a3e07-230">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="a3e07-231">[Plug-in Docker pour Maven]</span><span class="sxs-lookup"><span data-stu-id="a3e07-231">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
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
