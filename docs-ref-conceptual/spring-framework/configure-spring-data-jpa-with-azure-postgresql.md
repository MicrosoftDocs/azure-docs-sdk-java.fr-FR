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
# <a name="how-to-use-spring-data-jpa-with-azure-postgresql"></a><span data-ttu-id="6c010-103">Comment utiliser Spring Data JPA avec Azure PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6c010-103">How to use Spring Data JPA with Azure PostgreSQL</span></span>

## <a name="overview"></a><span data-ttu-id="6c010-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="6c010-104">Overview</span></span>

<span data-ttu-id="6c010-105">Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations dans une base de données Azure [PostgreSQL]https://www.postgresql.org/ à l’aide de l’[API de persistance Java (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="6c010-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [PostgreSQL]https://www.postgresql.org/ database using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c010-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="6c010-106">Prerequisites</span></span>

<span data-ttu-id="6c010-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6c010-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="6c010-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="6c010-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="6c010-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6c010-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="6c010-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="6c010-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="6c010-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6c010-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="6c010-112">[Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6c010-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span> <span data-ttu-id="6c010-113">ou l’utilitaire HTTP similaire pour tester la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6c010-113">or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="6c010-114">L’utilitaire de ligne de commande [psql](https://www.postgresql.org/docs/current/app-psql.html).</span><span class="sxs-lookup"><span data-stu-id="6c010-114">The [psql](https://www.postgresql.org/docs/current/app-psql.html) command-line utility.</span></span>
* <span data-ttu-id="6c010-115">Un client [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="6c010-115">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-postgresql-database-for-azure"></a><span data-ttu-id="6c010-116">Créer une base de données PostgreSQL pour Azure</span><span class="sxs-lookup"><span data-stu-id="6c010-116">Create a PostgreSQL database for Azure</span></span>

### <a name="create-a-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="6c010-117">Créer un serveur de base de données PostgreSQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="6c010-117">Create a PostgreSQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="6c010-118">Vous trouverez des informations plus détaillées sur la création de bases de données PostgreSQL dans l’article [Création d’un serveur Azure Database pour PostgreSQL à l’aide du portail Azure](/azure/postgresql/quickstart-create-server-database-portal).</span><span class="sxs-lookup"><span data-stu-id="6c010-118">You can read more detailed information about creating PostgreSQL databases in [Create an Azure Database for PostgreSQL server by using the Azure portal](/azure/postgresql/quickstart-create-server-database-portal).</span></span>

1. <span data-ttu-id="6c010-119">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="6c010-119">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6c010-120">Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Database pour PostgreSQL**.</span><span class="sxs-lookup"><span data-stu-id="6c010-120">Click **+Create a resource**, then **Databases**, and then click **Azure Database for PostgreSQL**.</span></span>

   ![Créer une base de données PostgreSQL][POSTGRESQL01]

1. <span data-ttu-id="6c010-122">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6c010-122">Enter the following information:</span></span>

   - <span data-ttu-id="6c010-123">**Nom du serveur** : choisissez un nom unique pour votre serveur PostgreSQL. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoyspostgresql.postgres.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="6c010-123">**Server name**: Choose a unique name for your PostgreSQL server; this will be used to create a fully-qualified domain name like *wingtiptoyspostgresql.postgres.database.azure.com*.</span></span>
   - <span data-ttu-id="6c010-124">**Abonnement**: indiquez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="6c010-124">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="6c010-125">**Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="6c010-125">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="6c010-126">**Sélectionner la source** : pour ce didacticiel, sélectionnez `Blank` pour créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="6c010-126">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="6c010-127">**Connexion d’administrateur du serveur** : spécifiez le nom d’administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="6c010-127">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="6c010-128">**Mot de passe** et **Confirmer le mot de passe** : spécifiez le mot de passe de votre administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="6c010-128">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="6c010-129">**Emplacement** : spécifiez la région géographique le plus proche de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="6c010-129">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="6c010-130">**Version** : spécifiez la version la plus à jour la base de données.</span><span class="sxs-lookup"><span data-stu-id="6c010-130">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="6c010-131">**Niveau tarifaire** : pour ce didacticiel, spécifiez le niveau tarifaire le moins onéreux.</span><span class="sxs-lookup"><span data-stu-id="6c010-131">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Créer les propriétés de la base de données PostgreSQL][POSTGRESQL02]

1. <span data-ttu-id="6c010-133">Après avoir entré toutes les informations ci-dessus, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="6c010-133">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-postgresql-database-server-using-the-azure-portal"></a><span data-ttu-id="6c010-134">Configurer une règle de pare-feu pour votre serveur de bases de données PostgreSQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="6c010-134">Configure a firewall rule for your PostgreSQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="6c010-135">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="6c010-135">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6c010-136">Cliquez sur **Toutes les ressources**, puis sur la base de données PostgreSQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="6c010-136">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Sélectionner votre base de données PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="6c010-138">Cliquez sur **Sécurité de la connexion**, puis, dans **Règles de pare-feu**, créez une règle en spécifiant un nom unique. Ensuite, entrez la plage d’adresses IP qui doivent accéder à votre base de données, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6c010-138">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configurer la sécurité de la connexion][POSTGRESQL04]

### <a name="retrieve-the-connection-string-for-your-postgresql-server-using-the-azure-portal"></a><span data-ttu-id="6c010-140">Récupérer la chaîne de connexion de votre serveur PostgreSQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="6c010-140">Retrieve the connection string for your PostgreSQL server using the Azure Portal</span></span>

1. <span data-ttu-id="6c010-141">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="6c010-141">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="6c010-142">Cliquez sur **Toutes les ressources**, puis sur la base de données PostgreSQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="6c010-142">Click **All Resources**, then click the PostgreSQL database you just created.</span></span>

   ![Sélectionner votre base de données PostgreSQL][POSTGRESQL03]

1. <span data-ttu-id="6c010-144">Cliquez sur **Chaînes de connexion** et copiez la valeur dans le champ de texte **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="6c010-144">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Récupérer votre chaîne de connexion JDBC][POSTGRESQL05]

### <a name="create-postgresql-database-using-the-psql-command-line-utility"></a><span data-ttu-id="6c010-146">Créer la base de données PostgreSQL à l’aide de l’utilitaire de ligne de commande `psql`</span><span class="sxs-lookup"><span data-stu-id="6c010-146">Create PostgreSQL database using the `psql` command-line utility</span></span>

1. <span data-ttu-id="6c010-147">Ouvrez un interpréteur de commandes et connectez-vous à votre serveur PostgreSQL en entrant une commande `psql`, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c010-147">Open a command shell and connect to your PostgreSQL server by entering a `psql` command like the following example:</span></span>

   ```shell
   psql --host=wingtiptoyspostgresql.postgres.database.azure.com --port=5432 --username=wingtiptoysuser@wingtiptoyspostgresql --dbname=postgres
   ```
   <span data-ttu-id="6c010-148">Où :</span><span class="sxs-lookup"><span data-stu-id="6c010-148">Where:</span></span>

   | <span data-ttu-id="6c010-149">Paramètre</span><span class="sxs-lookup"><span data-stu-id="6c010-149">Parameter</span></span> | <span data-ttu-id="6c010-150">Description</span><span class="sxs-lookup"><span data-stu-id="6c010-150">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="6c010-151">Spécifie le nom complet du serveur PostgreSQL mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6c010-151">Specifies your fully qualified PostgreSQL server name from earlier in this article.</span></span> |
   | `host` | <span data-ttu-id="6c010-152">Spécifie le port du serveur PostgreSQL, c’est-à-dire `5432` par défaut.</span><span class="sxs-lookup"><span data-stu-id="6c010-152">Specifies the PostgreSQL server port, which is `5432` by default.</span></span> |
   | `username` | <span data-ttu-id="6c010-153">Spécifie votre administrateur PostgreSQL et le nom abrégé de serveur mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6c010-153">Specifies your PostgreSQL administrator and shortened server name from earlier in this article.</span></span> |
   | `dbname` | <span data-ttu-id="6c010-154">Spécifie que vous souhaitez utiliser la base de données `postgres` par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="6c010-154">Specifies that you want to use the default `postgres` database for now.</span></span> |

   <span data-ttu-id="6c010-155">Votre serveur PostgreSQL doit répondre avec un affichage semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c010-155">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   psql (9.3.24, server 10.5)
   SSL connection (cipher: ECDHE-RSA-AES256-SHA384, bits: 256)
   Type "help" for help.
   
   postgres=>
   ```

1. <span data-ttu-id="6c010-156">Créez une base de données nommée *mypgsqldb* en entrant une commande `psql` comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c010-156">Create a database named *mypgsqldb* by entering a `psql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mypgsqldb;
   ```

   <span data-ttu-id="6c010-157">Votre serveur PostgreSQL doit répondre avec un affichage semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c010-157">Your PostgreSQL server should respond with a display like the following example:</span></span>

   ```shell
   CREATE DATABASE
   ```

1. <span data-ttu-id="6c010-158">FACULTATIF : vous pouvez vérifier la création de votre base de données en entrant `\l` au niveau de `psql`. Votre serveur PostgreSQL doit répondre avec une sortie semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c010-158">OPTIONAL: You can verify that your database was created by entering a `\l` at the `psql`; your PostgreSQL server should respond with something like the following example:</span></span>

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

1. <span data-ttu-id="6c010-159">Entrez `\q` pour quitter l’utilitaire `psql`.</span><span class="sxs-lookup"><span data-stu-id="6c010-159">Enter `\q` to exit the `psql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="6c010-160">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="6c010-160">Configure the sample application</span></span>

1. <span data-ttu-id="6c010-161">Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c010-161">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jpa-on-azure.git
   ```

1. <span data-ttu-id="6c010-162">Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="6c010-162">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="6c010-163">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :</span><span class="sxs-lookup"><span data-stu-id="6c010-163">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:postgresql://wingtiptoyspostgresql.postgres.database.azure.com:5432/mypgsqldb?ssl=true&sslmode=prefer
   spring.datasource.username=wingtiptoysuser@wingtiptoyspostgresql
   spring.datasource.password=********
    ```
   <span data-ttu-id="6c010-164">Où :</span><span class="sxs-lookup"><span data-stu-id="6c010-164">Where:</span></span>

   | <span data-ttu-id="6c010-165">Paramètre</span><span class="sxs-lookup"><span data-stu-id="6c010-165">Parameter</span></span> | <span data-ttu-id="6c010-166">Description</span><span class="sxs-lookup"><span data-stu-id="6c010-166">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="6c010-167">Spécifie votre chaîne JDBC PostgreSQL mentionnée plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6c010-167">Specifies your PostgreSQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="6c010-168">Spécifie le nom de votre administrateur PostgreSQL mentionné plus haut dans cet article, avec le nom abrégé du serveur accolé.</span><span class="sxs-lookup"><span data-stu-id="6c010-168">Specifies your PostgreSQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="6c010-169">Spécifie votre mot de passe administrateur PostgreSQL mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="6c010-169">Specifies your PostgreSQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="6c010-170">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="6c010-170">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="6c010-171">Packager et tester l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="6c010-171">Package and test the sample application</span></span> 

1. <span data-ttu-id="6c010-172">Compilez l’exemple d’application avec Maven :</span><span class="sxs-lookup"><span data-stu-id="6c010-172">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P postgresql
   ```

1. <span data-ttu-id="6c010-173">Démarrez l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="6c010-173">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="6c010-174">Créez des enregistrements à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="6c010-174">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="6c010-175">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c010-175">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="6c010-176">Récupérez tous les enregistrements existants à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="6c010-176">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="6c010-177">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c010-177">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="6c010-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="6c010-178">Summary</span></span>

<span data-ttu-id="6c010-179">Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations dans une base de données Azure PostgreSQL à l’aide de JPA.</span><span class="sxs-lookup"><span data-stu-id="6c010-179">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure PostgreSQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c010-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c010-180">Next steps</span></span>

<span data-ttu-id="6c010-181">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c010-181">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6c010-182">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="6c010-182">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="6c010-183">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6c010-183">Additional Resources</span></span>

<span data-ttu-id="6c010-184">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="6c010-184">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
