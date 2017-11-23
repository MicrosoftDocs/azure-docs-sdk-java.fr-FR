---
title: "Exécuter une application web Hello World dans un conteneur Linux à l’aide du kit de ressources Azure pour IntelliJ"
description: "Découvrez comment créer une application web Hello World basique dans un conteneur Linux, puis comment la publier sur Azure à l’aide du kit de ressources Azure pour IntelliJ."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 2c0bfc581b5bb033f301d5a1e632377442821392
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="run-a-hello-world-web-app-in-a-linux-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="dc3f1-103">Exécuter une application web Hello World dans un conteneur Linux à l’aide du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="dc3f1-103">Run a Hello World web app in a Linux container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="dc3f1-104">Les conteneurs [client Docker] constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-104">[Docker] containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="dc3f1-105">En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="dc3f1-106">Le kit de ressources Azure pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités permettant de déployer des conteneurs sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding features for to deploy containers to Microsoft Azure.</span></span>

<span data-ttu-id="dc3f1-107">Cet article décrit les étapes requises pour créer une application web Hello World basique et la publier dans un conteneur Linux sur Azure à l’aide du kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-107">This article demonstrates the steps that are required to create a basic Hello World web app and publish your web app in a Linux container to Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* <span data-ttu-id="dc3f1-108">Un [client Docker].</span><span class="sxs-lookup"><span data-stu-id="dc3f1-108">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dc3f1-109">Pour effectuer les étapes de ce didacticiel, vous devez configurer [client Docker] pour exposer le démon sur le port 2375 sans TLS.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-109">To complete the steps in this tutorial, you need to configure [Docker] to expose the daemon on port 2375 without TLS.</span></span> <span data-ttu-id="dc3f1-110">Vous pouvez configurer ce paramètre lors de l’installation de Docker ou via le menu des paramètres Docker.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-110">You can configure this setting when installing Docker, or through the Docker settings menu.</span></span>
>
> ![Menu des paramètres docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="dc3f1-112">Créer un projet d’application web</span><span class="sxs-lookup"><span data-stu-id="dc3f1-112">Create a new web app project</span></span>

1. <span data-ttu-id="dc3f1-113">Démarrez IntelliJ et connectez-vous à votre compte Azure en suivant les étapes indiquées dans l’article [Instructions de connexion pour le kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="dc3f1-113">Start IntelliJ and sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for IntelliJ] article.</span></span>

1. <span data-ttu-id="dc3f1-114">Cliquez sur le menu **Fichier**, puis sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-114">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Créer un projet][file-new-project]

1. <span data-ttu-id="dc3f1-116">Dans la boîte de dialogue **New Project**, sélectionnez **Maven**, puis **maven-archetype-webapp**, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-116">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Choisir une application web d’archétype Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="dc3f1-118">Spécifiez les valeurs **GroupId** et **ArtifactId** pour votre application web, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-118">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Spécifier GroupId et ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="dc3f1-120">Personnalisez les paramètres Maven ou acceptez les valeurs par défaut, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-120">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Spécifier les paramètres Maven][maven-options]

1. <span data-ttu-id="dc3f1-122">Spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-122">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Spécifier le nom du projet][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="dc3f1-124">Créer un Azure Container Registry à utiliser comme registre Docker privé</span><span class="sxs-lookup"><span data-stu-id="dc3f1-124">Create an Azure Container Registry to use as a private Docker registry</span></span>

<span data-ttu-id="dc3f1-125">Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-125">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dc3f1-126">Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0][Create Docker Registry using Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="dc3f1-126">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0][Create Docker Registry using Azure CLI].</span></span>
>

1. <span data-ttu-id="dc3f1-127">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-127">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="dc3f1-128">Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créer un registre de conteneurs Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-128">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="dc3f1-129">Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Conteneurs** puis cliquez sur **Registre de conteneurs Azure**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-129">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Créer un registre de conteneurs Azure][AR01]

1. <span data-ttu-id="dc3f1-131">Quand la page d’informations pour le modèle de registre de conteneurs Azure s’affiche, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-131">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Créer un registre de conteneurs Azure][AR02]

1. <span data-ttu-id="dc3f1-133">Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-133">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. <span data-ttu-id="dc3f1-135">Une fois votre registre de conteneurs créé, accédez à celui-ci dans le portail Azure puis cliquez sur **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-135">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="dc3f1-136">Notez le nom d’utilisateur et le mot de passe pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-136">Take note of the username and password for the next steps.</span></span>

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a><span data-ttu-id="dc3f1-138">Déployer votre application web dans un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="dc3f1-138">Deploy your web app in a Docker container</span></span>

1. <span data-ttu-id="dc3f1-139">Cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Ajouter la prise en charge Docker**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-139">Right-click your project in the project explorer, choose **Azure**, and then click **Add Docker Support**.</span></span>

   <span data-ttu-id="dc3f1-140">Un fichier Docker est automatiquement créé avec une configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-140">This will automatically create a Docker file with a default configuration.</span></span>

   ![Ajouter la prise en charge Docker][add-docker-support]

1. <span data-ttu-id="dc3f1-142">Une fois que vous avez ajouté la prise en charge Docker, cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Exécuter sur l’application web (Linux)**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-142">After you have added Docker support, right-click your project in the project explorer, choose **Azure**, and then click **Run on Web App (Linux)**.</span></span>

   ![Exécuter sur l’application web (Linux)][run-on-web-app-linux]

1. <span data-ttu-id="dc3f1-144">Quand la boîte de dialogue **Exécuter sur l’application web (Linux)** s’affiche, entrez les informations requises :</span><span class="sxs-lookup"><span data-stu-id="dc3f1-144">When the **Run on Web App (Linux)** dialog box is displayed, fill in the requisite information:</span></span>

   * <span data-ttu-id="dc3f1-145">**Nom** : spécifie le nom convivial qui s’affiche dans le kit de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-145">**Name**: This specifies the friendly name which is displayed in the Azure Toolkit.</span></span> 

   * <span data-ttu-id="dc3f1-146">**URL du serveur** : spécifie l’URL de votre registre de conteneurs déterminé dans la section précédente de cet article ; généralement elle utilise la syntaxe suivante : « *registre*.azurecr.io ».</span><span class="sxs-lookup"><span data-stu-id="dc3f1-146">**Server URL**: This specifies the URL for your container registry from the previous section of this article; typically this will use the following syntax: "*registry*.azurecr.io".</span></span> 

   * <span data-ttu-id="dc3f1-147">**Nom d’utilisateur** et **Mot de passe** : spécifie les clés d’accès de votre registre de conteneur déterminé dans la section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-147">**Username** and **Password**: Specifies the access keys for your container registry from the previous section of this article.</span></span> 

   * <span data-ttu-id="dc3f1-148">**Image et étiquette** : spécifie le nom d’image du conteneur ; généralement il utilise la syntaxe suivante : « *registre*.azurecr.io/*nom_app*:latest », où :</span><span class="sxs-lookup"><span data-stu-id="dc3f1-148">**Image and tag**: Specifies the container image name; typically this will use the following syntax: "*registry*.azurecr.io/*appname*:latest", where:</span></span> 
      * <span data-ttu-id="dc3f1-149">*registre* correspond au registre de conteneurs déterminé dans la section précédente de cet article,</span><span class="sxs-lookup"><span data-stu-id="dc3f1-149">*registry* is your container registry from the previous section of this article</span></span> 
      * <span data-ttu-id="dc3f1-150">*nom_app* correspond au nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-150">*appname* is the name of your web app</span></span> 

   * <span data-ttu-id="dc3f1-151">**Utiliser une application web existante** ou **Créer une application web** : spécifie si vous déployez votre conteneur dans une application web existante ou si vous en créez une.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-151">**Use Existing Web App** or **Create New Web App**: Specifies whether you will deploy your container to an existing web app or create a new web app.</span></span> 

   * <span data-ttu-id="dc3f1-152">**Groupe de ressources** : spécifie si vous utilisez un groupe de ressources existant ou si vous en créez un.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-152">**Resource Group**: Specifies whether you will use an existing or create a new resource group.</span></span> 

   * <span data-ttu-id="dc3f1-153">**Plan App Service** : spécifie si vous utilisez un plan App Service existant ou si vous en créez un.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-153">**App Service Plan**: Specifies whether you willuse an existing or create a new app service plan.</span></span> 

1. <span data-ttu-id="dc3f1-154">Quand vous avez terminé de configurer les paramètres indiqués ci-dessus, cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-154">When you have finished configuring the settings listed above, click **Run**.</span></span>

   ![Créer une application web][create-web-app]

1. <span data-ttu-id="dc3f1-156">Une fois que vous avez publié votre application web, vos paramètres sont enregistrés comme valeur par défaut, et vous pouvez exécuter votre application sur Azure en cliquant sur l’icône en forme de flèche verte dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-156">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="dc3f1-157">Vous pouvez modifier ces paramètres en cliquant sur le menu déroulant de votre application web, puis sur **Modifier les configurations**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-157">You can modify these settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Modifier les configurations][edit-configuration-menu]

1. <span data-ttu-id="dc3f1-159">Quand la boîte de dialogue **ExécRun/Debug Configurations** s’affiche, vous pouvez modifier les paramètres par défaut de votre choix. Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-159">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Boîte de dialogue Edit configuration][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="dc3f1-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dc3f1-161">Next steps</span></span>

<span data-ttu-id="dc3f1-162">Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker][client Docker] officiel.</span><span class="sxs-lookup"><span data-stu-id="dc3f1-162">For additional resources for Docker, see the official [Docker website][Docker].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[portail Azure]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[client Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
