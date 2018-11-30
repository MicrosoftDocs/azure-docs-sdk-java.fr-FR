---
title: Outils pour développeurs Azure Java | Microsoft Docs
description: Intégrations d’IDE, émulateurs, explorateurs de ressources et interfaces de ligne de commande pour développeurs Azure Java.
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 11/13/2018
ms.author: routlaw
ms.openlocfilehash: 9e9828540ddc678f69eab11f5a61eef8bf8e916c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339013"
---
# <a name="azure-tools-for-java-developers"></a><span data-ttu-id="798f7-103">Outils Azure pour développeurs Java</span><span class="sxs-lookup"><span data-stu-id="798f7-103">Azure tools for Java developers</span></span>

## <a name="supported-jdk-runtimes"></a><span data-ttu-id="798f7-104">Runtimes JDK pris en charge</span><span class="sxs-lookup"><span data-stu-id="798f7-104">Supported JDK runtimes</span></span>

<span data-ttu-id="798f7-105">Les développeurs Java disponibles sur Azure et Azure Stack peuvent générer et exécuter des applications de production Java 7, 8 et 11 grâce aux [versions OpenJDK d’Azul Systems Zulu Entreprise](https://www.azul.com/downloads/azure-only/zulu/) sans entraîner de frais supplémentaires de support.</span><span class="sxs-lookup"><span data-stu-id="798f7-105">Java developers on Azure and Azure Stack can build and run production Java 7,8, and 11 applications using [Azul Systems Zulu Enterprise builds of OpenJDK](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="798f7-106">Si vous exécutez actuellement des applications Java par le biais d’autres JDK, déplacez-les plutôt vers Zulu sur Azure pour disposer gratuitement d’un support et d’une maintenance.</span><span class="sxs-lookup"><span data-stu-id="798f7-106">If you’re currently running Java apps with other JDKs, consider migrating to Zulu on Azure for free support and maintenance.</span></span> 

<span data-ttu-id="798f7-107">Pour en savoir plus sur les kits de développement pris en charge disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="798f7-107">For more information about the supported JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="eclipse-and-intellij-plugins"></a><span data-ttu-id="798f7-108">Plug-ins Eclipse et IntelliJ</span><span class="sxs-lookup"><span data-stu-id="798f7-108">Eclipse and IntelliJ plugins</span></span>

<span data-ttu-id="798f7-109">Gérez les ressources Azure et déployez des applications à partir de votre environnement IDE avec le kit de ressources Azure pour [Eclipse](eclipse/azure-toolkit-for-eclipse.md) et [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span><span class="sxs-lookup"><span data-stu-id="798f7-109">Manage Azure resources and deploy apps from your IDE with The Azure toolkits for [Eclipse](eclipse/azure-toolkit-for-eclipse.md) and [IntelliJ](intellij/azure-toolkit-for-intellij.md).</span></span>   

![Kit de ressources IntelliJ affichant l’Explorateur Azure](media/intelliJ-azure-explorer.png)

<span data-ttu-id="798f7-111">[Prise en main du kit de ressources Azure pour Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Prise en main du kit de ressources Azure pour IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span><span class="sxs-lookup"><span data-stu-id="798f7-111">[Get started with Azure Toolkit for Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Get started with Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app)</span></span> 

## <a name="visual-studio-code"></a><span data-ttu-id="798f7-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="798f7-112">Visual Studio Code</span></span>

<span data-ttu-id="798f7-113">[VS Code](https://code.visualstudio.com/) est un éditeur de code léger, mais puissant, disponible sur MacOs, Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="798f7-113">[VS Code](https://code.visualstudio.com/) is a lightweight but powerful code editor available for MacOS, Windows, and Linux.</span></span> <span data-ttu-id="798f7-114">Cette solution supporte un flux de travail de développement Java simple et moderne via un jeu d’extensions assurant une prise en charge du projet, l’exécution du code, le débogage, le référencement et la navigation.</span><span class="sxs-lookup"><span data-stu-id="798f7-114">VS Code supports a simple, modern Java development workflow through a set of extensions that provide project support, code completion, debugging, linting, and navigation.</span></span>

<span data-ttu-id="798f7-115">[Prise en main de VS Code et Java](https://code.visualstudio.com/docs/java)
[Pack d’extensions Java pour VS Code](https://code.visualstudio.com/docs/java/extensions)</span><span class="sxs-lookup"><span data-stu-id="798f7-115">[Get Started with VS Code and Java](https://code.visualstudio.com/docs/java)
[Java extension pack for VS Code](https://code.visualstudio.com/docs/java/extensions)</span></span>  

## <a name="azure-cli-20"></a><span data-ttu-id="798f7-116">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="798f7-116">Azure CLI 2.0</span></span>

<span data-ttu-id="798f7-117">Azure CLI 2.0 offre une expérience en ligne de commande pour gérer les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="798f7-117">The Azure 2.0 CLI provides a command-line experience to manage Azure resources.</span></span> <span data-ttu-id="798f7-118">Vous pouvez l’utiliser dans votre navigateur avec [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) ou [l’installer](https://docs.microsoft.com/cli/azure/install-azure-cli) sur macOS, Linux et Windows et l’exécuter à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="798f7-118">You can use it in your browser with [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview), or you can [install](https://docs.microsoft.com/cli/azure/install-azure-cli) it on macOS, Linux, and Windows and run it from the command line.</span></span>

<span data-ttu-id="798f7-119">[Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="798f7-119">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>

## <a name="azure-storage-explorer"></a><span data-ttu-id="798f7-120">Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="798f7-120">Azure Storage Explorer</span></span> 

<span data-ttu-id="798f7-121">Gérez les comptes de stockage, conteneurs et fichiers blob Azure à partir de votre bureau.</span><span class="sxs-lookup"><span data-stu-id="798f7-121">Manage Azure storage accounts, containers, and blobs/files from your desktop.</span></span> <span data-ttu-id="798f7-122">L’Explorateur de stockage Azure est actuellement en version préliminaire et fonctionne sur Windows, macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="798f7-122">Azure Storage Explorer is currently in Preview and works on Windows, macOS, and Linux.</span></span>

[<span data-ttu-id="798f7-123">Prise en main de l’explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="798f7-123">Get started with Azure Storage Explorer</span></span>](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)
