---
title: Gestion des caches Redis avec l’Explorateur Azure pour IntelliJ
description: Découvrez comment gérer vos caches Redis Azure à l’aide de l’Explorateur Azure pour IntelliJ.
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
ms.openlocfilehash: 046ae0428d50a7f173f5ad15be53ffd8e66c11c5
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892520"
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a>Gestion des caches Redis avec l’Explorateur Azure pour IntelliJ

L’Explorateur Azure, qui fait partie du kit de ressources Azure pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour gérer les caches Redis de leur compte Azure à partir de l’IDE IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Créer un cache Redis à l’aide d’IntelliJ

Les étapes suivantes vous indiquent comment créer un cache Redis avec l’Explorateur Azure.

1. Connectez-vous à votre compte Azure à l’aide de la procédure décrite dans l’article [Azure Sign In Instructions for the Azure Toolkit for IntelliJ] (Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ).

1. Dans la fenêtre de l’outil **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Caches Redis**, puis cliquez sur **Créer un cache Redis**.

   ![Option de menu Créer un cache Redis][CR01]

1. Quand la boîte de dialogue **Nouveau cache Redis** s’affiche, spécifiez les options suivantes :

   ![Boîte de dialogue de création de cache Redis][CR02]

   a. **Nom DNS** : spécifie le sous-domaine DNS pour le nouveau cache Redis, placé avant « .redis.cache.windows.net », par exemple : *wingtiptoys.redis.cache.windows.net*.

   b. **Abonnement** : spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau cache Redis.

   c. **Groupe de ressources** : spécifie le groupe de ressources pour votre cache Redis ; vous devez en choisir un parmi les options ci-dessous : 
      * **Créer** : spécifie que vous souhaitez créer un groupe de ressources. 
      * **Utiliser existant** : spécifie que vous allez choisir à partir d’une liste de groupes de ressources associés à votre compte Azure. 

   d. **Emplacement** : spécifie l’emplacement où votre cache Redis est créé (par exemple *USA Ouest*).

   e. **Niveau tarifaire** : spécifie le niveau tarifaire utilisé par votre cache Redis ; ce paramètre détermine le nombre de connexions client. (Pour plus d’informations, consultez [Tarification du Cache Redis].)

   f. **Port non-SSL** : spécifie si le cache Redis autorise les connexions non-SSL ; par défaut, seules les connexions SSL sont autorisées.

1. Une fois que vous avez spécifié tous les paramètres du cache Redis, cliquez sur **OK**.

Une fois créé, votre cache Redis s’affiche dans l’Explorateur Azure.

   ![Cache Redis dans l’Explorateur Azure][CR03]

> [!NOTE]
>
> Pour plus d’informations sur la configuration des paramètres de votre cache Redis Azure, consultez [Configuration du Cache Redis Azure].
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a>Afficher les propriétés de votre cache Redis dans IntelliJ

1. Dans l’Explorateur Azure, cliquez avec le bouton droit sur votre cache Redis, puis cliquez sur **Afficher les propriétés**.

   ![Menu contextuel de l’Explorateur Azure permettant d’afficher les propriétés d’un cache Redis][SP01]

1. L’Explorateur Azure affiche les propriétés de votre cache Redis.

   ![Propriétés du cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Supprimer votre cache Redis à l’aide d’IntelliJ

1. Dans l’Explorateur Azure, cliquez avec le bouton droit sur votre cache Redis, puis cliquez sur **Supprimer**.

   ![Menu contextuel de l’Explorateur Azure pour supprimer un cache Redis][DE01]

1. Cliquez sur **Oui** quand vous êtes invité à supprimer votre cache Redis.

   ![Invite de suppression d’un cache Redis][DE02]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les caches Redis Azure, la configuration des paramètres et la tarification, consultez les liens suivants :

* [Cache Redis Azure]
* [Documentation du Cache Redis]
* [Tarification du Cache Redis]
* [Configuration du Cache Redis Azure]

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Tarification du Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis Azure]: https://azure.microsoft.com/services/cache/
[Documentation du Cache Redis]: /azure/redis-cache
[Configuration du Cache Redis Azure]: /azure/redis-cache/cache-configure
[Azure Sign In Instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ)

<!-- IMG List -->

[CR01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
