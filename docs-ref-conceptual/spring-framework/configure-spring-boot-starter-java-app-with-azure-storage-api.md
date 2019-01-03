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
ms.date: 12/19/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: 984a3edb89608c806537f991b42e309f31130896
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991443"
---
# <a name="how-to-use-the-spring-boot-starter-with-the-azure-storage-api"></a><span data-ttu-id="69216-103">Comment utiliser le démarreur Spring Boot avec une API de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="69216-103">How to use the Spring Boot Starter with the Azure Storage API</span></span>

## <a name="overview"></a><span data-ttu-id="69216-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="69216-104">Overview</span></span>

<span data-ttu-id="69216-105">Cet article vous présente la création d’une application personnalisée à l’aide de la solution **Spring Initializr**, puis vous explique comment utiliser cette application pour accéder au stockage Azure à l’aide de l’API de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="69216-105">This article walks you through creating a custom application using the **Spring Initializr**, and then using that application to access Azure storage by using the Azure Storage API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="69216-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="69216-106">Prerequisites</span></span>

<span data-ttu-id="69216-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="69216-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="69216-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou vous inscrire pour un [compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69216-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="69216-109">[Azure CLI](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69216-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="69216-110">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="69216-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="69216-111">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="69216-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="69216-112">Apache [Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="69216-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="69216-113">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="69216-113">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="69216-114">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="69216-114">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="69216-115">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="69216-115">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Options de base de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-basic.png)

   > [!NOTE]
   >
   > <span data-ttu-id="69216-117">Spring Initializr utilisera les noms de **Groupe** et d’**Artefact** pour créer le nom du package ; par exemple : *com.contoso.wingtiptoysdemo*.</span><span class="sxs-lookup"><span data-stu-id="69216-117">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.contoso.wingtiptoysdemo*.</span></span>
   >

1. <span data-ttu-id="69216-118">Faites défilez jusqu’à la section **Azure**, puis cochez la case **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="69216-118">Scroll down to the **Azure** section and check the box for **Azure Storage**.</span></span>

   ![Options complètes de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-advanced.png)

1. <span data-ttu-id="69216-120">Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="69216-120">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Options complètes de Spring Initializr](media/configure-spring-boot-starter-java-app-with-azure-storage/spring-initializr-generate.png)

1. <span data-ttu-id="69216-122">À l’invite, téléchargez le projet vers un emplacement sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="69216-122">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé](media/configure-spring-boot-starter-java-app-with-azure-storage/download-app.png)

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="69216-124">Se connecter à Azure et sélectionner l’abonnement à utiliser</span><span class="sxs-lookup"><span data-stu-id="69216-124">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="69216-125">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="69216-125">Open a command prompt.</span></span>

1. <span data-ttu-id="69216-126">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="69216-126">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="69216-127">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="69216-127">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="69216-128">Répertoriez vos abonnements :</span><span class="sxs-lookup"><span data-stu-id="69216-128">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="69216-129">Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-129">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="69216-130">Spécifiez le GUID du compte que vous souhaitez utiliser avec Azure, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-130">Specify the GUID for the account you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="69216-131">Création d'un compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="69216-131">Create an Azure Storage account</span></span>

1. <span data-ttu-id="69216-132">Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans cet article, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-132">Create a resource group for the Azure resources you will use in this article; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="69216-133">Où :</span><span class="sxs-lookup"><span data-stu-id="69216-133">Where:</span></span>

   | <span data-ttu-id="69216-134">Paramètre</span><span class="sxs-lookup"><span data-stu-id="69216-134">Parameter</span></span> | <span data-ttu-id="69216-135">Description</span><span class="sxs-lookup"><span data-stu-id="69216-135">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="69216-136">Spécifie un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="69216-136">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="69216-137">Spécifie la [Région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="69216-137">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="69216-138">L’interface Azure CLI affiche les résultats de la création de votre groupe de ressources ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-138">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

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

2. <span data-ttu-id="69216-139">Créez un compte Azure Storage dans le groupe de ressources associé à votre application Spring Boot, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-139">Create an Azure storage account in the in the resource group for your Spring Boot app; for example:</span></span>
   ```azurecli
   az storage account create --name wingtiptoysstorage --resource-group wingtiptoysresources --location westus --sku Standard_LRS
   ```
   <span data-ttu-id="69216-140">Où :</span><span class="sxs-lookup"><span data-stu-id="69216-140">Where:</span></span>

   | <span data-ttu-id="69216-141">Paramètre</span><span class="sxs-lookup"><span data-stu-id="69216-141">Parameter</span></span> | <span data-ttu-id="69216-142">Description</span><span class="sxs-lookup"><span data-stu-id="69216-142">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="69216-143">Spécifie un nom unique pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="69216-143">Specifies a unique name for your storage account.</span></span> |
   | `resource-group` | <span data-ttu-id="69216-144">Spécifie le nom du groupe de ressources créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="69216-144">Specifies the name of the resource group group you created in the previous step.</span></span> |
   | `location` | <span data-ttu-id="69216-145">Spécifie la [région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="69216-145">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your storage account will be hosted.</span></span> |
   | `sku` | <span data-ttu-id="69216-146">Spécifie l’une des valeurs suivantes : `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span><span class="sxs-lookup"><span data-stu-id="69216-146">Specifies one of the following: `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, `Standard_ZRS`.</span></span> |

   <span data-ttu-id="69216-147">Azure renvoie une longue chaîne JSON comportant l’état d’approvisionnement, par exemple : |</span><span class="sxs-lookup"><span data-stu-id="69216-147">Azure will return a long JSON string which contains the provisioning state; for example: |</span></span>

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

3. <span data-ttu-id="69216-148">Récupérez la chaîne de connexion associée à votre compte de stockage, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-148">Retrieve the connection string for your storage account; for example:</span></span>
   ```azurecli
   az storage account show-connection-string --name wingtiptoysstorage --resource-group wingtiptoysresources
   ```
   <span data-ttu-id="69216-149">Où :</span><span class="sxs-lookup"><span data-stu-id="69216-149">Where:</span></span>

   | <span data-ttu-id="69216-150">Paramètre</span><span class="sxs-lookup"><span data-stu-id="69216-150">Parameter</span></span> | <span data-ttu-id="69216-151">Description</span><span class="sxs-lookup"><span data-stu-id="69216-151">Description</span></span> |
   | ---|---|
   | `name` | <span data-ttu-id="69216-152">Spécifie un nom unique pour le compte de stockage créé lors des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="69216-152">Specifies a unique name of the storage account you created in previous steps.</span></span> |
   | `resource-group` | <span data-ttu-id="69216-153">Spécifie le nom du groupe de ressources créé lors des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="69216-153">Specifies the name of the resource group you created in previous steps.</span></span> |

   <span data-ttu-id="69216-154">Azure renvoie une chaîne JSON comportant la chaîne de connexion associée à votre compte de stockage, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-154">Azure will return a JSON string which contains the connection string for your storage account; for example:</span></span>

   ```json
   {
     "connectionString": "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz=="
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="69216-155">Configurer et compiler votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="69216-155">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="69216-156">Extrayez les fichiers de l’archive du projet téléchargé dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="69216-156">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="69216-157">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="69216-157">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="69216-158">Ajoutez la clé de votre compte de stockage, par exemple :</span><span class="sxs-lookup"><span data-stu-id="69216-158">Add the key for your storage account; for example:</span></span>
   ```yaml
   azure.storage.connection-string=DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=wingtiptoysstorage;AccountKey=AbCdEfGhIjKlMnOpQrStUvWxYz==
   ```

1. <span data-ttu-id="69216-159">Accédez au dossier */src/main/java/com/example/wingtiptoysdemo* de votre projet, puis ouvrez le fichier *WingtiptoysdemoApplication.java* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="69216-159">Navigate to the */src/main/java/com/example/wingtiptoysdemo* folder in your project and open the *WingtiptoysdemoApplication.java* file in a text editor.</span></span>

1. <span data-ttu-id="69216-160">Remplacez le code Java existant par l’exemple suivant qui répertorie les objets blob dans un conteneur :</span><span class="sxs-lookup"><span data-stu-id="69216-160">Replace the existing Java code with the following example that lists the blobs in a container:</span></span>

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
   > <span data-ttu-id="69216-161">L’exemple ci-dessus transfère automatiquement les paramétrages du compte de stockage définis dans le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="69216-161">The above example autowires the storage account settings that you defined in the *application.properties* file.</span></span>
   >

1. <span data-ttu-id="69216-162">Compilez et exécutez l’application :</span><span class="sxs-lookup"><span data-stu-id="69216-162">Compile and run the application:</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

   <span data-ttu-id="69216-163">L’application crée un conteneur et charge un fichier texte en tant qu’objet blob dans le conteneur, qui sera répertorié sous votre compte de stockage dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="69216-163">The application will create a container and upload a text file as a blob to the container, which will be listed under your storage account in the [Azure portal](https://portal.azure.com).</span></span>

   ![Répertorier les objets blob dans le portail Azure](media/configure-spring-boot-starter-java-app-with-azure-storage/list-blobs-in-portal.png)

   > [!NOTE]
   > 
   > <span data-ttu-id="69216-165">Lorsque vous compilez votre application, le message d’erreur suivant peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="69216-165">When you compile your application, you might see the following error message:</span></span>
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
   > <span data-ttu-id="69216-166">Le cas échéant, vous avez intérêt à désactiver la procédure de test Maven Surefire ; pour ce faire, ajoutez l’entrée suivante de plug-in dans votre fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="69216-166">If this happens, you might want to disable the Maven Surefire testing; to do so, add the following plugin entry in your *pom.xml* file:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="69216-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="69216-167">Next steps</span></span>

<span data-ttu-id="69216-168">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="69216-168">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="69216-169">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="69216-169">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="69216-170">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="69216-170">Additional Resources</span></span>

<span data-ttu-id="69216-171">Pour plus d’informations sur les instances Spring Boot Starters supplémentaires disponibles pour Microsoft Azure, consultez la section [Pour débuter avec Spring Boot pour Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="69216-171">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="69216-172">Pour plus d’informations sur l’intégration de la fonctionnalité Azure dans vos applications basées sur Spring, consultez la section [Spring Framework sur Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="69216-172">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="69216-173">Pour plus de détails sur les API Azure Storage supplémentaires pouvant être appelées à partir de vos applications Spring Boot, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="69216-173">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="69216-174">Utilisation du stockage d’objets blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="69216-174">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="69216-175">Utilisation du stockage de files d’attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="69216-175">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="69216-176">Utilisation du stockage Table Azure à partir de Java</span><span class="sxs-lookup"><span data-stu-id="69216-176">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="69216-177">Développer pour Azure Files avec Java</span><span class="sxs-lookup"><span data-stu-id="69216-177">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)
