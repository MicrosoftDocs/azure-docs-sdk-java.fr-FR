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
ms.openlocfilehash: 2f1e43f3835ffcdb138bf7e29a1656b7ee381281
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930895"
---
# <a name="azure-management-libraries-for-java-samples-for-web-apps"></a><span data-ttu-id="bedd0-104">Bibliothèques de gestion Azure pour des exemples Java pour applications web</span><span class="sxs-lookup"><span data-stu-id="bedd0-104">Azure management libraries for Java samples for web apps</span></span>

| <span data-ttu-id="bedd0-105">**Créer une application**</span><span class="sxs-lookup"><span data-stu-id="bedd0-105">**Create an app**</span></span> ||
|---|---|
| <span data-ttu-id="bedd0-106">[Créer une application web et la déployer à partir d’un protocole FTP ou de GitHub][1]</span><span class="sxs-lookup"><span data-stu-id="bedd0-106">[Create a web app and deploy from FTP or GitHub][1]</span></span> | <span data-ttu-id="bedd0-107">Déployez des applications web avec un Git local, un protocole FTP et une intégration continue à partir de GitHub.</span><span class="sxs-lookup"><span data-stu-id="bedd0-107">Deploy web apps from local Git, FTP, and continuous integration from GitHub.</span></span> |
| <span data-ttu-id="bedd0-108">[Créer une application web et gérer les emplacements de déploiement][2]</span><span class="sxs-lookup"><span data-stu-id="bedd0-108">[Create a web app and manage deployment slots][2]</span></span> | <span data-ttu-id="bedd0-109">Créez une application web et déployez-la sur des emplacements de site, puis permutez les déploiements entre les emplacements.</span><span class="sxs-lookup"><span data-stu-id="bedd0-109">Create a web app and deploy to staging slots, and then swap deployments between slots.</span></span> |
| <span data-ttu-id="bedd0-110">**Configurer l’application**</span><span class="sxs-lookup"><span data-stu-id="bedd0-110">**Configure app**</span></span> ||
| <span data-ttu-id="bedd0-111">[Créer une application web et configurer un domaine personnalisé][3]</span><span class="sxs-lookup"><span data-stu-id="bedd0-111">[Create a web app and configure a custom domain][3]</span></span> | <span data-ttu-id="bedd0-112">Créez une application web avec un domaine personnalisé et un certificat SSL auto-signé.</span><span class="sxs-lookup"><span data-stu-id="bedd0-112">Create a web app with a custom domain and self-signed SSL certificate.</span></span> |
| <span data-ttu-id="bedd0-113">**Mettre à l’échelle des applications**</span><span class="sxs-lookup"><span data-stu-id="bedd0-113">**Scale apps**</span></span> ||
| <span data-ttu-id="bedd0-114">[Mettre à l’échelle une application web à haute disponibilité dans plusieurs régions][4]</span><span class="sxs-lookup"><span data-stu-id="bedd0-114">[Scale a web app with high availability across multiple regions][4]</span></span> | <span data-ttu-id="bedd0-115">Mettez à l’échelle une application web dans trois régions géographiques différentes et rendez-les disponibles par le biais d’un point de terminaison unique à l’aide d’Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="bedd0-115">Scale a web app in three different geographical regions and make them available through a single endpoint using Azure Traffic Manager.</span></span> | 
| <span data-ttu-id="bedd0-116">**Connecter l’application aux ressources**</span><span class="sxs-lookup"><span data-stu-id="bedd0-116">**Connect app to resources**</span></span> ||
| <span data-ttu-id="bedd0-117">[Connecter une application web à un compte de stockage][5]</span><span class="sxs-lookup"><span data-stu-id="bedd0-117">[Connect a web app to a storage account][5]</span></span> | <span data-ttu-id="bedd0-118">Créez un compte de stockage Azure et ajoutez la chaîne de connexion de comptes de stockage aux paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="bedd0-118">Create an Azure storage account and add the storage account connection string to the app settings.</span></span> |
| <span data-ttu-id="bedd0-119">[Connecter une application web à une base de données SQL][6]</span><span class="sxs-lookup"><span data-stu-id="bedd0-119">[Connect a web app to a SQL database][6]</span></span> | <span data-ttu-id="bedd0-120">Créez une application web et une base de données SQL, puis ajoutez la chaîne de connexion de base de données SQL aux paramètres d’application.</span><span class="sxs-lookup"><span data-stu-id="bedd0-120">Create a web app and SQL database, and then add the SQL database connection string to the app settings.</span></span> |

[1]: java-sdk-configure-webapp-sources.md
[2]: https://azure.microsoft.com/resources/samples/app-service-java-manage-staging-and-production-slots-for-web-apps/
[3]: https://azure.microsoft.com/resources/samples/app-service-java-manage-web-apps-with-custom-domains/
[4]: https://azure.microsoft.com/resources/samples/app-service-java-scale-web-apps-on-linux/
[5]: https://azure.microsoft.com/resources/samples/app-service-java-manage-storage-connections-for-web-apps/
[6]: https://azure.microsoft.com/resources/samples/app-service-java-manage-data-connections-for-web-apps/