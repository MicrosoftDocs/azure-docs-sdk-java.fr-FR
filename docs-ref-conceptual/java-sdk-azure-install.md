---
title: Azure pour développeurs Java | Microsoft Docs
description: Kit de développement logiciel (SDK) Java et référence d’API pour Azure
keywords: Azure Java, référence d’API Azure Java, bibliothèque de classes Azure Java, SDK Azure
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 5c8bb4b81080461285551573eefc0d76b47b2d3d
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892530"
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="8ef26-104">Bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="8ef26-104">Azure libraries for Java</span></span>

<span data-ttu-id="8ef26-105">Les bibliothèques Azure facilitent l’utilisation des services Azure dans vos applications Java à l’aide d’interfaces natives.</span><span class="sxs-lookup"><span data-stu-id="8ef26-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="8ef26-106">Chaque bibliothèque est indépendante et peut être utilisée séparément.</span><span class="sxs-lookup"><span data-stu-id="8ef26-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="8ef26-107">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8ef26-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="8ef26-108">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="8ef26-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="8ef26-109">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="8ef26-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="8ef26-110">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ef26-110">Azure Cosmos DB</span></span>](#cosmos-db) |
| [<span data-ttu-id="8ef26-111">Service Bus</span><span class="sxs-lookup"><span data-stu-id="8ef26-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="8ef26-112">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ef26-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="8ef26-113">Key Vault</span><span class="sxs-lookup"><span data-stu-id="8ef26-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="8ef26-114">Concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="8ef26-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="8ef26-115">IoT Service</span><span class="sxs-lookup"><span data-stu-id="8ef26-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="8ef26-116">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="8ef26-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="8ef26-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="8ef26-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="8ef26-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="8ef26-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="8ef26-119">Batch</span><span class="sxs-lookup"><span data-stu-id="8ef26-119">Batch</span></span>](#batch) | [<span data-ttu-id="8ef26-120">Manage Azure resources (Gérer des ressources Azure)</span><span class="sxs-lookup"><span data-stu-id="8ef26-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="8ef26-121">Installer avec Maven</span><span class="sxs-lookup"><span data-stu-id="8ef26-121">Install with Maven</span></span>

<span data-ttu-id="8ef26-122">Ajoutez une entrée de dépendance dans votre fichier `pom.xml` pour importer une bibliothèque dans votre projet [Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="8ef26-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="8ef26-123">Par exemple, pour inclure la version la plus récente des [bibliothèque de gestion Azure pour Java](#management) :</span><span class="sxs-lookup"><span data-stu-id="8ef26-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="8ef26-124">D’autres outils de build Java comme Gradle sont pris en charge mais la procédure d’installation n’est pas détaillée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8ef26-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="8ef26-125">Passez en revue la documentation de votre outil de build pour savoir comment exploiter les imports Maven.</span><span class="sxs-lookup"><span data-stu-id="8ef26-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="8ef26-126">Bibliothèques de service Azure</span><span class="sxs-lookup"><span data-stu-id="8ef26-126">Azure service libraries</span></span>

<span data-ttu-id="8ef26-127">Intégrez les services Azure pour ajouter des fonctionnalités à vos applications à l’aide de ces bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="8ef26-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="8ef26-128">En savoir plus sur la création d’applications avec les services Azure sur le [centre de développement Java](https://azure.microsoft.com/develop/java).</span><span class="sxs-lookup"><span data-stu-id="8ef26-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="8ef26-129">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8ef26-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="8ef26-130">Stockage des données et service de messagerie pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="8ef26-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

<span data-ttu-id="8ef26-131">[Exemples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Référence](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notes de publication](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span><span class="sxs-lookup"><span data-stu-id="8ef26-131">[Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)</span></span>

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="8ef26-132">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="8ef26-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="8ef26-133">Pilote JDBC pour Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8ef26-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="8ef26-134">[Exemples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Référence](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notes de publication](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-134">[Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)</span></span>

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="8ef26-135">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="8ef26-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="8ef26-136">Stockage clé-valeur performant et à faible latence.</span><span class="sxs-lookup"><span data-stu-id="8ef26-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

<span data-ttu-id="8ef26-137">[Exemples](/azure/redis-cache/cache-java-get-started) | [Référence](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notes de publication](https://github.com/xetorthio/jedis/releases)</span><span class="sxs-lookup"><span data-stu-id="8ef26-137">[Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes](https://github.com/xetorthio/jedis/releases)</span></span>  

<a name="cosmos-db"></a>

### <a name="azure-cosmos-dbazurecosmos-dbintroduction"></a>[<span data-ttu-id="8ef26-138">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ef26-138">Azure Cosmos DB</span></span>](/azure/cosmos-db/introduction)

<span data-ttu-id="8ef26-139">Base de données NoSQL évolutive avec documents JSON et une syntaxe de requête SQL ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8ef26-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

<span data-ttu-id="8ef26-140">[Exemples](/azure/cosmos-db/sql-api-java-application) | [Référence](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notes de publication](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-140">[Samples](/azure/cosmos-db/sql-api-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)</span></span>

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="8ef26-141">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="8ef26-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="8ef26-142">Service Bus est une plateforme professionnelle de service de messagerie transactionnel.</span><span class="sxs-lookup"><span data-stu-id="8ef26-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 <span data-ttu-id="8ef26-143">[Exemples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Référence](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notes de publication](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="8ef26-143">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="8ef26-144">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ef26-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="8ef26-145">Gestion des identités et connexion sécurisée pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="8ef26-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
<span data-ttu-id="8ef26-146">[Exemples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Référence](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notes de publication](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span><span class="sxs-lookup"><span data-stu-id="8ef26-146">[Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)</span></span>
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="8ef26-147">Key Vault</span><span class="sxs-lookup"><span data-stu-id="8ef26-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="8ef26-148">Accédez en toute sécurité à des clés et des secrets à partir de vos applications.</span><span class="sxs-lookup"><span data-stu-id="8ef26-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

<span data-ttu-id="8ef26-149">[Exemples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Référence](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notes de publication](https://github.com/Azure/azure-keyvault-java)</span><span class="sxs-lookup"><span data-stu-id="8ef26-149">[Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes](https://github.com/Azure/azure-keyvault-java)</span></span> 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="8ef26-150">Concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="8ef26-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="8ef26-151">Événement à débit élevé et gestion de télémétrie pour instrumentation ou scénarios IoT.</span><span class="sxs-lookup"><span data-stu-id="8ef26-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

<span data-ttu-id="8ef26-152">[Exemples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Référence](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notes de publication](https://github.com/Azure/azure-event-hubs-java)</span><span class="sxs-lookup"><span data-stu-id="8ef26-152">[Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes](https://github.com/Azure/azure-event-hubs-java)</span></span>

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="8ef26-153">IoT Service</span><span class="sxs-lookup"><span data-stu-id="8ef26-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="8ef26-154">Gérez les identités, envoyez des messages et obtenez des commentaires à partir d’appareils inscrits dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="8ef26-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
<span data-ttu-id="8ef26-155">[Exemples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Référence](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notes de publication](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-155">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="8ef26-156">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="8ef26-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="8ef26-157">Envoyez un message à un IoT Hub à partir de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="8ef26-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

<span data-ttu-id="8ef26-158">[Exemples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Référence](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notes de publication](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-158">[Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)</span></span>

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="8ef26-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8ef26-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="8ef26-160">Capturez des données de n’importe quelle taille et de n’importe quelle forme dans un emplacement unique pour exécuter des analyses.</span><span class="sxs-lookup"><span data-stu-id="8ef26-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

<span data-ttu-id="8ef26-161">[Exemples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Référence](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notes de publication](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-161">[Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)</span></span>

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="8ef26-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="8ef26-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="8ef26-163">Suivez l’utilisation, ajoutez une télémétrie et surveillez vos applications web.</span><span class="sxs-lookup"><span data-stu-id="8ef26-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

<span data-ttu-id="8ef26-164">[Exemples](/azure/application-insights/app-insights-java-get-started) | [Référence](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notes de publication](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span><span class="sxs-lookup"><span data-stu-id="8ef26-164">[Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)</span></span>

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="8ef26-165">Batch</span><span class="sxs-lookup"><span data-stu-id="8ef26-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="8ef26-166">Exécutez efficacement des applications de calcul hautes performances en parallèle et à grande échelle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="8ef26-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

<span data-ttu-id="8ef26-167">[Exemples](https://github.com/azure/azure-batch-samples) | [Référence](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notes de publication](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-167">[Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)</span></span>

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="8ef26-168">Gérer des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="8ef26-168">Manage Azure resources</span></span>

<span data-ttu-id="8ef26-169">Créez, mettez à jour et supprimez des ressources Azure à partir de votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="8ef26-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

<span data-ttu-id="8ef26-170">[Exemples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Référence](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notes de publication](java-sdk-azure-release-notes.md)</span><span class="sxs-lookup"><span data-stu-id="8ef26-170">[Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes](java-sdk-azure-release-notes.md)</span></span>

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="8ef26-171">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="8ef26-171">ServiceBus</span></span>](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="8ef26-172">Service Bus est une plateforme professionnelle de service de messagerie transactionnel.</span><span class="sxs-lookup"><span data-stu-id="8ef26-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

<span data-ttu-id="8ef26-173">[Exemples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Référence](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notes de publication](https://github.com/Azure/azure-service-bus-java)</span><span class="sxs-lookup"><span data-stu-id="8ef26-173">[Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes](https://github.com/Azure/azure-service-bus-java)</span></span>

