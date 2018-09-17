---
title: Comment utiliser Spring Data Gremlin Starter avec l’API SQL Azure Cosmos DB
description: Découvrez comment configurer une application créée avec Spring Boot Initializer à l’aide de l’API SQL Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 4e0138e3cc474b4c47d3bf492e696ec49ea3ef37
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040267"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a>Comment utiliser Spring Data Gremlin Starter avec l’API SQL Azure Cosmos DB

## <a name="overview"></a>Vue d’ensemble

Le starter Spring Data Gremlin fournit une prise en charge de Spring Data pour le langage de requête Gremlin d’Apache, pouvant être utilisé par les développeurs avec n’importe quelle banque de données compatible avec Gremlin.

Cet article illustre la création d’une base de données Azure Cosmos à l’aide du Portail Azure pour une utilisation avec l’API Gremlin, l’utilisation de **[Spring Initializr]** pour la création d’une application java personnalisée, et l’ajout de la fonctionnalité Spring Data Gremlin Starter à votre application personnalisée pour le stockage et la récupération des données dans votre base de données Azure Cosmos à l’aide de Gremlin.

## <a name="prerequisites"></a>Prérequis

Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

> [!IMPORTANT]
>
> La version 2.0 de Spring Boot ou une version ultérieure est requise pour effectuer les différentes étapes de cet article.
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a>Créer une base de données Azure Cosmos à l’aide du portail Azure

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a>Créez votre base de données Cosmos Azure pour une utilisation avec l’API Gremlin

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+ Créer une ressource**.

   ![Créer une ressource][AZ01]

1. Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.

   ![Créer une base de données Azure Cosmos][AZ02]

1. Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :

   * Entrez un **ID** unique que vous utiliserez en tant q’URI de Gremlin pour votre base de données. Par exemple : si vous avez écrit **wingtiptoysdata** pour l’**ID**, l’URI de Gremlin sera alors *wingtiptoysdata.gremlin.cosmosdb.azure.com*.
   * Sélectionnez **Gremlin (Graphique)** pour l’API.
   * Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.
   * Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.
   * Spécifiez l’**Emplacement** pour votre base de données.
   
   Une fois ces options définies, cliquez sur **Créer** pour créer votre base de données.

   ![Spécifiez les options de la base de données Azure Cosmos][AZ03]

1. Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**. Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.

   ![Toutes les ressources][AZ04]

1. Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés d’accès**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.

   ![Clés d’accès][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a>Ajouter un graphique à votre base de données Azure Cosmos

1. Cliquez sur **Explorateur de données**, puis sur **Nouveau graphique**.

   ![Nouveau graphique][AZ06]

1. Lorsque la page **Ajouter un graphique** s’affiche, entrez les informations suivantes :

   * Définissez un **ID de base de données** unique pour votre base de données.
   * Définissez un **ID de graphique** unique pour votre graphique.
   * Vous pouvez choisir de préciser votre **Capacité de stockage**, ou accepter celle définie par défaut.
   * Définissez votre **Débit**, et choisissez pour cet exemple 400 unités de requête (RU).
   
   Une fois que vous avez défini ces options, cliquez sur **OK** pour créer votre graphique.

   ![Ajouter un graphique][AZ07]

1. Une fois votre graphique créé, vous pouvez utiliser l’**Explorateur de données** pour l’afficher.

   ![Affichage des propriétés du graphique][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Créer une application Spring Boot simple avec Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms du **Groupe** et de l’**Artefact** de votre application, choisissez une version de **Spring Boot** qui soit la version 2.0 ou ultérieure, puis cliquez sur le bouton **Générer le projet**.

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple : *com.example.wintiptoysdata.
   >

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a>Configurer votre application Spring Boot pour utiliser le starter Spring Data Gremlin

1. Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   -ou-

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez le starter Spring Data Gremlin à la liste de `<dependencies>` :

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml][PM02]

1. Enregistrez et fermez le fichier *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB

1. Localisez le répertoire des *ressources* de votre application, et créez un nouveau fichier qui s’intitule *application.yml*. Par exemple : 

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Créez le fichier application.yml][RE01]

1.  Ouvrez le fichier *application.yml* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   Où :
   | Champ | Description |
   | ---|---|
   | `endpoint` | Définit l’URI Gremlin pour votre base de données, provenant de l’**ID** que vous avez précisé lors de la création de votre base de données Azure Cosmos précédemment dans ce tutoriel. |
   | `port` | Définit le port TCP/IP, qui devrait être **443** pour le protocole HTTPS. |
   | `username` | Définit l’**ID de base donnée** et l’**ID de graphique** uniques que vous avez ajoutés dans votre graphique plus tôt dans ce tutoriel ; il doit être entré en respectant la syntaxe suivante : « /dbs/**{Database id}**/colls/**{Graph id}**  ». |
   | `password` | Définit la **Clé d’accès** primaire ou secondaire que vous avez copiée plus tôt au cours de ce tutoriel. |
   | `telemetryAllowed` | Choisissez **vrai** si vous souhaitez autoriser la télémétrie ; dans le cas contraire, choisissez **faux**.

1. Enregistrez et fermez le fichier *application.yml*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données

Dans cette section, vous pouvez créer les classes Java nécessaires au stockage de données dans votre base de données.

### <a name="modify-the-main-application-class"></a>Modifiez la classe d’application principale

1. Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localiser le fichier Java de l’application][JV01]

1. Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata;
   
   // These imports are required for the application.
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.example.wingtiptoysdata.domain.Network;
   import com.example.wingtiptoysdata.domain.Person;
   import com.example.wingtiptoysdata.domain.Relation;
   import com.example.wingtiptoysdata.repository.NetworkRepository;
   import com.example.wingtiptoysdata.repository.PersonRepository;
   import com.example.wingtiptoysdata.repository.RelationRepository;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import javax.annotation.PostConstruct;
   import javax.annotation.PreDestroy;
   
   @SpringBootApplication
   public class WingtiptoysdataApplication {
   
       // Define several person classes to store personal data.
       private final Person person1 = new Person("01", "Nellie Hughes", "23");
       private final Person person2 = new Person("02", "Delmar Alfred", "34");
       private final Person person3 = new Person("03", "Kelley Hunter", "45");
       private final Person person4 = new Person("04", "Roscoe Guerin", "56");
       private final Person person5 = new Person("05", "Gracie Chavez", "67");
   
       // Define relationship classes to define the relationships between some of the persons.
       private final Relation relation1 = new Relation("0102", "siblings", person1, person2);
       private final Relation relation2 = new Relation("0203", "coworkers", person2, person3);
       private final Relation relation3 = new Relation("0301", "parent", person3, person1);
       private final Relation relation4 = new Relation("0302", "parent", person3, person2);
       private final Relation relation5 = new Relation("0501", "grandparent", person5, person1);
       private final Relation relation6 = new Relation("0502", "grandparent", person5, person2);
   
       // Define the network.
       private final Network network = new Network();
   
       // Autowire the repositories and factory.
       @Autowired
       private PersonRepository personRepo;
       @Autowired
       private RelationRepository relationRepo;
       @Autowired
       private NetworkRepository networkRepo;
       @Autowired
       private GremlinFactory factory;
   
       // Run the Spring application and exit.
    public static void main(String[] args) {
           SpringApplication.run(WingtiptoysdataApplication.class, args);
           System.exit(0);
    }
   
       // Perform post-construct operations.    
       @PostConstruct
       public void setup() {
           // Delete any existing data from the database.
           this.networkRepo.deleteAll();
   
           // Add the relationship classes as edges.
           this.network.getEdges().add(this.relation1);
           this.network.getEdges().add(this.relation2);
           this.network.getEdges().add(this.relation3);
           this.network.getEdges().add(this.relation4);
           this.network.getEdges().add(this.relation5);
           this.network.getEdges().add(this.relation6);
   
           // Add the person classes as vertices.
           this.network.getVertexes().add(this.person1);
           this.network.getVertexes().add(this.person2);
           this.network.getVertexes().add(this.person3);
           this.network.getVertexes().add(this.person4);
           this.network.getVertexes().add(this.person5);
   
           // Save the network.
           this.networkRepo.save(this.network);
       }
   }
   ```

1. Enregistrez et fermez le fichier Java principal de l’application.

### <a name="define-a-basic-class-for-storing-configuration-information"></a>Définir une classe de base pour le stockage d’informations liées à la configuration

1. Créez un dossier intitulé *config* sous le répertoire du package de votre application, par exemple :

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. Créez un fichier java intitulé *UserRepositoryConfiguration.java* dans le répertoire *config*, ouvrez le fichier dans un éditeur de texte, et ajoutez-y les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.config;

   import com.microsoft.spring.data.gremlin.common.GremlinConfiguration;
   import com.microsoft.spring.data.gremlin.common.GremlinFactory;
   import com.microsoft.spring.data.gremlin.config.AbstractGremlinConfiguration;
   import com.microsoft.spring.data.gremlin.repository.config.EnableGremlinRepositories;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.context.properties.EnableConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   import org.springframework.context.annotation.PropertySource;
   
   @Configuration
   @EnableGremlinRepositories(basePackages = "com.example.wingtiptoysdata.repository")
   @EnableConfigurationProperties(GremlinConfiguration.class)
   @PropertySource("classpath:application.yml")
   public class UserRepositoryConfiguration extends AbstractGremlinConfiguration {
   
       @Autowired
       private GremlinConfiguration config;
   
       @Override
       public GremlinConfiguration getGremlinConfiguration() {
           return this.config;
       }
   }
   ```

1. Enregistrez et fermez le fichier *UserRepositoryConfiguration.java*.

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a>Établir un ensemble de classes qui définit les éléments de votre base de données de graphiques

1. Créez un dossier intitulé *domain*sous le répertoire de package de votre application, par exemple :

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. Créez un fichier java intitulé *Person.java* dans le répertoire *domain*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Vertex;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Vertex
   @AllArgsConstructor
   @NoArgsConstructor
   public class Person {
   
       @Id
       private String id;
   
       private String name;
   
       private String age;
   }
   ```

1. Enregistrez et fermez le fichier *Person.java*.

1. Créez un nouveau fichier java intitulé *Relation.java* dans le répertoire *domain*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.Edge;
   import com.microsoft.spring.data.gremlin.annotation.EdgeFrom;
   import com.microsoft.spring.data.gremlin.annotation.EdgeTo;
   import lombok.AllArgsConstructor;
   import lombok.Data;
   import lombok.NoArgsConstructor;
   import org.springframework.data.annotation.Id;
   
   @Data
   @Edge
   @AllArgsConstructor
   @NoArgsConstructor
   public class Relation {
   
       @Id
       private String id;
   
       private String name;
   
       @EdgeFrom
       private Person personFrom;
   
       @EdgeTo
       private Person personTo;
   }
   ```

1. Enregistrez et fermez le fichier *Relation.java*.

1. Créez un fichier intitulé *Network.java* dans le répertoire *domain*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.domain;
   
   import com.microsoft.spring.data.gremlin.annotation.EdgeSet;
   import com.microsoft.spring.data.gremlin.annotation.Graph;
   import com.microsoft.spring.data.gremlin.annotation.VertexSet;
   import lombok.Getter;
   import org.springframework.data.annotation.Id;
   
   import java.util.ArrayList;
   import java.util.List;
   
   @Graph
   public class Network {
   
       @Id
       private String id;
   
       public Network() {
           this.edges = new ArrayList<Object>();
           this.vertexes = new ArrayList<Object>();
       }
   
       @EdgeSet
       @Getter
       private List<Object> edges;
   
       @VertexSet
       @Getter
       private List<Object> vertexes;
   }
   ```

1. Enregistrez et fermez le fichier *Network.java*.

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a>Établir un ensemble de classes qui définit les référentiels de votre base de données de graphiques

1. Créez un dossier intitulé *repository* sous le répertoire du package de votre application, par exemple :

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. Créez un fichier java intitulé *NetworkRepository.java* dans le répertoire *repository*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. Enregistrez et fermez le fichier *NetworkRepository.java*.

1. Créez un fichier java intitulé *PersonRepository.java* dans le répertoire *repository*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. Enregistrez et fermez le fichier *PersonRepository.java*.

1. Créez un fichier java intitulé *RelationRepository.java* dans le répertoire *repository*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. Enregistrez et fermez le fichier *RelationRepository.java*.

## <a name="build-and-test-your-app"></a>Générer et tester votre application

1. Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :

   `cd C:\SpringBoot\wingtiptoysdata`

   -ou-

   `cd /users/example/home/wingtiptoysdata`

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Votre application affichera plusieurs messages CLR, et s’il n’y a pas d’erreurs, vous pouvez utiliser le Portail Azure pour consulter le contenu de votre base de données Azure Cosmos. Pour ce faire, cliquez sur **Explorateur de données** sur la page des propriétés pour votre base de données, cliquez sur **Exécuter requête Gremlin**, puis sélectionnez un élément dans la liste des résultats pour afficher les données.

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur la prise en charge Azure pour Gremlin et l’API Graph, voir les articles suivants :

* [Présentation de la base de données Azure Cosmos : API Graph](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [Prise en charge des graphes Azure Cosmos DB Gremlin](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [Azure Cosmos DB : créer une base de données de graphiques à l’aide de Java et du Portail Azure](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [Tutoriel : interroger Azure Cosmos DB à l’aide de l’API Graph et de Gremlin](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* [Starter Spring Data Gremlin]

Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :

* [Documentation Azure Cosmos DB]

* [Azure Cosmos DB : créer une base de données de documents à l’aide de Java et du Portail Azure][Build a SQL API app with Java]

* [Spring Data pour l’API SQL Azure Cosmos DB]

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].

**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes. Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>. En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.


<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data pour l’API SQL Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Starter Spring Data Gremlin]: https://github.com/Microsoft/spring-data-gremlin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ05.png
[AZ06]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ06.png
[AZ07]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ07.png
[AZ08]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/AZ08.png

[SI01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-data-gremlin-java-app-with-cosmos-db/JV03.png
