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
ms.date: 11/21/2018
ms.devlang: java
ms.service: storage
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: storage
ms.openlocfilehash: f94b2981f1e641a6e4b2d9d3028608a56a6590e7
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338873"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="0038e-103">Comment utiliser Spring Boot Starter pour Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0038e-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="0038e-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="0038e-104">Overview</span></span>

<span data-ttu-id="0038e-105">Cet article vous explique comment créer une application personnalisée à l’aide du **Spring Initializr**, puis en ajoutant le démarreur de stockage Azure à votre application, et en utilisant votre application pour charger un blob dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0038e-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0038e-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="0038e-106">Prerequisites</span></span>

<span data-ttu-id="0038e-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0038e-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="0038e-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou vous inscrire pour un [compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0038e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0038e-109">[Azure CLI](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0038e-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="0038e-110">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0038e-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="0038e-111">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="0038e-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="0038e-112">Apache [Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0038e-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="0038e-113">Spring Boot 2.0 ou version ultérieure est requis pour effectuer les différentes étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="0038e-113">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="0038e-114">Créer un compte de stockage Azure et un conteneur de blob pour votre application</span><span class="sxs-lookup"><span data-stu-id="0038e-114">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="0038e-115">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="0038e-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="0038e-116">Cliquez sur **+Créer une ressource**, puis **Stockage**, et cliquez ensuite sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="0038e-116">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Créer un compte de stockage Azure][IMG01]

1. <span data-ttu-id="0038e-118">Sur la page **Créer un espace de noms**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0038e-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="0038e-119">Saisissez un **Nom** unique qui fera partie de l’URI de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0038e-119">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="0038e-120">Par exemple : si vous saisissez **wingtiptoysstorage** comme **Nom**, votre URI sera *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="0038e-120">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="0038e-121">Choisissez **Stockage Blob** comme **Type de compte**.</span><span class="sxs-lookup"><span data-stu-id="0038e-121">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="0038e-122">Précisez l'**Emplacement** de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0038e-122">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="0038e-123">Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0038e-123">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="0038e-124">Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre compte de stockage ou choisissez un groupe de ressources déjà existant.</span><span class="sxs-lookup"><span data-stu-id="0038e-124">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Spécifier les options du compte de stockage Azure][IMG02]

1. <span data-ttu-id="0038e-126">Une fois ces options définies, cliquez sur **Créer** pour créer votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0038e-126">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="0038e-127">Lorsque le portail Azure a créé votre compte de stockage, cliquez sur **Blobs**, puis cliquez sur **+Conteneur**.</span><span class="sxs-lookup"><span data-stu-id="0038e-127">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Création du conteneur d’objets blob][IMG03]

1. <span data-ttu-id="0038e-129">Saisissez un **Nom** pour votre conteneur d’objets blob, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0038e-129">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Spécifiez les options du conteneur d’objets blob][IMG04]

1. <span data-ttu-id="0038e-131">Le portail Azure répertorie votre conteneur d’objets blob une fois qu’il a été créé.</span><span class="sxs-lookup"><span data-stu-id="0038e-131">The Azure portal will list your blob container after is has been created.</span></span>

   ![Revoir la liste des conteneurs d'objets blob][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="0038e-133">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="0038e-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="0038e-134">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="0038e-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="0038e-135">Spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="0038e-135">Specify the following options:</span></span>

   * <span data-ttu-id="0038e-136">Générez un projet **Maven** avec **Java**.</span><span class="sxs-lookup"><span data-stu-id="0038e-136">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="0038e-137">Spécifiez une version de **Spring Boot** égale ou supérieure à 2.0.</span><span class="sxs-lookup"><span data-stu-id="0038e-137">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="0038e-138">Indiquez les noms du **Groupe** et de l’**Artefact** de votre application.</span><span class="sxs-lookup"><span data-stu-id="0038e-138">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="0038e-139">Ajoutez la dépendance **Web**.</span><span class="sxs-lookup"><span data-stu-id="0038e-139">Add the **Web** dependency.</span></span>

      ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="0038e-141">Le Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.wingtiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="0038e-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="0038e-142">Une fois les options ci-dessus définies, cliquez sur **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="0038e-142">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="0038e-143">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0038e-143">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger le projet Spring][SI02]

1. <span data-ttu-id="0038e-145">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="0038e-145">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="0038e-146">Configurer votre application Spring Boot pour utiliser le démarreur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0038e-146">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="0038e-147">Localisez le fichier *pom.xml* dans le répertoire racine de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-147">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="0038e-148">-ou-</span><span class="sxs-lookup"><span data-stu-id="0038e-148">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="0038e-149">Ouvrez le fichier *pom.xml* dans un éditeur de texte, et ajoutez le démarreur de stockage Azure Spring Cloud à la liste des `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="0038e-149">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Modifier le fichier pom.xml][SI03]

1. <span data-ttu-id="0038e-151">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="0038e-151">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="0038e-152">Créer un fichier d’informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="0038e-152">Create an Azure Credential File</span></span>

1. <span data-ttu-id="0038e-153">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="0038e-153">Open a command prompt.</span></span>

1. <span data-ttu-id="0038e-154">Accédez au répertoire des *ressources* de votre application Spring Boot, par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-154">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="0038e-155">-ou-</span><span class="sxs-lookup"><span data-stu-id="0038e-155">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="0038e-156">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="0038e-156">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="0038e-157">Répertoriez vos abonnements :</span><span class="sxs-lookup"><span data-stu-id="0038e-157">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="0038e-158">Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-158">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. Specify the GUID for the subscription you want to use with Azure; for example:

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="0038e-159">Créez votre fichier d’informations d’identification Azure :</span><span class="sxs-lookup"><span data-stu-id="0038e-159">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="0038e-160">Cette commande créera un fichier *my.azureauth* dans votre répertoire des *ressources* avec un contenu similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0038e-160">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="0038e-161">Configurer votre application Spring Boot pour utiliser votre compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0038e-161">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="0038e-162">Localisez le fichier *application.properties* dans le répertoire des *ressources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-162">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="0038e-163">-ou-</span><span class="sxs-lookup"><span data-stu-id="0038e-163">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="0038e-164">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées à votre compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="0038e-164">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="0038e-165">Où :</span><span class="sxs-lookup"><span data-stu-id="0038e-165">Where:</span></span>

   |                   <span data-ttu-id="0038e-166">Champ</span><span class="sxs-lookup"><span data-stu-id="0038e-166">Field</span></span>                   |                                            <span data-ttu-id="0038e-167">Description</span><span class="sxs-lookup"><span data-stu-id="0038e-167">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="0038e-168">Spécifie le fichier d’informations d’identification Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0038e-168">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="0038e-169">Spécifie le groupe de ressources Azure qui contient votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0038e-169">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="0038e-170">Spécifie la région géographique que vous avez indiquée lors de la création de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0038e-170">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="0038e-171">Spécifie le compte de stockage Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0038e-171">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="0038e-172">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="0038e-172">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="0038e-173">Ajouter un exemple de code pour implémenter une fonctionnalité de stockage Azure simple</span><span class="sxs-lookup"><span data-stu-id="0038e-173">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="0038e-174">Dans cette section, vous pouvez créer les classes Java nécessaires au stockage d’un blob dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0038e-174">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="0038e-175">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="0038e-175">Modify the main application class</span></span>

1. <span data-ttu-id="0038e-176">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-176">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="0038e-177">-ou-</span><span class="sxs-lookup"><span data-stu-id="0038e-177">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="0038e-178">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0038e-178">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="0038e-179">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="0038e-179">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="0038e-180">Ajouter une classe de contrôleur web</span><span class="sxs-lookup"><span data-stu-id="0038e-180">Add a web controller class</span></span>

1. <span data-ttu-id="0038e-181">Créez un fichier Java nommé *WebController.java* dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-181">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="0038e-182">-ou-</span><span class="sxs-lookup"><span data-stu-id="0038e-182">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="0038e-183">Ouvrez le fichier Java de contrôleur web dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="0038e-183">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

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

   <span data-ttu-id="0038e-184">Là où la syntaxe `@Value("blob://[container]/[blob]")` définit respectivement les noms du conteneur et des objets blob dans lesquels vous souhaitez stocker les données.</span><span class="sxs-lookup"><span data-stu-id="0038e-184">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="0038e-185">Enregistrez et fermez le fichier Java du contrôleur web.</span><span class="sxs-lookup"><span data-stu-id="0038e-185">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="0038e-186">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-186">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="0038e-187">-ou-</span><span class="sxs-lookup"><span data-stu-id="0038e-187">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="0038e-188">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-188">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="0038e-189">Une fois votre application exécutée, vous pouvez utiliser *curl* pour tester votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0038e-189">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="0038e-190">a.</span><span class="sxs-lookup"><span data-stu-id="0038e-190">a.</span></span> <span data-ttu-id="0038e-191">Envoyez une demande POST pour mettre à jour le contenu d’un fichier :</span><span class="sxs-lookup"><span data-stu-id="0038e-191">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="0038e-192">Vous devriez voir une réponse indiquant que le fichier a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="0038e-192">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="0038e-193">b.</span><span class="sxs-lookup"><span data-stu-id="0038e-193">b.</span></span> <span data-ttu-id="0038e-194">Envoyez une demande GET pour vérifier le contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="0038e-194">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="0038e-195">Vous devriez voir le texte « Hello World » que vous avez envoyé.</span><span class="sxs-lookup"><span data-stu-id="0038e-195">You should see the "Hello World" text that you posted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0038e-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0038e-196">Next steps</span></span>

<span data-ttu-id="0038e-197">Pour plus d’informations sur les instances Spring Boot Starters supplémentaires disponibles pour Microsoft Azure, consultez la section [Pour débuter avec Spring Boot pour Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0038e-197">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="0038e-198">Pour plus d’informations sur l’intégration de la fonctionnalité Azure dans vos applications basées sur Spring, consultez la section [Spring Framework sur Azure](/java/azure/spring-framework/).</span><span class="sxs-lookup"><span data-stu-id="0038e-198">For additional information about integrating Azure functionality into your Spring-based applications, see [Spring Framework on Azure](/java/azure/spring-framework/).</span></span>

<span data-ttu-id="0038e-199">Pour plus de détails sur les API Azure Storage supplémentaires pouvant être appelées à partir de vos applications Spring Boot, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="0038e-199">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="0038e-200">Utilisation du stockage d’objets blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="0038e-200">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="0038e-201">Utilisation du stockage de files d’attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="0038e-201">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="0038e-202">Utilisation du stockage Table Azure à partir de Java</span><span class="sxs-lookup"><span data-stu-id="0038e-202">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="0038e-203">Développer pour Azure Files avec Java</span><span class="sxs-lookup"><span data-stu-id="0038e-203">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
