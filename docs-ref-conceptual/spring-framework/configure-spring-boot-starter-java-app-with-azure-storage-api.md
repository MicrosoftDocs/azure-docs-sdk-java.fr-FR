---
title: Comment utiliser le démarreur Spring Boot avec une API de stockage Azure
description: Découvrez comment configurer une application d’initialisation Spring Boot avec l’API de stockage Azure.
services: storage
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 94f7b1148d9282d33bc67da0e0d97a284a81d4d4
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339053"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-storage-api"></a>Comment utiliser le démarreur Spring Boot avec une API de stockage Azure

## <a name="overview"></a>Vue d’ensemble

Cet article vous présente la création d’une application personnalisée à l’aide de la solution **Spring Initializr**, puis vous explique comment utiliser cette application pour accéder au stockage Azure à l’aide de l’API de stockage Azure.

## <a name="prerequisites"></a>Prérequis

Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou vous inscrire pour un [compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).
* [Azure CLI](http://docs.microsoft.com/cli/azure/overview).
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* Apache [Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Créer une application personnalisée à l’aide de Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.

   ![Options de base de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > Spring Initializr utilisera les noms de **Groupe** et d’**Artefact** pour créer le nom du package ; par exemple : *com.contoso.wingtiptoysdemo*.
   >

1. Faites défilez jusqu’à la section **Azure**, puis cochez la case **Azure Storage**.

   ![Options complètes de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.

   ![Options complètes de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. À l’invite, téléchargez le projet vers un emplacement sur votre ordinateur local.

   ![Télécharger un projet Spring Boot personnalisé](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Se connecter à Azure et sélectionner l’abonnement à utiliser

1. Ouvrez une invite de commandes.

1. Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :

   ```azurecli
   az login
   ```
   Suivez les instructions pour terminer le processus de connexion.

1. Répertoriez vos abonnements :

   ```azurecli
   az account list
   ```
   Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. Spécifiez le GUID du compte que vous souhaitez utiliser avec Azure, par exemple :

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a>Création d'un compte Azure Storage

1. Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans cet article, par exemple :
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `name` | Spécifie un nom unique pour votre groupe de ressources. |
   | `location` | Spécifie la [Région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre groupe de ressources. |

   L’interface Azure CLI affiche les résultats de la création de votre groupe de ressources ; par exemple :  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

2. Créez un compte Azure Storage dans le groupe de ressources associé à votre application Spring Boot, par exemple :
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `name` | Spécifie un nom unique pour votre compte de stockage. |
   | `resource-group` | Spécifie le nom du groupe de ressources créé à l’étape précédente. |
   | `location` | Spécifie la [région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre compte de stockage. |
   | `sku` | Spécifie l’une des valeurs suivantes : `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`. |

   Azure renvoie une longue chaîne JSON comportant l’état d’approvisionnement, par exemple : |

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "identity": null,
     "kind": "Storage"
       ...
       ... (A long list of values will be displayed here.)
       ...
     "statusOfPrimary": "available",
     "statusOfSecondary": null,
     "tags": {},
     "type": "Microsoft.Storage/storageAccounts"
   }
   ```

3. Récupérez la chaîne de connexion associée à votre compte de stockage, par exemple :
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   Où :

   | Paramètre | Description |
   | ---|---|
   | `name` | Spécifie un nom unique pour le compte de stockage créé lors des étapes précédentes. |
   | `resource-group` | Spécifie le nom du groupe de ressources créé lors des étapes précédentes. |

   Azure renvoie une chaîne JSON comportant la chaîne de connexion associée à votre compte de stockage, par exemple :

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurer et compiler votre application Spring Boot

1. Extrayez les fichiers de l’archive du projet téléchargé dans un répertoire.

1. Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.

1. Ajoutez la clé de votre compte de stockage, par exemple :
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. Accédez au dossier */src/main/java/com/example/wingtiptoysdemo* de votre projet, puis ouvrez le fichier *WingtiptoysdemoApplication.java* dans un éditeur de texte.

1. Remplacez le code Java existant par l’exemple suivant qui répertorie les objets blob dans un conteneur :

   ```java
   package com.example.wingtiptoysdemo;

   import com.microsoft.azure.storage.*;
   import com.microsoft.azure.storage.blob.*;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   import java.net.URISyntaxException;

   @SpringBootApplication
   public class WingtiptoysdemoApplication implements CommandLineRunner {

      @Autowired
      private CloudStorageAccount cloudStorageAccount;

      final String containerName = "mycontainer";

      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysdemoApplication.class, args);
      }

      public void run(String... var1)
             throws URISyntaxException, StorageException {
          // Create a container (if it does not exist).
          createContainerIfNotExists(containerName);
          // Upload a blob to the container.
          uploadTextBlob(containerName);
      }

      private void createContainerIfNotExists(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Create the container if it does not exist.
            container.createIfNotExists();
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }

      private void uploadTextBlob(String containerName)
            throws URISyntaxException, StorageException {
         try
         {
            // Create a blob client.
            final CloudBlobClient blobClient = cloudStorageAccount.createCloudBlobClient();
            // Get a reference to a container. (Name must be lower case.)
            final CloudBlobContainer container = blobClient.getContainerReference(containerName);
            // Get a blob reference for a text file.
            CloudBlockBlob blob = container.getBlockBlobReference("test.txt");
            // Upload some text into the blob.
            blob.uploadText("Hello World!");
         }
         catch (Exception e)
         {
            // Output the stack trace.
            e.printStackTrace();
         }
      }
   }
   ```
   > [!NOTE]
   >
   > L’exemple ci-dessus transfère automatiquement les paramétrages du compte de stockage définis dans le fichier *application.properties*.
   >

1. Compilez et exécutez l’application :
   ```shell
   mvn clean package spring-boot:run
   ```

   L’application crée un conteneur et charge un fichier texte en tant qu’objet blob dans le conteneur, qui sera répertorié sous votre compte de stockage dans le [portail Azure](https://portal.azure.com).

   ![Répertorier les objets blob dans le portail Azure](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > Lorsque vous compilez votre application, le message d’erreur suivant peut s’afficher :
   > 
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] BUILD FAILURE`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[INFO] Total time: 2.616 s`<br/>
   > `[INFO] Finished at: 2017-11-11T13:14:15Z`<br/>
   > `[INFO] Final Memory: 26M/213M`<br/>
   > `[INFO] ------------------------------------------------------------------------`<br/>
   > `[ERROR] Failed to execute goal org.apache.maven.plugins:maven-surefire-plugin:2`<br/>
   > `.18.1:test (default-test) on project wingtiptoysdemo: Execution default-test of`<br/>
   > `goal org.apache.maven.plugins:maven-surefire-plugin:2.18.1:test failed: The for`<br/>
   > `ked VM terminated without properly saying goodbye. VM crash or System.exit called?`<br/>
   > `[ERROR] Command was /bin/sh -c cd /home/robert/SpringBoot/wingtiptoysdemo && /u`<br/>
   > `sr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -jar /home/robert/SpringBoot/wingt`<br/>
   > `iptoysdemo/target/surefire/surefirebooter6371623993063346766.jar /home/robert/S`<br/>
   > `pringBoot/wingtiptoysdemo/target/surefire/surefire5107893623933537917tmp /home/`<br/>
   > `robert/SpringBoot/wingtiptoysdemo/target/surefire/surefire_01414159391084128068tmp`<br/>
   > `[ERROR] -> [Help 1]`<br/>
   > 
   > Le cas échéant, vous avez intérêt à désactiver la procédure de test Maven Surefire ; pour ce faire, ajoutez l’entrée suivante de plug-in dans votre fichier *pom.xml* :
   > 
   > ```xml
   > <plugin>
   >   <groupId>org.apache.maven.plugins</groupId>
   >   <artifactId>maven-surefire-plugin</artifactId>
   >   <version>2.20.1</version>
   >   <configuration>
   >     <skipTests>true</skipTests>
   >   </configuration>
   > </plugin>
   > ```
   > 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les instances Spring Boot Starters supplémentaires disponibles pour Microsoft Azure, consultez la section [Pour débuter avec Spring Boot pour Azure](spring-boot-starters-for-azure.md).

Pour plus d’informations sur l’intégration de la fonctionnalité Azure dans vos applications basées sur Spring, consultez la section [Spring Framework sur Azure](/java/azure/spring-framework/).

Pour plus de détails sur les API Azure Storage supplémentaires pouvant être appelées à partir de vos applications Spring Boot, consultez les articles suivants :
* [Utilisation du stockage d’objets blob à partir de Java](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [Utilisation du stockage de files d’attente à partir de Java](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [Utilisation du stockage Table Azure à partir de Java](/azure/cosmos-db/table-storage-how-to-use-java)
* [Développer pour Azure Files avec Java](/azure/storage/files/storage-java-how-to-use-file-storage)
