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
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="85b90-104">Bibliothèques Azure Key Vault pour Java</span><span class="sxs-lookup"><span data-stu-id="85b90-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="85b90-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="85b90-105">Overview</span></span>

<span data-ttu-id="85b90-106">Protégez et gérez les clés de chiffrement et les secrets utilisés par les services et les applications cloud avec [Azure Key Vault](/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="85b90-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="85b90-107">Pour découvrir Azure Key Vault, consultez [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="85b90-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="85b90-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="85b90-108">Client library</span></span>

<span data-ttu-id="85b90-109">Créez, mettez à jour et supprimez des clés et des secrets dans Azure Key Vault avec les bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="85b90-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="85b90-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="85b90-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.1.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="85b90-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="85b90-111">Example</span></span>

<span data-ttu-id="85b90-112">Récupérez une [clé web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) à partir de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="85b90-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = kvc.getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="85b90-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="85b90-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/client)


## <a name="management-api"></a><span data-ttu-id="85b90-114">API de gestion</span><span class="sxs-lookup"><span data-stu-id="85b90-114">Management API</span></span>

<span data-ttu-id="85b90-115">Utilisez les bibliothèques de gestion Azure Key Vault pour créer des coffres de clé, autoriser des applications et gérer les autorisations.</span><span class="sxs-lookup"><span data-stu-id="85b90-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="85b90-116">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="85b90-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.15.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="85b90-117">Exemples</span><span class="sxs-lookup"><span data-stu-id="85b90-117">Example</span></span>

<span data-ttu-id="85b90-118">Autorisez et exécutez l’application avec le [principal du service](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` pour répertorier et récupérer les secrets d’un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="85b90-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

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
> [<span data-ttu-id="85b90-119">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="85b90-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/management)


## <a name="samples"></a><span data-ttu-id="85b90-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="85b90-120">Samples</span></span>

<span data-ttu-id="85b90-121">Explorez d’autres [exemples de code Java pour Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="85b90-121">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>
