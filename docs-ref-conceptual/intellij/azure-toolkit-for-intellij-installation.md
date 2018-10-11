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
# <a name="installing-the-azure-toolkit-for-intellij"></a><span data-ttu-id="9e2b9-103">Installation du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="9e2b9-103">Installing the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="9e2b9-104">Le kit de ressources Azure pour IntelliJ contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications cloud sur Azure avec l’environnement de développement IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-104">The Azure Toolkit for IntelliJ provides templates and functionality that allow you to easily create, develop, test, and deploy cloud application to Azure using the IntelliJ IDEA development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9e2b9-105">Le kit de ressources Azure pour IntelliJ est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante :</span><span class="sxs-lookup"><span data-stu-id="9e2b9-105">The Azure Toolkit for IntelliJ is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

<span data-ttu-id="9e2b9-106">Il existe deux méthodes pour installer le Kit de ressources Azure pour IntelliJ : en utilisant la boîte de dialogue **Paramètres**, ou en utilisant le menu **Configurer** sur l’écran de démarrage.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-106">There are two methods of installing the Azure Toolkit for IntelliJ: by using the **Settings** dialog box, and by using the **Configure** menu on the start screen.</span></span> <span data-ttu-id="9e2b9-107">Ces deux méthodes d’installation seront développées dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-107">Both installation methods will be demonstrated in the following steps.</span></span>

[!INCLUDE [azure-toolkit-for-IntelliJ-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-settings-dialog-box"></a><span data-ttu-id="9e2b9-108">Pour installer le Kit de ressources Azure pour IntelliJ à partir de la boîte de dialogue Settings (Paramètres)</span><span class="sxs-lookup"><span data-stu-id="9e2b9-108">To install the Azure Toolkit for IntelliJ from the settings dialog box</span></span>

1. <span data-ttu-id="9e2b9-109">Démarrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-109">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="9e2b9-110">Une fois IntelliJ IDEA ouvert, cliquez sur **File** (Fichier), puis sur **Settings** (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-110">When the IntelliJ IDEA opens, click **File**, then click **Settings**.</span></span>
   
   ![Ouvrir la boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][01a]

1. <span data-ttu-id="9e2b9-112">Dans la boîte de dialogue Settings (Paramètres), cliquez sur **Plugins** (Plug-ins), puis sur **Browse repositories** (Parcourir les référentiels).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-112">In the Settings dialog box, click **Plugins**, and then click **Browse repositories**.</span></span>
   
   ![Boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][02a]

1. <span data-ttu-id="9e2b9-114">Dans la boîte de dialogue **Browse Repositories** (Parcourir les référentiels) , tapez « Azure » dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-114">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="9e2b9-115">Mettez en surbrillance **Azure Toolkit for IntelliJ** (Kit de ressources Azure pour IntelliJ), puis cliquez sur **Install** (Installer).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-115">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Rechercher le kit de ressources Azure pour IntelliJ][03]
   
   <span data-ttu-id="9e2b9-117">IntelliJ IDEA affiche la progression de l’installation dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-117">IntelliJ IDEA displays the installation progress in a dialog box.</span></span>
   
   ![Progression de l’installation][04]

1. <span data-ttu-id="9e2b9-119">Une fois l’installation terminée, cliquez sur **Restart IntelliJ IDEA**(Redémarrer IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-119">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="9e2b9-121">Cliquez sur **OK** pour fermer la boîte de dialogue Settings (Paramètres).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-121">Click **OK** to close the Settings dialog box.</span></span>
   
   ![Fermer la boîte de dialogue Settings (Paramètres) d’IntelliJ IDEA][06]

1. <span data-ttu-id="9e2b9-123">Quand vous êtes invité à redémarrer IntelliJ IDEA ou à reporter l’opération, cliquez sur **Restart**(Redémarrer).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-123">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
<span data-ttu-id="9e2b9-124">1</span><span class="sxs-lookup"><span data-stu-id="9e2b9-124">1</span></span>   ![Restart IntelliJ IDEA][07]

## <a name="to-install-the-azure-toolkit-for-intellij-from-the-start-screen"></a><span data-ttu-id="9e2b9-126">Pour installer le Kit de ressources Azure pour IntelliJ à partir de l’écran d’accueil</span><span class="sxs-lookup"><span data-stu-id="9e2b9-126">To install the Azure Toolkit for IntelliJ from the start screen</span></span>

1. <span data-ttu-id="9e2b9-127">Démarrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-127">Start IntelliJ IDEA.</span></span>

1. <span data-ttu-id="9e2b9-128">Quand l’écran d’accueil d’IntelliJ IDEA s’affiche, cliquez sur **Configure** (Configurer), puis sur **Plugins** (Plug-ins).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-128">When the IntelliJ IDEA start screen appears, click **Configure**, then click **Plugins**.</span></span>
   
   ![Installer les plug-ins IntelliJ IDEA][01b]

1. <span data-ttu-id="9e2b9-130">Dans la boîte de dialogue **Plugins** (Plug-ins), cliquez sur **Browse repositories** (Parcourir les référentiels).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-130">In the **Plugins** dialog box, click **Browse repositories**.</span></span>
   
   ![Parcourir les référentiels de plug-ins IntelliJ IDEA][02b]

1. <span data-ttu-id="9e2b9-132">Dans la boîte de dialogue **Browse Repositories** (Parcourir les référentiels) , tapez « Azure » dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-132">In the **Browse Repositories** dialog box, type "Azure" in the search box.</span></span> <span data-ttu-id="9e2b9-133">Mettez en surbrillance **Azure Toolkit for IntelliJ** (Kit de ressources Azure pour IntelliJ), puis cliquez sur **Install** (Installer).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-133">Highlight **Azure Toolkit for IntelliJ**, and then click **Install**.</span></span>
   
   ![Rechercher le kit de ressources Azure pour IntelliJ][03]
   
   <span data-ttu-id="9e2b9-135">IntelliJ IDEA affiche la progression de l’installation dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e2b9-135">IntelliJ IDEA will display the installation progress in a dialog box.</span></span>
   
   ![Progression de l’installation][04]

1. <span data-ttu-id="9e2b9-137">Une fois l’installation terminée, cliquez sur **Restart IntelliJ IDEA**(Redémarrer IntelliJ IDEA).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-137">When the installation has completed, click **Restart IntelliJ IDEA**.</span></span>
   
   ![Restart IntelliJ IDEA][05]

1. <span data-ttu-id="9e2b9-139">Quand vous êtes invité à redémarrer IntelliJ IDEA ou à reporter l’opération, cliquez sur **Restart**(Redémarrer).</span><span class="sxs-lookup"><span data-stu-id="9e2b9-139">When prompted to restart IntelliJ IDEA or postpone, click **Restart**.</span></span>
   
   ![Restart IntelliJ IDEA][07]

## <a name="next-steps"></a><span data-ttu-id="9e2b9-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e2b9-141">Next steps</span></span>

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
