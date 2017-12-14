---
title: "Créer parallèlement des machines virtuelles dans plusieurs régions| Microsoft Docs"
description: "Exemple de code pour créer parallèlement des machines virtuelles dans plusieurs régions Azure à l’aide du kit de développement logiciel (SDK) Azure pour Java"
author: rloutlaw
manager: douge
ms.assetid: e5a36699-2d96-4571-84f9-a6af13f3c067
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: e20feb555c3a360eceae60c1569af9a00a5cd027
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a><span data-ttu-id="94258-103">Créer des machines virtuelles dans plusieurs régions à partir de vos applications Java</span><span class="sxs-lookup"><span data-stu-id="94258-103">Create virtual machines across multiple regions from your Java applications</span></span>

<span data-ttu-id="94258-104">[Cet exemple](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) crée parallèlement des machines virtuelles dans plusieurs régions Azure à l’aide des [bibliothèques de gestion Azure pour Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="94258-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) creates virtual machines in parallel across different Azure regions using the [Azure management libraries for Java](https://github.com/Azure/azure-sdk-for-java).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94258-105">L’exemple crée un total de 48 machines virtuelles qui exécutent Ubuntu 16.04 LTS de [taille STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) dans quatre régions différentes.</span><span class="sxs-lookup"><span data-stu-id="94258-105">The sample creates a total of 48 VMs running Ubuntu 16.04 LTS of [size STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) across four regions.</span></span> <span data-ttu-id="94258-106">L’exemple de code supprime ces machines virtuelles avant de quitter.</span><span class="sxs-lookup"><span data-stu-id="94258-106">The sample code deletes these virtual machines before exiting.</span></span> <span data-ttu-id="94258-107">Veillez à [vérifier les limites et les quotas de votre service](http://docs.microsoft.com/azure/azure-subscription-service-limits) avant d’exécuter cet exemple avec le nombre par défaut de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="94258-107">Make sure to [check your service limits and quota](http://docs.microsoft.com/azure/azure-subscription-service-limits) before running this sample with the default number of VMs.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="94258-108">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="94258-108">Run the sample</span></span>

<span data-ttu-id="94258-109">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="94258-109">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="94258-110">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="94258-110">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

<span data-ttu-id="94258-111">Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span><span class="sxs-lookup"><span data-stu-id="94258-111">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="94258-112">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="94258-112">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a><span data-ttu-id="94258-113">Définir des emplacements et des nombres pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="94258-113">Set locations and counts for the virtual machines</span></span>

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

<span data-ttu-id="94258-114">Cette `Map` est utilisée plus tard dans l’exemple pour définir la distribution globale des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="94258-114">This `Map` is used later in the sample to set the distrubtion of the VMs worldwide.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="94258-115">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="94258-115">Create a resource group</span></span> 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

<span data-ttu-id="94258-116">Chaque ressource dans l’exemple est gérée par ce groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="94258-116">Each resource in the sample is managed by this resource group.</span></span> <span data-ttu-id="94258-117">Les ressources sont ainsi plus faciles à nettoyer, car il suffit de supprimer le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="94258-117">This makes the resources easy to clean up later by deleting the resource group.</span></span>

## <a name="define-the-virtual-machines"></a><span data-ttu-id="94258-118">Définir les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="94258-118">Define the virtual machines</span></span>
```java
// list to store the VirtualMachine definitions
List<Creatable<VirtualMachine>> creatableVirtualMachines = new ArrayList<>();
    
// outer loop: iterate through each region included in the map
for (Map.Entry<Region, Integer> entry : virtualMachinesByLocation.entrySet()) {
    Region region = entry.getKey();
    Integer vmCount = entry.getValue();

    // Define one virtual network Creatable per region for the VMs to share
    String networkName = SdkContext.randomResourceName("vnetCOPD-", 20);
    Creatable<Network> networkCreatable = azure.networks().define(networkName)
           .withRegion(region)
           .withExistingResourceGroup(resourceGroup)
           .withAddressSpace("172.16.0.0/16");

    // Define one storage account Creatable per region for storing VM disks
    String storageAccountName = SdkContext.randomResourceName("stgcopd", 20);
    Creatable<StorageAccount> storageAccountCreatable = azure.storageAccounts()
        .define(storageAccountName)
              .withRegion(region)
              .withExistingResourceGroup(resourceGroup);

    // generate a common prefix for every VM name
    String linuxVMNamePrefix = SdkContext.randomResourceName("vm-", 15);

    // inner loop: iterate once for every VM instance in the region
    for (int i = 1; i <= vmCount; i++) {

        // Create one public IP address Creatable for each VM
        Creatable<PublicIpAddress> publicIpAddressCreatable = azure.publicIpAddresses()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withLeafDomainLabel(SdkContext.randomResourceName("pip", 10));

        publicIpCreatableKeys.add(publicIpAddressCreatable.key());

        // Create one virtual machine Creatable 
        Creatable<VirtualMachine> virtualMachineCreatable = azure.virtualMachines()
             .define(String.format("%s-%d", linuxVMNamePrefix, i))
             .withRegion(region)
             .withExistingResourceGroup(resourceGroup)
             .withNewPrimaryNetwork(networkCreatable)
             .withPrimaryPrivateIpAddressDynamic()
             .withNewPrimaryPublicIpAddress(publicIpAddressCreatable)
             .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
             .withRootUsername(userName)
             .withSsh(sshKey)
             .withSize(VirtualMachineSizeTypes.STANDARD_DS3_V2)
             .withNewStorageAccount(storageAccountCreatable);
        // add the virtual machine Creatable to the list     
        creatableVirtualMachines.add(virtualMachineCreatable); 
     }
}
```

<span data-ttu-id="94258-119">La boucle externe `for` ci-dessus itère chaque région, définissant ainsi un Creatable de réseau virtuel et de compte de stockage que les machines virtuelles de chaque région peuvent utiliser.</span><span class="sxs-lookup"><span data-stu-id="94258-119">The outer `for` loop above iterates through each region, defining a virtual network Creatable and storage account Creatable for use by all virtual machines in that region.</span></span> <span data-ttu-id="94258-120">En savoir plus sur l’utilisation de [Creatables](java-sdk-azure-concepts.md#Creatables) (objets pouvant être créés) pour créer uniquement les ressources nécessaires lors de l’utilisation de bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="94258-120">Learn more about using [Creatables](java-sdk-azure-concepts.md#Creatables) to create resources only as needed when using the management libraries.</span></span>

<span data-ttu-id="94258-121">La boucle interne `for` obtient un Creatable avec adresse IP publique pour la machine virtuelle. Elle définit ensuite un Creatable de machine virtuelle qui utilise les Creatables du réseau virtuel, du compte de stockage et de l’adresse IP publique créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="94258-121">The inner `for` loop gets a public IP address Creatable for the virtual machine and then defines a virtual machine Creatable using the Creatables for the virtual network, storage account, and public IP address defined previously.</span></span>  <span data-ttu-id="94258-122">Ce Creatable de machine virtuelle est alors ajouté à la liste `creatableVirtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="94258-122">This VirtualMachine Creatable is then added to the `creatableVirtualMachines` list.</span></span>

## <a name="create-the-virtual-machines"></a><span data-ttu-id="94258-123">Créer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="94258-123">Create the virtual machines</span></span>

```java
// create all virtual machines defined in the list, return all Creatable objects used
// including networks, public IP addresses, and storage accounts
CreatedResources<VirtualMachine> virtualMachines = azure.virtualMachines().create(creatableVirtualMachines);

// list the IDs of each virtual machine created 
for (VirtualMachine virtualMachine : virtualMachines.values()) {
    System.out.println(virtualMachine.id());
}

// call createdRelatedResource(key) to get the resources used to define the virtual machines. 
// Save the key at the time you define the Creatable to use CreatedResources like this
for (String publicIpCreatableKey : publicIpCreatableKeys) {
    PublicIPAddress pip = 
         (PublicIPAddress) virtualMachines.createdRelatedResource(publicIpCreatableKey);
}
```

<span data-ttu-id="94258-124">L’appel `azure.virtualMachines().create(creatableVirtualMachines)` crée parallèlement toutes les machines virtuelles que vous avez définies dans la liste `creatableVirtualMachines` sur l’ensemble des régions.</span><span class="sxs-lookup"><span data-stu-id="94258-124">The `azure.virtualMachines().create(creatableVirtualMachines)` call creates all of the virtual machines defined in the `creatableVirtualMachines` List in parallel across the regions.</span></span>

<span data-ttu-id="94258-125">Utilisez l’objet retourné `CreatedResources<VirtualMachine>`, en plus du type retourné `VirtualMachine`, pour accéder aux ressources créées dans l’abonnement Azure pendant la méthode `create()`.</span><span class="sxs-lookup"><span data-stu-id="94258-125">Use the returned `CreatedResources<VirtualMachine>` object to access any resources created in the Azure subscription during the the `create()` method, not just the returned `VirtualMachine` type.</span></span> <span data-ttu-id="94258-126">Remplacez la valeur retournée à partir de `createdRelatedResources()` par le bon type.</span><span class="sxs-lookup"><span data-stu-id="94258-126">Cast the returned value from `createdRelatedResources()` to the correct type.</span></span> 

<span data-ttu-id="94258-127">En savoir plus sur l’utilisation de `Creatable<T>` et `CreatedResources` dans notre [article sur les concepts de bibliothèque](java-sdk-azure-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="94258-127">Learn more about working with `Creatable<T>` and `CreatedResources` in our [library concepts article](java-sdk-azure-concepts.md).</span></span>

## <a name="delete-the-resource-group"></a><span data-ttu-id="94258-128">Supprimer le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="94258-128">Delete the resource group</span></span> 

```java
// finally block deletes the resource group before the code exits
// deleting a resource group deletes all resources created in it
finally {
    try {
        System.out.println("Deleting Resource Group: " + rgName);
        azure.resourceGroups().deleteByName(rgName);
        System.out.println("Deleted Resource Group: " + rgName);
    } catch (NullPointerException npe) {
        System.out.println("Did not create any resources in Azure. No clean up is necessary");
    } catch (Exception g) {
        g.printStackTrace();
    }
}
```

<span data-ttu-id="94258-129">Ce bloc supprime les ressources créées dans l’exemple avant qu’il ne se ferme.</span><span class="sxs-lookup"><span data-stu-id="94258-129">This block deletes resources created in the sample before the sample exits.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="94258-130">Explication de l’exemple</span><span class="sxs-lookup"><span data-stu-id="94258-130">Sample explanation</span></span>

<span data-ttu-id="94258-131">Affichez l’exemple de code complet sur [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span><span class="sxs-lookup"><span data-stu-id="94258-131">View the complete sample code on [Github](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).</span></span>

<span data-ttu-id="94258-132">L’exemple utilise l’objet `Creatable` pour définir un compte de stockage et un réseau virtuel pour chaque région dans lesquelles sont hébergées les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="94258-132">The sample uses `Creatable` objects to define a virtual network and storage account for each region hosting the virtual machines.</span></span> <span data-ttu-id="94258-133">Les objets `Creatable` sont ensuite définis pour l’adresse IP publique de chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94258-133">`Creatable` objects are then defined for the public IP address for each virtual machine.</span></span> <span data-ttu-id="94258-134">L’exemple définit les machines virtuelles à l’aide des objets `Creatable` et l’exemple ajoute la définition de la machine virtuelle à la liste `virtualMachineCreatable`.</span><span class="sxs-lookup"><span data-stu-id="94258-134">The sample defines the virtual machines using these `Creatable` objects, and sample adds the VM definition to the `virtualMachineCreatable` list.</span></span>

<span data-ttu-id="94258-135">Une fois que le code a ajouté les définitions de machine virtuelle à la liste, la méthode `azure.virtualMachines().create(creatableVirtualMachines)` crée parallèlement chaque machine virtuelle dans Azure.</span><span class="sxs-lookup"><span data-stu-id="94258-135">After the code adds every virtual machine definition to the list, `azure.virtualMachines().create(creatableVirtualMachines)` creates each virtual machine in parallel in Azure.</span></span>

<span data-ttu-id="94258-136">L’exemple de code obtient ensuite les adresses IP pour toutes les machines virtuelles créées à partir de l’objet CreatedResources afin de créer un [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) pour répartir les charges dans les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="94258-136">The sample code then gets the IP addresses for all of the created virtual machines from the returned CreatedResources object to create a [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) to distribute load across the virtual machines.</span></span> 

<span data-ttu-id="94258-137">Le bloc `finally` supprime les ressources présentes dans votre abonnement Azure, même en cas d’erreur.</span><span class="sxs-lookup"><span data-stu-id="94258-137">The `finally` block deletes the resources from your Azure subscription even in the case of an error.</span></span>

| <span data-ttu-id="94258-138">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="94258-138">Class used in sample</span></span> | <span data-ttu-id="94258-139">Remarques</span><span class="sxs-lookup"><span data-stu-id="94258-139">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="94258-140">VirtualMachine</span><span class="sxs-lookup"><span data-stu-id="94258-140">VirtualMachine</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | <span data-ttu-id="94258-141">Interrogez des propriétés et gérez l’état des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="94258-141">Query properties and manage state of virtual machines.</span></span> <span data-ttu-id="94258-142">Récupéré sous forme de liste avec `azure.virtualMachines().list()` ou par nom ou ID avec `azure.virtualMachines().getByResourceGroup()`</span><span class="sxs-lookup"><span data-stu-id="94258-142">Retrieved in list form from `azure.virtualMachines().list()` or by name or ID `azure.virtualMachines().getByResourceGroup()`</span></span>
| [<span data-ttu-id="94258-143">VirtualMachineSizeTypes</span><span class="sxs-lookup"><span data-stu-id="94258-143">VirtualMachineSizeTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | <span data-ttu-id="94258-144">Valeurs statiques qui correspondent aux [options de taille d’une machine virtuelle](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) utilisées comme paramètre dans `withSize()` lors de la définition d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94258-144">Static values that map to [virtual machine size options](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) for use as a parameter to `withSize()` when defining a virtual machine.</span></span>
| [<span data-ttu-id="94258-145">PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="94258-145">PublicIpAddress</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | <span data-ttu-id="94258-146">Défini mais pas immédiatement créé pour chaque machine virtuelle via `azure.publicIpAddresses().define()`.</span><span class="sxs-lookup"><span data-stu-id="94258-146">Defined, but not immediately created, for each virtual machine through `azure.publicIpAddresses().define()`.</span></span> <span data-ttu-id="94258-147">Stocker la clé pour chaque objet `Creatable` et récupérer ultérieurement via `createdRelatedResource()`</span><span class="sxs-lookup"><span data-stu-id="94258-147">Store the key for each `Creatable` and retrieve later through `createdRelatedResource()`</span></span>
| [<span data-ttu-id="94258-148">KnownLinuxVirtualMachineImage</span><span class="sxs-lookup"><span data-stu-id="94258-148">KnownLinuxVirtualMachineImage</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | <span data-ttu-id="94258-149">Ensemble d’options de machine virtuelle Linux utilisées comme paramètre dans `withPopularLinuxImage()` lors de la définition d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="94258-149">Set of Linux virtual machine options used as a parameter to `withPopularLinuxImage()` method when defining a virtual machine.</span></span>
| [<span data-ttu-id="94258-150">Réseau</span><span class="sxs-lookup"><span data-stu-id="94258-150">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="94258-151">L’exemple définit un réseau virtuel pour chaque région via `azure.networks().define()`.</span><span class="sxs-lookup"><span data-stu-id="94258-151">The sample defines one virtual network for each region through  `azure.networks().define()` .</span></span> 

## <a name="next-steps"></a><span data-ttu-id="94258-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94258-152">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]