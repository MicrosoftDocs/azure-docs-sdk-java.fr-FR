---
title: Créer une application web Hello World pour Azure à l’aide d’IntelliJ
description: Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour IntelliJ pour créer une application web Hello World pour Azure.
services: app-service
documentationcenter: java
author: selvasingh
manager: routlaw
editor: ''
ms.assetid: 75ce7b36-e3ae-491d-8305-4b42ce37db4e
ms.author: robmcm;asirveda
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: cc68e16a6940a1f0f2b08f0b63c90c58ec6dbc4e
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954190"
---
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a><span data-ttu-id="95b4d-103">Créer une application web Hello World pour Azure à l’aide d’IntelliJ</span><span class="sxs-lookup"><span data-stu-id="95b4d-103">Create a Hello World web app for Azure using IntelliJ</span></span>

<span data-ttu-id="95b4d-104">Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide du [Kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="95b4d-104">This tutorial shows how to create and deploy a basic Hello World application to Azure as a web app by using the [Azure Toolkit for IntelliJ].</span></span>

> [!NOTE]
>
> <span data-ttu-id="95b4d-105">Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour Eclipse], consultez [Créer une application web pour Azure à l’aide d’Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="95b4d-105">For a version of this article that uses the [Azure Toolkit for Eclipse], see [Create a Hello World web app for Azure using Eclipse][eclipse-hello-world].</span></span>
>

> [!IMPORTANT]
> 
> <span data-ttu-id="95b4d-106">Le Kit de ressources Azure pour IntelliJ a été mis à jour en août 2017 avec un flux de travail différent.</span><span class="sxs-lookup"><span data-stu-id="95b4d-106">The Azure Toolkit for IntelliJ was updated in August 2017 with a different workflow.</span></span> <span data-ttu-id="95b4d-107">Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.7 (ou antérieure) du Kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="95b4d-107">This article illustrates creating a Hello World web app by using version 3.0.7 (or later) of the Azure Toolkit for IntelliJ.</span></span> <span data-ttu-id="95b4d-108">Si vous utilisez la version 3.0.6 (ou ultérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans IntelliJ à l’aide de l’ancien kit de ressources][Legacy Version].</span><span class="sxs-lookup"><span data-stu-id="95b4d-108">If you are using the version 3.0.6 (or earlier) of the toolkit, you will need to follow the steps in [Create a Hello World web app for Azure in IntelliJ using the legacy toolkit][Legacy Version].</span></span>
> 

<span data-ttu-id="95b4d-109">À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :</span><span class="sxs-lookup"><span data-stu-id="95b4d-109">When you have completed this tutorial, your application will look similar to the following illustration when you view it in a web browser:</span></span>

![Version préliminaire de l’application Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a><span data-ttu-id="95b4d-111">Créer un projet d’application web</span><span class="sxs-lookup"><span data-stu-id="95b4d-111">Create a new web app project</span></span>

1. <span data-ttu-id="95b4d-112">Démarrez IntelliJ et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour IntelliJ][intelliJ-sign-in-instructions].</span><span class="sxs-lookup"><span data-stu-id="95b4d-112">Start IntelliJ, and sign into your Azure account by using the instructions in the [Azure Sign In Instructions for the Azure Toolkit for IntelliJ][intelliJ-sign-in-instructions] article.</span></span>

1. <span data-ttu-id="95b4d-113">Cliquez sur le menu **File**, sur **New**, puis sur **Project**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-113">Click the **File** menu, then click **New**, and then click **Project**.</span></span>
   
   ![Créer un projet][file-new-project]

1. <span data-ttu-id="95b4d-115">Dans la boîte de dialogue **New Project**, sélectionnez **Maven**, puis **maven-archetype-webapp**, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-115">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>
   
   ![Choisir une application web d’archétype Maven][maven-archetype-webapp]
   
1. <span data-ttu-id="95b4d-117">Spécifiez les valeurs **GroupId** et **ArtifactId** pour votre application web, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-117">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>
   
   ![Spécifier GroupId et ArtifactId][groupid-and-artifactid]

1. <span data-ttu-id="95b4d-119">Personnalisez les paramètres Maven ou acceptez les valeurs par défaut, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-119">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>
   
   ![Spécifier les paramètres Maven][maven-options]

1. <span data-ttu-id="95b4d-121">Spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-121">Specify your project name and location, and then click **Finish**.</span></span>
   
   ![Spécifier le nom du projet][project-name]

1. <span data-ttu-id="95b4d-123">Dans la vue de l’Explorateur de projets d’IntelliJ, développez **src**, **main**, puis **webapp**, puis double-cliquez sur **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-123">Within IntelliJ's Project Explorer view, expand **src**, then **main**, then **webapp**, and then double-click **index.jsp**.</span></span>
   
   ![Ouvrir la page d’index][open-index-page]

1. <span data-ttu-id="95b4d-125">Quand votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="95b4d-125">When your index.jsp file opens in IntelliJ, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="95b4d-126">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="95b4d-126">within the existing `<body>` element.</span></span> <span data-ttu-id="95b4d-127">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="95b4d-127">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Modifier la page d’index][edit-index-page]

1. <span data-ttu-id="95b4d-129">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="95b4d-129">Save index.jsp.</span></span>

## <a name="deploy-your-web-app-to-azure"></a><span data-ttu-id="95b4d-130">Déployer votre application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="95b4d-130">Deploy your web app to Azure</span></span>

1. <span data-ttu-id="95b4d-131">Dans la vue de l’Explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur votre projet, choisissez **Azure**, puis **Run on Web App**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-131">Within IntelliJ's Project Explorer view, right-click your project, choose **Azure**, and then choose **Run on Web App**.</span></span>
   
   ![Menu Run on Web App][run-on-web-app-menu]

1. <span data-ttu-id="95b4d-133">Dans la boîte de dialogue Run on Web App, vous pouvez choisir l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="95b4d-133">In the Run on Web App dialog box, you can choose one of the following options:</span></span>

   * <span data-ttu-id="95b4d-134">Choisissez une application web existante (le cas échéant), puis cliquez sur **Run**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-134">Choose an existing web app (if one exists), and then click **Run**.</span></span>

      ![Boîte de dialogue Run on Web App][run-on-web-app-dialog]

   * <span data-ttu-id="95b4d-136">Cliquez sur **Create New Web App**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-136">Click **Create New Web App**.</span></span> <span data-ttu-id="95b4d-137">Si vous choisissez de créer une application web, spécifiez les informations requises pour votre application web, puis cliquez sur **Run**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-137">If you choose to create a new web app, specify the requisite information for your web app, and then click **Run**.</span></span>

      ![Créer une application web][create-new-web-app-dialog]

1. <span data-ttu-id="95b4d-139">Le Kit de ressources affiche un message d’état une fois qu’il a réussi à déployer votre application web, avec l’URL de votre application web déployée.</span><span class="sxs-lookup"><span data-stu-id="95b4d-139">The toolkit will display a status message when it has successfully deployed your web app, which will also display the URL of your deployed web app.</span></span>

   ![Déploiement réussi][successfully-deployed]

1. <span data-ttu-id="95b4d-141">Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.</span><span class="sxs-lookup"><span data-stu-id="95b4d-141">You can browse to your web app using the link provided in the status message.</span></span>

   ![Accès à votre application web][browse-web-app]

1. <span data-ttu-id="95b4d-143">Une fois que vous avez publié votre application web, vos paramètres sont enregistrés comme valeur par défaut, et vous pouvez exécuter votre application sur Azure en cliquant sur l’icône en forme de flèche verte dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="95b4d-143">After you have published your web app, your settings will be saved as the default, and you can run your application on Azure by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="95b4d-144">Vous pouvez modifier vos paramètres en cliquant sur le menu déroulant de votre application web, puis sur **Edit Configurations**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-144">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Edit Configurations][edit-configuration-menu]

1. <span data-ttu-id="95b4d-146">Quand la boîte de dialogue **ExécRun/Debug Configurations** s’affiche, vous pouvez modifier les paramètres par défaut de votre choix. Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="95b4d-146">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Boîte de dialogue Edit configuration][edit-configuration-dialog]

## <a name="next-steps"></a><span data-ttu-id="95b4d-148">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95b4d-148">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="95b4d-149">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="95b4d-149">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Kit de ressources Azure pour IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Kit de ressources Azure pour Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[run-on-web-app-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[run-on-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
