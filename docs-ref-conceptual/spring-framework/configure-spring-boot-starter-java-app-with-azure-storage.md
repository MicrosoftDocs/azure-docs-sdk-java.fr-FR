---
title: Comment utiliser Spring Boot Starter pour Azure Storage
description: Découvrez comment configurer une application d’initialisation Spring Boot avec l’application de démarrage Azure Storage.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: a1f35df5939a51fa5ce50c29752226b6c7649a9d
ms.sourcegitcommit: 1c1412ad5d8960975c3fc7fd3d1948152ef651ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57335382"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a>Comment utiliser Spring Boot Starter pour Azure Storage

## <a name="overview"></a>Vue d’ensemble

Cet article vous explique comment créer une application personnalisée à l’aide du **Spring Initializr**, puis en ajoutant le démarreur de stockage Azure à votre application, et en utilisant votre application pour charger un blob dans votre compte de stockage Azure.

## <a name="prerequisites"></a>Prérequis

Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou vous inscrire pour un [compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).
* [Azure CLI](http://docs.microsoft.com/cli/azure/overview).
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* Apache [Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

> [!IMPORTANT]
>
> Spring Boot 2.0 ou version ultérieure est requis pour effectuer les différentes étapes de cet article.
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a>Créer un compte de stockage Azure et un conteneur de blob pour votre application

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **+Créer une ressource**, puis **Stockage**, et cliquez ensuite sur **Compte de stockage**.

   ![Créer un compte de stockage Azure][IMG01]

1. Sur la page **Créer un espace de noms**, saisissez les informations suivantes :

   * Saisissez un **Nom** unique qui fera partie de l’URI de votre compte de stockage. Par exemple : si vous saisissez **wingtiptoysstorage** comme **Nom**, votre URI sera *wingtiptoysstorage.core.windows.net*.
   * Choisissez **Stockage Blob** comme **Type de compte**.
   * Précisez l'**Emplacement** de votre compte de stockage.
   * Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre compte de stockage.
   * Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre compte de stockage ou choisissez un groupe de ressources déjà existant.

   ![Spécifier les options du compte de stockage Azure][IMG02]

1. Une fois ces options définies, cliquez sur **Créer** pour créer votre compte de stockage.

1. Lorsque le portail Azure a créé votre compte de stockage, cliquez sur **Blobs**, puis cliquez sur **+Conteneur**.

   ![Création du conteneur d’objets blob][IMG03]

1. Saisissez un **Nom** pour votre conteneur d’objets blob, puis cliquez sur **OK**.

   ![Spécifiez les options du conteneur d’objets blob][IMG04]

1. Le portail Azure répertorie votre conteneur d’objets blob une fois qu’il a été créé.

   ![Revoir la liste des conteneurs d'objets blob][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Créer une application Spring Boot simple avec Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Spécifiez les options suivantes :

   * Générez un projet **Maven** avec **Java**.
   * Spécifiez une version de **Spring Boot** égale ou supérieure à 2.0.
   * Indiquez les noms du **Groupe** et de l’**Artefact** de votre application.
   * Ajoutez la dépendance **Web**.

      ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Le Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.wingtiptoys.storage*.
   >

1. Une fois les options ci-dessus définies, cliquez sur **Générer le projet**.

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

   ![Télécharger le projet Spring][SI02]

1. Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a>Configurer votre application Spring Boot pour utiliser le démarreur de stockage Azure

1. Localisez le fichier *pom.xml* dans le répertoire racine de votre application. Par exemple :

   `C:\SpringBoot\storage\pom.xml`

   -ou-

   `/users/example/home/storage/pom.xml`

1. Ouvrez le fichier *pom.xml* dans un éditeur de texte, et ajoutez le démarreur de stockage Azure Spring Cloud à la liste des `<dependencies>` :

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Modifier le fichier pom.xml][SI03]

1. Enregistrez et fermez le fichier *pom.xml*.

## <a name="create-an-azure-credential-file"></a>Créer un fichier d’informations d’identification Azure

1. Ouvrez une invite de commandes.

1. Accédez au répertoire des *ressources* de votre application Spring Boot, par exemple :

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   -ou-

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. Connectez-vous à votre compte Azure :

   ```azurecli
   az login
   ```

1. Répertoriez vos abonnements :

   ```azurecli
   az account list
   ```
   Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. Spécifiez le GUID de l’abonnement que vous souhaitez utiliser avec Azure, par exemple :

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Créez votre fichier d’informations d’identification Azure :

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   Cette commande créera un fichier *my.azureauth* dans votre répertoire des *ressources* avec un contenu similaire à l’exemple suivant :

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a>Configurer votre application Spring Boot pour utiliser votre compte de stockage Azure

1. Localisez le fichier *application.properties* dans le répertoire des *ressources* de votre application. Par exemple :

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   -ou-

   `/users/example/home/storage/src/main/resources/application.properties`

2. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées à votre compte de stockage :

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   Où :

   |                   Champ                   |                                            Description                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            Spécifie le fichier d’informations d’identification Azure que vous avez précédemment créé dans ce didacticiel.             |
   |    `spring.cloud.azure.resource-group`    |           Spécifie le groupe de ressources Azure qui contient votre compte de stockage Azure.            |
   |        `spring.cloud.azure.region`        | Spécifie la région géographique que vous avez indiquée lors de la création de votre compte de stockage Azure. |
   |   `spring.cloud.azure.storage.account`    |            Spécifie le compte de stockage Azure que vous avez précédemment créé dans ce didacticiel.             |


3. Enregistrez et fermez le fichier *application.properties*.

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a>Ajouter un exemple de code pour implémenter une fonctionnalité de stockage Azure simple

Dans cette section, vous pouvez créer les classes Java nécessaires au stockage d’un blob dans votre compte de stockage Azure.

### <a name="modify-the-main-application-class"></a>Modifiez la classe d’application principale

1. Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   -ou-

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class StorageApplication {
      public static void main(String[] args) {
         SpringApplication.run(StorageApplication.class, args);
      }
   }
   ```

1. Enregistrez et fermez le fichier Java principal de l’application.

### <a name="add-a-web-controller-class"></a>Ajouter une classe de contrôleur web

1. Créez un fichier Java nommé *WebController.java* dans le répertoire de package de votre application. Par exemple :

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   -ou-

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. Ouvrez le fichier Java de contrôleur web dans un éditeur de texte, puis ajoutez-y les lignes suivantes :

   ```java
   package com.wingtiptoys.storage;

   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.core.io.Resource;
   import org.springframework.core.io.WritableResource;
   import org.springframework.util.StreamUtils;
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   import java.io.IOException;
   import java.io.OutputStream;
   import java.nio.charset.Charset;

   @RestController
   public class WebController {

      @Value("blob://test/myfile.txt")
      private Resource blobFile;

      @GetMapping(value = "/")
      public String readBlobFile() throws IOException {
         return StreamUtils.copyToString(
            this.blobFile.getInputStream(),
            Charset.defaultCharset()) + "\n";
      }

      @PostMapping(value = "/")
      public String writeBlobFile(@RequestBody String data) throws IOException {
         try (OutputStream os = ((WritableResource) this.blobFile).getOutputStream()) {
            os.write(data.getBytes());
         }
         return "File was updated.\n";
      }
   }
   ```

   Là où la syntaxe `@Value("blob://[container]/[blob]")` définit respectivement les noms du conteneur et des objets blob dans lesquels vous souhaitez stocker les données.

1. Enregistrez et fermez le fichier Java du contrôleur web.

1. Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :

   `cd C:\SpringBoot\storage`

   -ou-

   `cd /users/example/home/storage`

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Une fois votre application exécutée, vous pouvez utiliser *curl* pour tester votre application. Par exemple :

   a. Envoyez une demande POST pour mettre à jour le contenu d’un fichier :

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      Vous devriez voir une réponse indiquant que le fichier a été mis à jour.

   b. Envoyez une demande GET pour vérifier le contenu du fichier :

      ```shell
      curl -X GET http://localhost:8080/
      ```

     Vous devriez voir le texte « Hello World » que vous avez envoyé.

## <a name="summary"></a>Résumé

Dans ce didacticiel, vous avez créé une application Java à l’aide de **[Spring Initializr]**, ajouté le démarreur de stockage Azure à votre application, et configuré votre application pour charger un objet blob dans votre compte de stockage Azure.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur les instances Spring Boot Starters supplémentaires disponibles pour Microsoft Azure, consultez la section [Pour débuter avec Spring Boot pour Azure](spring-boot-starters-for-azure.md).

Pour plus de détails sur les API Azure Storage supplémentaires pouvant être appelées à partir de vos applications Spring Boot, consultez les articles suivants :
* [Utilisation du stockage d’objets blob à partir de Java](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [Utilisation du stockage de files d’attente à partir de Java](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [Utilisation du stockage Table Azure à partir de Java](/azure/cosmos-db/table-storage-how-to-use-java)
* [Développer pour Azure Files avec Java](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
