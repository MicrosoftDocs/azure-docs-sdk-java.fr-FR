---
title: "Notes de publication des bibliothèques de gestion Azure pour Java | Microsoft Docs"
description: "Découvrez les nouveautés et surveillez les dernières modifications dans les bibliothèques de gestion Azure pour Java"
keywords: "Azure, Java, API, référence, notes, mises à jour, déconseiller"
author: routlaw
manager: douge
ms.assetid: 1f128cf9-f747-4344-84e1-f9964709deb8
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: c0d5c4b3702d3bee4e93de51cec36e72aeaf598f
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2017
---
# <a name="release-notes"></a>Notes de publication 

## <a name="june-30-2017---110"></a>30 juin 2017 - 1.1.0 

La version 1.1 est rétrocompatible avec la version 1.0 dans les interfaces API destinées au public qui ont atteint l’étape de la disponibilité générale (stable) dans la version 1.0.

Les dernières modifications introduites dans les interfaces API marquées avec l’annotation @Beta dans la version .0

Si vous migrez votre code vers la version 1.1.0, vous pouvez utiliser [ces notes](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md) pour préparer votre code à la migration de la version 1.1.0 à 1.0.0.

### <a name="generally-availabile-in-v11"></a>Généralement disponible dans la version 1.1

Certaines des interfaces API qui étaient toujours en version bêta dans la version 1.0 sont désormais GA (stable) dans la version 1.1, notamment :

- méthodes Async
- toutes les méthodes dans le réseau de distribution de contenu qui étaient présentes dans la version bêta
- toutes les méthodes et interfaces dans Application Gateways qui étaient présentes dans la version bêta

 Certaines parties de la bibliothèque sont toujours en préversion. Consultez le tableau ci-dessous pour connaître l’état actuel des bibliothèques :

Service ou fonctionnalité | Disponible en tant que GA | Disponible en préversion  | Bientôt disponible |
---------|---------|---------|---------|
Calcul  | Les machines virtuelles et leurs extensions, les groupes de machines virtuelles identiques, les disques gérés   | Azure container service, Azure container registry |    |
Storage   |  Comptes de stockage       |         |   Chiffrement      |
Base de données SQL  | Bases de données, pare-feu, pools élastiques        |         |   Autres fonctionnalités      |
Mise en réseau    |  Réseaux virtuels, interfaces réseau, adresses IP, tables de routage, groupes de sécurité réseau, DNS, Traffic Manager, Application Gateways  |    Équilibreurs de charge     |   VPN, Network watcher   |
Autres services    |  Gestionnaire des ressources, Key Vault, Redis, CDN, Batch       |  Applications Web, applications de fonction, Service Bus, Graph RBAC, DocumentDB   | Surveiller, Scheduler, gestion des fonctions, rechercher, autres fonctionnalités Graph RBAC        |
Fondamentaux     |   Authentification - cœur, méthodes Async       |      |         |

### <a name="import-with-maven"></a>Importer avec Maven

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.2.1</version>
</dependency>
```

### <a name="get-help-and-give-feedback"></a>Obtenir de l’aide et donner son avis

Consultez la communauté [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-java-sdk) pour obtenir de l’aide concernant les bibliothèques dans votre code. Si vous rencontrez des bogues ou si vous avez des suggestions pour améliorer les bibliothèques, veuillez envoyer un rapport d’erreur via [GitHub](https://github.com/Azure/azure-sdk-for-java/issues).

### <a name="migrate-from-previous-releases"></a>Migrer à partir de versions précédentes

[Migrer à partir de la version 1.0.0-beta5](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.0.0.md) [Migrer à partir de la version 1.1.0](https://github.com/Azure/azure-sdk-for-java/blob/master/notes/prepare-for-1.1.0.md)


