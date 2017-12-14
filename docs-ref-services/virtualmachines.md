---
title: "Bibliothèques de machines virtuelle Azure pour Java"
description: 
keywords: Azure, Java, SDK, API, Calcul, Machines virtuelles
author: douge
ms.author: douge
manager: douge
ms.date: 05/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: compute
ms.openlocfilehash: f9a816d5787e41a4ee4643b1bc66bf21192ea298
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="33387-103">Bibliothèques de machines virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="33387-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="33387-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="33387-104">Overview</span></span>

<span data-ttu-id="33387-105">Des ressources de calcul à la demande et évolutives s’exécutant sous Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="33387-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="33387-106">Pour découvrir les machines virtuelles Azure, consultez la section [Créer une machine virtuelle Linux avec le portail Azure](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="33387-106">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="33387-107">API de gestion</span><span class="sxs-lookup"><span data-stu-id="33387-107">Management API</span></span>

<span data-ttu-id="33387-108">Créez, configurez et augmentez la taille des instances des machines virtuelles Windows et Linux dans Azure à partir de votre code avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="33387-108">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="33387-109">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="33387-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a><span data-ttu-id="33387-110">Exemple</span><span class="sxs-lookup"><span data-stu-id="33387-110">Example</span></span>

<span data-ttu-id="33387-111">Créez une machine virtuelle Linux dans un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="33387-111">Create a new Linux virtual machine in a new Azure resource group.</span></span>

```java
VirtualMachine newLinuxVm = azure.virtualMachines().define(linuxVmName)
            .withRegion(Region.US_EAST)
            .withNewResourceGroup("myResourceGroup")
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
            .withRootUsername(userName)
            .withSshKey(key)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="33387-112">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="33387-112">Explore the Management APIs</span></span>](/java/api/overview/azure/virtualmachines/managementapi)


## <a name="samples"></a><span data-ttu-id="33387-113">Exemples</span><span class="sxs-lookup"><span data-stu-id="33387-113">Samples</span></span>

<span data-ttu-id="33387-114">[Gérer les machines virtuelles][1] </span><span class="sxs-lookup"><span data-stu-id="33387-114">[Manage virtual machines][1] </span></span>  
<span data-ttu-id="33387-115">[Gérer des réseaux virtuels][6] </span><span class="sxs-lookup"><span data-stu-id="33387-115">[Manage virtual networks][6] </span></span>  
<span data-ttu-id="33387-116">[Créer une machine virtuelle à partir d’une image personnalisée][2] </span><span class="sxs-lookup"><span data-stu-id="33387-116">[Create a virtual machine from a custom image][2] </span></span>  
<span data-ttu-id="33387-117">[Créer des machines virtuelles entre des régions en parallèle][5]  </span><span class="sxs-lookup"><span data-stu-id="33387-117">[Create virtual machines across regions in parallel][5]  </span></span>  
<span data-ttu-id="33387-118">[Créer un groupe de machines virtuelles identiques avec un équilibreur de charge][7]</span><span class="sxs-lookup"><span data-stu-id="33387-118">[Create a virtual machine scale set with a load balancer][7]</span></span>    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

<span data-ttu-id="33387-119">Explorez d’autres [exemples de code Java pour les machines virtuelles Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que vous pouvez utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="33387-119">Explore more [sample Java code for Azure virtual machines](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) you can use in your apps.</span></span>