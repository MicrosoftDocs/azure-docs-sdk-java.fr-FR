---
title: "Azure pour développeurs Java | Microsoft Docs"
description: "Kit de développement logiciel (SDK) Java et référence d’API pour Azure"
keywords: "Azure Java, référence d’API Azure Java, bibliothèque de classes Azure Java, SDK Azure"
author: routlaw
manager: douge
ms.assetid: 7b92e776-959b-4632-8b1d-047ce1417616
ms.service: Azure
ms.devlang: java
ms.topic: reference
ms.technology: Azure
ms.date: 3/06/2016
ms.openlocfilehash: 10073a1b2250a37347128dd9c8faf1375b2ab6ae
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="5bf06-104">Bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="5bf06-104">Azure libraries for Java</span></span>

<span data-ttu-id="5bf06-105">Les bibliothèques Azure facilitent l’utilisation des services Azure dans vos applications Java à l’aide d’interfaces natives.</span><span class="sxs-lookup"><span data-stu-id="5bf06-105">Azure libraries help you consume Azure services in your Java apps using native interfaces.</span></span> <span data-ttu-id="5bf06-106">Chaque bibliothèque est indépendante et peut être utilisée séparément.</span><span class="sxs-lookup"><span data-stu-id="5bf06-106">Each library is independent and can be used separately from the others another.</span></span>

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [<span data-ttu-id="5bf06-107">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5bf06-107">Azure Storage</span></span>](#azure-storage) | [<span data-ttu-id="5bf06-108">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5bf06-108">SQL Database</span></span>](#sql-database)  | [<span data-ttu-id="5bf06-109">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="5bf06-109">Redis Cache</span></span>](#redis-cache)   | [<span data-ttu-id="5bf06-110">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="5bf06-110">DocumentDB</span></span>](#documentdb) |
| [<span data-ttu-id="5bf06-111">Service Bus</span><span class="sxs-lookup"><span data-stu-id="5bf06-111">Service Bus</span></span>](#servicebus)  | [<span data-ttu-id="5bf06-112">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bf06-112">Azure Active Directory</span></span>](#azuread) | [<span data-ttu-id="5bf06-113">Key Vault</span><span class="sxs-lookup"><span data-stu-id="5bf06-113">Key Vault</span></span>](#keyvault)  | [<span data-ttu-id="5bf06-114">Concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="5bf06-114">Event Hub</span></span>](#eventhub)
| [<span data-ttu-id="5bf06-115">IoT Service</span><span class="sxs-lookup"><span data-stu-id="5bf06-115">IoT Service</span></span>](#iotservice) | [<span data-ttu-id="5bf06-116">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="5bf06-116">IoT Device</span></span>](#iotdevice) | [<span data-ttu-id="5bf06-117">Data Lake</span><span class="sxs-lookup"><span data-stu-id="5bf06-117">Data Lake</span></span>](#datalake)  | [<span data-ttu-id="5bf06-118">AppInsights</span><span class="sxs-lookup"><span data-stu-id="5bf06-118">AppInsights</span></span>](#appinsights) | 
| [<span data-ttu-id="5bf06-119">Batch</span><span class="sxs-lookup"><span data-stu-id="5bf06-119">Batch</span></span>](#batch) | [<span data-ttu-id="5bf06-120">Manage Azure resources (Gérer des ressources Azure)</span><span class="sxs-lookup"><span data-stu-id="5bf06-120">Manage Azure resources</span></span>](#management) |

## <a name="install-with-maven"></a><span data-ttu-id="5bf06-121">Installer avec Maven</span><span class="sxs-lookup"><span data-stu-id="5bf06-121">Install with Maven</span></span>

<span data-ttu-id="5bf06-122">Ajoutez une entrée de dépendance dans votre fichier `pom.xml` pour importer une bibliothèque dans votre projet [Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="5bf06-122">Add a dependency entry in your `pom.xml` to import a library into your [Maven](https://maven.apache.org) project.</span></span>

<span data-ttu-id="5bf06-123">Par exemple, pour inclure la version la plus récente des [bibliothèque de gestion Azure pour Java](#management) :</span><span class="sxs-lookup"><span data-stu-id="5bf06-123">For example, to include the latest version of the [Azure management libraries for Java](#management):</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

<span data-ttu-id="5bf06-124">D’autres outils de build Java comme Gradle sont pris en charge mais la procédure d’installation n’est pas détaillée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="5bf06-124">Other Java build tools like Gradle are supported but the install steps are not provided in this article.</span></span> <span data-ttu-id="5bf06-125">Passez en revue la documentation de votre outil de build pour savoir comment exploiter les imports Maven.</span><span class="sxs-lookup"><span data-stu-id="5bf06-125">Review the documentation for your build tool on how to consume Maven imports.</span></span>

## <a name="azure-service-libraries"></a><span data-ttu-id="5bf06-126">Bibliothèques de service Azure</span><span class="sxs-lookup"><span data-stu-id="5bf06-126">Azure service libraries</span></span>

<span data-ttu-id="5bf06-127">Intégrez les services Azure pour ajouter des fonctionnalités à vos applications à l’aide de ces bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="5bf06-127">Integrate Azure services to add functionality to your apps using these libraries.</span></span> <span data-ttu-id="5bf06-128">En savoir plus sur la création d’applications avec les services Azure sur le [centre de développement Java](https://azure.microsoft.com/develop/java).</span><span class="sxs-lookup"><span data-stu-id="5bf06-128">Learn more about building apps with Azure services at the [Java developer center](https://azure.microsoft.com/develop/java).</span></span>

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[<span data-ttu-id="5bf06-129">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5bf06-129">Azure Storage</span></span>](/azure/storage/storage-introduction)  

<span data-ttu-id="5bf06-130">Stockage des données et service de messagerie pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="5bf06-130">Data storage and messaging for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[<span data-ttu-id="5bf06-131">Exemples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Référence](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-131">Samples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Reference](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[<span data-ttu-id="5bf06-132">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5bf06-132">SQL Database</span></span>](/azure/sql-database/sql-database-technical-overview)

<span data-ttu-id="5bf06-133">Pilote JDBC pour Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5bf06-133">JDBC driver for Azure SQL Database.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[<span data-ttu-id="5bf06-134">Exemples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Référence](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-134">Samples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Reference](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Release Notes</span></span>](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[<span data-ttu-id="5bf06-135">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="5bf06-135">Redis Cache</span></span>](https://azure.microsoft.com/services/cache/)

<span data-ttu-id="5bf06-136">Stockage clé-valeur performant et à faible latence.</span><span class="sxs-lookup"><span data-stu-id="5bf06-136">Low-latency, high-performance key-value store.</span></span>

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[<span data-ttu-id="5bf06-137">Exemples](/azure/redis-cache/cache-java-get-started) | [Référence](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-137">Samples](/azure/redis-cache/cache-java-get-started) | [Reference](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Release Notes</span></span>](https://github.com/xetorthio/jedis/releases)  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[<span data-ttu-id="5bf06-138">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5bf06-138">Cosmos DB</span></span>](/azure/documentdb/documentdb-introduction)

<span data-ttu-id="5bf06-139">Base de données NoSQL évolutive avec documents JSON et une syntaxe de requête SQL ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5bf06-139">Scalable NoSQL database with JSON documents and a SQL or JavaScript query syntax.</span></span>   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[<span data-ttu-id="5bf06-140">Exemples](/azure/documentdb/documentdb-java-application) | [Référence](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-140">Samples](/azure/documentdb/documentdb-java-application) | [Reference](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Release Notes</span></span>](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="5bf06-141">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="5bf06-141">ServiceBus</span></span>](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 <span data-ttu-id="5bf06-142">Service Bus est une plateforme professionnelle de service de messagerie transactionnel.</span><span class="sxs-lookup"><span data-stu-id="5bf06-142">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [<span data-ttu-id="5bf06-143">Exemples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Référence](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-143">Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[<span data-ttu-id="5bf06-144">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bf06-144">Azure Active Directory</span></span>](/azure/active-directory/active-directory-whatis)   

<span data-ttu-id="5bf06-145">Gestion des identités et connexion sécurisée pour vos applications.</span><span class="sxs-lookup"><span data-stu-id="5bf06-145">Identity management and secure sign-in for your applications.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[<span data-ttu-id="5bf06-146">Exemples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Référence](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-146">Samples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Reference](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Release Notes</span></span>](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[<span data-ttu-id="5bf06-147">Key Vault</span><span class="sxs-lookup"><span data-stu-id="5bf06-147">Key Vault</span></span>](/azure/key-vault) 

<span data-ttu-id="5bf06-148">Accédez en toute sécurité à des clés et des secrets à partir de vos applications.</span><span class="sxs-lookup"><span data-stu-id="5bf06-148">Safely access keys and secrets from your applications.</span></span> 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[<span data-ttu-id="5bf06-149">Exemples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Référence](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-149">Samples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Reference](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Release Notes</span></span>](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[<span data-ttu-id="5bf06-150">Concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="5bf06-150">Event Hub</span></span>](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
<span data-ttu-id="5bf06-151">Événement à débit élevé et gestion de télémétrie pour instrumentation ou scénarios IoT.</span><span class="sxs-lookup"><span data-stu-id="5bf06-151">High-throughput event and telemetry handling for your instrumentation or IoT scenarios.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[<span data-ttu-id="5bf06-152">Exemples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Référence](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-152">Samples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Reference](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[<span data-ttu-id="5bf06-153">IoT Service</span><span class="sxs-lookup"><span data-stu-id="5bf06-153">IoT Service</span></span>](/azure/iot-hub/)

<span data-ttu-id="5bf06-154">Gérez les identités, envoyez des messages et obtenez des commentaires à partir d’appareils inscrits dans votre IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5bf06-154">Manage identities, send messages, and get feedback from devices registered with your IoT hub.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[<span data-ttu-id="5bf06-155">Exemples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Référence](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-155">Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes</span></span>](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[<span data-ttu-id="5bf06-156">Appareil IoT</span><span class="sxs-lookup"><span data-stu-id="5bf06-156">IoT Device</span></span>](/azure/iot-hub/iot-hub-devguide)

<span data-ttu-id="5bf06-157">Envoyez un message à un IoT Hub à partir de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="5bf06-157">Send a message to an IoT hub from your device.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[<span data-ttu-id="5bf06-158">Exemples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Référence](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-158">Samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Reference](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Release Notes</span></span>](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[<span data-ttu-id="5bf06-159">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5bf06-159">Data Lake Store</span></span>](/azure/data-lake-store/data-lake-store-overview)   
   
<span data-ttu-id="5bf06-160">Capturez des données de n’importe quelle taille et de n’importe quelle forme dans un emplacement unique pour exécuter des analyses.</span><span class="sxs-lookup"><span data-stu-id="5bf06-160">Capture data of any size and shape into a single location for performing analytics.</span></span>    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[<span data-ttu-id="5bf06-161">Exemples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Référence](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-161">Samples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Reference](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Release Notes</span></span>](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[<span data-ttu-id="5bf06-162">AppInsights</span><span class="sxs-lookup"><span data-stu-id="5bf06-162">AppInsights</span></span>](/azure/application-insights/app-insights-overview)

<span data-ttu-id="5bf06-163">Suivez l’utilisation, ajoutez une télémétrie et surveillez vos applications web.</span><span class="sxs-lookup"><span data-stu-id="5bf06-163">Track usage, add telemetry, and monitor your web apps.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[<span data-ttu-id="5bf06-164">Exemples](/azure/application-insights/app-insights-java-get-started) | [Référence](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-164">Samples](/azure/application-insights/app-insights-java-get-started) | [Reference](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Release Notes</span></span>](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[<span data-ttu-id="5bf06-165">Batch</span><span class="sxs-lookup"><span data-stu-id="5bf06-165">Batch</span></span>](/azure/batch)

<span data-ttu-id="5bf06-166">Exécutez efficacement des applications de calcul hautes performances en parallèle et à grande échelle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="5bf06-166">Run large-scale parallel and high-performance computing applications efficiently in the cloud.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[<span data-ttu-id="5bf06-167">Exemples](https://github.com/azure/azure-batch-samples) | [Référence](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-167">Samples](https://github.com/azure/azure-batch-samples) | [Reference](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Release Notes</span></span>](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a><span data-ttu-id="5bf06-168">Gérer des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="5bf06-168">Manage Azure resources</span></span>

<span data-ttu-id="5bf06-169">Créez, mettez à jour et supprimez des ressources Azure à partir de votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="5bf06-169">Create, update, and delete Azure resources from your application code.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

[<span data-ttu-id="5bf06-170">Exemples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Référence](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-170">Samples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Reference](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Release Notes</span></span>](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomen-usazureservice-bus-messagingservice-bus-messaging-overview"></a>[<span data-ttu-id="5bf06-171">ServiceBus</span><span class="sxs-lookup"><span data-stu-id="5bf06-171">ServiceBus</span></span>](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview) 
   
<span data-ttu-id="5bf06-172">Service Bus est une plateforme professionnelle de service de messagerie transactionnel.</span><span class="sxs-lookup"><span data-stu-id="5bf06-172">Service Bus is an enterprise-class, transactional messaging platform service.</span></span>

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[<span data-ttu-id="5bf06-173">Exemples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Référence](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notes de publication</span><span class="sxs-lookup"><span data-stu-id="5bf06-173">Samples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Reference](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Release Notes</span></span>](https://github.com/Azure/azure-service-bus-java)

