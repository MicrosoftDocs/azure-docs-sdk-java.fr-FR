---
title: S’authentifier avec les bibliothèques de gestion Azure pour Java
description: S’authentifier avec un principal de service dans les bibliothèques de gestion Azure pour Java
keywords: Azure, Java, SDK, API, Maven, Gradle, authentification, Active Directory, principal du service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 10f457e3-578b-4655-8cd1-51339226ee7d
ms.openlocfilehash: 1d556955fcc5b73f1ba099a0b846b571ba64ccff
ms.sourcegitcommit: 107c3c5ed8c6991c751f95bcaf3757220940df9e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34050726"
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a>S’authentifier avec les bibliothèques Azure pour Java 

## <a name="connect-to-services-with-connection-strings"></a>Se connecter aux services avec des chaînes de connexion

La plupart des bibliothèques de service Azure utilisent une chaîne de connexion ou une clé sécurisée pour l’authentification. Par exemple, SQL Database inclut les informations de nom d’utilisateur et de mot de passe dans la chaîne de connexion JDBC :

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

Le stockage Azure utilise une clé de stockage pour autoriser l’application :

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

Les chaînes de connexion de service sont utilisées pour s’authentifier auprès d’autres services Azure tels que [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) et [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues). Vous pouvez obtenir les chaînes de connexion à l’aide du portail Azure ou Azure CLI.  Vous pouvez aussi utiliser les bibliothèques de gestion Azure pour Java pour interroger des ressources et générer des chaînes de connexion dans votre code. 

Par exemple, ce code utilise les bibliothèques de gestion pour créer une chaîne de connexion de compte de stockage :

```java
// create a new storage account
StorageAccount storage = azure.storageAccounts().getByResourceGroup("myResourceGroup","myStorageAccount");

// create a storage container to hold the file
List<StorageAccountKey> keys = storage.getKeys();
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.name()
        + ";AccountKey=" + keys.get(0).value()
        + ";EndpointSuffix=core.windows.net";
```

D’autres bibliothèques ont besoin que votre application s’exécute avec un [principal de service](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) qui l’autorise à s’exécuter avec des informations d’identification accordées. Cette configuration est similaire à celle de l’authentification basée sur un objet pour les bibliothèques de gestion répertoriées ci-dessous.

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a>S’authentifier avec les bibliothèques de gestion Azure pour Java

Vous pouvez authentifier votre application avec Azure de deux façons, lorsque vous utilisez les bibliothèques de gestion Java pour créer et gérer des ressources.

### <a name="authenticate-with-an-applicationtokencredentials-object"></a>S’authentifier avec un objet ApplicationTokenCredentials

Créez une instance de l’objet `ApplicationTokenCredentials` pour fournir les informations d’identification du principal de service à l’objet `Azure` de niveau supérieur à partir de votre code.

```java
import com.microsoft.azure.credentials.ApplicationTokenCredentials;
import com.microsoft.azure.AzureEnvironment;

// ...

ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(client, 
        tenant,
        key, 
        AzureEnvironment.AZURE);
        
Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credentials)
        .withDefaultSubscription();
```

Les valeurs `client`, `tenant` et `key` sont les mêmes valeurs du principal de service utilisées lors d’une [authentification basée sur un fichier](#mgmt-file). La valeur `AzureEnvironment.AZURE` crée des informations d’identification contre le cloud public Azure. Remplacez-la par une autre valeur, si vous avez besoin d’accéder à un autre cloud (par exemple, `AzureEnvironment.AZURE_GERMANY`).  

 Lisez les valeurs du principal de service depuis des variables d’environnement ou un stockage de gestion de secret tels que [Key Vault](/azure/key-vault/key-vault-whatis). Évitez d’utiliser ces valeurs sous forme de chaînes de texte en clair dans votre code pour éviter toute exposition accidentelle d’informations d’identification dans votre historique de contrôle de version.   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a>Authentification basée sur un fichier (version préliminaire)

La méthode d’authentification la plus simple consiste à créer un fichier de propriétés qui contient les informations d’identification d’un [principal de service Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) en utilisant le format suivant :

```text
# sample management library properties file
subscription=########-####-####-####-############
client=########-####-####-####-############
key=XXXXXXXXXXXXXXXX
tenant=########-####-####-####-############
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

- abonnement : utilisez la valeur *id* de `az account show` dans Azure CLI 2.0.
- client : utilisez la valeur *appId* de la sortie d’un principal de service créé pour exécuter l’application. Si votre application ne dispose pas d’un principal de service, [créez-en un avec Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).
- clé : utilisez la valeur *password* du principal de service pour créer la sortie CLI 
- abonné : utilisez la valeur *tenant* du principal de service pour créer la sortie CLI

Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire. Définissez une variable d’environnement avec le chemin complet du fichier dans l’interpréteur de commande :

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Créez l’objet de point d’entrée `Azure` pour commencer à utiliser les bibliothèques. Lisez l’emplacement du fichier de propriétés via la variable d’environnement.

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



