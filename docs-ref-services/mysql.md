---
title: Base de données Azure pour des bibliothèques MySQL pour Java
description: Documentation de référence pour les bibliothèques de client Java pour les bases de données Azure pour MySQL
keywords: Azure, Java,SDK, API, SQL, base de données, PostGres, MySQL
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
ms.locfileid: "21931015"
---
# <a name="azure-database-for-mysql-libraries-for-java"></a>Base de données Azure pour des bibliothèques MySQL pour Java

## <a name="overview"></a>Vue d'ensemble

[La base de données Azure pour MySQL](/azure/sql-database/sql-database-technical-overview) est un service de base de données relationnelle basé sur le moteur open source [MySQL](https://www.mysql.com/) Server. 

Pour découvrir la base de données Azure pour MySQL, consultez la section [Utiliser Java pour se connecter et interroger des données](/azure/mysql/connect-java).

## <a name="client-jbdc-driver"></a>Pilote JBDC du client

Connectez-vous à la base de données Azure pour MySQL à partir de vos applications à l’aide du [pilote JDBC MySQL](https://dev.mysql.com/downloads/connector/j/) open source. Vous pouvez utiliser l’[API JDBC Java](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/) pour vous connecter directement à la base de données ou utiliser les infrastructures d’accès aux données qui interagissent avec la base de données via JDBC comme [Hibernate](http://hibernate.org/).

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser le pilote JDBC du client dans votre projet.  

```XML
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.42</version>
</dependency>
```   

## <a name="example"></a>Exemple

Connectez-vous à la base de données Azure pour MySQL à l’aide du pilote JDBC et sélectionnez tous les enregistrements dans le tableau des ventes. Il est possible d’obtenir la chaîne de connexion JDBC de la base de données à partir du portail Azure.

```java
String url = String.format("jdbc:mysql://fabrikamysql.mysql.database.azure.com:3306/fabrikamdb?verifyServerCertificate=true&useSSL=true&requireSSL=false");
try {
    Connection conn = DriverManager.getConnection(url, "frank@fabrikamysql", "aBcDeFgHiJkL");
    String selectSql = "SELECT * FROM SALES";
    Statement statement = conn.createStatement();
    ResultSet resultSet = statement.executeQuery(selectSql);
}
```

## <a name="samples"></a>Exemples

[Créer une application web Java et MySQL](/azure/app-service-web/app-service-web-tutorial-java-mysql)   
[Concevoir une base de données MySQL à l’aide de l’interface Azure CLI](/azure/mysql/tutorial-design-database-using-cli)   

Explorez d’autres [exemples de code Java pour la base de données Azure pour MySQL](https://azure.microsoft.com/resources/samples/?platform=java&term=mysql) que vous pouvez utiliser avec vos applications.
