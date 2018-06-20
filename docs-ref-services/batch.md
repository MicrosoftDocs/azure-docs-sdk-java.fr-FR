---
title: Bibliothèques Azure Batch pour Java
description: Documentation de référence pour les bibliothèques Java Batch
keywords: Azure, Java, SDK, API, Batch, traitement, planification, longue durée
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: batch
ms.openlocfilehash: 67381d68d23f98579a472aefbebaa929af622b8d
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823592"
---
# <a name="azure-batch-libraries-for-java"></a><span data-ttu-id="e8224-104">Bibliothèques Azure Batch pour Java</span><span class="sxs-lookup"><span data-stu-id="e8224-104">Azure Batch libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="e8224-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e8224-105">Overview</span></span>

<span data-ttu-id="e8224-106">Exécutez efficacement des applications de calcul haute performance en parallèle et à grande échelle dans le cloud avec [Azure Batch](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="e8224-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>   

<span data-ttu-id="e8224-107">Pour découvrir Azure Batch, consultez [Créer un compte Batch avec le portail Azure](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="e8224-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="client-library"></a><span data-ttu-id="e8224-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="e8224-108">Client library</span></span>

<span data-ttu-id="e8224-109">Les bibliothèques de client Azure Batch vous permettent de configurer des nœuds et des pools de calcul, de définir des tâches et de les configurer pour s’exécuter dans les travaux. Vous pouvez configurer un gestionnaire de travaux pour contrôler et surveiller l’exécution du travail.</span><span class="sxs-lookup"><span data-stu-id="e8224-109">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="e8224-110">[En savoir plus](/azure/batch/batch-api-basics) sur l’utilisation de ces objets pour exécuter des solutions de calcul parallèles à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="e8224-110">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

<span data-ttu-id="e8224-111">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e8224-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="e8224-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="e8224-112">Example</span></span>

<span data-ttu-id="e8224-113">Configurez un pool de nœuds de calcul Linux dans un compte Batch :</span><span class="sxs-lookup"><span data-stu-id="e8224-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8224-114">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="e8224-114">Explore the Client APIs</span></span>](/java/api/overview/azure/batch/client)


## <a name="management-api"></a><span data-ttu-id="e8224-115">API de gestion</span><span class="sxs-lookup"><span data-stu-id="e8224-115">Management API</span></span>

<span data-ttu-id="e8224-116">Utilisez les bibliothèques de gestion Azure Batch pour créer et supprimer des comptes Batch, lire et régénérer les clés de compte Batch, et gérer le stockage de comptes Batch.</span><span class="sxs-lookup"><span data-stu-id="e8224-116">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

<span data-ttu-id="e8224-117">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e8224-117">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="e8224-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="e8224-118">Example</span></span>

<span data-ttu-id="e8224-119">Créez un compte Azure Batch, puis configurez pour ce compte une nouvelle application et un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="e8224-119">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```java
BatchAccount batchAccount = azure.batchAccounts().define("newBatchAcct")
    .withRegion(Region.US_EAST)
    .withNewResourceGroup("myResourceGroup")
    .defineNewApplication("batchAppName")
        .defineNewApplicationPackage(applicationPackageName)
        .withAllowUpdates(true)
        .withDisplayName(applicationDisplayName)
        .attach()
    .withNewStorageAccount("batchStorageAcct")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8224-120">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="e8224-120">Explore the Management APIs</span></span>](/java/api/overview/azure/batch/management)


## <a name="samples"></a><span data-ttu-id="e8224-121">Exemples</span><span class="sxs-lookup"><span data-stu-id="e8224-121">Samples</span></span>

<span data-ttu-id="e8224-122">[Gestion des comptes Batch][1]</span><span class="sxs-lookup"><span data-stu-id="e8224-122">[Manage Batch accounts][1]</span></span>   

<span data-ttu-id="e8224-123">Explorez d’autres [exemples de code Java pour Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="e8224-123">Explore more [sample Java code for Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) you can use in your apps.</span></span>

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts