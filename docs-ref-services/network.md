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
ms.openlocfilehash: 6eed6f45ee239db1286e94f210341febb189378d
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-network-libraries-for-java"></a><span data-ttu-id="27ac2-104">Bibliothèques réseau Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="27ac2-104">Azure Network libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="27ac2-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="27ac2-105">Overview</span></span>

<span data-ttu-id="27ac2-106">Connectez des ressources Azure, filtrez et équilibrez le trafic, et gérez le mappage avec [Azure Networking](/azure/networking/networking-overview).</span><span class="sxs-lookup"><span data-stu-id="27ac2-106">Connect Azure resources, filter and balance traffic, and manage routing with [Azure Networking](/azure/networking/networking-overview).</span></span>

<span data-ttu-id="27ac2-107">Pour découvrir Azure Networking, consultez la section [Créer votre premier réseau virtuel](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="27ac2-107">To get started with Azure Networking, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-api"></a><span data-ttu-id="27ac2-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="27ac2-108">Management API</span></span>

<span data-ttu-id="27ac2-109">Créez et gérez des [réseaux virtuels](/azure/virtual-network/virtual-networks-overview) Azure, [ExpressRoutes](/azure/expressroute/), et [Application Gateway](/azure/application-gateway/) avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="27ac2-109">Create and manage Azure [virtual networks](/azure/virtual-network/virtual-networks-overview) , [ExpressRoutes](/azure/expressroute/) , and [Application Gateways](/azure/application-gateway/) with the management API.</span></span>

<span data-ttu-id="27ac2-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="27ac2-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-network</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="27ac2-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="27ac2-111">Example</span></span>

<span data-ttu-id="27ac2-112">Créez un réseau virtuel avec un sous-réseau unique.</span><span class="sxs-lookup"><span data-stu-id="27ac2-112">Create a new virtual network with a single subnet.</span></span>

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
> [<span data-ttu-id="27ac2-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="27ac2-113">Explore the Management APIs</span></span>](/java/api/overview/azure/networking/managementapi)

## <a name="samples"></a><span data-ttu-id="27ac2-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="27ac2-114">Samples</span></span>

<span data-ttu-id="27ac2-115">[Gérer des réseaux virtuels](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span><span class="sxs-lookup"><span data-stu-id="27ac2-115">[Manage virtual networks](https://github.com/Azure-Samples/network-java-manage-virtual-network) </span></span>  
<span data-ttu-id="27ac2-116">[Gérer des interfaces réseau](https://github.com/Azure-Samples/network-java-manage-network-interface) </span><span class="sxs-lookup"><span data-stu-id="27ac2-116">[Manage network interfaces](https://github.com/Azure-Samples/network-java-manage-network-interface) </span></span>  
<span data-ttu-id="27ac2-117">[Gérer des passerelles Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span><span class="sxs-lookup"><span data-stu-id="27ac2-117">[Manage Application Gateways](https://github.com/Azure-Samples/application-gateway-java-manage-simple-application-gateways) </span></span>  
[<span data-ttu-id="27ac2-118">Gérer des équilibreurs de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="27ac2-118">Manage internet facing load balancers</span></span>](https://github.com/Azure-Samples/network-java-manage-internet-facing-load-balancers)   

<span data-ttu-id="27ac2-119">Explorez davantage d’[exemples de code Java pour Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="27ac2-119">Explore more [sample Java code for Azure Networking](https://azure.microsoft.com/resources/samples/?platform=java&term=network) you can use in your apps.</span></span>