---
title: Publier une application Spring Boot en tant que conteneur Docker avec le kit de ressources Azure pour Eclipse
description: Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: c116e0712afd8e48983f946f43eddfd0c79c0ba8
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38075471"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publier une application Spring Boot en tant que conteneur Docker avec le kit de ressources Azure pour Eclipse

L’[Spring Framework] est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. Un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.

[Docker] est une solution open source qui aide les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.

Ce didacticiel détaille la marche à suivre pour déployer une application Spring Boot en tant que conteneur Docker vers Microsoft Azure à l’aide du kit de ressources Azure pour Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>Cloner le référentiel Docker Spring Boot par défaut

### <a name="import-the-public-repository"></a>Importer le référentiel public

Les étapes suivantes détaillent les étapes du clonage du référentiel Spring Boot Docker sur votre ordinateur local à l’aide d’IntelliJ. Si vous voulez utiliser une ligne de commande, voir [Déployer une application Spring Boot sur Linux dans Azure Container Service][Deploy Spring Boot on Linux in AKS].

1. Ouvrez Eclipse.

1. Cliquez sur **Fichier** > **Importer**.

   ![Menu Importer fichier][CL01]

1. Lorsque la boîte de dialogue **Importer** s’ouvre :

   a. Développez **Git**.

   b. Sélectionnez **Projets de Git**.
   
   c. Cliquez sur **Suivant**.

   ![Boîte de dialogue Importer][CL02]

1. Sur la page **Sélectionner une source de référentiel** :

   a. Sélectionnez **Cloner l’URI**.
   
   b. Cliquez sur **Suivant**.

   ![Sélectionner la page source du référentiel][CL03]

1. Sur la page **Référentiel Git source** :

   a. Pour **URI**, entrez `https://github.com/spring-guides/gs-spring-boot-docker.git`. Cette étape devrait compléter automatiquement les champs **Hôte** et **Chemin d’accès du référentiel** avec les valeurs appropriées.
   
   b. Le référentiel Spring Boot est public. Vous n’avez donc pas à entrer vos identifiants Git.
   
   c. Cliquez sur **Suivant**.

   ![Page du référentiel Git source][CL04]

1. Dans la page **Sélection de la branche**, cliquez sur **Suivant**.

   ![Page Sélection de la branche][CL05]

1. Sur la page **Destination locale** :

   a. Spécifiez le dossier local où vous souhaitez placer votre référentiel local.
   
   b. Cliquez sur **Suivant**.

   ![Page Destination locale][CL06]

1. Sur la page **Sélectionner un assistant pour l’importation de projets** :

   a. Sélectionnez **Importer en tant que projet général**.
   
   b. Cliquez sur **Suivant**.

   ![Page « Sélectionner un assistant pour l’importation de projets »][CL07]

1. Sur la page **Importer des projets** :

   a. Spécifiez le nom de votre projet.
   
   b. Cliquez sur **Terminer**.

   ![Page Importer des projets][CL08]

1. Une fois le référentiel cloné avec succès, tous les fichiers répertoriés dans Eclipse sont visibles.

   ![Référentiel local][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Créer un projet Maven à partir de votre référentiel local

Le référentiel Spring Boot Docker contient un projet Maven terminé à utiliser pour ce didacticiel. 

1. Cliquez sur **Fichier** > **Importer**.

   ![Commande Importer du menu Fichier][CL01]

1. Lorsque la boîte de dialogue **Importer** s’ouvre :

   a. Développez **Maven**.
   
   b. Sélectionnez **Projets Maven existants**.
   
   c. Cliquez sur **Suivant**.

   ![Boîte de dialogue Importer][MV01]

1. Sur la page **Projets Maven** :

   a. Pour **Répertoire racine**, spécifiez le dossier **complete** dans votre référentiel local.
   
   b. Développez la section **Avancé**, puis entrez un nom personnalisé dans le champ **Modèle de nom**.
   
   c. Activez la case à cocher pour le fichier **pom.xml** dans le projet.
   
   d. Cliquez sur **Terminer**.

   ![Page Projets Maven][MV02]

1. Une fois le projet Maven ouvert, vous pouvez voir un deuxième projet répertorié dans Eclipse.

   ![Projet Maven local][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Générer votre application Spring Boot à l’aide de Maven

1. Dans l’explorateur de projets d’Eclipse, sélectionnez le projet Maven.

1. Cliquez sur **Exécuter** > **Exécuter en tant que** > **build Maven**.

   ![Commandes pour exécuter en tant que build Maven][BU01]

1. Une fois votre application générée, la fenêtre de console affiche l’état.

   ![Build Maven réussie][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publier votre application web sur Azure en utilisant un conteneur Docker

1. Dans l’explorateur de projets d’Eclipse, sélectionnez le projet Maven.

1. Cliquez sur le menu Azure **Publier**, puis sur **Publier en tant que conteneur Docker**.

   ![Commande Publier en tant que conteneur Docker][PU01]

1. Lorsque la boîte de dialogue **Déploiement de conteneur Docker sur Azure** s’affiche :

   a. Entrez un nom d’image Docker personnalisé.
   
   b. Pour **Artefact à déployer**, spécifiez le chemin d’accès au fichier **gs-spring-boot-docker-0.1.0.jar** que vous venez de créer.

   ![Spécifiez les options Docker][PU02]

   Tous les hôtes Docker existants s’affichent. 

1. Si vous choisissez d’effectuer le déploiement sur un hôte existant, vous pouvez passer à l’étape 5. Autrement, procédez comme suit pour créer un hôte :

   a. Cliquez sur **Add**.

      ![Ajouter un nouvel hôte Docker][PU03]

   b. Quand la boîte de dialogue **Create Docker Host** (Créer un hôte Docker) apparaît, vous pouvez accepter les valeurs par défaut ou spécifier divers paramètres personnalisés pour votre nouvel hôte Docker (pour des descriptions détaillées des différents paramètres, voir [Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ][Publish Container with Azure Toolkit]). Cliquez sur **Next** une fois que vous avez spécifié les paramètres à utiliser.

      ![Spécifier les options de l’hôte Docker][PU04]

   c. Vous pouvez utiliser des identifiants de connexion existants d’un coffre de clés Azure, ou entrer de nouveaux identifiants de connexion Docker. Cliquez sur **Finish** une fois que vous avez spécifié vos options.

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU05]

1. Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.

   ![Sélectionner l’hôte Docker à utiliser][PU06]

1. Dans la dernière page de la boîte de dialogue **Déploiement de conteneur Docker sur Azure**, vous devez spécifier les options suivantes :

   a. Vous pouvez spécifier un nom personnalisé pour le conteneur qui doit héberger votre conteneur Docker, ou accepter le nom par défaut.

   b. Entrez les ports TCP de votre hôte Docker en utilisant la syntaxe suivante : «  *[port externe]*:*[port interne]*. Par exemple, dans **80:8080**, 80 est un port externe et 8080 le port interne par défaut de Spring Boot.
   
      Si vous avez personnalisé le port interne (par exemple, en modifiant le fichier application.yml), vous devez spécifier le numéro de port pour que le routage dans Azure soit correct.

   c. Après avoir configuré ces options, cliquez sur **Terminer**.

   ![Déployer un conteneur Docker dans Azure][PU07]

1. Une fois que le kit de ressources Azure a terminé la publication, le journal d’activité d’Azure affiche le statut **Publié**.

   ![Déploiement réussi de l’hôte Docker][PU08]

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des ressources supplémentaires pour Docker, consultez le [Site web de Docker](https://www.docker.com/).

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: azure-toolkit-for-eclipse-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
