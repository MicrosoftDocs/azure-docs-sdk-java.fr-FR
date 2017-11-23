---
title: "Bibliothèques Azure DNS pour Java"
description: "Documentation de référence pour les bibliothèques de gestion Azure DNS Java"
keywords: Azure, Java, SDK, API, domaines, DNS, nom, service, service de nom de domaine
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: dns
ms.openlocfilehash: adac8e21a401bc91490b92fc5ccf90443eea569f
ms.sourcegitcommit: f6bf497d9b98f0608aefacf1e914d8be52964234
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/22/2017
---
# <a name="azure-traffic-manager-libraries-for-java"></a><span data-ttu-id="214f3-104">Bibliothèques Azure Traffic Manager pour Java</span><span class="sxs-lookup"><span data-stu-id="214f3-104">Azure Traffic Manager libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="214f3-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="214f3-105">Overview</span></span>

<span data-ttu-id="214f3-106">Fournissez des résolutions de nom de domaine et gérez vos enregistrements DNS avec les mêmes informations d’identification, les mêmes API, les mêmes outils et la même facturation que vos autres services Azure avec [Azure DNS](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="214f3-106">Provide domain name resolution and manage your DNS records using the same credentials, APIs, tools, and billing as your other Azure services with [Azure DNS](/azure/dns/dns-overview).</span></span>

<span data-ttu-id="214f3-107">Pour découvrir Azure DNS, consultez la section [Prise en main d’Azure DNS à l’aide d’Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span><span class="sxs-lookup"><span data-stu-id="214f3-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure CLI 2.0](/azure/dns/dns-getstarted-cli).</span></span>

## <a name="management-api"></a><span data-ttu-id="214f3-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="214f3-108">Management API</span></span>

<span data-ttu-id="214f3-109">Créez des zones DNS et ajoutez des enregistrements à des zones avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="214f3-109">Create DNS zones and add records to zones with the management API.</span></span>

<span data-ttu-id="214f3-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="214f3-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="214f3-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="214f3-111">Example</span></span>

<span data-ttu-id="214f3-112">Créez une zone DNS racine et ajoutez un enregistrement CNAME `www` dans un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="214f3-112">Create a root DNS zone and add a `www` CNAME record in an existing resource group.</span></span>

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="214f3-113">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="214f3-113">Explore the Management APIs</span></span>](/java/api/overview/azure/dns/managementapi)

## <a name="samples"></a><span data-ttu-id="214f3-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="214f3-114">Samples</span></span>

[<span data-ttu-id="214f3-115">Héberger et gérer des domaines avec Azure DNS</span><span class="sxs-lookup"><span data-stu-id="214f3-115">Host and manage your domains with Azure DNS</span></span>](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

<span data-ttu-id="214f3-116">Explorez d’autres [exemples de code Java pour Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="214f3-116">Explore more [sample Java code for Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) you can use in your apps.</span></span>

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
