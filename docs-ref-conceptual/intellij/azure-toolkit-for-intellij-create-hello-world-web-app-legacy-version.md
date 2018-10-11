---
title: Créer une application web Hello World pour Azure à l’aide de l’ancien kit de ressources pour IntelliJ
description: Ce didacticiel vous montre comment utiliser la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour IntelliJ pour créer une application web Hello World pour Azure.
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
ms.openlocfilehash: efc1dffa248987772827bbe7bc0caa9f10a0b4ef
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893391"
---
# <a name="create-a-hello-world-web-app-for-azure-using-the-legacy-toolkit-for-intellij"></a>Créer une application web Hello World pour Azure à l’aide de l’ancien kit de ressources pour IntelliJ

Ce didacticiel explique comment créer une application Hello World de base et la déployer sur Azure en tant qu’application web à l’aide de la version 3.0.6 (ou ultérieure) du [Kit de ressources Azure pour IntelliJ].

> [!NOTE]
>
> Pour obtenir une version de cet article qui utilise le [boîte à outils Azure pour Eclipse], consultez [Créer une application web pour Azure à l’aide d’Eclipse][eclipse-hello-world].
>

> [!IMPORTANT]
> 
> Le Kit de ressources Azure pour IntelliJ a été mis à jour en août 2017 avec un flux de travail différent. Cet article illustre la création d’une application web Hello World à l’aide de la version 3.0.6 (ou ultérieure) du Kit de ressources Azure pour IntelliJ. Si vous utilisez la version 3.0.7 (ou antérieure) du kit de ressources, vous devez suivre les étapes de l’article [Créer une application web Hello World pour Azure dans IntelliJ][Updated Version].
>

À la fin de ce didacticiel, votre application ressemble à l’illustration suivante quand vous l’affichez dans un navigateur web :

![Version préliminaire de l’application Hello World][01]

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="create-a-new-web-app-project"></a>Créer un projet d’application web

1. Démarrez IntelliJ et connectez-vous à votre compte Azure en suivant les instructions indiquées dans l’article [Instructions de connexion Azure pour le Kit de ressources Azure pour IntelliJ][intelliJ-sign-in-instructions].

1. Cliquez sur le menu **File**, sur **New**, puis sur **Project**.
   
   ![Fichier Nouveau Projet][02]

2. Dans la boîte de dialogue **New Project**, sélectionnez **Java**, **Web Application**, puis cliquez sur **New**.
   
   ![Boîte de dialogue Nouveau projet][03a]
   
3. Dans Sélection du répertoire de base pour la boîte de dialogue JDK, sélectionnez le dossier où est installé votre JDK, puis cliquez sur **OK**. Cliquez sur **Suivant** dans la boîte de dialogue Nouveau projet pour continuer.
   
   ![Spécifiez le répertoire de base du JDK][03b]

4. Pour les besoins de ce didacticiel, nommez le projet **Java-Web-App-On-Azure**, puis cliquez sur **Finish** (Terminer).
   
   ![Boîte de dialogue Nouveau projet][04]

5. Dans l’affichage de l’explorateur de projets d’IntelliJ, développez **Java-Web-App-On-Azure**, puis développez **web** et double-cliquez sur **index.jsp**.
   
   ![Page Ouvrir l’index][05c]

6. Quand votre fichier index.jsp s’ouvre dans IntelliJ, ajoutez un texte pour afficher dynamiquement **Hello World!** dans l’élément `<body>` existant. Le contenu `<body>` mis à jour doit ressembler à l’exemple suivant :
   
   ```java
   <body><b><% out.println("Hello World!"); %></b></body>
   ```

7. Enregistrez index.jsp.

## <a name="deploy-your-web-app-to-azure"></a>Déployer votre application web sur Azure

Vous pouvez déployer une application web Java sur Azure de plusieurs façons. Ce didacticiel décrit l’une des plus simples : votre application est déployée sur un conteneur d’application web Azure ; ainsi, aucun type de projet spécifique ni outil supplémentaire n’est nécessaire. Le JDK et le logiciel du conteneur web vous étant fournis par Azure, vous n’avez pas besoin de charger les vôtres ; vous devez uniquement être en possession de votre application web Java. Ainsi, le processus de publication de votre application ne prend que quelques secondes.

Avant de publier votre application, vous devez d’abord configurer vos paramètres de module. Pour ce faire, procédez comme suit :

1. Dans l’explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur le projet **Java-Web-App-On-Azure** . Quand le menu contextuel s’affiche, cliquez sur **Open Module Settings**(Ouvrir les paramètres du module).

   ![Ouvrir les paramètres du module][05a]

2. Lorsque la boîte de dialogue Structure de projet s’affiche :

   a. Cliquez sur **Artefacts** dans la liste des **Paramètres du projet**.

   b. Modifiez le nom de l’artefact dans la zone **Nom** pour qu’il ne contienne pas d’espaces blancs ou des caractères spéciaux. Cela est nécessaire dans la mesure où le nom est utilisé dans l’URI.

   c. Définissez le **Type** sur **Web Application: Archive** (Application Web : Archive).

   d. Cliquez sur **OK** pour fermer la boîte de dialogue Structure de projet.

   ![Ouvrir les paramètres du module][05b]

Lorsque vous avez configuré vos paramètres de module, vous pouvez publier votre application dans Azure à l’aide de la procédure suivante :

1. Dans l’explorateur de projets d’IntelliJ, cliquez avec le bouton droit sur le projet **Java-Web-App-On-Azure** . Quand le menu contextuel apparaît, sélectionnez **Azure**, puis cliquez sur **Publish as Azure Web App...** (Publier comme application web Azure...).
   
   ![Menu contextuel de publication Azure][06]

2. Si vous n’êtes pas encore connecté à Azure à partir d’IntelliJ, vous êtes invité à vous connecter à votre compte Azure. (Si vous avez plusieurs comptes Azure, certaines des invites du processus de connexion peuvent s’afficher plusieurs fois, même si elles semblent être identiques. Dans ce cas, continuez à suivre les instructions de connexion.)
   
   ![Boîte de dialogue de connexion à Azure][07]

3. Une fois que vous êtes connecté à votre compte Azure, la boîte de dialogue **Gérer les abonnements** affiche la liste des abonnements associés à vos informations d’identification. Si plusieurs abonnements sont répertoriés et que vous ne souhaitez utiliser qu’une partie d’entre eux, vous pouvez éventuellement désélectionner ceux qui ne vous intéressent pas. Quand vous avez sélectionné vos abonnements, cliquez sur **Fermer**.
   
   ![Gérer les abonnements][08]

4. Quand la boîte de dialogue **Deploy to Azure Web App Container** (Déployer sur le conteneur d’application web Azure) s’affiche, elle présente tous les conteneurs d’application web déjà créés ; si vous n’avez pas créé de conteneur, la liste est vide.
   
   ![Conteneurs d’applications][09]

5. Si vous n’avez pas déjà créé de conteneur d’application web Azure ou que vous souhaitez publier votre application dans un nouveau conteneur, procédez comme suit. Sinon, sélectionnez un conteneur d’application web existant et passez à l’étape 6 ci-dessous.
   
   a. Cliquez sur le signe **+**.
      
      ![Ajouter un conteneur d’application][10]

   b. La boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web) s’affiche, que nous allons utiliser au cours des prochaines étapes.
      
      ![Nouveau conteneur d’application][11a]
   
   c. Entrez un **nom DNS** pour votre conteneur d’application web ; celui-ci constitue le nom DNS feuille de l’URL hôte de votre application web dans Azure. Le nom doit être disponible et conforme aux exigences d’affectation de noms pour les applications web Azure.

   d. Dans le menu déroulant **Web Container** (Conteneur d’application), sélectionnez le logiciel approprié pour votre application.
      
      Pour le moment, vous pouvez choisir entre Tomcat 8, Tomcat 7 ou Jetty 9. Une distribution récente du logiciel sélectionné sera fournie par Azure, et il s’exécutera sur une distribution récente de JDK 8 créée par Oracle et fournie par Azure.

   e. Dans le menu déroulant **Subscription** (Abonnement), sélectionnez l’abonnement à utiliser pour ce déploiement.

   f. Dans le menu déroulant **Resource Group** (Groupe de ressources), sélectionnez le groupe de ressources auquel vous souhaitez associer votre application web. (Les groupes de ressources Azure permettent de regrouper les ressources associées afin de pouvoir, par exemple, les supprimer simultanément.)
      
      Vous pouvez sélectionner un groupe de ressources existant (le cas échéant) et passer directement à l’étape G ou suivre les étapes ci-dessous pour créer un groupe de ressources :
      
      * Sélectionnez **&lt;&lt; Créer un groupe de ressources &gt;&gt;** dans le menu déroulant **Groupe de ressources**.
      * La boîte de dialogue **New Resource Group** (Nouveau groupe de ressources) s’affiche :
        
         ![Nouveau groupe de ressources][12]

      * Dans la zone de texte **Name**, spécifiez un nom pour votre nouveau groupe de ressources.
      * Dans le menu déroulant **Region**, sélectionnez l’emplacement de centre de données Azure approprié pour votre groupe de ressources.
      * Cliquez sur **OK**.

   g. Le menu déroulant **App Service Plan** (Plan de Service d’application) répertorie les plans de service d’application qui sont associés au groupe de ressources que vous avez sélectionné. (Un plan App Service spécifie des informations telles que l’emplacement de votre application web, le niveau tarifaire et la taille d’instance de calcul.) Un seul plan App Service peut être utilisé pour plusieurs Web Apps. Pour cette raison, il est stocké séparément d’un déploiement d’application web spécifique.)
      
      Vous pouvez sélectionner un plan App Services existant (le cas échéant) et passer directement à l’étape H ou suivre les étapes ci-dessous pour créer un plan App Service :
      
      * Sélectionnez **&lt;&lt; Créer un plan App Service&gt;&gt;** dans le menu déroulant **Plan App Service**.
      * La boîte de dialogue **New App Service Plan** (Nouveau plan de Service d’application) s’affiche :
        
         ![Nouveau plan App Service][13]

      * Dans la zone de texte **Name**, spécifiez un nom pour votre nouveau plan App Service.
      * Dans le menu déroulant **Location**, sélectionnez l’emplacement de centre de données Azure approprié pour le plan.
      * Dans le menu déroulant **Pricing Tier**, sélectionnez la tarification appropriée pour le plan. À des fins de test, vous pouvez choisir **Free**(Gratuit).
      * Dans le menu déroulant **Instance Size**, sélectionnez la taille d’instance appropriée pour le plan. À des fins de test, vous pouvez choisir **Small**(Petite).
      * Cliquez sur **OK**.

   h. (Facultatif) Par défaut, une distribution récente de Java 8 sera déployée automatiquement par Azure sur votre conteneur d’application web en tant que machine virtuelle Java. Vous pouvez cependant sélectionner une version et une distribution de machine virtuelle Java différentes. Pour ce faire, procédez comme suit :
      
   * Cliquez sur l’onglet **JDK** dans la boîte de dialogue **New Web App Container** (Nouveau conteneur d’application web).
   * Vous pouvez choisir l’une des options suivantes :
        
      * Déployer le JDK proposé par défaut par Azure
      * Déployer un JDK tiers à partir d’une liste déroulante de JDK supplémentaires disponibles sur Azure
      * Déployer un JDK personnalisé, qui doit être empaqueté dans un fichier ZIP et accessible au public ou dans votre compte de stockage Azure
        
     ![Onglet JDK du nouveau conteneur d’application][11b]

   i. Une fois effectuées toutes les étapes ci-dessus, la boîte de dialogue New Web App Container doit ressembler à ceci :
      
      ![Nouveau conteneur d’application][14]
   
   j. Cliquez sur **OK** pour terminer la création de votre conteneur d’application web.
       
      Attendez quelques secondes pour que la liste des conteneurs d’application web s’actualise. Votre conteneur d’application web nouvellement créée doit maintenant être sélectionné dans la liste.

6. Vous êtes maintenant prêt à effectuer le déploiement initial de votre application web dans Azure ; cliquez sur **OK** pour déployer votre application Java sur le conteneur d’application web sélectionné. Par défaut, votre application est déployée en tant que sous-répertoire du serveur d’applications. Si vous voulez qu’elle soit déployée en tant qu’application racine, cochez la case **Deploy to root** (Déployer sur la racine) avant de cliquer sur **OK**.
   
   ![Déploiement sur Azure][15]

7. Ensuite, la vue **Journaux d’activité** doit apparaître et indiquer l’état du déploiement de votre application web.
   
   ![Indicateur de progression][16]
   
   Le processus de déploiement de votre application web sur Azure doit prendre seulement quelques secondes. Quand votre application est prête, un lien nommé **Publié** dans la colonne **État** apparaît. Quand vous cliquez sur le lien, vous êtes redirigé vers la page d’accueil de votre application web déployée, à laquelle vous pouvez accéder en suivant les étapes de la section suivante.

## <a name="browsing-to-your-web-app-on-azure"></a>Accès à votre application web sur Azure

Pour accéder à votre application web sur Azure, vous pouvez utiliser la vue **Explorateur Azure**.

Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : dans IntelliJ, cliquez sur le menu **View** (Affichage), sur **Tool Windows** (Fenêtres des outils), puis sur **Service Explorer** (Explorateur de services). Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.

Quand l’**Explorateur Azure** s’affiche, effectuez les étapes suivantes pour accéder à votre application web : 

1. Développez le nœud **Azure** .
2. Développez le nœud **Web Apps** (Applications web). 
3. Cliquez avec le bouton droit sur l’application web souhaitée.
4. Quand le menu contextuel s’affiche, cliquez sur **Open in Browser**(Ouvrir dans un navigateur).
   
   ![Parcourir l’application web][17]

## <a name="updating-your-web-app"></a>Mise à jour de votre application web

La mise à jour d’une application web Azure existante en cours d’exécution est un processus simple et rapide, que vous pouvez effectuer de deux façons :

* Vous pouvez mettre à jour le déploiement d’une application web Java existante.
* Vous pouvez publier une application Java supplémentaire dans le même conteneur d’application web.

Dans les deux cas, le processus est identique et ne prend que quelques secondes :

1. Dans l’Explorateur de projets IntelliJ, cliquez avec le bouton droit sur l’application Java que vous souhaitez mettre à jour ou ajouter à un conteneur d’application web existant.
2. Lorsque le menu contextuel s’affiche, sélectionnez **Azure** puis **Publish as Azure Web App...** (Publier en tant qu’application Web Azure...).
3. Comme vous vous êtes déjà connecté, la liste de vos conteneurs d’application web existants apparaît. Sélectionnez celui dans lequel vous souhaitez publier ou republier votre application Java, puis cliquez sur **OK**.

Quelques secondes plus tard, le **Journal des activités Azure** affiche votre déploiement mis à jour comme **publié** et êtes en mesure de vérifier votre application mise à jour dans un navigateur web.

## <a name="starting-stopping-or-restarting-an-existing-web-app"></a>Démarrage, arrêt ou redémarrage d’une application web existante

Pour démarrer ou arrêter un conteneur d’application web Azure existant (y compris toutes les applications Java déployées dans celui-ci), vous pouvez utiliser la vue **Explorateur Azure** .

Si la vue **Explorateur Azure** n’est pas déjà ouverte, procédez comme suit : dans IntelliJ, cliquez sur le menu **View** (Affichage), sur **Tool Windows** (Fenêtres des outils), puis sur **Service Explorer** (Explorateur de services). Si vous ne vous êtes pas déjà connecté, vous êtes invité à le faire.

Quand l’**Explorateur Azure** s’affiche, effectuez les étapes suivantes pour démarrer ou arrêter votre application web : 

1. Développez le nœud **Azure** .
2. Développez le nœud **Web Apps** (Applications web). 
3. Cliquez avec le bouton droit sur l’application web souhaitée.
4. Quand le menu contextuel s’affiche, cliquez sur **Démarrer**, **Arrêter** ou **Redémarrer**. Les options de menu étant sensibles au contexte, vous pouvez uniquement arrêter une application web en cours d’exécution ou démarrer une application web qui n’est pas en cours d’exécution.
   
   ![Arrêter l’application Web][18]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

Pour plus d’informations sur la création d’Azure Web Apps, consultez la [Vue d’ensemble de Web Apps].

<!-- URL List -->

[Kit de ressources Azure pour IntelliJ]: azure-toolkit-for-intellij.md
[boîte à outils Azure pour Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md
[eclipse-hello-world]: ../eclipse/azure-toolkit-for-eclipse-create-hello-world-web-app.md
[Vue d’ensemble de Web Apps]: /azure/app-service/app-service-web-overview
[Apache Tomcat]: http://tomcat.apache.org/
[Jetty]: http://www.eclipse.org/jetty/
[Updated Version]: azure-toolkit-for-intellij-create-hello-world-web-app.md
[intelliJ-sign-in-instructions]: azure-toolkit-for-intellij-sign-in-instructions.md

<!-- IMG List -->

[01]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/01-Web-Page.png
[02]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/02-File-New-Project.png
[03a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-Dialog.png
[03b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/03-New-Project-SDK-Dialog.png
[04]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/04-New-Project-Dialog.png
[05a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Module-Settings.png
[05b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Project-Structure-Dialog.png
[05c]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/05-Open-Index-Page.png
[06]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/06-Azure-Publish-Context-Menu.png
[07]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/07-Azure-Log-In-Dialog.png
[08]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/08-Manage-Subscriptions.png
[09]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/09-App-Containers.png
[10]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/10-Add-App-Container.png
[11a]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container.png
[11b]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/11-New-App-Container-JDK-Tab.png
[12]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/12-New-Resource-Group.png
[13]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/13-New-App-Service-Plan.png
[14]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/14-New-App-Container.png
[15]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/15-Deploy-To-Azure.png
[16]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/16-Progress-Indicator.png
[17]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/17-Browse-Web-App.png
[18]: ./media/azure-toolkit-for-intellij-create-hello-world-web-app-legacy-version/18-Stop-Web-App.png
