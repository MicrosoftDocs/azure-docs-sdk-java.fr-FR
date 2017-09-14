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
ms.openlocfilehash: 4c16d602d33b8d2c75e2b9de8f5f11ace138c25d
ms.sourcegitcommit: ae39830d5a54fedceac78d8df1718e77741e03fa
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2017
---
# <a name="azure-sql-database-libraries-for-java"></a>Bibliothèques Azure SQL Database pour Java

## <a name="overview"></a>Vue d'ensemble

[Azure SQL Database](/azure/sql-database/sql-database-technical-overview) est un service de base de données relationnelle reposant sur le moteur Microsoft SQL Server qui prend en charge les données de tables, JSON, spatiales et XML. 

Pour découvrir Azure SQL Database, consultez [Azure SQL Database : utiliser Java pour vous connecter et interroger des données](/azure/sql-database/sql-database-connect-query-java).

## <a name="client-jdbc-driver"></a>Pilote JDBC du client

Connectez-vous à Azure SQL Database à partir de vos applications à l’aide du [pilote JDBC SQL Database](/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server). Vous pouvez utiliser l’[API JDBC Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) pour vous connecter directement à la base de données ou utiliser les infrastructures d’accès aux données qui interagissent avec la base de données via JDBC comme [Hibernate](http://hibernate.org/).

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser le pilote JDBC du client dans votre projet.


```XML
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```   

### <a name="example"></a>Exemple

Connectez-vous à la base de données SQL et sélectionnez tous les enregistrements dans une table à l’aide de JDBC.

```java
String connectionString = "jdbc:sqlserver://fabrikam.database.windows.net:1433;database=fiber;user=raisa;password=testpass;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
try {
    Connection conn = DriverManager.getConnection(connectionString);
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery("SELECT * FROM SALES");
}  
```

## <a name="management-api"></a>API de gestion

Créez et gérez des ressources Azure SQL Database dans votre abonnement avec l’API de gestion.   

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-sql</artifactId>
    <version>1.2.1</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/sql/managementapi)

### <a name="example"></a>Exemple

Créez une ressource de base de données SQL et restreignez l’accès à une plage d’adresses IP à l’aide d’une règle de pare-feu.

```java
SqlServer sqlServer = azure.sqlServers().define(sqlDbName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(resourceGroupName)
                    .withAdministratorLogin(administratorLogin)
                    .withAdministratorPassword(administratorPassword)
                    .withNewFirewallRule("172.16.0.0", "172.31.255.255")
                    .create();
```

## <a name="samples"></a>Exemples

[!INCLUDE [java-sql-samples](../docs-ref-conceptual/includes/sql.md)]

Explorez d’autres [exemples de code Java pour Azure SQL Database](https://azure.microsoft.com/resources/samples/?platform=java&term=SQL) que vous pouvez utiliser avec vos applications.