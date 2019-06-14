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
ms.date: 12/19/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: f00afbdd09ce617f863ed758f4bdddcb40701e27
ms.sourcegitcommit: 5bbf64121a99019207ed8cca29280fc5183c7314
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/12/2019
ms.locfileid: "66840838"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="eab58-103">Comment utiliser Spring Boot Starter avec une API SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eab58-103">How to use the Spring Boot Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="eab58-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="eab58-104">Overview</span></span>

<span data-ttu-id="eab58-105">Azure Cosmos DB est un service de base de données distribué à l’échelle globale, qui permet aux développeurs de travailler sur des données à l’aide d’une série d’API standard, telles que SQL, MongoDB, Graph et Table.</span><span class="sxs-lookup"><span data-stu-id="eab58-105">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as SQL, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="eab58-106">La solution Spring Boot Starter de Microsoft permet aux développeurs d’utiliser des applications Spring Boot qui s’intègrent facilement avec Azure Cosmos DB à l’aide de l’API SQL.</span><span class="sxs-lookup"><span data-stu-id="eab58-106">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using the SQL API.</span></span>

<span data-ttu-id="eab58-107">Cet article illustre la création d’une base de données Azure Cosmos DB à l’aide du Portail Azure, puis l’utilisation de **[Spring Initializr]** pour créer une application Spring Boot personnalisée et ajouter la fonctionnalité [Spring Boot Cosmos DB Starter pour Azure] à votre application personnalisée afin de pouvoir stocker et récupérer des données dans votre base de données Azure Cosmos DB à l’aide de Spring Data et de l’API SQL Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eab58-107">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **[Spring Initializr]** to create a custom Spring Boot application, and then add the [Spring Boot Cosmos DB Starter for Azure] to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Spring Data and the Cosmos DB SQL API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eab58-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="eab58-108">Prerequisites</span></span>

<span data-ttu-id="eab58-109">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="eab58-109">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="eab58-110">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="eab58-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="eab58-111">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="eab58-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="eab58-112">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="eab58-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="eab58-113">Créer une base de données Azure Cosmos DB à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="eab58-113">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="eab58-114">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+ Créer une ressource**.</span><span class="sxs-lookup"><span data-stu-id="eab58-114">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="eab58-116">Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="eab58-116">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="eab58-118">Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="eab58-118">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="eab58-119">Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="eab58-119">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="eab58-120">Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="eab58-120">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="eab58-121">Entrez un **nom de compte** unique que vous allez utiliser en tant qu’URI de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="eab58-121">Enter a unique **Account Name**, which you will use as the URI for your database.</span></span> <span data-ttu-id="eab58-122">Par exemple : *wingtiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="eab58-122">For example: *wingtiptoysdata*.</span></span>
   * <span data-ttu-id="eab58-123">Choisissez **Core (SQL)** pour l’API.</span><span class="sxs-lookup"><span data-stu-id="eab58-123">Choose **Core (SQL)** for the API.</span></span>
   * <span data-ttu-id="eab58-124">Spécifiez l’**Emplacement** pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="eab58-124">Specify the **Location** for your database.</span></span>

   <span data-ttu-id="eab58-125">Une fois que vous avez défini ces options, cliquez sur **Vérifier + créer** pour créer votre base de données.</span><span class="sxs-lookup"><span data-stu-id="eab58-125">When you have specified these options, click **Review + create** to create your database.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="eab58-127">Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="eab58-127">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="eab58-128">Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="eab58-128">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="eab58-130">Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="eab58-130">When the properties page for your database is displayed, click **Keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Portail Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="eab58-132">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="eab58-132">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="eab58-133">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="eab58-133">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="eab58-134">Indiquez que vous souhaitez générer un **projet Maven** avec **Java**, indiquez votre version de **Spring Boot**, entrez les noms de **groupe** et d’**artefact** pour votre application, ajoutez **Support Azure** dans les dépendances, puis cliquez sur le bouton pour **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="eab58-134">Specify that you want to generate a **Maven Project** with **Java**, specify your **Spring Boot** version, enter the **Group** and **Artifact** names for your application, add **Azure Support** in the dependencies, and then click the button to **Generate Project**.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="eab58-136">Spring Initializr utilise les noms de **groupe** et d’**artefact** pour créer le nom du package. Par exemple : *com.example.wintiptoysdata*.</span><span class="sxs-lookup"><span data-stu-id="eab58-136">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoysdata*.</span></span>
   >

1. <span data-ttu-id="eab58-137">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local et décompressez les fichiers.</span><span class="sxs-lookup"><span data-stu-id="eab58-137">When prompted, download the project to a path on your local computer and extract the files.</span></span>

   ![Décompresser le projet Spring Boot personnalisé][SI02]

1. <span data-ttu-id="eab58-139">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="eab58-139">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-application-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="eab58-141">Configurer votre application Spring Boot pour utiliser Azure Spring Boot Starter</span><span class="sxs-lookup"><span data-stu-id="eab58-141">Configure your Spring Boot application to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="eab58-142">Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-142">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="eab58-143">-ou-</span><span class="sxs-lookup"><span data-stu-id="eab58-143">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. <span data-ttu-id="eab58-145">Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez les lignes suivantes à la liste `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="eab58-145">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-cosmosdb-spring-boot-starter</artifactId>
   </dependency>
   ```

   ![Modification du fichier pom.xml][PM02]

1. <span data-ttu-id="eab58-147">Vérifiez que la version de Spring Boot est la version que vous avez choisie lorsque vous avez créé votre application avec Spring Initializr ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-147">Verify that the Spring Boot version is the version that you chose when you created your application with the Spring Initializr; for example:</span></span>

   ```xml
   <parent>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-parent</artifactId>
      <version>2.1.5.RELEASE</version>
      <relativePath/>
   </parent>
   ```

1. <span data-ttu-id="eab58-148">Vérifiez que vous utilisez la version [Azure Spring Boot starters](https://github.com/microsoft/azure-spring-boot) la plus récente, par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-148">Verify that you use the most recent [Azure Spring Boot starters](https://github.com/microsoft/azure-spring-boot) version, for example:</span></span>

   ```xml
   <azure.version>2.1.6</azure.version>
   ```

1. <span data-ttu-id="eab58-149">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="eab58-149">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-application-to-use-your-azure-cosmos-db"></a><span data-ttu-id="eab58-150">Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eab58-150">Configure your Spring Boot application to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="eab58-151">Localisez le fichier *application.properties* dans le répertoire *resources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-151">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.properties`

   <span data-ttu-id="eab58-152">-ou-</span><span class="sxs-lookup"><span data-stu-id="eab58-152">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.properties`

   ![Localiser le fichier application.properties][RE01]

1. <span data-ttu-id="eab58-154">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="eab58-154">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.cosmosdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.cosmosdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.cosmosdb.database=wingtiptoysdata
   ```

   ![Modification du fichier application.properties][RE02]

1. <span data-ttu-id="eab58-156">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="eab58-156">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="eab58-157">Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données</span><span class="sxs-lookup"><span data-stu-id="eab58-157">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="eab58-158">Dans cette section, vous allez créer deux classes Java pour le stockage des données utilisateur, puis modifier votre classe d’application principale pour créer une instance de la classe *Utilisateur* et l’enregistrer dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="eab58-158">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the *User* class and save it to your database.</span></span>

### <a name="define-a-base-class-for-storing-user-data"></a><span data-ttu-id="eab58-159">Définir une classe de base pour le stockage des données utilisateur</span><span class="sxs-lookup"><span data-stu-id="eab58-159">Define a base class for storing user data</span></span>

1. <span data-ttu-id="eab58-160">Créez un fichier nommé *User.java* dans le même répertoire que celui du fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="eab58-160">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="eab58-161">Ouvrez le fichier *User.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une classe d’utilisateur générique qui stocke et récupère des valeurs dans votre base de données :</span><span class="sxs-lookup"><span data-stu-id="eab58-161">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="eab58-162">Enregistrez et fermez le fichier *User.java*.</span><span class="sxs-lookup"><span data-stu-id="eab58-162">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="eab58-163">Définir une interface de référentiel de données</span><span class="sxs-lookup"><span data-stu-id="eab58-163">Define a data repository interface</span></span>

1. <span data-ttu-id="eab58-164">Créez un fichier nommé *UserRepository.java* dans le même répertoire que le fichier Java principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="eab58-164">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="eab58-165">Ouvrez le fichier *UserRepository.java* dans un éditeur de texte, puis ajoutez-y les lignes suivantes pour définir une interface de référentiel utilisateur qui étend l’interface du référentiel de DocumentDB par défaut :</span><span class="sxs-lookup"><span data-stu-id="eab58-165">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoysdata;

   import com.microsoft.azure.spring.data.cosmosdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> { }
   ```

1. <span data-ttu-id="eab58-166">Enregistrez et fermez le fichier *UserRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="eab58-166">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="eab58-167">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="eab58-167">Modify the main application class</span></span>

1. <span data-ttu-id="eab58-168">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application, par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-168">Locate the main application Java file in the package directory of your application, for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="eab58-169">-ou-</span><span class="sxs-lookup"><span data-stu-id="eab58-169">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localiser le fichier Java de l’application][JV01]

1. <span data-ttu-id="eab58-171">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="eab58-171">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
    package com.example.wingtiptoysdata;

    import org.springframework.boot.CommandLineRunner;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    import java.util.Optional;
    import java.util.UUID;

    @SpringBootApplication
    public class WingtiptoysdataApplication implements CommandLineRunner {

        private final UserRepository repository;

        public WingtiptoysdataApplication(UserRepository repository) {
            this.repository = repository;
        }

        public static void main(String[] args) {
            // Execute the command line runner.
            SpringApplication.run(WingtiptoysdataApplication.class, args);
            System.exit(0);
        }

        public void run(String... args) throws Exception {
            // Create a unique identifier.
            String uuid = UUID.randomUUID().toString();

            // Create a new User class.
            final User testUser = new User(uuid, "John", "Doe");

            // For this example, remove all of the existing records.
            repository.deleteAll();

            // Save the User class to the Azure database.
            repository.save(testUser);

            // Retrieve the database record for the User class you just saved by ID.
            Optional<User> result = repository.findById(testUser.getId());

            // Display the results of the database record retrieval.
            System.out.println("\nSaved user is: " + result + "\n")
        }
    }
   ```

1. <span data-ttu-id="eab58-172">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="eab58-172">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="eab58-173">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="eab58-173">Build and test your app</span></span>

1. <span data-ttu-id="eab58-174">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-174">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="eab58-175">-ou-</span><span class="sxs-lookup"><span data-stu-id="eab58-175">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="eab58-176">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="eab58-176">Build your Spring Boot application with Maven and run it, for example:</span></span>

   ```shell
   mvnw clean spring-boot:run
   ```

1. <span data-ttu-id="eab58-177">Votre application affiche plusieurs messages d’exécution, et affichera un message comme les exemples ci dessous indiquant que les valeurs ont été stockées et récupérées avec succès dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="eab58-177">Your application will display several runtime messages, and it will display a message like the following examples to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ```shell
   Saved user is: Optional[User: 24093cb5-55fe-4d2c-b459-cb8bafdd39fe John Doe]
   ```

   ![Sortie réussie de l’application][JV02]

1. <span data-ttu-id="eab58-179">FACULTATIF : vous pouvez utiliser le portail Azure pour afficher le contenu d’Azure Cosmos DB à partir de la page des propriétés de votre base de données en cliquant sur **Explorateur de données**, puis en sélectionnant un élément dans la liste pour afficher le contenu.</span><span class="sxs-lookup"><span data-stu-id="eab58-179">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Data Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a><span data-ttu-id="eab58-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eab58-181">Next steps</span></span>

<span data-ttu-id="eab58-182">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="eab58-182">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eab58-183">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="eab58-183">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="eab58-184">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="eab58-184">Additional Resources</span></span>

<span data-ttu-id="eab58-185">Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="eab58-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="eab58-186">[Documentation Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="eab58-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="eab58-187">[Azure Cosmos DB : créer une base de données de documents à l’aide de Java et du portail Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="eab58-187">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="eab58-188">[Spring Data pour l’API SQL Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="eab58-188">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="eab58-189">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="eab58-189">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* <span data-ttu-id="eab58-190">[Spring Boot Cosmos DB Starter pour Azure]</span><span class="sxs-lookup"><span data-stu-id="eab58-190">[Spring Boot Cosmos DB Starter for Azure]</span></span>

* [<span data-ttu-id="eab58-191">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="eab58-191">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="eab58-192">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="eab58-192">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="eab58-193">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="eab58-193">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="eab58-194">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="eab58-194">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="eab58-195">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="eab58-195">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="eab58-196">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="eab58-196">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="eab58-197">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="eab58-197">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Build a SQL API app with Java]: /azure/cosmos-db/create-sql-api-java 
[Spring Data pour l’API SQL Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Boot Cosmos DB Starter pour Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[Spring Boot Cosmos DB Starter for Azure]: https://github.com/microsoft/azure-spring-boot/tree/master/azure-spring-boot-starters/azure-cosmosdb-spring-boot-starter
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: https://azure.microsoft.com/services/devops/java/
[Working with Azure DevOps and Java]: https://azure.microsoft.com/services/devops/java/
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
