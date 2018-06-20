---
title: Publier un conteneur Docker avec le kit de ressources Azure pour Eclipse
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
ms.openlocfilehash: aec3682cc14204ca2b395d4b851db7bb68cb8728
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954770"
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse

Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web. En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur. Le kit de ressources Azure pour Eclipse simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités pour *publier en tant que conteneur Docker* permettant le déploiement sur Microsoft Azure. Cet article vous guide à travers les étapes nécessaires à la publication de vos applications sur Azure en tant que conteneurs Docker.

> [!NOTE]
> Vous pouvez trouver plus d’informations sur Docker sur le [site web de Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publier votre application web sur Azure en utilisant un conteneur Docker

1. Ouvrez votre projet d’application web dans Eclipse.

1. Pour démarrer l’Assistant **Publish as Docker Container** (Publication en tant que conteneur Docker), procédez comme suit :

   * Dans la vue **Navigator** (Navigateur), cliquez avec le bouton droit sur votre projet, cliquez sur **Azure** puis sur **Publish as Docker Container** (Publier en tant que conteneur Docker).

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker) de la vue Navigator (Navigateur)][PUB01]

   * Dans la barre d’outils Eclipse, cliquez sur le bouton **Publish** (Publier) puis cliquez sur **Publish as Docker Container** (Publier en tant que conteneur Docker).

      ![Commande Publier en tant que conteneur Docker de la barre d’outils Eclipse][PUB02]
      
   L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) s’ouvre.

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB03]

1. Dans la fenêtre **Type an image name, select the artifact’s path and check a Docker host to be used** (Tapez un nom d’image, sélectionnez le chemin de l’artefact et indiquez un hôte Docker à utiliser), procédez comme suit :

   a. Dans la zone **Docker image name** (Nom de l’image Docker), entrez un nom unique pour votre hôte Docker. (L’Assistant crée automatiquement un nom, mais vous pouvez le modifier.)

   b. La zone **Hosts** (Hôtes) affiche tous les hôtes Docker que vous avez déjà créés. Effectuez l’une des actions suivantes :

   * Si vous avez un hôte Docker existant, vous pouvez déployer votre application web sur celui-ci.
   * Pour créer un hôte Docker, cliquez sur **Add** (Ajouter).  
      
      La boîte de dialogue **Create Docker Host** (Créer un hôte Docker) s’ouvre.

   ![Assistant Deploy Docker Container on Azure (Déployer un conteneur Docker dans Azure)][PUB04a]

1. Dans la fenêtre **Configure the new virtual machine** (Configurer la nouvelle machine virtuelle), spécifiez les options suivantes pour votre hôte Docker. (L’Assistant génère automatiquement la plupart des options pour vous, mais vous pouvez les modifier.)

   a. **Name** (Nom) : entrez un nom unique pour l’hôte Docker. (Ce n’est pas le même que le nom de l’image Docker que vous avez spécifié précédemment.)

   b. **Subscription** (Abonnement) : entrez l’abonnement Azure que vous utilisez pour votre hôte.

   c. **Region** (Région) : entrez la région géographique où se trouve votre hôte.

   d. Dans l’onglet **Host OS and Size** (Système d’exploitation et taille de l’hôte) : 
   * **Host OS** (Système d’exploitation de l’hôte) : entrez le système d’exploitation de la machine virtuelle qui contient votre hôte.
   * **Size** (Taille) : entrez la taille de la machine virtuelle de votre hôte.

   e. Dans l’onglet **Groupe de ressources** : 
   * **New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.
   * **Existing resource group** (Groupe de ressources existant) : entrez un groupe de ressources existant dans votre compte Azure.

   f. Dans l’onglet **Réseau** : 
   * **New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.
   * **Existing virtual network** (Réseau virtuel existant) : entrez un réseau virtuel existant dans votre compte Azure.

   g. Dans l’onglet **Stockage** : 
   * **New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.
   * **Existing storage account** (Compte de stockage existant) : entrez un compte de stockage existant dans votre compte Azure.

1. Cliquez sur **Suivant**.

1. Dans la fenêtre **Configure log in credentials and port settings** (Configurer les informations d’identification de connexion et les paramètres de port), sélectionnez une des options suivantes :

   * **Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifie un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure. 

   >[!NOTE]
   >Un coffre de clés Azure créé avec un compte ou un principal de service spécifique n’est pas automatiquement accessible par un autre compte ou principal de service qui partage l’abonnement. Pour permettre à un autre compte ou principal de service d’utiliser le coffre de clés, vous devez utiliser le portail Azure pour ajouter le compte ou le principal de service.
   >

   * **New log in credentials** (Nouvelles informations d’identification de connexion) : crée un nouvel ensemble d’informations d’identification de connexion. Si vous sélectionnez cette option, procédez comme suit : 
    
      * Sous l’onglet **VM Credentials** (Informations d’identification de la machine virtuelle), choisissez une des options suivantes pour les informations d’identification de connexion de la machine virtuelle de votre hôte Docker : 

         * **Username** (Nom d’utilisateur) : entrez le nom d’utilisateur des informations d’identification de connexion de votre machine virtuelle. 
         * **Password** (Mot de passe) et **Confirm** (Confirmer) : entrez le mot de passe pour les informations d’identification de connexion de votre machine virtuelle. 
         * **SSH** : entrez les paramètres SSH (Secure Shell) pour votre hôte Docker. Vous pouvez choisir parmi les options suivantes : 
            * **None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions SSH. 
            * **Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaire pour la connexion via SSH. 
            * **Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés. Le répertoire doit contenir les deux fichiers suivants : 
               * *id_rsa* : contient l’identification RSA d’un utilisateur. 
               * *id_rsa.pub* : contient la clé publique RSA qui est utilisée pour l’authentification. 
        
         ![Créer un hôte Docker][PUB05]

      * Sous l’onglet **Docker Daemon Credentials** (Informations d’identification du démon Docker), spécifiez les options suivantes : 

         * **Docker Daemon port** (Port du démon Docker) : entrez le port TCP unique pour votre hôte Docker. 
         * **TLS Security** (Sécurité TLS) : entrez les paramètres TLS (Transport Layer Security) pour votre hôte Docker. Vous pouvez choisir parmi les options suivantes : 
            * **None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions TLS. 
            * **Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaire pour la connexion via TLS. 
            * **Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres TLS précédemment enregistrés. Plus précisément, le répertoire doit contenir les six fichiers suivants : 
               * *ca.pem* et *ca-key.pem* : contiennent le certificat et la clé publique de l’autorité de certification TLS. 
               * *cert.pem* et *key.pem*: contiennent le certificat client et la clé publique qui est utilisée pour l’authentification TLS. 
               * *server.pem* et *server-key.pem* : contiennent la clé publique et le certificat de serveur pour l’hôte. 

         ![Créer un hôte Docker][PUB06]

1. Après avoir entré toutes les informations précédentes, cliquez sur **Finish** (Terminer).

1. Dans l’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker dans Azure), cliquez sur **Next** (Suivant).

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

1. Dans la fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer), procédez comme suit :

   a. Dans la zone **Docker container name** (Nom du conteneur Docker), entrez un nom unique pour votre conteneur Docker.

   b. Choisissez l’une des images Docker suivantes : 

      * **Predefined Docker image** (Image Docker prédéfinie) : spécifie une image Docker préexistante dans Azure. 

      >[!NOTE]
      >La liste des images Docker dans cette zone est constituée de plusieurs images configurées pour application d’un correctif par le kit de ressources Azure afin que votre artefact soit déployé automatiquement.
      >

      * **Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifie un fichier Dockerfile précédemment enregistré sur votre ordinateur local.

      >[!NOTE]
      >Il s’agit d’une fonctionnalité plus avancée destinée aux développeurs qui souhaitent déployer leur propre fichier Dockerfile. Toutefois, les développeurs qui utilisent cette option doivent s’assurer que leur fichier Docker est construit correctement. Comme le kit de ressources Azure ne valide pas le contenu d’un fichier Dockerfile personnalisé, le déploiement peut échouer si le fichier Dockerfile présente des problèmes. En outre, comme le kit de ressources Azure attend que le fichier Dockerfile personnalisé contienne un artefact d’application web, il tente d’ouvrir une connexion HTTP. Si les développeurs publient un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.
      >

   c. **Port settings** (Paramètres de port), entrez la liaison de port TCP unique pour votre conteneur Docker.

      ![La fenêtre Configure the Docker container to be created (Configurer le conteneur Docker à créer)][PUB08]

1. Après avoir terminé toutes les étapes précédentes, cliquez sur **Finish** (Terminer).

Le kit de ressources Azure commence le déploiement de votre application web sur Azure dans un conteneur Docker. 

## <a name="next-steps"></a>étapes suivantes

Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker].

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[site web de Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png