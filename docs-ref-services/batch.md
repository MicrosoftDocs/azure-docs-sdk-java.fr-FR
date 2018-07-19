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
# <a name="azure-batch-libraries-for-java"></a>Bibliothèques Azure Batch pour Java

## <a name="overview"></a>Vue d'ensemble

Exécutez efficacement des applications de calcul haute performance en parallèle et à grande échelle dans le cloud avec [Azure Batch](/azure/batch/batch-technical-overview).   

Pour découvrir Azure Batch, consultez [Créer un compte Batch avec le portail Azure](/azure/batch/batch-account-create-portal).

## <a name="client-library"></a>Bibliothèque cliente

Les bibliothèques de client Azure Batch vous permettent de configurer des nœuds et des pools de calcul, de définir des tâches et de les configurer pour s’exécuter dans les travaux. Vous pouvez configurer un gestionnaire de travaux pour contrôler et surveiller l’exécution du travail. [En savoir plus](/azure/batch/batch-api-basics) sur l’utilisation de ces objets pour exécuter des solutions de calcul parallèles à grande échelle.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```   

### <a name="example"></a>Exemples

Configurez un pool de nœuds de calcul Linux dans un compte Batch :

```java
// create the batch client for an account using its URI and keys
BatchClient client = BatchClient.open(new BatchSharedKeyCredentials("https://fabrikambatch.eastus.batch.azure.com", "fabrikambatch", batchKey));

// configure a pool of VMs to use 
VirtualMachineConfiguration configuration = new VirtualMachineConfiguration();
configuration.withNodeAgentSKUId("batch.node.ubuntu 16.04");
client.poolOperations().createPool(poolId, poolVMSize, configuration, poolVMCount);
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/batch/client)


## <a name="management-api"></a>API de gestion

Utilisez les bibliothèques de gestion Azure Batch pour créer et supprimer des comptes Batch, lire et régénérer les clés de compte Batch, et gérer le stockage de comptes Batch.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-batch</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Exemples

Créez un compte Azure Batch, puis configurez pour ce compte une nouvelle application et un compte de stockage Azure.

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
> [Explorer les API de gestion](/java/api/overview/azure/batch/management)


## <a name="samples"></a>Exemples

[Gestion des comptes Batch][1]   

Explorez d’autres [exemples de code Java pour Azure Batch](https://azure.microsoft.com/resources/samples/?platform=java&term=batch) que vous pouvez utiliser avec vos applications.

[1]: https://github.com/Azure-Samples/batch-java-manage-batch-accounts