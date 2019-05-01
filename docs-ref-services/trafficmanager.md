---
title: Bibliothèques Azure Traffic Manager pour Java
description: Documentation de référence pour les bibliothèques de gestion Java Traffic Manager
keywords: Azure, Java, SDK, API, équilibrage des charges, distribution de la charge, réseau, Traffic Manager
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: c9dc6bedfd8f7a79494a8a547983b2771e51a494
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593244"
---
# <a name="azure-traffic-manager-libraries-for-java"></a>Bibliothèques Azure Traffic Manager pour Java

## <a name="overview"></a>Vue d’ensemble

Contrôlez la distribution du trafic utilisateur pour les points de terminaison de service dans différents centres de données avec [ Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).

Pour découvrir Azure Traffic Manager, consultez [Créer un profil Traffic Manager](/azure/traffic-manager/traffic-manager-create-profile).

## <a name="management-api"></a>API de gestion

Créez des profils Traffic Manager, définissez des points de terminaison et modifiez la méthode de routage avec l’API de gestion. 

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.3.0</version>
</dependency>
```   

## <a name="example"></a>Exemples

Créez un profil Traffic Manager et assignez un point de terminaison unique.

```java
TrafficManagerProfile tmProfile = azure.trafficManagerProfiles().define("testTMProfile")
        .withNewResourceGroup(Region.US_EAST)
        .withLeafDomainLabel("testTMProfile")
        .withPriorityBasedRouting()
        .defineAzureTargetEndpoint("endpoint")
        .toResourceId(webAppId)
        .withRoutingPriority(1)
        .attach()
        .create();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/trafficmanager/management)

## <a name="samples"></a>Exemples

[Équilibrer le trafic d’application web dans plusieurs régions](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

Explorez d’autres [exemples de code Java pour Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que vous pouvez utiliser avec vos applications.
