---
title: Bibliothèques Azure pour Java
description: Vue d’ensemble des bibliothèques de gestion et de service Azure pour Java
keywords: Azure, Java, SDK, API
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: 9aaf22a2-382a-4b13-a8e3-0e467d607207
ms.openlocfilehash: 22a337e928085475e905a271f991147729d97671
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21930875"
---
# <a name="azure-libraries-for-java"></a><span data-ttu-id="0addd-104">Bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="0addd-104">Azure libraries for Java</span></span>

<span data-ttu-id="0addd-105">Les bibliothèques Azure pour Java vous aident à gérer les ressources Azure et à vous connecter aux différents services à partir de votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="0addd-105">The Azure libraries for Java help you manage Azure resources and connect to services from your application code.</span></span> <span data-ttu-id="0addd-106">Les bibliothèques sont disponibles en tant qu’[importations Maven](java-sdk-azure-install.md) que vous pouvez utiliser dans vos projets Java.</span><span class="sxs-lookup"><span data-stu-id="0addd-106">The libraries are available as [Maven imports](java-sdk-azure-install.md) for use in your Java projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="0addd-107">Gérer des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="0addd-107">Manage Azure resources</span></span>

<span data-ttu-id="0addd-108">Créez et gérez des ressources Azure à partir de vos applications Java à l’aide des [bibliothèques de gestion Azure pour Java](java-sdk-azure-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0addd-108">Create and manage Azure resources from your Java applications using the [Azure management libraries for Java](java-sdk-azure-get-started.md).</span></span> <span data-ttu-id="0addd-109">Ces bibliothèques permettent de créer vos propres outils et services d’automatisation Azure.</span><span class="sxs-lookup"><span data-stu-id="0addd-109">Use these libraries to build your own Azure automation tools and services.</span></span> 

<span data-ttu-id="0addd-110">Par exemple, pour créer une machine virtuelle Linux, vous devez écrire le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0addd-110">For example, to create a Linux VM you would write the following code:</span></span>

```java
VirtualMachine linuxVM = azure.virtualMachines().define("myAzureVM")
           .withRegion(region)
           .withExistingResourceGroup("sampleResourceGroup")
           .withNewPrimaryNetwork("10.0.0.0/28")
           .withPrimaryPrivateIpAddressDynamic()
           .withoutPrimaryPublicIpAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withSsh(key)
           .withUnmanagedStorage()
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
 ```

<span data-ttu-id="0addd-111">Vérifiez les [instructions d’installation](java-sdk-azure-install.md) pour obtenir une liste complète des bibliothèques et apprendre comment les importer dans vos projets. Consultez ensuite l’[article de prise en main](java-sdk-azure-get-started.md) pour configurer l’authentification et exécuter l’exemple de code dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0addd-111">Review the [install instructions](java-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](java-sdk-azure-get-started.md) to set up your authentication and run sample code against your own Azure subscription.</span></span> 

## <a name="connect-to-azure-services"></a><span data-ttu-id="0addd-112">Se connecter aux services Azure</span><span class="sxs-lookup"><span data-stu-id="0addd-112">Connect to Azure services</span></span>

<span data-ttu-id="0addd-113">En plus d’utiliser les bibliothèques Java pour créer et gérer des ressources dans Azure, vous pouvez vous en servir pour vous connecter et utiliser les ressources dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="0addd-113">In addition to using Java libraries to create and manage resources within Azure, you can also use Java libraries to connect  and use those resources in your apps.</span></span> <span data-ttu-id="0addd-114">Par exemple, vous pouvez mettre à jour une table SQL Database ou stocker des fichiers dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0addd-114">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="0addd-115">Sélectionnez la bibliothèque dont vous avez besoin pour un service particulier à partir de la [liste complète des bibliothèques](java-sdk-azure-install.md) et visitez le [centre de développement Java](https://azure.microsoft.com/develop/java/) pour trouver des didacticiels et des exemples de code vous aidant à les utiliser dans vos applications.</span><span class="sxs-lookup"><span data-stu-id="0addd-115">Select the library you need for a particular service from the [complete list of libraries](java-sdk-azure-install.md) and visit the [Java developer center](https://azure.microsoft.com/develop/java/) for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="0addd-116">Par exemple, pour imprimer le contenu de chaque objet blob dans un conteneur de stockage Azure :</span><span class="sxs-lookup"><span data-stu-id="0addd-116">For example, to print out the contents of every blob in an Azure storage container:</span></span>

```java
// get the container from the blob client
CloudBlobContainer container = blobClient.getContainerReference("blobcontainer");

// For each item in the container
for (ListBlobItem blobItem : container.listBlobs()) {
    // If the item is a blob, not a virtual directory
    if (blobItem instanceof CloudBlockBlob) {
        // Download the text
        CloudBlockBlob retrievedBlob = (CloudBlockBlob) blobItem;
        System.out.println(retrievedBlob.downloadText());
    }
}
```

## <a name="sample-code-and-reference"></a><span data-ttu-id="0addd-117">Exemple de code et référence</span><span class="sxs-lookup"><span data-stu-id="0addd-117">Sample code and reference</span></span>

<span data-ttu-id="0addd-118">Les exemples suivants détaillent les tâches d’automatisation courantes avec les bibliothèques de gestion Azure pour Java et disposent de codes préparés pour vos applications :</span><span class="sxs-lookup"><span data-stu-id="0addd-118">The following samples cover common automation tasks with the Azure management libraries for Java and have code ready to use in your own apps:</span></span>

- [<span data-ttu-id="0addd-119">Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="0addd-119">Virtual machines</span></span>](java-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="0addd-120">Applications Web</span><span class="sxs-lookup"><span data-stu-id="0addd-120">Web apps</span></span>](java-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="0addd-121">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="0addd-121">SQL Database</span></span>](java-sdk-azure-sql-database-samples.md)
   
<span data-ttu-id="0addd-122">Une [référence](https://docs.microsoft.com/java/api) est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="0addd-122">A [reference](https://docs.microsoft.com/java/api) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="0addd-123">Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration des versions précédentes sont disponibles dans les [notes de publication](java-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="0addd-123">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](java-sdk-azure-release-notes.md).</span></span>