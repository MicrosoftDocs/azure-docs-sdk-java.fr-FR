---
title: Bibliothèques de machines virtuelle Azure pour Java
description: ''
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
ms.openlocfilehash: ea71c556f32a83d59d76b5fed8f3be26229f0cb1
ms.sourcegitcommit: 4d52e47073fb0b3ac40a2689daea186bad5b1ef5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49799815"
---
# <a name="azure-virtual-machine-libraries"></a>Bibliothèques de machines virtuelle Azure

## <a name="overview"></a>Vue d’ensemble

Des ressources de calcul à la demande et évolutives s’exécutant sous Linux et Windows.

Pour découvrir les machines virtuelles Azure, consultez la section [Créer une machine virtuelle Linux avec le portail Azure](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API de gestion

Créez, configurez et augmentez la taille des instances des machines virtuelles Windows et Linux dans Azure à partir de votre code avec l’API de gestion.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-compute</artifactId>
    <version>1.3.0</version>
</dependency>
```   


## <a name="example"></a>Exemples

Créez une machine virtuelle Linux dans un groupe de ressources Azure.

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
> [Explorer les API de gestion](/java/api/overview/azure/virtualmachines/management)


## <a name="samples"></a>Exemples

[Gérer les machines virtuelles][1]   
[Gérer des réseaux virtuels][6]   
[Créer une machine virtuelle à partir d’une image personnalisée][2]   
[Créer des machines virtuelles entre des régions en parallèle][5]    
[Créer un groupe de machines virtuelles identiques avec un équilibreur de charge][7]    

[1]: ../docs-ref-conceptual/java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[5]: ../docs-ref-conceptual/java-sdk-virtual-machines-in-parallel.md
[6]: ../docs-ref-conceptual/java-sdk-manage-virtual-networks.md
[7]: ../docs-ref-conceptual/java-sdk-manage-vm-scalesets.md

Explorez d’autres [exemples de code Java pour les machines virtuelles Azure](https://azure.microsoft.com/resources/samples/?platform=java&term=VM) que vous pouvez utiliser avec vos applications.