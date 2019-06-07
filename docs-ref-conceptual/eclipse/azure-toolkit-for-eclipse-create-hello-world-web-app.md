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
# <a name="create-a-hello-world-web-app-for-azure-app-service-using-eclipse"></a>Créer une application web Hello World pour Azure App Service à l’aide d’Eclipse

Avec le plug-in open source [Azure Toolkit for Eclipse](https://marketplace.eclipse.org/content/azure-toolkit-eclipse), la création et le déploiement d’une application Hello World de base sur Azure App Service en tant qu’application web ne prennent que quelques minutes.

> [!NOTE]
>
> Si vous préférez utiliser IntelliJ IDEA, consultez notre [tutoriel similaire pour IntelliJ][intellij-hello-world].
>
>[!INCLUDE [quickstarts-free-trial-note](../includes/quickstarts-free-trial-note.md)]
>
> N’oubliez pas de nettoyer les ressources après avoir terminé ce tutoriel. Dans ce cas, l’exécution de ce guide ne provoquera pas de dépassement du quota de votre compte gratuit.
>

[!INCLUDE [azure-toolkit-for-intellij-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="installation-and-sign-in"></a>Installation et connexion

1. Faites glisser le bouton suivant vers votre espace de travail Eclipse en cours d’exécution pour installer le plug-in Azure Toolkit for Eclipse ([autres options d’installation](azure-toolkit-for-eclipse-installation.md)).

    [![Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client")

1. Pour vous connecter à votre compte Azure, cliquez sur **Tools**, **Azure**, puis **Sign In**.
   ![Menu d’Eclipse pour la connexion à Azure][I01]

1. Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Connexion à l’appareil**, puis cliquez sur **Connexion** ([autres options de connexion](azure-toolkit-for-eclipse-sign-in-instructions.md)).

   ![Fenêtre Connexion à Azure avec l’option Connexion à l’appareil activée][I02]

1. Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.

   ![Boîte de dialogue Connexion à Azure][I03]

1. Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.

   ![Navigateur de connexion à l’appareil][I04]

1. Pour finir, dans la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][I05]

## <a name="creating-web-app-project"></a>Création de projet d’application web

1. Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique). (si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)** , procédez comme suit : cliquez sur **File (Fichier)** , cliquez sur **New (Nouveau)** , sur **Project (Projet)...** , développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)** ).

   ![Création d’un nouveau projet Web dynamique][file-new-dynamic-web-project]

2. Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**. Votre écran se présente comme suit :
   
   ![Propriétés Nouveau projet web dynamique][dynamic-web-project-properties]

3. Cliquez sur **Terminer**.

4. Dans la vue Explorateur de projets d’Eclipse, développez **MyWebApp**. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)** , puis sur **JSP File (Fichier JSP)** .

   ![Créer Nouveau fichier JSP][create-new-jsp-file]

5. Dans la boîte de dialogue **New JSP File** (Nouveau fichier JSP), nommez le fichier **index.jsp**, conservez le dossier parent en tant que **MyWebApp/WebContent**, puis cliquez sur **Next** (Suivant).

   ![Boîte de dialogue New JSP File (Nouveau fichier JSP)][new-jsp-file-dialog]

6. Pour les besoins de ce didacticiel, dans la boîte de dialogue **Select JSP Template** (Sélectionner le modèle JSP), sélectionnez **New JSP File (html)** (Nouveau fichier JSP (html)) et cliquez sur **Finish** (Terminer).

   ![Sélectionner un modèle JSP][select-jsp-template]

7. Quand votre fichier index.jsp s’ouvre dans Eclipse, ajoutez un texte pour afficher dynamiquement **Hello World!** dans l’élément `<body>` existant. Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Enregistrez index.jsp.

## <a name="deploying-web-app-to-azure"></a>Déploiement d’application web sur Azure

1. Dans la vue de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet, choisissez **Azure**, puis **Publish as Azure Web App** (Publier en tant qu’application web Azure).
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. Lorsque la boîte de dialogue **Deploy Web App** (Déployer une application web) s’affiche, vous pouvez choisir l’une des options suivantes :

   * Sélectionnez une application web existante, s’il y en a.

      ![Sélectionner un App Service][select-app-service]

   * Cliquez sur **Create New Web App**.

      ![Créer un App Service][create-app-service]

      Spécifiez les informations requises pour votre application web dans la boîte de dialogue **Créer App Service**, puis cliquez sur **Créer**.

      Ici, vous pouvez configurer l’environnement d’exécution, les paramètres de l’application, le plan de service et le groupe de ressources.

      ![Boîte de dialogue Créer App Service][create-app-service-dialog]

1. Sélectionnez votre application web, puis cliquez sur **Déployer**.

   ![Déployer App Service][deploy-app-service]

1. Le Kit de ressources affiche un le statut **Published** (Publié) sous l’onglet **Azure Activity Log** lorsque le déploiement de votre application web a été effectué. Il s’agit d’un hyperlien pour l’URL de votre application web déployée.

   ![État de publication][publish-status]

1. Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.

   ![Accès à votre application web][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="cleaning-up-resources"></a>Suppression des ressources

1. Après avoir publié votre application web sur Azure, vous pouvez la gérer en cliquant avec le bouton droit dans Azure Explorer et en sélectionnant l’une des options dans le menu contextuel. Par exemple, vous pouvez **supprimer** votre application web ici afin de nettoyer la ressource pour ce tutoriel.

   ![Gérer App Service][manage-app-service]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].

<!-- URL List -->

[Azure Toolkit for Eclipse]: azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
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
