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
ms.openlocfilehash: 3808c6d56b04f28c84a89a25219e4ec523f87964
ms.sourcegitcommit: 61030d025614b084e897809e603b2ec79900ec8d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2018
---
# <a name="authenticate-with-the-azure-libraries-for-java"></a><span data-ttu-id="df7f1-104">S’authentifier avec les bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="df7f1-104">Authenticate with the Azure libraries for Java</span></span> 

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="df7f1-105">Se connecter aux services avec des chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="df7f1-105">Connect to services with connection strings</span></span>

<span data-ttu-id="df7f1-106">La plupart des bibliothèques de service Azure utilisent une chaîne de connexion ou une clé sécurisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="df7f1-106">Most Azure service libraries use a connection string or secure key for authentication.</span></span> <span data-ttu-id="df7f1-107">Par exemple, SQL Database inclut les informations de nom d’utilisateur et de mot de passe dans la chaîne de connexion JDBC :</span><span class="sxs-lookup"><span data-stu-id="df7f1-107">For example, SQL Database includes username and password information in the JDBC connection string:</span></span>

```java
String url = "jdbc:sqlserver://myazuredb.database.windows.net:1433;" + 
        "database=testjavadb;" + 
        "user=myazdbuser;" +
        "password=myazdbpass;" +
        "encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";
        Connection conn = DriverManager.getConnection(url);
```

<span data-ttu-id="df7f1-108">Le stockage Azure utilise une clé de stockage pour autoriser l’application :</span><span class="sxs-lookup"><span data-stu-id="df7f1-108">Azure Storage uses a storage key to authorize the application:</span></span>

```java
final String storageConnection = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName 
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";
```

<span data-ttu-id="df7f1-109">Les chaînes de connexion de service sont utilisées pour s’authentifier auprès d’autres services Azure tels que [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Cache Redis](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started) et [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span><span class="sxs-lookup"><span data-stu-id="df7f1-109">Service connection strings are used to authenticate to other Azure services like [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/sql-api-java-application#UseService), [Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-java-get-started), and [Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-java-how-to-use-queues).</span></span> <span data-ttu-id="df7f1-110">Vous pouvez obtenir les chaînes de connexion à l’aide du portail Azure ou Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="df7f1-110">You can get the connection strings using the Azure portal or the CLI.</span></span>  <span data-ttu-id="df7f1-111">Vous pouvez aussi utiliser les bibliothèques de gestion Azure pour Java pour interroger des ressources et générer des chaînes de connexion dans votre code.</span><span class="sxs-lookup"><span data-stu-id="df7f1-111">You can also use the Azure management libraries for Java to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="df7f1-112">Par exemple, ce code utilise les bibliothèques de gestion pour créer une chaîne de connexion de compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="df7f1-112">For example, this code uses the management libraries to create a storage account connection string:</span></span>

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

<span data-ttu-id="df7f1-113">D’autres bibliothèques ont besoin que votre application s’exécute avec un [principal de service](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) qui l’autorise à s’exécuter avec des informations d’identification accordées.</span><span class="sxs-lookup"><span data-stu-id="df7f1-113">Other libraries require your application to run with a [service prinicpal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="df7f1-114">Cette configuration est similaire à celle de l’authentification basée sur un objet pour les bibliothèques de gestion répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="df7f1-114">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

<a name="mgmt-auth"></a>

##  <a name="authenticate-with-the-azure-management-libraries-for-java"></a><span data-ttu-id="df7f1-115">S’authentifier avec les bibliothèques de gestion Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="df7f1-115">Authenticate with the Azure management libraries for Java</span></span>

<span data-ttu-id="df7f1-116">Vous pouvez authentifier votre application avec Azure de deux façons, lorsque vous utilisez les bibliothèques de gestion Java pour créer et gérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="df7f1-116">Two options are available to authenticate your application with Azure when using the Java management libraries to create and manage resources.</span></span>

### <a name="authenticate-with-an-applicationtokencredentials-object"></a><span data-ttu-id="df7f1-117">S’authentifier avec un objet ApplicationTokenCredentials</span><span class="sxs-lookup"><span data-stu-id="df7f1-117">Authenticate with an ApplicationTokenCredentials object</span></span>

<span data-ttu-id="df7f1-118">Créez une instance de l’objet `ApplicationTokenCredentials` pour fournir les informations d’identification du principal de service à l’objet `Azure` de niveau supérieur à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="df7f1-118">Create an instance of `ApplicationTokenCredentials` to supply the service principal credentials to the top-level `Azure` object from inside your code.</span></span>

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

<span data-ttu-id="df7f1-119">Les valeurs `client`, `tenant` et `key` sont les mêmes valeurs du principal de service utilisées lors d’une [authentification basée sur un fichier](#mgmt-file).</span><span class="sxs-lookup"><span data-stu-id="df7f1-119">The `client`, `tenant` and `key` are the same service principal values used with [file-based authentication](#mgmt-file).</span></span> <span data-ttu-id="df7f1-120">La valeur `AzureEnvironment.AZURE` crée des informations d’identification contre le cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="df7f1-120">The `AzureEnvironment.AZURE` value creates credentials against the Azure public cloud.</span></span> <span data-ttu-id="df7f1-121">Remplacez-la par une autre valeur, si vous avez besoin d’accéder à un autre cloud (par exemple, `AzureEnvironment.AZURE_GERMANY`).</span><span class="sxs-lookup"><span data-stu-id="df7f1-121">Change this to a different value if you need to access another cloud (for example, `AzureEnvironment.AZURE_GERMANY`).</span></span>  

 <span data-ttu-id="df7f1-122">Lisez les valeurs du principal de service depuis des variables d’environnement ou un stockage de gestion de secret tels que [Key Vault](/azure/key-vault/key-vault-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="df7f1-122">Read the service principal values from environment variables or a secret management store like [Key Vault](/azure/key-vault/key-vault-whatis.md).</span></span> <span data-ttu-id="df7f1-123">Évitez d’utiliser ces valeurs sous forme de chaînes de texte en clair dans votre code pour éviter toute exposition accidentelle d’informations d’identification dans votre historique de contrôle de version.</span><span class="sxs-lookup"><span data-stu-id="df7f1-123">Avoid setting these values as cleartext strings in your code to prevent accidentally exposing credentials in your version control history.</span></span>   

<a name="mgmt-file"></a>

### <a name="file-based-authentication-preview"></a><span data-ttu-id="df7f1-124">Authentification basée sur un fichier (version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="df7f1-124">File based authentication (Preview)</span></span>

<span data-ttu-id="df7f1-125">La méthode d’authentification la plus simple consiste à créer un fichier de propriétés qui contient les informations d’identification d’un [principal de service Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) en utilisant le format suivant :</span><span class="sxs-lookup"><span data-stu-id="df7f1-125">The simplest way to authenticate is to create a properties file that contains credentials for an [Azure service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) using the following format:</span></span>

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

- <span data-ttu-id="df7f1-126">abonnement : utilisez la valeur *id* de `az account show` dans Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="df7f1-126">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="df7f1-127">client : utilisez la valeur *appId* de la sortie d’un principal de service créé pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="df7f1-127">client: use the *appId* value from the output taken from a service principal created to run the application.</span></span> <span data-ttu-id="df7f1-128">Si votre application ne dispose pas d’un principal de service, [créez-en un avec Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="df7f1-128">If you don't have a service principal for your app, [create one with the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli).</span></span>
- <span data-ttu-id="df7f1-129">clé : utilisez la valeur *password* du principal de service pour créer la sortie CLI</span><span class="sxs-lookup"><span data-stu-id="df7f1-129">key: use the *password* value from the service principal create CLI output</span></span> 
- <span data-ttu-id="df7f1-130">abonné : utilisez la valeur *tenant* du principal de service pour créer la sortie CLI</span><span class="sxs-lookup"><span data-stu-id="df7f1-130">tenant: use the *tenant* value from the service principal create CLI output</span></span>

<span data-ttu-id="df7f1-131">Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire.</span><span class="sxs-lookup"><span data-stu-id="df7f1-131">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="df7f1-132">Définissez une variable d’environnement avec le chemin complet du fichier dans l’interpréteur de commande :</span><span class="sxs-lookup"><span data-stu-id="df7f1-132">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="df7f1-133">Créez l’objet de point d’entrée `Azure` pour commencer à utiliser les bibliothèques.</span><span class="sxs-lookup"><span data-stu-id="df7f1-133">Create the entry point `Azure` object to start working with the libraries.</span></span> <span data-ttu-id="df7f1-134">Lisez l’emplacement du fichier de propriétés via la variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="df7f1-134">Read the location of the properties file through the environment variable.</span></span>

```java
// pull in the location of the authenticaiton properties file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```



