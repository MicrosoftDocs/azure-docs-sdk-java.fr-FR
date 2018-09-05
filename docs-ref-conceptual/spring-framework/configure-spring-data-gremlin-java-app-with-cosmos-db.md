---
title: Comment utiliser Spring Data Gremlin Starter avec l’API SQL Azure Cosmos DB
description: Découvrez comment configurer une application créée avec Spring Boot Initializer à l’aide de l’API SQL Azure Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 08/20/2018
ms.devlang: java
ms.service: cosmos-db
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: data-services
ms.openlocfilehash: 0976f4b0c13ce5c577458f2974f5dce123bf7e59
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43241071"
---
# <a name="how-to-use-the-spring-data-gremlin-starter-with-the-azure-cosmos-db-sql-api"></a><span data-ttu-id="92000-103">Comment utiliser Spring Data Gremlin Starter avec l’API SQL Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92000-103">How to use the Spring Data Gremlin Starter with the Azure Cosmos DB SQL API</span></span>

## <a name="overview"></a><span data-ttu-id="92000-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="92000-104">Overview</span></span>

<span data-ttu-id="92000-105">Le starter Spring Data Gremlin fournit une prise en charge de Spring Data pour le langage de requête Gremlin d’Apache, pouvant être utilisé par les développeurs avec n’importe quelle banque de données compatible avec Gremlin.</span><span class="sxs-lookup"><span data-stu-id="92000-105">The Spring Data Gremlin Starter provides Spring Data support for the Gremlin query language from Apache, which developers can use with any Gremlin-compatible data store.</span></span>

<span data-ttu-id="92000-106">Cet article illustre la création d’une base de données Azure Cosmos à l’aide du Portail Azure pour une utilisation avec l’API Gremlin, l’utilisation de **[Spring Initializr]** pour la création d’une application java personnalisée, et l’ajout de la fonctionnalité Spring Data Gremlin Starter à votre application personnalisée pour le stockage et la récupération des données dans votre base de données Azure Cosmos à l’aide de Gremlin.</span><span class="sxs-lookup"><span data-stu-id="92000-106">This article demonstrates creating an Azure Cosmos DB by using the Azure portal for use with Gremlin API, then using the **[Spring Initializr]** to create a custom java application, and then add the Spring Data Gremlin Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using Gremlin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92000-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="92000-107">Prerequisites</span></span>

<span data-ttu-id="92000-108">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="92000-108">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="92000-109">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="92000-109">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="92000-110">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="92000-110">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="92000-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="92000-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="92000-112">La version 2.0 de Spring Boot ou une version ultérieure est requise pour effectuer les différentes étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="92000-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-cosmos-db-using-the-azure-portal"></a><span data-ttu-id="92000-113">Créer une base de données Azure Cosmos à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="92000-113">Create an Azure Cosmos DB using the Azure portal</span></span>

### <a name="create-your-azure-cosmos-database-for-use-with-gremlin-api"></a><span data-ttu-id="92000-114">Créez votre base de données Cosmos Azure pour une utilisation avec l’API Gremlin</span><span class="sxs-lookup"><span data-stu-id="92000-114">Create your Azure Cosmos Database for use with Gremlin API</span></span>

1. <span data-ttu-id="92000-115">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+ Créer une ressource**.</span><span class="sxs-lookup"><span data-stu-id="92000-115">Browse to the Azure portal at <https://portal.azure.com/> and click **+Create a resource**.</span></span>

   ![Créer une ressource][AZ01]

1. <span data-ttu-id="92000-117">Cliquez sur **Bases de données**, puis sur **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="92000-117">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Créer une base de données Azure Cosmos][AZ02]

1. <span data-ttu-id="92000-119">Sur le panneau **Azure Cosmos DB**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-119">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="92000-120">Entrez un **ID** unique que vous utiliserez en tant q’URI de Gremlin pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="92000-120">Enter a unique **ID**, which you will use as part of the Gremlin URI for your database.</span></span> <span data-ttu-id="92000-121">Par exemple : si vous avez écrit **wingtiptoysdata** pour l’**ID**, l’URI de Gremlin sera alors *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="92000-121">For example: if you entered **wingtiptoysdata** for the **ID**, the Gremlin URI would be *wingtiptoysdata.gremlin.cosmosdb.azure.com*.</span></span>
   * <span data-ttu-id="92000-122">Sélectionnez **Gremlin (Graphique)** pour l’API.</span><span class="sxs-lookup"><span data-stu-id="92000-122">Choose **Gremlin (Graph)** for the API.</span></span>
   * <span data-ttu-id="92000-123">Choisissez l’**Abonnement** vous souhaitez utiliser pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="92000-123">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="92000-124">Spécifiez si vous souhaitez utiliser un **Groupe de ressources** existant ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="92000-124">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="92000-125">Spécifiez l’**Emplacement** pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="92000-125">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="92000-126">Une fois ces options définies, cliquez sur **Créer** pour créer votre base de données.</span><span class="sxs-lookup"><span data-stu-id="92000-126">When you have specified these options, click **Create** to create your database.</span></span>

   ![Spécifiez les options de la base de données Azure Cosmos][AZ03]

1. <span data-ttu-id="92000-128">Une fois créée, la base de données apparaît sur le **Tableau de bord** Azure ainsi que sur les pages **Toutes les ressources** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="92000-128">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="92000-129">Vous pouvez cliquer sur votre base de données à tous ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="92000-129">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Toutes les ressources][AZ04]

1. <span data-ttu-id="92000-131">Lorsque la page des propriétés de votre base de données s’affiche, cliquez sur **Clés d’accès**, puis copiez votre URI et les clés d’accès de votre base de données. Vous allez utiliser ces valeurs dans votre application Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="92000-131">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Clés d’accès][AZ05]

### <a name="add-a-graph-to-your-azure-cosmos-database"></a><span data-ttu-id="92000-133">Ajouter un graphique à votre base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="92000-133">Add a graph to your Azure Cosmos Database</span></span>

1. <span data-ttu-id="92000-134">Cliquez sur **Explorateur de données**, puis sur **Nouveau graphique**.</span><span class="sxs-lookup"><span data-stu-id="92000-134">Click **Data Explorer**, and then click **New Graph**.</span></span>

   ![Nouveau graphique][AZ06]

1. <span data-ttu-id="92000-136">Lorsque la page **Ajouter un graphique** s’affiche, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-136">When the **Add Graph** is displayed, enter the following information:</span></span>

   * <span data-ttu-id="92000-137">Définissez un **ID de base de données** unique pour votre base de données.</span><span class="sxs-lookup"><span data-stu-id="92000-137">Specify a unique **Database id** for your database.</span></span>
   * <span data-ttu-id="92000-138">Définissez un **ID de graphique** unique pour votre graphique.</span><span class="sxs-lookup"><span data-stu-id="92000-138">Specify a unique **Graph id** for your graph.</span></span>
   * <span data-ttu-id="92000-139">Vous pouvez choisir de préciser votre **Capacité de stockage**, ou accepter celle définie par défaut.</span><span class="sxs-lookup"><span data-stu-id="92000-139">You can choose to specify your **Storage capacity**, or you can accept the default.</span></span>
   * <span data-ttu-id="92000-140">Définissez votre **Débit**, et choisissez pour cet exemple 400 unités de requête (RU).</span><span class="sxs-lookup"><span data-stu-id="92000-140">Specify your **Throughout**, and for this example you can choose 400 Request Units (RUs).</span></span>
   
   <span data-ttu-id="92000-141">Une fois que vous avez défini ces options, cliquez sur **OK** pour créer votre graphique.</span><span class="sxs-lookup"><span data-stu-id="92000-141">When you have specified these options, click **OK** to create your graph.</span></span>

   ![Ajouter un graphique][AZ07]

1. <span data-ttu-id="92000-143">Une fois votre graphique créé, vous pouvez utiliser l’**Explorateur de données** pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="92000-143">After your graph has been created, you can use the **Data Explorer** to view it.</span></span>

   ![Affichage des propriétés du graphique][AZ08]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="92000-145">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="92000-145">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="92000-146">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="92000-146">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="92000-147">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms du **Groupe** et de l’**Artefact** de votre application, choisissez une version de **Spring Boot** qui soit la version 2.0 ou ultérieure, puis cliquez sur le bouton **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="92000-147">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, specify your **Spring Boot** version with a version that is equal to or greater than 2.0, and then click **Generate Project**.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="92000-149">Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple : \*com.example.wintiptoysdata.</span><span class="sxs-lookup"><span data-stu-id="92000-149">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: \*com.example.wintiptoysdata.</span></span>
   >

1. <span data-ttu-id="92000-150">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="92000-150">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI02]

1. <span data-ttu-id="92000-152">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="92000-152">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-spring-data-gremlin-starter"></a><span data-ttu-id="92000-154">Configurer votre application Spring Boot pour utiliser le starter Spring Data Gremlin</span><span class="sxs-lookup"><span data-stu-id="92000-154">Configure your Spring Boot app to use the Spring Data Gremlin Starter</span></span>

1. <span data-ttu-id="92000-155">Localisez le fichier *pom.xml* dans le répertoire de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-155">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\pom.xml`

   <span data-ttu-id="92000-156">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-156">-or-</span></span>

   `/users/example/home/wingtiptoysdata/pom.xml`

   ![Localiser le fichier pom.xml][PM01]

1. <span data-ttu-id="92000-158">Ouvrez le fichier *pom.xml* dans un éditeur de texte, puis ajoutez le starter Spring Data Gremlin à la liste de `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="92000-158">Open the *pom.xml* file in a text editor, and add the Spring Data Gremlin Starter to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.spring.data.gremlin</groupId>
      <artifactId>spring-data-gremlin</artifactId>
      <version>2.0.0</version>
   </dependency>
   ```

   ![Modification du fichier pom.xml][PM02]

1. <span data-ttu-id="92000-160">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="92000-160">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="92000-161">Configurer votre application Spring Boot pour utiliser votre base de données Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="92000-161">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="92000-162">Localisez le répertoire des *ressources* de votre application, et créez un nouveau fichier qui s’intitule *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="92000-162">Locate the *resources* directory of your app, and create a new file named *application.yml*.</span></span> <span data-ttu-id="92000-163">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="92000-163">For example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\resources\application.yml`

   <span data-ttu-id="92000-164">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-164">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/resources/application.yml`

   ![Créez le fichier application.yml][RE01]

1.  <span data-ttu-id="92000-166">Ouvrez le fichier *application.yml* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées pour votre base de données :</span><span class="sxs-lookup"><span data-stu-id="92000-166">Open the *application.yml* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   gremlin:
      endpoint: wingtiptoys.gremlin.cosmosdb.azure.com
      port: 443
      username: /dbs/wingtiptoysdb/colls/wingtiptoysgraph
      password: 57686f6120447564652c20426f6220526f636b73==
      telemetryAllowed: false
   ```
   <span data-ttu-id="92000-167">Où :</span><span class="sxs-lookup"><span data-stu-id="92000-167">Where:</span></span>
   | <span data-ttu-id="92000-168">Champ</span><span class="sxs-lookup"><span data-stu-id="92000-168">Field</span></span> | <span data-ttu-id="92000-169">Description</span><span class="sxs-lookup"><span data-stu-id="92000-169">Description</span></span> |
   | ---|---|
   | `endpoint` | <span data-ttu-id="92000-170">Définit l’URI Gremlin pour votre base de données, provenant de l’**ID** que vous avez précisé lors de la création de votre base de données Azure Cosmos précédemment dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="92000-170">Specifies the Gremlin URI for your database, which is derived from the unique **ID** that you specified when you created your Azure Cosmos DB earlier in this tutorial.</span></span> |
   | `port` | <span data-ttu-id="92000-171">Définit le port TCP/IP, qui devrait être **443** pour le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="92000-171">Specifies the TCP/IP port, which should be **443** for HTTPS.</span></span> |
   | `username` | <span data-ttu-id="92000-172">Définit l’**ID de base donnée** et l’**ID de graphique** uniques que vous avez ajoutés dans votre graphique plus tôt dans ce tutoriel ; il doit être entré en respectant la syntaxe suivante : « /dbs/**{Database id}**/colls/**{Graph id}**  ».</span><span class="sxs-lookup"><span data-stu-id="92000-172">Specifies the unique **Database id** and **Graph id** that you used when you added your graph earlier in this tutorial; this must be entered using the following syntax: "/dbs/**{Database id}**/colls/**{Graph id}**".</span></span> |
   | `password` | <span data-ttu-id="92000-173">Définit la **Clé d’accès** primaire ou secondaire que vous avez copiée plus tôt au cours de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="92000-173">Specifies either the primary or secondary **Access key** that you copied earlier in this tutorial.</span></span> |
   | `telemetryAllowed` | <span data-ttu-id="92000-174">Choisissez **vrai** si vous souhaitez autoriser la télémétrie ; dans le cas contraire, choisissez **faux**.</span><span class="sxs-lookup"><span data-stu-id="92000-174">Specify **true** if you want to enable telemetry; otherwise, **false**.</span></span>

1. <span data-ttu-id="92000-175">Enregistrez et fermez le fichier *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="92000-175">Save and close the *application.yml* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="92000-176">Ajouter un exemple de code pour implémenter une fonctionnalité simple de base de données</span><span class="sxs-lookup"><span data-stu-id="92000-176">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="92000-177">Dans cette section, vous pouvez créer les classes Java nécessaires au stockage de données dans votre base de données.</span><span class="sxs-lookup"><span data-stu-id="92000-177">In this section, you create the necessary Java classes for storing data in your database.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="92000-178">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="92000-178">Modify the main application class</span></span>

1. <span data-ttu-id="92000-179">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-179">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\WingtiptoysdataApplication.java`

   <span data-ttu-id="92000-180">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-180">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/WingtiptoysdataApplication.java`

   ![Localiser le fichier Java de l’application][JV01]

1. <span data-ttu-id="92000-182">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-182">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="92000-183">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="92000-183">Save and close the main application Java file.</span></span>

### <a name="define-a-basic-class-for-storing-configuration-information"></a><span data-ttu-id="92000-184">Définir une classe de base pour le stockage d’informations liées à la configuration</span><span class="sxs-lookup"><span data-stu-id="92000-184">Define a basic class for storing configuration information</span></span>

1. <span data-ttu-id="92000-185">Créez un dossier intitulé *config* sous le répertoire du package de votre application, par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-185">Create a folder named *config* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\config`

   <span data-ttu-id="92000-186">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-186">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/config`

1. <span data-ttu-id="92000-187">Créez un fichier java intitulé *UserRepositoryConfiguration.java* dans le répertoire *config*, ouvrez le fichier dans un éditeur de texte, et ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-187">Create a new Java file named *UserRepositoryConfiguration.java* in the *config* directory, then open the file in a text editor, and add the following lines:</span></span>

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

1. <span data-ttu-id="92000-188">Enregistrez et fermez le fichier *UserRepositoryConfiguration.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-188">Save and close the *UserRepositoryConfiguration.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-elements-of-your-graph-database"></a><span data-ttu-id="92000-189">Établir un ensemble de classes qui définit les éléments de votre base de données de graphiques</span><span class="sxs-lookup"><span data-stu-id="92000-189">Define a set of classes that define the elements of your graph database</span></span>

1. <span data-ttu-id="92000-190">Créez un dossier intitulé *domain*sous le répertoire de package de votre application, par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-190">Create a folder named *domain* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\domain`

   <span data-ttu-id="92000-191">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-191">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/domain`

1. <span data-ttu-id="92000-192">Créez un fichier java intitulé *Person.java* dans le répertoire *domain*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-192">Create a new Java file named *Person.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="92000-193">Enregistrez et fermez le fichier *Person.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-193">Save and close the *Person.java* file.</span></span>

1. <span data-ttu-id="92000-194">Créez un nouveau fichier java intitulé *Relation.java* dans le répertoire *domain*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-194">Create a new Java file named *Relation.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="92000-195">Enregistrez et fermez le fichier *Relation.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-195">Save and close the *Relation.java* file.</span></span>

1. <span data-ttu-id="92000-196">Créez un fichier intitulé *Network.java* dans le répertoire *domain*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-196">Create a new Java file named *Network.java* in the *domain* directory, then open the file in a text editor and add the following lines:</span></span>

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

1. <span data-ttu-id="92000-197">Enregistrez et fermez le fichier *Network.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-197">Save and close the *Network.java* file.</span></span>

### <a name="define-a-set-of-classes-that-define-the-repositories-for-your-graph-database"></a><span data-ttu-id="92000-198">Établir un ensemble de classes qui définit les référentiels de votre base de données de graphiques</span><span class="sxs-lookup"><span data-stu-id="92000-198">Define a set of classes that define the repositories for your graph database</span></span>

1. <span data-ttu-id="92000-199">Créez un dossier intitulé *repository* sous le répertoire du package de votre application, par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-199">Create a folder named *repository* under the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoysdata\src\main\java\com\example\wingtiptoysdata\repository`

   <span data-ttu-id="92000-200">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-200">-or-</span></span>

   `/users/example/home/wingtiptoysdata/src/main/java/com/example/wingtiptoysdata/repository`

1. <span data-ttu-id="92000-201">Créez un fichier java intitulé *NetworkRepository.java* dans le répertoire *repository*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-201">Create a new Java file named *NetworkRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Network;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface NetworkRepository extends GremlinRepository<Network, String> {
   }
   ```

1. <span data-ttu-id="92000-202">Enregistrez et fermez le fichier *NetworkRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-202">Save and close the *NetworkRepository.java* file.</span></span>

1. <span data-ttu-id="92000-203">Créez un fichier java intitulé *PersonRepository.java* dans le répertoire *repository*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-203">Create a new Java file named *PersonRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Person;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface PersonRepository extends GremlinRepository<Person, String> {
   }
   ```

1. <span data-ttu-id="92000-204">Enregistrez et fermez le fichier *PersonRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-204">Save and close the *PersonRepository.java* file.</span></span>

1. <span data-ttu-id="92000-205">Créez un fichier java intitulé *RelationRepository.java* dans le répertoire *repository*, puis ouvrez le fichier dans un éditeur de texte et entrez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-205">Create a new Java file named *RelationRepository.java* in the *repository* directory, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.example.wingtiptoysdata.repository;
   
   import com.microsoft.spring.data.gremlin.repository.GremlinRepository;
   import com.example.wingtiptoysdata.domain.Relation;
   import org.springframework.stereotype.Repository;
   
   @Repository
   public interface RelationRepository extends GremlinRepository<Relation, String> {
   }
   ```

1. <span data-ttu-id="92000-206">Enregistrez et fermez le fichier *RelationRepository.java*.</span><span class="sxs-lookup"><span data-stu-id="92000-206">Save and close the *RelationRepository.java* file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="92000-207">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="92000-207">Build and test your app</span></span>

1. <span data-ttu-id="92000-208">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-208">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoysdata`

   <span data-ttu-id="92000-209">-ou-</span><span class="sxs-lookup"><span data-stu-id="92000-209">-or-</span></span>

   `cd /users/example/home/wingtiptoysdata`

1. <span data-ttu-id="92000-210">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="92000-210">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="92000-211">Votre application affichera plusieurs messages CLR, et s’il n’y a pas d’erreurs, vous pouvez utiliser le Portail Azure pour consulter le contenu de votre base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="92000-211">Your application will display several runtime messages, and if there were no errors, you can use the Azure portal to view the contents of your Azure Cosmos DB.</span></span> <span data-ttu-id="92000-212">Pour ce faire, cliquez sur **Explorateur de données** sur la page des propriétés pour votre base de données, cliquez sur **Exécuter requête Gremlin**, puis sélectionnez un élément dans la liste des résultats pour afficher les données.</span><span class="sxs-lookup"><span data-stu-id="92000-212">To do so, click **Data Explorer** on the properties page for your database, then click **Execute Gremlin Query**, and then select an item from the list of results to view the data.</span></span>

   ![Utilisation de l’Explorateur de documents pour afficher vos données][JV03]

## <a name="next-steps"></a><span data-ttu-id="92000-214">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92000-214">Next steps</span></span>

<span data-ttu-id="92000-215">Pour plus d’informations sur la prise en charge Azure pour Gremlin et l’API Graph, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="92000-215">For more information about Azure support for Gremlin and Graph API, see the following articles:</span></span>

* [<span data-ttu-id="92000-216">Présentation de la base de données Azure Cosmos : API Graph</span><span class="sxs-lookup"><span data-stu-id="92000-216">Introduction to Azure Cosmos DB: Graph API</span></span>](https://docs.microsoft.com/azure/cosmos-db/graph-introduction)

* [<span data-ttu-id="92000-217">Prise en charge des graphes Azure Cosmos DB Gremlin</span><span class="sxs-lookup"><span data-stu-id="92000-217">Azure Cosmos DB Gremlin graph support</span></span>](https://docs.microsoft.com/azure/cosmos-db/gremlin-support)

* [<span data-ttu-id="92000-218">Azure Cosmos DB : créer une base de données de graphiques à l’aide de Java et du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="92000-218">Azure Cosmos DB: Create a graph database using Java and the Azure portal</span></span>](https://docs.microsoft.com/azure/cosmos-db/create-graph-java)

* [<span data-ttu-id="92000-219">Tutoriel : interroger Azure Cosmos DB à l’aide de l’API Graph et de Gremlin</span><span class="sxs-lookup"><span data-stu-id="92000-219">Tutorial: Query Azure Cosmos DB Graph API by using Gremlin</span></span>](https://docs.microsoft.com/azure/cosmos-db/tutorial-query-graph)

* <span data-ttu-id="92000-220">[Starter Spring Data Gremlin]</span><span class="sxs-lookup"><span data-stu-id="92000-220">[Spring Data Gremlin Starter]</span></span>

<span data-ttu-id="92000-221">Pour plus d’informations sur l’utilisation d’Azure Cosmos DB et de Java, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="92000-221">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="92000-222">[Documentation Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="92000-222">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="92000-223">[Azure Cosmos DB : créer une base de données de documents à l’aide de Java et du Portail Azure][Build a SQL API app with Java]</span><span class="sxs-lookup"><span data-stu-id="92000-223">[Azure Cosmos DB: Create a document database using Java and the Azure portal][Build a SQL API app with Java]</span></span>

* <span data-ttu-id="92000-224">[Spring Data pour l’API SQL Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="92000-224">[Spring Data for Azure Cosmos DB SQL API]</span></span>

<span data-ttu-id="92000-225">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="92000-225">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="92000-226">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="92000-226">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="92000-227">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="92000-227">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="92000-228">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="92000-228">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="92000-229">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="92000-229">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="92000-230">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="92000-230">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="92000-231">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="92000-231">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="92000-232">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="92000-232">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>


<!-- URL List -->

[Documentation Azure Cosmos DB]: /azure/cosmos-db/
[Azure Cosmos DB Documentation]: /azure/cosmos-db/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Build a SQL API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java 
[Spring Data pour l’API SQL Azure Cosmos DB]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Spring Data for Azure Cosmos DB SQL API]: https://azure.microsoft.com/blog/spring-data-azure-cosmos-db-nosql-data-access-on-azure/
[Starter Spring Data Gremlin]: https://github.com/Microsoft/spring-data-gremlin
[Spring Data Gremlin Starter]: https://github.com/Microsoft/spring-data-gremlin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot]: http://projects.spring.io/spring-boot/
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
