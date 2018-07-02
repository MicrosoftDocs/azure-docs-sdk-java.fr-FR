---
title: ''
description: Ce didacticiel vous montre comment utiliser la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour Eclipse pour créer une application web Hello World pour Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 896e7eff389bc7d3ac119d315c50aae505a381da
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090802"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a><span data-ttu-id="b096c-102">Créer une application web Hello World pour Azure à l’aide de l’ancien kit de ressources pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="b096c-102">Create a Hello World web app for Azure using the legacy toolkit for Eclipse</span></span>

<span data-ttu-id="b096c-103">Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide de la version 3.0.6 (ou ultérieure) du [boîte à outils Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="b096c-103">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using version 3.0.6 (or earlier) of the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="b096c-104">Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour IntelliJ], consultez [Créer une application web pour Azure à l’aide d’IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="b096c-104">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="b096c-105">Le Kit de ressources Azure pour Eclipse a été mis à jour en août 2017 avec un flux de travail différent.</span><span class="sxs-lookup"><span data-stu-id="b096c-105">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="b096c-106">Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b096c-106">This article illustrates creating a Hello World web app by using version 3.0.6 (or earlier) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="b096c-107">Si vous utilisez la version 3.0.7 (ou antérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans Eclipse][Updated Version].</span><span class="sxs-lookup"><span data-stu-id="b096c-107">If you are using the version 3.0.7 (or later) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse][Updated Version].</span></span>
>

<span data-ttu-id="b096c-108">À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="b096c-108">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Version préliminaire de l’application Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="b096c-110">Créer un projet d’application web</span><span class="sxs-lookup"><span data-stu-id="b096c-110">Create a new web app project</span></span>

1. <span data-ttu-id="b096c-111">Démarrez Eclipse et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour Eclipse][eclipse-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="b096c-111">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="b096c-112">Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique).</span><span class="sxs-lookup"><span data-stu-id="b096c-112">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="b096c-113">(si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)**, procédez comme suit : cliquez sur **File (Fichier)**, cliquez sur **New (Nouveau)**, sur **Project (Projet)...**, développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)**).</span><span class="sxs-lookup"><span data-stu-id="b096c-113">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

2. <span data-ttu-id="b096c-114">Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="b096c-114">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="b096c-115">Votre écran se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="b096c-115">Your screen will appear similar to the following:</span></span>
   
   ![Création d’un nouveau projet Web dynamique][02]

3. <span data-ttu-id="b096c-117">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b096c-117">Click **Finish**.</span></span>

4. <span data-ttu-id="b096c-118">Dans la vue **Explorateur de projets** d’Eclipse, développez **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="b096c-118">Within Eclipse's **Project Explorer** view, expand **MyWebApp**.</span></span> <span data-ttu-id="b096c-119">Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.</span><span class="sxs-lookup"><span data-stu-id="b096c-119">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

5. <span data-ttu-id="b096c-120">Dans la boîte de dialogue **New JSP File** (Nouveau fichier JSP), nommez le fichier **index.jsp**, conservez le dossier parent en tant que **MyWebApp/WebContent**, puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="b096c-120">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

6. <span data-ttu-id="b096c-121">Pour les besoins de ce didacticiel, dans la boîte de dialogue **Select JSP Template** (Sélectionner le modèle JSP), sélectionnez **New JSP File (html)** (Nouveau fichier JSP (html)) et cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="b096c-121">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

7. <span data-ttu-id="b096c-122">Quand votre fichier index.jsp s’ouvre dans Eclipse, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="b096c-122">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="b096c-123">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="b096c-123">within the existing `<body>` element.</span></span> <span data-ttu-id="b096c-124">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b096c-124">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="b096c-125">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="b096c-125">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="b096c-126">Déployer votre application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="b096c-126">Deploy your web app to Azure</span></span>

<span data-ttu-id="b096c-127">Vous pouvez déployer une application web Java sur Azure de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="b096c-127">There are several ways by which you can deploy a Java web application to Azure.</span></span> <span data-ttu-id="b096c-128">Ce didacticiel décrit l’une des plus simples : votre application est déployée sur un conteneur d’application web Azure ; ainsi, aucun type de projet spécifique ni outil supplémentaire n’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b096c-128">This tutorial describes one of the simplest: your application will be deployed to an Azure Web App Container - no special project type nor additional tools are needed.</span></span> <span data-ttu-id="b096c-129">Le JDK et le logiciel du conteneur web vous étant fournis par Azure, vous n’avez pas besoin de charger les vôtres ; vous devez uniquement être en possession de votre application web Java.</span><span class="sxs-lookup"><span data-stu-id="b096c-129">The JDK and the web container software will be provided for you by Azure, so there is no need to upload your own; all you need is your Java Web App.</span></span> <span data-ttu-id="b096c-130">Ainsi, le processus de publication de votre application ne prend que quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="b096c-130">As a result, the publishing process for your application will take seconds, not minutes.</span></span>

1. <span data-ttu-id="b096c-131">Dans l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="b096c-131">In Eclipse's Project Explorer, right-click **MyWebApp**.</span></span>

2. <span data-ttu-id="b096c-132">Dans le menu contextuel, sélectionnez **Azure**, puis cliquez sur **Publish as Azure Web App...** (Publier en tant qu’application web Azure...).</span><span class="sxs-lookup"><span data-stu-id="b096c-132">In the context menu, select **Azure**, then click **Publish as Azure Web App...**</span></span>
   
   ![Publish as Azure Web App][03]
   
   <span data-ttu-id="b096c-134">Sinon, lorsque votre projet d’application web est sélectionné dans l’Explorateur de projets, vous pouvez cliquer sur le bouton de liste déroulante **Publish** (Publier) sur la barre d’outils et sélectionner **Publish as Azure Web App** (Publier en tant qu’application web Azure...) à partir cet emplacement :</span><span class="sxs-lookup"><span data-stu-id="b096c-134">Alternatively, while your web application project is selected in the Project Explorer, you can click the **Publish** dropdown button on the toolbar and select **Publish as Azure Web App** from there:</span></span>
   
   ![Publish as Azure Web App][14]

3. <span data-ttu-id="b096c-136">Si vous n’êtes pas encore connecté à Azure à partir d’Eclipse, vous serez invité à vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="b096c-136">If you have not already signed into Azure from Eclipse, you will be prompted to sign into your Azure account:</span></span>
   
   ![Boîte de dialogue Connexion à Azure][04]
   
   <span data-ttu-id="b096c-138">Si vous avez plusieurs comptes Azure, certaines des invites du processus de connexion peuvent s’afficher plusieurs fois, même si elles semblent être identiques.</span><span class="sxs-lookup"><span data-stu-id="b096c-138">If you have multiple Azure accounts, some of the prompts during the sign in process may be shown more than once, even if they appear to be the same.</span></span> <span data-ttu-id="b096c-139">Dans ce cas, continuez à suivre les instructions de connexion.</span><span class="sxs-lookup"><span data-stu-id="b096c-139">When this happens, continue following the sign in instructions.</span></span>

4. <span data-ttu-id="b096c-140">Une fois que vous êtes connecté à votre compte Azure, la boîte de dialogue **Gérer les abonnements** affiche la liste des abonnements associés à vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="b096c-140">After you have successfully signed into your Azure account, the **Manage Subscriptions** dialog box will display a list of subscriptions that are associated with your credentials.</span></span> <span data-ttu-id="b096c-141">Si plusieurs abonnements sont répertoriés et que vous ne souhaitez utiliser qu’une partie d’entre eux, vous pouvez éventuellement désélectionner ceux qui ne vous intéressent pas.</span><span class="sxs-lookup"><span data-stu-id="b096c-141">If there are multiple subscriptions listed and you want to work with only a specific subset of them, you may optionally uncheck the ones you do want to use.</span></span> <span data-ttu-id="b096c-142">Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="b096c-142">When you have selected your subscriptions, click **Close**.</span></span>
   
   ![Boîte de dialogue Gestion des abonnements][05]

5. <span data-ttu-id="b096c-144">Quand la boîte de dialogue **Deploy to Azure Web App Container** (Déployer sur le conteneur d’application web Azure) s’affiche, elle présente tous les conteneurs d’application web déjà créés ; si vous n’avez pas créé de conteneur, la liste est vide.</span><span class="sxs-lookup"><span data-stu-id="b096c-144">When the **Deploy to Azure Web App Container** dialog box appears, it will display any Web App containers that you have previously created; if you have not created any containers, the list will be empty.</span></span>
   
   ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][06]

6. <span data-ttu-id="b096c-146">Si vous n’avez pas déjà créé de conteneur d’application web Azure ou que vous souhaitez publier votre application dans un nouveau conteneur, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="b096c-146">If you have not created an Azure Web App Container before, or if you would like to publish your application to a new container, use the following steps.</span></span> <span data-ttu-id="b096c-147">Sinon, sélectionnez un conteneur d’application web existant et passez à l’étape 7 ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b096c-147">Otherwise, select an existing Web App Container and skip to step 7 below.</span></span>
   
   <span data-ttu-id="b096c-148">a.</span><span class="sxs-lookup"><span data-stu-id="b096c-148">a.</span></span> <span data-ttu-id="b096c-149">Cliquez sur **New...**</span><span class="sxs-lookup"><span data-stu-id="b096c-149">Click **New...**</span></span>
      
      ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][15]

   <span data-ttu-id="b096c-151">b.</span><span class="sxs-lookup"><span data-stu-id="b096c-151">b.</span></span> <span data-ttu-id="b096c-152">La boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b096c-152">The **New Web App Container** dialog box will be displayed:</span></span>
      
      ![Boîte de dialogue Nouveau conteneur d’application web][07a]

   <span data-ttu-id="b096c-154">c.</span><span class="sxs-lookup"><span data-stu-id="b096c-154">c.</span></span> <span data-ttu-id="b096c-155">Entrez un **nom DNS** pour votre conteneur d’application web ; celui-ci constitue le nom DNS feuille de l’URL hôte de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b096c-155">Enter a **DNS Label** for your Web App Container; this will form the leaf DNS label of the host URL for your web application in Azure.</span></span> <span data-ttu-id="b096c-156">(Le nom doit être disponible et conforme aux exigences d’affectation de noms pour les applications web Azure.)</span><span class="sxs-lookup"><span data-stu-id="b096c-156">(Note that the name must be available and conform to Azure Web App naming requirements.)</span></span>

   <span data-ttu-id="b096c-157">d.</span><span class="sxs-lookup"><span data-stu-id="b096c-157">d.</span></span> <span data-ttu-id="b096c-158">Dans le menu déroulant **Web Container** (Conteneur d’application), sélectionnez le logiciel approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="b096c-158">In the **Web Container** drop-down menu, select the appropriate software for your application.</span></span>
      
      <span data-ttu-id="b096c-159">Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9.</span><span class="sxs-lookup"><span data-stu-id="b096c-159">Currently, you can choose from Tomcat 8, Tomcat 7 or Jetty 9.</span></span> <span data-ttu-id="b096c-160">Une distribution récente du logiciel sélectionné sera fournie par Azure, et il s’exécutera sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.</span><span class="sxs-lookup"><span data-stu-id="b096c-160">A recent distribution of the selected software will be provided by Azure, and it will run on a recent distribution of JDK 8 created by Oracle and provided by Azure.</span></span>

   <span data-ttu-id="b096c-161">e.</span><span class="sxs-lookup"><span data-stu-id="b096c-161">e.</span></span> <span data-ttu-id="b096c-162">Dans le menu déroulant **Subscription** (Abonnement), sélectionnez l’abonnement à utiliser pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="b096c-162">In the **Subscription** drop-down menu, select the subscription you want to use for this deployment.</span></span>

   <span data-ttu-id="b096c-163">f.</span><span class="sxs-lookup"><span data-stu-id="b096c-163">f.</span></span> <span data-ttu-id="b096c-164">Dans le menu déroulant **Resource Group** (Groupe de ressources), sélectionnez le groupe de ressources auquel vous souhaitez associer votre application web.</span><span class="sxs-lookup"><span data-stu-id="b096c-164">In the **Resource Group** drop-down menu, select the Resource Group with which you want to associate your Web App.</span></span> <span data-ttu-id="b096c-165">(Les groupes de ressources Azure permettent de regrouper les ressources associées afin de pouvoir, par exemple, les supprimer simultanément.)</span><span class="sxs-lookup"><span data-stu-id="b096c-165">(Azure Resource Groups allow you to group related resources together so that, for example, they can be deleted together.)</span></span>
      
      <span data-ttu-id="b096c-166">Vous pouvez sélectionner un groupe de ressources existant (le cas échéant) et passer directement à l’étape G ou suivre les étapes ci-dessous pour créer un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="b096c-166">You can select an existing Resource Group (if you have any) and skip to step g below, or use the following these steps to create a new Resource Group:</span></span>
      
   * <span data-ttu-id="b096c-167">Cliquez sur **New...**</span><span class="sxs-lookup"><span data-stu-id="b096c-167">Click **New...**</span></span>
   * <span data-ttu-id="b096c-168">La boîte de dialogue **New Resource Group** (Nouveau groupe de ressources) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b096c-168">The **New Resource Group** dialog box will be displayed:</span></span>
        
       ![Boîte de dialogue Nouveau groupe de ressources][08]
   * <span data-ttu-id="b096c-170">Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b096c-170">In the the **Name** textbox, specify a name for your new Resource Group.</span></span>
   * <span data-ttu-id="b096c-171">Dans le menu déroulant **Region** (Région), sélectionnez l’emplacement de centre de données Azure approprié pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b096c-171">In the the **Region** drop-down menu, select the appropriate Azure data center location for your Resource Group.</span></span>
   * <span data-ttu-id="b096c-172">FACULTATIF : par défaut, une distribution récente de Java 8 sera déployée automatiquement par Azure sur votre conteneur d’application web en tant que votre machine virtuelle Java.</span><span class="sxs-lookup"><span data-stu-id="b096c-172">OPTIONAL: By default, a recent distribution of Java 8 will be deployed by Azure automatically to your web app container as your JVM.</span></span> <span data-ttu-id="b096c-173">Vous pouvez cependant spécifier une version et une distribution de machine virtuelle Java différentes si votre application web l’exige.</span><span class="sxs-lookup"><span data-stu-id="b096c-173">However, you can specify a different version and distribution of the JVM if your Web App requires it.</span></span> <span data-ttu-id="b096c-174">Pour spécifier le JDK de votre application web, cliquez sur l’onglet **JDK** et sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="b096c-174">To specify the JDK for your Web App, click the **JDK** tab, and select one of the following options:</span></span>
     * <span data-ttu-id="b096c-175">**Deploy the default JDK offered by Azure Web Apps service**(Déployer le JDK par défaut offert par le service Azure Web Apps) : cette option déploiera une distribution récente de Java 8.</span><span class="sxs-lookup"><span data-stu-id="b096c-175">**Deploy the default JDK offered by Azure Web Apps service**: This option will deploy a recent distribution of Java 8.</span></span>
     * <span data-ttu-id="b096c-176">**Deploy a 3rd party JDK available on Azure**(Déployer un JDK tiers disponible sur Azure) : cette option vous permet de choisir dans la liste des JDK fournis par Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b096c-176">**Deploy a 3rd party JDK available on Azure**: This option allows you to choose from the list of JDKs which are provided by Microsoft Azure.</span></span>
     * <span data-ttu-id="b096c-177">**Deploy my own JDK from this download location**(Déployer mon propre JDK à partir de cet emplacement de téléchargement) : cette option vous permet de spécifier votre propre distribution JDK, qui doit être fournie comme un fichier ZIP puis chargée vers un emplacement de téléchargement disponible publiquement ou un compte de stockage Azure auquel lequel vous avez accès.</span><span class="sxs-lookup"><span data-stu-id="b096c-177">**Deploy my own JDK from this download location**: This option allows you to specify your own JDK distribution, which must be packaged as a ZIP file and uploaded to either a publicly available download location or an Azure storage account for which you have access.</span></span>
          
       ![Boîte de dialogue Nouveau conteneur d’application web][07b]

   <span data-ttu-id="b096c-179">g.</span><span class="sxs-lookup"><span data-stu-id="b096c-179">g.</span></span> <span data-ttu-id="b096c-180">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b096c-180">Click **OK**.</span></span>

   <span data-ttu-id="b096c-181">h.</span><span class="sxs-lookup"><span data-stu-id="b096c-181">h.</span></span> <span data-ttu-id="b096c-182">Le menu déroulant **App Service Plan** (Plan de Service d’application) répertorie les plans de service d’application qui sont associés au groupe de ressources que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="b096c-182">The **App Service Plan** drop-down menu lists the app service plans that are associated with the Resource Group that you selected.</span></span> <span data-ttu-id="b096c-183">(Les plans App Service spécifient des informations telles que l’emplacement de votre application web, le niveau tarifaire et la taille d’instance de calcul.</span><span class="sxs-lookup"><span data-stu-id="b096c-183">(App Service Plans specify information such as the location of your Web App, the pricing tier and the compute instance size.</span></span> <span data-ttu-id="b096c-184">Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)</span><span class="sxs-lookup"><span data-stu-id="b096c-184">A single App Service Plan can be used for multiple Web Apps, which is why it is maintained separately from a specific Web App deployment.)</span></span>
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * <span data-ttu-id="b096c-185">Cliquez sur **New...**</span><span class="sxs-lookup"><span data-stu-id="b096c-185">Click **New...**</span></span>
      * <span data-ttu-id="b096c-186">La boîte de dialogue **New App Service Plan** (Nouveau plan de Service d’application) s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b096c-186">The **New App Service Plan** dialog box will be displayed:</span></span>
        
          ![Boîte de dialogue Nouveau plan App Service][09]
      * <span data-ttu-id="b096c-188">Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau plan de service d’application.</span><span class="sxs-lookup"><span data-stu-id="b096c-188">In the the **Name** textbox, specify a name for your new App Service Plan.</span></span>
      * <span data-ttu-id="b096c-189">Dans le menu déroulant **Location** (Emplacement), sélectionnez l’emplacement de centre de données Azure approprié pour le plan.</span><span class="sxs-lookup"><span data-stu-id="b096c-189">In the the **Location** drop-down menu, select the appropriate Azure data center location for the plan.</span></span>
      * <span data-ttu-id="b096c-190">Dans le menu déroulant **Pricing Tier** (Niveau de tarification), sélectionnez la tarification appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="b096c-190">In the the **Pricing Tier** drop-down menu, select the appropriate pricing for the plan.</span></span> <span data-ttu-id="b096c-191">À des fins de test, vous pouvez choisir **Free**(Gratuit).</span><span class="sxs-lookup"><span data-stu-id="b096c-191">For testing purposes you can choose **Free**.</span></span>
      * <span data-ttu-id="b096c-192">Dans le menu déroulant **Instance Size** (Taille de l’instance), sélectionnez la taille d’instance appropriée pour le plan.</span><span class="sxs-lookup"><span data-stu-id="b096c-192">In the the **Instance Size** drop-down menu, select the appropriate instance size for the plan.</span></span> <span data-ttu-id="b096c-193">À des fins de test, vous pouvez choisir **Small**(Petite).</span><span class="sxs-lookup"><span data-stu-id="b096c-193">For testing purposes you can choose **Small**.</span></span>

   <span data-ttu-id="b096c-194">i.</span><span class="sxs-lookup"><span data-stu-id="b096c-194">i.</span></span> <span data-ttu-id="b096c-195">Une fois effectuées toutes les étapes ci-dessus, la boîte de dialogue New Web App Container doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="b096c-195">Once you have completed all of the above steps, the New Web App Container dialog box should resemble the following illustration:</span></span>
      
      ![Boîte de dialogue Nouveau conteneur d’application web][10]

   <span data-ttu-id="b096c-197">j.</span><span class="sxs-lookup"><span data-stu-id="b096c-197">j.</span></span> <span data-ttu-id="b096c-198">Cliquez sur **OK** pour terminer la création de votre conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="b096c-198">Click **OK** to complete the creation of your new Web App container.</span></span>
       
      <span data-ttu-id="b096c-199">Attendez quelques secondes pour que la liste des conteneurs d’application web s’actualise. Votre conteneur d’application web nouvellement créée doit maintenant être sélectionné dans la liste.</span><span class="sxs-lookup"><span data-stu-id="b096c-199">Wait a few seconds for the list of the Web App containers to be refreshed, and your newly-created web app container should now be selected in the list.</span></span>

7. <span data-ttu-id="b096c-200">Vous êtes maintenant prêt à lancer le déploiement initial de votre application web sur Azure :</span><span class="sxs-lookup"><span data-stu-id="b096c-200">You are now ready to complete the initial deployment of your Web App to Azure:</span></span>
   
   ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][11]
   
   <span data-ttu-id="b096c-202">Cliquez sur **OK** pour déployer votre application Java sur le conteneur d’application web sélectionné.</span><span class="sxs-lookup"><span data-stu-id="b096c-202">Click **OK** to deploy your Java application to the selected Web App container.</span></span>
   
   <span data-ttu-id="b096c-203">Par défaut, votre application est déployée en tant que sous-répertoire du serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="b096c-203">By default, your application will be deployed as a subdirectory of the application server.</span></span> <span data-ttu-id="b096c-204">Si vous voulez qu’elle soit déployée en tant qu’application racine, cochez la case **Deploy to root** (Déployer sur la racine) avant de cliquer sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b096c-204">If you want it to be deployed as the root application, check the **Deploy to root** checkbox before clicking **OK**.</span></span>

8. <span data-ttu-id="b096c-205">Ensuite, la vue **Journaux d’activité** doit apparaître et indiquer l’état du déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="b096c-205">Next, you should see the **Azure Activity Log** view, which will indicate the deployment status of your Web App.</span></span>
   
   ![Journaux d’activité][12]
   
   <span data-ttu-id="b096c-207">Le processus de déploiement de votre application web sur Azure doit prendre seulement quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="b096c-207">The process of deploying your Web App to Azure should take only a few seconds to complete.</span></span> <span data-ttu-id="b096c-208">Quand votre application est prête, un lien nommé **Publié** in the **État** .</span><span class="sxs-lookup"><span data-stu-id="b096c-208">When your application ready, you will see a link named **Published** in the **Status** column.</span></span> <span data-ttu-id="b096c-209">Quand vous cliquez sur le lien, vous êtes redirigé vers la page d’accueil de votre application web déployée.</span><span class="sxs-lookup"><span data-stu-id="b096c-209">When you click the link, it will take you to your deployed Web App's home page.</span></span>

## <a name="updating-your-web-app"></a><span data-ttu-id="b096c-210">Mise à jour de votre application web</span><span class="sxs-lookup"><span data-stu-id="b096c-210">Updating your web app</span></span>

<span data-ttu-id="b096c-211">La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :</span><span class="sxs-lookup"><span data-stu-id="b096c-211">Updating an existing running Azure Web App is a quick and easy process, and you have two options for updating:</span></span>

* <span data-ttu-id="b096c-212">Vous pouvez mettre à jour le déploiement d’une application web Java existante.</span><span class="sxs-lookup"><span data-stu-id="b096c-212">You can update the deployment of an existing Java Web App.</span></span>
* <span data-ttu-id="b096c-213">Vous pouvez publier une application Java supplémentaire dans le même conteneur d’application web.</span><span class="sxs-lookup"><span data-stu-id="b096c-213">You can publish an additional Java application to the same Web App Container.</span></span>

<span data-ttu-id="b096c-214">Dans les deux cas, le processus est identique et ne prend que quelques secondes :</span><span class="sxs-lookup"><span data-stu-id="b096c-214">In either case, the process is identical and takes only a few seconds:</span></span>

1. <span data-ttu-id="b096c-215">Dans l’Explorateur de projets Eclipse, cliquez avec le bouton droit sur l’application Java que vous souhaitez mettre à jour ou ajouter à un conteneur d’application web existant.</span><span class="sxs-lookup"><span data-stu-id="b096c-215">In the Eclipse project explorer, right-click the Java application you want to update or add to an existing Web App Container.</span></span>

2. <span data-ttu-id="b096c-216">Lorsque le menu contextuel s’affiche, sélectionnez **Azure** puis **Publish as Azure Web App...** (Publier en tant qu’application Web Azure...).</span><span class="sxs-lookup"><span data-stu-id="b096c-216">When the context menu appears, select **Azure** and then **Publish as Azure Web App...**</span></span>

3. <span data-ttu-id="b096c-217">Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît.</span><span class="sxs-lookup"><span data-stu-id="b096c-217">Since you have already logged in previously, you will see a list of your existing Web App containers.</span></span> <span data-ttu-id="b096c-218">Sélectionnez celui dans lequel vous souhaitez publier ou republier votre application Java, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b096c-218">Select the one you want to publish or re-publish your Java application to and click **OK**.</span></span>

<span data-ttu-id="b096c-219">Quelques secondes plus tard, le **Journal des activités Azure** affiche votre déploiement mis à jour comme **publié** et êtes en mesure de vérifier votre application mise à jour dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b096c-219">A few seconds later, the **Azure Activity Log** view will show your updated deployment as **Published** and you will be able to verify your updated application in a web browser.</span></span>

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a><span data-ttu-id="b096c-220">Démarrage, arrêt ou redémarrage d’une application web existante</span><span class="sxs-lookup"><span data-stu-id="b096c-220">Starting, stopping, or restarting an existing web app</span></span>

<span data-ttu-id="b096c-221">Pour démarrer ou arrêter un conteneur d’application web Azure existant (y compris toutes les applications Java déployées dans celui-ci), vous pouvez utiliser la vue **Explorateur Azure** .</span><span class="sxs-lookup"><span data-stu-id="b096c-221">To start or stop an existing Azure Web App container, (including all the deployed Java applications in it), you can use the **Azure Explorer** view.</span></span>

<span data-ttu-id="b096c-222">Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : cliquez sur **Window** (Fenêtre) dans le menu d’Eclipse, puis cliquez successivement sur **Show View** (Afficher la vue), **Other...** (Autre...), **Azure** et **Explorateur Azure**.</span><span class="sxs-lookup"><span data-stu-id="b096c-222">If the **Azure Explorer** view is not already open, you can open it by clicking then **Window** menu in Eclipse, then click **Show View**, then **Other...**, then **Azure**, and then click **Azure Explorer**.</span></span> <span data-ttu-id="b096c-223">Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.</span><span class="sxs-lookup"><span data-stu-id="b096c-223">If you have not previously logged in, it will prompt you to do so.</span></span>

<span data-ttu-id="b096c-224">Quand l’ **Explorateur Azure** s’affiche, procédez comme suit pour démarrer ou arrêter votre application web :</span><span class="sxs-lookup"><span data-stu-id="b096c-224">When the **Azure Explorer** view is displayed, use follow these steps to start or stop your Web App:</span></span> 

1. <span data-ttu-id="b096c-225">Développez le nœud **Azure** .</span><span class="sxs-lookup"><span data-stu-id="b096c-225">Expand the **Azure** node.</span></span>

2. <span data-ttu-id="b096c-226">Développez le nœud **Web Apps** (Applications web).</span><span class="sxs-lookup"><span data-stu-id="b096c-226">Expand the **Web Apps** node.</span></span> 

3. <span data-ttu-id="b096c-227">Cliquez avec le bouton droit sur l’application web souhaitée.</span><span class="sxs-lookup"><span data-stu-id="b096c-227">Right-click the desired Web App.</span></span>

4. <span data-ttu-id="b096c-228">Quand le menu contextuel s’affiche, cliquez sur **Démarrer**, **Arrêter** ou **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="b096c-228">When the context menu appears, click **Start**, **Stop**, or **Restart**.</span></span> <span data-ttu-id="b096c-229">Les options de menu étant sensibles au contexte, vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b096c-229">Note that the menu choices are context-aware, so you can only stop a running web app or start a web app which is not currently running.</span></span>
   
   ![Arrêt d’une application web existante][13]

## <a name="next-steps"></a><span data-ttu-id="b096c-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b096c-231">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="b096c-232">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="b096c-232">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-eclipse-create-hello-world-web-app.md
[eclipse-sign-in-instructions]: azure-toolkit-for-eclipse-sign-in-instructions.md


<!-- IMG List -->

[01]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/02-Dynamic-Web-Project.png
[03]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/03-Context-Menu.png
[04]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/04-Log-In-Dialog.png
[05]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/05-Manage-Subscriptions-Dialog.png
[06]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/06-Deploy-To-Azure-Web-Container.png
[07a]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07a-New-Web-App-Container-Dialog.png
[07b]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/07b-New-Web-App-Container-Dialog.png
[08]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/08-New-Resource-Group-Dialog.png
[09]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/09-New-Service-Plan-Dialog.png
[10]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/10-Completed-Web-App-Container-Dialog.png
[11]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/11-Completed-Deploy-Dialog.png
[12]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/12-Activity-Log-View.png
[13]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/13-Azure-Explorer-Web-App.png
[14]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/14-publishDropdownButton.png
[15]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version/15-New-Azure-Web-Container.png
