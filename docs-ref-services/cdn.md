---
title: "Bibliothèques Azure CDN pour Java"
description: "Documentation de référence pour les bibliothèques de gestion Java CDN"
keywords: "Azure, Java, SDK, API, contenu, distribution, réseau, CDN"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: db9fb8a9a8f9f21061f1e16b77e3145d1fb1b119
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-cdn-libraries-for-java"></a><span data-ttu-id="5e852-104">Bibliothèques Azure CDN pour Java</span><span class="sxs-lookup"><span data-stu-id="5e852-104">Azure CDN libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="5e852-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5e852-105">Overview</span></span>

<span data-ttu-id="5e852-106">Mettez en cache le contenu web statique à des emplacements stratégiques afin de fournir un débit maximal aux utilisateurs disposant d’un [réseau de distribution de contenu (CDN) Azure](/azure/cdn/cdn-overview).</span><span class="sxs-lookup"><span data-stu-id="5e852-106">Cache static web content at strategically placed locations to provide maximum throughput for users with [Azure Content Delivery Network](/azure/cdn/cdn-overview) (CDN).</span></span>

<span data-ttu-id="5e852-107">Pour découvrir Azure CDN, consultez la section [Prise en main d’Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="5e852-107">To get started with Azure CDN, see [Getting started with Azure CDN](/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-api"></a><span data-ttu-id="5e852-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="5e852-108">Management API</span></span>

<span data-ttu-id="5e852-109">Créez des profils CDN, définissez des points de terminaison et ajoutez du contenu au réseau de distribution de contenu à l’aide de l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="5e852-109">Create CDN profiles, define endpoints, and add content to the CDN using the management API.</span></span>

<span data-ttu-id="5e852-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="5e852-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.2.1</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="5e852-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="5e852-111">Example</span></span>

<span data-ttu-id="5e852-112">Créez un profil CDN, assignez des points de terminaison et chargez du contenu dans votre réseau de distribution de contenu.</span><span class="sxs-lookup"><span data-stu-id="5e852-112">Create a CDN profile, assign endpoints, and load content into the CDN.</span></span>

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e852-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="5e852-113">Explore the Management APIs</span></span>](/java/api/overview/azure/cdn/managementapi)

## <a name="samples"></a><span data-ttu-id="5e852-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="5e852-114">Samples</span></span>

[<span data-ttu-id="5e852-115">Gérer les réseaux de distribution de contenu avec Java</span><span class="sxs-lookup"><span data-stu-id="5e852-115">Manage CDNs with Java</span></span>](https://github.com/Azure-Samples/cdn-java-manage-cdn)

<span data-ttu-id="5e852-116">Explorez d’autres [exemples de code Java pour Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="5e852-116">Explore more [sample Java code for Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) you can use in your apps.</span></span>