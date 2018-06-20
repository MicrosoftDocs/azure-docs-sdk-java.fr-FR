---
title: Bibliothèques Azure Cosmos DB pour Java
description: Consulter la documentation sur les bibliothèques de client Java pour Azure Cosmos DB
keywords: Azure, Java, SDK, API, SQL Database, MongoDB, Cosmos DB, NoSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/10/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: cosmosdb
ms.openlocfilehash: 6fc9f90cb3c8130aa82b20554a94a8b5ab78c083
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31823842"
---
# <a name="azure-cosmos-db-libraries-for-java"></a>Bibliothèques Azure Cosmos DB pour Java

## <a name="overview"></a>Vue d'ensemble

Stockez et interrogez une clé-valeur, un document JSON, un graphique et des données en colonne au sein d’une base de données globalement distribuée avec [Azure Cosmos DB](/azure/cosmos-db/introduction).

Pour découvrir Azure Cosmos DB, consultez [Azure Cosmos DB : créer une application API avec Java et le portail Azure](/azure/cosmos-db/create-sql-api-java).

## <a name="client-library"></a>Bibliothèque cliente

Connectez-vous à Azure Cosmos DB avec la bibliothèque cliente [SQL API](/azure/cosmos-db/sql-api-introduction) pour utiliser les données JSON avec [une syntaxe de requête SQL](/azure/cosmos-db/sql-api-sql-query).

[Ajouter une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente Cosmos DB dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-documentdb</artifactId>
    <version>1.12.0</version>
</dependency>
```

### <a name="example"></a>Exemples

Sélectionnez les documents JSON correspondants dans Cosmos DB à l’aide de la syntaxe de requête SQL.

```java
DocumentClient client = new DocumentClient("https://contoso.documents.azure.com:443",
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
> [Explorer les API clientes](/java/api/overview/azure/cosmosdb/client)


## <a name="samples"></a>Exemples

[Développer une application Java en utilisant l’API MongoDB d’Azure Cosmos DB][2]   
[Développer une application Java en utilisant l’API Graph d’Azure Cosmos DB][3]   
[Développer une application Java en utilisant l’API SQL d’Azure Cosmos DB][4]        

Explorez davantage d’[exemples de code Java pour Azure Cosmos DB](https://azure.microsoft.com/resources/samples/?platform=java&term=cosmos) à utiliser avec vos applications.

[2]: https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started
[3]: https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started
[4]: https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started
