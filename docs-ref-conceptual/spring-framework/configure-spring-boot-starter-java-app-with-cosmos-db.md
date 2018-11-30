---
title: Comment utiliser Spring Boot Starter avec une API SQL Azure Cosmos DB
description: Découvrez comment configurer une application créée avec Spring Boot Initializer à l’aide de l’API SQL Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 6675b3f76f19ec0bfdb28351681258b8c4792104
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339103"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a>Comment utiliser Spring Boot Starter avec une API SQL Azure Cosmos DB

## <a name="overview"></a>Vue d’ensemble

Azure Cosmos DB est un service de base de données distribué à l’échelle globale, qui permet aux développeurs de travailler sur des données à l’aide d’une série d’API standard, telles que SQL, MongoDB, Graph et Table. La solution Spring Boot Starter de Microsoft permet aux développeurs d’utiliser des applications Spring Boot qui s’intègrent facilement avec Azure Cosmos DB à l’aide de l’API SQL.

Cet article illustre la création d’une base de données Azure Cosmos DB à l’aide du Portail Azure, puis l’utilisation de **[Spring Initializr]** pour créer une application java personnalisée et ajouter la fonctionnalité Spring Boot Starter à votre application personnalisée afin de pouvoir stocker et récupérer des données dans votre base de données Azure Cosmos DB à l’aide de l’API SQL.

## <a name="prerequisites"></a>Prérequis

Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a>Créer une base de données Azure Cosmos DB à l’aide du portail Azure

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+ Créer une ressource**.

   ![Portail Azure][AZ01]

1. Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.

   ![Portail Azure][AZ02]

1. Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :

   * Entrez un **ID** unique que vous allez utiliser en tant qu’URI de votre base de données. Par exemple : *wingtiptoysdata.documents.azure.com*.
   * Choisissez **SQL** pour l’API.
   * Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.
   * Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.
   * Spécifiez l’**Emplacement** pour votre base de données.
   
   Une fois ces options définies, cliquez sur **Créer** pour créer votre base de données.

   ![Portail Azure][AZ03]

1. Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**. Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.

   ![Portail Azure][AZ04]

1. Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés d’accès**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Créer une application Spring Boot simple avec Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Spécifiez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms du **groupe** et de l’**artefact** de votre application, spécifiez votre version de **Spring Boot**, puis cliquez sur le bouton **Générer le projet**.

   > [!IMPORTANT]
   >
   > Il y a eu plusieurs changements cassants dans la version 2.0.n de l’application Spring Boot, qui seront utilisés pour compléter les étapes de cet article. Vous pouvez toujours utiliser l’une des versions 1.5.n de l’application Spring Boot pour compléter pas à pas ce didacticiel, les différences seront mises en évidence si nécessaire.
   >

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr utilise les noms de **groupe** et d’**artefact** pour créer le nom du package. Par exemple : *com.example.wintiptoysdata*.
   >

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a>Configurer votre application Spring Boot pour utiliser Azure Spring Boot Starter

1. Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   -ou-

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez les lignes suivantes à la liste `<dependencies>` :

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>2.0.4</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml][PM02]

   > [!IMPORTANT]
   >
   > Si vous utilisez l’une des versions 1.5.n de l’application Spring Boot pour compléter ce didacticiel, vous devrez spécifier l’ancienne version du démarreur Azure Cosmos DB ; par exemple :
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. Vérifiez que la version de Spring Boot est la version que vous avez choisie lorsque vous avez créé votre application avec Spring Initializr ; par exemple :

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.0.1.RELEASE</version>
      <relativePath/>
   </parent>
   ```

   > [!NOTE]
   >
   > Si vous utilisez l’une des versions de 1.5.n de l’application Spring Boot pour compléter ce didacticiel, vous devrez vérifier que c’est la bonne version ; par exemple : `<version>1.5.14.RELEASE</version>`.
   >

1. Enregistrez et fermez le fichier *pom.xml*.

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a>Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB

1. Localisez le fichier *application.properties* dans le répertoire *resources* de votre application. Par exemple :

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   -ou-

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Localiser le fichier application.properties][RE01]

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties][RE02]

1. Enregistrez et fermez le fichier *application.properties*.

## <a name="add-sample-code-to-implement-basic-database-functionality"></a>Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données

Dans cette section, vous allez créer deux classes Java pour le stockage des données utilisateur, et vous modifiez votre classe d’application principale pour créer une instance de la classe d’utilisateur et l’enregistrer dans votre base de données.

### <a name="define-a-basic-class-for-storing-user-data"></a>Définir une classe de base pour le stockage des données utilisateur

1. Créez un fichier nommé *User.java* dans le même répertoire que celui du fichier Java principal de votre application.

1. Ouvrez le fichier *User.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une classe d’utilisateur générique qui stocke et récupère des valeurs dans votre base de données :

   ```java
   package com.example.wingtiptoysdata;

   // Define a generic User class.
   public class User {
      private String id;
      private String firstName;
      private String lastName;
   
      public User() {
      }
   
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }
   
      public void setId(String id) {
         this.id = id;
      }
   
      public String getFirstName() {
         return firstName;
      }
   
      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }
   
      public String getLastName() {
         return lastName;
      }
   
      public void setLastName(String lastName) {
         this.lastName = lastName;
      }
   
      @Override
      public String toString() {
         return String.format("User: %s %s %s", id, firstName, lastName);
      }
   }
   ```

1. Enregistrez et fermez le fichier *User.java*.

### <a name="define-a-data-repository-interface"></a>Définir une interface de référentiel de données

1. Créez un fichier nommé *UserRepository.java* dans le même répertoire que le fichier Java principal de votre application.

1. Ouvrez le fichier *UserRepository.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une interface de référentiel utilisateur qui étend l’interface du référentiel de DocumentDB par défaut :

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. Enregistrez et fermez le fichier *UserRepository.java*.

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
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   // These imports are only used to create an ID for this example.
   import java.util.Date;
   import java.text.SimpleDateFormat;

   @SpringBootApplication
   public class wingtiptoysdataApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;

      public static void main(String[] args) {
         // Execute the command line runner.
         SpringApplication.run(wingtiptoysdataApplication.class, args);
         System.exit(0);
      }

      public void run(String... args) throws Exception {
         // Create a simple date/time ID.
         SimpleDateFormat userId = new SimpleDateFormat("yyyyMMddHHmmssSSS");
         Date currentDate = new Date();

         // Create a new User class.
         final User testUser = new User(userId.format(currentDate), "Gena", "Soto");

         // For this example, remove all of the existing records.
         repository.deleteAll();

         // Save the User class to the Azure database.
         repository.save(testUser);
      
         // Retrieve the database record for the User class you just saved by ID.
         // final User result = repository.findOne(testUser.getId());
         final User result = repository.findById(testUser.getId()).get();

         // Display the results of the database record retrieval.
         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

   > [!IMPORTANT]
   >
   > Si vous utilisez l’une des versions de 1.5.n de l’application Spring Boot pour compléter ce didacticiel, vous devrez remplacer la syntaxe `final User result = repository.findById(testUser.getId()).get();` par `final User result = repository.findOne(testUser.getId());`.
   >

1. Enregistrez et fermez le fichier Java principal de l’application.

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

1. Votre application affiche plusieurs messages d’exécution, et affichera un message comme les exemples ci dessous indiquant que les valeurs ont été stockées et récupérées avec succès dans votre base de données.

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Sortie réussie de l’application][JV02]

1. FACULTATIF : Vous pouvez utiliser le portail Azure pour afficher le contenu d’Azure Cosmos DB à partir de la page des propriétés de votre base de données en cliquant sur **Explorateur de données** puis en sélectionnant un élément dans la liste pour afficher les contenus.

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :

* [Documentation Azure Cosmos DB]

* [Azure Cosmos DB : créer une base de données de documents à l’aide de Java et du Portail Azure][Build a SQL API app with Java]

* [Spring Data pour l’API SQL Azure Cosmos DB]

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Document DB Spring Boot Starter pour Azure]

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].

**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes. Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>. En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.

<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data pour l’API SQL Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Document DB Spring Boot Starter pour Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ01.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ02.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ03.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ04.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/AZ05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/SI03.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE01.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/RE02.png

[PM01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM01.png
[PM02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/PM02.png

[JV01]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV01.png
[JV02]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV02.png
[JV03]: ./media/configure-spring-boot-starter-java-app-with-cosmos-db/JV03.png
