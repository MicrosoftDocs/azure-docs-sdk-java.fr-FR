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
ms.openlocfilehash: 015cb0615c28711ebb8feb5cea584a8a3779fa54
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="release-notes"></a><span data-ttu-id="231d2-104">Notes de publication</span><span class="sxs-lookup"><span data-stu-id="231d2-104">Release Notes</span></span> 

## <a name="october-5-2017---130"></a><span data-ttu-id="231d2-105">5 octobre 2017 - version 1.3.0</span><span class="sxs-lookup"><span data-stu-id="231d2-105">October 5, 2017 - 1.3.0</span></span> 

<span data-ttu-id="231d2-106">La version 1.3.0 a une compatibilité descendante avec les versions précédentes pour des services et une utilisation fonctionnelle qui atteignaient l’étape (stable) de la disponibilité générale dans les versions précédentes.</span><span class="sxs-lookup"><span data-stu-id="231d2-106">Version 1.3.0 is backwards compatible with previous versions for serivces and featured use that reached the general availability (stable) stage in previous releases.</span></span>

<span data-ttu-id="231d2-107">Les dernières modifications des versions préliminaires pour ces services possèdent l’annotation @Beta.</span><span class="sxs-lookup"><span data-stu-id="231d2-107">Any breaking changes from Preview versions for those services are marked with the @Beta annotation.</span></span>

<span data-ttu-id="231d2-108">Si vous migrez votre code vers la version 1.3.0, vous pouvez utiliser [ces notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) pour préparer votre code existant à la migration vers la version 1.3.</span><span class="sxs-lookup"><span data-stu-id="231d2-108">If you are migrating your code to 1.3.0, you can use [these notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) to prepare your existing code for the 1.3 version.</span></span>

### <a name="generally-availabile-in-v13"></a><span data-ttu-id="231d2-109">Généralement disponible dans la version 1.3</span><span class="sxs-lookup"><span data-stu-id="231d2-109">Generally availabile in V1.3</span></span>

<span data-ttu-id="231d2-110">Certaines API toujours en version bêta dans les versions précédentes sont désormais GA (stable), notamment :</span><span class="sxs-lookup"><span data-stu-id="231d2-110">Some of the APIs that were still in Beta in previous releases are now GA, in particular:</span></span>

- <span data-ttu-id="231d2-111">méthodes Async</span><span class="sxs-lookup"><span data-stu-id="231d2-111">async methods</span></span>
- <span data-ttu-id="231d2-112">toutes les méthodes dans le réseau de distribution de contenu qui étaient présentes dans la version bêta</span><span class="sxs-lookup"><span data-stu-id="231d2-112">all methods in CDN that were previously in Beta</span></span>
- <span data-ttu-id="231d2-113">toutes les méthodes et interfaces dans Application Gateways qui étaient présentes dans la version bêta</span><span class="sxs-lookup"><span data-stu-id="231d2-113">all methods and interfaces in Application Gateways that were previously in Beta</span></span>

 <span data-ttu-id="231d2-114">Certaines parties de la bibliothèque sont toujours en préversion.</span><span class="sxs-lookup"><span data-stu-id="231d2-114">Some parts of the library are still in Preview.</span></span> <span data-ttu-id="231d2-115">Consultez le tableau ci-dessous pour connaître l’état actuel des bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="231d2-115">Refer to the table below for the current state of the libraries:</span></span>

<span data-ttu-id="231d2-116">Service ou fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="231d2-116">Service or feature</span></span> | <span data-ttu-id="231d2-117">Disponible en tant que GA</span><span class="sxs-lookup"><span data-stu-id="231d2-117">Available as GA</span></span> | <span data-ttu-id="231d2-118">Disponible en préversion</span><span class="sxs-lookup"><span data-stu-id="231d2-118">Available as Preview</span></span> 
---------|---------|---------|-
<span data-ttu-id="231d2-119">Calcul</span><span class="sxs-lookup"><span data-stu-id="231d2-119">Compute</span></span>  | <span data-ttu-id="231d2-120">Les machines virtuelles et leurs extensions, les groupes de machines virtuelles identiques, les disques gérés</span><span class="sxs-lookup"><span data-stu-id="231d2-120">Virtual machines and VM extensions, Virtual machine scale sets, managed disks</span></span>   | <span data-ttu-id="231d2-121">Azure container service, Azure container registry</span><span class="sxs-lookup"><span data-stu-id="231d2-121">Azure container service, Azure container registry</span></span> 
<span data-ttu-id="231d2-122">Storage</span><span class="sxs-lookup"><span data-stu-id="231d2-122">Storage</span></span>   |  <span data-ttu-id="231d2-123">Comptes de stockage</span><span class="sxs-lookup"><span data-stu-id="231d2-123">Storage accounts</span></span>       |    <span data-ttu-id="231d2-124">Chiffrement</span><span class="sxs-lookup"><span data-stu-id="231d2-124">Encryption</span></span>     
<span data-ttu-id="231d2-125">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="231d2-125">SQL Database</span></span>  | <span data-ttu-id="231d2-126">Bases de données, pare-feu, pools élastiques</span><span class="sxs-lookup"><span data-stu-id="231d2-126">Databases, firewalls, elastic pools</span></span>              
<span data-ttu-id="231d2-127">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="231d2-127">Networking</span></span>    |  <span data-ttu-id="231d2-128">Réseaux virtuels, interfaces réseau, adresses IP, tables de routage, groupes de sécurité réseau, DNS, Traffic Manager, Application Gateways</span><span class="sxs-lookup"><span data-stu-id="231d2-128">Virtual networks , network interfaces , IP addresses ,routing tables, network security groups , DNS, Traffic managers, Application gateways</span></span>  |    <span data-ttu-id="231d2-129">Équilibreurs de charge, homologation de réseaux, passerelle de réseau virtuel, observateurs de réseau</span><span class="sxs-lookup"><span data-stu-id="231d2-129">Load balancers, Network peering, Virtual Network Gateway, Network watchers</span></span> 
<span data-ttu-id="231d2-130">Plus de services</span><span class="sxs-lookup"><span data-stu-id="231d2-130">More services</span></span>    |  <span data-ttu-id="231d2-131">Gestionnaire des ressources, Key Vault, Redis, CDN, Batch</span><span class="sxs-lookup"><span data-stu-id="231d2-131">Resource Manager, Key Vault, Redis,  CDN, Batch</span></span>       |  <span data-ttu-id="231d2-132">Applications Web, applications de fonction, Service Bus, Graphique RBAC, Cosmos DB, Recherche</span><span class="sxs-lookup"><span data-stu-id="231d2-132">Web apps, Function apps, Service Bus, Graph RBAC, Cosmos DB, Search</span></span>  
<span data-ttu-id="231d2-133">Notions de base</span><span class="sxs-lookup"><span data-stu-id="231d2-133">Fundamentals</span></span>     |   <span data-ttu-id="231d2-134">Authentification - Éléments de base, méthodes Async, identité du service administré</span><span class="sxs-lookup"><span data-stu-id="231d2-134">Authentication - core , Async methods , Managed Service Identity</span></span>      |      |

> <span data-ttu-id="231d2-135">Les fonctionnalités en version préliminaire possèdent l’annotation `@Beta` au niveau de la classe, de l’interface ou de la méthode dans les bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="231d2-135">Preview features are marked with a `@Beta` annotation at the class or interface or method level in libraries.</span></span> <span data-ttu-id="231d2-136">Ces fonctionnalités sont susceptibles d'être modifiées.</span><span class="sxs-lookup"><span data-stu-id="231d2-136">These features are subject to change.</span></span> <span data-ttu-id="231d2-137">Elles peuvent être modifiées de quelque façon que ce soit, ou même supprimées, à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="231d2-137">They can be modified in any way, or even removed, in the future.</span></span>

### <a name="import-with-maven"></a><span data-ttu-id="231d2-138">Importer avec Maven</span><span class="sxs-lookup"><span data-stu-id="231d2-138">Import with Maven</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a><span data-ttu-id="231d2-139">Obtenir de l’aide et donner son avis</span><span class="sxs-lookup"><span data-stu-id="231d2-139">Get help and give feedback</span></span>

<span data-ttu-id="231d2-140">Consultez la communauté [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) pour obtenir de l’aide concernant les bibliothèques dans votre code.</span><span class="sxs-lookup"><span data-stu-id="231d2-140">Check out the [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) community for help using the libraries in your own code.</span></span> <span data-ttu-id="231d2-141">Si vous rencontrez des bogues ou si vous avez des suggestions pour améliorer les bibliothèques, veuillez envoyer un rapport d’erreur via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span><span class="sxs-lookup"><span data-stu-id="231d2-141">If you encounter any bugs or have suggestions to improve these libraries, please file issues via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).</span></span>


