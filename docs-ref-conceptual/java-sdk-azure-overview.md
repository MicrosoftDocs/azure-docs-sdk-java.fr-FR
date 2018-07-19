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
# <a name="azure-libraries-for-java"></a>Bibliothèques Azure pour Java

Les bibliothèques Azure pour Java vous aident à gérer les ressources Azure et à vous connecter aux différents services à partir de votre code d’application. Les bibliothèques sont disponibles en tant qu’[importations Maven](java-sdk-azure-install.md) que vous pouvez utiliser dans vos projets Java. 

## <a name="manage-azure-resources"></a>Gérer des ressources Azure

Créez et gérez des ressources Azure à partir de vos applications Java à l’aide des [bibliothèques de gestion Azure pour Java](java-sdk-azure-get-started.md). Ces bibliothèques permettent de créer vos propres outils et services d’automatisation Azure. 

Par exemple, pour créer une machine virtuelle Linux, vous devez écrire le code suivant :

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

Vérifiez les [instructions d’installation](java-sdk-azure-install.md) pour obtenir une liste complète des bibliothèques et apprendre comment les importer dans vos projets. Consultez ensuite l’[article de prise en main](java-sdk-azure-get-started.md) pour configurer l’authentification et exécuter l’exemple de code dans votre abonnement Azure. 

## <a name="connect-to-azure-services"></a>Se connecter aux services Azure

En plus d’utiliser les bibliothèques Java pour créer et gérer des ressources dans Azure, vous pouvez vous en servir pour vous connecter et utiliser les ressources dans vos applications. Par exemple, vous pouvez mettre à jour une table SQL Database ou stocker des fichiers dans le stockage Azure. Sélectionnez la bibliothèque dont vous avez besoin pour un service particulier à partir de la [liste complète des bibliothèques](java-sdk-azure-install.md) et visitez le [centre de développement Java](https://azure.microsoft.com/develop/java/) pour trouver des didacticiels et des exemples de code vous aidant à les utiliser dans vos applications.

Par exemple, pour imprimer le contenu de chaque objet blob dans un conteneur de stockage Azure :

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

## <a name="sample-code-and-reference"></a>Exemple de code et référence

Les exemples suivants détaillent les tâches d’automatisation courantes avec les bibliothèques de gestion Azure pour Java et disposent de codes préparés pour vos applications :

- [Machines virtuelles](java-sdk-azure-virtual-machine-samples.md)
- [Applications Web](java-sdk-azure-web-apps-samples.md)
- [Base de données SQL](java-sdk-azure-sql-database-samples.md)
   
Une [référence](https://docs.microsoft.com/java/api) est disponible pour tous les packages dans les bibliothèques de service et les bibliothèques de gestion. Les nouvelles fonctionnalités, les dernières modifications et les instructions de migration des versions précédentes sont disponibles dans les [notes de publication](java-sdk-azure-release-notes.md).