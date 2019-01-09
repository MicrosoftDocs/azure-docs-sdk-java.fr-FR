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
# <a name="how-to-use-spring-data-mongodb-api-with-azure-cosmos-db"></a>Comment utiliser l’API MongoDB de Spring Data avec Azure Cosmos DB

## <a name="overview"></a>Vue d’ensemble

Cet article illustre la création d’un exemple d’application qui utilise [Spring Data] pour stocker et récupérer des informations à l’aide de l’[API MongoDB d’Azure Cosmos DB](/azure/cosmos-db/mongodb-introduction).

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.
* Un client [Git](https://git-scm.com/downloads).

## <a name="create-an-azure-cosmos-db-account"></a>Création d’un compte Azure Cosmos DB

### <a name="create-a-cosmos-db-account-using-the-azure-portal"></a>Créer un compte Cosmos DB à l’aide du portail Azure

> [!NOTE]
> 
> Vous trouverez des informations plus détaillées sur la création de comptes Azure Cosmos DB dans [la documentation Azure Cosmos DB](/azure/cosmos-db/).

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez successivement sur **+ Créer une ressource**, **Bases de données** et **Azure Cosmos DB**.

   ![Création d’un compte Azure Cosmos DB][COSMOSDB01]

1. Indiquez les informations suivantes :

   - **Abonnement**: indiquez l’abonnement Azure à utiliser.
   - **Groupe de ressources** : choisissez un groupe de ressources existant ou spécifiez un nom pour en créer un.
   - **Nom du compte** : choisissez un nom unique pour votre compte Cosmos DB. Il sera utilisé pour créer un nom de domaine complet comme *wingtiptoysmongodb.documents.azure.com*.
   - **API** : spécifiez `Azure Cosmos DB for MongoDB API` pour ce didacticiel.
   - **Emplacement** : spécifiez la région géographique le plus proche de votre base de données.

   ![Spécifier les paramètres de votre compte Cosmos DB][COSMOSDB02]
   
1. Après avoir entré toutes les informations ci-dessus, cliquez sur **Vérifier + créer**.

1. Si tout semble correct, cliquez sur **Créer**.

   ![Vérifier les paramètres de votre compte Cosmos DB][COSMOSDB03]

### <a name="retrieve-the-connection-string-for-your-azure-cosmos-db-account"></a>Récupérer la chaîne de connexion pour votre compte Azure Cosmos DB

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **Toutes les ressources**, puis sur le compte Azure Cosmos DB que vous venez de créer.

   ![Sélectionner votre compte Azure Cosmos DB][COSMOSDB04]

1. Cliquez sur **Chaînes de connexion** et copiez la valeur de la **chaîne de connexion principale**. Vous utiliserez cette valeur pour configurer votre application plus tard.

   ![Récupérer votre chaîne de connexion Cosmos DB][COSMOSDB06]

## <a name="configure-the-sample-application"></a>Configurer l’exemple d’application

1. Ouvrez un interpréteur de commandes et clonez l’exemple de projet à l’aide d’une commande git, comme dans l’exemple suivant :

   ```shell
   git clone https://github.com/spring-guides/gs-accessing-data-mongodb.git
   ```

1. Créez un répertoire *resources* dans le répertoire *&lt;project root&gt;/complete/src/main* de l’exemple de projet, puis créez un fichier *application.properties* dans le répertoire *resources*.

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez les lignes suivantes dans le fichier et remplacez les exemples de valeurs par les valeurs appropriées mentionnées précédemment  :

   ```yaml
   spring.data.mongodb.database=wingtiptoysmongodb
   spring.data.mongodb.uri=mongodb://wingtiptoysmongodb:AbCdEfGhIjKlMnOpQrStUvWxYz==@wingtiptoysmongodb.documents.azure.com:10255/?ssl=true&replicaSet=globaldb
   ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `spring.data.mongodb.database` | Spécifie le nom de votre compte Cosmos DB tel que spécifié plus haut dans cet article. |
   | `spring.data.mongodb.uri` | Spécifie la **chaîne de connexion principale** mentionnée plus haut dans cet article. |

1. Enregistrez et fermez le fichier *application.properties*.

## <a name="package-and-test-the-sample-application"></a>Packager et tester l’exemple d’application 

1. Compilez l’exemple d’application avec Maven et configurez Maven pour ignorer les tests ; par exemple :

   ```shell
   mvn clean package -DskipTests
   ```

1. Démarrez l’exemple d’application :

   ```shell
   java -jar target/gs-accessing-data-mongodb-0.1.0.jar
   ```
    
   Votre application doit renvoyer des valeurs comme suit :

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

## <a name="summary"></a>Résumé

Dans ce didacticiel, vous avez créé un exemple d’application Java qui utilise Spring Data pour stocker et récupérer des informations à l’aide de l’API MongoDB d’Azure Cosmos DB.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
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
