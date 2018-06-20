---
title: Base de données Azure pour des bibliothèques PostgreSQL pour Java
description: Documentation de référence pour les bibliothèques de client Java pour Azure Database pour PostgreSQL
keywords: Azure, Java, SDK, API, SQL, base de données PostGres, PostgreSQL
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: postgresql
ms.openlocfilehash: d6fa2acb9a2f44b157ae52ba6e41f6777a43b574
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930975"
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a><span data-ttu-id="e6f3a-104">Base de données Azure pour des bibliothèques PostgreSQL pour Java</span><span class="sxs-lookup"><span data-stu-id="e6f3a-104">Azure Database for PostgreSQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="e6f3a-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e6f3a-105">Overview</span></span>

<span data-ttu-id="e6f3a-106">[La base de données Azure pour PostgreSQL](/azure/sql-database/sql-database-technical-overview) est un service de base de données relationnelle Azure conçu pour les développeurs basés sur la version de la communauté du moteur open source de base de données [PostgreSQL](https://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="e6f3a-106">[Azure Database for PostgreSQL](/azure/sql-database/sql-database-technical-overview) is a relational database service in Azure built for developers based on the community version of open source [PostgreSQL](https://www.postgresql.org/) database engine.</span></span>

<span data-ttu-id="e6f3a-107">Pour découvrir la base de données Azure pour PostgreSQL, consultez la section [Utiliser Java pour se connecter et interroger des données](/azure/postgresql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="e6f3a-107">To get started with Azure Database for PostgreSQL, see [Use Java to connect and query data](/azure/postgresql/connect-java).</span></span>

## <a name="client-jdbc-driver"></a><span data-ttu-id="e6f3a-108">Pilote JDBC du client</span><span class="sxs-lookup"><span data-stu-id="e6f3a-108">Client JDBC driver</span></span>

<span data-ttu-id="e6f3a-109">Connectez-vous à la base de données Azure pour PostgreSQL à partir de vos applications à l’aide du [pilote JDBC PostgreSQL](https://jdbc.postgresql.org/) open source.</span><span class="sxs-lookup"><span data-stu-id="e6f3a-109">Connect to Azure Database for PostgreSQL from your applications using the open-source [PostgreSQL JDBC driver](https://jdbc.postgresql.org/).</span></span> <span data-ttu-id="e6f3a-110">Vous pouvez utiliser l’[API JDBC Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) pour vous connecter directement à la base de données ou utiliser les infrastructures d’accès aux données qui interagissent avec la base de données via JDBC comme [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="e6f3a-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="e6f3a-111">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser le pilote JDBC du client dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e6f3a-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="e6f3a-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="e6f3a-112">Example</span></span>

<span data-ttu-id="e6f3a-113">Connectez-vous à la base de données Azure pour PostgreSQL à l’aide du pilote JDBC PostgreSQL et sélectionnez tous les enregistrements dans le tableau des ventes.</span><span class="sxs-lookup"><span data-stu-id="e6f3a-113">Connect to Azure Database for PostgreSQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="e6f3a-114">Il est possible d’obtenir la chaîne de connexion JDBC de la base de données à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e6f3a-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:postgresql://mypostgresdb.postgres.database.azure.com:5432/mydb?user=frank@mypostgresdb&password=AbCdEfGhIjK&ssl=true");
Connection connection = null;
try {
    connection = DriverManager.getConnection(url);
    String selectSql = "SELECT * FROM SALES";
    Statement statement = connection.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="e6f3a-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="e6f3a-115">Samples</span></span>

[<span data-ttu-id="e6f3a-116">Concevoir une base de données PostgreSQL à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e6f3a-116">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

<span data-ttu-id="e6f3a-117">Explorez d’autres [exemples de code Java pour la base de données Azure pour PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="e6f3a-117">Explore more [sample Java code for Azure Database for PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) you can use in your apps.</span></span>
