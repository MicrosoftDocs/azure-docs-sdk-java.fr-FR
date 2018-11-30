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
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="b03b0-103">Comment utiliser Spring Boot Starter avec une API SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b03b0-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="b03b0-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="b03b0-104">Overview</span></span>

<span data-ttu-id="b03b0-105">Azure Cosmos DB est un service de base de données distribué à l’échelle globale, qui permet aux développeurs de travailler sur des données à l’aide d’une série d’API standard, telles que SQL, MongoDB, Graph et Table.</span><span class="sxs-lookup"><span data-stu-id="b03b0-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="b03b0-106">La solution Spring Boot Starter de Microsoft permet aux développeurs d’utiliser des applications Spring Boot qui s’intègrent facilement avec Azure Cosmos DB à l’aide de l’API SQL.</span><span class="sxs-lookup"><span data-stu-id="b03b0-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="b03b0-107">Cet article illustre la création d’une base de données Azure Cosmos DB à l’aide du Portail Azure, puis l’utilisation de **[Spring Initializr]** pour créer une application java personnalisée et ajouter la fonctionnalité Spring Boot Starter à votre application personnalisée afin de pouvoir stocker et récupérer des données dans votre base de données Azure Cosmos DB à l’aide de l’API SQL.</span><span class="sxs-lookup"><span data-stu-id="b03b0-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b03b0-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b03b0-108">Prerequisites</span></span>

<span data-ttu-id="b03b0-109">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b03b0-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="b03b0-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="b03b0-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b03b0-111">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b03b0-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="b03b0-112">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="b03b0-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="b03b0-113">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b03b0-113">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="b03b0-114">Créer une base de données Azure Cosmos DB à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b03b0-114">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="b03b0-115">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+ Créer une ressource**.</span><span class="sxs-lookup"><span data-stu-id="b03b0-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="b03b0-117">Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b03b0-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="b03b0-119">Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b03b0-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="b03b0-120">Entrez un **ID** unique que vous allez utiliser en tant qu’URI de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="b03b0-120">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="b03b0-121">Par exemple : *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="b03b0-121">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="b03b0-122">Choisissez **SQL** pour l’API.</span><span class="sxs-lookup"><span data-stu-id="b03b0-122">Choose **SQL** for the API.</span></span>
   * <span data-ttu-id="b03b0-123">Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="b03b0-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="b03b0-124">Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="b03b0-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="b03b0-125">Spécifiez l’**Emplacement** pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="b03b0-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="b03b0-126">Une fois ces options définies, cliquez sur **Créer** pour créer votre base de données.</span><span class="sxs-lookup"><span data-stu-id="b03b0-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="b03b0-128">Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="b03b0-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="b03b0-129">Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="b03b0-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="b03b0-131">Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés d’accès**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="b03b0-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="b03b0-133">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="b03b0-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="b03b0-134">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="b03b0-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="b03b0-135">Spécifiez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms du **groupe** et de l’**artefact** de votre application, spécifiez votre version de **Spring Boot**, puis cliquez sur le bouton **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="b03b0-135">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version, and then click the button to **Generate Project**.</span></span>

   > [!IMPORTANT]
   >
   > <span data-ttu-id="b03b0-136">Il y a eu plusieurs changements cassants dans la version 2.0.n de l’application Spring Boot, qui seront utilisés pour compléter les étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="b03b0-136">There were several breaking changes to the APIs in Spring Boot version 2.0.n, which will be used to complete the steps in this article.</span></span> <span data-ttu-id="b03b0-137">Vous pouvez toujours utiliser l’une des versions 1.5.n de l’application Spring Boot pour compléter pas à pas ce didacticiel, les différences seront mises en évidence si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b03b0-137">You can still use one of the Spring Boot 1.5.n versions to complete the steps in this tutorial, and the differences will be highlighted when necessary.</span></span>
   >

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="b03b0-139">Spring Initializr utilise les noms de **groupe** et d’**artefact** pour créer le nom du package. Par exemple : *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="b03b0-139">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="b03b0-140">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="b03b0-140">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. <span data-ttu-id="b03b0-142">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="b03b0-142">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="b03b0-144">Configurer votre application Spring Boot pour utiliser Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="b03b0-144">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="b03b0-145">Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-145">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="b03b0-146">-ou-</span><span class="sxs-lookup"><span data-stu-id="b03b0-146">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. <span data-ttu-id="b03b0-148">Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez les lignes suivantes à la liste `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="b03b0-148">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

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
   > <span data-ttu-id="b03b0-150">Si vous utilisez l’une des versions 1.5.n de l’application Spring Boot pour compléter ce didacticiel, vous devrez spécifier l’ancienne version du démarreur Azure Cosmos DB ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-150">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to specify the older version of the Azure Cosmos DB starter; for example:</span></span>
   >
   > ```xml
   > <dependency>
   >   <groupId>com.microsoft.azure</groupId>
   >   <artifactId>azure-documentdb-spring-boot-starter</artifactId>
   >   <version>0.1.4</version>
   > </dependency>
   > ```

1. <span data-ttu-id="b03b0-151">Vérifiez que la version de Spring Boot est la version que vous avez choisie lorsque vous avez créé votre application avec Spring Initializr ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-151">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

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
   > <span data-ttu-id="b03b0-152">Si vous utilisez l’une des versions de 1.5.n de l’application Spring Boot pour compléter ce didacticiel, vous devrez vérifier que c’est la bonne version ; par exemple : `<version>1.5.14.RELEASE</version>`.</span><span class="sxs-lookup"><span data-stu-id="b03b0-152">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to verify the correct version; for example: `<version>1.5.14.RELEASE</version>`.</span></span>
   >

1. <span data-ttu-id="b03b0-153">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="b03b0-153">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="b03b0-154">Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b03b0-154">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="b03b0-155">Localisez le fichier *application.properties* dans le répertoire *resources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-155">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="b03b0-156">-ou-</span><span class="sxs-lookup"><span data-stu-id="b03b0-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Localiser le fichier application.properties][RE01]

1. <span data-ttu-id="b03b0-158">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="b03b0-158">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties][RE02]

1. <span data-ttu-id="b03b0-160">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="b03b0-160">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="b03b0-161">Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données</span><span class="sxs-lookup"><span data-stu-id="b03b0-161">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="b03b0-162">Dans cette section, vous allez créer deux classes Java pour le stockage des données utilisateur, et vous modifiez votre classe d’application principale pour créer une instance de la classe d’utilisateur et l’enregistrer dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="b03b0-162">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="b03b0-163">Définir une classe de base pour le stockage des données utilisateur</span><span class="sxs-lookup"><span data-stu-id="b03b0-163">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="b03b0-164">Créez un fichier nommé *User.java* dans le même répertoire que celui du fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="b03b0-164">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="b03b0-165">Ouvrez le fichier *User.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une classe d’utilisateur générique qui stocke et récupère des valeurs dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="b03b0-165">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="b03b0-166">Enregistrez et fermez le fichier *User.java*.</span><span class="sxs-lookup"><span data-stu-id="b03b0-166">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="b03b0-167">Définir une interface de référentiel de données</span><span class="sxs-lookup"><span data-stu-id="b03b0-167">Define a data repository interface</span></span>

1. <span data-ttu-id="b03b0-168">Créez un fichier nommé *UserRepository.java* dans le même répertoire que le fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="b03b0-168">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="b03b0-169">Ouvrez le fichier *UserRepository.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une interface de référentiel utilisateur qui étend l’interface du référentiel de DocumentDB par défaut :</span><span class="sxs-lookup"><span data-stu-id="b03b0-169">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;
   
   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { } 
   ```

1. <span data-ttu-id="b03b0-170">Enregistrez et fermez le fichier *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="b03b0-170">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="b03b0-171">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="b03b0-171">Modify the main application class</span></span>

1. <span data-ttu-id="b03b0-172">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-172">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="b03b0-173">-ou-</span><span class="sxs-lookup"><span data-stu-id="b03b0-173">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localiser le fichier Java de l’application][JV01]

1. <span data-ttu-id="b03b0-175">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b03b0-175">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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
   > <span data-ttu-id="b03b0-176">Si vous utilisez l’une des versions de 1.5.n de l’application Spring Boot pour compléter ce didacticiel, vous devrez remplacer la syntaxe `final User result = repository.findById(testUser.getId()).get();` par `final User result = repository.findOne(testUser.getId());`.</span><span class="sxs-lookup"><span data-stu-id="b03b0-176">If you are using one of Spring Boot 1.5.n versions to complete this tutorial, you will need to replace the `final User result = repository.findById(testUser.getId()).get();` syntax with `final User result = repository.findOne(testUser.getId());`.</span></span>
   >

1. <span data-ttu-id="b03b0-177">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="b03b0-177">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="b03b0-178">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="b03b0-178">Build and test your app</span></span>

1. <span data-ttu-id="b03b0-179">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-179">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="b03b0-180">-ou-</span><span class="sxs-lookup"><span data-stu-id="b03b0-180">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="b03b0-181">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="b03b0-181">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="b03b0-182">Votre application affiche plusieurs messages d’exécution, et affichera un message comme les exemples ci dessous indiquant que les valeurs ont été stockées et récupérées avec succès dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="b03b0-182">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```
   User: 20170724025215132 Gena Soto
   ```

   ![Sortie réussie de l’application][JV02]

1. <span data-ttu-id="b03b0-184">FACULTATIF : Vous pouvez utiliser le portail Azure pour afficher le contenu d’Azure Cosmos DB à partir de la page des propriétés de votre base de données en cliquant sur **Explorateur de données** puis en sélectionnant un élément dans la liste pour afficher les contenus.</span><span class="sxs-lookup"><span data-stu-id="b03b0-184">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a><span data-ttu-id="b03b0-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b03b0-186">Next steps</span></span>

<span data-ttu-id="b03b0-187">Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="b03b0-187">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="b03b0-188">[Documentation Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="b03b0-188">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="b03b0-189">[Azure Cosmos DB : créer une base de données de documents à l’aide de Java et du Portail Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="b03b0-189">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="b03b0-190">[Spring Data pour l’API SQL Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="b03b0-190">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="b03b0-191">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="b03b0-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="b03b0-192">[Document DB Spring Boot Starter pour Azure]</span><span class="sxs-lookup"><span data-stu-id="b03b0-192">[Spring Boot Document DB Starter for Azure]</span></span>

* [<span data-ttu-id="b03b0-193">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b03b0-193">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="b03b0-194">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b03b0-194">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="b03b0-195">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b03b0-195">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="b03b0-196">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="b03b0-196">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="b03b0-197">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="b03b0-197">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="b03b0-198">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="b03b0-198">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="b03b0-199">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="b03b0-199">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data pour l’API SQL Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Document DB Spring Boot Starter pour Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[Spring Boot Document DB Starter for Azure]:https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[Java Tools for Visual Studio Team Services]: https://azure.microsoft.com/services/devops/java/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot]: http://projects.spring.io/spring-boot/
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
