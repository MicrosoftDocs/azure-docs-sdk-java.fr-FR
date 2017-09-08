---
title: "Base de données Azure pour des bibliothèques MySQL pour Java"
description: "Documentation de référence pour les bibliothèques de client Java pour les bases de données Azure pour MySQL"
keywords: "Azure, Java,SDK, API, SQL, base de données, PostGres, MySQL"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: mysql
ms.openlocfilehash: 72c94ef4bdad7adeae63da2efda93b52a9afef53
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-mysql-libraries-for-java"></a><span data-ttu-id="97766-104">Base de données Azure pour des bibliothèques MySQL pour Java</span><span class="sxs-lookup"><span data-stu-id="97766-104">Azure Database for MySQL libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="97766-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="97766-105">Overview</span></span>

<span data-ttu-id="97766-106">[La base de données Azure pour MySQL](/azure/sql-database/sql-database-technical-overview) est un service de base de données relationnelle basé sur le moteur open source [MySQL](https://www.mysql.com/) Server.</span><span class="sxs-lookup"><span data-stu-id="97766-106">[Azure Database for MySQL](/azure/sql-database/sql-database-technical-overview) is a relational database service based on the open source [MySQL](https://www.mysql.com/) Server engine.</span></span> 

<span data-ttu-id="97766-107">Pour découvrir la base de données Azure pour MySQL, consultez la section [Utiliser Java pour se connecter et interroger des données](/azure/mysql/connect-java).</span><span class="sxs-lookup"><span data-stu-id="97766-107">To get started with Azure Database for MySQL, see [Use Java to connect and query data](/azure/mysql/connect-java).</span></span>

## <a name="client-jbdc-driver"></a><span data-ttu-id="97766-108">Pilote JBDC du client</span><span class="sxs-lookup"><span data-stu-id="97766-108">Client JBDC driver</span></span>

<span data-ttu-id="97766-109">Connectez-vous à la base de données Azure pour MySQL à partir de vos applications à l’aide du [pilote JDBC MySQL](https://dev.mysql.com/downloads/connector/j/) open source.</span><span class="sxs-lookup"><span data-stu-id="97766-109">Connect to Azure Database for MySQL from your applications using the open-source [MySQL JDBC driver](https://dev.mysql.com/downloads/connector/j/).</span></span> <span data-ttu-id="97766-110">Vous pouvez utiliser l’[API JDBC Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) pour vous connecter directement à la base de données ou utiliser les infrastructures d’accès aux données qui interagissent avec la base de données via JDBC comme [Hibernate](http://hibernate.org/).</span><span class="sxs-lookup"><span data-stu-id="97766-110">You can use the [Java JDBC API](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) to directly connect to the database or use data access frameworks that interact with the database through JDBC such as [Hibernate](http://hibernate.org/).</span></span>

<span data-ttu-id="97766-111">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser le pilote JDBC du client dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="97766-111">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client JDBC driver in your project.</span></span>  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="97766-112">Exemple</span><span class="sxs-lookup"><span data-stu-id="97766-112">Example</span></span>

<span data-ttu-id="97766-113">Connectez-vous à la base de données Azure pour MySQL à l’aide du pilote JDBC et sélectionnez tous les enregistrements dans le tableau des ventes.</span><span class="sxs-lookup"><span data-stu-id="97766-113">Connect to Azure Database for MySQL using JDBC and select all records in the sales table.</span></span> <span data-ttu-id="97766-114">Il est possible d’obtenir la chaîne de connexion JDBC de la base de données à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="97766-114">You can get the JDBC connection string for the database from the Azure Portal.</span></span>

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a><span data-ttu-id="97766-115">Exemples</span><span class="sxs-lookup"><span data-stu-id="97766-115">Samples</span></span>

<span data-ttu-id="97766-116">[Créer une application web Java et MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span><span class="sxs-lookup"><span data-stu-id="97766-116">[Build a Java and MySQL web app](/azure/app-service-web/app-service-web-tutorial-java-mysql) </span></span>  
[<span data-ttu-id="97766-117">Concevoir une base de données MySQL à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="97766-117">Design a MySQL database using the Azure CLI</span></span>](/azure/mysql/tutorial-design-database-using-cli)   

<span data-ttu-id="97766-118">Explorez d’autres [exemples de code Java pour la base de données Azure pour MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="97766-118">Explore more [sample Java code for Azure Database for MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) you can use in your apps.</span></span>
