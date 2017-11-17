---
title: "Gérer les machines virtuelles Azure avec Java | Microsoft Docs"
description: "Exemple de code pour gérer des machines virtuelles Azure avec le kit de développement logiciel (SDK) pour Java"
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
---
# <a name="manage-azure-virtual-machines-from-your-java-applications"></a><span data-ttu-id="53847-103">Gérer les machines virtuelles Azure à partir de vos applications Java</span><span class="sxs-lookup"><span data-stu-id="53847-103">Manage Azure virtual machines from your Java applications</span></span>

<span data-ttu-id="53847-104">[Cet exemple](https://github.com/Azure-Samples/compute-java-manage-vm/) utilise les [bibliothèques de gestion Azure pour Java](https://github.com/Azure/azure-sdk-for-java) afin de créer et d’utiliser des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="53847-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-vm/) uses the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java) to create and work with Azure virtual machines.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="53847-105">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="53847-105">Run the sample</span></span>

<span data-ttu-id="53847-106">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="53847-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="53847-107">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="53847-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-vm.git
cd compute-java-manage-vm
mvn clean compile exec:java
```

<span data-ttu-id="53847-108">Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span><span class="sxs-lookup"><span data-stu-id="53847-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="53847-109">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="53847-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-windows-virtual-machine"></a><span data-ttu-id="53847-110">Créer une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="53847-110">Create a Windows virtual machine</span></span>

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

<span data-ttu-id="53847-111">Ce code :</span><span class="sxs-lookup"><span data-stu-id="53847-111">This code:</span></span>   

0. <span data-ttu-id="53847-112">Définit un élément Creatable `Disk` avec une taille de 50 Go et un nom aléatoire à utiliser avec une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="53847-112">Defines a `Disk` Creatable with a 50GB size and random name for use with a virtual machine.</span></span>
0. <span data-ttu-id="53847-113">Utilise la chaîne `azure.virtualMachines().define()..create()` pour créer la machine virtuelle Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="53847-113">Uses the `azure.virtualMachines().define()..create()` chain to create the Windows Server 2012 virtual machine.</span></span> <span data-ttu-id="53847-114">L’API crée l’élément `Disk` défini à l’étape précédente, en même temps que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="53847-114">The API creates the `Disk` defined in the previous step the same time as the virtual machine.</span></span> <span data-ttu-id="53847-115">Un disque de données de 10 Go est aussi attaché à la machine virtuelle via `withNewDataDisk(10)`.</span><span class="sxs-lookup"><span data-stu-id="53847-115">A 10GB data disk is also attached to the virtual machine through `withNewDataDisk(10)`.</span></span>

<span data-ttu-id="53847-116">En savoir plus sur l’utilisation d’éléments [Creatable<T> ](java-sdk-azure-concepts.md#Creatables) pour définir des représentations locales de ressources et pour les créer lorsque d’autres ressources Azure en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="53847-116">Learn more about using [Creatable<T> objects](java-sdk-azure-concepts.md#Creatables) to define local representations of resources and create them just as other Azure resources need them.</span></span>

## <a name="stop-start-and-restart-a-virtual-machine"></a><span data-ttu-id="53847-117">Arrêter, démarrer et redémarrer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="53847-117">Stop, start, and restart a virtual machine</span></span>

```java
// look up a virtual machine by its ID and then restart, stop, and start it
azureVM = azure.getVirtualMachine.getById(windowsVM.id());

azureVM.restart();
azureVM.powerOff();
azureVM.start();
```

<span data-ttu-id="53847-118">`powerOff()` arrête le système d’exploitation de la machine virtuelle, sans libérer ses ressources.</span><span class="sxs-lookup"><span data-stu-id="53847-118">`powerOff()` stops the virtual machine operating system but does not deallocate its resources.</span></span>

## <a name="add-a-virtual-machine-to-an-existing-network"></a><span data-ttu-id="53847-119">Ajouter une machine virtuelle à un réseau existant</span><span class="sxs-lookup"><span data-stu-id="53847-119">Add a virtual machine to an existing network</span></span>

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

<span data-ttu-id="53847-120">Utilisez `withPopularLinuxImage` pour définir une machine virtuelle Linux au lieu d’une machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="53847-120">Use `withPopularLinuxImage` to define a Linux VM instead of a Windows one.</span></span>


## <a name="list-virtual-machines"></a><span data-ttu-id="53847-121">Répertorier des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="53847-121">List virtual machines</span></span>

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

<span data-ttu-id="53847-122">Répertoriez toutes les machines virtuelles d’un abonnement en utilisant `azure.virtualMachines().list()` et itérez la carte renvoyée par `tags()` pour gérer des collections balisées de machines virtuelles dans des groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="53847-122">List all virtual machines for a subscription using `azure.virtualMachines().list()` and iterate through the Map returned by `tags()` to manage tagged collections of virtual machines across resource groups.</span></span>

## <a name="update-a-virtual-machine"></a><span data-ttu-id="53847-123">Mise à jour d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="53847-123">Update a virtual machine</span></span>

```java
// add a 10GB data disk to the virtual machine
windowsVM.update()
     .withNewDataDisk(10)
     .apply();
```

<span data-ttu-id="53847-124">Mettez à jour la configuration d’une machine virtuelle en utilisant `update()...apply()` ainsi que les méthodes utilisées pour configurer la machine virtuelle lors de sa création via `define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="53847-124">Update the virtual machine configuration using `update()...apply()` and the same methods used to configure the virtual machine when created through `define()...create()`.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="53847-125">Suppression d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="53847-125">Delete a virtual machine</span></span>

```java
// delete by ID if you already are working with the VM object
azure.virtualMachines().deleteById(windowsVM.id());

// delete by resource group and name
azure.virtualMachines().deleteByResourceGroup(rgName,windowsVmName);
```

## <a name="sample-explanation"></a><span data-ttu-id="53847-126">Explication de l’exemple</span><span class="sxs-lookup"><span data-stu-id="53847-126">Sample explanation</span></span>

<span data-ttu-id="53847-127">[L’exemple de code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) crée une machine virtuelle Windows avec un disque de données de 50 Go.</span><span class="sxs-lookup"><span data-stu-id="53847-127">[The sample code](https://github.com/Azure-Samples/compute-java-manage-vm/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachine.java) creates a Windows virtual machine with a 50GB data disk.</span></span> <span data-ttu-id="53847-128">L’exemple crée ensuite un deuxième disque de données de 10 Go et le joint à la machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="53847-128">The sample then creates a second 10GB data disk and attaches it to this Windows virtual machine.</span></span>
<span data-ttu-id="53847-129">Puis l’exemple crée une machine virtuelle Linux dans le réseau virtuel où se trouve la machine virtuelle Windows.</span><span class="sxs-lookup"><span data-stu-id="53847-129">Then the sample creates a Linux virtual machine in the same virtual network as the Windows virtual machine.</span></span>

<span data-ttu-id="53847-130">L’exemple consigne des informations sur les deux machines virtuelles et les supprime avant achèvement de l’opération.</span><span class="sxs-lookup"><span data-stu-id="53847-130">The sample logs information about both virtual machines and deletes them both before completing.</span></span>

| <span data-ttu-id="53847-131">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="53847-131">Class used in sample</span></span> | <span data-ttu-id="53847-132">Remarques</span><span class="sxs-lookup"><span data-stu-id="53847-132">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="53847-133">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="53847-133">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="53847-134">Interrogez des propriétés et gérez l’état des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="53847-134">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="53847-135">Récupéré sous forme de liste avec `azure.virtualMachines().list()` ou par nom ou ID avec `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="53847-135">Retrieved in list form  with`azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="53847-136">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="53847-136">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="53847-137">Classe avec des valeurs statiques qui mappent les [options de tailles d’une machine virtuelle](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), utilisées par la méthode `withSize()` pour définir les ressources allouées à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="53847-137">Class with static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/), used by the `withSize()` method to define the resources allocated to the VM.</span></span>
| [<span data-ttu-id="53847-138">Disque</span><span class="sxs-lookup"><span data-stu-id="53847-138">Disk</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk) | <span data-ttu-id="53847-139">Créez un disque pour stocker des données en utilisant `withData()` ou une image de système d’exploitation avec la méthode appropriée `withLinux` ou `withWindows` lorsque vous définissez le disque.</span><span class="sxs-lookup"><span data-stu-id="53847-139">Create a disk to store data using `withData()` or operating system image using the appropriate `withLinux` or `withWindows` method when defining the disk.</span></span> <span data-ttu-id="53847-140">Attachez des disques aux machines virtuelles lors de leur création (`using withNewDataDisk` ou `withExistingDataDisk`) ou après leur création en `update()..apply()` sur l’objet VirtualMachine.</span><span class="sxs-lookup"><span data-stu-id="53847-140">Attach disks to virtual machines either at the time of creation (`using withNewDataDisk` or `withExistingDataDisk`) or after creation by `update()..apply()` on the VirtualMachine object.</span></span>
| [<span data-ttu-id="53847-141">DiskSkuTypes</span><span class="sxs-lookup"><span data-stu-id="53847-141">DiskSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._disk_sku_types) | <span data-ttu-id="53847-142">Classe avec des valeurs statiques pour définir un disque avec une formule de stockage standard ou [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage).</span><span class="sxs-lookup"><span data-stu-id="53847-142">Class with static values to define a disk with a standard or [premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) storage plan.</span></span>
| [<span data-ttu-id="53847-143">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="53847-143">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="53847-144">Classe avec un ensemble d’options de machine virtuelle Linux à utiliser avec la méthode `withPopularLinuxImage()` au moment de définir une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="53847-144">Class with a set of Linux virtual machine options for use with the `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="53847-145">KnownWindowsVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="53847-145">KnownWindowsVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_windows_virtual_machine_image) | <span data-ttu-id="53847-146">Classe avec un ensemble d’options d’image de machine virtuelle Windows à utiliser avec la méthode `withPopularWindowsImage()` au moment définir une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="53847-146">Class with a set of Windows virtual machine image options for use with the `withPopularWindowsImage()` method when defining a virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53847-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53847-147">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]