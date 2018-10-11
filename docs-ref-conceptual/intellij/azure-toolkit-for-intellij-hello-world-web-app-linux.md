---
title: Déployer une application web Hello World s’exécutant dans un conteneur Linux dans le cloud à l’aide du kit de ressources Azure pour IntelliJ
description: Exécutez une application web Hello World de base dans un conteneur Linux et déployez-la dans le cloud à l’aide du kit de ressources Azure pour IntelliJ.
services: app-service\web
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
ms.openlocfilehash: d281f37b027d4011ea2e3106990c5e45b69ebc88
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892590"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-intellij"></a>Déployer une application web Hello World sur un conteneur Linux dans le cloud à l’aide du kit de ressources Azure pour IntelliJ

Les conteneurs [Docker] constituent une méthode largement utilisée pour déployer des applications web. En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur. Le kit de ressources Azure pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités permettant de déployer des conteneurs sur Microsoft Azure.

Cet article décrit les étapes requises pour créer une application web Hello World basique et la publier dans un conteneur Linux sur Azure à l’aide du kit de ressources Azure pour IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]
* Un [Docker].

> [!NOTE]
>
> Pour effectuer les étapes de ce didacticiel, vous devez configurer [Docker] pour exposer le démon sur le port 2375 sans TLS. Vous pouvez configurer ce paramètre lors de l’installation de Docker ou via le menu des paramètres Docker.
>
> ![Menu des paramètres docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Créer un projet d’application web

1. Démarrez IntelliJ et connectez-vous à votre compte Azure en suivant les étapes indiquées dans l’article [Instructions de connexion pour le Kit de ressources Azure pour IntelliJ](https://docs.microsoft.com/java/azure/intellij/azure-toolkit-for-intellij-sign-in-instructions).

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

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Créer un Azure Container Registry à utiliser comme registre Docker privé

Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.

> [!NOTE]
>
> Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0][Create Docker Registry using Azure CLI].
>

1. Accédez au [portail Azure] et connectez-vous.

   Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créez un registre de conteneur Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.

1. Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Conteneurs** puis cliquez sur **Registre de conteneurs Azure**.
   
   ![Créer un registre de conteneurs Azure][AR01]

1. Quand la page d’informations pour le modèle de registre de conteneurs Azure s’affiche, cliquez sur **Créer**. 

   ![Créer un registre de conteneurs Azure][AR02]

1. Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. Une fois votre registre de conteneurs créé, accédez à celui-ci dans le portail Azure puis cliquez sur **Clés d’accès**. Notez le nom d’utilisateur et le mot de passe pour les étapes suivantes.

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Déployer votre application web dans un conteneur Docker

1. Cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Ajouter la prise en charge Docker**.

   Un fichier Docker est automatiquement créé avec une configuration par défaut.

   ![Ajouter la prise en charge Docker][add-docker-support]

1. Une fois que vous avez ajouté la prise en charge Docker, cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Exécuter sur l’application web (Linux)**.

   ![Exécuter sur l’application web (Linux)][run-on-web-app-linux]

1. Quand la boîte de dialogue **Exécuter sur l’application web (Linux)** s’affiche, entrez les informations requises :

   * **Nom** : spécifie le nom convivial qui s’affiche dans le kit de ressources Azure. 

   * **URL du serveur** : spécifie l’URL de votre registre de conteneurs déterminé dans la section précédente de cet article ; généralement elle utilise la syntaxe suivante : « *registre*.azurecr.io ». 

   * **Nom d’utilisateur** et **Mot de passe** : spécifie les clés d’accès de votre registre de conteneur déterminé dans la section précédente de cet article. 

   * **Image et étiquette** : spécifie le nom d’image du conteneur ; généralement il utilise la syntaxe suivante : « *registre*.azurecr.io/*nom_app*:latest », où : 
      * *registre* correspond au registre de conteneurs déterminé dans la section précédente de cet article, 
      * *nom_app* correspond au nom de votre application web. 

   * **Utiliser une application web existante** ou **Créer une application web** : spécifie si vous déployez votre conteneur dans une application web existante ou si vous en créez une. 

   * **Groupe de ressources** : spécifie si vous utilisez un groupe de ressources existant ou si vous en créez un. 

   * **Plan App Service** : spécifie si vous utilisez un plan App Service existant ou si vous en créez un. 

1. Quand vous avez terminé de configurer les paramètres indiqués ci-dessus, cliquez sur **Exécuter**.

   ![Créer une application web][create-web-app]

1. Une fois que vous avez publié votre application web, vos paramètres sont enregistrés comme valeur par défaut, et vous pouvez exécuter votre application sur Azure en cliquant sur l’icône en forme de flèche verte dans la barre d’outils. Vous pouvez modifier ces paramètres en cliquant sur le menu déroulant de votre application web, puis sur **Modifier les configurations**.

   ![Menu Modifier les configurations][edit-configuration-menu]

1. Quand la boîte de dialogue **ExécRun/Debug Configurations** s’affiche, vous pouvez modifier les paramètres par défaut de votre choix. Cliquez ensuite sur **OK**.

   ![Boîte de dialogue Edit configuration][edit-configuration-dialog]

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker][Docker] officiel.

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Portail Azure]: https://portal.azure.com/
[Créez un registre de conteneur Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[AR01]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR01.png
[AR02]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR02.png
[AR03]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR03.png
[AR04]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/AR04.png

[docker-settings-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/file-new-project.png
[maven-archetype-webapp]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-archetype-webapp.png
[groupid-and-artifactid]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/groupid-and-artifactid.png
[maven-options]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/maven-options.png
[project-name]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/project-name.png
[add-docker-support]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/add-docker-support.png
[run-on-web-app-linux]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/run-on-web-app-linux.png
[create-web-app]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/create-web-app.png
[edit-configuration-menu]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-menu.png
[edit-configuration-dialog]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/edit-configuration-dialog.png
[successfully-deployed]: media/azure-toolkit-for-intellij-hello-world-web-app-linux/successfully-deployed.png
