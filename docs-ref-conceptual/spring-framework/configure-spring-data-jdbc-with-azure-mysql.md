---
title: Comment utiliser Spring Data JDBC avec Azure MySQL
description: Découvrez comment utiliser Spring Data JDBC avec une base de données Azure MySQL.
services: mysql
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: mysql
ms.tgt_pltfrm: multiple
ms.topic: article
ms.openlocfilehash: 5ec89194c72cef81c79d21382e41b33ebe91d3d0
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992123"
---
# <a name="how-to-use-spring-data-jdbc-with-azure-mysql"></a><span data-ttu-id="1069d-103">Comment utiliser Spring Data JDBC avec Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="1069d-103">How to use Spring Data JDBC with Azure MySQL</span></span>

## <a name="overview"></a><span data-ttu-id="1069d-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="1069d-104">Overview</span></span>

<span data-ttu-id="1069d-105">Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations dans une base de données Azure [MySQL](https://www.mysql.com/) à l’aide de [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span><span class="sxs-lookup"><span data-stu-id="1069d-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information in an Azure [MySQL](https://www.mysql.com/) database using [Java Database Connectivity (JDBC)](https://docs.oracle.com/javase/8/docs/technotes/guides/jdbc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1069d-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="1069d-106">Prerequisites</span></span>

<span data-ttu-id="1069d-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1069d-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="1069d-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="1069d-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="1069d-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="1069d-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="1069d-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="1069d-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="1069d-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1069d-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="1069d-112">[Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1069d-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="1069d-113">L’utilitaire de ligne de commande [mysql](https://dev.mysql.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1069d-113">The [mysql](https://dev.mysql.com/downloads/) command-line utility.</span></span>
* <span data-ttu-id="1069d-114">Un client [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="1069d-114">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-a-mysql-database-for-azure"></a><span data-ttu-id="1069d-115">Créer une base de données MySQL pour Azure</span><span class="sxs-lookup"><span data-stu-id="1069d-115">Create a MySQL database for Azure</span></span>

### <a name="create-a-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="1069d-116">Créer un serveur de base de données MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1069d-116">Create a MySQL database server using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="1069d-117">Vous trouverez des informations plus détaillées sur la création de bases de données MySQL dans l’article [Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="1069d-117">You can read more detailed information about creating MySQL databases in [Create an Azure Database for MySQL server by using the Azure portal](/azure/mysql/quickstart-create-mysql-server-database-using-azure-portal).</span></span>

1. <span data-ttu-id="1069d-118">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1069d-118">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1069d-119">Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Database pour MySQL**.</span><span class="sxs-lookup"><span data-stu-id="1069d-119">Click **+Create a resource**, then **Databases**, and then click **Azure Database for MySQL**.</span></span>

   ![Créer une base de données MySQL][MYSQL01]

1. <span data-ttu-id="1069d-121">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1069d-121">Enter the following information:</span></span>

   - <span data-ttu-id="1069d-122">**Nom du serveur** : choisissez un nom unique pour votre serveur MySQL. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoysmysql.mysql.database.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="1069d-122">**Server name**: Choose a unique name for your MySQL server; this will be used to create a fully-qualified domain name like *wingtiptoysmysql.mysql.database.azure.com*.</span></span>
   - <span data-ttu-id="1069d-123">**Abonnement**: indiquez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="1069d-123">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="1069d-124">**Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="1069d-124">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="1069d-125">**Sélectionner la source** : pour ce didacticiel, sélectionnez `Blank` pour créer une base de données.</span><span class="sxs-lookup"><span data-stu-id="1069d-125">**Select source**: For this tutorial, select `Blank` to create a new database.</span></span>
   - <span data-ttu-id="1069d-126">**Connexion d’administrateur du serveur** : spécifiez le nom d’administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="1069d-126">**Server admin login**: Specify the database administrator name.</span></span>
   - <span data-ttu-id="1069d-127">**Mot de passe** et **Confirmer le mot de passe** : spécifiez le mot de passe de votre administrateur de base de données.</span><span class="sxs-lookup"><span data-stu-id="1069d-127">**Password** and **Confirm password**: Specify the password for your database administrator.</span></span>
   - <span data-ttu-id="1069d-128">**Emplacement** : spécifiez la région géographique le plus proche de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="1069d-128">**Location**: Specify the closest geographic region for your database.</span></span>
   - <span data-ttu-id="1069d-129">**Version** : spécifiez la version la plus à jour la base de données.</span><span class="sxs-lookup"><span data-stu-id="1069d-129">**Version**: Specify the most-up-to-date database version.</span></span>
   - <span data-ttu-id="1069d-130">**Niveau tarifaire** : pour ce didacticiel, spécifiez le niveau tarifaire le moins onéreux.</span><span class="sxs-lookup"><span data-stu-id="1069d-130">**Pricing tier**: For this tutorial, specify the least-expensive pricing tier.</span></span>

   ![Créer les propriétés de la base de données MySQL][MYSQL02]

1. <span data-ttu-id="1069d-132">Après avoir entré toutes les informations ci-dessus, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="1069d-132">When you have entered all of the above information, click **Create**.</span></span>

### <a name="configure-a-firewall-rule-for-your-mysql-database-server-using-the-azure-portal"></a><span data-ttu-id="1069d-133">Configurer une règle de pare-feu pour votre serveur de bases de données MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1069d-133">Configure a firewall rule for your MySQL database server using the Azure Portal</span></span>

1. <span data-ttu-id="1069d-134">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1069d-134">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1069d-135">Cliquez sur **Toutes les ressources**, puis sur la base de données MySQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="1069d-135">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Sélectionner la base de données MySQL][MYSQL03]

1. <span data-ttu-id="1069d-137">Cliquez sur **Sécurité de la connexion**, puis, dans **Règles de pare-feu**, créez une règle en spécifiant un nom unique. Ensuite, entrez la plage d’adresses IP qui doivent accéder à votre base de données, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="1069d-137">Click **Connection security**, and in the **Firewall rules**, create a new rule by specifying a unique name for the rule, then enter the range of IP addresses that will need access to your database, and then click **Save**.</span></span>

   ![Configurer la sécurité de la connexion][MYSQL04]

### <a name="retrieve-the-connection-string-for-your-mysql-server-using-the-azure-portal"></a><span data-ttu-id="1069d-139">Récupérer la chaîne de connexion de votre serveur MySQL à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="1069d-139">Retrieve the connection string for your MySQL server using the Azure Portal</span></span>

1. <span data-ttu-id="1069d-140">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="1069d-140">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="1069d-141">Cliquez sur **Toutes les ressources**, puis sur la base de données MySQL que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="1069d-141">Click **All Resources**, then click the MySQL database you just created.</span></span>

   ![Sélectionner la base de données MySQL][MYSQL03]

1. <span data-ttu-id="1069d-143">Cliquez sur **Chaînes de connexion** et copiez la valeur dans le champ de texte **JDBC**.</span><span class="sxs-lookup"><span data-stu-id="1069d-143">Click **Connection strings**, and copy the value in the **JDBC** text field.</span></span>

   ![Récupérer votre chaîne de connexion JDBC][MYSQL05]

### <a name="create-mysql-database-using-the-mysql-command-line-utility"></a><span data-ttu-id="1069d-145">Créer la base de données MySQL à l’aide de l’utilitaire de ligne de commande `mysql`</span><span class="sxs-lookup"><span data-stu-id="1069d-145">Create MySQL database using the `mysql` command-line utility</span></span>

1. <span data-ttu-id="1069d-146">Ouvrez un interpréteur de commandes et connectez-vous à votre serveur MySQL en entrant une commande `mysql`, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-146">Open a command shell and connect to your MySQL server by entering a `mysql` command like the following example:</span></span>

   ```shell
   mysql --host wingtiptoysmysql.mysql.database.azure.com --user wingtiptoysuser@wingtiptoysmysql -p
   ```
   <span data-ttu-id="1069d-147">Où :</span><span class="sxs-lookup"><span data-stu-id="1069d-147">Where:</span></span>

   | <span data-ttu-id="1069d-148">Paramètre</span><span class="sxs-lookup"><span data-stu-id="1069d-148">Parameter</span></span> | <span data-ttu-id="1069d-149">Description</span><span class="sxs-lookup"><span data-stu-id="1069d-149">Description</span></span> |
   |---|---|
   | `host` | <span data-ttu-id="1069d-150">Spécifie le nom complet du serveur MySQL mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1069d-150">Specifies your fully qualified MySQL server name from earlier in this article.</span></span> |
   | `user` | <span data-ttu-id="1069d-151">Spécifie votre administrateur MySQL et le nom abrégé de serveur mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1069d-151">Specifies your MySQL administrator and shortened server name from earlier in this article.</span></span> |
   | `p` | <span data-ttu-id="1069d-152">Spécifie qu’il faut attendre l’invite de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1069d-152">Specifies to wait until prompted for a password.</span></span> |

   <span data-ttu-id="1069d-153">Votre serveur MySQL doit répondre avec un affichage semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-153">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Welcome to the MySQL monitor.  Commands end with ; or \g.
   Your MySQL connection id is 64552
   Server version: 5.6.39.0 MySQL Community Server (GPL)
   
   Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.
   
   Oracle is a registered trademark of Oracle Corporation and/or its
   affiliates. Other names may be trademarks of their respective
   owners.
   
   Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
   
   mysql>
   ```

1. <span data-ttu-id="1069d-154">Créez une base de données nommée *mysqldb* en entrant une commande `mysql` comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-154">Create a database named *mysqldb* by entering a `mysql` command like the following example:</span></span>

   ```SQL
   CREATE DATABASE mysqldb;
   ```

   <span data-ttu-id="1069d-155">Votre serveur MySQL doit répondre avec un affichage semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-155">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   Query OK, 1 row affected (0.30 sec)
   ```

1. <span data-ttu-id="1069d-156">FACULTATIF : vous pouvez vérifier que votre base de données a été créée en entrant une commande `mysql` comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-156">OPTIONAL: You can verify that your database was created by entering a `mysql` command like the following example:</span></span>

   ```SQL
   SHOW DATABASES;
   ```

   <span data-ttu-id="1069d-157">Votre serveur MySQL doit répondre avec un affichage semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-157">Your MySQL server should respond with a display like the following example:</span></span>

   ```shell
   +--------------------+
   | Database           |
   +--------------------+
   | information_schema |
   | mysql              |
   | mysqldb            |
   | performance_schema |
   | sys                |
   +--------------------+
   ```

1. <span data-ttu-id="1069d-158">Entrez `\q` pour quitter l’utilitaire `mysql`.</span><span class="sxs-lookup"><span data-stu-id="1069d-158">Enter `\q` to exit the `mysql` utility.</span></span>

## <a name="configure-the-sample-application"></a><span data-ttu-id="1069d-159">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="1069d-159">Configure the sample application</span></span>

1. <span data-ttu-id="1069d-160">Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1069d-160">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-jdbc-on-azure.git
   ```

1. <span data-ttu-id="1069d-161">Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="1069d-161">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="1069d-162">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :</span><span class="sxs-lookup"><span data-stu-id="1069d-162">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.datasource.url=jdbc:mysql://wingtiptoysmysql.mysql.database.azure.com:3306/mysqldb?useSSL=true&requireSSL=false&serverTimezone=UTC
   spring.datasource.username=wingtiptoysuser@wingtiptoysmysql
   spring.datasource.password=********
    ```
   <span data-ttu-id="1069d-163">Où :</span><span class="sxs-lookup"><span data-stu-id="1069d-163">Where:</span></span>

   | <span data-ttu-id="1069d-164">Paramètre</span><span class="sxs-lookup"><span data-stu-id="1069d-164">Parameter</span></span> | <span data-ttu-id="1069d-165">Description</span><span class="sxs-lookup"><span data-stu-id="1069d-165">Description</span></span> |
   |---|---|
   | `spring.datasource.url` | <span data-ttu-id="1069d-166">Spécifie votre chaîne JDBC MySQL mentionnée plus haut dans cet article, avec un fuseau horaire.</span><span class="sxs-lookup"><span data-stu-id="1069d-166">Specifies your MySQL JDBC string from earlier in this article, with the time zone added.</span></span> |
   | `spring.datasource.username` | <span data-ttu-id="1069d-167">Spécifie le nom de votre administrateur MySQL mentionné plus haut dans cet article, avec le nom abrégé du serveur accolé.</span><span class="sxs-lookup"><span data-stu-id="1069d-167">Specifies your MySQL administrator name from earlier in this article, with the shortened server name appended to it.</span></span> |
   | `spring.datasource.password` | <span data-ttu-id="1069d-168">Spécifie votre mot de passe administrateur MySQL mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="1069d-168">Specifies your MySQL administrator password from earlier in this article.</span></span> |

1. <span data-ttu-id="1069d-169">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="1069d-169">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="1069d-170">Packager et tester l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="1069d-170">Package and test the sample application</span></span> 

1. <span data-ttu-id="1069d-171">Compilez l’exemple d’application avec Maven :</span><span class="sxs-lookup"><span data-stu-id="1069d-171">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package -P mysql
   ```

1. <span data-ttu-id="1069d-172">Démarrez l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="1069d-172">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-jdbc-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="1069d-173">Créez des enregistrements à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="1069d-173">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="1069d-174">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="1069d-174">Your application should return values like the following:</span></span>

   ```shell
   Added Pet(id=1, name=dog, species=canine).

   Added Pet(id=2, name=cat, species=feline).
   ```

1. <span data-ttu-id="1069d-175">Récupérez tous les enregistrements existants à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="1069d-175">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="1069d-176">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="1069d-176">Your application should return values like the following:</span></span>

   ```json
   [{"id":1,"name":"dog","species":"canine"},{"id":2,"name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="1069d-177">Résumé</span><span class="sxs-lookup"><span data-stu-id="1069d-177">Summary</span></span>

<span data-ttu-id="1069d-178">Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations dans une base de données Azure MySQL à l’aide de JDBC.</span><span class="sxs-lookup"><span data-stu-id="1069d-178">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information in an Azure MySQL database using JDBC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1069d-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1069d-179">Next steps</span></span>

<span data-ttu-id="1069d-180">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="1069d-180">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1069d-181">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="1069d-181">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="1069d-182">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1069d-182">Additional Resources</span></span>

<span data-ttu-id="1069d-183">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="1069d-183">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[MYSQL01]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-01.png
[MYSQL02]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-02.png
[MYSQL03]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-03.png
[MYSQL04]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-04.png
[MYSQL05]: media/configure-spring-data-jdbc-with-azure-mysql/create-mysql-05.png
