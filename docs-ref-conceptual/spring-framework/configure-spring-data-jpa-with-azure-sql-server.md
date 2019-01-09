---
title: Comment utiliser Spring Data JPA avec Azure SQL Database
description: Découvrez comment utiliser Spring Data JPA avec une base de données SQL Azure.
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
ms.openlocfilehash: 7119283bec250a4ab0854ba2c29b0906624448e9
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992126"
---
# <a name="how-to-use-spring-data-jpa-with-azure-sql-database"></a><span data-ttu-id="1120e-103">Comment utiliser Spring Data JPA avec Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1120e-103">How to use Spring Data JPA with Azure SQL Database</span></span>

## <a name="overview"></a><span data-ttu-id="1120e-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="1120e-104">Overview</span></span>

<span data-ttu-id="1120e-105">Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations dans une [base de données SQL Azure](https://azure.microsoft.com/services/sql-database/) à l’aide de l’[API de persistance Java (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span><span class="sxs-lookup"><span data-stu-id="1120e-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) using [Java Persistence API (JPA)](https://docs.oracle.com/javaee/7/tutorial/persistence-intro.htm).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1120e-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="1120e-106">Prerequisites</span></span>

<span data-ttu-id="1120e-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1120e-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="1120e-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="1120e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1120e-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1120e-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1120e-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="1120e-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="1120e-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1120e-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="1120e-112">[Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1120e-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="1120e-113">Un client [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1120e-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-sql-satabase"></a><span data-ttu-id="1120e-114">Créer une base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1120e-114">Create an Azure SQL Satabase</span></span>

### <a name="create-a-sql-database-server-using-the-azure-portal"></a><span data-ttu-id="1120e-115">Créer un serveur de base de données SQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1120e-115">Create a SQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="1120e-116">Vous trouverez des informations plus détaillées sur la création de bases de données SQL Azure dans l’article [Création d’une base de données SQL Azure dans le portail Azure](/azure/sql-database/sql-database-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="1120e-116">You can read more detailed information about creating Azure SQL databases in [Create an Azure SQL database in the Azure portal](/azure/sql-database/sql-database-get-started-portal).</span></span>

1. <span data-ttu-id="1120e-117">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1120e-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1120e-118">Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="1120e-118">Click **+Create a resource**, then **Databases**, and then click **SQL Database**.</span></span>

   ![Créer une base de données SQL][SQL01]

1. <span data-ttu-id="1120e-120">Indiquez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1120e-120">Specify the following information:</span></span>

   - <span data-ttu-id="1120e-121">**Nom de la base de données** : choisissez un nom unique pour votre base de données SQL. Elle sera créée dans le serveur SQL de votre choix plus tard.</span><span class="sxs-lookup"><span data-stu-id="1120e-121">**Database name**: Choose a unique name for your SQL database; this will be created in the SQL server that you will specify later.</span></span>
   - <span data-ttu-id="1120e-122">**Abonnement**: indiquez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="1120e-122">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="1120e-123">**Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="1120e-123">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="1120e-124">**Sélectionner la source** : pour ce didacticiel, sélectionnez `Blank database` pour créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="1120e-124">**Select source**: For this tutorial, select `Blank database` to create a new database.</span></span>

   ![Spécifier les propriétés de la base de données SQL][SQL02]
   
1. <span data-ttu-id="1120e-126">Cliquez sur **Serveur** et **Créer un serveur**, puis spécifiez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1120e-126">Click **Server**, then **Create a new server**, and then specify the following information:</span></span>

   - <span data-ttu-id="1120e-127">**Nom du serveur** : choisissez un nom unique pour votre serveur SQL. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoyssql.database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="1120e-127">**Server name**: Choose a unique name for your SQL server; this will be used to create a fully-qualified domain name like *wingtiptoyssql.database.windows.net*.</span></span>
   - <span data-ttu-id="1120e-128">**Connexion d’administrateur du serveur** : spécifiez le nom d’administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="1120e-128">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="1120e-129">**Mot de passe** et **Confirmer le mot de passe** : spécifiez le mot de passe de votre administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="1120e-129">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="1120e-130">**Emplacement** : spécifiez la région géographique le plus proche de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="1120e-130">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Spécifier votre serveur SQL][SQL03]

1. <span data-ttu-id="1120e-132">Après avoir entré toutes les informations ci-dessus, cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="1120e-132">When you have entered all of the above information, click **Select**.</span></span>

1. <span data-ttu-id="1120e-133">Pour ce didacticiel, spécifiez le **niveau tarifaire** le moins onéreux; puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1120e-133">For this tutorial, specify the least-expensive **Pricing tier**, and then click **Create**.</span></span>

   ![Créer votre base de données SQL][SQL04]

### <a name="configure-a-firewall-rule-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="1120e-135">Configurer une règle de pare-feu pour votre serveur SQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1120e-135">Configure a firewall rule for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="1120e-136">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1120e-136">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1120e-137">Cliquez sur **Toutes les ressources**, puis sur le serveur SQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="1120e-137">Click **All Resources**, then click the SQL server you just created.</span></span>

   ![Sélectionner votre serveur SQL][SQL05]

1. <span data-ttu-id="1120e-139">Dans la section **Présentation**, cliquez sur **Afficher les paramètres de pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="1120e-139">In the **Overview** section, click **Show firewall settings**</span></span>

   ![Afficher les paramètres de pare-feu][SQL06]

1. <span data-ttu-id="1120e-141">Dans la section **Pare-feux et réseaux virtuels**, créez une règle en spécifiant un nom unique. Ensuite, entrez la plage d’adresses IP qui doivent accéder à votre base de données, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1120e-141">In the **Firewalls and virtual networks** section, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configurer les paramètres de pare-feu][SQL07]

### <a name="retrieve-the-connection-string-for-your-sql-server-using-the-azure-portal"></a><span data-ttu-id="1120e-143">Récupérer la chaîne de connexion de votre serveur SQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1120e-143">Retrieve the connection string for your SQL server using the Azure Portal</span></span>

1. <span data-ttu-id="1120e-144">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1120e-144">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1120e-145">Cliquez sur **Toutes les ressources**, puis sur la base de données SQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="1120e-145">Click **All Resources**, then click the SQL database you just created.</span></span>

   ![Sélectionner votre base de données SQL][SQL08]

1. <span data-ttu-id="1120e-147">Cliquez sur **Chaînes de connexion**, puis sur **JDBC**, et copiez la valeur dans le champ de texte JDBC.</span><span class="sxs-lookup"><span data-stu-id="1120e-147">Click **Connection strings**, then click **JDBC**, and copy the value in the JDBC text field.</span></span>

   ![Récupérer votre chaîne de connexion JDBC][SQL09]

## <a name="configure-the-sample-application"></a><span data-ttu-id="1120e-149">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="1120e-149">Configure the sample application</span></span>

1. <span data-ttu-id="1120e-150">Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1120e-150">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="1120e-151">Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="1120e-151">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="1120e-152">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :</span><span class="sxs-lookup"><span data-stu-id="1120e-152">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:sqlserver://wingtiptoyssql.database.windows.net:1433;database=wingtiptoys;encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;
   spring.datasource.username=wingtiptoysuser@wingtiptoyssql
   spring.datasource.password=********
    ```
   <span data-ttu-id="1120e-153">Où :</span><span class="sxs-lookup"><span data-stu-id="1120e-153">Where:</span></span>

   | <span data-ttu-id="1120e-154">Paramètre</span><span class="sxs-lookup"><span data-stu-id="1120e-154">Parameter</span></span> | <span data-ttu-id="1120e-155">Description</span><span class="sxs-lookup"><span data-stu-id="1120e-155">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="1120e-156">Spécifie une version modifiée de votre chaîne SQL JDBC mentionnée plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1120e-156">Specifies an edited version of your SQL JDBC string from earlier in this article.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="1120e-157">Spécifie le nom de votre administrateur SQL mentionné plus haut dans cet article, avec le nom abrégé du serveur accolé.</span><span class="sxs-lookup"><span data-stu-id="1120e-157">Specifies your SQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="1120e-158">Spécifie votre mot de passe administrateur SQL mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1120e-158">Specifies your SQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="1120e-159">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="1120e-159">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="1120e-160">Packager et tester l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="1120e-160">Package and test the sample application</span></span> 

1. <span data-ttu-id="1120e-161">Compilez l’exemple d’application avec Maven :</span><span class="sxs-lookup"><span data-stu-id="1120e-161">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P sql
   ```

1. <span data-ttu-id="1120e-162">Démarrez l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="1120e-162">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jpa-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="1120e-163">Créez des enregistrements à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="1120e-163">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="1120e-164">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="1120e-164">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="1120e-165">Récupérez tous les enregistrements existants à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="1120e-165">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="1120e-166">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="1120e-166">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="1120e-167">Résumé</span><span class="sxs-lookup"><span data-stu-id="1120e-167">Summary</span></span>

<span data-ttu-id="1120e-168">Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations dans une base de données Azure SQL à l’aide de JPA.</span><span class="sxs-lookup"><span data-stu-id="1120e-168">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure SQL database using JPA.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1120e-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1120e-169">Next steps</span></span>

<span data-ttu-id="1120e-170">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="1120e-170">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1120e-171">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="1120e-171">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="1120e-172">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1120e-172">Additional Resources</span></span>

<span data-ttu-id="1120e-173">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="1120e-173">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[SQL01]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-01.png
[SQL02]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-02.png
[SQL03]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-03.png
[SQL04]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-04.png
[SQL05]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-05.png
[SQL06]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-06.png
[SQL07]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-07.png
[SQL08]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-08.png
[SQL09]: media/configure-spring-data-jpa-with-azure-sql-server/create-azure-sql-09.png
