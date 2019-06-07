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
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="840a1-103">Installation du kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="840a1-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="840a1-104">Il existe deux façons d’installer Azure Toolkit for Eclipse :</span><span class="sxs-lookup"><span data-stu-id="840a1-104">There are two ways to install Azure Toolkit for Eclipse:</span></span>

  - [<span data-ttu-id="840a1-105">Place de marché Eclipse</span><span class="sxs-lookup"><span data-stu-id="840a1-105">Eclipse marketplace</span></span>](#eclipse-marketplace)
  - [<span data-ttu-id="840a1-106">Installer un nouveau logiciel</span><span class="sxs-lookup"><span data-stu-id="840a1-106">Install new software</span></span>](#install-new-software)

> [!NOTE] 
> 
> <span data-ttu-id="840a1-107">Le kit de ressources Azure pour Eclipse est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante :</span><span class="sxs-lookup"><span data-stu-id="840a1-107">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <https://github.com/microsoft/azure-tools-for-java> 
> 

[!INCLUDE [azure-toolkit-for-eclipse-basic-prerequisites](../includes/azure-toolkit-for-eclipse-basic-prerequisites.md)]

## <a name="eclipse-marketplace"></a><span data-ttu-id="840a1-108">Place de marché Eclipse</span><span class="sxs-lookup"><span data-stu-id="840a1-108">Eclipse marketplace</span></span>

1. <span data-ttu-id="840a1-109">Faites glisser le bouton suivant vers votre espace de travail Eclipse en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="840a1-109">Drag the following button to your running Eclipse workspace.</span></span>

    <span data-ttu-id="840a1-110">[![Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Faites glisser vers votre espace de travail Eclipse* en cours d’exécution. *Nécessite Eclipse Marketplace Client")</span><span class="sxs-lookup"><span data-stu-id="840a1-110">[![Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client](https://marketplace.eclipse.org/sites/all/themes/solstice/public/images/marketplace/btn-install.png)](http://marketplace.eclipse.org/marketplace-client-intro?mpc_install=1919278 "Drag to your running Eclipse* workspace. *Requires Eclipse Marketplace Client")</span></span>

2. <span data-ttu-id="840a1-111">Autrement, vous pouvez aussi rechercher et installer le **plug-in Azure Toolkit for Eclipse** à l’emplacement**Aide/Eclipse Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="840a1-111">Otherwise, it is also possible to search and install the **Azure Toolkit for Eclipse plugin** at **Help/Eclipse Marketplace**.</span></span>

    ![Marketplace](./media/azure-toolkit-for-eclipse-installation/marketplace.png)

## <a name="install-new-software"></a><span data-ttu-id="840a1-113">Installer un nouveau logiciel</span><span class="sxs-lookup"><span data-stu-id="840a1-113">Install new software</span></span>

1. <span data-ttu-id="840a1-114">Démarrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="840a1-114">Start Eclipse.</span></span>

1. <span data-ttu-id="840a1-115">Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="840a1-115">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>

   ![Installation du kit de ressources Azure pour Eclipse][01]

1. <span data-ttu-id="840a1-117">Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse/`, puis appuyez sur la touche **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="840a1-117">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="840a1-118">Dans le volet **Name** (Nom), cochez **Azure Toolkit for Java** (Kit de ressources Azure pour Java) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l’installation pour trouver le logiciel requis).</span><span class="sxs-lookup"><span data-stu-id="840a1-118">In the **Name** pane, check **Azure Toolkit for Java**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="840a1-119">Votre écran doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="840a1-119">Your screen should appear similar to the following:</span></span>

   ![Installation du kit de ressources Azure pour Eclipse][02]

1. <span data-ttu-id="840a1-121">En développant **Kit de ressources Azure pour Eclipse**, vous verrez une liste des composants qui seront installés. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="840a1-121">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="840a1-122">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="840a1-122">Feature</span></span> | <span data-ttu-id="840a1-123">Description</span><span class="sxs-lookup"><span data-stu-id="840a1-123">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="840a1-124">**Plug-in Application Insights pour Java**</span><span class="sxs-lookup"><span data-stu-id="840a1-124">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="840a1-125">Permet d’utiliser les services de journalisation et d’analyse de télémétrie d’Azure pour vos applications et instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="840a1-125">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="840a1-126">**Plug-in Azure Common**</span><span class="sxs-lookup"><span data-stu-id="840a1-126">**Azure Common Plugin**</span></span> | <span data-ttu-id="840a1-127">Fournit les fonctionnalités communes dont les autres composants du kit de ressources ont besoin.</span><span class="sxs-lookup"><span data-stu-id="840a1-127">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="840a1-128">**Outils Azure Container pour Eclipse**</span><span class="sxs-lookup"><span data-stu-id="840a1-128">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="840a1-129">Permet de créer et déployer un fichier WAR en tant que conteneur Docker à une machine docker.</span><span class="sxs-lookup"><span data-stu-id="840a1-129">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="840a1-130">**Conteneurs Azure pour Eclipse**</span><span class="sxs-lookup"><span data-stu-id="840a1-130">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="840a1-131">Permet de déployer un fichier WAR ou JAR en tant que conteneur Docker sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="840a1-131">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="840a1-132">**Azure Explorer pour Eclipse**</span><span class="sxs-lookup"><span data-stu-id="840a1-132">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="840a1-133">Fournit une interface de style Explorateur pour gérer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="840a1-133">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="840a1-134">**Microsoft JDBC Driver 6.1 pour SQL Server**</span><span class="sxs-lookup"><span data-stu-id="840a1-134">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="840a1-135">Fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="840a1-135">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="840a1-136">**Package pour les bibliothèques Microsoft Azure pour Java**</span><span class="sxs-lookup"><span data-stu-id="840a1-136">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="840a1-137">Fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc.</span><span class="sxs-lookup"><span data-stu-id="840a1-137">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="840a1-138">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="840a1-138">Click **Next**.</span></span> <span data-ttu-id="840a1-139">(Si vous rencontrez des délais d'attente inhabituels lors de l'installation du kit de ressources, assurez-vous que l'option **Contact all update sites during install to find required software** est désactivée.)</span><span class="sxs-lookup"><span data-stu-id="840a1-139">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="840a1-140">Dans la boîte de dialogue **Install Details** (Détails d’installation), cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="840a1-140">In the **Install Details** dialog, click **Next**.</span></span>

   ![Passer en revue les détails de l’installation][03]

1. <span data-ttu-id="840a1-142">Dans la boîte de dialogue **Review Licenses** (Vérifier les licences), passez en revue les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="840a1-142">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="840a1-143">Si vous acceptez les termes des contrats de licence, cliquez sur **I accept the terms of the license agreements** (J’accepte les termes des contrats de licence), puis sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="840a1-143">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="840a1-144">(Les étapes restantes supposent que vous acceptez les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="840a1-144">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="840a1-145">Si vous n'acceptez pas les termes des contrats de licence, quittez le processus d'installation.)</span><span class="sxs-lookup"><span data-stu-id="840a1-145">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>

   ![Review Licenses][04]

   <span data-ttu-id="840a1-147">Eclipse télécharge et installe les packages requis.</span><span class="sxs-lookup"><span data-stu-id="840a1-147">Eclipse will download and install the requisite packages.</span></span>

   ![Progression de l’installation][05]

1. <span data-ttu-id="840a1-149">Si vous êtes invité à redémarrer Eclipse pour terminer l’installation, cliquez sur **Yes**(Oui).</span><span class="sxs-lookup"><span data-stu-id="840a1-149">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>

   ![Invite de redémarrage][06]

## <a name="next-steps"></a><span data-ttu-id="840a1-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="840a1-151">Next steps</span></span>

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
