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
ms.openlocfilehash: 570f820e1349e1dfd01a6c7f323b5312c14c40c6
ms.sourcegitcommit: 4b63ecd2c92a9115dfae018618e4e4046b061b3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/14/2017
---
# <a name="azure-libraries-for-java"></a>Bibliothèques Azure pour Java

Les bibliothèques Azure facilitent l’utilisation des services Azure dans vos applications Java à l’aide d’interfaces natives. Chaque bibliothèque est indépendante et peut être utilisée séparément.

| | | | |
|:-------------:|:----------:|:----:|:---:|
| [Azure Storage](#azure-storage) | [Base de données SQL](#sql-database)  | [Cache Redis](#redis-cache)   | [Base de données de documents](#documentdb) |
| [Service Bus](#servicebus)  | [Azure Active Directory](#azuread) | [Key Vault](#keyvault)  | [Concentrateur d’événements](#eventhub)
| [IoT Service](#iotservice) | [Appareil IoT](#iotdevice) | [Data Lake](#datalake)  | [AppInsights](#appinsights) | 
| [Batch](#batch) | [Manage Azure resources (Gérer des ressources Azure)](#management) |

## <a name="install-with-maven"></a>Installer avec Maven

Ajoutez une entrée de dépendance dans votre fichier `pom.xml` pour importer une bibliothèque dans votre projet [Maven](https://maven.apache.org).

Par exemple, pour inclure la version la plus récente des [bibliothèque de gestion Azure pour Java](#management) :

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

D’autres outils de build Java comme Gradle sont pris en charge mais la procédure d’installation n’est pas détaillée dans cet article. Passez en revue la documentation de votre outil de build pour savoir comment exploiter les imports Maven.

## <a name="azure-service-libraries"></a>Bibliothèques de service Azure

Intégrez les services Azure pour ajouter des fonctionnalités à vos applications à l’aide de ces bibliothèques. En savoir plus sur la création d’applications avec les services Azure sur le [centre de développement Java](https://azure.microsoft.com/develop/java).

<a name="azure-storage"></a>

### <a name="azure-storageazurestoragestorage-introduction"></a>[Azure Storage](/azure/storage/storage-introduction)  

Stockage des données et service de messagerie pour vos applications.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.4.0</version>
</dependency>
```   

[Exemples](https://github.com/Azure/azure-storage-java/tree/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage) | [Référence](/java/api/overview/azure/storage) | [GitHub](https://github.com/Azure/azure-storage-java)  | [Notes de publication](https://github.com/Azure/azure-storage-java/blob/master/ChangeLog.txt)

<a name="sql-database"></a>

### <a name="sql-databaseazuresql-databasesql-database-technical-overview"></a>[Base de données SQL](/azure/sql-database/sql-database-technical-overview)

Pilote JDBC pour Azure SQL Database.

```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

[Exemples](/sql/connect/jdbc/step-3-proof-of-concept-connecting-to-sql-using-java) | [Référence](/java/api/overview/azure/sql) | [GitHub](https://github.com/Microsoft/mssql-jdbc)  | [Notes de publication](https://github.com/Microsoft/mssql-jdbc/blob/master/CHANGELOG.md)

<a name="redis-cache"></a>

### <a name="redis-cachehttpsazuremicrosoftcomservicescache"></a>[Cache Redis](https://azure.microsoft.com/services/cache/)

Stockage clé-valeur performant et à faible latence.

```XML
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
    <version>2.9.0</version>
    <type>jar</type>
    <scope>compile</scope>
</dependency>
```   

[Exemples](/azure/redis-cache/cache-java-get-started) | [Référence](http://xetorthio.github.io/jedis)  | [GitHub](https://github.com/xetorthio/jedis)  | [Notes de publication](https://github.com/xetorthio/jedis/releases)  

<a name="documentdb"></a>

### <a name="cosmos-dbazuredocumentdbdocumentdb-introduction"></a>[Cosmos DB](/azure/documentdb/documentdb-introduction)

Base de données NoSQL évolutive avec documents JSON et une syntaxe de requête SQL ou JavaScript.   

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

[Exemples](/azure/documentdb/documentdb-java-application) | [Référence](http://azure.github.io/azure-documentdb-java/) | [GitHub](https://github.com/Azure/azure-documentdb-java)   | [Notes de publication](https://github.com/Azure/azure-documentdb-java/blob/master/changelog.md)

<a name="servicebus"></a>
 
 ### <a name="servicebusazureservice-bus-messagingservice-bus-messaging-overview"></a>[ServiceBus](/azure/service-bus-messaging/service-bus-messaging-overview) 
    
 Service Bus est une plateforme professionnelle de service de messagerie transactionnel.
 
 ```XML
 <dependency> 
     <groupId>com.microsoft.azure</groupId> 
     <artifactId>azure-servicebus</artifactId> 
     <version>1.0.0</version> 
 </dependency>   
 ```
 
 [Exemples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Référence](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notes de publication](https://github.com/Azure/azure-service-bus-java)   
  
<a name="azuread"></a>

### <a name="azure-active-directoryazureactive-directoryactive-directory-whatis"></a>[Azure Active Directory](/azure/active-directory/active-directory-whatis)   

Gestion des identités et connexion sécurisée pour vos applications.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```
   
[Exemples](https://github.com/Azure-Samples?utf8=%E2%9C%93&q=active%20directory%20&type=&language=java) | [Référence](/java/api/overview/azure/activedirectory) | [GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-java) | [Notes de publication](https://github.com/AzureAD/azure-activedirectory-library-for-javaT-)
 
<a name="keyvault"></a>

### <a name="key-vaultazurekey-vault"></a>[Key Vault](/azure/key-vault) 

Accédez en toute sécurité à des clés et des secrets à partir de vos applications. 

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-keyvault</artifactId>
    <version>1.0.0</version>
</dependency>
```

[Exemples](https://github.com/Azure-Samples/key-vault-java-manage-key-vaults) | [Référence](/java/api/overview/azure/keyvault) | [GitHub](https://github.com/Azure/azure-keyvault-java) | [Notes de publication](https://github.com/Azure/azure-keyvault-java) 

<a name="eventhub"></a>

### <a name="event-hubazureevent-hubsevent-hubs-what-is-event-hubs"></a>[Concentrateur d’événements](/azure/event-hubs/event-hubs-what-is-event-hubs) 
   
Événement à débit élevé et gestion de télémétrie pour instrumentation ou scénarios IoT.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-eventhubs</artifactId> 
    <version>0.14.4</version> 
</dependency>   
```

[Exemples](https://github.com/Azure/azure-event-hubs/tree/master/samples#java) | [Référence](/java/api/overview/azure/eventhub) | [GitHub](https://github.com/azure/azure-event-hubs-java)  | [Notes de publication](https://github.com/Azure/azure-event-hubs-java)

<a name="iotservice"></a> 

### <a name="iot-serviceazureiot-hub"></a>[IoT Service](/azure/iot-hub/)

Gérez les identités, envoyez des messages et obtenez des commentaires à partir d’appareils inscrits dans votre IoT Hub.

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.7.23</version>
</dependency>
```   
   
[Exemples](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples) | [Référence](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notes de publication](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="iotdevice"></a> 

### <a name="iot-deviceazureiot-hubiot-hub-devguide"></a>[Appareil IoT](/azure/iot-hub/iot-hub-devguide)

Envoyez un message à un IoT Hub à partir de votre appareil.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.32</version>
</dependency>
```  

[Exemples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples) | [Référence](/java/api/overview/azure/iot) | [GitHub](https://github.com/Azure/azure-iot-sdk-java) | [Notes de publication](https://github.com/Azure/azure-iot-sdk-java/blob/master/readme.md)

<a name="datalake"></a> 

### <a name="data-lake-storeazuredata-lake-storedata-lake-store-overview"></a>[Data Lake Store](/azure/data-lake-store/data-lake-store-overview)   
   
Capturez des données de n’importe quelle taille et de n’importe quelle forme dans un emplacement unique pour exécuter des analyses.    

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

[Exemples](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started) | [Référence](/java/api/overview/azure/datalakestore) | [GitHub](https://github.com/Azure/azure-data-lake-store-java) | [Notes de publication](https://github.com/Azure/azure-data-lake-store-java/blob/master/CHANGES.md)

<a name="appinsights"></a> 

### <a name="appinsightsazureapplication-insightsapp-insights-overview"></a>[AppInsights](/azure/application-insights/app-insights-overview)

Suivez l’utilisation, ajoutez une télémétrie et surveillez vos applications web.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-web</artifactId>
    <version>1.0.8</version>
</dependency>
```

[Exemples](/azure/application-insights/app-insights-java-get-started) | [Référence](/java/api/overview/azure/appinsights) | [GitHub](https://github.com/Microsoft/ApplicationInsights-Java) | [Notes de publication](https://github.com/Microsoft/ApplicationInsights-Java#to-upgrade-to-the-latest-sdk)

<a name="batch"></a>

### <a name="batchazurebatch"></a>[Batch](/azure/batch)

Exécutez efficacement des applications de calcul hautes performances en parallèle et à grande échelle dans le cloud.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-batch</artifactId>
    <version>2.0.0</version>
</dependency>
```

[Exemples](https://github.com/azure/azure-batch-samples) | [Référence](/java/api/overview/azure/batch) | [GitHub](https://github.com/azure/azure-batch-sdk-for-java) | [Notes de publication](https://github.com/Azure/azure-batch-sdk-for-java/blob/master/README.md)

<a name="management"></a> 

## <a name="manage-azure-resources"></a>Gérer des ressources Azure

Créez, mettez à jour et supprimez des ressources Azure à partir de votre code d’application.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
```

[Exemples](https://github.com/Azure/azure-sdk-for-java#sample-code) | [Référence](https://docs.microsoft.com/java/api/overview/azure/) | [GitHub](https://github.com/Azure/azure-sdk-for-java) | [Notes de publication](java-sdk-azure-release-notes.md)

<a name="servicebus"></a>

### <a name="servicebushttpsdocsmicrosoftcomazureservice-bus-messagingservice-bus-messaging-overview"></a>[ServiceBus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) 
   
Service Bus est une plateforme professionnelle de service de messagerie transactionnel.

```XML
<dependency> 
    <groupId>com.microsoft.azure</groupId> 
    <artifactId>azure-servicebus</artifactId> 
    <version>1.0.0</version> 
</dependency>   
```

[Exemples](https://github.com/Azure/azure-service-bus/tree/master/samples/Java) | [Référence](https://docs.microsoft.com/java/api/overview/azure/servicebus) | [GitHub](https://github.com/azure/azure-service-bus-java)  | [Notes de publication](https://github.com/Azure/azure-service-bus-java)

