---
title: Créer une application web Hello World pour Azure App Service à l’aide d’IntelliJ
description: Ce didacticiel vous montre comment utiliser le Kit de ressources Azure pour IntelliJ pour créer une application web Hello World pour Azure.
services: app-service
keywords: java, intellij, application web, azure app service, hello world, démarrage rapide
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
ms.openlocfilehash: ae0749ce1ddab971f1a83e2e5e58492fd8ccb287
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626120"
---
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a><span data-ttu-id="bd2a1-104">Créer une application web Hello World pour Azure App Service à l’aide d’IntelliJ</span><span class="sxs-lookup"><span data-stu-id="bd2a1-104">Create a Hello World web app for Azure App Service using IntelliJ</span></span>

<span data-ttu-id="bd2a1-105">Grâce au plug-in open source [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053), la création et le déploiement d’une application Hello World de base sur Azure App Service en tant qu’application web ne prennent que quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-105">Using open sourced [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) plugin, creating and deploying a basic Hello World application to Azure App Service as a web app can be done in a few minutes.</span></span>

> [!NOTE]
>
> <span data-ttu-id="bd2a1-106">Si vous préférez utiliser Eclipse, consultez notre [tutoriel similaire pour Eclipse][eclipse-hello-world].</span><span class="sxs-lookup"><span data-stu-id="bd2a1-106">If you prefer using Eclipse, check out our [similar tutorial for Eclipse][eclipse-hello-world].</span></span>
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> <span data-ttu-id="bd2a1-107">N’oubliez pas de nettoyer les ressources après avoir terminé ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-107">Don't forget to clean up the resources after you complete this tutorial.</span></span> <span data-ttu-id="bd2a1-108">Dans ce cas, l’exécution de ce guide ne provoquera pas de dépassement du quota de votre compte gratuit.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-108">In that case, running this guide will not exceed your free account quota.</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a><span data-ttu-id="bd2a1-109">Installation et connexion</span><span class="sxs-lookup"><span data-stu-id="bd2a1-109">Installation and Sign-in</span></span>

1. <span data-ttu-id="bd2a1-110">Dans la boîte de dialogue Settings/Preferences d’IntelliJ IDEA (Ctrl+Alt+S), sélectionnez **Plugins**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-110">In IntelliJ IDEA's Settings/Preferences dialog (Ctrl+Alt+S), select **Plugins**.</span></span> <span data-ttu-id="bd2a1-111">Ensuite, recherchez **Azure Toolkit for IntelliJ** sur la **Place de marché** et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-111">Then, find the **Azure Toolkit for IntelliJ** in the **Marketplace** and click **Install**.</span></span> <span data-ttu-id="bd2a1-112">Une fois l’installation terminée, cliquez sur **Redémarrer** pour activer le plug-in.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-112">After installed, click **Restart** to activate the plugin.</span></span> 

   ![Plug-in Azure Toolkit for IntelliJ sur la Place de marché][marketplace]

2. <span data-ttu-id="bd2a1-114">Pour vous connecter à votre compte Azure, ouvrez la barre latérale **Azure Explorer**, puis cliquez sur l’icône **Connexion à Azure** dans la barre en haut (ou dans le menu IDEA **Tools/Azure/Azure Sign in**).</span><span class="sxs-lookup"><span data-stu-id="bd2a1-114">To sign in to your Azure account, open sidebar **Azure Explorer**, and then click the **Azure Sign In** icon in the bar on top (or from IDEA menu **Tools/Azure/Azure Sign in**).</span></span>

   ![Commande IntelliJ de connexion à Azure][I01]

3. <span data-ttu-id="bd2a1-116">Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Connexion à l’appareil**, puis cliquez sur **Connexion** ([autres options de connexion](azure-toolkit-for-intellij-sign-in-instructions.md)).</span><span class="sxs-lookup"><span data-stu-id="bd2a1-116">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in** ([other sign in options](azure-toolkit-for-intellij-sign-in-instructions.md)).</span></span>

   ![Fenêtre Connexion à Azure avec l’option Connexion à l’appareil activée][I02]

4. <span data-ttu-id="bd2a1-118">Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-118">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

5. <span data-ttu-id="bd2a1-120">Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-120">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Navigateur de connexion à l’appareil][I04]

6. <span data-ttu-id="bd2a1-122">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-122">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I05]

## <a name="creating-web-app-project"></a><span data-ttu-id="bd2a1-124">Création de projet d’application web</span><span class="sxs-lookup"><span data-stu-id="bd2a1-124">Creating web app project</span></span>

1. <span data-ttu-id="bd2a1-125">Dans IntelliJ, cliquez sur le menu **File**, sur **New**, puis sur **Project**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-125">In IntelliJ, click the **File** menu, then click **New**, and then click **Project**.</span></span>

   ![Créer un projet][file-new-project]

2. <span data-ttu-id="bd2a1-127">Dans la boîte de dialogue **New Project**, sélectionnez **Maven**, puis **maven-archetype-webapp**, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-127">In the **New Project** dialog box, select **Maven**, then **maven-archetype-webapp**, and then click **Next**.</span></span>

   ![Choisir une application web d’archétype Maven][maven-archetype-webapp]

3. <span data-ttu-id="bd2a1-129">Spécifiez les valeurs **GroupId** et **ArtifactId** pour votre application web, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-129">Specify the **GroupId** and **ArtifactId** for your web app, and then click **Next**.</span></span>

   ![Spécifier GroupId et ArtifactId][groupid-and-artifactid]

4. <span data-ttu-id="bd2a1-131">Personnalisez les paramètres Maven ou acceptez les valeurs par défaut, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-131">Customize any Maven settings or accept the defaults, and then click **Next**.</span></span>

   ![Spécifier les paramètres Maven][maven-options]

5. <span data-ttu-id="bd2a1-133">Spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-133">Specify your project name and location, and then click **Finish**.</span></span>

   ![Spécifier le nom du projet][project-name]

6. <span data-ttu-id="bd2a1-135">Sous la vue de l’Explorateur de projets, ouvrez et modifiez le fichier **src/main/webapp/index.jsp** comme suit et **enregistrez les modifications** :</span><span class="sxs-lookup"><span data-stu-id="bd2a1-135">Under Project Explorer view, open and edit the file **src/main/webapp/index.jsp** as following and **save the changes**:</span></span>

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Modifier la page d’index][edit-index-page]

## <a name="deploying-web-app-to-azure"></a><span data-ttu-id="bd2a1-137">Déploiement d’application web sur Azure</span><span class="sxs-lookup"><span data-stu-id="bd2a1-137">Deploying web app to Azure</span></span>

1. <span data-ttu-id="bd2a1-138">Sous la vue de l’Explorateur de projets, cliquez avec le bouton droit sur votre projet, développez **Azure**, puis cliquez sur **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-138">Under Project Explorer view, right-click your project, expand **Azure**, then click **Deploy to Azure**.</span></span>

   ![Menu Deploy to Azure][deploy-to-azure-menu]

1. <span data-ttu-id="bd2a1-140">Dans la boîte de dialogue Deploy to Azure, vous pouvez directement déployer l’application sur une application Web Tomcat existante si vous en avez déjà une. Sinon, vous devez tout d’abord en créer une.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-140">In the Deploy to Azure dialog box, you can directly deploy the application to an existing Tomcat webapp if you already have one, otherwise you should create a new one first.</span></span>
   1. <span data-ttu-id="bd2a1-141">Cliquez sur le lien **No Available webapp, click to create a new one** (Aucune application web disponible, cliquez pour en créer une) afin de créer une nouvelle application web. Vous pouvez choisir **Create New WebApp** dans la liste déroulante WebApp s’il existe des applications web dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-141">Click the link **No Available webapp, click to create a new one** to crete a new web app, you could choose **Create New WebApp** from WebApp dropdown if there are existing webapps in your subscription.</span></span>

      ![Boîte de dialogue Deploy to Azure][deploy-to-azure-dialog]

   1. <span data-ttu-id="bd2a1-143">Dans la boîte de dialogue contextuelle, choisissez **TOMCAT 8.5-jre8** en tant que conteneur web et spécifiez les autres informations requises, puis cliquez sur **OK** pour créer l’application web.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-143">In the pop-up dialog box, chose **TOMCAT 8.5-jre8** as Web Container and specify other required information, then click **OK** to create the webapp.</span></span>

      ![Créer une application web][create-new-web-app-dialog]

   1. <span data-ttu-id="bd2a1-145">Choisissez l’application web dans la liste déroulante WebApp, puis cliquez sur **Run**. (Vous pouvez commencer ici si vous souhaitez déployer vers une application web existante.)</span><span class="sxs-lookup"><span data-stu-id="bd2a1-145">Choose the web app from WebApp drop down, and then click **Run**.(You could start from here if you want deploy to an existing webapp)</span></span>

      ![Déployer vers une application web existante][deploy-to-existing-webapp]

1. <span data-ttu-id="bd2a1-147">Le Kit de ressources affiche un message d’état une fois qu’il a réussi à déployer votre application web, avec l’URL de votre application web déployée en cas de succès.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-147">The toolkit will display a status message when it has successfully deployed your web app, along with the URL of your deployed web app if succeed.</span></span>

   ![Déploiement réussi][successfully-deployed]

1. <span data-ttu-id="bd2a1-149">Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-149">You can browse to your web app using the link provided in the status message.</span></span>

   ![Accès à votre application web][browse-web-app]

## <a name="managing-deploy-configurations"></a><span data-ttu-id="bd2a1-151">Gestion des configurations de déploiement</span><span class="sxs-lookup"><span data-stu-id="bd2a1-151">Managing deploy configurations</span></span>

1. <span data-ttu-id="bd2a1-152">Une fois que vous avez publié votre application web, vos paramètres sont enregistrés comme valeur par défaut, et vous pouvez exécuter le déploiement en cliquant sur l’icône en forme de flèche verte dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-152">After you have published your web app, your settings will be saved as the default, and you can run the deployment by clicking the green arrow icon on the toolbar.</span></span> <span data-ttu-id="bd2a1-153">Vous pouvez modifier vos paramètres en cliquant sur le menu déroulant de votre application web, puis sur **Edit Configurations**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-153">You can modify your settings by clicking the drop-down menu for your web app and click **Edit Configurations**.</span></span>

   ![Menu Edit Configurations][edit-configuration-menu]

1. <span data-ttu-id="bd2a1-155">Quand la boîte de dialogue **Run/Debug Configurations** s’affiche, vous pouvez modifier les paramètres par défaut de votre choix. Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd2a1-155">When the **Run/Debug Configurations** dialog box is displayed, you can modify any of the default settings, and then click **OK**.</span></span>

   ![Boîte de dialogue Edit configuration][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a><span data-ttu-id="bd2a1-157">Suppression des ressources</span><span class="sxs-lookup"><span data-stu-id="bd2a1-157">Cleaning up resources</span></span>

1. <span data-ttu-id="bd2a1-158">Suppression des applications web dans Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="bd2a1-158">Deleting Web Apps in Azure Explorer</span></span>

     ![Nettoyer les ressources][clean-resources]

## <a name="next-steps"></a><span data-ttu-id="bd2a1-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd2a1-160">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<span data-ttu-id="bd2a1-161">Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].</span><span class="sxs-lookup"><span data-stu-id="bd2a1-161">For additional information about creating Azure Web Apps, see the [Web Apps Overview].</span></span>

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Web Apps Overview]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Legacy Version]: azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->
[marketplace]:./media/azure-toolkit-for-intellij-create-hello-world-web-app/marketplace.png
[file-new-project]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/file-new-project.png
[maven-archetype-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-archetype-webapp.png
[groupid-and-artifactid]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/groupid-and-artifactid.png
[maven-options]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/maven-options.png
[project-name]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/project-name.png
[open-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/open-index-page.png
[edit-index-page]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-index-page.png
[deploy-to-azure-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-menu.png
[deploy-to-azure-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/run-on-web-app-dialog.png
[deploy-to-existing-webapp]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/deploy-to-existing-webapp.png
[create-new-web-app-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/create-new-web-app-dialog.png
[successfully-deployed]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/successfully-deployed.png
[browse-web-app]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/browse-web-app.png
[edit-configuration-menu]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-menu.png
[edit-configuration-dialog]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/edit-configuration-dialog.png
[clean-resources]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app/clean-resource.png
[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-intellij-sign-in-instructions/I05.png
