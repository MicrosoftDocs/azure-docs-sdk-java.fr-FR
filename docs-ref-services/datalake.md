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
ms.locfileid: "31823722"
---
# <a name="azure-data-lake-store-libraries-for-java"></a>Bibliothèques Azure Data Lake Store pour Java

## <a name="overview"></a>Vue d'ensemble

Capturez des données quels que soient leur taille, leur type et leur ingestion dans un emplacement unique pour les analyser avec [Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

Pour découvrir Data Lake Store, consultez la section [Prise en main d’Azure Data Lake Store à l’aide de Java](/azure/data-lake-store/data-lake-store-get-started-java-sdk).


## <a name="client-library"></a>Bibliothèque cliente

Lisez et écrivez des fichiers, définissez les autorisations et les métadonnées, et gérez des fichiers et des répertoires dans Data Lake Store avec la bibliothèque cliente.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```XML
<dependency>
   <groupId>com.microsoft.azure</groupId>
   <artifactId>azure-data-lake-store-sdk</artifactId>
   <version>2.1.5</version>
</dependency>
```   

## <a name="example"></a>Exemples

Créez un client Data Lake à partir d’un nom de domaine complet et d’un jeton d’accès OAuth2. Créez ensuite un fichier dans Data Lake pour écrire dedans.

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
> [Explorer les API clientes](/java/api/overview/azure/datalakestore/client)


## <a name="management-api"></a>API de gestion

Utilisez l’API de gestion pour gérer les comptes Data Lake Store, les règles de pare-feu et les fournisseurs d’identité approuvés.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.


```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-datalake-store</artifactId>
    <version>1.0.0-beta1.3</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/datalakestore/management)

## <a name="samples"></a>Exemples

[Prise en main d’Azure Data Lake][1] 

[1]: https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started

Explorez d’autres [exemples de code Java pour Azure Data Lake Store](https://azure.microsoft.com/resources/samples/?platform=java&term=lake) que vous pouvez utiliser avec vos applications.
