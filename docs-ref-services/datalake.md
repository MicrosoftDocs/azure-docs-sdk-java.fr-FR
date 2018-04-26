---
title: Bibliothèques Azure Data Lake Store pour Java
description: Documentation de référence pour les bibliothèques Java Data Lake Store
keywords: Azure, Java, SDK, API, big data, data lake
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: data-lake-store
ms.openlocfilehash: bcd1fd17759f7d171006d7b2126019d00d06d1db
ms.sourcegitcommit: 49b17bbf34732512f836ee634818f1058147ff5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-data-lake-store-libraries-for-java"></a><span data-ttu-id="1ee97-104">Bibliothèques Azure Data Lake Store pour Java</span><span class="sxs-lookup"><span data-stu-id="1ee97-104">Azure Data Lake Store libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="1ee97-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1ee97-105">Overview</span></span>

<span data-ttu-id="1ee97-106">Capturez des données quels que soient leur taille, leur type et leur ingestion dans un emplacement unique pour les analyser avec [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="1ee97-106">Capture data of any size, type, and ingestion speed in a single place for analytics with [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

<span data-ttu-id="1ee97-107">Pour découvrir Data Lake Store, consultez la section [Prise en main d’Azure Data Lake Store à l’aide de Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span><span class="sxs-lookup"><span data-stu-id="1ee97-107">To get started with Data Lake Store, see [Get started with Azure Data Lake Store using Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).</span></span>


## <a name="client-library"></a><span data-ttu-id="1ee97-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="1ee97-108">Client library</span></span>

<span data-ttu-id="1ee97-109">Lisez et écrivez des fichiers, définissez les autorisations et les métadonnées, et gérez des fichiers et des répertoires dans Data Lake Store avec la bibliothèque cliente.</span><span class="sxs-lookup"><span data-stu-id="1ee97-109">Read and write files, set permissions and metadata, and manage files and directories in Data Lake Store with the client library.</span></span>

<span data-ttu-id="1ee97-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="1ee97-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="1ee97-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="1ee97-111">Example</span></span>

<span data-ttu-id="1ee97-112">Créez un client Data Lake à partir d’un nom de domaine complet et d’un jeton d’accès OAuth2. Créez ensuite un fichier dans Data Lake pour écrire dedans.</span><span class="sxs-lookup"><span data-stu-id="1ee97-112">Create a Data Lake client from a fully qualified domain name and OAuth2 access token, then create a file in Data Lake and write to it.</span></span>

```java
// AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);
ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

// create directory
client.createDirectory("/a/b/w");
        
// create file and write some content
String filename = "/a/b/c.txt";
OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
PrintStream out = new PrintStream(stream);
for (int i = 1; i <= 10; i++) {
    out.println("This is line #" + i);
    out.format("This is the same line (%d), but using formatted output. %n", i);
}
out.close();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ee97-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="1ee97-113">Explore the Client APIs</span></span>](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a><span data-ttu-id="1ee97-114">API de gestion</span><span class="sxs-lookup"><span data-stu-id="1ee97-114">Management API</span></span>

<span data-ttu-id="1ee97-115">Utilisez l’API de gestion pour gérer les comptes Data Lake Store, les règles de pare-feu et les fournisseurs d’identité approuvés.</span><span class="sxs-lookup"><span data-stu-id="1ee97-115">Use the management API to manage Data Lake Store accounts, firewall rules, and trusted identity providers.</span></span>

<span data-ttu-id="1ee97-116">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="1ee97-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1ee97-117">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="1ee97-117">Explore the Management APIs</span></span>](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="1ee97-118">Exemples</span><span class="sxs-lookup"><span data-stu-id="1ee97-118">Samples</span></span>

<span data-ttu-id="1ee97-119">[Prise en main d’Azure Data Lake][1]</span><span class="sxs-lookup"><span data-stu-id="1ee97-119">[Azure Data Lake Get Started][1]</span></span> 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

<span data-ttu-id="1ee97-120">Explorez d’autres [exemples de code Java pour Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="1ee97-120">Explore more [sample Java code for Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) you can use in your apps.</span></span>
