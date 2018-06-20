---
title: Gérer des comptes de stockage Azure avec Java | Microsoft Docs
description: Exemple de code pour gérer des comptes de stockage Azure avec le kit de développement logiciel (SDK) pour Java
author: rloutlaw
manager: douge
ms.assetid: 49be8b66-3b56-4c10-8f14-9d326d815cb4
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 5945164b2b04e1fa9169590a71f6c5f9f45842d6
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931055"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a><span data-ttu-id="877b8-103">Gérer des comptes de stockage Azure à partir de vos applications Java</span><span class="sxs-lookup"><span data-stu-id="877b8-103">Manage Azure storage accounts from your Java applications</span></span>

<span data-ttu-id="877b8-104">[Cet exemple](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) crée un compte de [stockage Azure](https://docs.microsoft.com/azure/storage/storage-introduction) et fonctionne avec les clés d’accès de compte à l’aide des [bibliothèques de gestion Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="877b8-104">[This sample](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) creates an [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction) account and works with the account access keys using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="877b8-105">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="877b8-105">Run the sample</span></span>

<span data-ttu-id="877b8-106">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="877b8-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="877b8-107">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="877b8-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

<span data-ttu-id="877b8-108">Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span><span class="sxs-lookup"><span data-stu-id="877b8-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="877b8-109">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="877b8-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a><span data-ttu-id="877b8-110">Créez un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="877b8-110">Create a storage account</span></span>

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

<span data-ttu-id="877b8-111">Le nom de stockage fourni doit être unique pour tous les noms dans Azure et contenir uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="877b8-111">The storage name provided must be unique across all names in Azure and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="877b8-112">Le niveau de performance par défaut et le profil de réplication utilisés pour ce compte est [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="877b8-112">The default performance and replication profile used for this account is [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).</span></span>

## <a name="list-keys-in-a-storage-account"></a><span data-ttu-id="877b8-113">Répertorier des clés dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="877b8-113">List keys in a storage account</span></span>
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

<span data-ttu-id="877b8-114">Deux clés sont fournies avec chaque compte de stockage Azure, afin que vous puissiez régénérer une clé tout en ayant toujours accès au stockage via la seconde.</span><span class="sxs-lookup"><span data-stu-id="877b8-114">Two keys are provided in each Azure storage account so that you can regenerate one key while still allowing access to storage using the other key.</span></span>

## <a name="regenerate-a-key-in-a-storage-account"></a><span data-ttu-id="877b8-115">Régénérer une clé dans un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="877b8-115">Regenerate a key in a storage account</span></span>

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

<span data-ttu-id="877b8-116">Vous devez mettre à jour toutes les ressources et applications Azure avec la nouvelle clé après en avoir généré une nouvelle.</span><span class="sxs-lookup"><span data-stu-id="877b8-116">You must update all Azure resources and applications with the new key after generating a new one.</span></span>

## <a name="list-all-storage-accounts-in-a-resource-group"></a><span data-ttu-id="877b8-117">Répertorier tous les comptes de stockage d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="877b8-117">List all storage accounts in a resource group</span></span>
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

<span data-ttu-id="877b8-118">La page [com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) fournit un ensemble de méthodes utiles pour inspecter la configuration d’un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="877b8-118">[com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) provides a set of useful methods to inspect the configuration of a storage account.</span></span>

## <a name="delete-a-storage-account"></a><span data-ttu-id="877b8-119">Suppression d'un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="877b8-119">Delete a storage account</span></span>
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> <span data-ttu-id="877b8-120">La suppression de comptes de stockage avec des images disque en cours d’utilisation connectées à des machines virtuelles ou avec des disques en cours d’utilisation par d’autres artefacts peut ne pas fonctionner avec ces méthodes.</span><span class="sxs-lookup"><span data-stu-id="877b8-120">Storage accounts with in-use disk images connected to virtual machines or disks in use by other artifacts may not remove with these methods.</span></span> <span data-ttu-id="877b8-121">Détachez le stockage de ces ressources avant de supprimer le compte.</span><span class="sxs-lookup"><span data-stu-id="877b8-121">Detach the storage from these resources before removing the account.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="877b8-122">Explication de l’exemple</span><span class="sxs-lookup"><span data-stu-id="877b8-122">Sample explanation</span></span>

<span data-ttu-id="877b8-123">[Exemple de code sur GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) :</span><span class="sxs-lookup"><span data-stu-id="877b8-123">[The sample code on GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts):</span></span>

- <span data-ttu-id="877b8-124">crée un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="877b8-124">creates a storage account</span></span>
- <span data-ttu-id="877b8-125">lit et régénère les clés d’accès</span><span class="sxs-lookup"><span data-stu-id="877b8-125">reads and regenerates access keys</span></span>
- <span data-ttu-id="877b8-126">répertorie tous les comptes de stockage d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="877b8-126">lists all storage accounts in a resource group</span></span>
- <span data-ttu-id="877b8-127">supprime le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="877b8-127">deletes the storage account</span></span> 

| <span data-ttu-id="877b8-128">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="877b8-128">Class used in sample</span></span> | <span data-ttu-id="877b8-129">Remarques</span><span class="sxs-lookup"><span data-stu-id="877b8-129">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="877b8-130">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="877b8-130">StorageAccount</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | <span data-ttu-id="877b8-131">Représentation d’un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="877b8-131">Representation of an Azure storage account.</span></span> <span data-ttu-id="877b8-132">Utilisez les méthodes dans la classe pour obtenir des informations sur le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="877b8-132">Use the methods in the class to get information about the storage account.</span></span>
| [<span data-ttu-id="877b8-133">StorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="877b8-133">StorageAccountKey</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | <span data-ttu-id="877b8-134">La classe `StorageAccount.getKeys()` retourne les clés du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="877b8-134">`StorageAccount.getKeys()` returns the storage account keys.</span></span> <span data-ttu-id="877b8-135">Utilisez les méthodes `regenerateKey` dans `StorageAccount` pour mettre à jour les clés.</span><span class="sxs-lookup"><span data-stu-id="877b8-135">Use the `regenerateKey` methods in `StorageAccount` to update the keys.</span></span>

## <a name="next-steps"></a><span data-ttu-id="877b8-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="877b8-136">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]