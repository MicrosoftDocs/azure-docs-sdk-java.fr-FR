---
title: Bibliothèques Azure Key Vault pour Java
description: Vue d’ensemble des bibliothèques Azure Key Vault pour Java
keywords: Azure, Java, SDK, API, keyvault, sécuriser, clés, secrets, coffre
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: keyvault
ms.openlocfilehash: 84ea77a19c326409f453f62359cf46c90398daeb
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799925"
---
# <a name="azure-key-vault-libraries-for-java"></a>Bibliothèques Azure Key Vault pour Java

## <a name="overview"></a>Vue d’ensemble

Protégez et gérez les clés de chiffrement et les secrets utilisés par les services et les applications cloud avec [Azure Key Vault](/azure/key-vault/).

Pour découvrir Azure Key Vault, consultez [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started).

## <a name="client-library"></a>Bibliothèque cliente

Créez, mettez à jour et supprimez des clés et des secrets dans Azure Key Vault avec les bibliothèques clientes.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.0</version>
</dependency>
```   

## <a name="example"></a>Exemples

Récupérez une [clé web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) à partir de Key Vault.

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a>API de gestion

Utilisez les bibliothèques de gestion Azure Key Vault pour créer des coffres de clé, autoriser des applications et gérer les autorisations. 

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a>Exemples

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
> [Explorer les API de gestion](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a>Exemples

Explorez d’autres [exemples de code Java pour Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que vous pouvez utiliser avec vos applications.
