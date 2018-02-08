---
title: "Créer une application web Hello World pour Azure à l’aide de l’ancien kit de ressources pour IntelliJ"
description: "Ce didacticiel vous montre comment utiliser la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour IntelliJ pour créer une application web Hello World pour Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: ebe98a604b52dc9a4b5a47cbf65a4c68a5c86fe3
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a><span data-ttu-id="89ffd-103">Créer une application web Hello World pour Azure à l’aide de l’ancien kit de ressources pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="89ffd-103">Create a Hello World web app for Azure using the legacy toolkit for IntelliJ</span></span>

<span data-ttu-id="89ffd-104">Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide de la version 3.0.6 (ou ultérieure) du [Kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="89ffd-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="89ffd-105">Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour Eclipse], consultez [Créer une application web pour Azure à l’aide d’Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="89ffd-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="89ffd-106">Le Kit de ressources Azure pour IntelliJ a été mis à jour en août 2017 avec un flux de travail différent.</span><span class="sxs-lookup"><span data-stu-id="89ffd-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="89ffd-107">Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="89ffd-107">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="89ffd-108">Si vous utilisez la version 3.0.7 (ou antérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans IntelliJ][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="89ffd-108">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ][Updated Version].</span></span>
>

<span data-ttu-id="89ffd-109">À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="89ffd-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Version préliminaire de l’application Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="89ffd-111">Créer un projet d’application web</span><span class="sxs-lookup"><span data-stu-id="89ffd-111">Create a new web app project</span></span>

1. <span data-ttu-id="89ffd-112">Démarrez IntelliJ et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="89ffd-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="89ffd-113">Cliquez sur le menu **File**, sur **New**, puis sur **Project**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Fichier Nouveau Projet][02]

2. <span data-ttu-id="89ffd-115">Dans la boîte de dialogue **New Project**, sélectionnez **Java**, **Web Application**, puis cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-115">In the **New Project** dialog box, select **Java**, then **Web Application**, and then click **New** to add a Project SDK.</span></span>
   
   ![Boîte de dialogue Nouveau projet][03a]
   
3. <span data-ttu-id="89ffd-117">Dans Sélection du répertoire de base pour la boîte de dialogue JDK, sélectionnez le dossier où est installé votre JDK, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-117">In the Select Home Directory for JDK dialog box, select the folder where your JDK is installed, and then click **OK**.</span></span> <span data-ttu-id="89ffd-118">Cliquez sur **Suivant** dans la boîte de dialogue Nouveau projet pour continuer.</span><span class="sxs-lookup"><span data-stu-id="89ffd-118">Click **Next** in the New Project dialog box to continue.</span></span>
   
   ![Spécifiez le répertoire de base du JDK][03b]

4. <span data-ttu-id="89ffd-120">Pour les besoins de ce didacticiel, nommez le projet **Java-Web-App-On-Azure**, puis cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="89ffd-120">For purposes of this tutorial, name the project **Java-Web-App-On-Azure**, and then click **Finish**.</span></span>
   
   ![Boîte de dialogue Nouveau projet][04]

5. <span data-ttu-id="89ffd-122">Dans l’affichage de l’explorateur de projets d’IntelliJ, développez **Java-Web-App-On-Azure**, puis développez **web** et double-cliquez sur **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-122">Within IntelliJ's Project Explorer view, expand **Java-Web-App-On-Azure**, then expand **web**, and then double-click **index.jsp**.</span></span>
   
   ![Page Ouvrir l’index][05c]

6. <span data-ttu-id="89ffd-124">Quand votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="89ffd-124">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="89ffd-125">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="89ffd-125">within the existing `<body>` element.</span></span> <span data-ttu-id="89ffd-126">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="89ffd-126">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. <span data-ttu-id="89ffd-127">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="89ffd-127">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="89ffd-128">Déployer votre application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="89ffd-128">Deploy your web app to Azure</span></span>

<span data-ttu-id="89ffd-129">Vous pouvez déployer une application web Java sur Azure de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="89ffd-129">There are several ways by which you can deploy a Java web app to Azure.</span></span> <span data-ttu-id="89ffd-130">Ce didacticiel décrit l’une des plus simples : votre application est déployée sur un conteneur d’application web Azure ; ainsi, aucun type de projet spécifique ni outil supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="89ffd-130">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="89ffd-131">Le JDK et le logiciel du conteneur web vous étant fournis par Azure, vous n’avez pas besoin de charger les vôtres ; vous devez uniquement être en possession de votre application web Java.</span><span class="sxs-lookup"><span data-stu-id="89ffd-131">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="89ffd-132">Ainsi, le processus de publication de votre application ne prend que quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="89ffd-132">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

<span data-ttu-id="89ffd-133">Avant de publier votre application, vous devez d’abord configurer vos paramètres de module.</span><span class="sxs-lookup"><span data-stu-id="89ffd-133">Before you publish your application, you first need to configure your module settings.</span></span> <span data-ttu-id="89ffd-134">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89ffd-134">To do so, use the following steps:</span></span>

1. <span data-ttu-id="89ffd-135">Dans l’explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur le projet **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="89ffd-135">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="89ffd-136">Quand le menu contextuel s’affiche, cliquez sur **Open Module Settings**(Ouvrir les paramètres du module).</span><span class="sxs-lookup"><span data-stu-id="89ffd-136">When the context menu appears, click **Open Module Settings**.</span></span>

   ![Ouvrir les paramètres du module][05a]

2. <span data-ttu-id="89ffd-138">Lorsque la boîte de dialogue Structure de projet s’affiche :</span><span class="sxs-lookup"><span data-stu-id="89ffd-138">When the Project Structure dialog box appears:</span></span>

   <span data-ttu-id="89ffd-139">a.</span><span class="sxs-lookup"><span data-stu-id="89ffd-139">a.</span></span> <span data-ttu-id="89ffd-140">Cliquez sur **Artefacts** dans la liste des **Paramètres du projet**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-140">Click **Artifacts** in the list of **Project Settings**.</span></span>

   <span data-ttu-id="89ffd-141">b.</span><span class="sxs-lookup"><span data-stu-id="89ffd-141">b.</span></span> <span data-ttu-id="89ffd-142">Modifiez le nom de l’artefact dans la zone **Nom** pour qu’il ne contienne pas d’espaces blancs ou des caractères spéciaux. Cela est nécessaire dans la mesure où le nom est utilisé dans l’URI.</span><span class="sxs-lookup"><span data-stu-id="89ffd-142">Change the artifact name in the **Name** box so that it doesn't contain whitespace or special characters; this is necessary since the name will be used in the Uniform Resource Identifier (URI).</span></span>

   <span data-ttu-id="89ffd-143">c.</span><span class="sxs-lookup"><span data-stu-id="89ffd-143">c.</span></span> <span data-ttu-id="89ffd-144">Définissez le **Type** sur **Web Application: Archive** (Application Web : Archive).</span><span class="sxs-lookup"><span data-stu-id="89ffd-144">Change the **Type** to **Web Application: Archive**.</span></span>

   <span data-ttu-id="89ffd-145">d.</span><span class="sxs-lookup"><span data-stu-id="89ffd-145">d.</span></span> <span data-ttu-id="89ffd-146">Cliquez sur **OK** pour fermer la boîte de dialogue Structure de projet.</span><span class="sxs-lookup"><span data-stu-id="89ffd-146">Click **OK** to close the Project Structure dialog box.</span></span>

   ![Ouvrir les paramètres du module][05b]

<span data-ttu-id="89ffd-148">Lorsque vous avez configuré vos paramètres de module, vous pouvez publier votre application dans Azure à l’aide de la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="89ffd-148">When you have configured your module settings, you can publish your application to Azure by using the following steps:</span></span>

1. <span data-ttu-id="89ffd-149">Dans l’explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur le projet **Java-Web-App-On-Azure** .</span><span class="sxs-lookup"><span data-stu-id="89ffd-149">In IntelliJ's Project Explorer, right-click the **Java-Web-App-On-Azure** project.</span></span> <span data-ttu-id="89ffd-150">Quand le menu contextuel apparaît, sélectionnez **Azure**, puis cliquez sur **Publish as Azure Web App...** (Publier comme application web Azure...).</span><span class="sxs-lookup"><span data-stu-id="89ffd-150">When the context menu appears, select **Azure**, and then click **Publish as Azure Web App...**</span></span>
   
   ![Menu contextuel de publication Azure][06]

2. <span data-ttu-id="89ffd-152">Si vous n’êtes pas encore connecté à Azure à partir d’IntelliJ, vous êtes invité à vous connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="89ffd-152">If you have not already signed in to Azure from IntelliJ, you will be prompted to sign in to your Azure account.</span></span> <span data-ttu-id="89ffd-153">(Si vous avez plusieurs comptes Azure, certaines des invites du processus de connexion peuvent s’afficher plusieurs fois, même si elles semblent être identiques.</span><span class="sxs-lookup"><span data-stu-id="89ffd-153">(If you have multiple Azure accounts, some of the prompts during the sign-in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="89ffd-154">Dans ce cas, continuez à suivre les instructions de connexion.)</span><span class="sxs-lookup"><span data-stu-id="89ffd-154">When this happens, continue to follow the sign-in instructions.)</span></span>
   
   ![Boîte de dialogue de connexion à Azure][07]

3. <span data-ttu-id="89ffd-156">Une fois que vous êtes connecté à votre compte Azure, la boîte de dialogue **Gérer les abonnements** affiche la liste des abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="89ffd-156">After you have successfully signed in to your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="89ffd-157">Si plusieurs abonnements sont répertoriés et que vous ne souhaitez utiliser qu’une partie d’entre eux, vous pouvez éventuellement désélectionner ceux qui ne vous intéressent pas. Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-157">(If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the subscriptions you don't want to use.) When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Gérer les abonnements][08]

4. <span data-ttu-id="89ffd-159">Quand la boîte de dialogue **Deploy to Azure Web App Container** (Déployer sur le conteneur d’application web Azure) s’affiche, elle présente tous les conteneurs d’application web déjà créés ; si vous n’avez pas créé de conteneur, la liste est vide.</span><span class="sxs-lookup"><span data-stu-id="89ffd-159">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Conteneurs d’applications][09]

5. <span data-ttu-id="89ffd-161">Si vous n’avez pas déjà créé de conteneur d’application web Azure ou que vous souhaitez publier votre application dans un nouveau conteneur, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="89ffd-161">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="89ffd-162">Sinon, sélectionnez un conteneur d’application web existant et passez à l’étape 6 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="89ffd-162">Otherwise, select an existing Web App Container and skip to step 6 below.</span></span>
   
   <span data-ttu-id="89ffd-163">a.</span><span class="sxs-lookup"><span data-stu-id="89ffd-163">a.</span></span> <span data-ttu-id="89ffd-164">Cliquez sur le signe **+**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-164">Click the **+** sign.</span></span>
      
      ![Ajouter un conteneur d’application][10]

   <span data-ttu-id="89ffd-166">b.</span><span class="sxs-lookup"><span data-stu-id="89ffd-166">b.</span></span> <span data-ttu-id="89ffd-167">La boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web) s’affiche, que nous allons utiliser au cours des prochaines étapes.</span><span class="sxs-lookup"><span data-stu-id="89ffd-167">The **New Web App Container** dialog box will be displayed, which will be used for the next several steps.</span></span>
      
      ![Nouveau conteneur d’application][11a]
   
   <span data-ttu-id="89ffd-169">c.</span><span class="sxs-lookup"><span data-stu-id="89ffd-169">c.</span></span> <span data-ttu-id="89ffd-170">Entrez un **nom DNS** pour votre conteneur d’application web ; celui-ci constitue le nom DNS feuille de l’URL hôte de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="89ffd-170">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="89ffd-171">Le nom doit être disponible et conforme aux exigences d’affectation de noms pour les applications web Azure.</span><span class="sxs-lookup"><span data-stu-id="89ffd-171">Note that the name must be available and conform to Azure Web App naming requirements.</span></span>

   <span data-ttu-id="89ffd-172">d.</span><span class="sxs-lookup"><span data-stu-id="89ffd-172">d.</span></span> <span data-ttu-id="89ffd-173">Dans le menu déroulant **Web Container** (Conteneur d’application), sélectionnez le logiciel approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="89ffd-173">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="89ffd-174">Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="89ffd-174">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="89ffd-175">Une distribution récente du logiciel sélectionné sera fournie par Azure, et il s’exécutera sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="89ffd-175">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="89ffd-176">e.</span><span class="sxs-lookup"><span data-stu-id="89ffd-176">e.</span></span> <span data-ttu-id="89ffd-177">Dans le menu déroulant **Subscription** (Abonnement), sélectionnez l’abonnement à utiliser pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="89ffd-177">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="89ffd-178">f.</span><span class="sxs-lookup"><span data-stu-id="89ffd-178">f.</span></span> <span data-ttu-id="89ffd-179">Dans le menu déroulant **Resource Group** (Groupe de ressources), sélectionnez le groupe de ressources auquel vous souhaitez associer votre application web.</span><span class="sxs-lookup"><span data-stu-id="89ffd-179">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="89ffd-180">(Les groupes de ressources Azure permettent de regrouper les ressources associées afin de pouvoir, par exemple, les supprimer simultanément.)</span><span class="sxs-lookup"><span data-stu-id="89ffd-180">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="89ffd-181">Vous pouvez sélectionner un groupe de ressources existant (le cas échéant) et passer directement à l’étape G ou suivre les étapes ci-dessous pour créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="89ffd-181">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="89ffd-182">Sélectionnez **&lt;&lt; Créer un groupe de ressources &gt;&gt;** dans le menu déroulant **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-182">Select **&lt;&lt; Create new Resource Group &gt;&gt;** in the **Resource Group** drop-down menu.</span></span>
      * <span data-ttu-id="89ffd-183">La boîte de dialogue **New Resource Group** (Nouveau groupe de ressources) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="89ffd-183">The **New Resource Group** dialog box will be displayed:</span></span>
        
         ![Nouveau groupe de ressources][12]

      * <span data-ttu-id="89ffd-185">Dans la zone de texte **Name**, spécifiez un nom pour votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="89ffd-185">In the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="89ffd-186">Dans le menu déroulant **Region**, sélectionnez l’emplacement de centre de données Azure approprié pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="89ffd-186">In the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="89ffd-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-187">Click **OK**.</span></span>

   <span data-ttu-id="89ffd-188">g.</span><span class="sxs-lookup"><span data-stu-id="89ffd-188">g.</span></span> <span data-ttu-id="89ffd-189">Le menu déroulant **App Service Plan** (Plan de Service d’application) répertorie les plans de service d’application qui sont associés au groupe de ressources que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="89ffd-189">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="89ffd-190">(Un plan App Service spécifie des informations telles que l’emplacement de votre application web, le niveau tarifaire et la taille d’instance de calcul.)</span><span class="sxs-lookup"><span data-stu-id="89ffd-190">(An App Service Plan specifies information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="89ffd-191">Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)</span><span class="sxs-lookup"><span data-stu-id="89ffd-191">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
      <span data-ttu-id="89ffd-192">Vous pouvez sélectionner un plan App Services existant (le cas échéant) et passer directement à l’étape H ou suivre les étapes ci-dessous pour créer un plan App Service :</span><span class="sxs-lookup"><span data-stu-id="89ffd-192">You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following steps to create a new App Service Plan:</span></span>
      
      * <span data-ttu-id="89ffd-193">Sélectionnez **&lt;&lt; Créer un plan App Service&gt;&gt;** dans le menu déroulant **Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-193">Select **&lt;&lt; Create new App Service Plan &gt;&gt;** in the **App Service Plan** drop-down menu.</span></span>
      * <span data-ttu-id="89ffd-194">La boîte de dialogue **New App Service Plan** (Nouveau plan de Service d’application) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="89ffd-194">The **New App Service Plan** dialog box will be displayed:</span></span>
        
         ![Nouveau plan App Service][13]

      * <span data-ttu-id="89ffd-196">Dans la zone de texte **Name**, spécifiez un nom pour votre nouveau plan App Service.</span><span class="sxs-lookup"><span data-stu-id="89ffd-196">In the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="89ffd-197">Dans le menu déroulant **Location**, sélectionnez l’emplacement de centre de données Azure approprié pour le plan.</span><span class="sxs-lookup"><span data-stu-id="89ffd-197">In the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="89ffd-198">Dans le menu déroulant **Pricing Tier**, sélectionnez la tarification appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="89ffd-198">In the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="89ffd-199">À des fins de test, vous pouvez choisir **Free**(Gratuit).</span><span class="sxs-lookup"><span data-stu-id="89ffd-199">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="89ffd-200">Dans le menu déroulant **Instance Size**, sélectionnez la taille d’instance appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="89ffd-200">In the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="89ffd-201">À des fins de test, vous pouvez choisir **Small**(Petite).</span><span class="sxs-lookup"><span data-stu-id="89ffd-201">For testing purposes you can choose **Small**.</span></span>
      * <span data-ttu-id="89ffd-202">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-202">Click **OK**.</span></span>

   <span data-ttu-id="89ffd-203">h.</span><span class="sxs-lookup"><span data-stu-id="89ffd-203">h.</span></span> <span data-ttu-id="89ffd-204">(Facultatif) Par défaut, une distribution récente de Java 8 sera déployée automatiquement par Azure sur votre conteneur d’application web en tant que machine virtuelle Java.</span><span class="sxs-lookup"><span data-stu-id="89ffd-204">(Optional) By default, a recent distribution of Java 8 will be automatically deployed as your JVM by Azure to your web app container.</span></span> <span data-ttu-id="89ffd-205">Vous pouvez cependant sélectionner une version et une distribution de machine virtuelle Java différentes.</span><span class="sxs-lookup"><span data-stu-id="89ffd-205">However, you can select a different version and distribution of the JVM.</span></span> <span data-ttu-id="89ffd-206">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89ffd-206">To do so, use the following steps:</span></span>
      
      * <span data-ttu-id="89ffd-207">Cliquez sur l’onglet **JDK** dans la boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web).</span><span class="sxs-lookup"><span data-stu-id="89ffd-207">Click the **JDK** tab in the **New Web App Container** dialog box.</span></span>
      * <span data-ttu-id="89ffd-208">Vous pouvez choisir l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="89ffd-208">You can choose from one of the following options:</span></span>
        
         * <span data-ttu-id="89ffd-209">Déployer le JDK proposé par défaut par Azure</span><span class="sxs-lookup"><span data-stu-id="89ffd-209">Deploy the default JDK which is offered by Azure</span></span>
         * <span data-ttu-id="89ffd-210">Déployer un JDK tiers à partir d’une liste déroulante de JDK supplémentaires disponibles sur Azure</span><span class="sxs-lookup"><span data-stu-id="89ffd-210">Deploy a 3rd party JDK from a drop-down list of additional JDKs which are available on Azure</span></span>
         * <span data-ttu-id="89ffd-211">Déployer un JDK personnalisé, qui doit être empaqueté dans un fichier ZIP et accessible au public ou dans votre compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="89ffd-211">Deploy a custom JDK, which must be packaged as a ZIP file and either publicly available or in your Azure storage account</span></span>
        
      ![Onglet JDK du nouveau conteneur d’application][11b]

   <span data-ttu-id="89ffd-213">i.</span><span class="sxs-lookup"><span data-stu-id="89ffd-213">i.</span></span> <span data-ttu-id="89ffd-214">Une fois effectuées toutes les étapes ci-dessus, la boîte de dialogue New Web App Container doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="89ffd-214">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Nouveau conteneur d’application][14]
   
   <span data-ttu-id="89ffd-216">j.</span><span class="sxs-lookup"><span data-stu-id="89ffd-216">j.</span></span> <span data-ttu-id="89ffd-217">Cliquez sur **OK** pour terminer la création de votre conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="89ffd-217">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="89ffd-218">Attendez quelques secondes pour que la liste des conteneurs d’application web s’actualise. Votre conteneur d’application web nouvellement créée doit maintenant être sélectionné dans la liste.</span><span class="sxs-lookup"><span data-stu-id="89ffd-218">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

6. <span data-ttu-id="89ffd-219">Vous êtes maintenant prêt à effectuer le déploiement initial de votre application web dans Azure ; cliquez sur **OK** pour déployer votre application Java sur le conteneur d’application web sélectionné.</span><span class="sxs-lookup"><span data-stu-id="89ffd-219">You are now ready to complete the initial deployment of your Web App to Azure; click **OK** to deploy your Java application to the selected Web App container.</span></span> <span data-ttu-id="89ffd-220">Par défaut, votre application est déployée en tant que sous-répertoire du serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="89ffd-220">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="89ffd-221">Si vous voulez qu’elle soit déployée en tant qu’application racine, cochez la case **Deploy to root** (Déployer sur la racine) avant de cliquer sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-221">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>
   
   ![Déploiement sur Azure][15]

7. <span data-ttu-id="89ffd-223">Ensuite, la vue **Journaux d’activité** doit apparaître et indiquer l’état du déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="89ffd-223">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Indicateur de progression][16]
   
   <span data-ttu-id="89ffd-225">Le processus de déploiement de votre application web sur Azure doit prendre seulement quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="89ffd-225">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="89ffd-226">Quand votre application est prête, un lien nommé **Publié** dans la colonne **État** apparaît.</span><span class="sxs-lookup"><span data-stu-id="89ffd-226">When your application is ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="89ffd-227">Quand vous cliquez sur le lien, vous êtes redirigé vers la page d’accueil de votre application web déployée, à laquelle vous pouvez accéder en suivant les étapes de la section suivante.</span><span class="sxs-lookup"><span data-stu-id="89ffd-227">When you click the link, it will take you to your deployed Web App's home page, or you can use the steps in the following section to browse to your web app.</span></span>

## <a name="browsing-to-your-web-app-on-azure"></a><span data-ttu-id="89ffd-228">Accès à votre application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="89ffd-228">Browsing to your Web App on Azure</span></span>

<span data-ttu-id="89ffd-229">Pour accéder à votre application web sur Azure, vous pouvez utiliser la vue **Explorateur Azure**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-229">To browse to your Web App on Azure, you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="89ffd-230">Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : dans IntelliJ, cliquez sur le menu **View** (Affichage), sur **Tool Windows** (Fenêtres des outils), puis sur **Service Explorer** (Explorateur de services).</span><span class="sxs-lookup"><span data-stu-id="89ffd-230">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="89ffd-231">Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="89ffd-231">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="89ffd-232">Quand l’**Explorateur Azure** s’affiche, effectuez les étapes suivantes pour accéder à votre application web :</span><span class="sxs-lookup"><span data-stu-id="89ffd-232">When the **Azure Explorer** view is displayed, follow these steps to browse to your Web App:</span></span> 

1. <span data-ttu-id="89ffd-233">Développez le nœud **Azure** .</span><span class="sxs-lookup"><span data-stu-id="89ffd-233">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="89ffd-234">Développez le nœud **Web Apps** (Applications web).</span><span class="sxs-lookup"><span data-stu-id="89ffd-234">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="89ffd-235">Cliquez avec le bouton droit sur l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="89ffd-235">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="89ffd-236">Quand le menu contextuel s’affiche, cliquez sur **Open in Browser**(Ouvrir dans un navigateur).</span><span class="sxs-lookup"><span data-stu-id="89ffd-236">When the context menu appears, click **Open in Browser**.</span></span>
   
   ![Parcourir l’application web][17]

## <a name="updating-your-web-app"></a><span data-ttu-id="89ffd-238">Mise à jour de votre application web</span><span class="sxs-lookup"><span data-stu-id="89ffd-238">Updating your web app</span></span>

<span data-ttu-id="89ffd-239">La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :</span><span class="sxs-lookup"><span data-stu-id="89ffd-239">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="89ffd-240">Vous pouvez mettre à jour le déploiement d’une application web Java existante.</span><span class="sxs-lookup"><span data-stu-id="89ffd-240">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="89ffd-241">Vous pouvez publier une application Java supplémentaire dans le même conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="89ffd-241">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="89ffd-242">Dans les deux cas, le processus est identique et ne prend que quelques secondes :</span><span class="sxs-lookup"><span data-stu-id="89ffd-242">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="89ffd-243">Dans l’Explorateur de projets IntelliJ, cliquez avec le bouton droit sur l’application Java que vous souhaitez mettre à jour ou ajouter à un conteneur d’application web existant.</span><span class="sxs-lookup"><span data-stu-id="89ffd-243">In the IntelliJ project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>
2. <span data-ttu-id="89ffd-244">Lorsque le menu contextuel s’affiche, sélectionnez **Azure** puis **Publish as Azure Web App...** (Publier en tant qu’application Web Azure...).</span><span class="sxs-lookup"><span data-stu-id="89ffd-244">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>
3. <span data-ttu-id="89ffd-245">Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît.</span><span class="sxs-lookup"><span data-stu-id="89ffd-245">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="89ffd-246">Sélectionnez celui dans lequel vous souhaitez publier ou republier votre application Java, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-246">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="89ffd-247">Quelques secondes plus tard, le **Journal des activités Azure** affiche votre déploiement mis à jour comme **publié** et êtes en mesure de vérifier votre application mise à jour dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="89ffd-247">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="89ffd-248">Démarrage, arrêt ou redémarrage d’une application web existante</span><span class="sxs-lookup"><span data-stu-id="89ffd-248">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="89ffd-249">Pour démarrer ou arrêter un conteneur d’application web Azure existant (y compris toutes les applications Java déployées dans celui-ci), vous pouvez utiliser la vue **Explorateur Azure** .</span><span class="sxs-lookup"><span data-stu-id="89ffd-249">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="89ffd-250">Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : dans IntelliJ, cliquez sur le menu **View** (Affichage), sur **Tool Windows** (Fenêtres des outils), puis sur **Service Explorer** (Explorateur de services).</span><span class="sxs-lookup"><span data-stu-id="89ffd-250">If the **Azure Explorer** view is not already open, you can open it by clicking then **View** menu in IntelliJ, then click **Tool Windows**, and then click **Service Explorer**.</span></span> <span data-ttu-id="89ffd-251">Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="89ffd-251">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="89ffd-252">Quand l’**Explorateur Azure** s’affiche, effectuez les étapes suivantes pour démarrer ou arrêter votre application web :</span><span class="sxs-lookup"><span data-stu-id="89ffd-252">When the **Azure Explorer** view is displayed, follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="89ffd-253">Développez le nœud **Azure** .</span><span class="sxs-lookup"><span data-stu-id="89ffd-253">Expand the **Azure** node.</span></span>
2. <span data-ttu-id="89ffd-254">Développez le nœud **Web Apps** (Applications web).</span><span class="sxs-lookup"><span data-stu-id="89ffd-254">Expand the **Web Apps** node.</span></span> 
3. <span data-ttu-id="89ffd-255">Cliquez avec le bouton droit sur l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="89ffd-255">Right-click the desired Web App.</span></span>
4. <span data-ttu-id="89ffd-256">Quand le menu contextuel s’affiche, cliquez sur **Démarrer**, **Arrêter** ou **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="89ffd-256">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="89ffd-257">Les options de menu étant sensibles au contexte, vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="89ffd-257">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Arrêter l’application Web][18]

## <a name="next-steps"></a><span data-ttu-id="89ffd-259">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89ffd-259">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="89ffd-260">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="89ffd-260">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de ressources Azure pour IntelliJ]: azure-toolkit-for-intellij.md
[Kit de ressources Azure pour Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
