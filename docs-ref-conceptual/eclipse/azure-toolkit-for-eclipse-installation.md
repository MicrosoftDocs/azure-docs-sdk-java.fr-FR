---
title: Installer le Kit de ressources Azure pour Eclipse
description: "Découvrez comment installer le plug-in Kit de ressources Azure pour Eclipse pour créer et déployer des applications cloud sur Azure."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 54f636f1291832702bfed2b49888b531d358cb73
ms.sourcegitcommit: 9c354a65b0f8ad49a528f40ddee647b091f7d246
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2018
---
# <a name="install-the-azure-toolkit-for-eclipse"></a>Installer le Kit de ressources Azure pour Eclipse

Le kit de ressources Azure pour Eclipse contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications cloud Azure depuis l’environnement de développement Eclipse.

> [!NOTE] 
> 
> Le kit de ressources Azure pour Eclipse est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante : 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Les étapes suivantes vous montrent comment installer le kit de ressources Azure pour Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a>Pour installer le Kit de ressources Azure pour Eclipse

1. Démarrez Eclipse.

1. Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.
   
   ![Installation du kit de ressources Azure pour Eclipse][01]

1. Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse/`, puis appuyez sur la touche **Entrée**.

1. Dans le volet **Name** (Nom), cochez **Azure Toolkit for Eclipse** (Kit de ressources Azure pour Eclipse) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l'installation pour trouver le logiciel requis). Votre écran doit se présenter comme suit :
   
   ![Installation du kit de ressources Azure pour Eclipse][02]

1. En développant **Kit de ressources Azure pour Eclipse**, vous verrez une liste des composants qui seront installés. Par exemple :

   | Fonctionnalité | DESCRIPTION | 
   |---|---| 
   | **Plug-in Application Insights pour Java** | Permet d’utiliser les services de journalisation et d’analyse de télémétrie d’Azure pour vos applications et instances de serveur. | 
   | **Plug-in Azure Common** | Fournit les fonctionnalités communes dont les autres composants du kit de ressources ont besoin. | 
   | **Outils Azure Container pour Eclipse** | Permet de créer et déployer un fichier WAR en tant que conteneur Docker à une machine docker. | 
   | **Conteneurs Azure pour Eclipse** | Permet de déployer un fichier WAR ou JAR en tant que conteneur Docker sur une machine virtuelle Azure. | 
   | **Azure Explorer pour Eclipse** | Fournit une interface de style Explorateur pour gérer vos ressources Azure. | 
   | **Microsoft JDBC Driver 6.1 pour SQL Server** | Fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8. | 
   | **Package pour les bibliothèques Microsoft Azure pour Java** | Fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc. | 

1. Cliquez sur **Suivant**. (Si vous rencontrez des délais d'attente inhabituels lors de l'installation du kit de ressources, assurez-vous que l'option **Contact all update sites during install to find required software** est désactivée.)

1. Dans la boîte de dialogue **Install Details** (Détails d’installation), cliquez sur **Next** (Suivant).
   
   ![Passer en revue les détails de l’installation][03]

1. Dans la boîte de dialogue **Review Licenses** (Vérifier les licences), passez en revue les termes des contrats de licence. Si vous acceptez les termes des contrats de licence, cliquez sur **I accept the terms of the license agreements** (J’accepte les termes des contrats de licence), puis sur **Finish** (Terminer). (Les étapes restantes supposent que vous acceptez les termes des contrats de licence. Si vous n'acceptez pas les termes des contrats de licence, quittez le processus d'installation.)
   
   ![Review Licenses][04]
   
   Eclipse télécharge et installe les packages requis.
   
   ![Progression de l’installation][05]

1. Si vous êtes invité à redémarrer Eclipse pour terminer l’installation, cliquez sur **Yes**(Oui).
   
   ![Invite de redémarrage][06]

## <a name="next-steps"></a>étapes suivantes

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
