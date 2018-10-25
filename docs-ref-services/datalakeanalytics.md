---
title: Bibliothèques Azure Data Lake Analytics pour Java
description: Documentation de référence pour les bibliothèques Java Data Lake Analytics
keywords: Azure, Java, SDK, API, big data, data lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: 0e97d2c53ca6b993a2240b37576e765009f81c51
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799855"
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a>Bibliothèques Azure Data Lake Analytics pour Java

## <a name="overview"></a>Vue d’ensemble

Exécutez des travaux d’analyse Big Data mis à l’échelle de manière à obtenir des jeux de données conséquents avec [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

Pour découvrir Azure Data Lake Analytics, consultez l’article [Prise en main d’Azure Data Lake Analytics à l’aide du Kit de développement logiciel (SDK) Java](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).

## <a name="management-api"></a>API de gestion

Utilisez l’API de gestion pour gérer les comptes, les travaux, les stratégies et les catalogues Data Lake Analytics.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a>Exemples

Envoyez un nouveau travail U-SQL à Data Lake Analytics.

```java
// authenticate with service principal credentials
ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
DataLakeAnalyticsJobManagementClient adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);

// set up job parameters
UUID jobId = java.util.UUID.randomUUID();
USqlJobProperties properties = new USqlJobProperties();
properties.setScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();");
JobInformation parameters = new JobInformation();
parameters.setName("testJob");
parameters.setJobId(jobId);
parameters.setType(JobType.USQL);
parameters.setProperties(properties);

// create the job
JobInformation jobInfo = adlaJobClient.getJobOperations().create(accountName, jobId, parameters).getBody();
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Exemples

[Azure Data Lake Analytics à l’aide du Kit de développement logiciel (SDK) Java][1] 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) d’exemples Azure Data Lake Analytics.
