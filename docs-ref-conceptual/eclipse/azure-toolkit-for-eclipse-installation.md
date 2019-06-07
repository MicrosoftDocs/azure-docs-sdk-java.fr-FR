---
title: Installation du kit de ressources Azure pour Eclipse
description: Découvrez comment installer le plug-in Kit de ressources Azure pour Eclipse pour créer et déployer des applications cloud sur Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: 9e93ff6a-f42b-4d99-b55b-624136b4a730
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 8e6630f7e019d950249e7e84024ac800a0f2f136
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270843"
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a>Installation du kit de ressources Azure pour Eclipse

Il existe deux façons d’installer Azure Toolkit for Eclipse :

  - [Place de marché Eclipse](#eclipse-marketplace)
  - [Installer un nouveau logiciel](#install-new-software)

> [!NOTE] 
> 
> Le kit de ressources Azure pour Eclipse est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante : 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

[!INCLUDE [azure-toolkit-for-eclipse-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="eclipse-marketplace"></a>Place de marché Eclipse

1. Faites glisser le bouton suivant vers votre espace de travail Eclipse en cours d’exécution.

    [![Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client")

2. Autrement, vous pouvez aussi rechercher et installer le **plug-in Azure Toolkit for Eclipse** à l’emplacement**Aide/Eclipse Marketplace**.

    ![Marketplace](./media/azure-toolkit-for-eclipse-installation/marketplace.png)

## <a name="install-new-software"></a>Installer un nouveau logiciel

1. Démarrez Eclipse.

1. Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.

   ![Installation du kit de ressources Azure pour Eclipse][01]

1. Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse/`, puis appuyez sur la touche **Entrée**.

1. Dans le volet **Name** (Nom), cochez **Azure Toolkit for Java** (Kit de ressources Azure pour Java) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l’installation pour trouver le logiciel requis). Votre écran doit se présenter comme suit :

   ![Installation du kit de ressources Azure pour Eclipse][02]

1. En développant **Kit de ressources Azure pour Eclipse**, vous verrez une liste des composants qui seront installés. Par exemple :

   | Fonctionnalité | Description | 
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

## <a name="next-steps"></a>Étapes suivantes

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
