---
title: Bibliothèques de stockage Azure pour Java
description: ''
keywords: Azure, Java, SDK, API, stockage
author: douge
ms.author: douge
manager: douge
ms.date: 02/07/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: ec06e79374176b5a4795d27c5fbbb2260e65cd8c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893590"
---
# <a name="azure-storage-libraries-for-java"></a>Bibliothèques de stockage Azure pour Java

## <a name="overview"></a>Vue d’ensemble

Lisez et écrivez des fichiers, des données d’objets blob, des paires clé-valeur et des messages à partir de vos applications Java avec le [stockage Azure](/azure/storage/storage-introduction).

Pour découvrir le stockage Azure, consultez l’article [Utilisation du stockage d'objets blob à partir de Java](/azure/storage/storage-java-how-to-use-blob-storage).

## <a name="client-library"></a>Bibliothèque cliente

Utilisez [des chaînes de connexion](/azure/storage/storage-create-storage-account#manage-your-storage-account) pour vous connecter à un compte de stockage Azure, puis utilisez les classes et méthodes des bibliothèques clientes pour utiliser le stockage d’objets blob, de tables, de fichiers ou de files d’attente. 

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>7.0.0</version>
</dependency>
```   

### <a name="example"></a>Exemples

Écrivez un fichier image du système de fichiers local dans un nouvel objet blob dans un conteneur de stockage d’objets blob Azure.


```java
String storageConnectionString = "DefaultEndpointsProtocol=https;" + 
"AccountName=fabrikamblobstorage;" + 
"AccountKey=keyvalue;EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.parse(storageConnectionString);
CloudBlobClient serviceClient = account.createCloudBlobClient();
CloudBlobContainer container = serviceClient.getContainerReference(blobContainer);

// write a blob from a local filesystem path to the container as logo.png
CloudBlockBlob blob = container.getBlockBlobReference("logo.png");
blob.uploadFromFile("/Users/raisa/fabrikam.png");
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

[Gérer des comptes de stockage Azure](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)    
[Lire et écrire des objets dans le stockage d’objets blob](https://github.com/Azure-Samples/storage-blob-java-getting-started)   
[Lire et écrire des messages avec des files d’attente](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
[Lire les fichiers de stockage d’objets blob dans une application web](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

Explorez davantage d’[exemples de code Java pour le stockage Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) à utiliser avec vos applications.
