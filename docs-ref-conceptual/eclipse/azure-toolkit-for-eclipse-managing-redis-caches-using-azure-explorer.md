---
title: Gestion des caches Redis à l’aide de l’Explorateur Azure pour Eclipse
description: Découvrez comment gérer vos caches redis Azure à l’aide de l’Explorateur Azure pour Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 2d3f2363bd0b41808cd409417327b924cb86d85b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954820"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-eclipse"></a>Gestion des caches Redis à l’aide de l’Explorateur Azure pour Eclipse

L’Explorateur Azure, qui fait partie du kit de ressources Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour gérer des caches redis dans leur compte Azure à partir de l’IDE Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Créer un cache Redis à l’aide d’Eclipse

Les étapes suivantes vous indiquent comment créer un cache redis à l’aide de l’Explorateur Azure.

1. Connectez-vous à votre compte Azure à l’aide de la procédure décrite dans l’article [Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse].

1. Dans la fenêtre de l’outil **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Caches Redis**, puis cliquez sur **Créer un cache Redis**.

   ![Créer un Menu pour le Cache Redis][CR01]

1. Quand la boîte de dialogue **Nouveau cache Redis** s’affiche, spécifiez les options suivantes :

   ![Créer une nouvelle boîte de dialogue pour le Cache Redis][CR02]

   a. **Nom DNS** : spécifie le sous-domaine DNS pour le nouveau cache Redis, lequel est précédé de « .redis.cache.windows.net », par exemple : *wingtiptoys.redis.cache.windows.net*.

   b. **Abonnement** : spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau cache Redis.

   c. **Groupe de ressources** : spécifie le groupe de ressources pour votre cache Redis ; vous devez en choisir un parmi les options ci-dessous :
      * **Créer** : spécifie que vous souhaitez créer un groupe de ressources.
      * **Utiliser existant** : spécifie que vous allez choisir à partir d’une liste de groupes de ressources associés à votre compte Azure.

   d. **Emplacement** : spécifie l’emplacement où votre cache Redis est créé (par exemple *États-Unis de l’Ouest*).

   e. **Niveau tarifaire** : spécifie le niveau tarifaire utilisé par votre cache Redis ; ce paramètre détermine le nombre de connexions client. (Pour plus d’informations, consultez [Tarification du Cache Redis].)

   f. **Port non-SSL** : spécifie si le cache Redis autorise les connexions non-SSL ; par défaut, seules les connexions SSL sont autorisées.

1. Une fois que vous avez spécifié tous les paramètres du cache Redis, cliquez sur **OK**.

Une fois créé, votre cache Redis s’affiche dans l’Explorateur Azure.

   ![Cache Redis dans l’Explorateur Azure][CR03]

> [!NOTE]
>
> Pour plus d’informations sur la configuration des paramètres de votre cache Redis Azure, consultez [Configuration du Cache Redis Azure].
>

## <a name="display-the-properties-for-your-redis-cache-in-eclipse"></a>Afficher les propriétés de votre cache Redis dans Eclipse

1. Dans l’Explorateur Azure, cliquez avec le bouton droit sur votre cache Redis, puis cliquez sur **Afficher les propriétés**.

   ![Menu contextuel de l’Explorateur Azure permettant d’afficher les propriétés d’un cache Redis][SP01]

1. L’Explorateur Azure affiche les propriétés de votre cache Redis.

   ![Propriétés du cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Supprimer votre cache Redis à l’aide d’Eclipse

1. Dans l’Explorateur Windows Azure, cliquez avec le bouton droit de votre cache redis sur **Supprimer**.

   ![Menu contextuel de l’Explorateur Azure permettant de supprimer un cache Redis][DE01]

1. Cliquez sur **OK** quand vous êtes invité à supprimer votre cache Redis.

   ![Invite de suppression d’un cache Redis][DE02]

## <a name="next-steps"></a>étapes suivantes

Pour plus d’informations sur les caches Redis Azure, la configuration des paramètres et la tarification, consultez les liens suivants :

* [Cache Redis Azure]
* [Documentation du Cache Redis]
* [Tarification du Cache Redis]
* [Configuration du Cache Redis Azure]

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
