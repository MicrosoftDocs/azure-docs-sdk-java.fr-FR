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
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-intellij"></a>Créer une application web Hello World pour Azure App Service à l’aide d’IntelliJ

Grâce au plug-in open source [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053), la création et le déploiement d’une application Hello World de base sur Azure App Service en tant qu’application web ne prennent que quelques minutes.

> [!NOTE]
>
> Si vous préférez utiliser Eclipse, consultez notre [tutoriel similaire pour Eclipse][eclipse-hello-world].
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> N’oubliez pas de nettoyer les ressources après avoir terminé ce tutoriel. Dans ce cas, l’exécution de ce guide ne provoquera pas de dépassement du quota de votre compte gratuit.
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-intellij-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a>Installation et connexion

1. Dans la boîte de dialogue Settings/Preferences d’IntelliJ IDEA (Ctrl+Alt+S), sélectionnez **Plugins**. Ensuite, recherchez **Azure Toolkit for IntelliJ** sur la **Place de marché** et cliquez sur **Installer**. Une fois l’installation terminée, cliquez sur **Redémarrer** pour activer le plug-in. 

   ![Plug-in Azure Toolkit for IntelliJ sur la Place de marché][marketplace]

2. Pour vous connecter à votre compte Azure, ouvrez la barre latérale **Azure Explorer**, puis cliquez sur l’icône **Connexion à Azure** dans la barre en haut (ou dans le menu IDEA **Tools/Azure/Azure Sign in**).

   ![Commande IntelliJ de connexion à Azure][I01]

3. Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Connexion à l’appareil**, puis cliquez sur **Connexion** ([autres options de connexion](azure-toolkit-for-intellij-sign-in-instructions.md)).

   ![Fenêtre Connexion à Azure avec l’option Connexion à l’appareil activée][I02]

4. Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.

   ![Boîte de dialogue Connexion à Azure][I03]

5. Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.

   ![Navigateur de connexion à l’appareil][I04]

6. Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][I05]

## <a name="creating-web-app-project"></a>Création de projet d’application web

1. Dans IntelliJ, cliquez sur le menu **File**, sur **New**, puis sur **Project**.

   ![Créer un projet][file-new-project]

2. Dans la boîte de dialogue **New Project**, sélectionnez **Maven**, puis **maven-archetype-webapp**, puis cliquez sur **Next**.

   ![Choisir une application web d’archétype Maven][maven-archetype-webapp]

3. Spécifiez les valeurs **GroupId** et **ArtifactId** pour votre application web, puis cliquez sur **Next**.

   ![Spécifier GroupId et ArtifactId][groupid-and-artifactid]

4. Personnalisez les paramètres Maven ou acceptez les valeurs par défaut, puis cliquez sur **Next**.

   ![Spécifier les paramètres Maven][maven-options]

5. Spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish**.

   ![Spécifier le nom du projet][project-name]

6. Sous la vue de l’Explorateur de projets, ouvrez et modifiez le fichier **src/main/webapp/index.jsp** comme suit et **enregistrez les modifications** :

   ```html
   <html>
    <body>
      <b><% out.println("Hello World!"); %></b>
    </body>
   </html>
   ```

   ![Modifier la page d’index][edit-index-page]

## <a name="deploying-web-app-to-azure"></a>Déploiement d’application web sur Azure

1. Sous la vue de l’Explorateur de projets, cliquez avec le bouton droit sur votre projet, développez **Azure**, puis cliquez sur **Deploy to Azure**.

   ![Menu Deploy to Azure][deploy-to-azure-menu]

1. Dans la boîte de dialogue Deploy to Azure, vous pouvez directement déployer l’application sur une application Web Tomcat existante si vous en avez déjà une. Sinon, vous devez tout d’abord en créer une.
   1. Cliquez sur le lien **No Available webapp, click to create a new one** (Aucune application web disponible, cliquez pour en créer une) afin de créer une nouvelle application web. Vous pouvez choisir **Create New WebApp** dans la liste déroulante WebApp s’il existe des applications web dans votre abonnement.

      ![Boîte de dialogue Deploy to Azure][deploy-to-azure-dialog]

   1. Dans la boîte de dialogue contextuelle, choisissez **TOMCAT 8.5-jre8** en tant que conteneur web et spécifiez les autres informations requises, puis cliquez sur **OK** pour créer l’application web.

      ![Créer une application web][create-new-web-app-dialog]

   1. Choisissez l’application web dans la liste déroulante WebApp, puis cliquez sur **Run**. (Vous pouvez commencer ici si vous souhaitez déployer vers une application web existante.)

      ![Déployer vers une application web existante][deploy-to-existing-webapp]

1. Le Kit de ressources affiche un message d’état une fois qu’il a réussi à déployer votre application web, avec l’URL de votre application web déployée en cas de succès.

   ![Déploiement réussi][successfully-deployed]

1. Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.

   ![Accès à votre application web][browse-web-app]

## <a name="managing-deploy-configurations"></a>Gestion des configurations de déploiement

1. Une fois que vous avez publié votre application web, vos paramètres sont enregistrés comme valeur par défaut, et vous pouvez exécuter le déploiement en cliquant sur l’icône en forme de flèche verte dans la barre d’outils. Vous pouvez modifier vos paramètres en cliquant sur le menu déroulant de votre application web, puis sur **Edit Configurations**.

   ![Menu Edit Configurations][edit-configuration-menu]

1. Quand la boîte de dialogue **Run/Debug Configurations** s’affiche, vous pouvez modifier les paramètres par défaut de votre choix. Cliquez ensuite sur **OK**.

   ![Boîte de dialogue Edit configuration][edit-configuration-dialog]

## <a name="cleaning-up-resources"></a>Suppression des ressources

1. Suppression des applications web dans Azure Explorer

     ![Nettoyer les ressources][clean-resources]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].

<!-- URL List -->

[Azure Toolkit for IntelliJ]: azure-toolkit-for-intellij.md
[Azure Toolkit for Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
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
