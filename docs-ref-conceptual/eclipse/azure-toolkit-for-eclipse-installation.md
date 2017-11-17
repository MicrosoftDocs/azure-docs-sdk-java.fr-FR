---
title: Installation du kit de ressources Azure pour Eclipse
description: "Apprenez à installer le Kit de ressources Azure pour Eclipse."
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
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 59a8bfb6ab4db8ea8c6c9025ca3ced8a13192628
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="installing-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="01b67-103">Installation du kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="01b67-103">Installing the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="01b67-104">Le kit de ressources Azure pour Eclipse contient des modèles et des fonctionnalités qui vous permettent de créer, de développer, de tester et de déployer des applications Azure avec l’environnement de développement Eclipse.</span><span class="sxs-lookup"><span data-stu-id="01b67-104">The Azure Toolkit for Eclipse provides templates and functionality that allow you to easily create, develop, test, and deploy Azure applications using the Eclipse development environment.</span></span> <span data-ttu-id="01b67-105">Le kit de ressources Azure pour Eclipse est un projet Open Source.</span><span class="sxs-lookup"><span data-stu-id="01b67-105">The Azure Toolkit for Eclipse is an Open Source project.</span></span> <span data-ttu-id="01b67-106">Le code source est disponible sous la licence du MIT à partir de <https://github.com/microsoft/azure-tools-for-java>.</span><span class="sxs-lookup"><span data-stu-id="01b67-106">The source code is available under the MIT License from <https://github.com/microsoft/azure-tools-for-java>.</span></span>

<span data-ttu-id="01b67-107">Les étapes suivantes vous montrent comment installer le kit de ressources Azure pour Eclipse.</span><span class="sxs-lookup"><span data-stu-id="01b67-107">The following steps show you how to install the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="to-install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="01b67-108">Pour installer le Kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="01b67-108">To install the Azure Toolkit for Eclipse</span></span>

1. <span data-ttu-id="01b67-109">Démarrez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="01b67-109">Start Eclipse.</span></span>

1. <span data-ttu-id="01b67-110">Cliquez sur le menu **Help** (Aide), puis sur **Install New Software** (Installer un nouveau logiciel), comme indiqué dans l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="01b67-110">Click the **Help** menu, and then click **Install New Software**, as shown in the following illustration.</span></span>
   
   ![Installation du kit de ressources Azure pour Eclipse][01]

1. <span data-ttu-id="01b67-112">Dans la boîte de dialogue **Available Software** (Logiciels disponibles), dans la zone de texte **Work with** (Fonctionnement avec), tapez `http://dl.microsoft.com/eclipse/`, puis appuyez sur la touche **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="01b67-112">In the **Available Software** dialog, within the **Work with** text box, type `http://dl.microsoft.com/eclipse/` followed by the **Enter** key.</span></span>

1. <span data-ttu-id="01b67-113">Dans le volet **Name** (Nom), cochez **Azure Toolkit for Eclipse** (Kit de ressources Azure pour Eclipse) et décochez **Contact all update sites during install to find required software** (Contacter tous les sites de mise à jour durant l'installation pour trouver le logiciel requis).</span><span class="sxs-lookup"><span data-stu-id="01b67-113">In the **Name** pane, check **Azure Toolkit for Eclipse**, and uncheck **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="01b67-114">Votre écran doit se présenter comme suit :</span><span class="sxs-lookup"><span data-stu-id="01b67-114">Your screen should appear similar to the following:</span></span>
   
   ![Installation du kit de ressources Azure pour Eclipse][02]

1. <span data-ttu-id="01b67-116">Si vous développez le **Kit de ressources Azure pour Eclipse**, la liste d’objets suivante apparaît :</span><span class="sxs-lookup"><span data-stu-id="01b67-116">If you expand the **Azure Toolkit for Eclipse**, you will see a list of items like following example:</span></span>
   
   * <span data-ttu-id="01b67-117">**Application Insights Plugin for Java**: ce composant vous permet d'utiliser les services de journalisation et d'analyse de télémétrie d'Azure pour vos applications et instances de serveur.</span><span class="sxs-lookup"><span data-stu-id="01b67-117">**Application Insights Plugin for Java**: This component allows you to use Azure's telemetry logging and analysis services for your applications and server instances.</span></span>
   * <span data-ttu-id="01b67-118">**Azure Access Control Services Filter**: ce composant prend en charge l’authentification des utilisateurs de l’application avec Azure ACS, permettant les scénarios d’authentification unique et l’externalisation de la logique d’identité hors de l’application.</span><span class="sxs-lookup"><span data-stu-id="01b67-118">**Azure Access Control Services Filter**: This component provides support for authenticating application users with Azure ACS, enabling single sign-on scenarios and externalizing identity logic from the application.</span></span>
   * <span data-ttu-id="01b67-119">**Azure Common Plugin**: ce composant fournit les fonctionnalités communes nécessaires aux autres composants du kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="01b67-119">**Azure Common Plugin**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="01b67-120">**Azure Explorer for Eclipse**: ce composant fournit les fonctionnalités communes nécessaires aux autres composants du kit de ressources.</span><span class="sxs-lookup"><span data-stu-id="01b67-120">**Azure Explorer for Eclipse**: This component provides the common functionality needed by other toolkit components.</span></span>
   * <span data-ttu-id="01b67-121">**Azure Plugin for Eclipse with Java**: ce composant prend en charge le développement de projets qui aident à générer, tester et déployer des applications Java pour le cloud Microsoft Azure dans Eclipse et par le biais de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="01b67-121">**Azure Plugin for Eclipse with Java**: This component provides support for developing projects that help build, test and deploy Java applications for the Microsoft Azure cloud in Eclipse and via command line.</span></span>
   * <span data-ttu-id="01b67-122">**Azure Web Apps Plugin with Java**: ce composant prend en charge le déploiement d’applications web Java sur des conteneurs d’application web Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="01b67-122">**Azure Web Apps Plugin with Java**: This component provides support for deploying Java web applications to Microsoft Azure Web App containers.</span></span>
   * <span data-ttu-id="01b67-123">**Microsoft JDBC Driver 4.2 for SQL Server**: ce composant fournit l’API JDBC pour SQL Server et Microsoft Azure SQL Database pour Java Platform Enterprise Edition 8.</span><span class="sxs-lookup"><span data-stu-id="01b67-123">**Microsoft JDBC Driver 4.2 for SQL Server**: This component provides JDBC API for SQL Server and Microsoft Azure SQL Database for Java Platform Enterprise Edition 8.</span></span>
   * <span data-ttu-id="01b67-124">**Package for Apache Qpid Client Libraries for JMS**: ce composant fournit le composant client JMS du projet Apache Qpid pour permettre à votre application d’utiliser la messagerie AMQP dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="01b67-124">**Package for Apache Qpid Client Libraries for JMS**: This component provides the JMS client component from the Apache Qpid project to enable your application to use AMQP messaging in Microsoft Azure.</span></span>
   * <span data-ttu-id="01b67-125">**Package for Microsoft Azure Libraries for Java**: ce composant fournit des API pour accéder aux services Microsoft Azure, tels que Storage, Service Bus, le runtime de service, etc.</span><span class="sxs-lookup"><span data-stu-id="01b67-125">**Package for Microsoft Azure Libraries for Java**: This component provides APIs for accessing Microsoft Azure services, such as storage, service bus, service runtime, etc.</span></span>

1. <span data-ttu-id="01b67-126">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="01b67-126">Click **Next**.</span></span> <span data-ttu-id="01b67-127">(Si vous rencontrez des délais d'attente inhabituels lors de l'installation du kit de ressources, assurez-vous que l'option **Contact all update sites during install to find required software** est désactivée.)</span><span class="sxs-lookup"><span data-stu-id="01b67-127">(If you experience unusual delays when installing the toolkit, ensure that **Contact all update sites during install to find required software** is unchecked.)</span></span>

1. <span data-ttu-id="01b67-128">Dans la boîte de dialogue **Install Details** (Détails d’installation), cliquez sur **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="01b67-128">In the **Install Details** dialog, click **Next**.</span></span>
   
   ![Passer en revue les détails de l’installation][03]

1. <span data-ttu-id="01b67-130">Dans la boîte de dialogue **Review Licenses** (Vérifier les licences), passez en revue les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="01b67-130">In the **Review Licenses** dialog, review the terms of the license agreements.</span></span> <span data-ttu-id="01b67-131">Si vous acceptez les termes des contrats de licence, cliquez sur **I accept the terms of the license agreements** (J’accepte les termes des contrats de licence), puis sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="01b67-131">If you accept the terms of the license agreements, click **I accept the terms of the license agreements** and then click **Finish**.</span></span> <span data-ttu-id="01b67-132">(Les étapes restantes supposent que vous acceptez les termes des contrats de licence.</span><span class="sxs-lookup"><span data-stu-id="01b67-132">(The remaining steps assume you do accept the terms of the license agreements.</span></span> <span data-ttu-id="01b67-133">Si vous n'acceptez pas les termes des contrats de licence, quittez le processus d'installation.)</span><span class="sxs-lookup"><span data-stu-id="01b67-133">If you do not accept the terms of the license agreements, exit the installation process.)</span></span>
   
   ![Review Licenses][04]
   
   <span data-ttu-id="01b67-135">Eclipse télécharge et installe les packages requis.</span><span class="sxs-lookup"><span data-stu-id="01b67-135">Eclipse will download and install the requisite packages.</span></span>
   
   ![Progression de l’installation][05]

1. <span data-ttu-id="01b67-137">Si vous êtes invité à redémarrer Eclipse pour terminer l’installation, cliquez sur **Yes**(Oui).</span><span class="sxs-lookup"><span data-stu-id="01b67-137">If prompted to restart Eclipse to complete installation, click **Yes**.</span></span>
   
   ![Invite de redémarrage][06]

## <a name="next-steps"></a><span data-ttu-id="01b67-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01b67-139">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690946.aspx -->

<!-- IMG List -->

[01]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-01.png
[02]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-02.png
[03]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-03.png
[04]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-04.png
[05]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-05.png
[06]: media/azure-toolkit-for-eclipse-installation/eclipse-installation-06.png
