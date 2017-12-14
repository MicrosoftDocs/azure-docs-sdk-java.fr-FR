---
title: "Gestion des caches Redis à l’aide de l’Explorateur Azure pour Eclipse"
description: "Découvrez comment gérer vos caches redis Azure à l’aide de l’Explorateur Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 010f959b4a381fc625914620c282ef0452f525a9
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="7b7f4-103">Gestion des caches Redis à l’aide de l’Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="7b7f4-103">Managing Redis Caches using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="7b7f4-104">L’Explorateur Azure, qui fait partie du kit de ressources Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour gérer des caches redis dans leur compte Azure à partir de l’IDE Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside the Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="7b7f4-105">Créer un cache Redis à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="7b7f4-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="7b7f4-106">Les étapes suivantes vous indiquent comment créer un cache redis à l’aide de l’Explorateur Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-106">The following steps walk you through the steps to create a redis cache using the Azure Explorer.</span></span>

1. <span data-ttu-id="7b7f4-107">Connectez-vous à votre compte Azure à l’aide de la procédure décrite dans l’article [Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="7b7f4-107">Sign in to your Azure account using the steps in the [Sign In Instructions for the Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="7b7f4-108">Dans la fenêtre de l’outil **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Caches Redis**, puis cliquez sur **Créer un cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-108">In the **Azure Explorer** tool window, expand the **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Créer un Menu pour le Cache Redis][CR01]

1. <span data-ttu-id="7b7f4-110">Quand la boîte de dialogue **Nouveau cache Redis** s’affiche, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="7b7f4-110">When the **New Redis Cache** dialog box appears, specify the following options:</span></span>

   ![Créer une nouvelle boîte de dialogue pour le Cache Redis][CR02]

   <span data-ttu-id="7b7f4-112">a.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-112">a.</span></span> <span data-ttu-id="7b7f4-113">**Nom DNS** : spécifie le sous-domaine DNS pour le nouveau cache Redis, lequel est précédé de « .redis.cache.windows.net », par exemple : *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-113">**DNS Name**: Specifies the DNS subdomain for the new redis cache, which is prepended to ".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="7b7f4-114">b.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-114">b.</span></span> <span data-ttu-id="7b7f4-115">**Abonnement** : spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau cache Redis.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-115">**Subscription**: Specifies the Azure subscription you want to use for the new redis cache.</span></span>

   <span data-ttu-id="7b7f4-116">c.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-116">c.</span></span> <span data-ttu-id="7b7f4-117">**Groupe de ressources** : spécifie le groupe de ressources pour votre cache Redis ; vous devez en choisir un parmi les options ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7b7f4-117">**Resource Group**: Specifies the resource group for your redis cache; you need to choose one of the following options:</span></span>
      * <span data-ttu-id="7b7f4-118">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-118">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="7b7f4-119">**Utiliser existant** : spécifie que vous allez choisir à partir d’une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="7b7f4-120">d.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-120">d.</span></span> <span data-ttu-id="7b7f4-121">**Emplacement** : spécifie l’emplacement où votre cache Redis est créé (par exemple *États-Unis de l’Ouest*).</span><span class="sxs-lookup"><span data-stu-id="7b7f4-121">**Location**: Specifies the location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="7b7f4-122">e.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-122">e.</span></span> <span data-ttu-id="7b7f4-123">**Niveau tarifaire** : spécifie le niveau tarifaire utilisé par votre cache Redis ; ce paramètre détermine le nombre de connexions client.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines the number of client connections.</span></span> <span data-ttu-id="7b7f4-124">(Pour plus d’informations, consultez [Tarification du Cache Redis].)</span><span class="sxs-lookup"><span data-stu-id="7b7f4-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="7b7f4-125">f.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-125">f.</span></span> <span data-ttu-id="7b7f4-126">**Port non-SSL** : spécifie si le cache Redis autorise les connexions non-SSL ; par défaut, seules les connexions SSL sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="7b7f4-127">Une fois que vous avez spécifié tous les paramètres du cache Redis, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="7b7f4-128">Une fois créé, votre cache Redis s’affiche dans l’Explorateur Azure.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-128">After your redis cache has been created, it will be displayed in the Azure Explorer.</span></span>

   ![Cache Redis dans l’Explorateur Azure][CR03]

> [!NOTE]
>
> <span data-ttu-id="7b7f4-130">Pour plus d’informations sur la configuration des paramètres de votre cache Redis Azure, consultez [Configuration du Cache Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="7b7f4-130">For more information about configuring your Azure redis cache settings, see [How to configure Azure Redis Cache].</span></span>
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="7b7f4-131">Afficher les propriétés de votre cache Redis dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="7b7f4-131">Display the properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="7b7f4-132">Dans l’Explorateur Azure, cliquez avec le bouton droit sur votre cache Redis, puis cliquez sur **Afficher les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-132">In the Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Menu contextuel de l’Explorateur Azure permettant d’afficher les propriétés d’un cache Redis][SP01]

1. <span data-ttu-id="7b7f4-134">L’Explorateur Azure affiche les propriétés de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-134">The Azure Explorer displays the properties for your redis cache.</span></span>

   ![Propriétés du cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="7b7f4-136">Supprimer votre cache Redis à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="7b7f4-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="7b7f4-137">Dans l’Explorateur Windows Azure, cliquez avec le bouton droit de votre cache redis sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-137">In the Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Menu contextuel de l’Explorateur Azure permettant de supprimer un cache Redis][DE01]

1. <span data-ttu-id="7b7f4-139">Cliquez sur **OK** quand vous êtes invité à supprimer votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="7b7f4-139">Click **OK** when prompted to delete your redis cache.</span></span>

   ![Invite de suppression d’un cache Redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="7b7f4-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7b7f4-141">Next steps</span></span>

<span data-ttu-id="7b7f4-142">Pour plus d’informations sur les caches Redis Azure, la configuration des paramètres et la tarification, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="7b7f4-142">For more information about Azure redis caches, configuration settings and pricing, see the following links:</span></span>

* <span data-ttu-id="7b7f4-143">[Cache Redis Azure]</span><span class="sxs-lookup"><span data-stu-id="7b7f4-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="7b7f4-144">[Documentation du Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="7b7f4-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="7b7f4-145">[Tarification du Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="7b7f4-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="7b7f4-146">[Configuration du Cache Redis Azure]</span><span class="sxs-lookup"><span data-stu-id="7b7f4-146">[How to configure Azure Redis Cache]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Tarification du Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis Azure]: https://azure.microsoft.com/services/cache/
[Documentation du Cache Redis]: /azure/redis-cache/
[Configuration du Cache Redis Azure]: /azure/redis-cache/cache-configure

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png