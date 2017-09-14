---
title: "Notes de publication des bibliothèques de gestion Azure pour Java | Microsoft Docs"
description: "Découvrez les nouveautés et surveillez les dernières modifications dans les bibliothèques de gestion Azure pour Java"
keywords: "Azure, Java, API, référence, notes, mises à jour, déconseiller"
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="e317b-104">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="e317b-104">Release Notes</span></span> 

## <a name="june-30-2017---110"></a><span data-ttu-id="e317b-105">30 juin 2017 - 1.1.0</span><span class="sxs-lookup"><span data-stu-id="e317b-105">June 30, 2017 - 1.1.0</span></span> 

<span data-ttu-id="e317b-106">La version 1.1 est rétrocompatible avec la version 1.0 dans les interfaces API destinées au public qui ont atteint l’étape de la disponibilité générale (stable) dans la version 1.0.</span><span class="sxs-lookup"><span data-stu-id="e317b-106">V1.1 is backwards compatible with V1.0 in the APIs intended for public use that reached the general availability (stable) stage in V1.0.</span></span>

<span data-ttu-id="e317b-107">Les dernières modifications introduites dans les interfaces API marquées avec l’annotation @Beta dans la version .0</span><span class="sxs-lookup"><span data-stu-id="e317b-107">Some breaking changes were introduced in APIs marked with the @Beta annotation in V.0</span></span>

<span data-ttu-id="e317b-108">Si vous migrez votre code vers la version 1.1.0, vous pouvez utiliser [ces notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) pour préparer votre code à la migration de la version 1.1.0 à 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="e317b-108">If you are migrating your code to 1.1.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) for preparing your code for 1.1.0 from 1.0.0.</span></span>

### <a name="generally-availabile-in-v11"></a><span data-ttu-id="e317b-109">Généralement disponible dans la version 1.1</span><span class="sxs-lookup"><span data-stu-id="e317b-109">Generally availabile in V1.1</span></span>

<span data-ttu-id="e317b-110">Certaines des interfaces API qui étaient toujours en version bêta dans la version 1.0 sont désormais GA (stable) dans la version 1.1, notamment :</span><span class="sxs-lookup"><span data-stu-id="e317b-110">Some of the APIs that were still in Beta in V1.0 are now GA in V1.1, in particular:</span></span>

- <span data-ttu-id="e317b-111">méthodes Async</span><span class="sxs-lookup"><span data-stu-id="e317b-111">async methods</span></span>
- <span data-ttu-id="e317b-112">toutes les méthodes dans le réseau de distribution de contenu qui étaient présentes dans la version bêta</span><span class="sxs-lookup"><span data-stu-id="e317b-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="e317b-113">toutes les méthodes et interfaces dans Application Gateways qui étaient présentes dans la version bêta</span><span class="sxs-lookup"><span data-stu-id="e317b-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="e317b-114">Certaines parties de la bibliothèque sont toujours en préversion.</span><span class="sxs-lookup"><span data-stu-id="e317b-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="e317b-115">Consultez le tableau ci-dessous pour connaître l’état actuel des bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="e317b-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="e317b-116">Service ou fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="e317b-116">Service or feature</span></span> | <span data-ttu-id="e317b-117">Disponible en tant que GA</span><span class="sxs-lookup"><span data-stu-id="e317b-117">Available as GA</span></span> | <span data-ttu-id="e317b-118">Disponible en préversion</span><span class="sxs-lookup"><span data-stu-id="e317b-118">Available as Preview</span></span>  | <span data-ttu-id="e317b-119">Bientôt disponible</span><span class="sxs-lookup"><span data-stu-id="e317b-119">Coming soon</span></span> |
---------|---------|---------|---------|
<span data-ttu-id="e317b-120">Calcul</span><span class="sxs-lookup"><span data-stu-id="e317b-120">Compute</span></span>  | <span data-ttu-id="e317b-121">Les machines virtuelles et leurs extensions, les groupes de machines virtuelles identiques, les disques gérés</span><span class="sxs-lookup"><span data-stu-id="e317b-121">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="e317b-122">Azure container service, Azure container registry</span><span class="sxs-lookup"><span data-stu-id="e317b-122">Azure container service, Azure container registry</span></span> |    |
<span data-ttu-id="e317b-123">Storage</span><span class="sxs-lookup"><span data-stu-id="e317b-123">Storage</span></span>   |  <span data-ttu-id="e317b-124">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="e317b-124">Storage accounts</span></span>       |         |   <span data-ttu-id="e317b-125">Chiffrement</span><span class="sxs-lookup"><span data-stu-id="e317b-125">Encryption</span></span>      |
<span data-ttu-id="e317b-126">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="e317b-126">SQL Database</span></span>  | <span data-ttu-id="e317b-127">Bases de données, pare-feu, pools élastiques</span><span class="sxs-lookup"><span data-stu-id="e317b-127">Databases, firewalls, elastic pools</span></span>        |         |   <span data-ttu-id="e317b-128">Autres fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="e317b-128">More features</span></span>      |
<span data-ttu-id="e317b-129">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="e317b-129">Networking</span></span>    |  <span data-ttu-id="e317b-130">Réseaux virtuels, interfaces réseau, adresses IP, tables de routage, groupes de sécurité réseau, DNS, Traffic Manager, Application Gateways</span><span class="sxs-lookup"><span data-stu-id="e317b-130">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="e317b-131">Équilibreurs de charge</span><span class="sxs-lookup"><span data-stu-id="e317b-131">Load balancers</span></span>     |   <span data-ttu-id="e317b-132">VPN, Network watcher</span><span class="sxs-lookup"><span data-stu-id="e317b-132">VPN, Network watchers</span></span>   |
<span data-ttu-id="e317b-133">Autres services</span><span class="sxs-lookup"><span data-stu-id="e317b-133">More services</span></span>    |  <span data-ttu-id="e317b-134">Gestionnaire des ressources, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="e317b-134">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="e317b-135">Applications Web, applications de fonction, Service Bus, Graph RBAC, DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e317b-135">Web apps, Function apps, Service Bus, Graph RBAC, DocumentDB</span></span>   | <span data-ttu-id="e317b-136">Surveiller, Scheduler, gestion des fonctions, rechercher, autres fonctionnalités Graph RBAC</span><span class="sxs-lookup"><span data-stu-id="e317b-136">Monitor ,Scheduler, Functions management, Search, more Graph RBAC features</span></span>        |
<span data-ttu-id="e317b-137">Fondamentaux</span><span class="sxs-lookup"><span data-stu-id="e317b-137">Fundamentals</span></span>     |   <span data-ttu-id="e317b-138">Authentification - cœur, méthodes Async</span><span class="sxs-lookup"><span data-stu-id="e317b-138">Authentication - core , Async methods</span></span>       |      |         |

### <a name="import-with-maven"></a><span data-ttu-id="e317b-139">Importer avec Maven</span><span class="sxs-lookup"><span data-stu-id="e317b-139">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="e317b-140">Obtenir de l’aide et donner son avis</span><span class="sxs-lookup"><span data-stu-id="e317b-140">Get help and give feedback</span></span>

<span data-ttu-id="e317b-141">Consultez la communauté [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) pour obtenir de l’aide concernant les bibliothèques dans votre code.</span><span class="sxs-lookup"><span data-stu-id="e317b-141">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="e317b-142">Si vous rencontrez des bogues ou si vous avez des suggestions pour améliorer les bibliothèques, veuillez envoyer un rapport d’erreur via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="e317b-142">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>

### <a name="migrate-from-previous-releases"></a><span data-ttu-id="e317b-143">Migrer à partir de versions précédentes</span><span class="sxs-lookup"><span data-stu-id="e317b-143">Migrate from previous releases</span></span>

<span data-ttu-id="e317b-144">[Migrer à partir de la version 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrer à partir de la version 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span><span class="sxs-lookup"><span data-stu-id="e317b-144">[Migrate from 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md)  [Migrate from 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)</span></span>


