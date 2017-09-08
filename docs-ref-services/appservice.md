---
title: "Bibliothèques Azure App Service pour Java"
description: "Déployez automatiquement des applications web sur Azure App Service à l’aide de l’API de gestion Azure."
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
ms.openlocfilehash: 03ca1c4d73015b4ca7abbadf95609e32dfc82c66
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-app-service-libraries-for-java"></a><span data-ttu-id="60491-104">Bibliothèques Azure App Service pour Java</span><span class="sxs-lookup"><span data-stu-id="60491-104">Azure App Service libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="60491-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="60491-105">Overview</span></span>

<span data-ttu-id="60491-106">Déployez et gérez des sites Web, des applications web et des API REST avec [Azure App Service](/azure/app-service).</span><span class="sxs-lookup"><span data-stu-id="60491-106">Deploy and manage websites, web applications, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="60491-107">Pour découvrir Azure App Service, consultez la section [Créer votre première application web Java dans Azure](/azure/app-service-web/app-service-web-get-started-java).</span><span class="sxs-lookup"><span data-stu-id="60491-107">To get started with Azure App Service, see [Create your first Java web app in Azure](/azure/app-service-web/app-service-web-get-started-java).</span></span>

## <a name="management-api"></a><span data-ttu-id="60491-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="60491-108">Management API</span></span>

<span data-ttu-id="60491-109">Déployez, mettez à l’échelle et configurez des applications dans Azure App Service avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="60491-109">Deploy, scale, and configure applications in Azure App Service with the management API.</span></span>

<span data-ttu-id="60491-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="60491-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-appservice</artifactId>
    <version>1.1.2</version>
</dependency>
```   

> [!div class="nextstepaction"]
> [<span data-ttu-id="60491-111">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="60491-111">Explore the Management APIs</span></span>](/java/api/overview/azure)

### <a name="example"></a><span data-ttu-id="60491-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="60491-112">Example</span></span>

<span data-ttu-id="60491-113">Déployez une application Web à partir d’une image Docker sur une application Web Azure en cours d’exécution sur Linux.</span><span class="sxs-lookup"><span data-stu-id="60491-113">Deploy a webapp from a Docker image into an Azure Web App running on Linux.</span></span>

```java
WebApp app = azure.webApps().define("newLinuxWebApp")
    .withExistingLinuxPlan(myLinuxAppServicePlan)
    .withExistingResourceGroup("myResourceGroup")
    .withPrivateDockerHubImage("username/my-java-app")
    .withCredentials("dockerHubUser","dockerHubPassword")
    .withAppSetting("PORT","8080").
    .create();
```

## <a name="samples"></a><span data-ttu-id="60491-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="60491-114">Samples</span></span>

<span data-ttu-id="60491-115">[Déployer une application web à partir d’un protocole FTP ou de GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="60491-115">[Deploy a web app from FTP or GitHub][1]</span></span>  
<span data-ttu-id="60491-116">[Permuter entre les versions d’application avec les emplacements de déploiement][2]</span><span class="sxs-lookup"><span data-stu-id="60491-116">[Swap between app versions with deployment slots][2]</span></span>  
<span data-ttu-id="60491-117">[Configurer un domaine personnalisé][3] </span><span class="sxs-lookup"><span data-stu-id="60491-117">[Configure a custom domain][3] </span></span>  
<span data-ttu-id="60491-118">[Mettre à l’échelle une application web dans plusieurs régions][4]</span><span class="sxs-lookup"><span data-stu-id="60491-118">[Scale a web app across multiple regions][4]</span></span>   

<span data-ttu-id="60491-119">Explorez d’autres [exemples de code Java pour Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="60491-119">Explore more [sample Java code for Azure App Service](https://azure.microsoft.com/resources/samples/?platform=java&term=appservice) you can use in your apps.</span></span>

[1]: ../docs-ref-conceptual/java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
