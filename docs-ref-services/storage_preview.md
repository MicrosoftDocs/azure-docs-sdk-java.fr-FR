---
title: Bibliothèques de stockage Azure pour Java
description: ''
keywords: Azure, Java, SDK, API, stockage
author: douge
ms.author: douge
manager: douge
ms.date: 10/19/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: storage
ms.openlocfilehash: fba48dfa04f223dce72a0ee54da967565ebd3687
ms.sourcegitcommit: 66f3dd4bdb09712b73c9194e23028567c0c4ee3f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50235236"
---
# <a name="azure-storage-libraries-for-java"></a><span data-ttu-id="05b6d-103">Bibliothèques de stockage Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="05b6d-103">Azure Storage libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="05b6d-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="05b6d-104">Overview</span></span>

<span data-ttu-id="05b6d-105">Lisez et écrivez des fichiers, des données d’objets blob et des messages à partir de vos applications Java avec le [stockage Azure](/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="05b6d-105">Read and write blob (object) data, files, and messages from your Java applications with [Azure Storage](/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="05b6d-106">Pour découvrir le stockage Azure, consultez l’article [Utilisation du stockage d'objets blob à partir de Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span><span class="sxs-lookup"><span data-stu-id="05b6d-106">To get started with Azure Storage, see [How to use Blob storage from Java](/azure/storage/blobs/storage-quickstart-blobs-java-v10).</span></span>

## <a name="client-library"></a><span data-ttu-id="05b6d-107">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="05b6d-107">Client library</span></span>

<span data-ttu-id="05b6d-108">Utilisez une clé partagée, un jeton SAP ou un jeton OAuth à partir d’Azure Active Directory pour autoriser avec des services de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="05b6d-108">Use a Shared Key, SAS token or an OAuth token from the Azure Active Directory to authorize with Azure Storage services.</span></span> <span data-ttu-id="05b6d-109">Utilisez ensuite les classes de bibliothèques du client et des méthodes pour travailler avec des objets blob, des fichiers ou un stockage de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="05b6d-109">Then use the client libraries' classes and methods to work with blob, file, or queue storage.</span></span> 

<span data-ttu-id="05b6d-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="05b6d-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>   

<span data-ttu-id="05b6d-111">**Dépendance pour le service Blob** :</span><span class="sxs-lookup"><span data-stu-id="05b6d-111">**Dependency for Blob service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-blob</artifactId>
    <version>10.1.0</version>
</dependency>
```

<span data-ttu-id="05b6d-112">**Dépendance pour le service de file d’attente** :</span><span class="sxs-lookup"><span data-stu-id="05b6d-112">**Dependency for Queue service**:</span></span>
```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage-queue</artifactId>
    <version>10.0.0-Preview</version>
</dependency>
```


### <a name="example"></a><span data-ttu-id="05b6d-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="05b6d-113">Example</span></span>

<span data-ttu-id="05b6d-114">Écrivez un fichier image du système de fichiers local dans un nouvel objet blob dans un conteneur de stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="05b6d-114">Write an image file from the local file system into a new blob in an existing Azure Storage blob container.</span></span>


```java
// Retrieve the credentials and initialize SharedKeyCredentials
String accountName = System.getenv("AZURE_STORAGE_ACCOUNT");
String accountKey = System.getenv("AZURE_STORAGE_ACCESS_KEY");

// Create a BlockBlobURL to run operations on Block Blobs. Alternatively create a ServiceURL, or ContainerURL for operations on Blob service, and Blob containers
SharedKeyCredentials creds = new SharedKeyCredentials(accountName, accountKey);

// We are using a default pipeline here, you can learn more about it at https://github.com/Azure/azure-storage-java/wiki/Azure-Storage-Java-V10-Overview
final BlockBlobURL blobURL = new BlockBlobURL(
    new URL("https://" + accountName + ".blob.core.windows.net/mycontainer/myimage.jpg"), 
        StorageURL.createPipeline(creds, new PipelineOptions())
);

AsynchronousFileChannel fileChannel = AsynchronousFileChannel.open(Paths.get("myimage.jpg"));
TransferManager.uploadFileToBlockBlob(fileChannel, blobURL,0, null).blockingGet();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="05b6d-115">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="05b6d-115">Explore the Client APIs</span></span>](/java/api/overview/azure/storage/client)

## <a name="management-api"></a><span data-ttu-id="05b6d-116">API de gestion</span><span class="sxs-lookup"><span data-stu-id="05b6d-116">Management API</span></span>

<span data-ttu-id="05b6d-117">Créez et gérez les comptes de stockage Azure et les clés de connexion avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="05b6d-117">Crete and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="05b6d-118">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="05b6d-118">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-storage</artifactId>
    <version>1.3.0</version>
</dependency
```   

### <a name="example"></a><span data-ttu-id="05b6d-119">Exemples</span><span class="sxs-lookup"><span data-stu-id="05b6d-119">Example</span></span>

<span data-ttu-id="05b6d-120">Créez un compte de stockage Azure dans votre abonnement et récupérez sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="05b6d-120">Create a new Azure Storage account in your subscription and retrieve its access keys.</span></span>

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
> [<span data-ttu-id="05b6d-121">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="05b6d-121">Explore the Management APIs</span></span>](/java/api/overview/azure/storage/management)


## <a name="samples"></a><span data-ttu-id="05b6d-122">Exemples</span><span class="sxs-lookup"><span data-stu-id="05b6d-122">Samples</span></span>

<span data-ttu-id="05b6d-123">[Kit de développement logiciel de Stockage Azure pour Java](https://github.com/azure/azure-storage-java)
[Lire et écrire des objets dans le stockage d’objets blob](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span><span class="sxs-lookup"><span data-stu-id="05b6d-123">[Azure Storage SDK for Java](https://github.com/azure/azure-storage-java)
[Read and write objects to blob storage](https://github.com/Azure-Samples/storage-blobs-java-v10-quickstart) </span></span>  
[<span data-ttu-id="05b6d-124">Lire et écrire des messages avec des files d’attente</span><span class="sxs-lookup"><span data-stu-id="05b6d-124">Read and write messages with queues</span></span>](https://github.com/Azure-Samples/storage-queue-java-getting-started)   
