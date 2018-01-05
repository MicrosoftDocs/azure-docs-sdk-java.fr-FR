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
# <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="4b006-103">Installer le Kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="4b006-103">Install the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="4b006-104">Le kit de ressources Azure pour Eclipse contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications cloud Azure depuis l’environnement de développement Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4b006-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy cloud  applications to Azure from the Eclipse development environment.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="4b006-105">Le kit de ressources Azure pour Eclipse est un projet Open Source, dont le code source est disponible sous licence MIT sur le site du projet sur GitHub à l’adresse suivante :</span><span class="sxs-lookup"><span data-stu-id="4b006-105">The Azure Toolkit for Eclipse is an Open Source project, whose source code is available under the MIT License from the project's site on GitHub at the following URL:</span></span> 
> 
> <span data-ttu-id="4b006-106"><https://github.com/microsoft/azure-tools-for-java></span><span class="sxs-lookup"><span data-stu-id="4b006-106"><https://github.com/microsoft/azure-tools-for-java></span></span> 
> 

<span data-ttu-id="4b006-107">Les étapes suivantes vous montrent comment installer le kit de ressources Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4b006-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="4b006-108">Pour installer le Kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="4b006-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="4b006-109">Démarrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="4b006-109">Start Eclipse.</span></span>

1. <span data-ttu-id="4b006-110">Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="4b006-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Installation du kit de ressources Azure pour Eclipse][01]

1. <span data-ttu-id="4b006-112">Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse/`, puis appuyez sur la touche **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="4b006-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="4b006-113">Dans le volet **Name** (Nom), cochez **Azure Toolkit for Eclipse** (Kit de ressources Azure pour Eclipse) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l'installation pour trouver le logiciel requis).</span><span class="sxs-lookup"><span data-stu-id="4b006-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="4b006-114">Votre écran doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b006-114">Your screen should appear similar to the following:</span></span>
   
   ![Installation du kit de ressources Azure pour Eclipse][02]

1. <span data-ttu-id="4b006-116">En développant **Kit de ressources Azure pour Eclipse**, vous verrez une liste des composants qui seront installés. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4b006-116">If you expand **Azure Toolkit for Eclipse**, you will see a list of components that will be installed; for example:</span></span>

   | <span data-ttu-id="4b006-117">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="4b006-117">Feature</span></span> | <span data-ttu-id="4b006-118">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="4b006-118">Description</span></span> | 
   |---|---| 
   | <span data-ttu-id="4b006-119">**Plug-in Application Insights pour Java**</span><span class="sxs-lookup"><span data-stu-id="4b006-119">**Application Insights Plugin for Java**</span></span> | <span data-ttu-id="4b006-120">Permet d’utiliser les services de journalisation et d’analyse de télémétrie d’Azure pour vos applications et instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="4b006-120">Allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span> | 
   | <span data-ttu-id="4b006-121">**Plug-in Azure Common**</span><span class="sxs-lookup"><span data-stu-id="4b006-121">**Azure Common Plugin**</span></span> | <span data-ttu-id="4b006-122">Fournit les fonctionnalités communes dont les autres composants du kit de ressources ont besoin.</span><span class="sxs-lookup"><span data-stu-id="4b006-122">provides the common functionality needed by other toolkit components.</span></span> | 
   | <span data-ttu-id="4b006-123">**Outils Azure Container pour Eclipse**</span><span class="sxs-lookup"><span data-stu-id="4b006-123">**Azure Container Tools for Eclipse**</span></span> | <span data-ttu-id="4b006-124">Permet de créer et déployer un fichier WAR en tant que conteneur Docker à une machine docker.</span><span class="sxs-lookup"><span data-stu-id="4b006-124">Enables you to build and deploy a .WAR as a Docker container to a docker machine.</span></span> | 
   | <span data-ttu-id="4b006-125">**Conteneurs Azure pour Eclipse**</span><span class="sxs-lookup"><span data-stu-id="4b006-125">**Azure Containers for Eclipse**</span></span> | <span data-ttu-id="4b006-126">Permet de déployer un fichier WAR ou JAR en tant que conteneur Docker sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="4b006-126">Enables you to deploy a .WAR or .JAR artifact as a Docker container to an Azure virtual machine.</span></span> | 
   | <span data-ttu-id="4b006-127">**Azure Explorer pour Eclipse**</span><span class="sxs-lookup"><span data-stu-id="4b006-127">**Azure Explorer for Eclipse**</span></span> | <span data-ttu-id="4b006-128">Fournit une interface de style Explorateur pour gérer vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="4b006-128">Provides an explorer-style interface for managing your Azure resources.</span></span> | 
   | <span data-ttu-id="4b006-129">**Microsoft JDBC Driver 6.1 pour SQL Server**</span><span class="sxs-lookup"><span data-stu-id="4b006-129">**Microsoft JDBC Driver 6.1 for SQL Server**</span></span> | <span data-ttu-id="4b006-130">Fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="4b006-130">Provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span> | 
   | <span data-ttu-id="4b006-131">**Package pour les bibliothèques Microsoft Azure pour Java**</span><span class="sxs-lookup"><span data-stu-id="4b006-131">**Package for Microsoft Azure Libraries for Java**</span></span> | <span data-ttu-id="4b006-132">Fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc.</span><span class="sxs-lookup"><span data-stu-id="4b006-132">Provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span> | 

1. <span data-ttu-id="4b006-133">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="4b006-133">Click **Next**.</span></span> <span data-ttu-id="4b006-134">(Si vous rencontrez des délais d'attente inhabituels lors de l'installation du kit de ressources, assurez-vous que l'option **Contact all update sites during install to find required software** est désactivée.)</span><span class="sxs-lookup"><span data-stu-id="4b006-134">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="4b006-135">Dans la boîte de dialogue **Install Details** (Détails d’installation), cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="4b006-135">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Passer en revue les détails de l’installation][03]

1. <span data-ttu-id="4b006-137">Dans la boîte de dialogue **Review Licenses** (Vérifier les licences), passez en revue les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="4b006-137">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="4b006-138">Si vous acceptez les termes des contrats de licence, cliquez sur **I accept the terms of the license agreements** (J’accepte les termes des contrats de licence), puis sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="4b006-138">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="4b006-139">(Les étapes restantes supposent que vous acceptez les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="4b006-139">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="4b006-140">Si vous n'acceptez pas les termes des contrats de licence, quittez le processus d'installation.)</span><span class="sxs-lookup"><span data-stu-id="4b006-140">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licenses][04]
   
   <span data-ttu-id="4b006-142">Eclipse télécharge et installe les packages requis.</span><span class="sxs-lookup"><span data-stu-id="4b006-142">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progression de l’installation][05]

1. <span data-ttu-id="4b006-144">Si vous êtes invité à redémarrer Eclipse pour terminer l’installation, cliquez sur **Yes**(Oui).</span><span class="sxs-lookup"><span data-stu-id="4b006-144">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Invite de redémarrage][06]

## <a name="next-steps"></a><span data-ttu-id="4b006-146">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b006-146">Next steps</span></span>

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
