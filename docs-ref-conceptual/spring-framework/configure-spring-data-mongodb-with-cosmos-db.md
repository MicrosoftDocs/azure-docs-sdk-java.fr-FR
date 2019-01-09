---
title: Comment utiliser l’API MongoDB de Spring Data avec Azure Cosmos DB
description: Découvrez comment utiliser l’API MongoDB de Spring Data avec Azure Cosmos DB.
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
ms.openlocfilehash: 55fb356820e2cc5eb8d1fe4030053d9e580583af
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53992159"
---
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a><span data-ttu-id="c00d7-103">Comment utiliser l’API MongoDB de Spring Data avec Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c00d7-103">How to use Spring Data MongoDB API with Azure Cosmos DB</span></span>

## <a name="overview"></a><span data-ttu-id="c00d7-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c00d7-104">Overview</span></span>

<span data-ttu-id="c00d7-105">Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations à l’aide de l’[API MongoDB d’Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction).</span><span class="sxs-lookup"><span data-stu-id="c00d7-105">This article demonstrates creating a sample application that uses [Spring Data] to store and retrieve information using the [Azure Cosmos DB MongoDB API](/azure/cosmos-db/mongodb-introduction).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c00d7-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c00d7-106">Prerequisites</span></span>

<span data-ttu-id="c00d7-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c00d7-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="c00d7-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="c00d7-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c00d7-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c00d7-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c00d7-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c00d7-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c00d7-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c00d7-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>
* <span data-ttu-id="c00d7-112">Un client [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="c00d7-112">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="c00d7-113">Création d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c00d7-113">Create an Azure Cosmos DB account</span></span>

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a><span data-ttu-id="c00d7-114">Créer un compte Cosmos DB à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="c00d7-114">Create a Cosmos DB account using the Azure Portal</span></span>

> [!NOTE]
> 
> <span data-ttu-id="c00d7-115">Vous trouverez des informations plus détaillées sur la création de comptes Azure Cosmos DB dans [la documentation Azure Cosmos DB](/azure/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="c00d7-115">You can read more detailed information about creating Azure Cosmos DB accounts in [Azure Cosmos DB Documentation](/azure/cosmos-db/).</span></span>

1. <span data-ttu-id="c00d7-116">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="c00d7-116">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="c00d7-117">Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="c00d7-117">Click **+Create a resource**, then **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Création d’un compte Azure Cosmos DB][COSMOSDB01]

1. <span data-ttu-id="c00d7-119">Indiquez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c00d7-119">Specify the following information:</span></span>

   - <span data-ttu-id="c00d7-120">**Abonnement**: indiquez l’abonnement Azure à utiliser.</span><span class="sxs-lookup"><span data-stu-id="c00d7-120">**Subscription**: Specify your Azure subscription to use.</span></span>
   - <span data-ttu-id="c00d7-121">**Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="c00d7-121">**Resource group**: Specify whether to create a new resource group, or choose an existing resource group.</span></span>
   - <span data-ttu-id="c00d7-122">**Nom du compte** : choisissez un nom unique pour votre compte Cosmos DB. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoysmongodb.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="c00d7-122">**Account name**: Choose a unique name for your Cosmos DB account; this will be used to create a fully-qualified domain name like *wingtiptoysmongodb.documents.azure.com*.</span></span>
   - <span data-ttu-id="c00d7-123">**API** : spécifiez `Azure Cosmos DB for MongoDB API` pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c00d7-123">**API**: Specify `Azure Cosmos DB for MongoDB API` for this tutorial.</span></span>
   - <span data-ttu-id="c00d7-124">**Emplacement** : spécifiez la région géographique le plus proche de votre base de données.</span><span class="sxs-lookup"><span data-stu-id="c00d7-124">**Location**: Specify the closest geographic region for your database.</span></span>

   ![Spécifier les paramètres de votre compte Cosmos DB][COSMOSDB02]
   
1. <span data-ttu-id="c00d7-126">Après avoir entré toutes les informations ci-dessus, cliquez sur **Vérifier + créer**.</span><span class="sxs-lookup"><span data-stu-id="c00d7-126">When you have entered all of the above information, click **Review + create**.</span></span>

1. <span data-ttu-id="c00d7-127">Si tout semble correct, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="c00d7-127">If everything looks correct on the review page, click **Create**.</span></span>

   ![Vérifier les paramètres de votre compte Cosmos DB][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a><span data-ttu-id="c00d7-129">Récupérer la chaîne de connexion pour votre compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c00d7-129">Retrieve the connection string for your Azure Cosmos DB account</span></span>

1. <span data-ttu-id="c00d7-130">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="c00d7-130">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="c00d7-131">Cliquez sur **Toutes les ressources**, puis sur le compte Azure Cosmos DB que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="c00d7-131">Click **All Resources**, then click the Azure Cosmos DB account you just created.</span></span>

   ![Sélectionner votre compte Azure Cosmos DB][COSMOSDB04]

1. <span data-ttu-id="c00d7-133">Cliquez sur **Chaînes de connexion** et copiez la valeur de la **chaîne de connexion principale**. Vous utiliserez cette valeur pour configurer votre application plus tard.</span><span class="sxs-lookup"><span data-stu-id="c00d7-133">Click **Connection strings**, and copy the value for the **Primary Connection String** field; you will use that value to configure your application later.</span></span>

   ![Récupérer votre chaîne de connexion Cosmos DB][COSMOSDB06]

## <a name="configure-the-sample-application"></a><span data-ttu-id="c00d7-135">Configurer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="c00d7-135">Configure the sample application</span></span>

1. <span data-ttu-id="c00d7-136">Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c00d7-136">Open a command shell and clone the sample project using a git command like the following example:</span></span>

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. <span data-ttu-id="c00d7-137">Créez un répertoire *resources* dans le répertoire *&lt;project root&gt;/complete/src/main* de l’exemple de projet, puis créez un fichier *application.properties* dans le répertoire *resources*.</span><span class="sxs-lookup"><span data-stu-id="c00d7-137">Create a *resources* directory in the *&lt;project root&gt;/complete/src/main* directory of the sample project, and create an *application.properties* file in the *resources* directory.</span></span>

1. <span data-ttu-id="c00d7-138">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment  :</span><span class="sxs-lookup"><span data-stu-id="c00d7-138">Open the *application.properties* file in a text editor, and add the following lines in the file, and replace the sample values with the appropriate values from earlier:</span></span>

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   <span data-ttu-id="c00d7-139">Où :</span><span class="sxs-lookup"><span data-stu-id="c00d7-139">Where:</span></span>

   | <span data-ttu-id="c00d7-140">Paramètre</span><span class="sxs-lookup"><span data-stu-id="c00d7-140">Parameter</span></span> | <span data-ttu-id="c00d7-141">Description</span><span class="sxs-lookup"><span data-stu-id="c00d7-141">Description</span></span> |
   |---|---|
   | `spring.data.mongodb.database` | <span data-ttu-id="c00d7-142">Spécifie le nom de votre compte Cosmos DB tel que spécifié plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c00d7-142">Specifies the name of your Cosmos DB account from earlier in this article.</span></span> |
   | `spring.data.mongodb.uri` | <span data-ttu-id="c00d7-143">Spécifie la **chaîne de connexion principale** mentionnée plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="c00d7-143">Specifies the **Primary Connection String** from earlier in this article.</span></span> |

1. <span data-ttu-id="c00d7-144">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="c00d7-144">Save and close the *application.properties* file.</span></span>

## <a name="package-and-test-the-sample-application"></a><span data-ttu-id="c00d7-145">Packager et tester l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="c00d7-145">Package and test the sample application</span></span> 

1. <span data-ttu-id="c00d7-146">Compilez l’exemple d’application avec Maven et configurez Maven pour ignorer les tests ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="c00d7-146">Build the sample application with Maven, and configure Maven to skip tests; for example:</span></span>

   ```shell
   mvn clean package -DskipTests
   ```

1. <span data-ttu-id="c00d7-147">Démarrez l’exemple d’application :</span><span class="sxs-lookup"><span data-stu-id="c00d7-147">Start the sample application; for example:</span></span>

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   <span data-ttu-id="c00d7-148">Votre application doit renvoyer des valeurs comme suit :</span><span class="sxs-lookup"><span data-stu-id="c00d7-148">Your application should return values like the following:</span></span>

   ```json
   Customers found with findAll():
   -------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   
   Customer found with findByFirstName('Alice'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customers found with findByLastName('Smith'):
   --------------------------------
   Customer[id=5c1b4ae4d0b5080ac105cc13, firstName='Alice', lastName='Smith']
   Customer[id=5c1b4ae4d0b5080ac105cc14, firstName='Bob', lastName='Smith']
   ```

## <a name="summary"></a><span data-ttu-id="c00d7-149">Résumé</span><span class="sxs-lookup"><span data-stu-id="c00d7-149">Summary</span></span>

<span data-ttu-id="c00d7-150">Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations à l’aide de l’API MongoDB d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c00d7-150">In this tutorial, you created a sample Java application that uses Spring Data to store and retrieve information using the Azure Cosmos DB MongoDB API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c00d7-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c00d7-151">Next steps</span></span>

<span data-ttu-id="c00d7-152">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="c00d7-152">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c00d7-153">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="c00d7-153">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="c00d7-154">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c00d7-154">Additional Resources</span></span>

<span data-ttu-id="c00d7-155">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="c00d7-155">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

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

[COSMOSDB01]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-01.png
[COSMOSDB02]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-02.png
[COSMOSDB03]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-03.png
[COSMOSDB04]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-04.png
[COSMOSDB06]: media/configure-spring-data-mongodb-with-cosmos-db/create-cosmos-db-06.png
