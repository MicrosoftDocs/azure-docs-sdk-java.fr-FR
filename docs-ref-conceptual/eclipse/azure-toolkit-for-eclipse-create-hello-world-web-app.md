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
ms.openlocfilehash: 5e025c90c2619ec72ffddf5815fd49c3ac59c00f
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33883646"
---
# <a name="create-a-hello-world-web-app-for-azure-using-eclipse"></a>Créer une application web Hello World pour Azure à l’aide d’Eclipse

Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide du [Kit de ressources Azure pour Eclipse].

> [!NOTE]
>
> Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour IntelliJ], consultez [Créer une application web pour Azure à l’aide d’IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> Le Kit de ressources Azure pour Eclipse a été mis à jour en août 2017 avec un flux de travail différent. Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.7 (ou antérieure) du Kit de ressources Azure pour Eclipse. Si vous utilisez la version 3.0.6 (ou ultérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans Eclipse à l’aide de l’ancien kit de ressources][Legacy Version].
> 

À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :

![Version préliminaire de l’application Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Créer un projet d’application web

1. Démarrez Eclipse et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour Eclipse][instructions-connexion-eclipse].

1. Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique). (si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)**, procédez comme suit : cliquez sur **File (Fichier)**, cliquez sur **New (Nouveau)**, sur **Project (Projet)...**, développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)**).

   ![Création d’un nouveau projet Web dynamique][file-new-dynamic-web-project]

2. Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**. Votre écran se présente comme suit :
   
   ![Propriétés Nouveau projet web dynamique][dynamic-web-project-properties]

3. Cliquez sur **Terminer**.

4. Dans la vue Explorateur de projets d’Eclipse, développez **MyWebApp**. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.

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

## <a name="deploy-your-web-app-to-azure"></a>Déployer votre application web sur Azure

1. Dans la vue de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet, choisissez **Azure**, puis **Publish as Azure Web App** (Publier en tant qu’application web Azure).
   
   ![Publish as Azure Web App][publish-as-azure-web-app]

1. Lorsque la boîte de dialogue **Deploy Web App** (Déployer une application web) s’affiche, vous pouvez choisir l’une des options suivantes :

   * Sélectionnez une application web existante, s’il y en a.

      ![Sélectionner un App Service][select-app-service]

   * Cliquez sur **Create New Web App**.

      ![Créer un App Service][create-app-service]

      Spécifiez les informations requises pour votre application web dans la boîte de dialogue **Créer App Service**, puis cliquez sur **Créer**.

      ![Boîte de dialogue Créer App Service][create-app-service-dialog]

1. Sélectionnez votre application web, puis cliquez sur **Déployer**.

   ![Déployer App Service][deploy-app-service]

1. Le Kit de ressources affiche un le statut **Published** (Publié) sous l’onglet **Azure Activity Log** lorsque le déploiement de votre application web a été effectué. Il s’agit d’un hyperlien pour l’URL de votre application web déployée.

   ![État de publication][publish-status]

1. Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.

   ![Accès à votre application web][browse-web-app]

1. Après avoir publié votre application web sur Azure, vous pouvez la gérer en faisant un clic droit et en sélectionnant une des options dans le menu contextuel. Vous pouvez par exemple **Démarrer**, **Arrêter** ou **Supprimer** votre application web.

   ![Gérer App Service][manage-app-service]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
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
