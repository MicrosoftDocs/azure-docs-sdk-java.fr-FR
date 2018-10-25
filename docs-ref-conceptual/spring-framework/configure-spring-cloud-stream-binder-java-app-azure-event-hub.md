---
title: Comment créer une application Spring Cloud Stream Binder avec Azure Event Hubs
description: Découvrez comment configurer une application basée sur Java Spring Cloud Stream Binder développée avec Spring Boot Initializer à l’aide d’Azure Event Hubs.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 09/10/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: dfc3b6121bddcb637735047e2e7bc7485da9a4fe
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799945"
---
# <a name="how-to-create-a-spring-cloud-stream-binder-application-with-azure-event-hubs"></a><span data-ttu-id="2ec8e-103">Comment créer une application Spring Cloud Stream Binder avec Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2ec8e-103">How to create a Spring Cloud Stream Binder application with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="2ec8e-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="2ec8e-104">Overview</span></span>

<span data-ttu-id="2ec8e-105">Cet article vous explique comment configurer une application Java basée sur Spring Cloud Stream Binder développée avec Spring Boot Initializer à l’aide d’Azure Events Hubs.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder application created with the Spring Boot Initializer with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ec8e-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="2ec8e-106">Prerequisites</span></span>

<span data-ttu-id="2ec8e-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="2ec8e-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="2ec8e-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="2ec8e-109">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="2ec8e-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="2ec8e-111">La version 2.0 de Spring Boot ou une version ultérieure est requise pour effectuer les différentes étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-111">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="2ec8e-112">Créer un hub Azure Event Hub à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="2ec8e-112">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="2ec8e-113">Créer un espace de noms Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="2ec8e-113">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="2ec8e-114">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-114">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="2ec8e-115">Cliquez sur **+Créer une ressource**, puis sur **Internet des objets**, et cliquez ensuite sur **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-115">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Créer un espace de noms Azure Event Hub][IMG01]

1. <span data-ttu-id="2ec8e-117">Sur la page **Créer un espace de noms**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-117">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="2ec8e-118">Saisissez un **Nom** unique qui fera partie de l’URI de l’espace de noms de votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-118">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="2ec8e-119">Par exemple : si vous saisissez **wingtiptoys** comme **Nom**, votre URI sera *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-119">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="2ec8e-120">Choisissez un **Niveau tarifaire** pour l’espace de noms de votre hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-120">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="2ec8e-121">Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-121">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="2ec8e-122">Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre espace de noms ou choisissez un groupe de ressources déjà existant.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-122">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="2ec8e-123">Précisez l’**Emplacement** de l’espace de noms de votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-123">Specify the **Location** for your event hub namespace.</span></span>

   ![Spécifier les options de l’espace de noms de votre Event Hub Azure][IMG02]

1. <span data-ttu-id="2ec8e-125">Une fois les options ci-dessus définies, cliquez sur **Créer** pour créer votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-125">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="2ec8e-126">Créer un Hub d’événements Azure dans votre espace de noms</span><span class="sxs-lookup"><span data-stu-id="2ec8e-126">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="2ec8e-127">Accédez au portail Azure à l’adresse <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-127">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="2ec8e-128">Cliquez sur **Toutes les ressources**, puis sur l’espace de noms que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-128">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Sélectionnez l’espace de noms de votre Event Hub Azure][IMG03]

1. <span data-ttu-id="2ec8e-130">Cliquez sur **Event Hubs**, puis sur **+Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-130">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Ajoutez un nouvel hub Azure Event Hub][IMG04]

1. <span data-ttu-id="2ec8e-132">Sur la page **Créer un Event Hub**, saisissez un **Nom** unique pour votre Event Hub, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-132">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Créer un Event Hub Azure][IMG05]

1. <span data-ttu-id="2ec8e-134">Lorsque votre Hub d’événements est créé, il sera répertorié sur la page **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-134">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Créer un Event Hub Azure][IMG06]

### <a name="create-an-azure-storage-account-for-your-event-hub-checkpoints"></a><span data-ttu-id="2ec8e-136">Créez un compte de stockage Azure pour les points de contrôle de votre Hub d’événements</span><span class="sxs-lookup"><span data-stu-id="2ec8e-136">Create an Azure Storage Account for your Event Hub checkpoints</span></span>

1. <span data-ttu-id="2ec8e-137">Accédez au portail Azure à l’adresse <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-137">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="2ec8e-138">Cliquez sur **+ Créer une ressource**, puis **Stockage**, et cliquez ensuite sur **Compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-138">Click **+Create a resource**, then **Storage**, and then click **Storage Account**.</span></span>

   ![Créer un compte de stockage Azure][IMG07]

1. <span data-ttu-id="2ec8e-140">Sur la page **Créer un espace de noms**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-140">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="2ec8e-141">Saisissez un **Nom** unique qui fera partie de l’URI de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-141">Enter a unique **Name**, which will become part of the URI for your storage account.</span></span> <span data-ttu-id="2ec8e-142">Par exemple : si vous saisissez **wingtiptoys** comme **Nom**, votre URI sera *wingtiptoys.core.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-142">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.core.windows.net*.</span></span>
   * <span data-ttu-id="2ec8e-143">Choisissez **Stockage Blob** comme **Type de compte**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-143">Choose **Blob storage** for the **Account kind**.</span></span>
   * <span data-ttu-id="2ec8e-144">Précisez l'**Emplacement** de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-144">Specify the **Location** for your storage account.</span></span>
   * <span data-ttu-id="2ec8e-145">Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-145">Choose the **Subscription** you want to use for your storage account.</span></span>
   * <span data-ttu-id="2ec8e-146">Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre compte de stockage ou choisissez un groupe de ressources déjà existant.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-146">Specify whether to create a new **Resource group** for your storage account, or choose an existing resource group.</span></span>

   ![Spécifier les options du compte de stockage Azure][IMG08]

1. <span data-ttu-id="2ec8e-148">Une fois les options ci-dessus définies, cliquez sur **Créer** pour créer votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-148">When you have specified the options listed above, click **Create** to create your storage account.</span></span>

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="2ec8e-149">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="2ec8e-149">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="2ec8e-150">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-150">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="2ec8e-151">Spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-151">Specify the following options:</span></span>

   * <span data-ttu-id="2ec8e-152">Générez un projet **Maven** avec **Java**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-152">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="2ec8e-153">Spécifiez une version de **Spring Boot** égale ou supérieure à 2.0.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-153">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="2ec8e-154">Indiquez les noms du **Groupe** et de l’**Artefact** de votre application.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-154">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="2ec8e-155">Ajoutez la dépendance **Web**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-155">Add the **Web** dependency.</span></span>

      ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="2ec8e-157">Le Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.wingtiptoys.eventhub*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-157">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.eventhub*.</span></span>
   >

1. <span data-ttu-id="2ec8e-158">Une fois les options ci-dessus définies, cliquez sur **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-158">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="2ec8e-159">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-159">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger le projet Spring][SI02]

1. <span data-ttu-id="2ec8e-161">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-161">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-azure-event-hub-starter"></a><span data-ttu-id="2ec8e-162">Configurer votre application Spring Boot pour utiliser le starter Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="2ec8e-162">Configure your Spring Boot app to use the Azure Event Hub starter</span></span>

1. <span data-ttu-id="2ec8e-163">Localisez le fichier *pom.xml* dans le répertoire racine de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-163">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\pom.xml`

   <span data-ttu-id="2ec8e-164">-ou-</span><span class="sxs-lookup"><span data-stu-id="2ec8e-164">-or-</span></span>

   `/users/example/home/eventhub/pom.xml`

1. <span data-ttu-id="2ec8e-165">Ouvrez le fichier *pom.xml* dans un éditeur de texte, et ajoutez le starter Spring Cloud Azure Event Hub Stream Binder à la liste des `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-165">Open the *pom.xml* file in a text editor, and add the Spring Cloud Azure Event Hub Stream Binder starter to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-eventhub-stream-binder</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Modifier le fichier pom.xml][SI03]

1. <span data-ttu-id="2ec8e-167">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-167">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="2ec8e-168">Créer un fichier d’informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="2ec8e-168">Create an Azure Credential File</span></span>

1. <span data-ttu-id="2ec8e-169">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-169">Open a command prompt.</span></span>

1. <span data-ttu-id="2ec8e-170">Accédez au répertoire des *ressources* de votre application Spring Boot, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-170">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="2ec8e-171">-ou-</span><span class="sxs-lookup"><span data-stu-id="2ec8e-171">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="2ec8e-172">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-172">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="2ec8e-173">Répertoriez vos abonnements :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-173">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="2ec8e-174">Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-174">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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

1. <span data-ttu-id="2ec8e-175">Créez votre fichier d’informations d’identification Azure :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-175">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="2ec8e-176">Cette commande créera un fichier *my.azureauth* dans votre répertoire des *ressources* avec un contenu similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-176">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="2ec8e-177">Configurer votre application Spring Boot pour utiliser Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="2ec8e-177">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="2ec8e-178">Localisez le fichier *application.properties* dans le répertoire des *ressources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-178">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="2ec8e-179">-ou-</span><span class="sxs-lookup"><span data-stu-id="2ec8e-179">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="2ec8e-180">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées à votre Event Hub :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-180">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace
   spring.cloud.azure.eventhub.checkpoint-storage-account=wingtiptoysstorage
   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   spring.cloud.stream.eventhub.bindings.input.consumer.checkpoint-mode=MANUAL
   ```
   <span data-ttu-id="2ec8e-181">Où :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-181">Where:</span></span>

   |                          <span data-ttu-id="2ec8e-182">Champ</span><span class="sxs-lookup"><span data-stu-id="2ec8e-182">Field</span></span>                           |                                                                                   <span data-ttu-id="2ec8e-183">Description</span><span class="sxs-lookup"><span data-stu-id="2ec8e-183">Description</span></span>                                                                                    |
   |----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |        `spring.cloud.azure.credential-file-path`         |                                                    <span data-ttu-id="2ec8e-184">Spécifie le fichier d’informations d’identification Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-184">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |           `spring.cloud.azure.resource-group`            |                                                      <span data-ttu-id="2ec8e-185">Spécifie le groupe de ressources Azure qui contient votre Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-185">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |               `spring.cloud.azure.region`                |                                           <span data-ttu-id="2ec8e-186">Spécifie la région géographique que vous avez indiquée lors de la création de votre Hub d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-186">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |         `spring.cloud.azure.eventhub.namespace`          |                                          <span data-ttu-id="2ec8e-187">Spécifie le nom unique que vous avez choisi lors de la création de votre Hub d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-187">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.azure.eventhub.checkpoint-storage-account` |                                                    <span data-ttu-id="2ec8e-188">Spécifie le compte de stockage Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-188">Specifies Azure Storage Account that you created earlier in this tutorial.</span></span>                                                    |
   |     `spring.cloud.stream.bindings.input.destination`     |                            <span data-ttu-id="2ec8e-189">Spécifie la destination d’entrée Azure Event Hub, qui, dans le cas présent, est le hub que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-189">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |       `spring.cloud.stream.bindings.input.group `        | <span data-ttu-id="2ec8e-190">Spécifie un groupe de consommateurs d’un Event Hub Azure, qui peut être défini comme « $Default » afin d’utiliser le groupe de consommateurs de base généré lors de la création de votre Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-190">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   |    `spring.cloud.stream.bindings.output.destination`     |                               <span data-ttu-id="2ec8e-191">Spécifie l’Event Hub Azure qui servira de destination de sortie. Dans le cas présent, il sera identique à la destination d’entrée.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-191">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="2ec8e-192">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-192">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="2ec8e-193">Ajouter un exemple de code pour implémenter une fonctionnalité Event Hub de base</span><span class="sxs-lookup"><span data-stu-id="2ec8e-193">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="2ec8e-194">Dans cette section, vous créez les classes Java nécessaires à l’envoi d’événements dans votre hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-194">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="2ec8e-195">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="2ec8e-195">Modify the main application class</span></span>

1. <span data-ttu-id="2ec8e-196">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-196">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\java\com\wingtiptoys\eventhub\EventhubApplication.java`

   <span data-ttu-id="2ec8e-197">-ou-</span><span class="sxs-lookup"><span data-stu-id="2ec8e-197">-or-</span></span>

   `/users/example/home/eventhub/src/main/java/com/wingtiptoys/eventhub/EventhubApplication.java`

1. <span data-ttu-id="2ec8e-198">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-198">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class EventhubApplication {
      public static void main(String[] args) {
         SpringApplication.run(EventhubApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="2ec8e-199">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-199">Save and close the main application Java file.</span></span>

### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="2ec8e-200">Créer une nouvelle classe pour le connecteur source</span><span class="sxs-lookup"><span data-stu-id="2ec8e-200">Create a new class for the source connector</span></span>

1. <span data-ttu-id="2ec8e-201">Créez un nouveau ficher Java intitulé *EventhubSource.java* dans le répertoire du package de votre application, ouvrez ensuite ce fichier dans un éditeur de texte et ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-201">Create a new Java file named *EventhubSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class EventhubSource {

      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String postMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```
1. <span data-ttu-id="2ec8e-202">Enregistrez et fermez le fichier *EventhubSource.java*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-202">Save and close the *EventhubSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="2ec8e-203">Créez une nouvelle classe pour le connecteur du récepteur</span><span class="sxs-lookup"><span data-stu-id="2ec8e-203">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="2ec8e-204">Créez un nouveau ficher Java intitulé *EventhubSink.java* dans le répertoire de package de votre application, ouvrez ensuite ce fichier dans un éditeur de texte et ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-204">Create a new Java file named *EventhubSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.eventhub;

   import com.microsoft.azure.spring.integration.core.AzureHeaders;
   import com.microsoft.azure.spring.integration.core.api.Checkpointer;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;
   import org.springframework.messaging.handler.annotation.Header;

   @EnableBinding(Sink.class)
   public class EventhubSink {

      private static final Logger LOGGER = LoggerFactory.getLogger(EventhubSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message, @Header(AzureHeaders.CHECKPOINTER) Checkpointer checkpointer) {
         LOGGER.info("New message received: '{}'", message);
         checkpointer.success().handle((r, ex) -> {
            if (ex == null) {
               LOGGER.info("Message '{}' successfully checkpointed", message);
            }
            return null;
         });
      }
   }
   ```

1. <span data-ttu-id="2ec8e-205">Enregistrez et fermez le fichier *EventhubSink.java*.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-205">Save and close the *EventhubSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="2ec8e-206">Générez et testez votre application</span><span class="sxs-lookup"><span data-stu-id="2ec8e-206">Build and test your application</span></span>

1. <span data-ttu-id="2ec8e-207">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-207">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\eventhub`

   <span data-ttu-id="2ec8e-208">-ou-</span><span class="sxs-lookup"><span data-stu-id="2ec8e-208">-or-</span></span>

   `cd /users/example/home/eventhub`

1. <span data-ttu-id="2ec8e-209">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-209">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="2ec8e-210">Une fois votre application exécutée, vous pouvez utiliser *curl* pour tester votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-210">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="2ec8e-211">Vous devriez voir « hello » publié dans les journaux de votre application.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-211">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="2ec8e-212">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="2ec8e-212">For example:</span></span>

   ```shell
   [Thread-13] INFO com.wingtiptoys.eventhub.EventhubSink - New message received: 'hello'
   [pool-10-thread-7] INFO com.wingtiptoys.eventhub.EventhubSink - Message 'hello' successfully checkpointed
   ```

## <a name="next-steps"></a><span data-ttu-id="2ec8e-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ec8e-213">Next steps</span></span>

<span data-ttu-id="2ec8e-214">Pour plus d’informations sur la prise en charge Azure pour Event Hub Stream Binder, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="2ec8e-214">For more information about Azure support for Event Hub Stream Binder, see the following articles:</span></span>

* [<span data-ttu-id="2ec8e-215">Nouveautés des concentrateurs d’événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="2ec8e-215">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="2ec8e-216">Créer un espace de noms Event Hubs et un concentrateur d’événements avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2ec8e-216">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="2ec8e-217">Comment utiliser le starter Spring Boot pour Apache Kafka avec Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2ec8e-217">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>](configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub.md)

<span data-ttu-id="2ec8e-218">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="2ec8e-218">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="2ec8e-219">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-219">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="2ec8e-220">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-220">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="2ec8e-221">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-221">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="2ec8e-222">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="2ec8e-222">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-azure-event-hub/create-project-03.png
