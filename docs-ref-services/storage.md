---
title: "Bibliothèques de stockage Azure pour Java"
description: 
keywords: Azure, Java, SDK, API, stockage
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: 7c8b6958d5e2892f35af8771d9d53eda28c430ef
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="5a46d-103">Bibliothèques de stockage Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="5a46d-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="5a46d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5a46d-104">Overview</span></span>

<span data-ttu-id="5a46d-105">Lisez et écrivez des fichiers, des données d’objets blob, des paires clé-valeur et des messages à partir de vos applications Java avec le [stockage Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="5a46d-105">Read and write files, blob (object) data, key-value pairs, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="5a46d-106">Pour découvrir le stockage Azure, consultez l’article [Utilisation du stockage d'objets blob à partir de Java](/azure/storage/storage-java-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="5a46d-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/storage-java-how-to-use-blob-storage).</span></span>

## <a name="client-library"></a><span data-ttu-id="5a46d-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="5a46d-107">Client library</span></span>

<span data-ttu-id="5a46d-108">Utilisez [des chaînes de connexion](/azure/storage/storage-create-storage-account#manage-your-storage-account) pour vous connecter à un compte de stockage Azure, puis utilisez les classes et méthodes des bibliothèques clientes pour utiliser le stockage d’objets blob, de tables, de fichiers ou de files d’attente.</span><span class="sxs-lookup"><span data-stu-id="5a46d-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span> 

<span data-ttu-id="5a46d-109">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="5a46d-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.3.1</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="5a46d-110">Exemple</span><span class="sxs-lookup"><span data-stu-id="5a46d-110">Example</span></span>

<span data-ttu-id="5a46d-111">Écrivez un fichier image du système de fichiers local dans un nouvel objet blob dans un conteneur de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="5a46d-111">Write a image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


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
> [<span data-ttu-id="5a46d-112">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="5a46d-112">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/clientlibrary)

## <a name="management-api"></a><span data-ttu-id="5a46d-113">API de gestion</span><span class="sxs-lookup"><span data-stu-id="5a46d-113">Management API</span></span>

<span data-ttu-id="5a46d-114">Créez et gérez les comptes de stockage Azure et les clés de connexion avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="5a46d-114">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="5a46d-115">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="5a46d-115">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.1.2</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="5a46d-116">Exemple</span><span class="sxs-lookup"><span data-stu-id="5a46d-116">Example</span></span>

<span data-ttu-id="5a46d-117">Créez un compte de stockage Azure dans votre abonnement et récupérez sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="5a46d-117">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="5a46d-118">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="5a46d-118">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/managementapi)


## <a name="samples"></a><span data-ttu-id="5a46d-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="5a46d-119">Samples</span></span>

<span data-ttu-id="5a46d-120">[Gérer des comptes de stockage Azure](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span><span class="sxs-lookup"><span data-stu-id="5a46d-120">[Manage Azure Storage accounts](../docs-ref-conceptual/java-sdk-manage-storage-accounts.md)  </span></span>  
<span data-ttu-id="5a46d-121">[Lire et écrire des objets dans le stockage d’objets blob](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="5a46d-121">[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blob-java-getting-started) </span></span>  
<span data-ttu-id="5a46d-122">[Lire et écrire des messages avec des files d’attente](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span><span class="sxs-lookup"><span data-stu-id="5a46d-122">[Read and write messages with queues](https://github.com/Azure-Samples/storage-queue-java-getting-started) </span></span>  
[<span data-ttu-id="5a46d-123">Lire les fichiers de stockage d’objets blob dans une application web</span><span class="sxs-lookup"><span data-stu-id="5a46d-123">Read files from blob storage in a web app</span></span>](https://github.com/Azure-Samples/app-service-java-manage-storage-connections-for-web-apps-on-linux)

<span data-ttu-id="5a46d-124">Explorez davantage d’[exemples de code Java pour le stockage Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="5a46d-124">Explore more [sample Java code for Azure Storage](https://azure.microsoft.com/resources/samples/?platform=java&term=storage) you can use in your apps.</span></span>