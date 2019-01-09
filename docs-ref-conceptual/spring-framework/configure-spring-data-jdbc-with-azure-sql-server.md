---
title: Comment utiliser Spring Data JDBC avec Azure SQL Database
description: Découvrez comment utiliser Spring Data JDBC avec une base de données SQL Azure.
services: sql-database
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: sql-database
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 92f489b513eeb05efaacdf07af2b976de8f84868
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992119"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-sql-database"></a>Comment utiliser Spring Data JDBC avec Azure SQL Database

## <a name="overview"></a>Vue d’ensemble

Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations dans une [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) à l’aide de [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.
* [Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité.
* Un client [Git](https://git-scm.com/downloads).

## <a name="create-an-azure-sql-satabase"></a>Créer une base de données SQL Azure

### <a name="create-a-sql-database-server-using-the-azure-portal"></a>Créer un serveur de base de données SQL à l’aide du portail Azure

> [!NOTE]
> 
> Vous trouverez des informations plus détaillées sur la création de bases de données SQL Azure dans l’article [Création d’une base de données SQL Azure dans le portail Azure](/azure/sql-database/sql-database-get-started-portal).

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Base de données SQL**.

   ![Créer une base de données SQL][SQL01]

1. Indiquez les informations suivantes :

   - **Nom de la base de données** : choisissez un nom unique pour votre base de données SQL. Elle sera créée dans le serveur SQL de votre choix plus tard.
   - **Abonnement**: indiquez l’abonnement Azure à utiliser.
   - **Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.
   - **Sélectionner la source** : pour ce didacticiel, sélectionnez `Blank database` pour créer une base de données.

   ![Spécifier les propriétés de la base de données SQL][SQL02]
   
1. Cliquez sur **Serveur** et **Créer un serveur**, puis spécifiez les informations suivantes :

   - **Nom du serveur** : choisissez un nom unique pour votre serveur SQL. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoyssql.database.windows.net*.
   - **Connexion d’administrateur du serveur** : spécifiez le nom d’administrateur de base de données.
   - **Mot de passe** et **Confirmer le mot de passe** : spécifiez le mot de passe de votre administrateur de base de données.
   - **Emplacement** : spécifiez la région géographique le plus proche de votre base de données.

   ![Spécifier votre serveur SQL][SQL03]

1. Après avoir entré toutes les informations ci-dessus, cliquez sur **Sélectionner**.

1. Pour ce didacticiel, spécifiez le **niveau tarifaire** le moins onéreux; puis cliquez sur **Créer**.

   ![Créer votre base de données SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a>Configurer une règle de pare-feu pour votre serveur SQL à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur le serveur SQL que vous venez de créer.

   ![Sélectionner votre serveur SQL][SQL05]

1. Dans la section **Présentation**, cliquez sur **Afficher les paramètres de pare-feu**.

   ![Afficher les paramètres de pare-feu][SQL06]

1. Dans la section **Pare-feux et réseaux virtuels**, créez une règle en spécifiant un nom unique. Ensuite, entrez la plage d’adresses IP qui doivent accéder à votre base de données, puis cliquez sur **Enregistrer**.

   ![Configurer les paramètres de pare-feu][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a>Récupérer la chaîne de connexion de votre serveur SQL à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur la base de données SQL que vous venez de créer.

   ![Sélectionner votre base de données SQL][SQL08]

1. Cliquez sur **Chaînes de connexion**, puis sur **JDBC**, et copiez la valeur dans le champ de texte JDBC.

   ![Récupérer votre chaîne de connexion JDBC][SQL09]

## <a name="configure-the-sample-application"></a>Configurer l’exemple d’application

1. Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `spring.datasource.url` | Spécifie une version modifiée de votre chaîne SQL JDBC mentionnée plus haut dans cet article. |
   | `spring.datasource.username` | Spécifie le nom de votre administrateur SQL mentionné plus haut dans cet article, avec le nom abrégé du serveur accolé. |
   | `spring.datasource.password` | Spécifie votre mot de passe administrateur SQL mentionné plus haut dans cet article. |

1. Enregistrez et fermez le fichier *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Packager et tester l’exemple d’application 

1. Compilez l’exemple d’application avec Maven :

   ```shell
   mvn clean package -P sql
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

Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations dans une base de données Azure SQL à l’aide de JDBC.

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

[SQL01]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jdbc-with-azure-sql-server/create-azure-sql-09.png
