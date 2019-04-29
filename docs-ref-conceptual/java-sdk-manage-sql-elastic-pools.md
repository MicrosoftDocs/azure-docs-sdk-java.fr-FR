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
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893570"
---
# <a name="manage-azure-sql-databases-in-elastic-pools-from-your-java-applications"></a><span data-ttu-id="0516d-103">Gérer des bases de données SQL Azure dans les pools élastiques à partir de vos applications Java</span><span class="sxs-lookup"><span data-stu-id="0516d-103">Manage Azure SQL databases in elastic pools from your Java applications</span></span>

<span data-ttu-id="0516d-104">[Cet exemple](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) crée un serveur de base de données SQL avec un [pool élastique](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) pour gérer et mettre à l’échelle des ressources pour plusieurs bases de données dans un plan unique.</span><span class="sxs-lookup"><span data-stu-id="0516d-104">[This sample](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool) creates a SQL database server with an [elastic pool](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to manage and scale resources for mulitple databases in a single plan.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="0516d-105">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="0516d-105">Run the sample</span></span>

<span data-ttu-id="0516d-106">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0516d-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="0516d-107">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0516d-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool
cd sql-database-java-manage-sql-dbs-in-elastic-pool
mvn clean compile exec:java
```

[<span data-ttu-id="0516d-108">Affichez l’exemple de code complet sur GitHub</span><span class="sxs-lookup"><span data-stu-id="0516d-108">View the complete code sample on GitHub</span></span>](https://github.com/Azure-Samples/sql-database-java-manage-sql-dbs-in-elastic-pool)

## <a name="authenticate-with-azure"></a><span data-ttu-id="0516d-109">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="0516d-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-sql-database-server-with-an-elastic-pool"></a><span data-ttu-id="0516d-110">Créer un serveur SQL Database avec un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-110">Create a SQL database server with an elastic pool</span></span>

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

<span data-ttu-id="0516d-111">Consultez la [référence de classe ElasticPoolEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) pour les valeurs d’édition actuelles.</span><span class="sxs-lookup"><span data-stu-id="0516d-111">See the [ElasticPoolEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) for current edition values.</span></span> <span data-ttu-id="0516d-112">Examinez la [documentation du pool élastique de base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) pour comparer les caractéristiques de ressource d’édition.</span><span class="sxs-lookup"><span data-stu-id="0516d-112">Review the [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) to compare edition resource characteristics.</span></span> 

## <a name="change-database-transaction-unit-dtu-settings-in-an-elastic-pool"></a><span data-ttu-id="0516d-113">Modifier les paramètres de l’unité de transaction de base de données (DTU) dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-113">Change Database Transaction Unit (DTU) settings in an elastic pool</span></span>

```java
// Set an pool of 200 eDTUs to share between the databases
// and ensure that a database always has 10 DTUs available but never uses more than 50
elasticPool = elasticPool.update()
                    .withDtu(200)
                    .withDatabaseDtuMin(10)
                    .withDatabaseDtuMax(50)
                    .apply();
```

<span data-ttu-id="0516d-114">Examinez la [documentation de DTU et d’eDTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) pour en savoir plus sur l’allocation des ressources aux les bases de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0516d-114">Review the [DTUs and eDTUs documentation](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu) to learn more about allocating resources to SQL databases.</span></span>

## <a name="create-a-new-database-and-add-it-to-an-elastic-pool"></a><span data-ttu-id="0516d-115">Créer une nouvelle base de données et l’ajouter à un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-115">Create a new database and add it to an elastic pool</span></span>

```java
// Add a newly created database to the elastic pool
SqlDatabase anotherDatabase = sqlServer.databases().define(anotherDatabaseName).create();
elasticPool.update().withExistingDatabase(anotherDatabase).apply();            
```

<span data-ttu-id="0516d-116">L’API crée `anotherDatabase` au [niveau S0](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) dans la première instruction.</span><span class="sxs-lookup"><span data-stu-id="0516d-116">The API creates `anotherDatabase` at [S0 tier](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers) in the first statement.</span></span> <span data-ttu-id="0516d-117">Le déplacement de `anotherDatabase` vers le pool élastique attribue les ressources de base de données en fonction des paramètres du pool.</span><span class="sxs-lookup"><span data-stu-id="0516d-117">Moving `anotherDatabase` to the elastic pool assigns the database resources based on the pool settings.</span></span>

## <a name="remove-a-database-from-an-elastic-pool"></a><span data-ttu-id="0516d-118">Supprimer une base de données à partir d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-118">Remove a database from an elastic pool</span></span>
```java
// Assign an edition since the database resources are no longer managed in the pool 
anotherDatabase = anotherDatabase.update()
                     .withoutElasticPool()
                     .withEdition(DatabaseEditions.STANDARD)
                     .apply();
```

<span data-ttu-id="0516d-119">Consultez la [référence de classe DatabaseEditions](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) pour les valeurs à passer à `withEdition()`.</span><span class="sxs-lookup"><span data-stu-id="0516d-119">See the [DatabaseEditions class reference](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) for values to pass to `withEdition()`.</span></span>

## <a name="list-current-database-activities-in-an-elastic-pool"></a><span data-ttu-id="0516d-120">Lister les activités de base de données en cours dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-120">List current database activities in an elastic pool</span></span>
```java
// get a list of in-flight elastic operations on databases in the pool and log them 
for (ElasticPoolDatabaseActivity databaseActivity : elasticPool.listDatabaseActivities()) {
    System.out.println("Database " + databaseActivity.databaseName() 
        + " performing operation " + databaseActivity.operation() + 
        " with objective " + databaseActivity.requestedServiceObjective());
}
```

<span data-ttu-id="0516d-121">Les activités de base de données incluent le déplacement d’une base de données dans ou hors d’un pool élastique et la mise à jour de bases de données dans un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="0516d-121">Database activities include moving a database in or out of an elastic pool and updating databases in an elastic pool.</span></span>


## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="0516d-122">Répertorier les bases de données dans un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-122">List databases in an elastic pool</span></span>
```java
// Log a list of databases in the elastic pool 
for (SqlDatabase databaseInServer : elasticPool.listDatabases()) {
    System.out.println(databaseInServer.name());
}
```

<span data-ttu-id="0516d-123">Passez en revue les méthodes dans [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) pour interroger les bases de données plus en détail.</span><span class="sxs-lookup"><span data-stu-id="0516d-123">Review the methods in [com.microsoft.azure.management.sql.SqlDatabase](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) to query the databases in more detail.</span></span>

## <a name="delete-an-elastic-pool"></a><span data-ttu-id="0516d-124">Supprimer un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-124">Delete an elastic pool</span></span>
```java
sqlServer.elasticPools().delete(elasticPoolName);
```

<span data-ttu-id="0516d-125">Le pool élastique doit être vide avant d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="0516d-125">The elastic pool must be empty before deleting it.</span></span>

## <a name="sample-code-summary"></a><span data-ttu-id="0516d-126">Exemple de résumé de code.</span><span class="sxs-lookup"><span data-stu-id="0516d-126">Sample code summary.</span></span>

<span data-ttu-id="0516d-127">L’exemple crée un serveur SQL avec deux bases de données gérées dans un pool élastique unique.</span><span class="sxs-lookup"><span data-stu-id="0516d-127">The sample creates a SQL server with two databases managed in a single elasic pool.</span></span> <span data-ttu-id="0516d-128">Les limites de ressources du pool élastique sont mises à jour, puis les bases de données supplémentaires sont ajoutées au pool.</span><span class="sxs-lookup"><span data-stu-id="0516d-128">The elastic pool resource limits are updated, then additional databases are added to the pool.</span></span> <span data-ttu-id="0516d-129">Le code lit ensuite la configuration et l’état du pool élastique.</span><span class="sxs-lookup"><span data-stu-id="0516d-129">The code then reads the elastic pool's configuration and state.</span></span> 

<span data-ttu-id="0516d-130">L’exemple supprime toutes les ressources qu'il a créées avant de quitter.</span><span class="sxs-lookup"><span data-stu-id="0516d-130">The sample deletes all resources it created before exiting.</span></span>

| <span data-ttu-id="0516d-131">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="0516d-131">Class used in sample</span></span> | <span data-ttu-id="0516d-132">Notes</span><span class="sxs-lookup"><span data-stu-id="0516d-132">Notes</span></span> |
|-------|-------|
| [<span data-ttu-id="0516d-133">SqlServer</span><span class="sxs-lookup"><span data-stu-id="0516d-133">SqlServer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_server) | <span data-ttu-id="0516d-134">Serveur de base de données SQL dans Azure créé par la chaîne fluent `azure.sqlServers().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="0516d-134">SQL DB server in Azure created by `azure.sqlServers().define()...create()` fluent chain.</span></span> <span data-ttu-id="0516d-135">Fournit des méthodes pour créer et travailler avec des pools élastiques et des bases de données.</span><span class="sxs-lookup"><span data-stu-id="0516d-135">Provides methods to create and work with elastic pools and databases.</span></span> 
| [<span data-ttu-id="0516d-136">SqlDatabase</span><span class="sxs-lookup"><span data-stu-id="0516d-136">SqlDatabase</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_database) | <span data-ttu-id="0516d-137">Objet côté du client représentant une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0516d-137">Client side object representing a SQL database.</span></span> <span data-ttu-id="0516d-138">Créé via `sqlServer().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="0516d-138">Created through `sqlServer().define()...create()`.</span></span> 
| [<span data-ttu-id="0516d-139">DatabaseEditions</span><span class="sxs-lookup"><span data-stu-id="0516d-139">DatabaseEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._database_editions) | <span data-ttu-id="0516d-140">Champs statiques constants utilisés pour définir des ressources de base de données lors de la création d’une base de données en dehors d’un pool élastique ou lors du déplacement d’une base de données en dehors d’un pool élastique</span><span class="sxs-lookup"><span data-stu-id="0516d-140">Constant static fields used to set database resources when creating a database outside of an elastic pool or when moving a database out of an elastic pool</span></span>  
| [<span data-ttu-id="0516d-141">SqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="0516d-141">SqlElasticPool</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._sql_elastic_pool) | <span data-ttu-id="0516d-142">Créée à partir de la section `withNewElasticPool()` de la chaîne fluent qui a créé SqlServer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0516d-142">Created from the `withNewElasticPool()` section of the fluent chain that created the SqlServer in Azure.</span></span> <span data-ttu-id="0516d-143">Fournit des méthodes pour définir des limites de ressources pour les bases de données en cours d’exécution dans le pool élastique et pour le pool élastique lui-même.</span><span class="sxs-lookup"><span data-stu-id="0516d-143">Provides methods to set resource limits for databases running in the elastic pool and for the elastic pool itself.</span></span> 
| [<span data-ttu-id="0516d-144">ElasticPoolEditions</span><span class="sxs-lookup"><span data-stu-id="0516d-144">ElasticPoolEditions</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_editions) | <span data-ttu-id="0516d-145">Classe de champs constants définissant les ressources disponibles sur un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="0516d-145">Class of constant fields defining the resources available to an elastic pool.</span></span> <span data-ttu-id="0516d-146">Consultez la [documentation du pool élastique de la base de données SQL](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) pour les détails du niveau.</span><span class="sxs-lookup"><span data-stu-id="0516d-146">See [SQL database elastic pool documentation](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-pool) for tier details.</span></span> 
| [<span data-ttu-id="0516d-147">ElasticPoolDatabaseActivity</span><span class="sxs-lookup"><span data-stu-id="0516d-147">ElasticPoolDatabaseActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_database_activity) | <span data-ttu-id="0516d-148">Récupéré à partir de `SqlElasticPool.listDatabaseActivities()`.</span><span class="sxs-lookup"><span data-stu-id="0516d-148">Retreived from `SqlElasticPool.listDatabaseActivities()`.</span></span> <span data-ttu-id="0516d-149">Chaque objet de ce type représente une activité effectuée sur une base de données dans le pool élastique.</span><span class="sxs-lookup"><span data-stu-id="0516d-149">Each object of this type represents an activity performed on a database in the elastic pool.</span></span>
| [<span data-ttu-id="0516d-150">ElasticPoolActivity</span><span class="sxs-lookup"><span data-stu-id="0516d-150">ElasticPoolActivity</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.sql._elastic_pool_activity) | <span data-ttu-id="0516d-151">Récupérées dans une liste à partir de `SqlElasticPool.listActivities()`.</span><span class="sxs-lookup"><span data-stu-id="0516d-151">Retrieved in a List from `SqlElasticPool.listActivities()`.</span></span> <span data-ttu-id="0516d-152">Chacun des objets dans la liste représente une activité effectuée sur le pool élastique (les bases de données dans le pool élastique ne sont pas concernées).</span><span class="sxs-lookup"><span data-stu-id="0516d-152">Each of object in the list represents an activity performed on the elastic pool (not the databases in the elastic pool).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0516d-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0516d-153">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]