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
# <a name="partner-center-libraries-for-java"></a>Bibliothèques de l’Espace partenaires pour Java

## <a name="overview"></a>Vue d’ensemble

Les bibliothèques de l’Espace partenaires pour Java sont regroupées dans un Kit de développement logiciel (SDK) qui permet d’interagir avec le service de l’Espace partenaires de Microsoft. Les partenaires peuvent ainsi effectuer les opérations de l’Espace partenaires de manière programmatique. Ce Kit est le dernier-né du portefeuille existant d’API REST, après le Kit de développement logiciel (SDK) .NET.

## <a name="client-library"></a>Bibliothèque cliente

Gérez les ressources dans l’Espace partenaires à l’aide de la bibliothèque de client.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```xml
<dependency>
    <groupId>com.microsoft.store</groupId>
    <artifactId>partnercenter</artifactId>
    <version>1.8.0</version>
</dependency>
```   

### <a name="example"></a>Exemples

Récupère une liste complète des clients associés au revendeur authentifié.

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

## <a name="samples"></a>Exemples

[Scénarios pris en charge](https://docs.microsoft.com/partner-center/develop/scenarios)
[Exemple d’application de console](https://github.com/Microsoft/Partner-Center-Java-Samples)  