---
title: Gérer les machines virtuelles Azure avec Java | Microsoft Docs
description: Exemple de code pour gérer des machines virtuelles Azure avec le kit de développement logiciel (SDK) pour Java
author: rloutlaw
manager: douge
ms.assetid: 88629aee-6279-433e-a08b-4f8e290446d0
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e3048b3317477f4b1fb8edf93e4bebad6b7fafce
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
ms.locfileid: "21931165"
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a>Gérer les machines virtuelles Azure à partir de vos applications Java

[Cet exemple](https://github.com/Azure-Samples/compute-java-manage-vm/) utilise les [bibliothèques de gestion Azure pour Java](https://github.com/Azure/azure-sdk-for-java) afin de créer et d’utiliser des machines virtuelles Azure.

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a>Créer une machine virtuelle Windows

```java
// Prepare a data disk for VM
Disk dataDisk = azure.disks().define(SdkContext.randomResourceName("dsk", 30))
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withData()
            .withSizeInGB(50)
            .create();

// create the windows virtual machine with the data disk            
VirtualMachine windowsVM = azure.virtualMachines().define(windowsVmName)
            .withRegion(region)
            .withNewResourceGroup(rgName)
            .withNewPrimaryNetwork("10.0.0.0/28")
            .withPrimaryPrivateIpAddressDynamic()
            .withoutPrimaryPublicIpAddress()
            .withPopularWindowsImage(KnownWindowsVirtualMachineImage.WINDOWS_SERVER_2012_R2_DATACENTER)
            .withAdminUsername(userName)
            .withAdminPassword(password)
            .withNewDataDisk(10)
            .withNewDataDisk(dataDiskCreatable)
            .withExistingDataDisk(dataDisk)
            .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
            .create();
```

Ce code :   

0. Définit un élément Creatable `Disk` avec une taille de 50 Go et un nom aléatoire à utiliser avec une machine virtuelle.
0. Utilise la chaîne `azure.virtualMachines().define()..create()` pour créer la machine virtuelle Windows Server 2012. L’API crée l’élément `Disk` défini à l’étape précédente, en même temps que la machine virtuelle. Un disque de données de 10 Go est aussi attaché à la machine virtuelle via `withNewDataDisk(10)`.

En savoir plus sur l’utilisation d’éléments [Creatable<T> ](java-sdk-azure-concepts.md#Creatables) pour définir des représentations locales de ressources et pour les créer lorsque d’autres ressources Azure en ont besoin.

## <a name="stop-start-and-restart-a-virtual-machine"></a>Arrêter, démarrer et redémarrer une machine virtuelle

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

`powerOff()` arrête le système d’exploitation de la machine virtuelle, sans libérer ses ressources.

## <a name="add-a-virtual-machine-to-an-existing-network"></a>Ajouter une machine virtuelle à un réseau existant

```java
// Get the virtual network the current virtual machine is using
Network network = windowsVM.getPrimaryNetworkInterface().primaryIPConfiguration().getNetwork();

// Create a Linux VM in the same subnet
VirtualMachine linuxVM = azure.virtualMachines().define(linuxVmName)
           .withRegion(region)
           .withExistingResourceGroup(rgName)
           .withExistingPrimaryNetwork(network)
           .withSubnet("subnet1") // default subnet name when no name specified at creation
           .withPrimaryPrivateIPAddressDynamic()
           .withoutPrimaryPublicIPAddress()
           .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
           .withRootUsername(userName)
           .withRootPassword(password)
           .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
           .create();
```

Utilisez `withPopularLinuxImage` pour définir une machine virtuelle Linux au lieu d’une machine virtuelle Windows.


## <a name="list-virtual-machines"></a>Répertorier des machines virtuelles

```java
// get a list of VMs in the same resource group as an existing VM
String resourceGroupName = windowsVM.resourceGroupName();
PagedList<VirtualMachine> resourceGroupVMs = azure.virtualMachines()
        .listByResourceGroup(resourceGroupName); 

// for each vitual machine in the resource group, log their name and plan
for (VirtualMachine virtualMachine : azure.virtualMachines().listByResourceGroup(resourceGroupName)) {
    System.out.println("VM " + virtualMachine.computerName() + 
        " has plan " + virtualMachine.plan());
}
```

Répertoriez toutes les machines virtuelles d’un abonnement en utilisant `azure.virtualMachines().list()` et itérez la carte renvoyée par `tags()` pour gérer des collections balisées de machines virtuelles dans des groupes de ressources.

## <a name="update-a-virtual-machine"></a>Mise à jour d’une machine virtuelle

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

Mettez à jour la configuration d’une machine virtuelle en utilisant `update()...apply()` ainsi que les méthodes utilisées pour configurer la machine virtuelle lors de sa création via `define()...create()`.

## <a name="delete-a-virtual-machine"></a>Suppression d'une machine virtuelle

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a>Explication de l’exemple

[L’exemple de code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) crée une machine virtuelle Windows avec un disque de données de 50 Go. L’exemple crée ensuite un deuxième disque de données de 10 Go et le joint à la machine virtuelle Windows.
Puis l’exemple crée une machine virtuelle Linux dans le réseau virtuel où se trouve la machine virtuelle Windows.

L’exemple consigne des informations sur les deux machines virtuelles et les supprime avant achèvement de l’opération.

| Classe utilisée dans l’exemple | Remarques
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Interrogez des propriétés et gérez l’état des machines virtuelles. Récupéré sous forme de liste avec `azure.virtualMachines().list()` ou par nom ou ID avec `azure.virtualMachines().getByResourceGroup()`
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Classe avec des valeurs statiques qui mappent les [options de tailles d’une machine virtuelle](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), utilisées par la méthode `withSize()` pour définir les ressources allouées à la machine virtuelle.
| [Disque](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | Créez un disque pour stocker des données en utilisant `withData()` ou une image de système d’exploitation avec la méthode appropriée `withLinux` ou `withWindows` lorsque vous définissez le disque. Attachez des disques aux machines virtuelles lors de leur création (`using withNewDataDisk` ou `withExistingDataDisk`) ou après leur création en `update()..apply()` sur l’objet VirtualMachine.
| [DiskSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | Classe avec des valeurs statiques pour définir un disque avec une formule de stockage standard ou [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Classe avec un ensemble d’options de machine virtuelle Linux à utiliser avec la méthode `withPopularLinuxImage()` au moment de définir une machine virtuelle.
| [KnownWindowsVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | Classe avec un ensemble d’options d’image de machine virtuelle Windows à utiliser avec la méthode `withPopularWindowsImage()` au moment définir une machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]