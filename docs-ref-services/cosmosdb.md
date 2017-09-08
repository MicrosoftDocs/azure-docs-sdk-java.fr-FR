---
title: "Bibliothèques Azure Cosmos DB pour Java"
description: "Consulter la documentation sur les bibliothèques de client Java pour Azure Cosmos DB"
keywords: "Azure, Java, SDK, API, SQL, base de données, MongoDB, Cosmos DB, NoSQL, DocumentDB"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 249907528c24395b0da5d64e4dc06e3422894cfe
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-cosmos-db-libraries-for-java"></a><span data-ttu-id="bd618-104">Bibliothèques Azure Cosmos DB pour Java</span><span class="sxs-lookup"><span data-stu-id="bd618-104">Azure Cosmos DB libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="bd618-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bd618-105">Overview</span></span>

<span data-ttu-id="bd618-106">Stockez et interrogez une clé-valeur, un document JSON, un graphique et des données en colonne au sein d’une base de données globalement distribuée avec [Cosmos DB](/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="bd618-106">Store and query key-value, JSON document, graph, and columnar data in a globally distributed database with [Cosmos DB](/azure/cosmos-db/introduction).</span></span>

<span data-ttu-id="bd618-107">Pour découvrir Cosmos DB, consultez [Azure Cosmos DB : créer une application API avec Java et le portail Azure](/azure/cosmos-db/create-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="bd618-107">To get started with Cosmos DB, see [Azure Cosmos DB: Build an API app with Java and the Azure portal](/azure/cosmos-db/create-documentdb-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="bd618-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="bd618-108">Client library</span></span>

<span data-ttu-id="bd618-109">Connectez-vous à Cosmos DB avec la bibliothèque cliente [DocumentDB](/azure/cosmos-db/documentdb-introduction) pour utiliser les données JSON avec [une syntaxe de requête SQL](/azure/cosmos-db/documentdb-sql-query).</span><span class="sxs-lookup"><span data-stu-id="bd618-109">Connect to Cosmos DB using the [DocumentDB](/azure/cosmos-db/documentdb-introduction) client library to work with JSON data with [SQL query syntax](/azure/cosmos-db/documentdb-sql-query).</span></span>

<span data-ttu-id="bd618-110">[Ajouter une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente Cosmos DB dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="bd618-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the Cosmos DB client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="bd618-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="bd618-111">Example</span></span>

<span data-ttu-id="bd618-112">Sélectionnez les documents JSON correspondants dans Cosmos DB à l’aide de la syntaxe de requête SQL.</span><span class="sxs-lookup"><span data-stu-id="bd618-112">Select matching JSON documents in Cosmos DB using SQL query syntax.</span></span>

```java
DocumentClient client = new DocumentClient(new DocumentClient("https://contoso.documents.azure.com:443",
                "contosoCosmosDBKey", 
                new ConnectionPolicy(),
                ConsistencyLevel.Session);

List<Document> results = client.queryDocuments("dbs/" + DATABASE_ID + "/colls/" + COLLECTION_ID,
        "SELECT * FROM myCollection WHERE myCollection.email = 'allen [at] contoso.com'",
        null)
    .getQueryIterable()
    .toList();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd618-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="bd618-113">Explore the Client APIs</span></span>](/java/api/overview/azure/cosmosdb/clientlibrary)


## <a name="samples"></a><span data-ttu-id="bd618-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="bd618-114">Samples</span></span>

<span data-ttu-id="bd618-115">[Développer une application Java en utilisant l’API MongoDB d’Azure Cosmos DB][2] </span><span class="sxs-lookup"><span data-stu-id="bd618-115">[Develop a Java app using Azure Cosmos DB MongoDB API][2] </span></span>  
<span data-ttu-id="bd618-116">[Développer une application Java en utilisant l’API Graph d’Azure Cosmos DB][3] </span><span class="sxs-lookup"><span data-stu-id="bd618-116">[Develop a Java app using Azure Cosmos DB Graph API][3] </span></span>  
<span data-ttu-id="bd618-117">[Développer une application Java en utilisant l’API DocumentDB d’Azure Cosmos DB][4]</span><span class="sxs-lookup"><span data-stu-id="bd618-117">[Develop a Java app using Azure Cosmos DB DocumentDB API][4]</span></span>        

<span data-ttu-id="bd618-118">Explorez davantage d’[exemples de code Java pour Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="bd618-118">Explore more [sample Java code for Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) you can use in your apps.</span></span>

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started