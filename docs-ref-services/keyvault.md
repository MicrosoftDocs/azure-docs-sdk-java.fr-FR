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
# <a name="azure-key-vault-libraries-for-java"></a><span data-ttu-id="ff8a1-104">Bibliothèques Azure Key Vault pour Java</span><span class="sxs-lookup"><span data-stu-id="ff8a1-104">Azure Key Vault libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ff8a1-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ff8a1-105">Overview</span></span>

<span data-ttu-id="ff8a1-106">Protégez et gérez les clés de chiffrement et les secrets utilisés par les services et les applications cloud avec [Azure Key Vault](/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="ff8a1-106">Safeguard and manage cryptographic keys and secrets used by cloud applications and services with [Azure Key Vault](/azure/key-vault/).</span></span>

<span data-ttu-id="ff8a1-107">Pour découvrir Azure Key Vault, consultez [Prise en main d’Azure Key Vault](/azure/key-vault/key-vault-get-started).</span><span class="sxs-lookup"><span data-stu-id="ff8a1-107">To get started with Azure Key Vault, see [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="ff8a1-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="ff8a1-108">Client library</span></span>

<span data-ttu-id="ff8a1-109">Créez, mettez à jour et supprimez des clés et des secrets dans Azure Key Vault avec les bibliothèques clientes.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-109">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="ff8a1-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="ff8a1-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="ff8a1-111">Example</span></span>

<span data-ttu-id="ff8a1-112">Récupérez une [clé web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) à partir de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```java
KeyVaultClient kvc = new KeyVaultClient(credentials);
KeyBundle returnedKeyBundle = getKey(vaultUrl, keyName);
JsonWebKey jsonKey = returnedKeyBundle.key();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ff8a1-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="ff8a1-113">Explore the Client APIs</span></span>](/java/api/overview/azure/keyvault/clientlibrary)


## <a name="management-api"></a><span data-ttu-id="ff8a1-114">API de gestion</span><span class="sxs-lookup"><span data-stu-id="ff8a1-114">Management API</span></span>

<span data-ttu-id="ff8a1-115">Utilisez les bibliothèques de gestion Azure Key Vault pour créer des coffres de clé, autoriser des applications et gérer les autorisations.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-115">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="ff8a1-116">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-keyvault</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="ff8a1-117">Exemple</span><span class="sxs-lookup"><span data-stu-id="ff8a1-117">Example</span></span>

<span data-ttu-id="ff8a1-118">Autorisez et exécutez l’application avec le [principal du service](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` pour répertorier et récupérer les secrets d’un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-118">Authorize and application running with [service principal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) `clientId` to list and retrieve secrets from a key vault.</span></span> 

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
> [<span data-ttu-id="ff8a1-119">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="ff8a1-119">Explore the Management APIs</span></span>](/java/api/overview/azure/keyvault/managementapi)


## <a name="samples"></a><span data-ttu-id="ff8a1-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="ff8a1-120">Samples</span></span>

<span data-ttu-id="ff8a1-121">[Gérer les coffres de clés][1]</span><span class="sxs-lookup"><span data-stu-id="ff8a1-121">[Manage Key Vaults][1]</span></span>   

[1]: https://github.com/Azure-Samples/key-vault-java-manage-key-vaults

<span data-ttu-id="ff8a1-122">Explorez d’autres [exemples de code Java pour Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="ff8a1-122">Explore more [sample Java code for Azure Key Vault](https://azure.microsoft.com/resources/samples/?platform=java&term=key+vault) you can use in your apps.</span></span>