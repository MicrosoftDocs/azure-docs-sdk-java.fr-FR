---
title: "Bibliothèques Azure Key Vault pour Java"
description: "Vue d’ensemble des bibliothèques Azure Key Vault pour Java"
keywords: "Azure, Java, SDK, API, keyvault, sécuriser, clés, secrets, coffre"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: 51ac51f5436397a0c9f1a4572dcf79a40f10b538
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-key-vault-libraries-for-java"></a>Bibliothèques Azure Key Vault pour Java

## <a name="overview"></a>Vue d'ensemble

Protégez et gérez les clés de chiffrement et les secrets utilisés par les services et les applications cloud avec [Azure Key Vault](/azure/key-vault/).

Pour découvrir Azure Key Vault, consultez [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started).

## <a name="client-library"></a>Bibliothèque cliente

Créez, mettez à jour et supprimez des clés et des secrets dans Azure Key Vault avec les bibliothèques clientes.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a>Exemple

Récupérez une [clé web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) à partir de Key Vault.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a>API de gestion

Utilisez les bibliothèques de gestion Azure Key Vault pour créer des coffres de clé, autoriser des applications et gérer les autorisations. 

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Exemple

Autorisez et exécutez l’application avec le [principal du service](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` pour répertorier et récupérer les secrets d’un coffre de clés. 

```java
vault1 = vault1.update()
            .defineAccessPolicy()
                .forServicePrincipal(clientId)
                .allowKeyAllPermissions()
                .allowSecretPermissions(SecretPermissions.GET)
                .allowSecretPermissions(SecretPermissions.LIST)
                .attach()
            .apply();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a>Exemples

[Gérer les coffres de clés][1]   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

Explorez d’autres [exemples de code Java pour Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que vous pouvez utiliser avec vos applications.
