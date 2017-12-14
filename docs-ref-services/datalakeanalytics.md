---
title: "Bibliothèques Azure Data Lake Analytics pour Java"
description: "Documentation de référence pour les bibliothèques Java Data Lake Analytics"
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
ms.openlocfilehash: 70cfe1417d460172df0cb753d2b719a635978ca8
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/14/2017
---
# <a name="azure-data-lake-analytics-libraries-for-java"></a><span data-ttu-id="79047-104">Bibliothèques Azure Data Lake Analytics pour Java</span><span class="sxs-lookup"><span data-stu-id="79047-104">Azure Data Lake Analytics libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="79047-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="79047-105">Overview</span></span>

<span data-ttu-id="79047-106">Exécutez des travaux d’analyse Big Data mis à l’échelle de manière à obtenir des jeux de données conséquents avec [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span><span class="sxs-lookup"><span data-stu-id="79047-106">Run big data analysis jobs that scale to massive data sets with [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

<span data-ttu-id="79047-107">Pour découvrir Azure Data Lake Analytics, consultez l’article [Prise en main d’Azure Data Lake Analytics à l’aide du Kit de développement logiciel (SDK) Java](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="79047-107">To get started with Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics using Java SDK](/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk).</span></span>

## <a name="management-api"></a><span data-ttu-id="79047-108">API de gestion</span><span class="sxs-lookup"><span data-stu-id="79047-108">Management API</span></span>

<span data-ttu-id="79047-109">Utilisez l’API de gestion pour gérer les comptes, les travaux, les stratégies et les catalogues Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="79047-109">Use the management API to manage Data Lake Analytics accounts, jobs, policies, and catalogs.</span></span>

<span data-ttu-id="79047-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="79047-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-analytics</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

## <a name="example"></a><span data-ttu-id="79047-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="79047-111">Example</span></span>

<span data-ttu-id="79047-112">Envoyez un nouveau travail U-SQL à Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="79047-112">Submit a new U-SQL job to Data Lake Analytics.</span></span>

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
> [<span data-ttu-id="79047-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="79047-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakeanalytics/managementapi)

## <a name="samples"></a><span data-ttu-id="79047-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="79047-114">Samples</span></span>

<span data-ttu-id="79047-115">[Azure Data Lake Analytics à l’aide du Kit de développement logiciel (SDK) Java][1]</span><span class="sxs-lookup"><span data-stu-id="79047-115">[Azure Data Lake Analytics using Java SDK][1]</span></span> 

[1]: https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-get-started-java-sdk

<span data-ttu-id="79047-116">Affichez la [liste complète](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) d’exemples Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="79047-116">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=java&term=analytics) of Azure Data Lake Analytics samples.</span></span>