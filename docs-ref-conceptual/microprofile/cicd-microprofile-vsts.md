---
title: CI/CD pour les applications MicroProfile utilisant Azure DevOps
description: Découvrez comment configurer un cycle de mise en production CI/CD pour déployer une application MicroProfile vers une application web Azure pour l’instance des conteneurs à l’aide d’Azure DevOps
services: Azure DevOps
documentationcenter: MicroProfile
author: ruyakubu
manager: brunoborges
editor: ruyakubu
ms.assetid: ''
ms.author: ruyakubu
ms.date: 09/14/2018
ms.devlang: Java
ms.service: Azure DevOps
ms.tgt_pltfrm: multiple
ms.topic: tutorial
ms.workload: web
ms.openlocfilehash: c2b6bf3370982d26d8d23fede370e0105a70b734
ms.sourcegitcommit: fd67d4088be2cad01c642b9ecf3f9475d9cb4f3c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46506437"
---
# <a name="cicd-for-microprofile-applications-using-azure-devops"></a>CI/CD pour les applications MicroProfile utilisant Azure DevOps

Ce didacticiel explique comment les développeurs Java EE peuvent facilement configurer un cycle de mise en production CI/CD pour déployer leurs applications [MicroProfile](http://microprofile.io) vers une application web Azure pour les conteneurs à l’aide de Azure DevOps (anciennement nommé VSTS).  Dans cet exemple, nous allons utiliser une application MicroProfile qui utilise un [Payara Micro](https://www.payara.fish/payara_micro) en tant qu’image de base.   

```Dockerfile
FROM payara/micro:5.182
COPY target/*.war $DEPLOY_DIR/ROOT.war
EXPOSE 8080
```
Nous allons commencer le processus de conteneurisation Azure DevOps en générant une image Docker et en envoyant l’image conteneur vers un registre de conteneurs Azure.  Puis terminez avec un pipeline de mise en production DevOps de Azure pour déployer l’image conteneur vers une application Web.

## <a name="prerequisites"></a>Prérequis
- Copiez et enregistrez l’URL Git à partir de [Github](https://github.com/Azure-Samples/microprofile-hello-azure)
- Inscrivez-vous ou connectez-vous à votre compte [Azure DevOps](https://dev.azure.com)
- Créez un nouveau [projet Azure DevOps](https://docs.microsoft.com/en-us/vsts/organizations/projects/create-project?view=vsts&tabs=new-nav) et utilisez l’URL Git ci-dessus pour **importer un référentiel**
- Créez un [Registre de conteneurs Azure](https://azure.microsoft.com/en-us/services/container-registry) (ACR)
- Créez une application web Azure pour le conteneur
> [!NOTE]
>
> Sélectionnez « Démarrage rapide » dans les réglages du conteneur lors de la configuration de l’instance de l’application web


## <a name="create-a-build-definition"></a>Créez une définition de build

La définition de build dans Azure DevOps exécute automatiquement toutes les tâches dans la build à chaque validation dans une application source Java EE.  Dans cet exemple, Azure DevOps utilisera Maven pour générer le projet Java MicroProfile.

1. Cliquez sur l’onglet « Build et Mise en production » en haut la page de votre projet Azure DevOps.  Ensuite, sélectionnez le lien **Builds** 

<img src="media/VSTS/Buid-and-Release1.png">

2. Cliquez sur le bouton **Nouveau Pipeline**, puis **Continuer** pour commencer à définir vos tâches de build
3. Sélectionnez « Maven » dans la liste des modèles, puis cliquez sur le bouton **Appliquer** pour générer votre projet Java
4. Utilisez le menu déroulant du champ Pool d’agent pour sélectionner l’option **Aperçu de l’hébergement Linux**.
> [!NOTE]
>
> Cela indique à Azure DevOps, quel serveur build utiliser.  Vous pouvez utiliser votre propre serveur de build personnalisée

5. Pour configurer votre build pour une intégration continue, sélectionnez l’onglet **Déclencheurs** et cochez la case **Autoriser l’intégration continue**.  

<img src="media/VSTS/Build-Triggers2.png"> 
 
6. Sélectionnez l’onglet **Tâches** pour revenir à la page de pipeline de build principale
7. Sélectionnez l’option **Sauvegarder** dans le menu déroulant **Enregistrer et mettre en file d'attente**
 

## <a name="create-a-docker-build-image"></a>Générez une image de build Docker

Dans cette tâche, Azure DevOps utilise un fichier Docker avec une image de base Payara Micro pour générer une image Docker.  

1. Sélectionnez l’onglet **Tâches** pour revenir à la page de pipeline de build principale
2. Cliquez sur l’icône **+** pour ajouter une nouvelle tâche à la définition de build
 
<img src="media/VSTS/Tasks-add4.png">
 
3. Sélectionnez « Docker » dans la liste des modèles, puis cliquez sur le bouton **Ajouter**
4. Saisissez un nom de description pour le champ **Nom d'affichage**
5. Vérifiez que le **Registre de conteneurs Azure** est sélectionné dans le menu déroulant de l’onglet **Type de registre de conteneurs**.
> [!NOTE]
>
>  Si vous utilisez Docker Hub ou un autre registre, sélectionnez « Registre de conteneurs » à la place.  Cliquez ensuite sur le bouton « + Nouveau » pour fournir les informations d’identification et de connexion de celui-ci. Passez ensuite à la section des commandes pour continuer.

6. Dans la section **Abonnement Azure**, utilisez le menu déroulant pour sélectionner votre ID d’abonnement Azure.  Cliquez ensuite sur le bouton **Autoriser**
7. Dans le menu déroulant du **Registre de conteneurs Azure**, sélectionnez le registre de conteneurs que vous avez créé avec Azure.
8. Vérifiez que l’option **build** est sélectionnée dans le menu déroulant des **Commandes**.
9. Pour le **fichier Docker**, cliquez sur l’icône du menu de navigation à côté de la zone de texte pour sélectionner le fichier Docker dans le projet github.  Cliquez ensuite sur le bouton **OK**.

<img src="media/VSTS/Dockerfile5.png">

10. Sous le **Nom de l’Image**, cochez la case **Inclure la dernière balise**. 
11. Sélectionnez l’option **Sauvegarder** dans le menu déroulant **Enregistrer et mettre en file d'attente**.

## <a name="push-docker-image-to-acr"></a>Envoyez l’image Docker à l’ACR

Dans cette tâche, Azure DevOps enverra l’image docker à votre Registre de conteneurs Azure.  Cela sera utilisé pour exécuter l’application API de MicroProfile en tant qu’application web Java conteneurisée.

1. Puisque nous utilisons Docker dans Azure DevOps, vous pouvez créer un nouveau modèle de Docker en répétant les étapes 1 à 7 ci-dessus dans la section **Créer une image de build Docker**.
2. Sélectionnez **envoyer (push)** dans le menu déroulant **Commande**.
3. Cliquez sur l’onglet **Enregistrer et mettre en file d'attente**, puis sélectionnez l’option **Enregistrer et mettre en file d'attente**.
4. Vérifiez que l’option **Aperçu de l’hébergement Linux** est sélectionnée dans le pool d’agents de la fenêtre indépendante.  Cliquez ensuite sur le bouton **Enregistrer et mettre en file d’attente**.
5. Cliquez sur le numéro de build pour vérifier que le pipeline de build du projet Java s’est effectué correctement.

<img src="media/VSTS/Build-Number6.png">
 

## <a name="create-a-release-definition-for-a-java-app"></a>Créez une définition de mise en production pour une application Java

Le pipeline de mise en production dans Azure DevOps déclenche automatiquement le déploiement d’artefacts de build vers un environnement cible comme Azure dès que le processus de build s’effectue correctement.   Le pipeline de mise en production peut être créé pour les environnements de développement, de test, de mises en lots ou de production.

1. Cliquez sur l’onglet « Build et Mise en production » en haut la page de votre projet Azure DevOps.  Puis, sélectionnez le lien **Mises en production**.

<img src="media/VSTS/Release-new-pipeline7.png">
 
2. Cliquez sur le bouton «Nouveau pipeline»**
3. Sélectionnez **Déployer une application Java sur Azure App Service** dans la liste des modèles, puis cliquez sur le bouton **Appliquer**.

<img src="media/VSTS/deploy-java-template8.png">
 
4. Définir un **Nom de la phase** (par exemple, Développement, Test, Mise en lots ou Production).  Cliquez ensuite sur le bouton **X** pour fermer la fenêtre indépendante
5. Cliquez sur le bouton **+ Ajouter** dans la section Artefacts.  Cela connectera des artefacts issus de la définition de build à cette définition de mise en production.  
6. Utilisez le menu déroulant pour la **Source (pipeline de build)** pour sélectionner votre définition de build. Puis cliquez sur le bouton **Ajouter** pour continuer.

<img src="media/VSTS/add-artifact9.png">
 
7. Cliquez sur l’onglet **Tâches** du pipeline.  Sélectionnez ensuite votre nom de la phase.
 
<img src="media/VSTS/release-stage10.png">

8. Dans la section **Abonnement Azure**, utilisez le menu déroulant pour sélectionner votre ID d’abonnement Azure.
9. Sélectionnez **Application Linux** dans le menu déroulant **Type d’application**
10. Sélectionnez le nom de l’application Web pour l’instance de conteneur que vous avez créé précédemment dans le menu déroulant **Nom de l’App service**
11. Saisissez le nom de votre registre de conteneurs Azure dans le champ **Registre ou Espaces de noms**.  Par exemple **myregistry.azure.io**
12. Saisissez le nom de registre dans le champ **Référentiel**
13. Cliquez sur **Déployer Azure App Service**.  Entrez la balise de l’image de conteneur dans la zone de texte **Balise** 
14. Cliquez sur **Exécuter sur l’agent**.  Sélectionnez **Aperçu de l’hébergement Linux** dans le pool d’agents du menu déroulant 

## <a name="setup-environment-variables"></a>Valeurs des variables d’environnement

1. Cliquez sur l’onglet **Variables**.  Puis cliquez sur le bouton **+ Ajouter** pour définir vos variables d’environnement
2. Ajoutez le nom de variable et les valeurs pour l’url de votre registre de conteneurs, le nom d’utilisateur et le mot de passe.   Par mesure de sécurité, cliquez sur l’icône en forme de verrou pour conserver la valeur du mot de passe masquée.

Par exemple : 
- registry.password
- registry.url
- registry.username

<img src="media/VSTS/environment-variables12.png">

3. Cliquez sur l’onglet **Tâches** pour revenir à la page de définition de pipeline de mise en production principale
4. Cliquez sur **Déployer Azure App Service**. 
5. Agrandissez la section **Application et Paramètres de Configuration**, puis cliquez dans le menu de navigation pour que le champ des **Paramètres de l’application** ajoute une variable d’environnement pour se connecter au registre de conteneurs pendant le déploiement.
6. Cliquez sur le bouton ** + Ajouter ** pour définir les paramètres d’application suivants et affecter les variables d’environnement
- DOCKER_REGISTRY_SERVER_PASSWORD = $(registry.password)
- DOCKER_REGISTRY_SERVER_URL = $(registry.url)
- DOCKER_REGISTRY_SERVER_USERNAME = $(registry.username)

<img src="media/VSTS/environment-variables14.png">
 
7. Cliquez sur le bouton **OK** pour continuer

## <a name="setup-continious-deployment--deploy-java-application"></a>Paramétrage du déploiement continu & Déployer l’application Java

1. Pour autoriser le déploiement continu, cliquez sur l’onglet **Pipelines**
2. Dans la section des artefacts, cliquez sur l’icône en forme d’éclair.  Définissez ensuite le **Déclencheur de déploiement continu** pour l’activer.

<img src="media/VSTS/release-enable-CD.png">
 
3. Cliquez sur le bouton **Sauvegarder**, puis le bouton **OK** 
4. Cliquez dans le menu déroulant **+ Mise en production**, puis sélectionnez le lien **Créer une mise en production**
5. Utilisez le menu déroulant **Phases pour modifier le déclencheur d’automatique à manuel**pour sélectionner la case de votre nom de la phase
6. Cliquez sur le bouton **Créer** pour continuer
7. Cliquez sur le numéro de mise en production.  Pointez ensuite votre souris sur le nom de la phase et cliquez sur le bouton **Déployer**
8. Cliquez ensuite sur le bouton **Déployer** dans la fenêtre indépendante pour démarrer le processus de déploiement vers Azure


## <a name="test-the-java-web-application"></a>Testez l’application web Java
1. Exécutez l’url de l’application web dans un navigateur web :  
https://{nom-de-votre-application}.azurewebsites.net/api/hello

 
<img src="media/VSTS/web-app16.png">

2. La page web doit indiquer **Hello Azure !**
 
<img src="media/VSTS/web-api17.png">
