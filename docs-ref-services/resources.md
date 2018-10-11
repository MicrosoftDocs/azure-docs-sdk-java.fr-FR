---
title: Bibliothèques Azure Resource Manager pour Java
description: Documentation de référence pour les bibliothèques de gestionnaire de ressources Java
keywords: Azure, Java, SDK, API, groupes de ressources,ARM, gestionnaire de ressources
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 326357e5b4667cc06a6058cb29e9685428174dee
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893004"
---
# <a name="azure-resource-manager-libraries-for-java"></a>Bibliothèques Azure Resource Manager pour Java

## <a name="overview"></a>Vue d’ensemble

Déployez, surveillez et gérez des ressources dans des groupes avec [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de gestion

Utilisez l’API de gestion pour créer des groupes de ressources et déployer des ressources à partir de modèles.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-resources</artifactId>
    <version>1.3.0</version>
</dependency>
```

## <a name="example"></a>Exemples

Créer un groupe de ressources dans la région Azure Est des États-Unis.

```java
ResourceGroup resourceGroup = azure.resourceGroups().define("myResourceGroup")
            .withRegion(Region.US_EAST)
            .create();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/resources/management)

## <a name="samples"></a>Exemples

[Gérer des groupes de ressources Azure avec Java][1] 
[Déployer des ressources à l’aide d’un modèle ARM][2]

[1]: https://github.com/Azure-Samples/resources-java-manage-resource-group
[2]: https://github.com/Azure-Samples/resources-java-deploy-using-arm-template

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=java&term=resource) d’exemples Azure Resource Manager.
