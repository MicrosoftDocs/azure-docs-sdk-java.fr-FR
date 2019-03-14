---
title: Créer une application web Hello World pour Azure à l’aide d’Eclipse
description: Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour Eclipse pour créer une application Web Hello World pour Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 20d41e88-9eab-462e-8ee3-89da71e7a33f
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c98f966eb17e3fbde877451c8f8fefb21e6bf686
ms.sourcegitcommit: dca98b953fa3149fb2e6aa49e27e843b6df0c6c2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2019
ms.locfileid: "57786888"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a><span data-ttu-id="e6d86-103">Créer une application web Hello World pour Azure à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="e6d86-103">Create a Hello World web app for Azure using Eclipse</span></span>

<span data-ttu-id="e6d86-104">Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide du [Kit de ressources Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="e6d86-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for Eclipse].</span></span>

> [!NOTE]
>
> <span data-ttu-id="e6d86-105">Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour IntelliJ], consultez [Créer une application web pour Azure à l’aide d’IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="e6d86-105">For a version of this article that uses the [Azure Toolkit for IntelliJ], see [Create a Hello World web app for Azure using IntelliJ][intellij-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="e6d86-106">Le Kit de ressources Azure pour Eclipse a été mis à jour en août 2017 avec un flux de travail différent.</span><span class="sxs-lookup"><span data-stu-id="e6d86-106">The Azure Toolkit for Eclipse was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="e6d86-107">Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.7 (ou antérieure) du Kit de ressources Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e6d86-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for Eclipse.</span></span> <span data-ttu-id="e6d86-108">Si vous utilisez la version 3.0.6 (ou ultérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans Eclipse à l’aide de l’ancien kit de ressources][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="e6d86-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in Eclipse using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="e6d86-109">À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="e6d86-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Version préliminaire de l’application Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="e6d86-111">Créer un projet d’application web</span><span class="sxs-lookup"><span data-stu-id="e6d86-111">Create a new web app project</span></span>

1. <span data-ttu-id="e6d86-112">Démarrez Eclipse et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour Eclipse][instructions-connexion-eclipse].</span><span class="sxs-lookup"><span data-stu-id="e6d86-112">Start Eclipse, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for Eclipse][eclipse-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="e6d86-113">Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique).</span><span class="sxs-lookup"><span data-stu-id="e6d86-113">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="e6d86-114">(si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)**, procédez comme suit : cliquez sur **File (Fichier)**, cliquez sur **New (Nouveau)**, sur **Project (Projet)...**, développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)**).</span><span class="sxs-lookup"><span data-stu-id="e6d86-114">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Création d’un nouveau projet Web dynamique][file-new-dynamic-web-project]

2. <span data-ttu-id="e6d86-116">Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-116">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="e6d86-117">Votre écran se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6d86-117">Your screen will appear similar to the following:</span></span>
   
   ![Propriétés Nouveau projet web dynamique][dynamic-web-project-properties]

3. <span data-ttu-id="e6d86-119">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-119">Click **Finish**.</span></span>

4. <span data-ttu-id="e6d86-120">Dans la vue Explorateur de projets d’Eclipse, développez **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-120">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="e6d86-121">Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-121">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Créer Nouveau fichier JSP][create-new-jsp-file]

5. <span data-ttu-id="e6d86-123">Dans la boîte de dialogue **New JSP File** (Nouveau fichier JSP), nommez le fichier **index.jsp**, conservez le dossier parent en tant que **MyWebApp/WebContent**, puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="e6d86-123">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Boîte de dialogue New JSP File (Nouveau fichier JSP)][new-jsp-file-dialog]

6. <span data-ttu-id="e6d86-125">Pour les besoins de ce didacticiel, dans la boîte de dialogue **Select JSP Template** (Sélectionner le modèle JSP), sélectionnez **New JSP File (html)** (Nouveau fichier JSP (html)) et cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="e6d86-125">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Sélectionner un modèle JSP][select-jsp-template]

7. <span data-ttu-id="e6d86-127">Quand votre fichier index.jsp s’ouvre dans Eclipse, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="e6d86-127">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="e6d86-128">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="e6d86-128">within the existing `<body>` element.</span></span> <span data-ttu-id="e6d86-129">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e6d86-129">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="e6d86-130">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="e6d86-130">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="e6d86-131">Déployer votre application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="e6d86-131">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="e6d86-132">Dans la vue de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet, choisissez **Azure**, puis **Publish as Azure Web App** (Publier en tant qu’application web Azure).</span><span class="sxs-lookup"><span data-stu-id="e6d86-132">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. <span data-ttu-id="e6d86-134">Lorsque la boîte de dialogue **Deploy Web App** (Déployer une application web) s’affiche, vous pouvez choisir l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e6d86-134">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="e6d86-135">Sélectionnez une application web existante, s’il y en a.</span><span class="sxs-lookup"><span data-stu-id="e6d86-135">Select an existing web app if one exists.</span></span>

      ![Sélectionner un App Service][select-app-service]

   * <span data-ttu-id="e6d86-137">Cliquez sur **Create New Web App**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-137">Click **Create New Web App**.</span></span>

      ![Créer un App Service][create-app-service]

      <span data-ttu-id="e6d86-139">Spécifiez les informations requises pour votre application web dans la boîte de dialogue **Créer App Service**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-139">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="e6d86-140">Ici, vous pouvez configurer l’environnement d’exécution, les paramètres de l’application, le plan de service et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e6d86-140">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Boîte de dialogue Créer App Service][create-app-service-dialog]

1. <span data-ttu-id="e6d86-142">Sélectionnez votre application web, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="e6d86-142">Select your web app and then click **Deploy**.</span></span>

   ![Déployer App Service][deploy-app-service]

1. <span data-ttu-id="e6d86-144">Le Kit de ressources affiche un le statut **Published** (Publié) sous l’onglet **Azure Activity Log** lorsque le déploiement de votre application web a été effectué. Il s’agit d’un hyperlien pour l’URL de votre application web déployée.</span><span class="sxs-lookup"><span data-stu-id="e6d86-144">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![État de publication][publish-status]

1. <span data-ttu-id="e6d86-146">Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.</span><span class="sxs-lookup"><span data-stu-id="e6d86-146">You can browse to your web app using the link provided in the status message.</span></span>

   ![Accès à votre application web][browse-web-app]

1. <span data-ttu-id="e6d86-148">Après avoir publié votre application web sur Azure, vous pouvez la gérer en faisant un clic droit et en sélectionnant une des options dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="e6d86-148">After you have published your web to Azure, you can manage your app by right-clicking on it and selecting one of the options on the context menu.</span></span> <span data-ttu-id="e6d86-149">Vous pouvez par exemple **Démarrer**, **Arrêter** ou **Supprimer** votre application web.</span><span class="sxs-lookup"><span data-stu-id="e6d86-149">For example, you can **Start**, **Stop**, or **Delete** your web app.</span></span>

   ![Gérer App Service][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="e6d86-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e6d86-151">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="e6d86-152">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="e6d86-152">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->

[browse-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/browse-web-app.png
[file-new-dynamic-web-project]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/file-new-dynamic-web-project.png
[dynamic-web-project-properties]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/dynamic-web-project-properties.png
[create-new-jsp-file]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-new-jsp-file.png
[new-jsp-file-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/new-jsp-file-dialog.png
[select-jsp-template]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-jsp-template.png
[publish-as-azure-web-app]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-as-azure-web-app.png
[deploy-web-app-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-web-app-dialog.png
[select-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/select-app-service.png
[create-app-service-dialog]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service-dialog.png
[publish-status]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/publish-status.png
[create-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/create-app-service.png
[deploy-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/deploy-app-service.png
[manage-app-service]: ./media/azure-toolkit-for-eclipse-create-hello-world-web-app/manage-app-service.png
