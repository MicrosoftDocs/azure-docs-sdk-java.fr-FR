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
ms.openlocfilehash: 620ee28691f70ed6cf29c4f7c169cd43a6e71351
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592574"
---
# <a name="manage-azure-storage-accounts-from-your-java-applications"></a>Gérer des comptes de stockage Azure à partir de vos applications Java

[Cet exemple](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) crée un compte de [stockage Azure](https://docs.microsoft.com/azure/storage/storage-introduction) et fonctionne avec les clés d’accès de compte à l’aide des [bibliothèques de gestion Java](https://github.com/Azure/azure-sdk-for-java). 

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/storage-java-manage-storage-accounts.git
cd storage-java-manage-storage-accounts
mvn clean compile exec:java
```

Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts).

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)] 

## <a name="create-a-storage-account"></a>Créez un compte de stockage.

```java
// create a new storage account
StorageAccount storageAccount = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .create();
```

Le nom de stockage fourni doit être unique pour tous les noms dans Azure et contenir uniquement des lettres minuscules et chiffres. Le niveau de performance par défaut et le profil de réplication utilisés pour ce compte est [Standard_GRS](https://docs.microsoft.com/azure/storage/storage-redundancy#geo-redundant-storage).

## <a name="list-keys-in-a-storage-account"></a>Répertorier des clés dans un compte de stockage
```java
// list the name and value for each access key in the storage account
List<StorageAccountKey> storageAccountKeys = storageAccount.getKeys();
for(StorageAccountKey key : storageAccountKeys)    {
    System.out.println("Key name: " + key.keyName() + " with value "+ key.value());
}
```

Deux clés sont fournies avec chaque compte de stockage Azure, afin que vous puissiez régénérer une clé tout en ayant toujours accès au stockage via la seconde.

## <a name="regenerate-a-key-in-a-storage-account"></a>Régénérer une clé dans un compte de stockage

```java
// regenerate the first key in a storage account and return an updated list of keys 
List<StorageAccountKey> updatedStorageAccountKeys =
    storageAccount.regenerateKey(storageAccountKeys.get(0).keyName());
```

Vous devez mettre à jour toutes les ressources et applications Azure avec la nouvelle clé après en avoir généré une nouvelle.

## <a name="list-all-storage-accounts-in-a-resource-group"></a>Répertorier tous les comptes de stockage d’un groupe de ressources
```java
// get a list of accounts in a resource group , log info about each one
List<StorageAccount> accounts = azure.storageAccounts().listByResourceGroup(rgName);
for (StorageAccount sa : accounts) {
    System.out.println("Storage Account " + sa.name() + " created @ " + sa.creationTime());
}
```

La page [com.microsoft.azure.management.storage.StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account) fournit un ensemble de méthodes utiles pour inspecter la configuration d’un compte de stockage.

## <a name="delete-a-storage-account"></a>Suppression d'un compte de stockage
```java
// delete by ID when you already have a storage account object
azure.storageAccounts().deleteById(storageAccount.id());

// delete by resource group and account name if you don't have an account object
azure.storageAccounts().deleteByResourceGroup(rgName,accountName);
```

> [!NOTE]
> La suppression de comptes de stockage avec des images disque en cours d’utilisation connectées à des machines virtuelles ou avec des disques en cours d’utilisation par d’autres artefacts peut ne pas fonctionner avec ces méthodes. Détachez le stockage de ces ressources avant de supprimer le compte.

## <a name="sample-explanation"></a>Explication de l’exemple

[Exemple de code sur GitHub](https://github.com/Azure-Samples/storage-java-manage-storage-accounts) :

- crée un compte de stockage
- lit et régénère les clés d’accès
- répertorie tous les comptes de stockage d’un groupe de ressources
- supprime le compte de stockage 

| Classe utilisée dans l’exemple | Notes
|-------|-------|
| [StorageAccount](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account)  | Représentation d’un compte de stockage Azure. Utilisez les méthodes dans la classe pour obtenir des informations sur le compte de stockage.
| [StorageAccountKey](https://docs.microsoft.com/java/api/com.microsoft.azure.management.storage._storage_account_key) | La classe `StorageAccount.getKeys()` retourne les clés du compte de stockage. Utilisez les méthodes `regenerateKey` dans `StorageAccount` pour mettre à jour les clés.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]