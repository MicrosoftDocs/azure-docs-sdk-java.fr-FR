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
ms.openlocfilehash: 8b831f4545be9162d28f8ba86eb7271ffa4391af
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954740"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-eclipse"></a>Créer une application web Hello World pour Azure à l’aide de l’ancien kit de ressources pour Eclipse

Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide de la version 3.0.6 (ou ultérieure) du [Kit de ressources Azure pour Eclipse].

> [!NOTE]
>
> Pour obtenir une version de cet article qui utilise le [Kit de ressources Azure pour IntelliJ], consultez [Créer une application web pour Azure à l’aide d’IntelliJ][intellij-hello-world].
>

> [!IMPORTANT]
> 
> Le Kit de ressources Azure pour Eclipse a été mis à jour en août 2017 avec un flux de travail différent. Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour Eclipse. Si vous utilisez la version 3.0.7 (ou antérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans Eclipse][Updated Version].
>

À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :

![Version préliminaire de l’application Hello World][01]

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Créer un projet d’application web

1. Démarrez Eclipse et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour Eclipse][eclipse-sign-in-instructions].

1. Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique). (si **Dynamic Web Project (Projet web dynamique)** n’est pas répertorié en tant que projet disponible une fois que vous avez cliqué sur **File (Fichier)** et **New (Nouveau)**, procédez comme suit : cliquez sur **File (Fichier)**, cliquez sur **New (Nouveau)**, sur **Project (Projet)...**, développez **Web**, puis cliquez sur **Dynamic Web Project (Projet web dynamique)** et sur **Next (Suivant)**).

2. Pour l’exemple de ce didacticiel, nommez le projet **MyWebApp**. Votre écran se présente comme suit :
   
   ![Création d’un nouveau projet Web dynamique][02]

3. Cliquez sur **Terminer**.

4. Dans la vue **Explorateur de projets** d’Eclipse, développez **MyWebApp**. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.

5. Dans la boîte de dialogue **New JSP File** (Nouveau fichier JSP), nommez le fichier **index.jsp**, conservez le dossier parent en tant que **MyWebApp/WebContent**, puis cliquez sur **Next** (Suivant).

6. Pour les besoins de ce didacticiel, dans la boîte de dialogue **Select JSP Template** (Sélectionner le modèle JSP), sélectionnez **New JSP File (html)** (Nouveau fichier JSP (html)) et cliquez sur **Finish** (Terminer).

7. Quand votre fichier index.jsp s’ouvre dans Eclipse, ajoutez un texte pour afficher dynamiquement **Hello World!** dans l’élément `<body>` existant. Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :
   
   ```jsp
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

8. Enregistrez index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Déployer votre application web sur Azure

Vous pouvez déployer une application web Java sur Azure de plusieurs façons. Ce didacticiel décrit l’une des plus simples : votre application est déployée sur un conteneur d’application web Azure ; ainsi, aucun type de projet spécifique ni outil supplémentaire n’est nécessaire. Le JDK et le logiciel du conteneur web vous étant fournis par Azure, vous n’avez pas besoin de charger les vôtres ; vous devez uniquement être en possession de votre application web Java. Ainsi, le processus de publication de votre application ne prend que quelques secondes.

1. Dans l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur **MyWebApp**.

2. Dans le menu contextuel, sélectionnez **Azure**, puis cliquez sur **Publish as Azure Web App...** (Publier en tant qu’application web Azure...).
   
   ![Publish as Azure Web App][03]
   
   Sinon, lorsque votre projet d’application web est sélectionné dans l’Explorateur de projets, vous pouvez cliquer sur le bouton de liste déroulante **Publish** (Publier) sur la barre d’outils et sélectionner **Publish as Azure Web App** (Publier en tant qu’application web Azure...) à partir cet emplacement :
   
   ![Publish as Azure Web App][14]

3. Si vous n’êtes pas encore connecté à Azure à partir d’Eclipse, vous serez invité à vous connecter à votre compte Azure :
   
   ![Boîte de dialogue Connexion à Azure][04]
   
   Si vous avez plusieurs comptes Azure, certaines des invites du processus de connexion peuvent s’afficher plusieurs fois, même si elles semblent être identiques. Dans ce cas, continuez à suivre les instructions de connexion.

4. Une fois que vous êtes connecté à votre compte Azure, la boîte de dialogue **Gérer les abonnements** affiche la liste des abonnements associés à vos informations d’identification. Si plusieurs abonnements sont répertoriés et que vous ne souhaitez utiliser qu’une partie d’entre eux, vous pouvez éventuellement désélectionner ceux qui ne vous intéressent pas. Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.
   
   ![Boîte de dialogue Gestion des abonnements][05]

5. Quand la boîte de dialogue **Deploy to Azure Web App Container** (Déployer sur le conteneur d’application web Azure) s’affiche, elle présente tous les conteneurs d’application web déjà créés ; si vous n’avez pas créé de conteneur, la liste est vide.
   
   ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][06]

6. Si vous n’avez pas déjà créé de conteneur d’application web Azure ou que vous souhaitez publier votre application dans un nouveau conteneur, procédez comme suit. Sinon, sélectionnez un conteneur d’application web existant et passez à l’étape 7 ci-dessous.
   
   a. Cliquez sur **New...**
      
      ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][15]

   b. La boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web) s’affiche :
      
      ![Boîte de dialogue Nouveau conteneur d’application web][07a]

   c. Entrez un **nom DNS** pour votre conteneur d’application web ; celui-ci constitue le nom DNS feuille de l’URL hôte de votre application web dans Azure. (Le nom doit être disponible et conforme aux exigences d’affectation de noms pour les applications web Azure.)

   d. Dans le menu déroulant **Web Container** (Conteneur d’application), sélectionnez le logiciel approprié pour votre application.
      
      Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9. Une distribution récente du logiciel sélectionné sera fournie par Azure, et il s’exécutera sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.

   e. Dans le menu déroulant **Subscription** (Abonnement), sélectionnez l’abonnement à utiliser pour ce déploiement.

   f. Dans le menu déroulant **Resource Group** (Groupe de ressources), sélectionnez le groupe de ressources auquel vous souhaitez associer votre application web. (Les groupes de ressources Azure permettent de regrouper les ressources associées afin de pouvoir, par exemple, les supprimer simultanément.)
      
      Vous pouvez sélectionner un groupe de ressources existant (le cas échéant) et passer directement à l’étape G ou suivre les étapes ci-dessous pour créer un groupe de ressources :
      
      * Cliquez sur **New...**
      * La boîte de dialogue **New Resource Group** (Nouveau groupe de ressources) s’affiche :
        
          ![Boîte de dialogue Nouveau groupe de ressources][08]
      * Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau groupe de ressources.
      * Dans le menu déroulant **Region** (Région), sélectionnez l’emplacement de centre de données Azure approprié pour votre groupe de ressources.
      * FACULTATIF : par défaut, une distribution récente de Java 8 sera déployée automatiquement par Azure sur votre conteneur d’application web en tant que votre machine virtuelle Java. Vous pouvez cependant spécifier une version et une distribution de machine virtuelle Java différentes si votre application web l’exige. Pour spécifier le JDK de votre application web, cliquez sur l’onglet **JDK** et sélectionnez une des options suivantes :
         * **Deploy the default JDK offered by Azure Web Apps service**(Déployer le JDK par défaut offert par le service Azure Web Apps) : cette option déploiera une distribution récente de Java 8.
         * **Deploy a 3rd party JDK available on Azure**(Déployer un JDK tiers disponible sur Azure) : cette option vous permet de choisir dans la liste des JDK fournis par Microsoft Azure.
         * **Deploy my own JDK from this download location**(Déployer mon propre JDK à partir de cet emplacement de téléchargement) : cette option vous permet de spécifier votre propre distribution JDK, qui doit être fournie comme un fichier ZIP puis chargée vers un emplacement de téléchargement disponible publiquement ou un compte de stockage Azure auquel lequel vous avez accès.
          
         ![Boîte de dialogue Nouveau conteneur d’application web][07b]

   g. Cliquez sur **OK**.

   h. Le menu déroulant **App Service Plan** (Plan de Service d’application) répertorie les plans de service d’application qui sont associés au groupe de ressources que vous avez sélectionné. (Les plans App Service spécifient des informations telles que l’emplacement de votre application web, le niveau tarifaire et la taille d’instance de calcul. Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)
      
       You can select an existing App Service Plan (if you have any) and skip to step h below, or use the following these steps to create a new App Service Plan:
      
      * Cliquez sur **New...**
      * La boîte de dialogue **New App Service Plan** (Nouveau plan de Service d’application) s’affiche :
        
          ![Boîte de dialogue Nouveau plan App Service][09]
      * Dans la zone de texte **Name** (Nom), spécifiez un nom pour votre nouveau plan de service d’application.
      * Dans le menu déroulant **Location** (Emplacement), sélectionnez l’emplacement de centre de données Azure approprié pour le plan.
      * Dans le menu déroulant **Pricing Tier** (Niveau de tarification), sélectionnez la tarification appropriée pour le plan. À des fins de test, vous pouvez choisir **Free**(Gratuit).
      * Dans le menu déroulant **Instance Size** (Taille de l’instance), sélectionnez la taille d’instance appropriée pour le plan. À des fins de test, vous pouvez choisir **Small**(Petite).

   i. Une fois effectuées toutes les étapes ci-dessus, la boîte de dialogue New Web App Container doit ressembler à ceci :
      
      ![Boîte de dialogue Nouveau conteneur d’application web][10]

   j. Cliquez sur **OK** pour terminer la création de votre conteneur d’application web.
       
      Attendez quelques secondes pour que la liste des conteneurs d’application web s’actualise. Votre conteneur d’application web nouvellement créée doit maintenant être sélectionné dans la liste.

7. Vous êtes maintenant prêt à lancer le déploiement initial de votre application web sur Azure :
   
   ![Boîte de dialogue Déployer sur le conteneur d’application web Azure][11]
   
   Cliquez sur **OK** pour déployer votre application Java sur le conteneur d’application web sélectionné.
   
   Par défaut, votre application est déployée en tant que sous-répertoire du serveur d’applications. Si vous voulez qu’elle soit déployée en tant qu’application racine, cochez la case **Deploy to root** (Déployer sur la racine) avant de cliquer sur **OK**.

8. Ensuite, la vue **Journaux d’activité** doit apparaître et indiquer l’état du déploiement de votre application web.
   
   ![Journaux d’activité][12]
   
   Le processus de déploiement de votre application web sur Azure doit prendre seulement quelques secondes. Quand votre application est prête, un lien nommé **Publié** in the **État** . Quand vous cliquez sur le lien, vous êtes redirigé vers la page d’accueil de votre application web déployée.

## <a name="updating-your-web-app"></a>Mise à jour de votre application web

La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :

* Vous pouvez mettre à jour le déploiement d’une application web Java existante.
* Vous pouvez publier une application Java supplémentaire dans le même conteneur d’application web.

Dans les deux cas, le processus est identique et ne prend que quelques secondes :

1. Dans l’Explorateur de projets Eclipse, cliquez avec le bouton droit sur l’application Java que vous souhaitez mettre à jour ou ajouter à un conteneur d’application web existant.

2. Lorsque le menu contextuel s’affiche, sélectionnez **Azure** puis **Publish as Azure Web App...** (Publier en tant qu’application Web Azure...).

3. Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît. Sélectionnez celui dans lequel vous souhaitez publier ou republier votre application Java, puis cliquez sur **OK**.

Quelques secondes plus tard, le **Journal des activités Azure** affiche votre déploiement mis à jour comme **publié** et êtes en mesure de vérifier votre application mise à jour dans un navigateur web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Démarrage, arrêt ou redémarrage d’une application web existante

Pour démarrer ou arrêter un conteneur d’application web Azure existant (y compris toutes les applications Java déployées dans celui-ci), vous pouvez utiliser la vue **Explorateur Azure** .

Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : cliquez sur **Window** (Fenêtre) dans le menu d’Eclipse, puis cliquez successivement sur **Show View** (Afficher la vue), **Other...** (Autre...), **Azure** et **Explorateur Azure**. Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.

Quand l’ **Explorateur Azure** s’affiche, procédez comme suit pour démarrer ou arrêter votre application web : 

1. Développez le nœud **Azure** .

2. Développez le nœud **Web Apps** (Applications web). 

3. Cliquez avec le bouton droit sur l’application web souhaitée.

4. Quand le menu contextuel s’affiche, cliquez sur **Démarrer**, **Arrêter** ou **Redémarrer**. Les options de menu étant sensibles au contexte, vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.
   
   ![Arrêt d’une application web existante][13]

## <a name="next-steps"></a>étapes suivantes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[intellij-hello-world]: ../intellij/azure-toolkit-for-intellij-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
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
