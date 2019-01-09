---
title: Comment utiliser Spring Data JDBC avec Azure MySQL
description: Découvrez comment utiliser Spring Data JDBC avec une base de données Azure MySQL.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 5ec89194c72cef81c79d21382e41b33ebe91d3d0
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992123"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-mysql"></a>Comment utiliser Spring Data JDBC avec Azure MySQL

## <a name="overview"></a>Vue d’ensemble

Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations dans une base de données Azure [MySQL](https://www.mysql.com/) à l’aide de [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.
* [Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité.
* L’utilitaire de ligne de commande [mysql](https://dev.mysql.com/downloads/).
* Un client [Git](https://git-scm.com/downloads).

## <a name="create-a-mysql-database-for-azure"></a>Créer une base de données MySQL pour Azure

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a>Créer un serveur de base de données MySQL à l’aide du portail Azure

> [!NOTE]
> 
> Vous trouverez des informations plus détaillées sur la création de bases de données MySQL dans l’article [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Database pour MySQL**.

   ![Créer une base de données MySQL][MYSQL01]

1. Entrez les informations suivantes :

   - **Nom du serveur** : choisissez un nom unique pour votre serveur MySQL. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoysmysql.mysql.database.azure.com*.
   - **Abonnement**: indiquez l’abonnement Azure à utiliser.
   - **Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.
   - **Sélectionner la source** : pour ce didacticiel, sélectionnez `Blank` pour créer une base de données.
   - **Connexion d’administrateur du serveur** : spécifiez le nom d’administrateur de base de données.
   - **Mot de passe** et **Confirmer le mot de passe** : spécifiez le mot de passe de votre administrateur de base de données.
   - **Emplacement** : spécifiez la région géographique le plus proche de votre base de données.
   - **Version** : spécifiez la version la plus à jour la base de données.
   - **Niveau tarifaire** : pour ce didacticiel, spécifiez le niveau tarifaire le moins onéreux.

   ![Créer les propriétés de la base de données MySQL][MYSQL02]

1. Après avoir entré toutes les informations ci-dessus, cliquez sur **Créer**.

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a>Configurer une règle de pare-feu pour votre serveur de bases de données MySQL à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur la base de données MySQL que vous venez de créer.

   ![Sélectionner la base de données MySQL][MYSQL03]

1. Cliquez sur **Sécurité de la connexion**, puis, dans **Règles de pare-feu**, créez une règle en spécifiant un nom unique. Ensuite, entrez la plage d’adresses IP qui doivent accéder à votre base de données, puis cliquez sur **Enregistrer**.

   ![Configurer la sécurité de la connexion][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a>Récupérer la chaîne de connexion de votre serveur MySQL à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur la base de données MySQL que vous venez de créer.

   ![Sélectionner la base de données MySQL][MYSQL03]

1. Cliquez sur **Chaînes de connexion** et copiez la valeur dans le champ de texte **JDBC**.

   ![Récupérer votre chaîne de connexion JDBC][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a>Créer la base de données MySQL à l’aide de l’utilitaire de ligne de commande `mysql`

1. Ouvrez un interpréteur de commandes et connectez-vous à votre serveur MySQL en entrant une commande `mysql`, comme dans l’exemple suivant :

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `host` | Spécifie le nom complet du serveur MySQL mentionné plus haut dans cet article. |
   | `user` | Spécifie votre administrateur MySQL et le nom abrégé de serveur mentionné plus haut dans cet article. |
   | `p` | Spécifie qu’il faut attendre l’invite de mot de passe. |

   Votre serveur MySQL doit répondre avec un affichage semblable à l’exemple suivant :

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. Créez une base de données nommée *mysqldb* en entrant une commande `mysql` comme dans l’exemple suivant :

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   Votre serveur MySQL doit répondre avec un affichage semblable à l’exemple suivant :

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. FACULTATIF : vous pouvez vérifier que votre base de données a été créée en entrant une commande `mysql` comme dans l’exemple suivant :

   ```SQL
   SHOW DATABASES;
   ```

   Votre serveur MySQL doit répondre avec un affichage semblable à l’exemple suivant :

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. Entrez `\q` pour quitter l’utilitaire `mysql`.

## <a name="configure-the-sample-application"></a>Configurer l’exemple d’application

1. Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :

   ```yaml
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false&serverTimezone=UTC
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `spring.datasource.url` | Spécifie votre chaîne JDBC MySQL mentionnée plus haut dans cet article, avec un fuseau horaire. |
   | `spring.datasource.username` | Spécifie le nom de votre administrateur MySQL mentionné plus haut dans cet article, avec le nom abrégé du serveur accolé. |
   | `spring.datasource.password` | Spécifie votre mot de passe administrateur MySQL mentionné plus haut dans cet article. |

1. Enregistrez et fermez le fichier *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Packager et tester l’exemple d’application 

1. Compilez l’exemple d’application avec Maven :

   ```shell
   mvn clean package -P mysql
   ```

1. Démarrez l’exemple d’application :

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. Créez des enregistrements à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   Votre application doit renvoyer des valeurs comme suit :

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. Récupérez tous les enregistrements existants à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   Votre application doit renvoyer des valeurs comme suit :

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a>Résumé

Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations dans une base de données Azure MySQL à l’aide de JDBC.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Data]: https://spring.io/projects/spring-data
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[MYSQL01]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-05.png
