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
ms.openlocfilehash: 86cef07873ae7a2ba75aab1044fe4d241cd5b13e
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270871"
---
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="b17e1-103">Installation du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b17e1-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="b17e1-104">Le kit de ressources Azure pour IntelliJ contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications cloud sur Azure avec l’environnement de développement IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b17e1-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b17e1-105">Le kit de ressources Azure pour IntelliJ est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante :</span><span class="sxs-lookup"><span data-stu-id="b17e1-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="b17e1-106">Il existe deux méthodes pour installer le Kit de ressources Azure pour IntelliJ : en utilisant la boîte de dialogue **Paramètres**, ou en utilisant le menu **Configurer** sur l’écran de démarrage.</span><span class="sxs-lookup"><span data-stu-id="b17e1-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="b17e1-107">Ces deux méthodes d’installation seront développées dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="b17e1-107">Both installation methods will be demonstrated in the following steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b17e1-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b17e1-108">Prerequisites</span></span>

<span data-ttu-id="b17e1-109">Azure Toolkit for IntelliJ nécessite les composants logiciels suivants :</span><span class="sxs-lookup"><span data-stu-id="b17e1-109">The Azure Toolkit for IntelliJ requires to the following software components:</span></span>

* <span data-ttu-id="b17e1-110">Java Development Kit (JDK) 8 +, par exemple : [OpenJDK](https://openjdk.java.net/) ou [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span><span class="sxs-lookup"><span data-stu-id="b17e1-110">An Java Development Kit (JDK) 8+ installed, for example: [OpenJDK](https://openjdk.java.net/) or [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)</span></span>
* <span data-ttu-id="b17e1-111">[IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition ou Community Edition</span><span class="sxs-lookup"><span data-stu-id="b17e1-111">An [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) Ultimate Edition or Community Edition installed</span></span>

> [!NOTE]
> 
> <span data-ttu-id="b17e1-112">La page [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) dans le référentiel de plug-in JetBrains liste les versions compatibles avec le kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="b17e1-112">The [Azure Toolkit for IntelliJ](https://plugins.jetbrains.com/plugin/8053) page at the JetBrains Plugin Repository lists the builds that are compatible with the toolkit.</span></span>
> 

<!--
> [!IMPORTANT]
> 
> If you are using the Azure Toolkit for IntelliJ on Windows, the toolkit requires installing the Azure SDK 2.9.6 or later in order to use the Azure emulator. You have two options for installing the Azure SDK:
> 
> * You can download and install the Azure SDK by using the [Web Platform Installer (WebPI)](http://go.microsoft.com/fwlink/?LinkID=252838).
> * If you do not have the Azure SDK installed when you create your first Azure deployment project, you will be prompted to automatically download install the requisite version of the Azure SDK.
> 
> Note that the Azure SDK is only required on Windows.
> 
-->


## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="b17e1-113">Pour installer le Kit de ressources Azure pour IntelliJ à partir de la boîte de dialogue Settings (Paramètres)</span><span class="sxs-lookup"><span data-stu-id="b17e1-113">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="b17e1-114">Démarrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b17e1-114">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b17e1-115">Une fois IntelliJ IDEA ouvert, cliquez sur **File** (Fichier), puis sur **Settings** (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="b17e1-115">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Ouvrir la boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][01a]

1. <span data-ttu-id="b17e1-117">Dans la boîte de dialogue Settings (Paramètres), cliquez sur **Plugins** (Plug-ins), puis sur **Browse repositories** (Parcourir les référentiels).</span><span class="sxs-lookup"><span data-stu-id="b17e1-117">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][02a]

1. <span data-ttu-id="b17e1-119">Dans la boîte de dialogue **Browse Repositories** (Parcourir les référentiels) , tapez « Azure » dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="b17e1-119">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="b17e1-120">Mettez en surbrillance **Azure Toolkit for IntelliJ** (Kit de ressources Azure pour IntelliJ), puis cliquez sur **Install** (Installer).</span><span class="sxs-lookup"><span data-stu-id="b17e1-120">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Rechercher le kit de ressources Azure pour IntelliJ][03]
   
   <span data-ttu-id="b17e1-122">IntelliJ IDEA affiche la progression de l’installation dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b17e1-122">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Progression de l’installation][04]

1. <span data-ttu-id="b17e1-124">Une fois l’installation terminée, cliquez sur **Restart IntelliJ IDEA**(Redémarrer IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="b17e1-124">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="b17e1-126">Cliquez sur **OK** pour fermer la boîte de dialogue Settings (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="b17e1-126">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Fermer la boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][06]

1. <span data-ttu-id="b17e1-128">Quand vous êtes invité à redémarrer IntelliJ IDEA ou à reporter l’opération, cliquez sur **Restart**(Redémarrer).</span><span class="sxs-lookup"><span data-stu-id="b17e1-128">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="b17e1-129">1</span><span class="sxs-lookup"><span data-stu-id="b17e1-129">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="b17e1-131">Pour installer le Kit de ressources Azure pour IntelliJ à partir de l’écran d’accueil</span><span class="sxs-lookup"><span data-stu-id="b17e1-131">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="b17e1-132">Démarrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="b17e1-132">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="b17e1-133">Quand l’écran d’accueil d’IntelliJ IDEA s’affiche, cliquez sur **Configure** (Configurer), puis sur **Plugins** (Plug-ins).</span><span class="sxs-lookup"><span data-stu-id="b17e1-133">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Installer les plug-ins IntelliJ IDEA][01b]

1. <span data-ttu-id="b17e1-135">Dans la boîte de dialogue **Plugins** (Plug-ins), cliquez sur **Browse repositories** (Parcourir les référentiels).</span><span class="sxs-lookup"><span data-stu-id="b17e1-135">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Parcourir les référentiels de plug-ins IntelliJ IDEA][02b]

1. <span data-ttu-id="b17e1-137">Dans la boîte de dialogue **Browse Repositories** (Parcourir les référentiels) , tapez « Azure » dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="b17e1-137">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="b17e1-138">Mettez en surbrillance **Azure Toolkit for IntelliJ** (Kit de ressources Azure pour IntelliJ), puis cliquez sur **Install** (Installer).</span><span class="sxs-lookup"><span data-stu-id="b17e1-138">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Rechercher le kit de ressources Azure pour IntelliJ][03]
   
   <span data-ttu-id="b17e1-140">IntelliJ IDEA affiche la progression de l’installation dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b17e1-140">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Progression de l’installation][04]

1. <span data-ttu-id="b17e1-142">Une fois l’installation terminée, cliquez sur **Restart IntelliJ IDEA**(Redémarrer IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="b17e1-142">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="b17e1-144">Quand vous êtes invité à redémarrer IntelliJ IDEA ou à reporter l’opération, cliquez sur **Restart**(Redémarrer).</span><span class="sxs-lookup"><span data-stu-id="b17e1-144">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="b17e1-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b17e1-146">Next steps</span></span>

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
