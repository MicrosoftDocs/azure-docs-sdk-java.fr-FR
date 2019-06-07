---
title: Créer une application web Hello World pour Azure App Service à l’aide d’Eclipse
description: Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour Eclipse pour créer une application Web Hello World pour Azure.
services: app-service
keywords: java, eclipse, web app, azure app service, hello world, démarrage rapide
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
ms.openlocfilehash: 7e88298afaf0b4601d85d6063b7096c79e677421
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625851"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a><span data-ttu-id="12a97-104">Créer une application web Hello World pour Azure App Service à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="12a97-104">Create a Hello World web app for Azure App Service using Eclipse</span></span>

<span data-ttu-id="12a97-105">Avec le plug-in open source [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse), la création et le déploiement d’une application Hello World de base sur Azure App Service en tant qu’application web ne prennent que quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="12a97-105">Using open sourced [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="12a97-106">Si vous préférez utiliser IntelliJ IDEA, consultez notre [tutoriel similaire pour IntelliJ][intellij-hello-world].</span><span class="sxs-lookup"><span data-stu-id="12a97-106">If you prefer using IntelliJ IDEA, check out our [similar tutorial for IntelliJ][intellij-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="12a97-107">N’oubliez pas de nettoyer les ressources après avoir terminé ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="12a97-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="12a97-108">Dans ce cas, l’exécution de ce guide ne provoquera pas de dépassement du quota de votre compte gratuit.</span><span class="sxs-lookup"><span data-stu-id="12a97-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="12a97-109">Installation et connexion</span><span class="sxs-lookup"><span data-stu-id="12a97-109">Installation and sign-in</span></span>

1. <span data-ttu-id="12a97-110">Faites glisser le bouton suivant vers votre espace de travail Eclipse en cours d’exécution pour installer le plug-in Azure Toolkit for Eclipse ([autres options d’installation](azure-toolkit-for-eclipse-installation.md)).</span><span class="sxs-lookup"><span data-stu-id="12a97-110">Drag the following button to your running Eclipse workspace to install the Azure Toolkit for Eclipse plugin ([other installation options](azure-toolkit-for-eclipse-installation.md)).</span></span>

    <span data-ttu-id="12a97-111">[![Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client")</span><span class="sxs-lookup"><span data-stu-id="12a97-111">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

1. <span data-ttu-id="12a97-112">Pour vous connecter à votre compte Azure, cliquez sur **Tools**, **Azure**, puis **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="12a97-112">To sign in to your Azure account, click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="12a97-113">![Menu d’Eclipse pour la connexion à Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="12a97-113">![Eclipse Menu for Azure Sign In][I01]</span></span>

1. <span data-ttu-id="12a97-114">Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Connexion à l’appareil**, puis cliquez sur **Connexion** ([autres options de connexion](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="12a97-114">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign-in options](azure-toolkit-for-eclipse-sign-in-instructions.md)).</span></span>

   ![Fenêtre Connexion à Azure avec l’option Connexion à l’appareil activée][I02]

1. <span data-ttu-id="12a97-116">Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.</span><span class="sxs-lookup"><span data-stu-id="12a97-116">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

1. <span data-ttu-id="12a97-118">Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12a97-118">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Navigateur de connexion à l’appareil][I04]

1. <span data-ttu-id="12a97-120">Pour finir, dans la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="12a97-120">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="12a97-122">Création de projet d’application web</span><span class="sxs-lookup"><span data-stu-id="12a97-122">Creating web app project</span></span>

1. <span data-ttu-id="12a97-123">Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique).</span><span class="sxs-lookup"><span data-stu-id="12a97-123">Click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="12a97-124">(si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)** , procédez comme suit : cliquez sur **File (Fichier)** , cliquez sur **New (Nouveau)** , sur **Project (Projet)...** , développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)** ).</span><span class="sxs-lookup"><span data-stu-id="12a97-124">(If you don't see **Dynamic Web Project** listed as an available project after clicking **File** and **New**, then do the following: click **File**, click **New**, click **Project...**, expand **Web**, click **Dynamic Web Project**, and click **Next**.)</span></span>

   ![Création d’un nouveau projet Web dynamique][file-new-dynamic-web-project]

2. <span data-ttu-id="12a97-126">Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="12a97-126">For purposes of this tutorial, name the project **MyWebApp**.</span></span> <span data-ttu-id="12a97-127">Votre écran se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="12a97-127">Your screen will appear similar to the following:</span></span>
   
   ![Propriétés Nouveau projet web dynamique][dynamic-web-project-properties]

3. <span data-ttu-id="12a97-129">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="12a97-129">Click **Finish**.</span></span>

4. <span data-ttu-id="12a97-130">Dans la vue Explorateur de projets d’Eclipse, développez **MyWebApp**.</span><span class="sxs-lookup"><span data-stu-id="12a97-130">Within Eclipse's Project Explorer view, expand **MyWebApp**.</span></span> <span data-ttu-id="12a97-131">Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)** , puis sur **JSP File (Fichier JSP)** .</span><span class="sxs-lookup"><span data-stu-id="12a97-131">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>

   ![Créer Nouveau fichier JSP][create-new-jsp-file]

5. <span data-ttu-id="12a97-133">Dans la boîte de dialogue **New JSP File** (Nouveau fichier JSP), nommez le fichier **index.jsp**, conservez le dossier parent en tant que **MyWebApp/WebContent**, puis cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="12a97-133">In the **New JSP File** dialog box, name the file **index.jsp**, keep the parent folder as **MyWebApp/WebContent**, and then click **Next**.</span></span>

   ![Boîte de dialogue New JSP File (Nouveau fichier JSP)][new-jsp-file-dialog]

6. <span data-ttu-id="12a97-135">Pour les besoins de ce didacticiel, dans la boîte de dialogue **Select JSP Template** (Sélectionner le modèle JSP), sélectionnez **New JSP File (html)** (Nouveau fichier JSP (html)) et cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="12a97-135">In the **Select JSP Template** dialog box, for purposes of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>

   ![Sélectionner un modèle JSP][select-jsp-template]

7. <span data-ttu-id="12a97-137">Quand votre fichier index.jsp s’ouvre dans Eclipse, ajoutez un texte pour afficher dynamiquement **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="12a97-137">When your index.jsp file opens in Eclipse, add in text to dynamically display **Hello World!**</span></span> <span data-ttu-id="12a97-138">dans l’élément `<body>` existant.</span><span class="sxs-lookup"><span data-stu-id="12a97-138">within the existing `<body>` element.</span></span> <span data-ttu-id="12a97-139">Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="12a97-139">Your updated `<body>` content should resemble the following example:</span></span>
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. <span data-ttu-id="12a97-140">Enregistrez index.jsp.</span><span class="sxs-lookup"><span data-stu-id="12a97-140">Save index.jsp.</span></span>

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="12a97-141">Déploiement d’application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="12a97-141">Deploying web app to Azure</span></span>

1. <span data-ttu-id="12a97-142">Dans la vue de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet, choisissez **Azure**, puis **Publish as Azure Web App** (Publier en tant qu’application web Azure).</span><span class="sxs-lookup"><span data-stu-id="12a97-142">Within Eclipse's Project Explorer view, right-click your project, choose **Azure**, and then choose **Publish as Azure Web App**.</span></span>
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. <span data-ttu-id="12a97-144">Lorsque la boîte de dialogue **Deploy Web App** (Déployer une application web) s’affiche, vous pouvez choisir l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="12a97-144">When the **Deploy Web App** dialog box appears, you can choose one of the following options:</span></span>

   * <span data-ttu-id="12a97-145">Sélectionnez une application web existante, s’il y en a.</span><span class="sxs-lookup"><span data-stu-id="12a97-145">Select an existing web app if one exists.</span></span>

      ![Sélectionner un App Service][select-app-service]

   * <span data-ttu-id="12a97-147">Cliquez sur **Create New Web App**.</span><span class="sxs-lookup"><span data-stu-id="12a97-147">Click **Create New Web App**.</span></span>

      ![Créer un App Service][create-app-service]

      <span data-ttu-id="12a97-149">Spécifiez les informations requises pour votre application web dans la boîte de dialogue **Créer App Service**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="12a97-149">Specify the requisite information for your web app in the **Create App Service** dialog box, and then click **Create**.</span></span>

      <span data-ttu-id="12a97-150">Ici, vous pouvez configurer l’environnement d’exécution, les paramètres de l’application, le plan de service et le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="12a97-150">Here you can configure the runtime environment, app settings, service plan and resource group.</span></span>

      ![Boîte de dialogue Créer App Service][create-app-service-dialog]

1. <span data-ttu-id="12a97-152">Sélectionnez votre application web, puis cliquez sur **Déployer**.</span><span class="sxs-lookup"><span data-stu-id="12a97-152">Select your web app and then click **Deploy**.</span></span>

   ![Déployer App Service][deploy-app-service]

1. <span data-ttu-id="12a97-154">Le Kit de ressources affiche un le statut **Published** (Publié) sous l’onglet **Azure Activity Log** lorsque le déploiement de votre application web a été effectué. Il s’agit d’un hyperlien pour l’URL de votre application web déployée.</span><span class="sxs-lookup"><span data-stu-id="12a97-154">The toolkit will display a **Published** status under the **Azure Activity Log** tab when it has successfully deployed your web app, which is a hyperlink for the URL of your deployed web app.</span></span>

   ![État de publication][publish-status]

1. <span data-ttu-id="12a97-156">Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.</span><span class="sxs-lookup"><span data-stu-id="12a97-156">You can browse to your web app using the link provided in the status message.</span></span>

   ![Accès à votre application web][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a><span data-ttu-id="12a97-158">Suppression des ressources</span><span class="sxs-lookup"><span data-stu-id="12a97-158">Cleaning up resources</span></span>

1. <span data-ttu-id="12a97-159">Après avoir publié votre application web sur Azure, vous pouvez la gérer en cliquant avec le bouton droit dans Azure Explorer et en sélectionnant l’une des options dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="12a97-159">After you have published your web app to Azure, you can manage it by right-clicking in Azure Explorer and selecting one of the options in the context menu.</span></span> <span data-ttu-id="12a97-160">Par exemple, vous pouvez **supprimer** votre application web ici afin de nettoyer la ressource pour ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="12a97-160">For example, you can **Delete** your web app here to clean up the resource for this tutorial.</span></span>

   ![Gérer App Service][manage-app-service]

## <a name="next-steps"></a><span data-ttu-id="12a97-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12a97-162">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<span data-ttu-id="12a97-163">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="12a97-163">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-eclipse-create-hello-world-web-app-legacy-version.md

<!-- IMG List -->
[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
