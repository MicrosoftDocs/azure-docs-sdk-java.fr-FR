---
title: Installation du kit de ressources Azure pour IntelliJ
description: Découvrez comment installer le plug-in Kit de ressources Azure pour IntelliJ pour créer et déployer des applications cloud sur Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: c6817c7b-f28c-4c06-8216-41c7a8117de3
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 0f3df5c8cf3c83c1ce9a4ca32c753b5fc39ab1df
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892880"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a>Installation du kit de ressources Azure pour IntelliJ

Le kit de ressources Azure pour IntelliJ contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications cloud sur Azure avec l’environnement de développement IntelliJ IDEA.

> [!NOTE] 
> 
> Le kit de ressources Azure pour IntelliJ est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante : 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

Il existe deux méthodes pour installer le Kit de ressources Azure pour IntelliJ : en utilisant la boîte de dialogue **Paramètres**, ou en utilisant le menu **Configurer** sur l’écran de démarrage. Ces deux méthodes d’installation seront développées dans les étapes suivantes.

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a>Pour installer le Kit de ressources Azure pour IntelliJ à partir de la boîte de dialogue Settings (Paramètres)

1. Démarrez IntelliJ IDEA.

1. Une fois IntelliJ IDEA ouvert, cliquez sur **File** (Fichier), puis sur **Settings** (Paramètres).
   
   ![Ouvrir la boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][01a]

1. Dans la boîte de dialogue Settings (Paramètres), cliquez sur **Plugins** (Plug-ins), puis sur **Browse repositories** (Parcourir les référentiels).
   
   ![Boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][02a]

1. Dans la boîte de dialogue **Browse Repositories** (Parcourir les référentiels) , tapez « Azure » dans la zone de recherche. Mettez en surbrillance **Azure Toolkit for IntelliJ** (Kit de ressources Azure pour IntelliJ), puis cliquez sur **Install** (Installer).
   
   ![Rechercher le kit de ressources Azure pour IntelliJ][03]
   
   IntelliJ IDEA affiche la progression de l’installation dans une boîte de dialogue.
   
   ![Progression de l’installation][04]

1. Une fois l’installation terminée, cliquez sur **Restart IntelliJ IDEA**(Redémarrer IntelliJ IDEA).
   
   ![Restart IntelliJ IDEA][05]

1. Cliquez sur **OK** pour fermer la boîte de dialogue Settings (Paramètres).
   
   ![Fermer la boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][06]

1. Quand vous êtes invité à redémarrer IntelliJ IDEA ou à reporter l’opération, cliquez sur **Restart**(Redémarrer).
   
1   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a>Pour installer le Kit de ressources Azure pour IntelliJ à partir de l’écran d’accueil

1. Démarrez IntelliJ IDEA.

1. Quand l’écran d’accueil d’IntelliJ IDEA s’affiche, cliquez sur **Configure** (Configurer), puis sur **Plugins** (Plug-ins).
   
   ![Installer les plug-ins IntelliJ IDEA][01b]

1. Dans la boîte de dialogue **Plugins** (Plug-ins), cliquez sur **Browse repositories** (Parcourir les référentiels).
   
   ![Parcourir les référentiels de plug-ins IntelliJ IDEA][02b]

1. Dans la boîte de dialogue **Browse Repositories** (Parcourir les référentiels) , tapez « Azure » dans la zone de recherche. Mettez en surbrillance **Azure Toolkit for IntelliJ** (Kit de ressources Azure pour IntelliJ), puis cliquez sur **Install** (Installer).
   
   ![Rechercher le kit de ressources Azure pour IntelliJ][03]
   
   IntelliJ IDEA affiche la progression de l’installation dans une boîte de dialogue.
   
   ![Progression de l’installation][04]

1. Une fois l’installation terminée, cliquez sur **Restart IntelliJ IDEA**(Redémarrer IntelliJ IDEA).
   
   ![Restart IntelliJ IDEA][05]

1. Quand vous êtes invité à redémarrer IntelliJ IDEA ou à reporter l’opération, cliquez sur **Restart**(Redémarrer).
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[01a]: media/azure-toolkit-for-intellij-installation/01-intellij-file-settings.png
[01b]: media/azure-toolkit-for-intellij-installation/01-intellij-configure-dropdown.png
[02a]: media/azure-toolkit-for-intellij-installation/02-intellij-settings-dialog.png
[02b]: media/azure-toolkit-for-intellij-installation/02-intellij-plugins-dialog.png
[03]: media/azure-toolkit-for-intellij-installation/03-intellij-browse-repositories.png
[04]: media/azure-toolkit-for-intellij-installation/04-install-progress.png
[05]: media/azure-toolkit-for-intellij-installation/05-restart-intellij.png
[06]: media/azure-toolkit-for-intellij-installation/06-intellij-settings-dialog.png
[07]: media/azure-toolkit-for-intellij-installation/07-restart-intellij.png
