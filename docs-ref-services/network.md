---
title: "Bibliothèques réseau Azure pour Java"
description: "Consulter la documentation sur les bibliothèques de gestion de réseau Java"
keywords: "Azure, Java, SDK, API, mise en réseau, équilibrage de charge, réseau virtuel, sous-réseau"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: networking
ms.openlocfilehash: de03cf7c073c3a0dd636e23a4554987e7cad11f7
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-network-libraries-for-java"></a>Bibliothèques réseau Azure pour Java

## <a name="overview"></a>Vue d'ensemble

Connectez des ressources Azure, filtrez et équilibrez le trafic, et gérez le mappage avec [Azure Networking](/azure/networking/networking-overview).

Pour découvrir Azure Networking, consultez la section [Créer votre premier réseau virtuel](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-api"></a>API de gestion

Créez et gérez des [réseaux virtuels](/azure/virtual-network/virtual-networks-overview) Azure, [ExpressRoutes](/azure/expressroute/), et [Application Gateway](/azure/application-gateway/) avec l’API de gestion.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.2.1</version>
</dependency>
```   

### <a name="example"></a>Exemple

Créez un réseau virtuel avec un sous-réseau unique.

```java
Network virtualNetwork1 = azure.networks().define(vnetName1)
        .withRegion(Region.US_EAST)
        .withExistingResourceGroup("myResourceGroup")
        .withAddressSpace("192.168.0.0/16")
        .defineSubnet("myVirtualNetwork")
            .withAddressPrefix("192.168.2.0/24")
            .attach()
        .create();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/networking/managementapi)

## <a name="samples"></a>Exemples

[Gérer des réseaux virtuels](https://github.com/Azure-Samples/network-java-manage-virtual-network)   
[Gérer des interfaces réseau](https://github.com/Azure-Samples/network-java-manage-network-interface)   
[Gérer des passerelles Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways)   
[Gérer des équilibreurs de charge accessible sur Internet](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

Explorez davantage d’[exemples de code Java pour Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) à utiliser avec vos applications.
