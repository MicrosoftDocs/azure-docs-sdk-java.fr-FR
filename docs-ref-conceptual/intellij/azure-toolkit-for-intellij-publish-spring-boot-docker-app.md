---
title: "Publier une application Spring Boot en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ"
description: "Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 94042f388be503975990eca62d8ee0e0e35b89d2
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publier une application Spring Boot en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ

L’[infrastructure Spring] est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. Un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.

[Docker] est une solution open source qui aide les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.

Ce didacticiel détaille la marche à suivre pour déployer une application Spring Boot en tant que conteneur Docker vers Microsoft Azure à l’aide du kit de ressources Azure pour IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Cloner le référentiel Docker Spring Boot par défaut

Les étapes suivantes détaillent la procédure de clonage du référentiel Docker Spring Boot à l’aide d’IntelliJ. Si vous voulez utiliser une ligne de commande, voir [Déployer une application Spring Boot sur Linux dans Azure Container Service][Deploy Spring Boot on Linux in ACS].

1. Ouvrez IntelliJ.

1. Dans l’écran d’accueil, dans la liste **Check out from version control** (Extraire à partir de la gestion de version), sélectionnez **GitHub**.

   ![Option GitHub pour le contrôle de version][CL01]

1. Si vous êtes invité à vous connecter, entrez vos informations d’identification.

   * Si vous utilisez un nom d’utilisateur/mot de passe pour vous connecter à GitHub : 

      ![Boîte de dialogue pour la saisie du nom d’utilisateur et du mot de passe GitHub][CL02a]

   * Si vous utilisez un jeton pour vous connecter à GitHub : 

      ![Boîte de dialogue pour la saisie d’un jeton GitHub][CL02b]

1. Entrez **https://github.com/spring-guides/gs-spring-boot-docker.git** pour l’URL du référentiel, spécifiez les informations de votre chemin d’accès local et du dossier, puis cliquez sur **Cloner**.

   ![Boîte de dialogue Cloner le référentiel][CL03]

1. Lorsque vous êtes invité à créer un projet IntelliJ, sélectionnez **Non**.

   ![Refus de créer un projet IntelliJ][CL04]

1. Dans la page d'accueil, cliquez sur **Import Project** (Importer un projet).

   ![Choix d’importer un projet][CL05]

1. Recherchez le chemin d’accès de l’emplacement où vous avez cloné le référentiel Spring Boot, sélectionnez le dossier **complete** sous la racine, puis cliquez sur **OK**.

   ![Sélectionner un dossier pour l’importation][CL06]

1. Lorsque vous y êtes invité, sélectionnez **Create project from existing sources** (Créer un projet à partir de sources existantes).

   ![Option pour créer un projet à partir de sources existantes][CL07]

1. Spécifiez le nom de votre projet ou acceptez le nom par défaut, vérifiez que le chemin du dossier **complete** est correct, puis cliquez sur **Suivant**.

   ![Spécifier le nom du projet][CL08]

1. Personnalisez les répertoires pour l’importation, puis cliquez sur **Next**.

   ![Choisir des répertoires][CL09]

1. Passez en revue les bibliothèques à importer, puis cliquez sur **Next**.

   ![Passer en revue les bibliothèques de projet][CL10]

1. Passez en revue la structure des modules, puis cliquez sur **Next**.

   ![Passer en revue la structure des modules][CL11]

1. Spécifiez votre JDK, puis cliquez sur **Next**.

   ![Spécifier un JDK][CL12]

1. Cliquez sur **Terminer**.

   ![Bouton Terminer][CL13]

IntelliJ importe l’application Spring Boot en tant que projet, et affiche la structure une fois l’importation terminée.

![Application Spring Boot dans IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Générer votre application Spring Boot

### <a name="build-the-app-by-using-the-maven-pom"></a>Générer l’application à l’aide du fichier POM Maven

1. Si la fenêtre de l’outil Maven n’est pas ouverte, ouvrez-la. Cliquez sur **View (Affichage)** > **Tool Windows (Fenêtre Outil)** > **Maven Projects (Projets Maven)**.

   ![Commandes Fenêtres Outil et Projets Maven][BU01]

1. Dans la fenêtre Outil de Maven, cliquez avec le bouton droit sur **package**, puis choisissez **Run Maven Build** (Exécuter la build Maven) (si votre projet Maven ne s’affiche pas automatiquement, cliquez sur l’icône **Réimporter** dans la barre d’outils de Maven).

   ![Commande Run Maven Build][BU02]

1. Une fois votre application Spring Boot créée, IntelliJ doit afficher le message **BUILD SUCCESS** (GÉNÉRATION RÉUSSIE).

   ![Message BUILD SUCCESS][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Créer un artefact prêt pour le déploiement

Pour publier votre application Spring Boot, vous devrez créer un artefact prêt pour le déploiement. Procédez comme suit :

1. Ouvrez votre projet d’application web dans IntelliJ.

1. Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.

   ![Commande Project Structure][ART01]

1. Cliquez sur le signe plus de couleur verte (**+**) pour ajouter un artefact, cliquez sur **JAR**, puis sur **Empty** (Vide).

   ![Ajouter un artefact][ART02]

1. Nommez votre artefact tout en prenant garde à ne pas ajouter l’extension « .jar », puis spécifiez le dossier cible pour la sortie Maven.

   ![Spécifier les propriétés de l’artefact][ART03]

1. Créez un manifeste pour votre artefact (facultatif) :

   a. Cliquez sur **Create Manifest** (Créer un manifeste).

      ![Cliquer sur le bouton Create Manifest][ART04a]

   b. Choisissez le chemin par défaut pour l’artefact, puis cliquez sur **OK**.

      ![Spécifier le chemin de l’artefact][ART04b]

   c. Cliquez sur les points de suspension (**...**) pour localiser la classe principale.

      ![Localiser la classe principale][ART04c]

   d. Choisissez votre classe principale, puis cliquez sur **OK**.

      ![Spécifier la classe principale][ART04d]

1. Cliquez sur **OK**.

   ![Fermer la boîte de dialogue Project Structure][ART05]

> [!NOTE]
> Pour plus d’informations sur la création d’artefacts dans IntelliJ, consultez [Configuring Artifacts] (Configuration des artefacts) sur le site web JetBrains.
>

### <a name="build-the-artifact-for-deployment"></a>Générer l’artefact pour le déploiement

1. Cliquez sur **Build** (Générer), puis sur **Artifacts** (Artefacts).

   ![Commande Build Artifacts][BU04]

1. Quand le menu contextuel **Build Artifact** (Générer un artefact) s’affiche, cliquez sur **Build** (Générer).

   ![Menu contextuel Build Artifact][BU05]

IntelliJ doit afficher l’artefact terminé pour votre application Spring Boot dans la fenêtre Outil du projet.

   ![Artefact créé][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publier votre application web sur Azure en utilisant un conteneur Docker

1. Si vous ne vous êtes pas connecté à votre compte Azure, procédez de la manière décrite dans [Instructions de connexion pour le Kit de ressources Azure pour IntelliJ][Azure Sign In for IntelliJ].

1. Dans la fenêtre Outil d’exploration de projets, cliquez avec le bouton droit sur le projet, puis sélectionnez **Azure** > **Publish as Docker Container** (Publier en tant que conteneur Docker).

   ![Commande Publish as Docker Container][PU01]

1. Quand la boîte de dialogue **Deploy Docker Container on Azure** (Déployer un conteneur Docker sur Azure) apparaît, tous les hôtes Docker existants sont affichés. Si vous choisissez d’effectuer le déploiement dans un hôte existant, vous pouvez passer directement à l’étape 4. Autrement, procédez comme suit pour créer un hôte :

   a. Cliquez sur le signe plus de couleur verte (**+**).

      ![Ajouter un nouvel hôte Docker][PU02]

   b. Quand la boîte de dialogue **Create Docker Host** (Créer un hôte Docker) apparaît, vous pouvez accepter les valeurs par défaut ou spécifier divers paramètres personnalisés pour votre nouvel hôte Docker (pour des descriptions détaillées des différents paramètres, voir [Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ][Publish Container with Azure Toolkit]). Cliquez sur **Next** une fois que vous avez spécifié les paramètres à utiliser.

      ![Spécifier les options de l’hôte Docker][PU03a]

   c. Vous pouvez utiliser des identifiants de connexion existants d’un coffre de clés Azure, ou entrer de nouveaux identifiants de connexion Docker. Cliquez sur **Finish** une fois que vous avez spécifié vos options.

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU03b]

1. Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.

   ![Sélectionner l’hôte Docker à utiliser][PU04]

1. Dans la dernière page de la boîte de dialogue **Deploy Docker Container on Azure** (Déployer un conteneur Docker sur Azure), spécifiez les options suivantes :

   a. Vous pouvez spécifier un nom personnalisé pour le conteneur qui doit héberger votre conteneur Docker, ou accepter le nom par défaut.

   b. Entrez les ports TCP de votre hôte Docker en utilisant la syntaxe suivante : « *[port externe]*:*[port interne]*. Par exemple, dans **80:8080**, 80 est un port externe et 8080 le port interne par défaut de Spring Boot.
   
      Si vous avez personnalisé le port interne (par exemple, en modifiant le fichier application.yml), vous devez spécifier le numéro de port pour que le routage dans Azure soit correct.

   c. Après avoir configuré ces options, cliquez sur **Terminer**.

   ![Déployer un conteneur Docker dans Azure][PU05]

1. Une fois que le kit de ressources Azure a terminé la publication, le journal d’activité d’Azure affiche le statut **Publié**.

   ![Déploiement réussi de l’hôte Docker][PU06]

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur les autres méthodes permettant de créer des applications Spring Boot à l’aide d’IntelliJ, voir [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) (Création de projets Spring Boot) sur le site web de JetBrains.

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuration des artefacts)
[Deploy Spring Boot on Linux in ACS]:/azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
