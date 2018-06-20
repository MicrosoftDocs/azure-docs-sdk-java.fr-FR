---
title: Bibliothèques Cache Redis pour Java
description: Documentation de référence pour les bibliothèques clientes et de gestion Java pour les bases de données pour Cache Redis
keywords: Azure, Java, SDK, API, cache, Redis, cache web, clé-valeur, en mémoire
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: redis-cache
ms.openlocfilehash: dd03825d9ae7cba32087f92262d5ef213cf3af0b
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823622"
---
# <a name="redis-cache-libraries-for-java"></a>Bibliothèques Cache Redis pour Java

## <a name="overview"></a>Vue d'ensemble

Cache Redis Azure est un magasin clé-valeur sécurisé et distribué basé sur le cache open source populaire [Redis](https://redis.io/). 

Pour découvrir le Cache Redis Azure, consultez [Utilisation du Cache Redis Azure avec Java](/azure/redis-cache/cache-java-get-started).

## <a name="client-library"></a>Bibliothèque cliente

Connectez-vous à Cache Redis Azure et au magasin, et récupérez des valeurs à partir du cache à l’aide du client open source [Jedis](https://github.com/xetorthio/jedis).  

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.   

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
</dependency>
```

## <a name="example"></a>Exemples

Connectez-vous à Azure Redis et insérez une chaîne dans le cache.

```java
JedisShardInfo shardInfo = new JedisShardInfo("<name>.redis.cache.windows.net", 6380, useSsl);
    shardInfo.setPassword("<key>"); /* Use your access key. */
    Jedis jedis = new Jedis(shardInfo);
    jedis.set("foo", "bar");
```

## <a name="management-api"></a>API de gestion

Créez, mettez à l’échelle les ressources Azure Redis et gérez les clés d’accès avec l’API de gestion.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-redis</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Exemples

Créez un Cache Redis Azure dans le [niveau standard à deux nœuds](https://azure.microsoft.com/services/cache/). 

```java
RedisCache cache = azure.redisCaches().define(redisCacheName1)
    .withRegion(Region.US_CENTRAL)
    .withNewResourceGroup(rgName)
    .withStandardSku();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/rediscache/management)

## <a name="samples"></a>Exemples

[Gérer Cache Redis Azure](https://github.com/Azure-Samples/redis-java-manage-cache)   

Explorez d’autres [exemples de code Java pour Cache Redis Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=redis) que vous pouvez utiliser avec vos applications.
