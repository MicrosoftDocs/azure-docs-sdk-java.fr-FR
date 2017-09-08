---
title: "Base de données Azure pour des bibliothèques PostgreSQL pour Java"
description: "Documentation de référence pour les bibliothèques de client Java pour Azure Database pour PostgreSQL"
keywords: "Azure, Java, SDK, API, SQL, base de données PostGres, PostgreSQL"
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
---
# <a name="azure-database-for-postgresql-libraries-for-java"></a>Base de données Azure pour des bibliothèques PostgreSQL pour Java

## <a name="overview"></a>Vue d'ensemble

[La base de données Azure pour PostgreSQL](/azure/sql-database/sql-database-technical-overview) est un service de base de données relationnelle Azure conçu pour les développeurs basés sur la version de la communauté du moteur open source de base de données [PostgreSQL](https://www.postgresql.org/).

Pour découvrir la base de données Azure pour PostgreSQL, consultez la section [Utiliser Java pour se connecter et interroger des données](/azure/postgresql/connect-java).

## <a name="client-jdbc-driver"></a>Pilote JDBC du client

Connectez-vous à la base de données Azure pour PostgreSQL à partir de vos applications à l’aide du [pilote JDBC PostgreSQL](https://jdbc.postgresql.org/) open source. Vous pouvez utiliser l’[API JDBC Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) pour vous connecter directement à la base de données ou utiliser les infrastructures d’accès aux données qui interagissent avec la base de données via JDBC comme [Hibernate](http://hibernate.org/).

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser le pilote JDBC du client dans votre projet.  

```XML
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
</dependency>
```   

## <a name="example"></a>Exemple

Connectez-vous à la base de données Azure pour PostgreSQL à l’aide du pilote JDBC PostgreSQL et sélectionnez tous les enregistrements dans le tableau des ventes. Il est possible d’obtenir la chaîne de connexion JDBC de la base de données à partir du portail Azure.

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

## <a name="samples"></a>Exemples

[Concevoir une base de données PostgreSQL à l’aide de l’interface Azure CLI](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) 

Explorez d’autres [exemples de code Java pour la base de données Azure pour PostgreSQL](https://azure.microsoft.com/resources/samples/?platform=java&term=postgres) que vous pouvez utiliser avec vos applications.
