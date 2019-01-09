---
title: Comment utiliser Spring Data JPA avec Azure PostgreSQL
description: Découvrez comment utiliser Spring Data JPA avec une base de données PostgreSQL Azure.
services: postgresql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: postgresql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 1849e03674534882a579f85b2654a628bd867487
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992130"
---
# <a name="how-to-use-spring-data-jpa-with-azure-postgresql"></a>Comment utiliser Spring Data JPA avec Azure PostgreSQL

## <a name="overview"></a>Vue d’ensemble

Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations dans une base de données Azure [PostgreSQL]https://www.postgresql.org/ à l’aide de l’[API de persistance Java (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.
* [Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité. ou l’utilitaire HTTP similaire pour tester la fonctionnalité.
* L’utilitaire de ligne de commande [psql](https://www.postgresql.org/docs/current/app-psql.html).
* Un client [Git](https://git-scm.com/downloads).

## <a name="create-a-postgresql-database-for-azure"></a>Créer une base de données PostgreSQL pour Azure

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a>Créer un serveur de base de données PostgreSQL à l’aide du portail Azure

> [!NOTE]
> 
> Vous trouverez des informations plus détaillées sur la création de bases de données PostgreSQL dans l’article [Création d’un serveur Azure Database pour PostgreSQL à l’aide du portail Azure](/azure/postgresql/quickstart-create-server-database-portal).

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Database pour PostgreSQL**.

   ![Créer une base de données PostgreSQL][POSTGRESQL01]

1. Entrez les informations suivantes :

   - **Nom du serveur** : choisissez un nom unique pour votre serveur PostgreSQL. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoyspostgresql.postgres.database.azure.com*.
   - **Abonnement**: indiquez l’abonnement Azure à utiliser.
   - **Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.
   - **Sélectionner la source** : pour ce didacticiel, sélectionnez `Blank` pour créer une base de données.
   - **Connexion d’administrateur du serveur** : spécifiez le nom d’administrateur de base de données.
   - **Mot de passe** et **Confirmer le mot de passe** : spécifiez le mot de passe de votre administrateur de base de données.
   - **Emplacement** : spécifiez la région géographique le plus proche de votre base de données.
   - **Version** : spécifiez la version la plus à jour la base de données.
   - **Niveau tarifaire** : pour ce didacticiel, spécifiez le niveau tarifaire le moins onéreux.

   ![Créer les propriétés de la base de données PostgreSQL][POSTGRESQL02]

1. Après avoir entré toutes les informations ci-dessus, cliquez sur **Créer**.

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a>Configurer une règle de pare-feu pour votre serveur de bases de données PostgreSQL à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur la base de données PostgreSQL que vous venez de créer.

   ![Sélectionner votre base de données PostgreSQL][POSTGRESQL03]

1. Cliquez sur **Sécurité de la connexion**, puis, dans **Règles de pare-feu**, créez une règle en spécifiant un nom unique. Ensuite, entrez la plage d’adresses IP qui doivent accéder à votre base de données, puis cliquez sur **Enregistrer**.

   ![Configurer la sécurité de la connexion][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a>Récupérer la chaîne de connexion de votre serveur PostgreSQL à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur la base de données PostgreSQL que vous venez de créer.

   ![Sélectionner votre base de données PostgreSQL][POSTGRESQL03]

1. Cliquez sur **Chaînes de connexion** et copiez la valeur dans le champ de texte **JDBC**.

   ![Récupérer votre chaîne de connexion JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a>Créer la base de données PostgreSQL à l’aide de l’utilitaire de ligne de commande `psql`

1. Ouvrez un interpréteur de commandes et connectez-vous à votre serveur PostgreSQL en entrant une commande `psql`, comme dans l’exemple suivant :

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `host` | Spécifie le nom complet du serveur PostgreSQL mentionné plus haut dans cet article. |
   | `host` | Spécifie le port du serveur PostgreSQL, c’est-à-dire `5432` par défaut. |
   | `username` | Spécifie votre administrateur PostgreSQL et le nom abrégé de serveur mentionné plus haut dans cet article. |
   | `dbname` | Spécifie que vous souhaitez utiliser la base de données `postgres` par défaut pour l’instant. |

   Votre serveur PostgreSQL doit répondre avec un affichage semblable à l’exemple suivant :

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. Créez une base de données nommée *mypgsqldb* en entrant une commande `psql` comme dans l’exemple suivant :

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   Votre serveur PostgreSQL doit répondre avec un affichage semblable à l’exemple suivant :

   ```shell
   CREATE DATABASE
   ```

1. FACULTATIF : vous pouvez vérifier la création de votre base de données en entrant `\l` au niveau de `psql`. Votre serveur PostgreSQL doit répondre avec une sortie semblable à l’exemple suivant :

   ```shell
                   List of databases
          Name        |      Owner      | Encoding
   -------------------+-----------------+----------
    azure_maintenance | azure_superuser | UTF8
    azure_sys         | azure_superuser | UTF8
    mypgsqldb         | wingtiptoysuser | UTF8
    postgres          | azure_superuser | UTF8
    template0         | azure_superuser | UTF8
    template1         | azure_superuser | UTF8
   (6 rows)
   ```

1. Entrez `\q` pour quitter l’utilitaire `psql`.

## <a name="configure-the-sample-application"></a>Configurer l’exemple d’application

1. Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `spring.datasource.url` | Spécifie votre chaîne JDBC PostgreSQL mentionnée plus haut dans cet article. |
   | `spring.datasource.username` | Spécifie le nom de votre administrateur PostgreSQL mentionné plus haut dans cet article, avec le nom abrégé du serveur accolé. |
   | `spring.datasource.password` | Spécifie votre mot de passe administrateur PostgreSQL mentionné plus haut dans cet article. |

1. Enregistrez et fermez le fichier *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Packager et tester l’exemple d’application 

1. Compilez l’exemple d’application avec Maven :

   ```shell
   mvn clean package -P postgresql
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

Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations dans une base de données Azure PostgreSQL à l’aide de JPA.

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

[POSTGRESQL01]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-01.png
[POSTGRESQL02]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-02.png
[POSTGRESQL03]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-03.png
[POSTGRESQL04]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-04.png
[POSTGRESQL05]: media/configure-spring-data-jpa-with-azure-postgresql/create-postgresql-05.png
