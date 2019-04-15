---
title: Bibliothèques Azure Application Insights pour Java
description: Consulter la documentation sur l’API de gestion Java pour Azure Application Insights
keywords: Azure, Java, SDK, API, AppInsights, télémétrie, diagnostics, suivi, journaux d’activité, performances
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
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893410"
---
# <a name="azure-application-insights-libraries-for-java"></a>Bibliothèques Azure Application Insights pour Java

## <a name="overview"></a>Vue d’ensemble

Détectez, hiérarchisez et diagnostiquez des problèmes dans vos applications et services web avec [Application Insights](/azure/application-insights/app-insights-overview).

Pour découvrir Application Insights, consultez [Prise en main d'Application Insights dans un projet web Java](/azure/application-insights/app-insights-java-get-started).

## <a name="client-library"></a>Bibliothèque cliente

Ajoutez la télémétrie pour suivre les événements, les exceptions et les métriques d’utilisateur dans vos applications avec la bibliothèque cliente Application Insights.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>   
    <version>1.0.8</version>
</dependency>
```   

### <a name="example"></a>Exemples

Créez une entrée de métrique et donnez-lui une valeur.

```java
    MetricTelemetry sample = new MetricTelemetry();
    sample.setName("metric name");
    sample.setValue(42.3);
    telemetryClient.TrackMetric(sample);
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/appinsights/client)

## <a name="samples"></a>Exemples

Explorez davantage d’[exemples de code Java pour Application Insights](https://azure.microsoft.com/en-us/resources/samples/?term=insights&platform=java) à utiliser avec vos applications.
