---
title: Exemples d’applications web de bibliothèques de gestion Azure pour Java
description: Obtenez des exemples de code pour créer et mettre à jour des applications web Azure hébergées dans App Service à l’aide des bibliothèques de gestion Azure pour Java.
keywords: Azure, Java, SDK, API, Maven, Gradle, applications web, app service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 43633e5c-9fb1-4807-ba63-e24c126754e2
ms.openlocfilehash: be4031059587ceb88f6824356f677c37a198de80
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592584"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a>Bibliothèques de gestion Azure pour des exemples Java pour applications web

| **Créer une application** ||
|---|---|
| [Créer une application web et la déployer à partir d’un protocole FTP ou de GitHub][1] | Déployez des applications web avec un Git local, un protocole FTP et une intégration continue à partir de GitHub. |
| [Créer une application web et gérer les emplacements de déploiement][2] | Créez une application web et déployez-la sur des emplacements de site, puis permutez les déploiements entre les emplacements. |
| **Configurer l’application** ||
| [Créer une application web et configurer un domaine personnalisé][3] | Créez une application web avec un domaine personnalisé et un certificat SSL auto-signé. |
| **Mettre à l’échelle des applications** ||
| [Mettre à l’échelle une application web à haute disponibilité dans plusieurs régions][4] | Mettez à l’échelle une application web dans trois régions géographiques différentes et rendez-les disponibles par le biais d’un point de terminaison unique à l’aide d’Azure Traffic Manager. | 
| **Connecter l’application aux ressources** ||
| [Connecter une application web à un compte de stockage][5] | Créez un compte de stockage Azure et ajoutez la chaîne de connexion de comptes de stockage aux paramètres d’application. |
| [Connecter une application web à une base de données SQL][6] | Créez une application web et une base de données SQL, puis ajoutez la chaîne de connexion de base de données SQL aux paramètres d’application. |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/