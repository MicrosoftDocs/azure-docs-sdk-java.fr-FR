---
title: "Bibliothèques Azure SQL Database pour Java"
description: "Connectez-vous à Azure SQL Database à l’aide du pilote JDBC ou des instances de base de données de gestion Azure SQL avec l’API de gestion."
keywords: "Azure, Java, SDK, API, SQL, base de données, JDBC"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/05/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: sql-database
ms.openlocfilehash: 3ae4015ae57e5eac4dafb30f4a42881986501853
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-sql-database-libraries-for-java"></a><span data-ttu-id="007b0-104">Bibliothèques Azure SQL Database pour Java</span><span class="sxs-lookup"><span data-stu-id="007b0-104">Azure SQL Database libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="007b0-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="007b0-105">Overview</span></span>

<span data-ttu-id="007b0-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) est un service de base de données relationnelle reposant sur le moteur Microsoft SQL Server qui prend en charge les données de tables, JSON, spatiales et XML.</span><span class="sxs-lookup"><span data-stu-id="007b0-106">[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) is a relational database service using the Microsoft SQL Server engine that supports table, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="007b0-107">Pour découvrir Azure SQL Database, consultez [Azure SQL Database : utiliser Java pour vous connecter et interroger des données](/azure/sql-database/sql-database-connect-query-java).</span><span class="sxs-lookup"><span data-stu-id="007b0-107">To get started with Azure SQL Database, see [Azure SQL Database: Use Java to connect and query data](/azure/sql-database/sql-database-connect-query-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="007b0-108">Pilote JDBC du client</span><span class="sxs-lookup"><span data-stu-id="007b0-108">Client JDBC driver</span></span>

<span data-ttu-id="007b0-109">Connectez-vous à Azure SQL Database à partir de vos applications à l’aide du [pilote JDBC SQL Database](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span><span class="sxs-lookup"><span data-stu-id="007b0-109">Connect to Azure SQL Database from your applications using the [SQL Database JDBC driver](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server).</span></span> <span data-ttu-id="007b0-110">Vous pouvez utiliser l’[API JDBC Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) pour vous connecter directement à la base de données ou utiliser les infrastructures d’accès aux données qui interagissent avec la base de données via JDBC comme [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="007b0-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect with the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="007b0-111">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser le pilote JDBC du client dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="007b0-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="007b0-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="007b0-112">Example</span></span>

<span data-ttu-id="007b0-113">Connectez-vous à la base de données SQL et sélectionnez tous les enregistrements dans une table à l’aide de JDBC.</span><span class="sxs-lookup"><span data-stu-id="007b0-113">Connect to SQL database and select all records in a table using JDBC.</span></span>

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a><span data-ttu-id="007b0-114">API de gestion</span><span class="sxs-lookup"><span data-stu-id="007b0-114">Management API</span></span>

<span data-ttu-id="007b0-115">Créez et gérez des ressources Azure SQL Database dans votre abonnement avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="007b0-115">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span>   

<span data-ttu-id="007b0-116">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="007b0-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="007b0-117">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="007b0-117">Explore the Management APIs</span></span>](/java/api/overview/azure/sql/managementapi)

### <a name="example"></a><span data-ttu-id="007b0-118">Exemple</span><span class="sxs-lookup"><span data-stu-id="007b0-118">Example</span></span>

<span data-ttu-id="007b0-119">Créez une ressource de base de données SQL et restreignez l’accès à une plage d’adresses IP à l’aide d’une règle de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="007b0-119">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a><span data-ttu-id="007b0-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="007b0-120">Samples</span></span>

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

<span data-ttu-id="007b0-121">Explorez d’autres [exemples de code Java pour Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="007b0-121">Explore more [sample Java code for Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) you can use in your apps.</span></span>