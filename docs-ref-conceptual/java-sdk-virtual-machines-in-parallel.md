---
title: Créer parallèlement des machines virtuelles dans plusieurs régions| Microsoft Docs
description: Exemple de code pour créer parallèlement des machines virtuelles dans plusieurs régions Azure à l’aide du kit de développement logiciel (SDK) Azure pour Java
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
ms.locfileid: "21931195"
---
# <a name="create-virtual-machines-across-multiple-regions-from-your-java-applications"></a>Créer des machines virtuelles dans plusieurs régions à partir de vos applications Java

[Cet exemple](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) crée parallèlement des machines virtuelles dans plusieurs régions Azure à l’aide des [bibliothèques de gestion Azure pour Java](https://github.com/Azure/azure-sdk-for-java).

> [!IMPORTANT]
> L’exemple crée un total de 48 machines virtuelles qui exécutent Ubuntu 16.04 LTS de [taille STANDARD_DS3_V2](http://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes) dans quatre régions différentes. L’exemple de code supprime ces machines virtuelles avant de quitter. Veillez à [vérifier les limites et les quotas de votre service](http://docs.microsoft.com/azure/azure-subscription-service-limits) avant d’exécuter cet exemple avec le nombre par défaut de machines virtuelles.

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel.git
cd compute-java-create-virtual-machines-across-regions-in-parallel
mvn clean compile exec:java
```

Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/CreateVirtualMachinesInParallel.java).

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="set-locations-and-counts-for-the-virtual-machines"></a>Définir des emplacements et des nombres pour les machines virtuelles

```java
// use a Map to define how where and how many VMs to create 
Map<Region, Integer> virtualMachinesByLocation = new HashMap<Region, Integer>();

// create 12 virtual machines in four regions
virtualMachinesByLocation.put(Region.US_EAST, 12);
virtualMachinesByLocation.put(Region.US_SOUTH_CENTRAL, 12);
virtualMachinesByLocation.put(Region.US_WEST, 12);
virtualMachinesByLocation.put(Region.US_NORTH_CENTRAL, 12);
```

Cette `Map` est utilisée plus tard dans l’exemple pour définir la distribution globale des machines virtuelles.

## <a name="create-a-resource-group"></a>Créer un groupe de ressources 

```java
// logically associate the resources in the sample into a randomly named resource group
final String rgName = SdkContext.randomResourceName("rgCOPD", 24);
ResourceGroup resourceGroup = azure.resourceGroups().define(rgName)
                .withRegion(Region.US_EAST)
                .create();
```

Chaque ressource dans l’exemple est gérée par ce groupe de ressources. Les ressources sont ainsi plus faciles à nettoyer, car il suffit de supprimer le groupe de ressources.

## <a name="define-the-virtual-machines"></a>Définir les machines virtuelles
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

La boucle externe `for` ci-dessus itère chaque région, définissant ainsi un Creatable de réseau virtuel et de compte de stockage que les machines virtuelles de chaque région peuvent utiliser. En savoir plus sur l’utilisation de [Creatables](java-sdk-azure-concepts.md#Creatables) (objets pouvant être créés) pour créer uniquement les ressources nécessaires lors de l’utilisation de bibliothèques de gestion.

La boucle interne `for` obtient un Creatable avec adresse IP publique pour la machine virtuelle. Elle définit ensuite un Creatable de machine virtuelle qui utilise les Creatables du réseau virtuel, du compte de stockage et de l’adresse IP publique créés précédemment.  Ce Creatable de machine virtuelle est alors ajouté à la liste `creatableVirtualMachines`.

## <a name="create-the-virtual-machines"></a>Créer les machines virtuelles

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

L’appel `azure.virtualMachines().create(creatableVirtualMachines)` crée parallèlement toutes les machines virtuelles que vous avez définies dans la liste `creatableVirtualMachines` sur l’ensemble des régions.

Utilisez l’objet retourné `CreatedResources<VirtualMachine>`, en plus du type retourné `VirtualMachine`, pour accéder aux ressources créées dans l’abonnement Azure pendant la méthode `create()`. Remplacez la valeur retournée à partir de `createdRelatedResources()` par le bon type. 

En savoir plus sur l’utilisation de `Creatable<T>` et `CreatedResources` dans notre [article sur les concepts de bibliothèque](java-sdk-azure-concepts.md).

## <a name="delete-the-resource-group"></a>Supprimer le groupe de ressources 

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

Ce bloc supprime les ressources créées dans l’exemple avant qu’il ne se ferme.

## <a name="sample-explanation"></a>Explication de l’exemple

Affichez l’exemple de code complet sur [GitHub](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel).

L’exemple utilise l’objet `Creatable` pour définir un compte de stockage et un réseau virtuel pour chaque région dans lesquelles sont hébergées les machines virtuelles. Les objets `Creatable` sont ensuite définis pour l’adresse IP publique de chaque machine virtuelle. L’exemple définit les machines virtuelles à l’aide des objets `Creatable` et l’exemple ajoute la définition de la machine virtuelle à la liste `virtualMachineCreatable`.

Une fois que le code a ajouté les définitions de machine virtuelle à la liste, la méthode `azure.virtualMachines().create(creatableVirtualMachines)` crée parallèlement chaque machine virtuelle dans Azure.

L’exemple de code obtient ensuite les adresses IP pour toutes les machines virtuelles créées à partir de l’objet CreatedResources afin de créer un [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) pour répartir les charges dans les machines virtuelles. 

Le bloc `finally` supprime les ressources présentes dans votre abonnement Azure, même en cas d’erreur.

| Classe utilisée dans l’exemple | Remarques
|-------|-------|
| [VirtualMachine](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine) | Interrogez des propriétés et gérez l’état des machines virtuelles. Récupéré sous forme de liste avec `azure.virtualMachines().list()` ou par nom ou ID avec `azure.virtualMachines().getByResourceGroup()`
| [VirtualMachineSizeTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_size_types) | Valeurs statiques qui correspondent aux [options de taille d’une machine virtuelle](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) utilisées comme paramètre dans `withSize()` lors de la définition d’une machine virtuelle.
| [PublicIpAddress](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._public_i_p_address) | Défini mais pas immédiatement créé pour chaque machine virtuelle via `azure.publicIpAddresses().define()`. Stocker la clé pour chaque objet `Creatable` et récupérer ultérieurement via `createdRelatedResource()`
| [KnownLinuxVirtualMachineImage](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._known_linux_virtual_machine_image) | Ensemble d’options de machine virtuelle Linux utilisées comme paramètre dans `withPopularLinuxImage()` lors de la définition d’une machine virtuelle.
| [Réseau](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | L’exemple définit un réseau virtuel pour chaque région via `azure.networks().define()`. 

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]