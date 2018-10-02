---
title: CI/CD pour les applications MicroProfile utilisant Azure DevOps
description: Découvrez comment configurer un cycle de mise en production CI/CD pour déployer une application MicroProfile vers une application web Azure pour l’instance des conteneurs à l’aide d’Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506437"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a><span data-ttu-id="8fa28-103">CI/CD pour les applications MicroProfile utilisant Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="8fa28-103">CI/CD for MicroProfile applications using Azure DevOps</span></span>

<span data-ttu-id="8fa28-104">Ce didacticiel explique comment les développeurs Java EE peuvent facilement configurer un cycle de mise en production CI/CD pour déployer leurs applications [MicroProfile](http://microprofile.io) vers une application web Azure pour les conteneurs à l’aide de Azure DevOps (anciennement nommé VSTS).</span><span class="sxs-lookup"><span data-stu-id="8fa28-104">This tutorial will show how Java EE developers can easily setup a CI/CD release cycle to deploy their [MicroProfile](http://microprofile.io) applications to an Azure Web App for Containers using Azure DevOps (formally known as VSTS).</span></span>  <span data-ttu-id="8fa28-105">Dans cet exemple, nous allons utiliser une application MicroProfile qui utilise un [Payara Micro](https://www.payara.fish/payara_micro) en tant qu’image de base.</span><span class="sxs-lookup"><span data-stu-id="8fa28-105">In this example, we’ll be using a MicroProfile application that uses a [Payara Micro](https://www.payara.fish/payara_micro) as a base image.</span></span>   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
<span data-ttu-id="8fa28-106">Nous allons commencer le processus de conteneurisation Azure DevOps en générant une image Docker et en envoyant l’image conteneur vers un registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa28-106">We will start the Azure DevOps containerize process by building a Docker image and pushing the container image to an Azure Container Register.</span></span>  <span data-ttu-id="8fa28-107">Puis terminez avec un pipeline de mise en production DevOps de Azure pour déployer l’image conteneur vers une application Web.</span><span class="sxs-lookup"><span data-stu-id="8fa28-107">Then complete with a Azure DevOps release pipeline to deploy the container image to a Web App.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fa28-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="8fa28-108">Prerequisites</span></span>
- <span data-ttu-id="8fa28-109">Copiez et enregistrez l’URL Git à partir de [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span><span class="sxs-lookup"><span data-stu-id="8fa28-109">Copy and save the Git url from [Github](https://github.com/Azure-Samples/microprofile-hello-azure)</span></span>
- <span data-ttu-id="8fa28-110">Inscrivez-vous ou connectez-vous à votre compte [Azure DevOps](https://dev.azure.com)</span><span class="sxs-lookup"><span data-stu-id="8fa28-110">Register or Log into your [Azure DevOps](https://dev.azure.com) account</span></span>
- <span data-ttu-id="8fa28-111">Créez un nouveau [projet Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) et utilisez l’URL Git ci-dessus pour **importer un référentiel**</span><span class="sxs-lookup"><span data-stu-id="8fa28-111">Create a new [Azure DevOps project](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) and use the above Git url to **import a repository**</span></span>
- <span data-ttu-id="8fa28-112">Créez un [Registre de conteneurs Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span><span class="sxs-lookup"><span data-stu-id="8fa28-112">Create an [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry) (ACR)</span></span>
- <span data-ttu-id="8fa28-113">Créez une application web Azure pour le conteneur</span><span class="sxs-lookup"><span data-stu-id="8fa28-113">Create an Azure Web App for Container</span></span>
> [!NOTE]
>
> <span data-ttu-id="8fa28-114">Sélectionnez « Démarrage rapide » dans les réglages du conteneur lors de la configuration de l’instance de l’application web</span><span class="sxs-lookup"><span data-stu-id="8fa28-114">Select "Quickstart" in the Container Settings when provisioning the Web App instance</span></span>


## <a name="create-a-build-definition"></a><span data-ttu-id="8fa28-115">Créez une définition de build</span><span class="sxs-lookup"><span data-stu-id="8fa28-115">Create a Build definition</span></span>

<span data-ttu-id="8fa28-116">La définition de build dans Azure DevOps exécute automatiquement toutes les tâches dans la build à chaque validation dans une application source Java EE.</span><span class="sxs-lookup"><span data-stu-id="8fa28-116">The build definition in Azure DevOps automatically executes all the tasks in the build each time there’s a commit in Java EE application source application.</span></span>  <span data-ttu-id="8fa28-117">Dans cet exemple, Azure DevOps utilisera Maven pour générer le projet Java MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="8fa28-117">In this example, Azure DevOps will use Maven to build the Java MicroProfile project.</span></span>

1. <span data-ttu-id="8fa28-118">Cliquez sur l’onglet « Build et Mise en production » en haut la page de votre projet Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="8fa28-118">Click on the "Build and Release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="8fa28-119">Ensuite, sélectionnez le lien **Builds**</span><span class="sxs-lookup"><span data-stu-id="8fa28-119">Then, select the **Builds** link</span></span> 

<img src="media/VSTS/Buid-and-Release1.png">

2. <span data-ttu-id="8fa28-120">Cliquez sur le bouton **Nouveau Pipeline**, puis **Continuer** pour commencer à définir vos tâches de build</span><span class="sxs-lookup"><span data-stu-id="8fa28-120">Click on the **New Pipeline** button, and then **Continue** to start defining your build tasks</span></span>
3. <span data-ttu-id="8fa28-121">Sélectionnez « Maven » dans la liste des modèles, puis cliquez sur le bouton **Appliquer** pour générer votre projet Java</span><span class="sxs-lookup"><span data-stu-id="8fa28-121">Select "Maven" from the list of templates, then click on the **Apply** button to build your Java project</span></span>
4. <span data-ttu-id="8fa28-122">Utilisez le menu déroulant du champ Pool d’agent pour sélectionner l’option **Aperçu de l’hébergement Linux**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-122">Use the drop-down menu for the Agent pool field to select **Hosted Linux Preview** option.</span></span>
> [!NOTE]
>
> <span data-ttu-id="8fa28-123">Cela indique à Azure DevOps, quel serveur build utiliser.</span><span class="sxs-lookup"><span data-stu-id="8fa28-123">This informs Azure DevOps which build server to use.</span></span>  <span data-ttu-id="8fa28-124">Vous pouvez utiliser votre propre serveur de build personnalisée</span><span class="sxs-lookup"><span data-stu-id="8fa28-124">You can use your private customized build server</span></span>

5. <span data-ttu-id="8fa28-125">Pour configurer votre build pour une intégration continue, sélectionnez l’onglet **Déclencheurs** et cochez la case **Autoriser l’intégration continue**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-125">To configure your build for continuous integration, select the **Triggers** tab and check the **Enable continuous integration** checkbox.</span></span>  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. <span data-ttu-id="8fa28-126">Sélectionnez l’onglet **Tâches** pour revenir à la page de pipeline de build principale</span><span class="sxs-lookup"><span data-stu-id="8fa28-126">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
7. <span data-ttu-id="8fa28-127">Sélectionnez l’option **Sauvegarder** dans le menu déroulant **Enregistrer et mettre en file d'attente**</span><span class="sxs-lookup"><span data-stu-id="8fa28-127">Use the **Save & queue** drop-down menu to select the **Save** option</span></span>
 

## <a name="create-a-docker-build-image"></a><span data-ttu-id="8fa28-128">Générez une image de build Docker</span><span class="sxs-lookup"><span data-stu-id="8fa28-128">Create a Docker Build Image</span></span>

<span data-ttu-id="8fa28-129">Dans cette tâche, Azure DevOps utilise un fichier Docker avec une image de base Payara Micro pour générer une image Docker.</span><span class="sxs-lookup"><span data-stu-id="8fa28-129">In this task, Azure DevOps uses a Dockerfile with a base image from Payara Micro to create a Docker image.</span></span>  

1. <span data-ttu-id="8fa28-130">Sélectionnez l’onglet **Tâches** pour revenir à la page de pipeline de build principale</span><span class="sxs-lookup"><span data-stu-id="8fa28-130">Select the **Tasks** tab to return back to the main build pipeline page</span></span>
2. <span data-ttu-id="8fa28-131">Cliquez sur l’icône **+** pour ajouter une nouvelle tâche à la définition de build</span><span class="sxs-lookup"><span data-stu-id="8fa28-131">Click on the **+** icon to add new task to the build definition</span></span>
 
<img src="media/VSTS/Tasks-add4.png">
 
3. <span data-ttu-id="8fa28-132">Sélectionnez « Docker » dans la liste des modèles, puis cliquez sur le bouton **Ajouter**</span><span class="sxs-lookup"><span data-stu-id="8fa28-132">Select "Docker" from the list of templates, then click on the **Add** button</span></span>
4. <span data-ttu-id="8fa28-133">Saisissez un nom de description pour le champ **Nom d'affichage**</span><span class="sxs-lookup"><span data-stu-id="8fa28-133">Enter a description name for the **Display name** field</span></span>
5. <span data-ttu-id="8fa28-134">Vérifiez que le **Registre de conteneurs Azure** est sélectionné dans le menu déroulant de l’onglet **Type de registre de conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-134">Verify that **Azure Container Registry** is selected in the drop-down menu for **Container registry type**.</span></span>
> [!NOTE]
>
>  <span data-ttu-id="8fa28-135">Si vous utilisez Docker Hub ou un autre registre, sélectionnez « Registre de conteneurs » à la place.</span><span class="sxs-lookup"><span data-stu-id="8fa28-135">If you are using Docker Hub or another registry, select "Container Registry" instead.</span></span>  <span data-ttu-id="8fa28-136">Cliquez ensuite sur le bouton « + Nouveau » pour fournir les informations d’identification et de connexion de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="8fa28-136">Then click on the "+ New" button to provide the credentials and connection information for it.</span></span> <span data-ttu-id="8fa28-137">Passez ensuite à la section des commandes pour continuer.</span><span class="sxs-lookup"><span data-stu-id="8fa28-137">Then skip to the Commands section to continue.</span></span>

6. <span data-ttu-id="8fa28-138">Dans la section **Abonnement Azure**, utilisez le menu déroulant pour sélectionner votre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa28-138">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>  <span data-ttu-id="8fa28-139">Cliquez ensuite sur le bouton **Autoriser**</span><span class="sxs-lookup"><span data-stu-id="8fa28-139">Then click on the **Authorize** button</span></span>
7. <span data-ttu-id="8fa28-140">Dans le menu déroulant du **Registre de conteneurs Azure**, sélectionnez le registre de conteneurs que vous avez créé avec Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa28-140">In the **Azure container registry** drop-down menu, select registry name you created in Azure.</span></span>
8. <span data-ttu-id="8fa28-141">Vérifiez que l’option **build** est sélectionnée dans le menu déroulant des **Commandes**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-141">Verify that **build** option is selected in the **Command** drop-down menu.</span></span>
9. <span data-ttu-id="8fa28-142">Pour le **fichier Docker**, cliquez sur l’icône du menu de navigation à côté de la zone de texte pour sélectionner le fichier Docker dans le projet github.</span><span class="sxs-lookup"><span data-stu-id="8fa28-142">For the **Dockerfile**, click on the path navigation icon next to the textbox to select the Dockerfile from the github project.</span></span>  <span data-ttu-id="8fa28-143">Cliquez ensuite sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-143">Then click the **OK** button.</span></span>

<img src="media/VSTS/Dockerfile5.png">

10. <span data-ttu-id="8fa28-144">Sous le **Nom de l’Image**, cochez la case **Inclure la dernière balise**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-144">Under the **Image name**, check the **Include latest tag** checkbox.</span></span> 
11. <span data-ttu-id="8fa28-145">Sélectionnez l’option **Sauvegarder** dans le menu déroulant **Enregistrer et mettre en file d'attente**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-145">Use the **Save & queue** drop-down menu to select the **Save** option.</span></span>

## <a name="push-docker-image-to-acr"></a><span data-ttu-id="8fa28-146">Envoyez l’image Docker à l’ACR</span><span class="sxs-lookup"><span data-stu-id="8fa28-146">Push Docker Image to ACR</span></span>

<span data-ttu-id="8fa28-147">Dans cette tâche, Azure DevOps enverra l’image docker à votre Registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa28-147">In this task, Azure DevOps will push the docker image to your Azure Container Registry.</span></span>  <span data-ttu-id="8fa28-148">Cela sera utilisé pour exécuter l’application API de MicroProfile en tant qu’application web Java conteneurisée.</span><span class="sxs-lookup"><span data-stu-id="8fa28-148">This will be used to run the MicroProfile API application as a containerized Java web app.</span></span>

1. <span data-ttu-id="8fa28-149">Puisque nous utilisons Docker dans Azure DevOps, vous pouvez créer un nouveau modèle de Docker en répétant les étapes 1 à 7 ci-dessus dans la section **Créer une image de build Docker**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-149">Since we are using Docker in Azure DevOps, create a new Docker template by repeating steps 1 - 7 above in the **Create a Docker Build Image** section.</span></span>
2. <span data-ttu-id="8fa28-150">Sélectionnez **envoyer (push)** dans le menu déroulant **Commande**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-150">Select **push** in the **Command** drop-down menu.</span></span>
3. <span data-ttu-id="8fa28-151">Cliquez sur l’onglet **Enregistrer et mettre en file d'attente**, puis sélectionnez l’option **Enregistrer et mettre en file d'attente**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-151">Click on the **Save & queue** tab, then select **Save & queue** option.</span></span>
4. <span data-ttu-id="8fa28-152">Vérifiez que l’option **Aperçu de l’hébergement Linux** est sélectionnée dans le pool d’agents de la fenêtre indépendante.</span><span class="sxs-lookup"><span data-stu-id="8fa28-152">Verify that the **Hosted Linux Preview** is select for the Agent pool on the pop-up window.</span></span>  <span data-ttu-id="8fa28-153">Cliquez ensuite sur le bouton **Enregistrer et mettre en file d’attente**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-153">Then click on the **Save & queue** button.</span></span>
5. <span data-ttu-id="8fa28-154">Cliquez sur le numéro de build pour vérifier que le pipeline de build du projet Java s’est effectué correctement.</span><span class="sxs-lookup"><span data-stu-id="8fa28-154">Click on the build number to verify that the build pipeline for the Java project completed successfully.</span></span>

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a><span data-ttu-id="8fa28-155">Créez une définition de mise en production pour une application Java</span><span class="sxs-lookup"><span data-stu-id="8fa28-155">Create a release definition for a Java app</span></span>

<span data-ttu-id="8fa28-156">Le pipeline de mise en production dans Azure DevOps déclenche automatiquement le déploiement d’artefacts de build vers un environnement cible comme Azure dès que le processus de build s’effectue correctement.</span><span class="sxs-lookup"><span data-stu-id="8fa28-156">The release pipeline in Azure DevOps automatically triggers the deployment of build artifacts to a target environment like Azure as soon as the Build process completes successfully.</span></span>   <span data-ttu-id="8fa28-157">Le pipeline de mise en production peut être créé pour les environnements de développement, de test, de mises en lots ou de production.</span><span class="sxs-lookup"><span data-stu-id="8fa28-157">The release pipeline can be created for dev, test, staging or production environments.</span></span>

1. <span data-ttu-id="8fa28-158">Cliquez sur l’onglet « Build et Mise en production » en haut la page de votre projet Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="8fa28-158">Click on the "Build and release" tab on top your Azure DevOps project page.</span></span>  <span data-ttu-id="8fa28-159">Puis, sélectionnez le lien **Mises en production**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-159">Then, select the **Releases** link.</span></span>

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. <span data-ttu-id="8fa28-160">Cliquez sur le bouton «Nouveau pipeline»\*\*</span><span class="sxs-lookup"><span data-stu-id="8fa28-160">Click on the "New pipeline\*\* button</span></span>
3. <span data-ttu-id="8fa28-161">Sélectionnez **Déployer une application Java sur Azure App Service** dans la liste des modèles, puis cliquez sur le bouton **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-161">Select the **Deploy a Java app to Azure App Service** in the list of templates, then click on the **Apply** button.</span></span>

<img src="media/VSTS/deploy-java-template8.png">
 
4. <span data-ttu-id="8fa28-162">Définir un **Nom de la phase** (par exemple, Développement, Test, Mise en lots ou Production).</span><span class="sxs-lookup"><span data-stu-id="8fa28-162">Set a **Stage name** (e.g Dev, Test, Staging or Production).</span></span>  <span data-ttu-id="8fa28-163">Cliquez ensuite sur le bouton **X** pour fermer la fenêtre indépendante</span><span class="sxs-lookup"><span data-stu-id="8fa28-163">Then click on the **X** button to close the pop-up window</span></span>
5. <span data-ttu-id="8fa28-164">Cliquez sur le bouton **+ Ajouter** dans la section Artefacts.</span><span class="sxs-lookup"><span data-stu-id="8fa28-164">Click on the **+ Add** button in the Artifacts section.</span></span>  <span data-ttu-id="8fa28-165">Cela connectera des artefacts issus de la définition de build à cette définition de mise en production.</span><span class="sxs-lookup"><span data-stu-id="8fa28-165">This will link artifacts from the build definition to this release definition.</span></span>  
6. <span data-ttu-id="8fa28-166">Utilisez le menu déroulant pour la **Source (pipeline de build)** pour sélectionner votre définition de build.</span><span class="sxs-lookup"><span data-stu-id="8fa28-166">Use the drop-down menu for the **Source (build pipeline)** to select your build definition.</span></span> <span data-ttu-id="8fa28-167">Puis cliquez sur le bouton **Ajouter** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="8fa28-167">Then click the **Add** button to continue.</span></span>

<img src="media/VSTS/add-artifact9.png">
 
7. <span data-ttu-id="8fa28-168">Cliquez sur l’onglet **Tâches** du pipeline.</span><span class="sxs-lookup"><span data-stu-id="8fa28-168">Click on the **Tasks** tab on the pipeline.</span></span>  <span data-ttu-id="8fa28-169">Sélectionnez ensuite votre nom de la phase.</span><span class="sxs-lookup"><span data-stu-id="8fa28-169">Then, select your stage name.</span></span>
 
<img src="media/VSTS/release-stage10.png">

8. <span data-ttu-id="8fa28-170">Dans la section **Abonnement Azure**, utilisez le menu déroulant pour sélectionner votre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8fa28-170">Use the **Azure subscription** drop-down menu to select your azure subscription ID.</span></span>
9. <span data-ttu-id="8fa28-171">Sélectionnez **Application Linux** dans le menu déroulant **Type d’application**</span><span class="sxs-lookup"><span data-stu-id="8fa28-171">Select **Linux App** from the **App type** drop-down menu</span></span>
10. <span data-ttu-id="8fa28-172">Sélectionnez le nom de l’application Web pour l’instance de conteneur que vous avez créé précédemment dans le menu déroulant **Nom de l’App service**</span><span class="sxs-lookup"><span data-stu-id="8fa28-172">Select the name of the Web App for Container instance you created above in the **App service name** drop-down menu</span></span>
11. <span data-ttu-id="8fa28-173">Saisissez le nom de votre registre de conteneurs Azure dans le champ **Registre ou Espaces de noms**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-173">Enter the name of your azure container registry in the **Registry or Namespaces** field.</span></span>  <span data-ttu-id="8fa28-174">Par exemple **myregistry.azure.io**</span><span class="sxs-lookup"><span data-stu-id="8fa28-174">E.g **myregistry.azure.io**</span></span>
12. <span data-ttu-id="8fa28-175">Saisissez le nom de registre dans le champ **Référentiel**</span><span class="sxs-lookup"><span data-stu-id="8fa28-175">Enter the registry name in the **Repository** field</span></span>
13. <span data-ttu-id="8fa28-176">Cliquez sur **Déployer Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-176">Click on **Deploy Azure App Service**.</span></span>  <span data-ttu-id="8fa28-177">Entrez la balise de l’image de conteneur dans la zone de texte **Balise**</span><span class="sxs-lookup"><span data-stu-id="8fa28-177">Enter the tag for the container image in the **Tag** textbox</span></span> 
14. <span data-ttu-id="8fa28-178">Cliquez sur **Exécuter sur l’agent**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-178">Click on **Run on agent**.</span></span>  <span data-ttu-id="8fa28-179">Sélectionnez **Aperçu de l’hébergement Linux** dans le pool d’agents du menu déroulant</span><span class="sxs-lookup"><span data-stu-id="8fa28-179">Select **Hosted Linux Preview** in the Agent pool drop-down menu</span></span> 

## <a name="setup-environment-variables"></a><span data-ttu-id="8fa28-180">Valeurs des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="8fa28-180">Setup Environment Variables</span></span>

1. <span data-ttu-id="8fa28-181">Cliquez sur l’onglet **Variables**.  Puis cliquez sur le bouton **+ Ajouter** pour définir vos variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="8fa28-181">Click on the **Variables** tab.  Then click on the **+ Add** button to define your environment variables</span></span>
2. <span data-ttu-id="8fa28-182">Ajoutez le nom de variable et les valeurs pour l’url de votre registre de conteneurs, le nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8fa28-182">Add the variable name and values for your container registry url, username and password.</span></span>   <span data-ttu-id="8fa28-183">Par mesure de sécurité, cliquez sur l’icône en forme de verrou pour conserver la valeur du mot de passe masquée.</span><span class="sxs-lookup"><span data-stu-id="8fa28-183">For security, click on the lock icon to keep the password value hidden.</span></span>

<span data-ttu-id="8fa28-184">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="8fa28-184">For example:</span></span>
- <span data-ttu-id="8fa28-185">registry.password</span><span class="sxs-lookup"><span data-stu-id="8fa28-185">registry.password</span></span>
- <span data-ttu-id="8fa28-186">registry.url</span><span class="sxs-lookup"><span data-stu-id="8fa28-186">registry.url</span></span>
- <span data-ttu-id="8fa28-187">registry.username</span><span class="sxs-lookup"><span data-stu-id="8fa28-187">registry.username</span></span>

<img src="media/VSTS/environment-variables12.png">

3. <span data-ttu-id="8fa28-188">Cliquez sur l’onglet **Tâches** pour revenir à la page de définition de pipeline de mise en production principale</span><span class="sxs-lookup"><span data-stu-id="8fa28-188">Click on the **Tasks** tab to return to the main release pipeline definition page</span></span>
4. <span data-ttu-id="8fa28-189">Cliquez sur **Déployer Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="8fa28-189">Click on **Deploy Azure App Service**.</span></span> 
5. <span data-ttu-id="8fa28-190">Agrandissez la section **Application et Paramètres de Configuration**, puis cliquez dans le menu de navigation pour que le champ des **Paramètres de l’application** ajoute une variable d’environnement pour se connecter au registre de conteneurs pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="8fa28-190">Expand the **Application and Configuration Settings** section, then click on the navigation path for the **App Settings** field to add environments variable to connect to the container registry during deployment.</span></span>
6. <span data-ttu-id="8fa28-191">Cliquez sur le bouton \*\* + Ajouter \*\* pour définir les paramètres d’application suivants et affecter les variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="8fa28-191">Click on the \*\* + Add\*\* button to define the following app settings and assign the environment variables</span></span>
- <span data-ttu-id="8fa28-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span><span class="sxs-lookup"><span data-stu-id="8fa28-192">DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)</span></span>
- <span data-ttu-id="8fa28-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span><span class="sxs-lookup"><span data-stu-id="8fa28-193">DOCKER_REGISTRY_SERVER_URL = $(registry.url)</span></span>
- <span data-ttu-id="8fa28-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span><span class="sxs-lookup"><span data-stu-id="8fa28-194">DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)</span></span>

<img src="media/VSTS/environment-variables14.png">
 
7. <span data-ttu-id="8fa28-195">Cliquez sur le bouton **OK** pour continuer</span><span class="sxs-lookup"><span data-stu-id="8fa28-195">Click on the **OK** button to continue</span></span>

## <a name="setup-continious-deployment--deploy-java-application"></a><span data-ttu-id="8fa28-196">Paramétrage du déploiement continu & Déployer l’application Java</span><span class="sxs-lookup"><span data-stu-id="8fa28-196">Setup Continious Deployment & Deploy Java Application</span></span>

1. <span data-ttu-id="8fa28-197">Pour autoriser le déploiement continu, cliquez sur l’onglet **Pipelines**</span><span class="sxs-lookup"><span data-stu-id="8fa28-197">To enable continuous deployment, click the **Pipelines** tab</span></span>
2. <span data-ttu-id="8fa28-198">Dans la section des artefacts, cliquez sur l’icône en forme d’éclair.</span><span class="sxs-lookup"><span data-stu-id="8fa28-198">In the Artifacts section, click on the lightening icon.</span></span>  <span data-ttu-id="8fa28-199">Définissez ensuite le **Déclencheur de déploiement continu** pour l’activer.</span><span class="sxs-lookup"><span data-stu-id="8fa28-199">Then set the **Continuous deployment trigger** to Enabled.</span></span>

<img src="media/VSTS/release-enable-CD.png">
 
3. <span data-ttu-id="8fa28-200">Cliquez sur le bouton **Sauvegarder**, puis le bouton **OK**</span><span class="sxs-lookup"><span data-stu-id="8fa28-200">Click on the **Save** button, then the **OK** button</span></span> 
4. <span data-ttu-id="8fa28-201">Cliquez dans le menu déroulant **+ Mise en production**, puis sélectionnez le lien **Créer une mise en production**</span><span class="sxs-lookup"><span data-stu-id="8fa28-201">Click on the **+ Release** drop-down menu, then select **Create a release** link</span></span>
5. <span data-ttu-id="8fa28-202">Utilisez le menu déroulant **Phases pour modifier le déclencheur d’automatique à manuel**pour sélectionner la case de votre nom de la phase</span><span class="sxs-lookup"><span data-stu-id="8fa28-202">Use the **Stages for a trigger change from automated to manual** drop-down menu to select the checkbox for your stage name</span></span>
6. <span data-ttu-id="8fa28-203">Cliquez sur le bouton **Créer** pour continuer</span><span class="sxs-lookup"><span data-stu-id="8fa28-203">Click the **Create** button to continue</span></span>
7. <span data-ttu-id="8fa28-204">Cliquez sur le numéro de mise en production.</span><span class="sxs-lookup"><span data-stu-id="8fa28-204">Click on the release number.</span></span>  <span data-ttu-id="8fa28-205">Pointez ensuite votre souris sur le nom de la phase et cliquez sur le bouton **Déployer**</span><span class="sxs-lookup"><span data-stu-id="8fa28-205">Then hover your mouse cursor over the stage name and click on the **Deploy** button</span></span>
8. <span data-ttu-id="8fa28-206">Cliquez ensuite sur le bouton **Déployer** dans la fenêtre indépendante pour démarrer le processus de déploiement vers Azure</span><span class="sxs-lookup"><span data-stu-id="8fa28-206">The click on the **Deploy** button on the pop-up window to start the deployment process to Azure</span></span>


## <a name="test-the-java-web-application"></a><span data-ttu-id="8fa28-207">Testez l’application web Java</span><span class="sxs-lookup"><span data-stu-id="8fa28-207">Test the Java Web Application</span></span>
1. <span data-ttu-id="8fa28-208">Exécutez l’url de l’application web dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="8fa28-208">Run the web app url in web browser:</span></span>  
<span data-ttu-id="8fa28-209">https://{nom-de-votre-application}.azurewebsites.net/api/hello</span><span class="sxs-lookup"><span data-stu-id="8fa28-209">https://{your-app-service-name}.azurewebsites.net/api/hello</span></span>

 
<img src="media/VSTS/web-app16.png">

2. <span data-ttu-id="8fa28-210">La page web doit indiquer **Hello Azure !**</span><span class="sxs-lookup"><span data-stu-id="8fa28-210">The web page should say **Hello Azure!**</span></span>
 
<img src="media/VSTS/web-api17.png">
