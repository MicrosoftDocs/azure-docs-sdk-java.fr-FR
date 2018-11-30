---
title: Comment utiliser le démarreur Spring Boot pour Apache Kafka avec Azure Event Hubs
description: Découvrez comment configurer une application créée avec Spring Boot Initializr pour utiliser Apache Kafka avec Azure Event Hubs.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: ab465b56c05c7d480109fc97a4f1c74beaf53856
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339113"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a><span data-ttu-id="dd87c-103">Comment utiliser le démarreur Spring Boot pour Apache Kafka avec Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="dd87c-103">How to use the Spring Boot Starter for Apache Kafka with Azure Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="dd87c-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="dd87c-104">Overview</span></span>

<span data-ttu-id="dd87c-105">Cet article vous explique comment configurer un Stream Binder Spring Cloud basé sur Java développé avec l’initialiseur Spring Boot pour utiliser [Apache Kafka] avec Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="dd87c-105">This article demonstrates how to configure a Java-based Spring Cloud Stream Binder created with the Spring Boot Initializer to use [Apache Kafka] with Azure Event Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd87c-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="dd87c-106">Prerequisites</span></span>

<span data-ttu-id="dd87c-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dd87c-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="dd87c-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="dd87c-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="dd87c-109">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dd87c-109">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="dd87c-110">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="dd87c-110">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="dd87c-111">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="dd87c-111">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="dd87c-112">Spring Boot 2.0 ou version ultérieure est requis pour effectuer les différentes étapes de cet article.</span><span class="sxs-lookup"><span data-stu-id="dd87c-112">Spring Boot version 2.0 or greater is required to complete the steps in this article.</span></span>
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a><span data-ttu-id="dd87c-113">Créer un hub Azure Event Hub à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd87c-113">Create an Azure Event Hub using the Azure portal</span></span>

### <a name="create-an-azure-event-hub-namespace"></a><span data-ttu-id="dd87c-114">Créer un espace de noms Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="dd87c-114">Create an Azure Event Hub Namespace</span></span>

1. <span data-ttu-id="dd87c-115">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="dd87c-115">Browse to the Azure portal at <https://portal.azure.com/> and sign in.</span></span>

1. <span data-ttu-id="dd87c-116">Cliquez sur **+Créer une ressource**, puis sur **Internet des objets**, et cliquez ensuite sur **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-116">Click **+Create a resource**, then **Internet of Things**, and then click **Event Hubs**.</span></span>

   ![Créer un espace de noms Azure Event Hub][IMG01]

1. <span data-ttu-id="dd87c-118">Sur la page **Créer un espace de noms**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd87c-118">On the **Create Namespace** page, enter the following information:</span></span>

   * <span data-ttu-id="dd87c-119">Saisissez un **Nom** unique qui fera partie de l’URI de l’espace de noms de votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="dd87c-119">Enter a unique **Name**, which will become part of the URI for your event hub namespace.</span></span> <span data-ttu-id="dd87c-120">Par exemple : si vous saisissez **wingtiptoys** comme **Nom**, votre URI sera *wingtiptoys.servicebus.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="dd87c-120">For example: if you entered **wingtiptoys** for the **Name**, the URI would be *wingtiptoys.servicebus.windows.net*.</span></span>
   * <span data-ttu-id="dd87c-121">Choisissez un **Niveau tarifaire** pour l’espace de noms de votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="dd87c-121">Choose a **Pricing tier** for your event hub namespace.</span></span>
   * <span data-ttu-id="dd87c-122">Spécifiez **Activer Kafka** pour votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="dd87c-122">Specify **Enable Kafka** for your namespace.</span></span>
   * <span data-ttu-id="dd87c-123">Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="dd87c-123">Choose the **Subscription** you want to use for your namespace.</span></span>
   * <span data-ttu-id="dd87c-124">Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre espace de noms ou choisissez un groupe de ressources déjà existant.</span><span class="sxs-lookup"><span data-stu-id="dd87c-124">Specify whether to create a new **Resource group** for your namespace, or choose an existing resource group.</span></span>
   * <span data-ttu-id="dd87c-125">Précisez l’**Emplacement** de l’espace de noms de votre Event Hub.</span><span class="sxs-lookup"><span data-stu-id="dd87c-125">Specify the **Location** for your event hub namespace.</span></span>

   ![Spécifier les options de l’espace de noms de votre Event Hub Azure][IMG02]

1. <span data-ttu-id="dd87c-127">Une fois les options ci-dessus définies, cliquez sur **Créer** pour créer votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="dd87c-127">When you have specified the options listed above, click **Create** to create your namespace.</span></span>

### <a name="create-an-azure-event-hub-in-your-namespace"></a><span data-ttu-id="dd87c-128">Créer un Hub d’événements Azure dans votre espace de noms</span><span class="sxs-lookup"><span data-stu-id="dd87c-128">Create an Azure Event Hub in your namespace</span></span>

1. <span data-ttu-id="dd87c-129">Accédez au portail Azure à l’adresse <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="dd87c-129">Browse to the Azure portal at <https://portal.azure.com/>.</span></span>

1. <span data-ttu-id="dd87c-130">Cliquez sur **Toutes les ressources**, puis sur l’espace de noms que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="dd87c-130">Click **All resources**, and then click the namespace that you created.</span></span>

   ![Sélectionnez l’espace de noms de votre Event Hub Azure][IMG03]

1. <span data-ttu-id="dd87c-132">Cliquez sur **Event Hubs**, puis sur **+Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-132">Click **Event Hubs**, and then click **+Event Hub**.</span></span>

   ![Ajoutez un nouvel hub Azure Event Hub][IMG04]

1. <span data-ttu-id="dd87c-134">Sur la page **Créer un Event Hub**, saisissez un **Nom** unique pour votre Event Hub, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-134">On the **Create Event Hub** page, enter a unique **Name** for your Event Hub, and then click **Create**.</span></span>

   ![Créer un Event Hub Azure][IMG05]

1. <span data-ttu-id="dd87c-136">Lorsque votre Hub d’événements est créé, il sera répertorié sur la page **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-136">When your Event Hub has been created, it will be listed on the **Event Hubs** page.</span></span>

   ![Créer un Event Hub Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="dd87c-138">Créer une application Spring Boot simple avec Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="dd87c-138">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="dd87c-139">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="dd87c-139">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="dd87c-140">Spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd87c-140">Specify the following options:</span></span>

   * <span data-ttu-id="dd87c-141">Générez un projet **Maven** avec **Java**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-141">Generate a **Maven** project with **Java**.</span></span>
   * <span data-ttu-id="dd87c-142">Spécifiez une version de **Spring Boot** égale ou supérieure à 2.0.</span><span class="sxs-lookup"><span data-stu-id="dd87c-142">Specify a **Spring Boot** version that is equal to or greater than 2.0.</span></span>
   * <span data-ttu-id="dd87c-143">Indiquez les noms du **Groupe** et de l’**Artefact** de votre application.</span><span class="sxs-lookup"><span data-stu-id="dd87c-143">Specify the **Group** and **Artifact** names for your application.</span></span>
   * <span data-ttu-id="dd87c-144">Ajoutez la dépendance **Web**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-144">Add the **Web** dependency.</span></span>

      ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="dd87c-146">Le Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.wingtiptoys.kafka*.</span><span class="sxs-lookup"><span data-stu-id="dd87c-146">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.wingtiptoys.kafka*.</span></span>
   >

1. <span data-ttu-id="dd87c-147">Une fois les options ci-dessus définies, cliquez sur **Générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="dd87c-147">When you have specified the options listed above, click **Generate Project**.</span></span>

1. <span data-ttu-id="dd87c-148">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="dd87c-148">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger le projet Spring][SI02]

1. <span data-ttu-id="dd87c-150">Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="dd87c-150">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a><span data-ttu-id="dd87c-151">Configurez votre application Spring Boot pour utiliser le flux Kafka Spring Cloud et les démarreurs d’Event Hub Azure</span><span class="sxs-lookup"><span data-stu-id="dd87c-151">Configure your Spring Boot app to use the Spring Cloud Kafka Stream and Azure Event Hub starters</span></span>

1. <span data-ttu-id="dd87c-152">Localisez le fichier *pom.xml* dans le répertoire racine de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-152">Locate the *pom.xml* file in the root directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\pom.xml`

   <span data-ttu-id="dd87c-153">-ou-</span><span class="sxs-lookup"><span data-stu-id="dd87c-153">-or-</span></span>

   `/users/example/home/kafka/pom.xml`

1. <span data-ttu-id="dd87c-154">Ouvrez le fichier *pom.xml* dans un éditeur de texte, et ajoutez le flux Kafka Spring Cloud et les démarreurs Event Hub Azure à la liste des `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="dd87c-154">Open the *pom.xml* file in a text editor, and add the Spring Cloud Kafka Stream and Azure Event Hub starters to the list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Modifier le fichier pom.xml][SI03]

1. <span data-ttu-id="dd87c-156">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="dd87c-156">Save and close the *pom.xml* file.</span></span>

## <a name="create-an-azure-credential-file"></a><span data-ttu-id="dd87c-157">Créer un fichier d’informations d’identification Azure</span><span class="sxs-lookup"><span data-stu-id="dd87c-157">Create an Azure Credential File</span></span>

1. <span data-ttu-id="dd87c-158">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="dd87c-158">Open a command prompt.</span></span>

1. <span data-ttu-id="dd87c-159">Accédez au répertoire des *ressources* de votre application Spring Boot, par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-159">Navigate to the *resources* directory of your Spring Boot app; for example:</span></span>

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   <span data-ttu-id="dd87c-160">-ou-</span><span class="sxs-lookup"><span data-stu-id="dd87c-160">-or-</span></span>

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. <span data-ttu-id="dd87c-161">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="dd87c-161">Sign in to your Azure account:</span></span>

   ```azurecli
   az login
   ```

1. <span data-ttu-id="dd87c-162">Répertoriez vos abonnements :</span><span class="sxs-lookup"><span data-stu-id="dd87c-162">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="dd87c-163">Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-163">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

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
   
1. <span data-ttu-id="dd87c-164">Spécifiez le GUID de l’abonnement que vous souhaitez utiliser avec Azure, par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-164">Specify the GUID for the subscription you want to use with Azure; for example:</span></span>

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. <span data-ttu-id="dd87c-165">Créez votre fichier d’informations d’identification Azure :</span><span class="sxs-lookup"><span data-stu-id="dd87c-165">Create your Azure Credential file:</span></span>

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   <span data-ttu-id="dd87c-166">Cette commande créera un fichier *my.azureauth* dans votre répertoire des *ressources* avec un contenu similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dd87c-166">This command will create a *my.azureauth* file in your *resources* directory with contents that resemble the following example:</span></span>

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

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a><span data-ttu-id="dd87c-167">Configurer votre application Spring Boot pour utiliser Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="dd87c-167">Configure your Spring Boot app to use your Azure Event Hub</span></span>

1. <span data-ttu-id="dd87c-168">Localisez le fichier *application.properties* dans le répertoire des *ressources* de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-168">Locate the *application.properties* in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   <span data-ttu-id="dd87c-169">-ou-</span><span class="sxs-lookup"><span data-stu-id="dd87c-169">-or-</span></span>

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. <span data-ttu-id="dd87c-170">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées à votre Event Hub :</span><span class="sxs-lookup"><span data-stu-id="dd87c-170">Open the *application.properties* file in a text editor, add the following lines, and then replace the sample values with the appropriate properties for your event hub:</span></span>

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   <span data-ttu-id="dd87c-171">Où :</span><span class="sxs-lookup"><span data-stu-id="dd87c-171">Where:</span></span>

   |                       <span data-ttu-id="dd87c-172">Champ</span><span class="sxs-lookup"><span data-stu-id="dd87c-172">Field</span></span>                       |                                                                                   <span data-ttu-id="dd87c-173">Description</span><span class="sxs-lookup"><span data-stu-id="dd87c-173">Description</span></span>                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    <span data-ttu-id="dd87c-174">Spécifie le fichier d’informations d’identification Azure que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dd87c-174">Specifies Azure credential file that you created earlier in this tutorial.</span></span>                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      <span data-ttu-id="dd87c-175">Spécifie le groupe de ressources Azure qui contient votre Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="dd87c-175">Specifies the Azure Resource Group that contains your Azure Event Hub.</span></span>                                                      |
   |            `spring.cloud.azure.region`            |                                           <span data-ttu-id="dd87c-176">Spécifie la région géographique que vous avez indiquée lors de la création de votre Hub d’événements Azure.</span><span class="sxs-lookup"><span data-stu-id="dd87c-176">Specifies the geographical region that you specified when you created your Azure Event Hub.</span></span>                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          <span data-ttu-id="dd87c-177">Spécifie le nom unique que vous avez choisi lors de la création de l’espace de noms de votre Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="dd87c-177">Specifies the unique name that you specified when you created your Azure Event Hub Namespace.</span></span>                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            <span data-ttu-id="dd87c-178">Spécifie l’Event Hub Azure qui servira de destination d’entrée. Dans le cas présent, il s’agit du hub que vous avez précédemment créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dd87c-178">Specifies the input destination Azure Event Hub, which for this tutorial is the  hub you created earlier in this tutorial.</span></span>                            |
   |    `spring.cloud.stream.bindings.input.group `    | <span data-ttu-id="dd87c-179">Spécifie un groupe de consommateurs d’un Event Hub Azure, qui peut être défini comme « $Default » afin d’utiliser le groupe de consommateurs de base généré lors de la création de votre Event Hub Azure.</span><span class="sxs-lookup"><span data-stu-id="dd87c-179">Specifies a Consumer Group from Azure Event Hub, which can be set to '$Default' in order to use the basic consumer group that was created when you created your Azure Event Hub.</span></span> |
   | `spring.cloud.stream.bindings.output.destination` |                               <span data-ttu-id="dd87c-180">Spécifie l’Event Hub Azure qui servira de destination de sortie. Dans le cas présent, il sera identique à la destination d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dd87c-180">Specifies the output destination Azure Event Hub, which for this tutorial will be the same as the input destination.</span></span>                               |


3. <span data-ttu-id="dd87c-181">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="dd87c-181">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a><span data-ttu-id="dd87c-182">Ajouter un exemple de code pour implémenter une fonctionnalité Event Hub de base</span><span class="sxs-lookup"><span data-stu-id="dd87c-182">Add sample code to implement basic event hub functionality</span></span>

<span data-ttu-id="dd87c-183">Dans cette section, vous créez les classes Java nécessaires à l’envoi d’événements dans votre hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="dd87c-183">In this section, you create the necessary Java classes for sending events to your event hub.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="dd87c-184">Modifiez la classe d’application principale</span><span class="sxs-lookup"><span data-stu-id="dd87c-184">Modify the main application class</span></span>

1. <span data-ttu-id="dd87c-185">Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-185">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   <span data-ttu-id="dd87c-186">-ou-</span><span class="sxs-lookup"><span data-stu-id="dd87c-186">-or-</span></span>

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. <span data-ttu-id="dd87c-187">Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd87c-187">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. <span data-ttu-id="dd87c-188">Enregistrez et fermez le fichier Java principal de l’application.</span><span class="sxs-lookup"><span data-stu-id="dd87c-188">Save and close the main application Java file.</span></span>


### <a name="create-a-new-class-for-the-source-connector"></a><span data-ttu-id="dd87c-189">Créer une nouvelle classe pour le connecteur source</span><span class="sxs-lookup"><span data-stu-id="dd87c-189">Create a new class for the source connector</span></span>

1. <span data-ttu-id="dd87c-190">Créez un nouveau ficher Java intitulé *KafkaSource.java* dans le répertoire de package de votre application. Ouvrez ensuite ce fichier dans un éditeur de texte et ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd87c-190">Create a new Java file named *KafkaSource.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. <span data-ttu-id="dd87c-191">Enregistrez et fermez le fichier *KafkaSource.java*.</span><span class="sxs-lookup"><span data-stu-id="dd87c-191">Save and close the *KafkaSource.java* file.</span></span>

### <a name="create-a-new-class-for-the-sink-connector"></a><span data-ttu-id="dd87c-192">Créez une nouvelle classe pour le connecteur récepteur</span><span class="sxs-lookup"><span data-stu-id="dd87c-192">Create a new class for the sink connector</span></span>

1. <span data-ttu-id="dd87c-193">Créez un nouveau ficher Java intitulé *KafkaSink.java* dans le répertoire de package de votre application. Ouvrez ensuite ce fichier dans un éditeur de texte et ajoutez-y les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="dd87c-193">Create a new Java file named *KafkaSink.java* in the package directory of your app, then open the file in a text editor and add the following lines:</span></span>

   ```java
   package com.wingtiptoys.kafka;

   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;

   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. <span data-ttu-id="dd87c-194">Enregistrez et fermez le fichier *KafkaSink.java*.</span><span class="sxs-lookup"><span data-stu-id="dd87c-194">Save and close the *KafkaSink.java* file.</span></span>

## <a name="build-and-test-your-application"></a><span data-ttu-id="dd87c-195">Générez et testez votre application</span><span class="sxs-lookup"><span data-stu-id="dd87c-195">Build and test your application</span></span>

1. <span data-ttu-id="dd87c-196">Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-196">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\kafka`

   <span data-ttu-id="dd87c-197">-ou-</span><span class="sxs-lookup"><span data-stu-id="dd87c-197">-or-</span></span>

   `cd /users/example/home/kafka`

1. <span data-ttu-id="dd87c-198">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-198">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="dd87c-199">Une fois votre application exécutée, vous pouvez utiliser *curl* pour tester votre application. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="dd87c-199">Once your application is running, you can use *curl* to test your application; for example:</span></span>

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   <span data-ttu-id="dd87c-200">Vous devriez voir « hello » publié dans les journaux de votre application.</span><span class="sxs-lookup"><span data-stu-id="dd87c-200">You should see "hello" posted to your application's logs.</span></span> <span data-ttu-id="dd87c-201">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="dd87c-201">For example:</span></span>

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> <span data-ttu-id="dd87c-202">Afin de tester votre application, vous pouvez modifier votre fichier *KafkaSource.java* pour qu’il contienne un formulaire HTML simple comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="dd87c-202">For testing purposes, you could modify your *KafkaSource.java* so that it contains a simple HTML form like the following example:</span></span>
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> <span data-ttu-id="dd87c-203">Cela vous permettra d’utiliser un navigateur web pour tester votre application :</span><span class="sxs-lookup"><span data-stu-id="dd87c-203">This will allow you to use a web browser to test your application:</span></span>
> 
> ![Tester votre application à l’aide d’un navigateur web][TB01]
> 
> <span data-ttu-id="dd87c-205">Lorsque vous envoyez le formulaire, votre application affiche les résultats :</span><span class="sxs-lookup"><span data-stu-id="dd87c-205">When you submit the form, your application will display the results:</span></span>
> 
> ![Réponse de l’application dans un navigateur web][TB02]
> 

## <a name="next-steps"></a><span data-ttu-id="dd87c-207">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd87c-207">Next steps</span></span>

<span data-ttu-id="dd87c-208">Pour plus d’informations sur la prise en charge Azure pour le Stream Binder Event Hub Apache Kafka, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="dd87c-208">For more information about Azure support for Event Hub Stream Binder and Apache Kafka, see the following articles:</span></span>

* [<span data-ttu-id="dd87c-209">Nouveautés des concentrateurs d’événements Azure ?</span><span class="sxs-lookup"><span data-stu-id="dd87c-209">What is Azure Event Hubs?</span></span>](/azure/event-hubs/event-hubs-about)

* [<span data-ttu-id="dd87c-210">Azure Event Hubs pour Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="dd87c-210">Azure Event Hubs for Apache Kafka</span></span>](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [<span data-ttu-id="dd87c-211">Créer un espace de noms Event Hubs et un concentrateur d’événements avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="dd87c-211">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>](/azure/event-hubs/event-hubs-create)

* [<span data-ttu-id="dd87c-212">Créer des Event Hubs prenant en charge Apache Kafka</span><span class="sxs-lookup"><span data-stu-id="dd87c-212">Create Apache Kafka enabled event hubs</span></span>](/azure/event-hubs/event-hubs-create-kafka-enabled)

<span data-ttu-id="dd87c-213">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="dd87c-213">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="dd87c-214">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="dd87c-214">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="dd87c-215">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="dd87c-215">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="dd87c-216">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="dd87c-216">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="dd87c-217">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="dd87c-217">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
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

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
