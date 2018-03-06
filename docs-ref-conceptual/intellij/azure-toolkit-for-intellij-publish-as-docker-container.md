---
title: Publier un conteneur Docker avec le kit de ressources Azure pour IntelliJ
description: "Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f92040b34b9897d9feea8d2ec5e8748e75fff7f7
ms.sourcegitcommit: 381a865f2849be8e3044d24cd4b3b54e9bbb7abc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2018
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ

Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web. En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur. Le kit de ressources Azure pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités pour *publier en tant que conteneur Docker* permettant le déploiement sur Microsoft Azure. Cet article vous guide à travers les étapes nécessaires à la publication de vos applications sur Azure en tant que conteneurs Docker.

> [!NOTE]
>
> Vous pouvez trouver plus d’informations sur Docker sur le [site web de Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Publier votre application web sur Azure en utilisant un conteneur Docker

> [!NOTE]
> * Pour publier votre application web, vous devrez créer un artefact prêt pour le déploiement. Pour plus d’informations, consultez la section [Informations supplémentaires sur la création d’artefacts](#artifacts).
>
> * Une fois que vous avez utilisé l’Assistant de déploiement au moins une fois, la plupart de vos paramètres sont utilisés comme valeurs par défaut quand vous réexécutez l’Assistant.
>

1. Ouvrez votre projet d’application web dans IntelliJ.

2. Pour démarrer l’Assistant **Publish as Docker Container** (Publication en tant que conteneur Docker), procédez comme suit :

   * Dans la fenêtre de l’outil **Project** (Projet), cliquez avec le bouton droit sur votre projet, cliquez sur **Azure** puis sur **Publish as Docker Container** (Publier en tant que conteneur Docker) :

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker)][PUB01]

   * Dans la barre d’outils IntelliJ, cliquez sur le bouton **Publish Group** (Publier le groupe) puis cliquez sur **Publish as Docker Container** (Publier en tant que conteneur Docker) :

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker)][PUB02]  
    L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) s’ouvre.

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB03]

3. Dans la fenêtre **Type an image name, select the artifact’s path and check a Docker host to be used** (Tapez un nom d’image, sélectionnez le chemin de l’artefact et indiquez un hôte Docker à utiliser), procédez comme suit : 

   a. Dans la zone **Docker image name** (Nom de l’image Docker), entrez un nom unique pour votre hôte Docker. (L’Assistant crée automatiquement un nom, mais vous pouvez le modifier.) 

   b. La zone **Hosts** (Hôtes) affiche tous les hôtes Docker que vous avez déjà créés. Effectuez l’une des actions suivantes : 
      * Si vous avez un hôte Docker existant, vous pouvez déployer votre application web sur celui-ci.
      * Pour créer un hôte Docker, cliquez sur le signe plus de couleur verte (**+**).  
       La boîte de dialogue **Create Docker Host** (Créer un hôte Docker) s’ouvre. 

      ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. Dans la fenêtre **Configure the new virtual machine** (Configurer la nouvelle machine virtuelle), fournissez les informations suivantes sur votre hôte Docker. (L’Assistant génère automatiquement la plupart des informations pour vous, mais vous pouvez les modifier.) 

   a. Dans la zone **Name** (Nom), entrez un nom unique pour votre hôte Docker. (Ce n’est pas le même que le nom de l’image Docker que vous avez spécifié précédemment.) 
    
   b. Dans la zone **Subscription** (Abonnement), entrez l’abonnement Azure que vous utilisez pour votre hôte. 
      
   c. Dans la zone **Region** (Région), entrez la région géographique où se trouve votre hôte.
      
   d. Sous l’onglet **OS and Size** (Système d’exploitation et taille), procédez comme suit :      
      * **Host OS** (Système d’exploitation de l’hôte) : entrez le système d’exploitation de la machine virtuelle qui contient votre hôte. 
      * **Size** (Taille) : entrez la taille de la machine virtuelle de votre hôte.   
       
   e. Sous l’onglet **Resource Group** (Groupe de ressources), sélectionnez une des options suivantes :      
      * **New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.
      * **Existing resource group** (Groupe de ressources existant) : spécifiez un groupe de ressources existant dans votre compte Azure. 
       
   f. Sous l’onglet **Network** (Réseau), sélectionnez une des options suivantes :      
      * **New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.
      * **Existing virtual network** (Réseau virtuel existant) : spécifiez un réseau virtuel existant dans votre compte Azure. 
       
   g. Sous l’onglet **Storage** (Stockage), sélectionnez une des options suivantes :      
      * **New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.
      * **Compte de stockage existant** : spécifiez un compte de stockage existant dans votre compte Azure.
       
5. Cliquez sur **Suivant**.  
     La fenêtre **Configure log in credentials and port settings** (Configurer les informations d’identification de connexion et les paramètres de port) s’ouvre.

      ![La fenêtre Configure log in credentials and port settings (Configurer les informations d’identification de connexion et les paramètres de port)][PUB05]

6. Sélectionnez l’une des options suivantes :

      * **Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifiez un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.

          > [!NOTE]
          > Un coffre de clés Azure créé avec un compte ou un principal de service spécifique n’est pas automatiquement accessible par un autre compte ou principal de service qui partage l’abonnement. Pour permettre à un autre compte ou principal de service d’utiliser le coffre de clés, vous devez utiliser le portail Azure pour ajouter le compte ou le principal de service.

      * **New log in credentials** (Nouvelles informations d’identification de connexion) : créez un nouvel ensemble d’informations d’identification de connexion. Si vous sélectionnez cette option, procédez comme suit :

        a. Sous l’onglet **Informations d’identification de la machine virtuelle**, renseignez les informations suivantes pour les informations d’identification de connexion de la machine virtuelle de votre hôte Docker : * **Nom d’utilisateur** : entrez le nom d’utilisateur pour les informations d’identification de connexion de votre machine virtuelle.
             * **Password** (Mot de passe) et **Confirm** (Confirmer) : entrez le mot de passe pour les informations d’identification de connexion de votre machine virtuelle.
             * **SSH** : entrez les paramètres SSH (Secure Shell) pour votre hôte Docker. Vous pouvez sélectionner une des options suivantes : * **Aucun** : spécifie que votre machine virtuelle n’autorise pas les connexions SSH.
                * **Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaires pour la connexion via SSH.
                * **Import from directory** (Importer à partir du répertoire) : vous permet de spécifier un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés. Le répertoire doit contenir les deux fichiers suivants :
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        b. Sous l’onglet **Docker Daemon Access** (Accès au démon Docker), fournissez les informations suivantes :

          ![Créer un hôte Docker][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. Après avoir entré les informations nécessaires, cliquez sur **Finish** (Terminer).  
    L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) réapparaît.

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

8. Cliquez sur **Suivant**.  
    La fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer) s’ouvre.

   ![La fenêtre Configure the Docker container to be created (Configurer le conteneur Docker à créer)][PUB08]

9. Dans la fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer), fournissez les informations suivantes : 

   a. Dans la zone **Docker container name** (Nom du conteneur Docker), entrez un nom unique pour votre conteneur Docker.

   b. Choisissez l’une des images Docker suivantes : 

      * **Predefined Docker image** (Image Docker prédéfinie) : spécifiez une image Docker préexistante dans Azure. 

        > [!NOTE]
        > La liste des images Docker dans cette zone est constituée de plusieurs images configurées pour application d’un correctif par le kit de ressources Azure afin que votre artefact soit déployé automatiquement. 

      * **Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifiez un fichier Dockerfile précédemment enregistré sur votre ordinateur local.

        > [!NOTE]
        > Il s’agit d’une fonctionnalité plus avancée destinée aux développeurs qui veulent déployer leur propre fichier Dockerfile. Toutefois, les développeurs qui utilisent cette option doivent s’assurer que leur fichier Docker est construit correctement. Comme le kit de ressources Azure ne valide pas le contenu d’un fichier Dockerfile personnalisé, le déploiement peut échouer si le fichier Dockerfile présente des problèmes. En outre, comme la boîte à outils Azure attend que le fichier Dockerfile personnalisé contienne un artefact d’application web, il tente d’ouvrir une connexion HTTP. Si les développeurs publier un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.

   c. Dans la zone **Port settings** (Paramètres de port), entrez la liaison de port TCP unique pour votre conteneur Docker. 

10. Après avoir terminé les étapes précédentes, cliquez sur **Finish** (Terminer). 

Le kit de ressources Azure commence le déploiement de votre application web sur Azure dans un conteneur Docker. Sauf si vous avez configuré le déploiement d’IntelliJ en arrière-plan, une barre de progression **Deploying to Azure** (Déploiement sur Azure) s’affiche. 

![La barre de progression du déploiement][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Informations supplémentaires sur la création d’artefacts

Pour créer un artefact prêt pour le déploiement, procédez comme suit :

1. Ouvrez votre projet d’application web dans IntelliJ.

2. Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.

   ![La commande Structure de projet][ART01]

3. Pour ajouter un artefact, cliquez sur le signe plus de couleur verte (**+**) puis cliquez sur **Web Application: Archive** (Application web : Archive).

   ![La commande Web Application: Archive (Application web : Archive)][ART02]

4. Dans la zone **Name** (Nom), entrez un nom pour votre artefact (n’incluez pas l’extension *.war*) puis cliquez sur **OK**.

   ![La zone Name (Nom) de l’artefact][ART03]

Pour plus d’informations sur la création d’artefacts dans IntelliJ, consultez [Configuring artifacts] sur le site web de JetBrains.

## <a name="next-steps"></a>étapes suivantes

Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker].

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[site web de Docker]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
