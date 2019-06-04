---
title: Bibliothèques Azure DNS pour Java
description: Documentation de référence pour les bibliothèques de gestion Azure DNS Java
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
ms.openlocfilehash: 90751d2134b218e16415effeb336a62c6c737cb3
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65626068"
---
# <a name="azure-dns-libraries-for-java"></a>Bibliothèques Azure DNS pour Java

## <a name="overview"></a>Vue d'ensemble

Fournissez des résolutions de nom de domaine et gérez vos enregistrements DNS avec les mêmes informations d’identification, les mêmes API, les mêmes outils et la même facturation que vos autres services Azure avec [Azure DNS](/azure/dns/dns-overview).

Pour découvrir Azure DNS, consultez la section [Prise en main d’Azure DNS à l’aide d’Azure CLI 2.0](/azure/dns/dns-getstarted-cli).

## <a name="management-api"></a>API de gestion

Créez des zones DNS et ajoutez des enregistrements à des zones avec l’API de gestion.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-dns</artifactId>
    <version>1.22.0</version>
</dependency>
```   

### <a name="example"></a>Exemples

Créez une zone DNS racine et ajoutez un enregistrement CNAME `www` dans un groupe de ressources existant.

```java
DnsZone rootDnsZone = azure.dnsZones().define("contoso.com")
        .withExistingResourceGroup("myResourceGroup")
        .create();
rootDnsZone = rootDnsZone.update()
        .withCNameRecordSet("www", "172.30.241.20")
        .apply();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/dns/management)

## <a name="samples"></a>Exemples

[Héberger et gérer des domaines avec Azure DNS](https://github.com/Azure-Samples/dns-java-host-and-manage-your-domains)

Explorez d’autres [exemples de code Java pour Azure DNS](https://azure.microsoft.com/resources/samples/?platform=java&term=dns) que vous pouvez utiliser avec vos applications.

<!---Loc Comment: Please, refer to conversation section to check the issue. Thanks.--->
