---
title: Comment utiliser Spring Boot Starter avec une API Azure Cosmos DB DocumentDB
description: "Découvrez comment configurer une application créée avec Spring Boot Initializer à l’aide de l’API Azure Cosmos DB DocumentDB."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Spring Starter, Cosmos DB, DocumentDB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a80ac6be1064e40cd0b693ac4e6c0b1a9723cfc4
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="ba7d2-104">Comment utiliser Spring Boot Starter avec une API Azure Cosmos DB DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ba7d2-104">How to use the Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="ba7d2-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ba7d2-105">Overview</span></span>

<span data-ttu-id="ba7d2-106">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ba7d2-107">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="ba7d2-108">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="ba7d2-109">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="ba7d2-110">Azure Cosmos DB est un service de base de données distribué à l’échelle globale, qui permet aux développeurs de travailler sur des données à l’aide d’une série d’API standard, telles que DocumentDB, MongoDB, Graph et Table.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-110">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="ba7d2-111">La solution Spring Boot Starter de Microsoft permet aux développeurs d’utiliser des applications Spring Boot qui s’intègrent facilement avec Azure Cosmos DB à l’aide d’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-111">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="ba7d2-112">Cet article illustre la création d’une base de données Azure Cosmos DB à l’aide du portail Azure, puis l’utilisation de **Spring Initializr** pour créer une application java personnalisée et ajouter la fonctionnalité Spring Boot Starter à votre application personnalisée afin de pouvoir stocker et récupérer des données dans votre base de données Azure Cosmos DB à l’aide de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-112">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **Spring Initializr** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba7d2-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ba7d2-113">Prerequisites</span></span>

<span data-ttu-id="ba7d2-114">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-114">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="ba7d2-115">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="ba7d2-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="ba7d2-116">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="ba7d2-117">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="ba7d2-118">Créer une base de données Azure Cosmos DB à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="ba7d2-118">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="ba7d2-119">Accédez au portail Azure à l’adresse <https://portal.azure.com/>, puis cliquez sur **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-119">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="ba7d2-121">Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="ba7d2-123">Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-123">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="ba7d2-124">Entrez un **ID** unique que vous allez utiliser en tant qu’URI de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-124">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="ba7d2-125">Par exemple : *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="ba7d2-126">Choisissez **SQL (Document DB)** pour l’API.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-126">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="ba7d2-127">Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-127">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="ba7d2-128">Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-128">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="ba7d2-129">Spécifiez l’**Emplacement** pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-129">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="ba7d2-130">Une fois ces options définies, cliquez sur **Créer** pour créer votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-130">When you have specified these options, click **Create** to create your database.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="ba7d2-132">Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="ba7d2-133">Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-133">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="ba7d2-135">Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés d’accès**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-135">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="ba7d2-137">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="ba7d2-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="ba7d2-138">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ba7d2-139">Spécifiez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le bouton **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-139">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ba7d2-141">Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="ba7d2-142">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. <span data-ttu-id="ba7d2-144">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="ba7d2-146">Configurer votre application Spring Boot pour utiliser Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="ba7d2-146">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="ba7d2-147">Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-147">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="ba7d2-148">-ou-</span><span class="sxs-lookup"><span data-stu-id="ba7d2-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. <span data-ttu-id="ba7d2-150">Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez les lignes suivantes à la liste `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-150">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml][PM02]

1. <span data-ttu-id="ba7d2-152">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-152">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="ba7d2-153">Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ba7d2-153">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="ba7d2-154">Localisez le fichier *application.properties* dans le répertoire *resources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-154">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="ba7d2-155">-ou-</span><span class="sxs-lookup"><span data-stu-id="ba7d2-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Localiser le fichier application.properties][RE01]

1. <span data-ttu-id="ba7d2-157">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-157">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties][RE02]

1. <span data-ttu-id="ba7d2-159">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-159">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="ba7d2-160">Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données</span><span class="sxs-lookup"><span data-stu-id="ba7d2-160">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="ba7d2-161">Dans cette section, vous allez créer deux classes Java pour le stockage des données utilisateur, et vous modifiez votre classe d’application principale pour créer une instance de la classe d’utilisateur et l’enregistrer dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-161">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="ba7d2-162">Définir une classe de base pour le stockage des données utilisateur</span><span class="sxs-lookup"><span data-stu-id="ba7d2-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="ba7d2-163">Créez un fichier nommé *User.java* dans le même répertoire que celui du fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-163">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="ba7d2-164">Ouvrez le fichier *User.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une classe d’utilisateur générique qui stocke et récupère des valeurs dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-164">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
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
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="ba7d2-165">Enregistrez et fermez le fichier *User.java*.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-165">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="ba7d2-166">Définir une interface de référentiel de données</span><span class="sxs-lookup"><span data-stu-id="ba7d2-166">Define a data repository interface</span></span>

1. <span data-ttu-id="ba7d2-167">Créez un fichier nommé *UserRepository.java* dans le même répertoire que le fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-167">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="ba7d2-168">Ouvrez le fichier *UserRepository.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une interface de référentiel utilisateur qui étend l’interface du référentiel de DocumentDB par défaut :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-168">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="ba7d2-169">Enregistrez et fermez le fichier *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-169">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="ba7d2-170">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="ba7d2-170">Modify the main application class</span></span>

1. <span data-ttu-id="ba7d2-171">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-171">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="ba7d2-172">-ou-</span><span class="sxs-lookup"><span data-stu-id="ba7d2-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Localiser le fichier Java de l’application][JV01]

1. <span data-ttu-id="ba7d2-174">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-174">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="ba7d2-175">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-175">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="ba7d2-176">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="ba7d2-176">Build and test your app</span></span>

1. <span data-ttu-id="ba7d2-177">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-177">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="ba7d2-178">-ou-</span><span class="sxs-lookup"><span data-stu-id="ba7d2-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="ba7d2-179">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="ba7d2-180">Votre application affiche plusieurs messages d’exécution, et vous devriez voir s’afficher le message `User: testFirstName testLastName` indiquant que les valeurs ont été correctement stockées et récupérées dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-180">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Sortie réussie de l’application][JV02]

1. <span data-ttu-id="ba7d2-182">FACULTATIF : vous pouvez utiliser le portail Azure pour afficher le contenu de votre base de données Azure Cosmos DB à partir de la page de propriétés de votre base de données, en cliquant sur **Explorateur de documents**, puis en sélectionnant un élément dans la liste pour afficher son contenu.</span><span class="sxs-lookup"><span data-stu-id="ba7d2-182">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a><span data-ttu-id="ba7d2-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba7d2-184">Next steps</span></span>

<span data-ttu-id="ba7d2-185">Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="ba7d2-186">[Documentation Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="ba7d2-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="ba7d2-187">[Azure Cosmos DB : Créer une application API DocumentDB avec Java et le portail Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="ba7d2-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and the Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="ba7d2-188">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="ba7d2-188">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="ba7d2-189">Spring Boot DocumenDB Starter pour Azure</span><span class="sxs-lookup"><span data-stu-id="ba7d2-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="ba7d2-190">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ba7d2-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="ba7d2-191">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="ba7d2-191">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="ba7d2-192">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ba7d2-192">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
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
