---
title: Bibliothèques de stockage Azure pour Java
description: ''
keywords: Azure, Java, SDK, API, stockage
author: douge
ms.author: seguler
manager: dineshm
ms.date: 10/29/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 68a5fdbf8e2fbfe83f9ea09112d64488e0c11d08
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235230"
---
# <a name="azure-storage-libraries-for-java"></a>Bibliothèques de stockage Azure pour Java

## <a name="overview"></a>Vue d’ensemble

Lisez et écrivez des fichiers, des données d’objets blob et des messages à partir de vos applications Java avec le [stockage Azure](/azure/storage/storage-introduction).

Pour découvrir le stockage Azure, consultez l’article [Démarrage rapide : Charger, télécharger et répertorier des objets blob à l’aide du kit de développement logiciel Java V7](/azure/storage/blobs/storage-quickstart-blobs-java).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez une clé partagée, un jeton SAP ou un jeton OAuth à partir d’Azure Active Directory pour autoriser avec des services de stockage Azure. Utilisez ensuite les classes de bibliothèques du client et des méthodes pour travailler avec des objets blob, des fichiers ou un stockage de file d’attente. 

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.   

**Dépendance pour le kit de développement logiciel (SDK) Stockage Azure hérité v7** :
```XML
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/azure-storage -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>8.0.0</version>
</dependency>
```

### <a name="example"></a>Exemples

Écrivez un fichier image du système de fichiers local dans un nouvel objet blob dans un conteneur de stockage d’objets blob Azure.


```java
// Parse the connection string and create a blob client to interact with Blob storage
CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient blobClient = storageAccount.createCloudBlobClient();
CloudBlobContainer container = blobClient.getContainerReference("quickstartcontainer");

// Create the container if it does not exist with public access.
container.createIfNotExists(BlobContainerPublicAccessType.CONTAINER, new BlobRequestOptions(), new OperationContext());         
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/storage/client)

## <a name="management-api"></a>API de gestion

Créez et gérez les comptes de stockage Azure et les clés de connexion avec l’API de gestion.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a>Exemples

Créez un compte de stockage Azure dans votre abonnement et récupérez sa clé d’accès.

```java
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
        .withRegion(Region.US_EAST)
        .withNewResourceGroup(rgName)
        .create();

// get a list of storage account keys related to the account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/storage/management)


## <a name="samples"></a>Exemples

[Kit de développement logiciel de Stockage Azure pour Java](https://github.com/azure/azure-storage-java)
[Lire et écrire des objets dans le stockage d’objets blob](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart)   
[Lire et écrire des messages avec des files d’attente](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
