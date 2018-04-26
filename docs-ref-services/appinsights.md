---
title: Bibliothèques Azure Application Insights pour Java
description: Consulter la documentation sur l’API de gestion Java pour Azure Application Insights
keywords: Azure, Java, SDK, API, AppInsights, télémétrie, diagnostics, suivi, journaux, performances
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: appinsights
ms.openlocfilehash: d881ff66ad806e13f7d2cbafff6ce85c23240304
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-application-insights-libraries-for-java"></a><span data-ttu-id="69165-104">Bibliothèques Azure Application Insights pour Java</span><span class="sxs-lookup"><span data-stu-id="69165-104">Azure Application Insights libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="69165-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="69165-105">Overview</span></span>

<span data-ttu-id="69165-106">Détectez, hiérarchisez et diagnostiquez des problèmes dans vos applications et services web avec [Application Insights](/azure/application-insights/app-insights-overview).</span><span class="sxs-lookup"><span data-stu-id="69165-106">Detect, triage, and diagnose issues in your web apps and services with [Application Insights](/azure/application-insights/app-insights-overview).</span></span>

<span data-ttu-id="69165-107">Pour découvrir Application Insights, consultez [Prise en main d'Application Insights dans un projet web Java](/azure/application-insights/app-insights-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="69165-107">To get started with Application Insights, see [Get started with Application Insights in a Java web project](/azure/application-insights/app-insights-java-get-started).</span></span>

## <a name="client-library"></a><span data-ttu-id="69165-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="69165-108">Client library</span></span>

<span data-ttu-id="69165-109">Ajoutez la télémétrie pour suivre les événements, les exceptions et les métriques d’utilisateur dans vos applications avec la bibliothèque cliente Application Insights.</span><span class="sxs-lookup"><span data-stu-id="69165-109">Add telemetry to track events, exceptions, and user metrics in your apps with the Application Insights client library.</span></span>

<span data-ttu-id="69165-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="69165-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="69165-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="69165-111">Example</span></span>

<span data-ttu-id="69165-112">Créez une entrée de métrique et donnez-lui une valeur.</span><span class="sxs-lookup"><span data-stu-id="69165-112">Create a new metric entry and record a value for it.</span></span>

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="69165-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="69165-113">Explore the Client APIs</span></span>](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a><span data-ttu-id="69165-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="69165-114">Samples</span></span>

<span data-ttu-id="69165-115">Explorez davantage d’[exemples de code Java pour Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="69165-115">Explore more [sample Java code for Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) you can use in your apps.</span></span>
