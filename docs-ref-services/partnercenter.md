---
title: Kit SDK Java de l’Espace partenaires
description: Documentation de référence pour le Kit de développement logiciel (SDK) Java de l’Espace partenaires
keywords: API, CSP, Cloud, Cloud Solution Provider, Java, Espace partenaires, Kit de développement logiciel (SDK)
author: iswillia
ms.author: iswillia
manager: lesliep
ms.date: 10/09/2018
ms.topic: reference
ms.prod: partnercenter
ms.technology: partnercenter
ms.devlang: java
ms.openlocfilehash: 2adfbdbd37d6eb91e48ee37091f951b3f7d59eb9
ms.sourcegitcommit: 4da7d2f470331feb7d76a1658f5825f365cdba9a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49121642"
---
# <a name="partner-center-libraries-for-java"></a><span data-ttu-id="95616-104">Bibliothèques de l’Espace partenaires pour Java</span><span class="sxs-lookup"><span data-stu-id="95616-104">Partner Center libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="95616-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="95616-105">Overview</span></span>

<span data-ttu-id="95616-106">Les bibliothèques de l’Espace partenaires pour Java sont regroupées dans un Kit de développement logiciel (SDK) qui permet d’interagir avec le service de l’Espace partenaires de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="95616-106">The Partner Center libraries for Java is a SDK that provides the ability to interact with Microsoft's Partner Center service.</span></span> <span data-ttu-id="95616-107">Les partenaires peuvent ainsi effectuer les opérations de l’Espace partenaires de manière programmatique.</span><span class="sxs-lookup"><span data-stu-id="95616-107">This enables partners to perform the Partner Center operations programmatically.</span></span> <span data-ttu-id="95616-108">Ce Kit est le dernier-né du portefeuille existant d’API REST, après le Kit de développement logiciel (SDK) .NET.</span><span class="sxs-lookup"><span data-stu-id="95616-108">This is the latest addition to existing portfolio of REST APIs and the .NET SDK.</span></span>

## <a name="client-library"></a><span data-ttu-id="95616-109">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="95616-109">Client library</span></span>

<span data-ttu-id="95616-110">Gérez les ressources dans l’Espace partenaires à l’aide de la bibliothèque de client.</span><span class="sxs-lookup"><span data-stu-id="95616-110">Manage resources in Partner Center using the client library.</span></span>

<span data-ttu-id="95616-111">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="95616-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="95616-112">Exemples</span><span class="sxs-lookup"><span data-stu-id="95616-112">Example</span></span>

<span data-ttu-id="95616-113">Récupère une liste complète des clients associés au revendeur authentifié.</span><span class="sxs-lookup"><span data-stu-id="95616-113">Retrieves a complete list of customer associated with the authenticated reseller.</span></span>

```java
IPartnerCredentials appCredentials = PartnerCredentials.getInstance().generateByApplicationCredentials('YOUR_APP_ID', 'YOUR_APP_SECRET', 'YOUR_TENANT_ID');
IAggregatePartner partnerOperations = PartnerService.getInstance().createPartnerOperations(appCredentials);

// Query the customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(100));
this.getContext().getConsoleHelper().stopProgress();

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while ( customersEnumerator.hasValue() )
{
    /*
     * Perform some operation with the current page of customers using 
     * customersEnumerator.getCurrent()  
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="samples"></a><span data-ttu-id="95616-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="95616-114">Samples</span></span>

<span data-ttu-id="95616-115">[Scénarios pris en charge](https://docs.microsoft.com/partner-center/develop/scenarios)
[Exemple d’application de console](https://github.com/Microsoft/Partner-Center-Java-Samples)</span><span class="sxs-lookup"><span data-stu-id="95616-115">[Supported scenarios](https://docs.microsoft.com/partner-center/develop/scenarios)
[Sample console application](https://github.com/Microsoft/Partner-Center-Java-Samples)</span></span>  