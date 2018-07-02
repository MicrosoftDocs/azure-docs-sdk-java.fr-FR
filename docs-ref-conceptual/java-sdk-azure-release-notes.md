---
title: Notes de publication des bibliothèques de gestion Azure pour Java | Microsoft Docs
description: Découvrez les nouveautés et surveillez les dernières modifications dans les bibliothèques de gestion Azure pour Java
keywords: Azure, Java, API, référence, notes, mises à jour, déconseiller
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 0aaa83ceb42192441decb5972baae56fed337fb2
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090682"
---
# <a name="release-notes"></a>Notes de publication 

## <a name="october-5-2017---130"></a>5 octobre 2017 - version 1.3.0 

La version 1.3.0 a une compatibilité descendante avec les versions précédentes pour des services et une utilisation fonctionnelle qui atteignaient l’étape (stable) de la disponibilité générale dans les versions précédentes.

Les dernières modifications des versions préliminaires pour ces services possèdent l’annotation @Beta.

Si vous migrez votre code vers la version 1.3.0, vous pouvez utiliser [ces notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.3.0.md) pour préparer votre code existant à la migration vers la version 1.3.

### <a name="generally-availabile-in-v13"></a>Généralement disponible dans la version 1.3

Certaines API toujours en version bêta dans les versions précédentes sont désormais GA (stable), notamment :

- méthodes Async
- toutes les méthodes dans le réseau de distribution de contenu qui étaient présentes dans la version bêta
- toutes les méthodes et interfaces dans Application Gateways qui étaient présentes dans la version bêta

  Certaines parties de la bibliothèque sont toujours en préversion. Consultez le tableau ci-dessous pour connaître l’état actuel des bibliothèques :

Service ou fonctionnalité | Disponible en tant que GA | Disponible en préversion 
---------|---------|---------|-
Calcul  | Les machines virtuelles et leurs extensions, les groupes de machines virtuelles identiques, les disques gérés   | Azure container service, Azure container registry 
Stockage   |  Comptes de stockage       |    Chiffrement     
Base de données SQL  | Bases de données, pare-feu, pools élastiques              
Mise en réseau    |  Réseaux virtuels, interfaces réseau, adresses IP, tables de routage, groupes de sécurité réseau, DNS, Traffic Manager, Application Gateways  |    Équilibreurs de charge, homologation de réseaux, passerelle de réseau virtuel, observateurs de réseau 
Plus de services    |  Gestionnaire des ressources, Key Vault, Redis, CDN, Batch       |  Applications Web, applications de fonction, Service Bus, Graphique RBAC, Cosmos DB, Recherche  
Notions de base     |   Authentification - Éléments de base, méthodes Async, identité du service administré      |      |

> Les fonctionnalités en version préliminaire possèdent l’annotation `@Beta` au niveau de la classe, de l’interface ou de la méthode dans les bibliothèques. Ces fonctionnalités sont susceptibles d'être modifiées. Elles peuvent être modifiées de quelque façon que ce soit, ou même supprimées, à l’avenir.

### <a name="import-with-maven"></a>Importer avec Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Obtenir de l’aide et donner son avis

Consultez la communauté [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) pour obtenir de l’aide concernant les bibliothèques dans votre code. Si vous rencontrez des bogues ou si vous avez des suggestions pour améliorer les bibliothèques, veuillez envoyer un rapport d’erreur via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).


