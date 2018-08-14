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
# <a name="create-a-hello-world-web-app-for-azure-using-intellij"></a>Créer une application web Hello World pour Azure à l’aide d’IntelliJ

Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide du [Kit de ressources Azure pour IntelliJ].

> [!NOTE]
>
> Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour Eclipse], consultez [Créer une application web pour Azure à l’aide d’Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> Le Kit de ressources Azure pour IntelliJ a été mis à jour en août 2017 avec un flux de travail différent. Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.7 (ou antérieure) du Kit de ressources Azure pour IntelliJ. Si vous utilisez la version 3.0.6 (ou ultérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans IntelliJ à l’aide de l’ancien kit de ressources][Legacy Version].
> 

À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :

![Version préliminaire de l’application Hello World][browse-web-app]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Créer un projet d’application web

1. Démarrez IntelliJ et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour IntelliJ][intelliJ-sign-in-instructions].

1. Cliquez sur le menu **File**, sur **New**, puis sur **Project**.
   
   ![Créer un projet][file-new-project]

1. Dans la boîte de dialogue **New Project**, sélectionnez **Maven**, puis **maven-archetype-webapp**, puis cliquez sur **Next**.
   
   ![Choisir une application web d’archétype Maven][maven-archetype-webapp]
   
1. Spécifiez les valeurs **GroupId** et **ArtifactId** pour votre application web, puis cliquez sur **Next**.
   
   ![Spécifier GroupId et ArtifactId][groupid-and-artifactid]

1. Personnalisez les paramètres Maven ou acceptez les valeurs par défaut, puis cliquez sur **Next**.
   
   ![Spécifier les paramètres Maven][maven-options]

1. Spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish**.
   
   ![Spécifier le nom du projet][project-name]

1. Dans la vue de l’Explorateur de projets d’IntelliJ, développez **src**, **main**, puis **webapp**, puis double-cliquez sur **index.jsp**.
   
   ![Ouvrir la page d’index][open-index-page]

1. Quand votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez un texte pour afficher dynamiquement **Hello World!** dans l’élément `<body>` existant. Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ``` 

   ![Modifier la page d’index][edit-index-page]

1. Enregistrez index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Déployer votre application web sur Azure

1. Dans la vue de l’Explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur votre projet, choisissez **Azure**, puis **Run on Web App**.
   
   ![Menu Run on Web App][run-on-web-app-menu]

1. Dans la boîte de dialogue Run on Web App, vous pouvez choisir l’une des options suivantes :

   * Choisissez une application web existante (le cas échéant), puis cliquez sur **Run**.

      ![Boîte de dialogue Run on Web App][run-on-web-app-dialog]

   * Cliquez sur **Create New Web App**. Si vous choisissez de créer une application web, spécifiez les informations requises pour votre application web, puis cliquez sur **Run**.

      ![Créer une application web][create-new-web-app-dialog]

1. Le Kit de ressources affiche un message d’état une fois qu’il a réussi à déployer votre application web, avec l’URL de votre application web déployée.

   ![Déploiement réussi][successfully-deployed]

1. Vous pouvez accéder à votre application web à l’aide du lien fourni dans le message d’état.

   ![Accès à votre application web][browse-web-app]

1. Une fois que vous avez publié votre application web, vos paramètres sont enregistrés comme valeur par défaut, et vous pouvez exécuter votre application sur Azure en cliquant sur l’icône en forme de flèche verte dans la barre d’outils. Vous pouvez modifier vos paramètres en cliquant sur le menu déroulant de votre application web, puis sur **Edit Configurations**.

   ![Menu Edit Configurations][edit-configuration-menu]

1. Quand la boîte de dialogue **ExécRun/Debug Configurations** s’affiche, vous pouvez modifier les paramètres par défaut de votre choix. Cliquez ensuite sur **OK**.

   ![Boîte de dialogue Edit configuration][edit-configuration-dialog]

## <a name="next-steps"></a>étapes suivantes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].

<!-- URL List -->

[Kit de ressources Azure pour IntelliJ]: azure-toolkit-for-intellij.md
[Kit de ressources Azure pour Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
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
