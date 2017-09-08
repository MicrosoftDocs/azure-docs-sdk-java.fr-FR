---
title: "Bibliothèques Cache Redis pour Java"
description: "Documentation de référence pour les bibliothèques clientes et de gestion Java pour les bases de données pour Cache Redis"
keywords: "Azure, Java, SDK, API, cache, Redis, cache web, clé-valeur, en mémoire"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: 25c91e02d1ce52afab68286c89c859ab61da56fe
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="redis-cache-libraries-for-java"></a><span data-ttu-id="985ae-104">Bibliothèques Cache Redis pour Java</span><span class="sxs-lookup"><span data-stu-id="985ae-104">Redis Cache libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="985ae-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="985ae-105">Overview</span></span>

<span data-ttu-id="985ae-106">Cache Redis Azure est un magasin clé-valeur sécurisé et distribué basé sur le cache open source populaire [Redis](https://redis.io/).</span><span class="sxs-lookup"><span data-stu-id="985ae-106">Azure Redis Cache is a secure, distributed key-value store based on the popular open source [Redis](https://redis.io/) cache.</span></span> 

<span data-ttu-id="985ae-107">Pour découvrir le Cache Redis Azure, consultez [Utilisation du Cache Redis Azure avec Java](/azure/redis-cache/cache-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="985ae-107">To get started with Azure Redis Cache, see [How to use Azure Redis Cache with Java](/azure/redis-cache/cache-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="985ae-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="985ae-108">Client library</span></span>

<span data-ttu-id="985ae-109">Connectez-vous à Cache Redis Azure et au magasin, et récupérez des valeurs à partir du cache à l’aide du client open source [Jedis](https://github.com/xetorthio/jedis).</span><span class="sxs-lookup"><span data-stu-id="985ae-109">Connect to Azure Redis Cache and store and retrieve values from the cache using the open-source [Jedis](https://github.com/xetorthio/jedis) client.</span></span>  

<span data-ttu-id="985ae-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="985ae-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a><span data-ttu-id="985ae-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="985ae-111">Example</span></span>

<span data-ttu-id="985ae-112">Connectez-vous à Azure Redis et insérez une chaîne dans le cache.</span><span class="sxs-lookup"><span data-stu-id="985ae-112">Connect to Azure Redis and insert a string into the cache.</span></span>

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a><span data-ttu-id="985ae-113">API de gestion</span><span class="sxs-lookup"><span data-stu-id="985ae-113">Management API</span></span>

<span data-ttu-id="985ae-114">Créez, mettez à l’échelle les ressources Azure Redis et gérez les clés d’accès avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="985ae-114">Create and scale Azure Redis resources and manage access keys to with the management API.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.1.2</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="985ae-115">Exemple</span><span class="sxs-lookup"><span data-stu-id="985ae-115">Example</span></span>

<span data-ttu-id="985ae-116">Créez un Cache Redis Azure dans le [niveau standard à deux nœuds](https://azure.microsoft.com/services/cache/).</span><span class="sxs-lookup"><span data-stu-id="985ae-116">Create a new Azure Redis Cache in the [two-node standard tier](https://azure.microsoft.com/services/cache/).</span></span> 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="985ae-117">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="985ae-117">Explore the Management APIs</span></span>](/java/api/overview/azure/rediscache/managementapi)

## <a name="samples"></a><span data-ttu-id="985ae-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="985ae-118">Samples</span></span>

[<span data-ttu-id="985ae-119">Gérer Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="985ae-119">Manage Azure Redis Cache</span></span>](https://github.com/Azure-Samples/redis-java-manage-cache)   

<span data-ttu-id="985ae-120">Explorez d’autres [exemples de code Java pour Cache Redis Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="985ae-120">Explore more [sample Java code for Azure Redis Cache](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) you can use in your apps.</span></span>
