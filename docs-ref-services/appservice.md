---
title: Bibliothèques Azure App Service pour Java
description: Déployez automatiquement des applications web sur Azure App Service à l’aide de l’API de gestion Azure.
keywords: Azure, Java, SDK, API, applications web, mobile, App Service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/09/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appservice
ms.openlocfilehash: 49063e48ec739b912c418774f531f11b16a3ff1e
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799825"
---
# <a name="azure-app-service-libraries-for-java"></a>Bibliothèques Azure App Service pour Java

## <a name="overview"></a>Vue d’ensemble

Déployez et gérez des sites Web, des applications web et des API REST avec [Azure App Service](/azure/app-service).

Pour découvrir Azure App Service, consultez la section [Créer votre première application web Java dans Azure](/azure/app-service-web/app-service-web-get-started-java).

## <a name="management-api"></a>API de gestion

Déployez, mettez à l’échelle et configurez des applications dans Azure App Service avec l’API de gestion.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.3.0</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/appservice/management)

### <a name="example"></a>Exemples

Déployez une application Web à partir d’une image Docker sur une application Web Azure en cours d’exécution sur Linux.

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a>Exemples

[Déployer une application web à partir d’un protocole FTP ou de GitHub][1]  
[Permuter entre les versions d’application avec les emplacements de déploiement][2]  
[Configurer un domaine personnalisé][3]   
[Mettre à l’échelle une application web dans plusieurs régions][4]   

Explorez d’autres [exemples de code Java pour Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) que vous pouvez utiliser avec vos applications.

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
