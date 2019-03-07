---
title: Déployer une application web Hello World s’exécutant dans un conteneur Linux dans le cloud à l’aide d’Azure Toolkit for Eclipse
description: Exécutez une application web Hello World de base dans un conteneur Linux et déployez-la dans le cloud à l’aide d’Azure Toolkit for Eclipse.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649245"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="0a3cc-103">Déployer une application web Hello World sur un conteneur Linux dans le cloud à l’aide d’Azure Toolkit for Eclipse</span><span class="sxs-lookup"><span data-stu-id="0a3cc-103">Deploy a Hello World web app to a Linux container in the cloud using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="0a3cc-104">Les conteneurs [Docker] constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="0a3cc-105">En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="0a3cc-106">Azure Toolkit for Eclipse simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités permettant de déployer des conteneurs sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="0a3cc-107">Cet article décrit les étapes à suivre pour créer une application web Hello World de base et la publier dans un conteneur Linux sur Azure à l’aide d’Azure Toolkit for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* <span data-ttu-id="0a3cc-108">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="0a3cc-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0a3cc-109">Pour effectuer les étapes de ce didacticiel, vous devez configurer [Docker] pour exposer le démon sur le port 2375 sans TLS.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="0a3cc-110">Vous pouvez configurer ce paramètre lors de l’installation de Docker ou via le menu des paramètres Docker.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menu des paramètres docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="0a3cc-112">Créer un projet d’application web</span><span class="sxs-lookup"><span data-stu-id="0a3cc-112">Create a new web app project</span></span>

1. <span data-ttu-id="0a3cc-113">Démarrez Eclipse et connectez-vous à votre compte Azure en suivant les étapes de l’article [Instructions de connexion pour Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="0a3cc-113">Start Eclipse and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions) article.</span></span>

1. <span data-ttu-id="0a3cc-114">Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique).</span><span class="sxs-lookup"><span data-stu-id="0a3cc-114">Click the **File** menu, then click **New**, and then click **Dynamic Web Project**.</span></span>
   
   ![Créer un projet][file-new-project]

1. <span data-ttu-id="0a3cc-116">Dans la boîte de dialogue **New Dynamic Web Project** (Nouveau projet web dynamique) spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="0a3cc-116">In the **New Dynamic Web Project** dialog box, specify your project name and location, and then click **Finish**.</span></span>
   
   ![Spécifier le nom du projet][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="0a3cc-118">Créer un Azure Container Registry à utiliser comme registre Docker privé</span><span class="sxs-lookup"><span data-stu-id="0a3cc-118">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="0a3cc-119">Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-119">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0a3cc-120">Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="0a3cc-120">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="0a3cc-121">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-121">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="0a3cc-122">Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créer un registre de conteneurs Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-122">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="0a3cc-123">Cliquez sur l’icône de menu pour **+ Créer une ressource**, cliquez sur **Conteneurs**, puis sur **Registre de conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-123">Click the menu icon for **+ Create a resource**, then click **Containers**, and then click **Container Registry**.</span></span>
   
   ![Créer un registre de conteneurs Azure][create-container-registry-01]

1. <span data-ttu-id="0a3cc-125">Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-125">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurer les paramètres du registre de conteneurs Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="0a3cc-127">Déployer votre application web dans un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="0a3cc-127">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="0a3cc-128">Cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Ajouter la prise en charge Docker**.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-128">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="0a3cc-129">Un fichier Docker est automatiquement créé avec une configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-129">This will automatically create a Docker file with a default configuration.</span></span>

   ![Ajouter la prise en charge Docker][add-docker-support]

1. <span data-ttu-id="0a3cc-131">Une fois que vous avez ajouté la prise en charge Docker, cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Publish to Web App for Containers** (Publier sur Web App pour conteneurs).</span><span class="sxs-lookup"><span data-stu-id="0a3cc-131">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Publish to Web App for Containers**.</span></span>

   ![Publish to Web App for Containers (Publier sur Web App pour conteneurs)][run-on-web-app-for-containers]

1. <span data-ttu-id="0a3cc-133">Quand la boîte de dialogue **Run on Web App for Containers** (Exécuter sur Web App pour conteneurs) s’affiche, entrez les informations demandées :</span><span class="sxs-lookup"><span data-stu-id="0a3cc-133">When the **Run on Web App for Containers** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="0a3cc-134">**Docker File** (Fichier Docker) : spécifie le chemin au fichier Docker créé quand vous avez ajouté la prise en charge Docker à votre projet.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-134">**Docker File**: This specifies the path to the Docker file that was created when you added Docker support to your project.</span></span> 

   * <span data-ttu-id="0a3cc-135">**Container Registry** (Registre de conteneurs) : dans le menu déroulant, choisissez le registre de conteneurs que vous avez créé dans la section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-135">**Container Registry**: Choose the container registry from the drop-down menu that you created in the previous section of this article.</span></span> <span data-ttu-id="0a3cc-136">Les champs **Server URL** (URL du serveur), **Username** (Nom d’utilisateur) et **Password** (Mot de passe) sont renseignés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-136">The fields for **Server URL**, **Username**, and **Password** will be automatically populated.</span></span>

   * <span data-ttu-id="0a3cc-137">**Image and tag** (Image et étiquette) : spécifie le nom de l’image conteneur. Ce nom suit généralement la syntaxe « *registre*.azurecr.io/*nom_app*:latest », où :</span><span class="sxs-lookup"><span data-stu-id="0a3cc-137">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="0a3cc-138">*registre* correspond au registre de conteneurs déterminé dans la section précédente de cet article,</span><span class="sxs-lookup"><span data-stu-id="0a3cc-138">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="0a3cc-139">*nom_app* correspond au nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-139">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="0a3cc-140">**Web App for Container** (Web App pour conteneurs) : choisissez **Use Existing** (Utiliser l’existant) pour déployer votre conteneur dans une application web existante ou **Create New** (Créer) pour créer une application web.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-140">**Web App for Container**: Choose **Use Existing** or **Create New** to specify whether you will deploy your container to an existing web app or create a new web app.</span></span>  <span data-ttu-id="0a3cc-141">Le nom de l’application (**App name**) que vous indiquez sert à générer l’URL de votre application web ; par exemple : *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-141">The **App name** that you specify will create the URL for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   * <span data-ttu-id="0a3cc-142">**Groupe de ressources** : indique si vous utilisez un groupe de ressources existant ou si vous en créez un.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-142">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="0a3cc-143">**App Service Plan** (Plan App Service) : indique si vous utilisez un plan App Service existant ou si vous en créez un.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-143">**App Service Plan**: Specifies whether you will use an existing or create a new app service plan.</span></span> 

   ![Run on Web App for Containers (Exécuter sur Web App pour conteneurs)][run-on-web-app-linux]

1. <span data-ttu-id="0a3cc-145">Quand vous avez terminé de configurer les paramètres ci-dessus, cliquez sur **Exécuter** pour publier votre application web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-145">When you have finished configuring the settings listed above, click **OK** to publish your web app to Azure.</span></span>

1. <span data-ttu-id="0a3cc-146">Une fois votre application web publiée, vous pouvez y accéder à l’aide de l’URL spécifiée précédemment ; par exemple : *wingtiptoys.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-146">After your web app has been published, you can browse to the URL that specifed earlier for your web app; for example: *wingtiptoys.azurewebsites.net*.</span></span>

   ![Accès à votre application web][browsing-to-web-app]

## <a name="next-steps"></a><span data-ttu-id="0a3cc-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a3cc-148">Next steps</span></span>

<span data-ttu-id="0a3cc-149">Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker][Docker] officiel.</span><span class="sxs-lookup"><span data-stu-id="0a3cc-149">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png