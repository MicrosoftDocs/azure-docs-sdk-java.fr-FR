---
title: Bibliothèques Azure CDN pour Java
description: Documentation de référence pour les bibliothèques de gestion Java CDN
keywords: Azure, Java, SDK, API, contenu, distribution, réseau, CDN
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cdn
ms.openlocfilehash: 199e9b4b2b2431e23954d24e4adeb4326eb4741c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893070"
---
# <a name="azure-cdn-libraries-for-java"></a>Bibliothèques Azure CDN pour Java

## <a name="overview"></a>Vue d’ensemble

Mettez en cache le contenu web statique à des emplacements stratégiques afin de fournir un débit maximal aux utilisateurs disposant d’un [réseau de distribution de contenu (CDN) Azure](/azure/cdn/cdn-overview).

Pour découvrir Azure CDN, consultez la section [Prise en main d’Azure CDN](/azure/cdn/cdn-create-new-endpoint).

## <a name="management-api"></a>API de gestion

Créez des profils CDN, définissez des points de terminaison et ajoutez du contenu au réseau de distribution de contenu à l’aide de l’API de gestion.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-cdn</artifactId>
    <version>1.3.0</version>
</dependency>
```   

### <a name="example"></a>Exemples

Créez un profil CDN, assignez des points de terminaison et chargez du contenu dans votre réseau de distribution de contenu.

```java
CdnProfile profile = azure.cdnProfiles().define("testCDN")
        .withRegion(Region.US_EAST)
        .withNewResourceGroup()
        .withStandardVerizonSku()
        .withNewEndpoint("webAppHostname1")
        .withNewEndpoint("webAppHostname2")
        .create();

List<String> contentList = new ArrayList<String>();
contentList.add("/client.js");
contentList.add("/media/fabrikam_logo.png");

for (CdnEndpoint endpoint : profile.endpoints().values()) {
    endpoint.loadContent(contentList);
}
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/cdn/management)

## <a name="samples"></a>Exemples

[Gérer les réseaux de distribution de contenu avec Java](https://github.com/Azure-Samples/cdn-java-manage-cdn)

Explorez d’autres [exemples de code Java pour Azure CDN](https://azure.microsoft.com/resources/samples/?platform=java&term=cdn) que vous pouvez utiliser avec vos applications.