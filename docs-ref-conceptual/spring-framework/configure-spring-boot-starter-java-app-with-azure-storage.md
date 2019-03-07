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
# <a name="how-to-use-the-spring-boot-starter-for-azure-storage"></a><span data-ttu-id="c084f-103">Comment utiliser Spring Boot Starter pour Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c084f-103">How to use the Spring Boot Starter for Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="c084f-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c084f-104">Overview</span></span>

<span data-ttu-id="c084f-105">Cet article vous explique comment créer une application personnalisée à l’aide du **Spring Initializr**, puis en ajoutant le démarreur de stockage Azure à votre application, et en utilisant votre application pour charger un blob dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c084f-105">This article walks you through creating a custom application using the **Spring Initializr**, then adding the Azure storage starter to your application, and then using your application to upload a blob to your Azure storage account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c084f-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c084f-106">Prerequisites</span></span>

<span data-ttu-id="c084f-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c084f-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="c084f-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou vous inscrire pour un [compte Azure gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c084f-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c084f-109">[Azure CLI](http://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c084f-109">The [Azure Command-Line Interface (CLI)](http://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="c084f-110">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c084f-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="c084f-111">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="c084f-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="c084f-112">Apache [Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c084f-112">Apache's [Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="c084f-113">Spring Boot 2.0 ou version ultérieure est requis pour effectuer les différentes étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="c084f-113">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-storage-account-and-blob-container-for-your-application"></a><span data-ttu-id="c084f-114">Créer un compte de stockage Azure et un conteneur de blob pour votre application</span><span class="sxs-lookup"><span data-stu-id="c084f-114">Create an Azure Storage Account and blob container for your application</span></span>

1. <span data-ttu-id="c084f-115">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="c084f-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="c084f-116">Cliquez sur **+Créer une ressource**, puis **Stockage**, et cliquez ensuite sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="c084f-116">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Créer un compte de stockage Azure][IMG01]

1. <span data-ttu-id="c084f-118">Sur la page **Créer un espace de noms**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c084f-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="c084f-119">Saisissez un **Nom** unique qui fera partie de l’URI de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c084f-119">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="c084f-120">Par exemple : si vous saisissez **wingtiptoysstorage** comme **Nom**, votre URI sera *wingtiptoysstorage.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="c084f-120">For example: if you entered **wingtiptoysstorage** for the **Name**, the URI would be *wingtiptoysstorage.core.windows.net*.</span></span>
   * <span data-ttu-id="c084f-121">Choisissez **Stockage Blob** comme **Type de compte**.</span><span class="sxs-lookup"><span data-stu-id="c084f-121">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="c084f-122">Précisez l'**Emplacement** de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c084f-122">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="c084f-123">Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c084f-123">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="c084f-124">Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre compte de stockage ou choisissez un groupe de ressources déjà existant.</span><span class="sxs-lookup"><span data-stu-id="c084f-124">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Spécifier les options du compte de stockage Azure][IMG02]

1. <span data-ttu-id="c084f-126">Une fois ces options définies, cliquez sur **Créer** pour créer votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="c084f-126">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

1. <span data-ttu-id="c084f-127">Lorsque le portail Azure a créé votre compte de stockage, cliquez sur **Blobs**, puis cliquez sur **+Conteneur**.</span><span class="sxs-lookup"><span data-stu-id="c084f-127">When the Azure portal has created your storage account, click **Blobs**, then click **+Container**.</span></span>

   ![Création du conteneur d’objets blob][IMG03]

1. <span data-ttu-id="c084f-129">Saisissez un **Nom** pour votre conteneur d’objets blob, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c084f-129">Enter a **Name** for your blob container, and then click **OK**.</span></span>

   ![Spécifiez les options du conteneur d’objets blob][IMG04]

1. <span data-ttu-id="c084f-131">Le portail Azure répertorie votre conteneur d’objets blob une fois qu’il a été créé.</span><span class="sxs-lookup"><span data-stu-id="c084f-131">The Azure portal will list your blob container after is has been created.</span></span>

   ![Revoir la liste des conteneurs d'objets blob][IMG05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="c084f-133">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="c084f-133">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="c084f-134">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="c084f-134">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="c084f-135">Spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="c084f-135">Specify the following options:</span></span>

   * <span data-ttu-id="c084f-136">Générez un projet **Maven** avec **Java**.</span><span class="sxs-lookup"><span data-stu-id="c084f-136">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="c084f-137">Spécifiez une version de **Spring Boot** égale ou supérieure à 2.0.</span><span class="sxs-lookup"><span data-stu-id="c084f-137">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="c084f-138">Indiquez les noms du **Groupe** et de l’**Artefact** de votre application.</span><span class="sxs-lookup"><span data-stu-id="c084f-138">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="c084f-139">Ajoutez la dépendance **Web**.</span><span class="sxs-lookup"><span data-stu-id="c084f-139">Add the **Web** dependency.</span></span>

      ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="c084f-141">Le Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.wingtiptoys.storage*.</span><span class="sxs-lookup"><span data-stu-id="c084f-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.storage*.</span></span>
   >

1. <span data-ttu-id="c084f-142">Une fois les options ci-dessus définies, cliquez sur **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="c084f-142">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="c084f-143">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="c084f-143">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger le projet Spring][SI02]

1. <span data-ttu-id="c084f-145">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="c084f-145">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-storage-starter"></a><span data-ttu-id="c084f-146">Configurer votre application Spring Boot pour utiliser le démarreur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c084f-146">Configure your Spring Boot app to use the Azure Storage starter</span></span>

1. <span data-ttu-id="c084f-147">Localisez le fichier *pom.xml* dans le répertoire racine de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-147">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\pom.xml`

   <span data-ttu-id="c084f-148">-ou-</span><span class="sxs-lookup"><span data-stu-id="c084f-148">-or-</span></span>

   `/users/example/home/storage/pom.xml`

1. <span data-ttu-id="c084f-149">Ouvrez le fichier *pom.xml* dans un éditeur de texte, et ajoutez le démarreur de stockage Azure Spring Cloud à la liste des `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="c084f-149">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Storage starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-azure-starter-storage</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Modifier le fichier pom.xml][SI03]

1. <span data-ttu-id="c084f-151">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="c084f-151">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="c084f-152">Créer un fichier d’informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="c084f-152">Create an Azure Credential File</span></span>

1. <span data-ttu-id="c084f-153">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="c084f-153">Open a command prompt.</span></span>

1. <span data-ttu-id="c084f-154">Accédez au répertoire des *ressources* de votre application Spring Boot, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-154">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\storage\src\main\resources
   ```

   <span data-ttu-id="c084f-155">-ou-</span><span class="sxs-lookup"><span data-stu-id="c084f-155">-or-</span></span>

   ```shell
   cd /users/example/home/storage/src/main/resources
   ```

1. <span data-ttu-id="c084f-156">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="c084f-156">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="c084f-157">Répertoriez vos abonnements :</span><span class="sxs-lookup"><span data-stu-id="c084f-157">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="c084f-158">Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-158">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="c084f-159">Spécifiez le GUID de l’abonnement que vous souhaitez utiliser avec Azure, par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-159">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="c084f-160">Créez votre fichier d’informations d’identification Azure :</span><span class="sxs-lookup"><span data-stu-id="c084f-160">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="c084f-161">Cette commande créera un fichier *my.azureauth* dans votre répertoire des *ressources* avec un contenu similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c084f-161">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-storage-account"></a><span data-ttu-id="c084f-162">Configurer votre application Spring Boot pour utiliser votre compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="c084f-162">Configure your Spring Boot app to use your Azure Storage account</span></span>

1. <span data-ttu-id="c084f-163">Localisez le fichier *application.properties* dans le répertoire des *ressources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-163">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\resources\application.properties`

   <span data-ttu-id="c084f-164">-ou-</span><span class="sxs-lookup"><span data-stu-id="c084f-164">-or-</span></span>

   `/users/example/home/storage/src/main/resources/application.properties`

2. <span data-ttu-id="c084f-165">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées à votre compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="c084f-165">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your storage account:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.storage.account=wingtiptoysstorage
   ```
   <span data-ttu-id="c084f-166">Où :</span><span class="sxs-lookup"><span data-stu-id="c084f-166">Where:</span></span>

   |                   <span data-ttu-id="c084f-167">Champ</span><span class="sxs-lookup"><span data-stu-id="c084f-167">Field</span></span>                   |                                            <span data-ttu-id="c084f-168">Description</span><span class="sxs-lookup"><span data-stu-id="c084f-168">Description</span></span>                                            |
   |-------------------------------------------|---------------------------------------------------------------------------------------------------|
   | `spring.cloud.azure.credential-file-path` |            <span data-ttu-id="c084f-169">Spécifie le fichier d’informations d’identification Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c084f-169">Specifies Azure credential file that you created earlier in this tutorial.</span></span>             |
   |    `spring.cloud.azure.resource-group`    |           <span data-ttu-id="c084f-170">Spécifie le groupe de ressources Azure qui contient votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c084f-170">Specifies the Azure Resource Group that contains your Azure Storage account.</span></span>            |
   |        `spring.cloud.azure.region`        | <span data-ttu-id="c084f-171">Spécifie la région géographique que vous avez indiquée lors de la création de votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c084f-171">Specifies the geographical region that you specified when you created your Azure Storage account.</span></span> |
   |   `spring.cloud.azure.storage.account`    |            <span data-ttu-id="c084f-172">Spécifie le compte de stockage Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c084f-172">Specifies Azure Storage account that you created earlier in this tutorial.</span></span>             |


3. <span data-ttu-id="c084f-173">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="c084f-173">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-azure-storage-functionality"></a><span data-ttu-id="c084f-174">Ajouter un exemple de code pour implémenter une fonctionnalité de stockage Azure simple</span><span class="sxs-lookup"><span data-stu-id="c084f-174">Add sample code to implement basic Azure storage functionality</span></span>

<span data-ttu-id="c084f-175">Dans cette section, vous pouvez créer les classes Java nécessaires au stockage d’un blob dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c084f-175">In this section, you create the necessary Java classes for storing a blob in your Azure storage account.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="c084f-176">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="c084f-176">Modify the main application class</span></span>

1. <span data-ttu-id="c084f-177">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-177">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\StorageApplication.java`

   <span data-ttu-id="c084f-178">-ou-</span><span class="sxs-lookup"><span data-stu-id="c084f-178">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/StorageApplication.java`

1. <span data-ttu-id="c084f-179">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c084f-179">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

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

1. <span data-ttu-id="c084f-180">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="c084f-180">Save and close the main application Java file.</span></span>

### <a name="add-a-web-controller-class"></a><span data-ttu-id="c084f-181">Ajouter une classe de contrôleur web</span><span class="sxs-lookup"><span data-stu-id="c084f-181">Add a web controller class</span></span>

1. <span data-ttu-id="c084f-182">Créez un fichier Java nommé *WebController.java* dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-182">Create a new Java file named *WebController.java* in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\storage\src\main\java\com\wingtiptoys\storage\WebController.java`

   <span data-ttu-id="c084f-183">-ou-</span><span class="sxs-lookup"><span data-stu-id="c084f-183">-or-</span></span>

   `/users/example/home/storage/src/main/java/com/wingtiptoys/storage/WebController.java`

1. <span data-ttu-id="c084f-184">Ouvrez le fichier Java de contrôleur web dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c084f-184">Open the web controller Java file in a text editor, and add the following lines to the file:</span></span>

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

   <span data-ttu-id="c084f-185">Là où la syntaxe `@Value("blob://[container]/[blob]")` définit respectivement les noms du conteneur et des objets blob dans lesquels vous souhaitez stocker les données.</span><span class="sxs-lookup"><span data-stu-id="c084f-185">Where the `@Value("blob://[container]/[blob]")` syntax respectively defines the names of the container and blob where you want to store the data.</span></span>

1. <span data-ttu-id="c084f-186">Enregistrez et fermez le fichier Java du contrôleur web.</span><span class="sxs-lookup"><span data-stu-id="c084f-186">Save and close the web controller Java file.</span></span>

1. <span data-ttu-id="c084f-187">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-187">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\storage`

   <span data-ttu-id="c084f-188">-ou-</span><span class="sxs-lookup"><span data-stu-id="c084f-188">-or-</span></span>

   `cd /users/example/home/storage`

1. <span data-ttu-id="c084f-189">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-189">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c084f-190">Une fois votre application exécutée, vous pouvez utiliser *curl* pour tester votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c084f-190">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   <span data-ttu-id="c084f-191">a.</span><span class="sxs-lookup"><span data-stu-id="c084f-191">a.</span></span> <span data-ttu-id="c084f-192">Envoyez une demande POST pour mettre à jour le contenu d’un fichier :</span><span class="sxs-lookup"><span data-stu-id="c084f-192">Send a POST request to update a file's contents:</span></span>

      ```shell
      curl -X POST -H "Content-Type: text/plain" -d "Hello World" http://localhost:8080/
      ```

      <span data-ttu-id="c084f-193">Vous devriez voir une réponse indiquant que le fichier a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="c084f-193">You should see a response that the file was updated.</span></span>

   <span data-ttu-id="c084f-194">b.</span><span class="sxs-lookup"><span data-stu-id="c084f-194">b.</span></span> <span data-ttu-id="c084f-195">Envoyez une demande GET pour vérifier le contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="c084f-195">Send a GET request to verify the file's contents:</span></span>

      ```shell
      curl -X GET http://localhost:8080/
      ```

     <span data-ttu-id="c084f-196">Vous devriez voir le texte « Hello World » que vous avez envoyé.</span><span class="sxs-lookup"><span data-stu-id="c084f-196">You should see the "Hello World" text that you posted.</span></span>

## <a name="summary"></a><span data-ttu-id="c084f-197">Résumé</span><span class="sxs-lookup"><span data-stu-id="c084f-197">Summary</span></span>

<span data-ttu-id="c084f-198">Dans ce didacticiel, vous avez créé une application Java à l’aide de **[Spring Initializr]**, ajouté le démarreur de stockage Azure à votre application, et configuré votre application pour charger un objet blob dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c084f-198">In this tutorial, you created a new Java application using the **[Spring Initializr]**, added the Azure storage starter to your application, and then configured your application to upload a blob to your Azure storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c084f-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c084f-199">Next steps</span></span>

<span data-ttu-id="c084f-200">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="c084f-200">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c084f-201">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="c084f-201">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="c084f-202">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c084f-202">Additional Resources</span></span>

<span data-ttu-id="c084f-203">Pour plus d’informations sur les instances Spring Boot Starters supplémentaires disponibles pour Microsoft Azure, consultez la section [Pour débuter avec Spring Boot pour Azure](spring-boot-starters-for-azure.md).</span><span class="sxs-lookup"><span data-stu-id="c084f-203">For more information about the additional Spring Boot Starters that are available for Microsoft Azure, see [Spring Boot Starters for Azure](spring-boot-starters-for-azure.md).</span></span>

<span data-ttu-id="c084f-204">Pour plus de détails sur les API Azure Storage supplémentaires pouvant être appelées à partir de vos applications Spring Boot, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="c084f-204">For detailed information about additional Azure storage APIs that you can call from your Spring Boot applications, see the following articles:</span></span>
* [<span data-ttu-id="c084f-205">Utilisation du stockage d’objets blob à partir de Java</span><span class="sxs-lookup"><span data-stu-id="c084f-205">How to use Azure Blob storage from Java</span></span>](/azure/storage/blobs/storage-java-how-to-use-blob-storage)
* [<span data-ttu-id="c084f-206">Utilisation du stockage de files d’attente à partir de Java</span><span class="sxs-lookup"><span data-stu-id="c084f-206">How to use Azure Queue storage from Java</span></span>](/azure/storage/queues/storage-java-how-to-use-queue-storage)
* [<span data-ttu-id="c084f-207">Utilisation du stockage Table Azure à partir de Java</span><span class="sxs-lookup"><span data-stu-id="c084f-207">How to use Azure Table storage from Java</span></span>](/azure/cosmos-db/table-storage-how-to-use-java)
* [<span data-ttu-id="c084f-208">Développer pour Azure Files avec Java</span><span class="sxs-lookup"><span data-stu-id="c084f-208">How to use Azure File storage from Java</span></span>](/azure/storage/files/storage-java-how-to-use-file-storage)

<!-- IMG List -->

[IMG01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-01.png
[IMG02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-02.png
[IMG03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-03.png
[IMG04]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-04.png
[IMG05]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-storage-account-05.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-01.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-02.png
[SI03]: ./media/configure-spring-boot-starter-java-app-with-azure-storage/create-project-03.png
