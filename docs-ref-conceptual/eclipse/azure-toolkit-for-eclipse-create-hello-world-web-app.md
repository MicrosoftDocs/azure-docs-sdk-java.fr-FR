---
title: "Créer une application web Azure de base à l’aide d’Eclipse"
description: "Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour Eclipse pour créer une application Web Hello World pour Azure."
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: 
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/19/2017
ms.author: robmcm;asirveda
ms.openlocfilehash: dcab31ad99fb79a91374d95c2b8b0d9d10346f5f
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2017
---
# <a name="create-a-basic-azure-web-app-using-eclipse"></a><span data-ttu-id="82cca-103">Créer une application web Azure de base à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="82cca-103">Create a basic Azure web app using Eclipse</span></span>
<span data-ttu-id="82cca-104">Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide du [Kit de ressources Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="82cca-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a Web App by using the [Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="82cca-105">Un exemple JSP de base est présenté par souci de simplicité, mais des étapes similaires conviennent également pour un servlet Java en ce qui concerne le déploiement d’Azure.</span><span class="sxs-lookup"><span data-stu-id="82cca-105">A basic JSP example is shown for simplicity, but similar steps would be appropriate for a Java servlet, as far as Azure deployment is concerned.</span></span>

<span data-ttu-id="82cca-106">À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="82cca-106">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Version préliminaire de l’application Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-create-a-hello-world-application"></a><span data-ttu-id="82cca-108">Pour créer une application Hello World</span><span class="sxs-lookup"><span data-stu-id="82cca-108">To create a Hello World application</span></span>
<span data-ttu-id="82cca-109">Tout d’abord, nous allons commencer par créer un projet Java.</span><span class="sxs-lookup"><span data-stu-id="82cca-109">First, we'll start off with creating a Java project.</span></span>

1. <span data-ttu-id="82cca-110">Démarrez Eclipse, puis, dans le menu, cliquez successivement sur **File (Fichier)**, **New (Nouveau)** et **Projet web dynamique (Dynamic Web Project)**.</span><span class="sxs-lookup"><span data-stu-id="82cca-110">Start Eclipse, and at the menu click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="82cca-111">(si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)**, procédez comme suit : cliquez sur **File (Fichier)**, cliquez sur **New (Nouveau)**, sur **Project (Projet)...**, développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)**).</span><span class="sxs-lookup"><span data-stu-id="82cca-111">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="82cca-112">Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="82cca-112">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="82cca-113">Votre écran se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="82cca-113">Your screen will appear similar to the following:</span></span>
   
   ![Création d’un nouveau projet Web dynamique][02]

3. <span data-ttu-id="82cca-115">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="82cca-115">Click **Finish**.</span></span>

4. <span data-ttu-id="82cca-116">Dans la vue Explorateur de projets d’Eclipse, développez **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="82cca-116">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="82cca-117">Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.</span><span class="sxs-lookup"><span data-stu-id="82cca-117">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="82cca-118">Dans la boîte de dialogue **New JSP File** (Nouveau fichier JSP), nommez le fichier **index.jsp**, conservez le dossier parent en tant que **MyWebApp/WebContent**, puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="82cca-118">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="82cca-119">Pour les besoins de ce didacticiel, dans la boîte de dialogue **Select JSP Template** (Sélectionner le modèle JSP), sélectionnez **New JSP File (html)** (Nouveau fichier JSP (html)) et cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="82cca-119">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="82cca-120">Quand votre fichier index.jsp s’ouvre dans Eclipse, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="82cca-120">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="82cca-121">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="82cca-121">within the existing `<body>` element.</span></span> <span data-ttu-id="82cca-122">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="82cca-122">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="82cca-123">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="82cca-123">Save index.jsp.</span></span>

## <a name="to-deploy-your-application-to-an-azure-web-app-container"></a><span data-ttu-id="82cca-124">Pour déployer votre application sur un conteneur d’application web Azure</span><span class="sxs-lookup"><span data-stu-id="82cca-124">To deploy your application to an Azure Web App Container</span></span>
<span data-ttu-id="82cca-125">Vous pouvez déployer une application web Java sur Azure de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="82cca-125">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="82cca-126">Ce didacticiel décrit l’une des plus simples : votre application est déployée sur un conteneur d’application web Azure ; ainsi, aucun type de projet spécifique ni outil supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="82cca-126">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="82cca-127">Le JDK et le logiciel du conteneur web vous étant fournis par Azure, vous n’avez pas besoin de charger les vôtres ; vous devez uniquement être en possession de votre application web Java.</span><span class="sxs-lookup"><span data-stu-id="82cca-127">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="82cca-128">Ainsi, le processus de publication de votre application ne prend que quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="82cca-128">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="82cca-129">Dans l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="82cca-129">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="82cca-130">Dans le menu contextuel, sélectionnez **Azure**, puis cliquez sur **Publish as Azure Web App...** (Publier en tant qu’application web Azure...).</span><span class="sxs-lookup"><span data-stu-id="82cca-130">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Publish as Azure Web App][03]
   
   <span data-ttu-id="82cca-132">Sinon, lorsque votre projet d’application web est sélectionné dans l’Explorateur de projets, vous pouvez cliquer sur le bouton de liste déroulante **Publish** (Publier) sur la barre d’outils et sélectionner **Publish as Azure Web App** (Publier en tant qu’application web Azure...) à partir cet emplacement :</span><span class="sxs-lookup"><span data-stu-id="82cca-132">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Publish as Azure Web App][14]

3. <span data-ttu-id="82cca-134">Si vous n’êtes pas encore connecté à Azure à partir d’Eclipse, vous serez invité à vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="82cca-134">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Boîte de dialogue Connexion à Azure][04]
   
   <span data-ttu-id="82cca-136">Si vous avez plusieurs comptes Azure, certaines des invites du processus de connexion peuvent s’afficher plusieurs fois, même si elles semblent être identiques.</span><span class="sxs-lookup"><span data-stu-id="82cca-136">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="82cca-137">Dans ce cas, continuez à suivre les instructions de connexion.</span><span class="sxs-lookup"><span data-stu-id="82cca-137">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="82cca-138">Une fois que vous êtes connecté à votre compte Azure, la boîte de dialogue **Gérer les abonnements** affiche la liste des abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="82cca-138">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="82cca-139">Si plusieurs abonnements sont répertoriés et que vous ne souhaitez utiliser qu’une partie d’entre eux, vous pouvez éventuellement désélectionner ceux qui ne vous intéressent pas.</span><span class="sxs-lookup"><span data-stu-id="82cca-139">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="82cca-140">Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="82cca-140">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Boîte de dialogue Gestion des abonnements][05]

5. <span data-ttu-id="82cca-142">Quand la boîte de dialogue **Deploy to Azure Web App Container** (Déployer sur le conteneur d’application web Azure) s’affiche, elle présente tous les conteneurs d’application web déjà créés ; si vous n’avez pas créé de conteneur, la liste est vide.</span><span class="sxs-lookup"><span data-stu-id="82cca-142">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][06]

6. <span data-ttu-id="82cca-144">Si vous n’avez pas déjà créé de conteneur d’application web Azure ou que vous souhaitez publier votre application dans un nouveau conteneur, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="82cca-144">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="82cca-145">Sinon, sélectionnez un conteneur d’application web existant et passez à l’étape 7 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="82cca-145">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="82cca-146">a.</span><span class="sxs-lookup"><span data-stu-id="82cca-146">a.</span></span> <span data-ttu-id="82cca-147">Cliquez sur **New...**</span><span class="sxs-lookup"><span data-stu-id="82cca-147">Click **New...**</span></span>
      
      ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][15]

   <span data-ttu-id="82cca-149">b.</span><span class="sxs-lookup"><span data-stu-id="82cca-149">b.</span></span> <span data-ttu-id="82cca-150">La boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="82cca-150">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Boîte de dialogue Nouveau conteneur d’application web][07a]

   <span data-ttu-id="82cca-152">c.</span><span class="sxs-lookup"><span data-stu-id="82cca-152">c.</span></span> <span data-ttu-id="82cca-153">Entrez un **nom DNS** pour votre conteneur d’application web ; celui-ci constitue le nom DNS feuille de l’URL hôte de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="82cca-153">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="82cca-154">(Le nom doit être disponible et conforme aux exigences d’affectation de noms pour les applications web Azure.)</span><span class="sxs-lookup"><span data-stu-id="82cca-154">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="82cca-155">d.</span><span class="sxs-lookup"><span data-stu-id="82cca-155">d.</span></span> <span data-ttu-id="82cca-156">Dans le menu déroulant **Web Container** (Conteneur d’application), sélectionnez le logiciel approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="82cca-156">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="82cca-157">Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="82cca-157">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="82cca-158">Une distribution récente du logiciel sélectionné sera fournie par Azure, et il s’exécutera sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="82cca-158">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="82cca-159">e.</span><span class="sxs-lookup"><span data-stu-id="82cca-159">e.</span></span> <span data-ttu-id="82cca-160">Dans le menu déroulant **Subscription** (Abonnement), sélectionnez l’abonnement à utiliser pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="82cca-160">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="82cca-161">f.</span><span class="sxs-lookup"><span data-stu-id="82cca-161">f.</span></span> <span data-ttu-id="82cca-162">Dans le menu déroulant **Resource Group** (Groupe de ressources), sélectionnez le groupe de ressources auquel vous souhaitez associer votre application web.</span><span class="sxs-lookup"><span data-stu-id="82cca-162">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="82cca-163">(Les groupes de ressources Azure permettent de regrouper les ressources associées afin de pouvoir, par exemple, les supprimer simultanément.)</span><span class="sxs-lookup"><span data-stu-id="82cca-163">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="82cca-164">Vous pouvez sélectionner un groupe de ressources existant (le cas échéant) et passer directement à l’étape G ou suivre les étapes ci-dessous pour créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="82cca-164">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
      * <span data-ttu-id="82cca-165">Cliquez sur **New...**</span><span class="sxs-lookup"><span data-stu-id="82cca-165">Click **New...**</span></span>
      * <span data-ttu-id="82cca-166">La boîte de dialogue **New Resource Group** (Nouveau groupe de ressources) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="82cca-166">The **New Resource Group** dialog box will be displayed:</span></span>
        
          ![Boîte de dialogue Nouveau groupe de ressources][08]
      * <span data-ttu-id="82cca-168">Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="82cca-168">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
      * <span data-ttu-id="82cca-169">Dans le menu déroulant **Region** (Région), sélectionnez l’emplacement de centre de données Azure approprié pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="82cca-169">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
      * <span data-ttu-id="82cca-170">FACULTATIF : par défaut, une distribution récente de Java 8 sera déployée automatiquement par Azure sur votre conteneur d’application web en tant que votre machine virtuelle Java.</span><span class="sxs-lookup"><span data-stu-id="82cca-170">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="82cca-171">Vous pouvez cependant spécifier une version et une distribution de machine virtuelle Java différentes si votre application web l’exige.</span><span class="sxs-lookup"><span data-stu-id="82cca-171">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="82cca-172">Pour spécifier le JDK de votre application web, cliquez sur l’onglet **JDK** et sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="82cca-172">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
         * <span data-ttu-id="82cca-173">**Deploy the default JDK offered by Azure Web Apps service**(Déployer le JDK par défaut offert par le service Azure Web Apps) : cette option déploiera une distribution récente de Java 8.</span><span class="sxs-lookup"><span data-stu-id="82cca-173">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
         * <span data-ttu-id="82cca-174">**Deploy a 3rd party JDK available on Azure**(Déployer un JDK tiers disponible sur Azure) : cette option vous permet de choisir dans la liste des JDK fournis par Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82cca-174">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
         * <span data-ttu-id="82cca-175">**Deploy my own JDK from this download location**(Déployer mon propre JDK à partir de cet emplacement de téléchargement) : cette option vous permet de spécifier votre propre distribution JDK, qui doit être fournie comme un fichier ZIP puis chargée vers un emplacement de téléchargement disponible publiquement ou un compte de stockage Azure auquel lequel vous avez accès.</span><span class="sxs-lookup"><span data-stu-id="82cca-175">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
         ![Boîte de dialogue Nouveau conteneur d’application web][07b]

   <span data-ttu-id="82cca-177">g.</span><span class="sxs-lookup"><span data-stu-id="82cca-177">g.</span></span> <span data-ttu-id="82cca-178">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="82cca-178">Click **OK**.</span></span>

   <span data-ttu-id="82cca-179">h.</span><span class="sxs-lookup"><span data-stu-id="82cca-179">h.</span></span> <span data-ttu-id="82cca-180">Le menu déroulant **App Service Plan** (Plan de Service d’application) répertorie les plans de service d’application qui sont associés au groupe de ressources que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="82cca-180">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="82cca-181">(Les plans App Service spécifient des informations telles que l’emplacement de votre application web, le niveau tarifaire et la taille d’instance de calcul.</span><span class="sxs-lookup"><span data-stu-id="82cca-181">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="82cca-182">Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)</span><span class="sxs-lookup"><span data-stu-id="82cca-182">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="82cca-183">Cliquez sur **New...**</span><span class="sxs-lookup"><span data-stu-id="82cca-183">Click **New...**</span></span>
      * <span data-ttu-id="82cca-184">La boîte de dialogue **New App Service Plan** (Nouveau plan de Service d’application) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="82cca-184">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Boîte de dialogue Nouveau plan App Service][09]
      * <span data-ttu-id="82cca-186">Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau plan de service d’application.</span><span class="sxs-lookup"><span data-stu-id="82cca-186">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="82cca-187">Dans le menu déroulant **Location** (Emplacement), sélectionnez l’emplacement de centre de données Azure approprié pour le plan.</span><span class="sxs-lookup"><span data-stu-id="82cca-187">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="82cca-188">Dans le menu déroulant **Pricing Tier** (Niveau de tarification), sélectionnez la tarification appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="82cca-188">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="82cca-189">À des fins de test, vous pouvez choisir **Free**(Gratuit).</span><span class="sxs-lookup"><span data-stu-id="82cca-189">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="82cca-190">Dans le menu déroulant **Instance Size** (Taille de l’instance), sélectionnez la taille d’instance appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="82cca-190">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="82cca-191">À des fins de test, vous pouvez choisir **Small**(Petite).</span><span class="sxs-lookup"><span data-stu-id="82cca-191">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="82cca-192">i.</span><span class="sxs-lookup"><span data-stu-id="82cca-192">i.</span></span> <span data-ttu-id="82cca-193">Une fois effectuées toutes les étapes ci-dessus, la boîte de dialogue New Web App Container doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="82cca-193">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Boîte de dialogue Nouveau conteneur d’application web][10]

   <span data-ttu-id="82cca-195">j.</span><span class="sxs-lookup"><span data-stu-id="82cca-195">j.</span></span> <span data-ttu-id="82cca-196">Cliquez sur **OK** pour terminer la création de votre conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="82cca-196">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="82cca-197">Attendez quelques secondes pour que la liste des conteneurs d’application web s’actualise. Votre conteneur d’application web nouvellement créée doit maintenant être sélectionné dans la liste.</span><span class="sxs-lookup"><span data-stu-id="82cca-197">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="82cca-198">Vous êtes maintenant prêt à lancer le déploiement initial de votre application web sur Azure :</span><span class="sxs-lookup"><span data-stu-id="82cca-198">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][11]
   
   <span data-ttu-id="82cca-200">Cliquez sur **OK** pour déployer votre application Java sur le conteneur d’application web sélectionné.</span><span class="sxs-lookup"><span data-stu-id="82cca-200">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="82cca-201">Par défaut, votre application est déployée en tant que sous-répertoire du serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="82cca-201">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="82cca-202">Si vous voulez qu’elle soit déployée en tant qu’application racine, cochez la case **Deploy to root** (Déployer sur la racine) avant de cliquer sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="82cca-202">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="82cca-203">Ensuite, la vue **Journaux d’activité** doit apparaître et indiquer l’état du déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="82cca-203">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Journaux d’activité][12]
   
   <span data-ttu-id="82cca-205">Le processus de déploiement de votre application web sur Azure doit prendre seulement quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="82cca-205">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="82cca-206">Quand votre application est prête, un lien nommé **Publié** in the **État** .</span><span class="sxs-lookup"><span data-stu-id="82cca-206">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="82cca-207">Quand vous cliquez sur le lien, vous êtes redirigé vers la page d’accueil de votre application web déployée.</span><span class="sxs-lookup"><span data-stu-id="82cca-207">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="82cca-208">Mise à jour de votre application web</span><span class="sxs-lookup"><span data-stu-id="82cca-208">Updating your web app</span></span>
<span data-ttu-id="82cca-209">La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :</span><span class="sxs-lookup"><span data-stu-id="82cca-209">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="82cca-210">Vous pouvez mettre à jour le déploiement d’une application web Java existante.</span><span class="sxs-lookup"><span data-stu-id="82cca-210">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="82cca-211">Vous pouvez publier une application Java supplémentaire dans le même conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="82cca-211">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="82cca-212">Dans les deux cas, le processus est identique et ne prend que quelques secondes :</span><span class="sxs-lookup"><span data-stu-id="82cca-212">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="82cca-213">Dans l’Explorateur de projets Eclipse, cliquez avec le bouton droit sur l’application Java que vous souhaitez mettre à jour ou ajouter à un conteneur d’application web existant.</span><span class="sxs-lookup"><span data-stu-id="82cca-213">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="82cca-214">Lorsque le menu contextuel s’affiche, sélectionnez **Azure** puis **Publish as Azure Web App...** (Publier en tant qu’application Web Azure...).</span><span class="sxs-lookup"><span data-stu-id="82cca-214">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="82cca-215">Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît.</span><span class="sxs-lookup"><span data-stu-id="82cca-215">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="82cca-216">Sélectionnez celui dans lequel vous souhaitez publier ou republier votre application Java, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="82cca-216">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="82cca-217">Quelques secondes plus tard, le **Journal des activités Azure** affiche votre déploiement mis à jour comme **publié** et êtes en mesure de vérifier votre application mise à jour dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="82cca-217">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="82cca-218">Démarrage, arrêt ou redémarrage d’une application web existante</span><span class="sxs-lookup"><span data-stu-id="82cca-218">Starting, stopping, or restarting an existing web app</span></span>
<span data-ttu-id="82cca-219">Pour démarrer ou arrêter un conteneur d’application web Azure existant (y compris toutes les applications Java déployées dans celui-ci), vous pouvez utiliser la vue **Explorateur Azure** .</span><span class="sxs-lookup"><span data-stu-id="82cca-219">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="82cca-220">Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : cliquez sur **Window** (Fenêtre) dans le menu d’Eclipse, puis cliquez successivement sur **Show View** (Afficher la vue), **Other...** (Autre...), **Azure** et **Explorateur Azure**.</span><span class="sxs-lookup"><span data-stu-id="82cca-220">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="82cca-221">Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="82cca-221">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="82cca-222">Quand l’ **Explorateur Azure** s’affiche, procédez comme suit pour démarrer ou arrêter votre application web :</span><span class="sxs-lookup"><span data-stu-id="82cca-222">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="82cca-223">Développez le nœud **Azure** .</span><span class="sxs-lookup"><span data-stu-id="82cca-223">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="82cca-224">Développez le nœud **Web Apps** (Applications web).</span><span class="sxs-lookup"><span data-stu-id="82cca-224">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="82cca-225">Cliquez avec le bouton droit sur l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="82cca-225">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="82cca-226">Quand le menu contextuel s’affiche, cliquez sur **Démarrer**, **Arrêter** ou **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="82cca-226">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="82cca-227">Les options de menu étant sensibles au contexte, vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="82cca-227">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Arrêt d’une application web existante][13]

## <a name="next-steps"></a><span data-ttu-id="82cca-229">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="82cca-229">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="82cca-230">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="82cca-230">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: azure-toolkit-for-eclipse.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/15-New-Azure-Web-Container.png
