---
title: Comment utiliser Spring Boot Starter avec une API Azure Cosmos DB DocumentDB
description: "Découvrez comment configurer une application créée avec Spring Boot Initializer à l’aide de l’API Azure Cosmos DB DocumentDB."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: 06553920aebb5f27e4d02279e7024d6766e0be94
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="89b41-103">Comment utiliser Spring Boot Starter avec une API Azure Cosmos DB DocumentDB</span><span class="sxs-lookup"><span data-stu-id="89b41-103">How to use the Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="89b41-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="89b41-104">Overview</span></span>

<span data-ttu-id="89b41-105">Azure Cosmos DB est un service de base de données distribué à l’échelle globale, qui permet aux développeurs de travailler sur des données à l’aide d’une série d’API standard, telles que DocumentDB, MongoDB, Graph et Table.</span><span class="sxs-lookup"><span data-stu-id="89b41-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="89b41-106">La solution Spring Boot Starter de Microsoft permet aux développeurs d’utiliser des applications Spring Boot qui s’intègrent facilement avec Azure Cosmos DB à l’aide d’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="89b41-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="89b41-107">Cet article illustre la création d’une base de données Azure Cosmos DB à l’aide du portail Azure, puis l’utilisation de **[Spring Initializr]** pour créer une application java personnalisée et ajouter la fonctionnalité Spring Boot Starter à votre application personnalisée afin de pouvoir stocker et récupérer des données dans votre base de données Azure Cosmos DB à l’aide de l’API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="89b41-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89b41-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89b41-108">Prerequisites</span></span>

<span data-ttu-id="89b41-109">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89b41-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="89b41-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="89b41-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="89b41-111">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="89b41-111">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="89b41-112">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="89b41-112">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="89b41-113">Créer une base de données Azure Cosmos DB à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="89b41-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="89b41-114">Accédez au portail Azure à l’adresse <https://portal.azure.com/>, puis cliquez sur **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="89b41-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="89b41-116">Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="89b41-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="89b41-118">Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="89b41-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="89b41-119">Entrez un **ID** unique que vous allez utiliser en tant qu’URI de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="89b41-119">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="89b41-120">Par exemple : *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="89b41-120">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="89b41-121">Choisissez **SQL (Document DB)** pour l’API.</span><span class="sxs-lookup"><span data-stu-id="89b41-121">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="89b41-122">Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="89b41-122">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="89b41-123">Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="89b41-123">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="89b41-124">Spécifiez l’**Emplacement** pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="89b41-124">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="89b41-125">Une fois ces options définies, cliquez sur **Créer** pour créer votre base de données.</span><span class="sxs-lookup"><span data-stu-id="89b41-125">When you have specified these options, click **Create** to create your database.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="89b41-127">Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="89b41-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="89b41-128">Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="89b41-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="89b41-130">Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés d’accès**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="89b41-130">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="89b41-132">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="89b41-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="89b41-133">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="89b41-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="89b41-134">Spécifiez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le bouton **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="89b41-134">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="89b41-136">Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="89b41-136">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="89b41-137">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="89b41-137">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. <span data-ttu-id="89b41-139">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="89b41-139">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="89b41-141">Configurer votre application Spring Boot pour utiliser Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="89b41-141">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="89b41-142">Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89b41-142">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="89b41-143">-ou-</span><span class="sxs-lookup"><span data-stu-id="89b41-143">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. <span data-ttu-id="89b41-145">Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez les lignes suivantes à la liste `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="89b41-145">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml][PM02]

1. <span data-ttu-id="89b41-147">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="89b41-147">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="89b41-148">Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="89b41-148">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="89b41-149">Localisez le fichier *application.properties* dans le répertoire *resources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89b41-149">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="89b41-150">-ou-</span><span class="sxs-lookup"><span data-stu-id="89b41-150">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Localiser le fichier application.properties][RE01]

1. <span data-ttu-id="89b41-152">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="89b41-152">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties][RE02]

1. <span data-ttu-id="89b41-154">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="89b41-154">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="89b41-155">Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données</span><span class="sxs-lookup"><span data-stu-id="89b41-155">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="89b41-156">Dans cette section, vous allez créer deux classes Java pour le stockage des données utilisateur, et vous modifiez votre classe d’application principale pour créer une instance de la classe d’utilisateur et l’enregistrer dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="89b41-156">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="89b41-157">Définir une classe de base pour le stockage des données utilisateur</span><span class="sxs-lookup"><span data-stu-id="89b41-157">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="89b41-158">Créez un fichier nommé *User.java* dans le même répertoire que celui du fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="89b41-158">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="89b41-159">Ouvrez le fichier *User.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une classe d’utilisateur générique qui stocke et récupère des valeurs dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="89b41-159">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="89b41-160">Enregistrez et fermez le fichier *User.java*.</span><span class="sxs-lookup"><span data-stu-id="89b41-160">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="89b41-161">Définir une interface de référentiel de données</span><span class="sxs-lookup"><span data-stu-id="89b41-161">Define a data repository interface</span></span>

1. <span data-ttu-id="89b41-162">Créez un fichier nommé *UserRepository.java* dans le même répertoire que le fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="89b41-162">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="89b41-163">Ouvrez le fichier *UserRepository.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une interface de référentiel utilisateur qui étend l’interface du référentiel de DocumentDB par défaut :</span><span class="sxs-lookup"><span data-stu-id="89b41-163">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="89b41-164">Enregistrez et fermez le fichier *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="89b41-164">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="89b41-165">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="89b41-165">Modify the main application class</span></span>

1. <span data-ttu-id="89b41-166">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89b41-166">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="89b41-167">-ou-</span><span class="sxs-lookup"><span data-stu-id="89b41-167">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Localiser le fichier Java de l’application][JV01]

1. <span data-ttu-id="89b41-169">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="89b41-169">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="89b41-170">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="89b41-170">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="89b41-171">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="89b41-171">Build and test your app</span></span>

1. <span data-ttu-id="89b41-172">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89b41-172">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="89b41-173">-ou-</span><span class="sxs-lookup"><span data-stu-id="89b41-173">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="89b41-174">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="89b41-174">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="89b41-175">Votre application affiche plusieurs messages d’exécution, et vous devriez voir s’afficher le message `User: testFirstName testLastName` indiquant que les valeurs ont été correctement stockées et récupérées dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="89b41-175">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Sortie réussie de l’application][JV02]

1. <span data-ttu-id="89b41-177">FACULTATIF : vous pouvez utiliser le portail Azure pour afficher le contenu de votre base de données Azure Cosmos DB à partir de la page de propriétés de votre base de données, en cliquant sur **Explorateur de documents**, puis en sélectionnant un élément dans la liste pour afficher son contenu.</span><span class="sxs-lookup"><span data-stu-id="89b41-177">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a><span data-ttu-id="89b41-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="89b41-179">Next steps</span></span>

<span data-ttu-id="89b41-180">Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="89b41-180">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="89b41-181">[Documentation Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="89b41-181">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="89b41-182">[Azure Cosmos DB : Créer une application API DocumentDB avec Java et le portail Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="89b41-182">[Azure Cosmos DB: Build a DocumentDB API app with Java and the Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="89b41-183">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="89b41-183">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="89b41-184">Spring Boot DocumenDB Starter pour Azure</span><span class="sxs-lookup"><span data-stu-id="89b41-184">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="89b41-185">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="89b41-185">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="89b41-186">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="89b41-186">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="89b41-187">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="89b41-187">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="89b41-188">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="89b41-188">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="89b41-189">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="89b41-189">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="89b41-190">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="89b41-190">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="89b41-191">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="89b41-191">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
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
