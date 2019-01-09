---
title: Comment utiliser l’API Apache Cassandra de Spring Data avec Azure Cosmos DB
description: Découvrez comment utiliser l’API Apache Cassandra de Spring Data avec Azure Cosmos DB.
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
ms.openlocfilehash: 1f3f7a55b49d64077df9e7d4d6acc3af4495b424
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992122"
---
# <a name="how-to-use-spring-data-apache-cassandra-api-with-azure-cosmos-db"></a><span data-ttu-id="e3894-103">Comment utiliser l’API Apache Cassandra de Spring Data avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e3894-103">How to use Spring Data Apache Cassandra API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="e3894-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="e3894-104">Overview</span></span>

<span data-ttu-id="e3894-105">Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations à l’aide de l’[API Cassandra d’Azure Cosmos DB](/azure/cosmos-db/cassandra-introduction).</span><span class="sxs-lookup"><span data-stu-id="e3894-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB Cassandra API](/azure/cosmos-db/cassandra-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3894-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="e3894-106">Prerequisites</span></span>

<span data-ttu-id="e3894-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e3894-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="e3894-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="e3894-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e3894-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e3894-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="e3894-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="e3894-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="e3894-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e3894-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="e3894-112">[Curl](https://curl.haxx.se/) ou l’utilitaire HTTP similaire pour tester la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e3894-112">[Curl](https://curl.haxx.se/) or similar HTTP utility to test functionality.</span></span>
* <span data-ttu-id="e3894-113">Un client [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="e3894-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="e3894-114">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e3894-114">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="e3894-115">Créer un compte Cosmos DB à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="e3894-115">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="e3894-116">Vous trouverez des informations plus détaillées sur la création de comptes Azure Cosmos DB dans [la documentation Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e3894-116">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="e3894-117">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="e3894-117">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e3894-118">Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="e3894-118">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Création d’un compte Azure Cosmos DB][COSMOSDB01]

1. <span data-ttu-id="e3894-120">Indiquez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3894-120">Specify the following information:</span></span>

   - <span data-ttu-id="e3894-121">**Abonnement**: indiquez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="e3894-121">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="e3894-122">**Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="e3894-122">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="e3894-123">**Nom du compte** : choisissez un nom unique pour votre compte Cosmos DB. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoyscassandra.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="e3894-123">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoyscassandra.documents.azure.com*.</span></span>
   - <span data-ttu-id="e3894-124">**API** : spécifiez `Cassandra` pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e3894-124">**API**: Specify `Cassandra` for this tutorial.</span></span>
   - <span data-ttu-id="e3894-125">**Emplacement** : spécifiez la région géographique le plus proche de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="e3894-125">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Spécifier les paramètres de votre compte Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="e3894-127">Après avoir entré toutes les informations ci-dessus, cliquez sur **Vérifier + créer**.</span><span class="sxs-lookup"><span data-stu-id="e3894-127">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="e3894-128">Si tout semble correct, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e3894-128">If everything looks correct on the review page, click **Create**.</span></span>

   ![Vérifier les paramètres de votre compte Cosmos DB][COSMOSDB03]

### <a name="add-a-keyspace-to-your-azure-cosmos-db-account"></a><span data-ttu-id="e3894-130">Ajoutez un espace de clés à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3894-130">Add a keyspace to your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="e3894-131">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="e3894-131">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e3894-132">Cliquez sur **Toutes les ressources**, puis sur le compte Azure Cosmos DB que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="e3894-132">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Sélectionner votre compte Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="e3894-134">Cliquez sur **Explorateur de données**, puis sur **Nouvel espace de clés**.</span><span class="sxs-lookup"><span data-stu-id="e3894-134">Click **Data Explorer**, then click **New Keyspace**.</span></span> <span data-ttu-id="e3894-135">Entrez un identificateur unique pour votre **ID d’espace de clés**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3894-135">Enter a unique identifier for your **Keyspace id**, then click **OK**.</span></span>

   ![Créer un espace de clés Cosmos DB][COSMOSDB05]

### <a name="retrieve-the-connection-settings-for-your-azure-cosmos-db-account"></a><span data-ttu-id="e3894-137">Récupérer les paramètres de connexion pour votre compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e3894-137">Retrieve the connection settings for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="e3894-138">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="e3894-138">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="e3894-139">Cliquez sur **Toutes les ressources**, puis sur le compte Azure Cosmos DB que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="e3894-139">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Sélectionner votre compte Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="e3894-141">Cliquez sur **Chaînes de connexion**, puis copiez les valeurs des champs **Point de contact**, **Port**, **Nom d’utilisateur** et **Mot de passe principal** . Vous utiliserez ces valeurs pour configurer votre application plus tard.</span><span class="sxs-lookup"><span data-stu-id="e3894-141">Click **Connection strings**, and copy the values for the **Contact Point**, **Port**, **Username**, and **Primary Password** fields; you will use those values to configure your application later.</span></span>

   ![Récupérer vos paramètres de connexion Cosmos DB][COSMOSDB05]

## <a name="configure-the-sample-application"></a><span data-ttu-id="e3894-143">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="e3894-143">Configure the sample application</span></span>

1. <span data-ttu-id="e3894-144">Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e3894-144">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/Azure-Samples/spring-data-cassandra-on-azure.git
   ```

1. <span data-ttu-id="e3894-145">Recherchez le fichier *application.properties* dans le répertoire *resources* de l’exemple de projet, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="e3894-145">Locate the *application.properties* file in the *resources* directory of the sample project, or create the file if it does not already exist.</span></span>

1. <span data-ttu-id="e3894-146">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez ou configurez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment :</span><span class="sxs-lookup"><span data-stu-id="e3894-146">Open the *application.properties* file in a text editor, and add or configure the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.cassandra.contact-points=wingtiptoyscassandra.cassandra.cosmosdb.azure.com
   spring.data.cassandra.port=10350
   spring.data.cassandra.username=wingtiptoyscassandra
   spring.data.cassandra.password=********
   ```
   <span data-ttu-id="e3894-147">Où :</span><span class="sxs-lookup"><span data-stu-id="e3894-147">Where:</span></span>

   | <span data-ttu-id="e3894-148">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e3894-148">Parameter</span></span> | <span data-ttu-id="e3894-149">Description</span><span class="sxs-lookup"><span data-stu-id="e3894-149">Description</span></span> |
   |---|---|
   | `spring.data.cassandra.contact-points` | <span data-ttu-id="e3894-150">Spécifie le **point de contact** mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e3894-150">Specifies the **Contact Point** from earlier in this article.</span></span> |
   | `spring.data.cassandra.port` | <span data-ttu-id="e3894-151">Spécifie le **port** mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e3894-151">Specifies the **Port** from earlier in this article.</span></span> |
   | `spring.data.cassandra.username` | <span data-ttu-id="e3894-152">Spécifie le **nom d’utilisateur** mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e3894-152">Specifies your **Username** from earlier in this article.</span></span> |
   | `spring.data.cassandra.password` | <span data-ttu-id="e3894-153">Spécifie le **mot de passe principal** mentionné plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="e3894-153">Specifies your **Primary Password** from earlier in this article.</span></span> |

1. <span data-ttu-id="e3894-154">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="e3894-154">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="e3894-155">Packager et tester l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="e3894-155">Package and test the sample application</span></span> 

1. <span data-ttu-id="e3894-156">Compilez l’exemple d’application avec Maven :</span><span class="sxs-lookup"><span data-stu-id="e3894-156">Build the sample application with Maven; for example:</span></span>

   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="e3894-157">Démarrez l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="e3894-157">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/spring-data-cassandra-on-azure-0.1.0-SNAPSHOT.jar
   ```

1. <span data-ttu-id="e3894-158">Créez des enregistrements à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="e3894-158">Create new records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s -d '{"name":"dog","species":"canine"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets

   curl -s -d '{"name":"cat","species":"feline"}' -H "Content-Type: application/json" -X POST http://localhost:8080/pets
   ```

   <span data-ttu-id="e3894-159">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3894-159">Your application should return values like the following:</span></span>

   ```shell
   Added Pet{id=60fa8cb0-0423-11e9-9a70-39311962166b, name='dog', species='canine'}.

   Added Pet{id=72c1c9e0-0423-11e9-9a70-39311962166b, name='cat', species='feline'}.
   ```

1. <span data-ttu-id="e3894-160">Récupérez tous les enregistrements existants à l’aide de `curl` à partir d’une invite de commandes comme dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="e3894-160">Retrieve all of the existing records using `curl` from a command prompt like the following examples:</span></span>

   ```shell
   curl -s http://localhost:8080/pets
   ```
    
   <span data-ttu-id="e3894-161">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3894-161">Your application should return values like the following:</span></span>

   ```json
   [{"id":"60fa8cb0-0423-11e9-9a70-39311962166b","name":"dog","species":"canine"},{"id":"72c1c9e0-0423-11e9-9a70-39311962166b","name":"cat","species":"feline"}]
   ```

## <a name="summary"></a><span data-ttu-id="e3894-162">Résumé</span><span class="sxs-lookup"><span data-stu-id="e3894-162">Summary</span></span>

<span data-ttu-id="e3894-163">Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations à l’aide de l’API Cassandra d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e3894-163">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB Cassandra API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3894-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3894-164">Next steps</span></span>

<span data-ttu-id="e3894-165">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e3894-165">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3894-166">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="e3894-166">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="e3894-167">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e3894-167">Additional Resources</span></span>

<span data-ttu-id="e3894-168">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="e3894-168">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB05]: media/configure-spring-data-apache-cassandra-with-cosmos-db/create-cosmos-db-05.png
