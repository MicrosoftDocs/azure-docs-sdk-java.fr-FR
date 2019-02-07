---
title: Déployer une application web Hello World s’exécutant dans un conteneur Linux dans le cloud à l’aide d’Azure Toolkit for Eclipse
description: Exécutez une application web Hello World de base dans un conteneur Linux et déployez-la dans le cloud à l’aide d’Azure Toolkit for Eclipse.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/20/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 799f21a282956f9a88aa35743157fc1292197569
ms.sourcegitcommit: 54e7f077d694a5b1dd7fa6c8870b7d476af9829c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/02/2019
ms.locfileid: "55649245"
---
# <a name="deploy-a-hello-world-web-app-to-a-linux-container-in-the-cloud-using-the-azure-toolkit-for-eclipse"></a>Déployer une application web Hello World sur un conteneur Linux dans le cloud à l’aide d’Azure Toolkit for Eclipse

Les conteneurs [Docker] constituent une méthode largement utilisée pour déployer des applications web. En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur. Azure Toolkit for Eclipse simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités permettant de déployer des conteneurs sur Microsoft Azure.

Cet article décrit les étapes à suivre pour créer une application web Hello World de base et la publier dans un conteneur Linux sur Azure à l’aide d’Azure Toolkit for Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]
* Un client [Docker].

> [!NOTE]
>
> Pour effectuer les étapes de ce didacticiel, vous devez configurer [Docker] pour exposer le démon sur le port 2375 sans TLS. Vous pouvez configurer ce paramètre lors de l’installation de Docker ou via le menu des paramètres Docker.
>
> ![Menu des paramètres docker][docker-settings-menu]
>

## <a name="create-a-new-web-app-project"></a>Créer un projet d’application web

1. Démarrez Eclipse et connectez-vous à votre compte Azure en suivant les étapes de l’article [Instructions de connexion pour Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).

1. Cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique).
   
   ![Créer un projet][file-new-project]

1. Dans la boîte de dialogue **New Dynamic Web Project** (Nouveau projet web dynamique) spécifiez le nom et l’emplacement de votre projet, puis cliquez sur **Finish** (Terminer).
   
   ![Spécifier le nom du projet][project-name]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Créer un Azure Container Registry à utiliser comme registre Docker privé

Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.

> [!NOTE]
>
> Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0][Create Docker Registry using Azure CLI].
>

1. Accédez au [portail Azure] et connectez-vous.

   Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créer un registre de conteneurs Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.

1. Cliquez sur l’icône de menu pour **+ Créer une ressource**, cliquez sur **Conteneurs**, puis sur **Registre de conteneurs**.
   
   ![Créer un registre de conteneurs Azure][create-container-registry-01]

1. Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.

   ![Configurer les paramètres du registre de conteneurs Azure][create-container-registry-02]

## <a name="deploy-your-web-app-in-a-docker-container"></a>Déployer votre application web dans un conteneur Docker

1. Cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Ajouter la prise en charge Docker**.

   Un fichier Docker est automatiquement créé avec une configuration par défaut.

   ![Ajouter la prise en charge Docker][add-docker-support]

1. Une fois que vous avez ajouté la prise en charge Docker, cliquez avec le bouton droit sur votre projet dans l’Explorateur de projets, choisissez **Azure**, puis cliquez sur **Publish to Web App for Containers** (Publier sur Web App pour conteneurs).

   ![Publish to Web App for Containers (Publier sur Web App pour conteneurs)][run-on-web-app-for-containers]

1. Quand la boîte de dialogue **Run on Web App for Containers** (Exécuter sur Web App pour conteneurs) s’affiche, entrez les informations demandées :

   * **Docker File** (Fichier Docker) : spécifie le chemin au fichier Docker créé quand vous avez ajouté la prise en charge Docker à votre projet. 

   * **Container Registry** (Registre de conteneurs) : dans le menu déroulant, choisissez le registre de conteneurs que vous avez créé dans la section précédente de cet article. Les champs **Server URL** (URL du serveur), **Username** (Nom d’utilisateur) et **Password** (Mot de passe) sont renseignés automatiquement.

   * **Image and tag** (Image et étiquette) : spécifie le nom de l’image conteneur. Ce nom suit généralement la syntaxe « *registre*.azurecr.io/*nom_app*:latest », où : 
      * *registre* correspond au registre de conteneurs déterminé dans la section précédente de cet article, 
      * *nom_app* correspond au nom de votre application web. 

   * **Web App for Container** (Web App pour conteneurs) : choisissez **Use Existing** (Utiliser l’existant) pour déployer votre conteneur dans une application web existante ou **Create New** (Créer) pour créer une application web.  Le nom de l’application (**App name**) que vous indiquez sert à générer l’URL de votre application web ; par exemple : *wingtiptoys.azurewebsites.net*.

   * **Groupe de ressources** : indique si vous utilisez un groupe de ressources existant ou si vous en créez un. 

   * **App Service Plan** (Plan App Service) : indique si vous utilisez un plan App Service existant ou si vous en créez un. 

   ![Run on Web App for Containers (Exécuter sur Web App pour conteneurs)][run-on-web-app-linux]

1. Quand vous avez terminé de configurer les paramètres ci-dessus, cliquez sur **Exécuter** pour publier votre application web sur Azure.

1. Une fois votre application web publiée, vous pouvez y accéder à l’aide de l’URL spécifiée précédemment ; par exemple : *wingtiptoys.azurewebsites.net*.

   ![Accès à votre application web][browsing-to-web-app]

## <a name="next-steps"></a>Étapes suivantes

Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker][Docker] officiel.

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Portail Azure]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Create Docker Registry using Azure CLI]: /azure/container-registry/container-registry-get-started-azure-cli

[Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[add-docker-support]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/add-docker-support.png
[browsing-to-web-app]:  media/azure-toolkit-for-eclipse-hello-world-web-app-linux/browsing-to-web-app.png
[create-container-registry-01]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-01.png
[create-container-registry-02]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/create-container-registry-02.png
[docker-settings-menu]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/docker-settings-menu.png
[file-new-project]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/file-new-project.png
[project-name]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/project-name.png
[run-on-web-app-for-containers]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-for-containers.png
[run-on-web-app-linux]: media/azure-toolkit-for-eclipse-hello-world-web-app-linux/run-on-web-app-linux.png
