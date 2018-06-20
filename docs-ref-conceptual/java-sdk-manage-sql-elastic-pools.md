---
title: Gérer des pools élastiques de base de données SQL avec Java | Microsoft Docs
description: Exemple de code pour créer et configurer des bases de données SQL Azure à l’aide du Kit de développement logiciel (SDK) pour Java
author: rloutlaw
manager: douge
ms.assetid: 9b461de8-46bc-4650-8e9e-59531f4e2a53
ms.topic: article
ms.service: Azure
ms.devlang: java
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 9ec0cf3083b8659fa850b798ca0ecf18b2757234
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931115"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a>Gérer des bases de données SQL Azure dans les pools élastiques à partir de vos applications Java

[Cet exemple](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) crée un serveur de base de données SQL avec un [pool élastique](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) pour gérer et mettre à l’échelle des ressources pour plusieurs bases de données dans un plan unique.

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[Affichez l’exemple de code complet sur GitHub](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a>Créer un serveur de base de données SQL avec un pool élastique

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    // Use ElasticPoolEditions.STANDARD as the edition
                    // and create two databases
                    .withNewElasticPool(elasticPoolName, ElasticPoolEditions.STANDARD, 
                        database1Name, database2Name)
                    .create();
```

Consultez la [référence de classe ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) pour les valeurs d’édition actuelles. Examinez la [documentation du pool élastique de base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) pour comparer les caractéristiques de ressource d’édition. 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a>Modifier les paramètres de l’unité de transaction de base de données (DTU) dans un pool élastique

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

Examinez la [documentation de DTU et d’eDTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) pour en savoir plus sur l’allocation des ressources aux les bases de données SQL.

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a>Créer une nouvelle base de données et l’ajouter à un pool élastique

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

L’API crée `anotherDatabase` au [niveau S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) dans la première instruction. Le déplacement de `anotherDatabase` vers le pool élastique attribue les ressources de base de données en fonction des paramètres du pool.

## <a name="remove-a-database-from-an-elastic-pool"></a>Supprimer une base de données à partir d’un pool élastique
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

Consultez la [référence de classe DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) pour les valeurs à passer à `withEdition()`.

## <a name="list-current-database-activities-in-an-elastic-pool"></a>Lister les activités de base de données en cours dans un pool élastique
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

Les activités de base de données incluent le déplacement d’une base de données dans ou hors d’un pool élastique et la mise à jour de bases de données dans un pool élastique.


## <a name="list-databases-in-an-elastic-pool"></a>Répertorier les bases de données dans un pool élastique
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

Passez en revue les méthodes dans [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) pour interroger les bases de données plus en détail.

## <a name="delete-an-elastic-pool"></a>Supprimer un pool élastique
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

Le pool élastique doit être vide avant d’être supprimé.

## <a name="sample-code-summary"></a>Exemple de résumé de code.

L’exemple crée un serveur SQL avec deux bases de données gérées dans un pool élastique unique. Les limites de ressources du pool élastique sont mises à jour, puis les bases de données supplémentaires sont ajoutées au pool. Le code lit ensuite la configuration et l’état du pool élastique. 

L’exemple supprime toutes les ressources qu'il a créées avant de quitter.

| Classe utilisée dans l’exemple | Remarques |
|-------|-------|
| [SqlServer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | Serveur de base de données SQL dans Azure créé par la chaîne fluent `azure.sqlServers().define()...create()`. Fournit des méthodes pour créer et travailler avec des pools élastiques et des bases de données. 
| [SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | Objet côté du client représentant une base de données SQL. Créé via `sqlServer().define()...create()`. 
| [DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | Champs statiques constants utilisés pour définir des ressources de base de données lors de la création d’une base de données en dehors d’un pool élastique ou lors du déplacement d’une base de données en dehors d’un pool élastique  
| [SqlElasticPool](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | Créée à partir de la section `withNewElasticPool()` de la chaîne fluent qui a créé SqlServer dans Azure. Fournit des méthodes pour définir des limites de ressources pour les bases de données en cours d’exécution dans le pool élastique et pour le pool élastique lui-même. 
| [ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | Classe de champs constants définissant les ressources disponibles sur un pool élastique. Consultez la [documentation du pool élastique de la base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) pour les détails du niveau. 
| [ElasticPoolDatabaseActivity](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | Récupéré à partir de `SqlElasticPool.listDatabaseActivities()`. Chaque objet de ce type représente une activité effectuée sur une base de données dans le pool élastique.
| [ElasticPoolActivity](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | Récupérées dans une liste à partir de `SqlElasticPool.listActivities()`. Chacun des objets dans la liste représente une activité effectuée sur le pool élastique (les bases de données dans le pool élastique ne sont pas concernées).

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]