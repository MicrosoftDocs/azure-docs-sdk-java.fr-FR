---
title: "Bibliothèques Azure Traffic Manager pour Java"
description: "Documentation de référence pour les bibliothèques de gestion Java Traffic Manager"
keywords: "Azure, Java, SDK, API, équilibrage des charges, distribution de la charge, réseau, Traffic Manager"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: traffic-manager
ms.openlocfilehash: a38db9a0d92d7dedc5ff49b83ad2658aa61729dd
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="ab627-104">Bibliothèques Azure Traffic Manager pour Java</span><span class="sxs-lookup"><span data-stu-id="ab627-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ab627-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ab627-105">Overview</span></span>

<span data-ttu-id="ab627-106">Contrôlez la distribution du trafic utilisateur pour les points de terminaison de service dans différents centres de données avec [ Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="ab627-106">Control the distribution of user traffic for service endpoints in different datacenters with [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>

<span data-ttu-id="ab627-107">Pour découvrir Azure Traffic Manager, consultez [Créer un profil Traffic Manager](/azure/traffic-manager/traffic-manager-create-profile).</span><span class="sxs-lookup"><span data-stu-id="ab627-107">To get started with Azure Traffic Manager, see [Create a Traffic Manager profile](/azure/traffic-manager/traffic-manager-create-profile).</span></span>

## <a name="management-api"></a><span data-ttu-id="ab627-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="ab627-108">Management API</span></span>

<span data-ttu-id="ab627-109">Créez des profils Traffic Manager, définissez des points de terminaison et modifiez la méthode de routage avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="ab627-109">Create Traffic Manager profiles, define endpoints, and change the routing method with the management API.</span></span> 

<span data-ttu-id="ab627-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ab627-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-trafficmanager</artifactId>
    <version>1.2.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="ab627-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="ab627-111">Example</span></span>

<span data-ttu-id="ab627-112">Créez un profil Traffic Manager et assignez un point de terminaison unique.</span><span class="sxs-lookup"><span data-stu-id="ab627-112">Create a Traffic Manager profile and assign a single endpoint.</span></span>

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
> [<span data-ttu-id="ab627-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="ab627-113">Explore the Management APIs</span></span>](/java/api/overview/azure/trafficmanager/managementapi)

## <a name="samples"></a><span data-ttu-id="ab627-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="ab627-114">Samples</span></span>

[<span data-ttu-id="ab627-115">Équilibrer le trafic d’application web dans plusieurs régions</span><span class="sxs-lookup"><span data-stu-id="ab627-115">Balance web app traffic across multiple regions</span></span>](https://github.com/Azure-Samples/traffic-manager-java-manage-profiles)

<span data-ttu-id="ab627-116">Explorez d’autres [exemples de code Java pour Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="ab627-116">Explore more [sample Java code for Azure Traffic Manager](https://azure.microsoft.com/resources/samples/?platform=java&term=traffic) you can use in your apps.</span></span>
