---
title: Bibliothèques Azure Resource Manager pour Java
description: Documentation de référence pour les bibliothèques de gestionnaire de ressources Java
keywords: Azure, Java, SDK, API, groupes de ressources,ARM, gestionnaire de ressources
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 326357e5b4667cc06a6058cb29e9685428174dee
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893004"
---
# <a name="azure-resource-manager-libraries-for-java"></a><span data-ttu-id="72165-104">Bibliothèques Azure Resource Manager pour Java</span><span class="sxs-lookup"><span data-stu-id="72165-104">Azure Resource Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="72165-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="72165-105">Overview</span></span>

<span data-ttu-id="72165-106">Déployez, surveillez et gérez des ressources dans des groupes avec [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="72165-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="72165-107">API de gestion</span><span class="sxs-lookup"><span data-stu-id="72165-107">Management API</span></span>

<span data-ttu-id="72165-108">Utilisez l’API de gestion pour créer des groupes de ressources et déployer des ressources à partir de modèles.</span><span class="sxs-lookup"><span data-stu-id="72165-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

<span data-ttu-id="72165-109">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="72165-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="72165-110">Exemples</span><span class="sxs-lookup"><span data-stu-id="72165-110">Example</span></span>

<span data-ttu-id="72165-111">Créer un groupe de ressources dans la région Azure Est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="72165-111">Create a new resource group in the Azure Eastern US region.</span></span>

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="72165-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="72165-112">Explore the Management APIs</span></span>](/java/api/overview/azure/resources/management)

## <a name="samples"></a><span data-ttu-id="72165-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="72165-113">Samples</span></span>

<span data-ttu-id="72165-114">[Gérer des groupes de ressources Azure avec Java][1] 
[Déployer des ressources à l’aide d’un modèle ARM][2]</span><span class="sxs-lookup"><span data-stu-id="72165-114">[Manage Azure Resource Groups with Java][1] 
[Deploy resources using an ARM template][2]</span></span>

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

<span data-ttu-id="72165-115">Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) d’exemples Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="72165-115">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) of Azure Resource Manager samples.</span></span>
