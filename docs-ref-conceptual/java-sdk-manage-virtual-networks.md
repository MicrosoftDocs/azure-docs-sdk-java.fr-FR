---
title: Gérer les réseaux virtuels Azure avec Java | Microsoft Docs
description: Exemple de code pour gérer les réseaux virtuels Azure dans votre code Java
author: rloutlaw
manager: douge
ms.assetid: 92736911-3df6-46e7-b751-25bb36bf89b9
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 6989c5184d09ac011cb39eb21ad8d96db3f0c107
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592554"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a><span data-ttu-id="270a2-103">Créer et gérer des réseaux virtuels Azure à partir de vos applications Java</span><span class="sxs-lookup"><span data-stu-id="270a2-103">Create and manage Azure virtual networks from your Java apps</span></span>

<span data-ttu-id="270a2-104">[Cet exemple](https://github.com/Azure-Samples/network-java-manage-virtual-network) crée un [réseau virtuel](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) pour isoler vos ressources Azure sur un segment de réseau que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="270a2-104">[This sample](https://github.com/Azure-Samples/network-java-manage-virtual-network) creates a [virtual network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) to isolate your Azure resources on network segment you control.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="270a2-105">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="270a2-105">Run the sample</span></span>

<span data-ttu-id="270a2-106">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="270a2-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="270a2-107">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="270a2-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

<span data-ttu-id="270a2-108">Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span><span class="sxs-lookup"><span data-stu-id="270a2-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="270a2-109">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="270a2-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a><span data-ttu-id="270a2-110">Créer un groupe de sécurité réseau pour bloquer le trafic Internet</span><span class="sxs-lookup"><span data-stu-id="270a2-110">Create a network security group to block Internet traffic</span></span>

```java
// this NSG definition block traffic to and from the public Internet
NetworkSecurityGroup backEndSubnetNsg = azure.networkSecurityGroups()
              .define(vnet1BackEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup(rgName)
                    .defineRule("DenyInternetInComing")
                        .denyInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="270a2-111">Cette [règle de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) bloque tout trafic Internet public entrant et sortant.</span><span class="sxs-lookup"><span data-stu-id="270a2-111">This [network security rule](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) blocks both inbound and outbound public Internet traffic.</span></span> <span data-ttu-id="270a2-112">Ce groupe de sécurité réseau n’aura d’effet qu’une fois appliqué à un sous-réseau de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="270a2-112">This network security group will not have an effect until applied to a subnet in your virtual network.</span></span>

## <a name="create-a-virtual-network-with-two-subnets"></a><span data-ttu-id="270a2-113">Créer un réseau virtuel avec deux sous-réseaux</span><span class="sxs-lookup"><span data-stu-id="270a2-113">Create a virtual network with two subnets</span></span>

```java
// create the a virtual network with two subnets
// assign the backend subnet a rule blocking public internet traffic
Network virtualNetwork1 = azure.networks().define(vnetName1)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withAddressSpace("192.168.0.0/16")
                    .withSubnet(vnet1FrontEndSubnetName, "192.168.1.0/24")
                    .defineSubnet(vnet1BackEndSubnetName)
                        .withAddressPrefix("192.168.2.0/24")
                        .withExistingNetworkSecurityGroup(backEndSubnetNsg)
                        .attach()
                    .create();
```

<span data-ttu-id="270a2-114">Le sous-réseau principal refuse l’accès à Internet, selon les règles définies dans le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="270a2-114">The backend subnet denies Internet access usingfollowing the rules set in the network security group.</span></span> <span data-ttu-id="270a2-115">Le sous-réseau frontal utilise les [règles par défaut](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) permettant le trafic Internet sortant.</span><span class="sxs-lookup"><span data-stu-id="270a2-115">The front end subnet uses the [default rules](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) which allow outbound traffic to the Internet.</span></span>

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a><span data-ttu-id="270a2-116">Créer une règle de groupe de sécurité réseau visant à autoriser le trafic HTTP entrant</span><span class="sxs-lookup"><span data-stu-id="270a2-116">Create a network security group to allow inbound HTTP traffic</span></span>
```java
// create a rule that allows inbound HTTP and blocks outbound Internet traffic
NetworkSecurityGroup frontEndSubnetNsg = azure.networkSecurityGroups()
               .define(vnet1FrontEndSubnetNsgName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .defineRule("AllowHttpInComing")
                        .allowInbound()
                        .fromAddress("INTERNET")
                        .fromAnyPort()
                        .toAnyAddress()
                        .toPort(80)
                        .withProtocol(SecurityRuleProtocol.TCP)
                        .attach()
                    .defineRule("DenyInternetOutGoing")
                        .denyOutbound()
                        .fromAnyAddress()
                        .fromAnyPort()
                        .toAddress("INTERNET")
                        .toAnyPort()
                        .withAnyProtocol()
                        .attach()
                    .create();
```

<span data-ttu-id="270a2-117">Cette règle de sécurité réseau ouvre un trafic entrant sur le port 80 depuis l’Internet public, et bloque tout trafic sortant du réseau vers l’Internet public.</span><span class="sxs-lookup"><span data-stu-id="270a2-117">This network security rule opens up inbound traffic on port 80 from the public Internet, and blocks all outbound traffic from inside the network to the public Internet.</span></span> 

## <a name="update-a-virtual-network"></a><span data-ttu-id="270a2-118">Mettre à jour un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="270a2-118">Update a virtual network</span></span>
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

<span data-ttu-id="270a2-119">Mettez à jour le sous-réseau frontal pour autoriser le trafic HTTP entrant avec la règle de sécurité réseau créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="270a2-119">Update the front end subnet to allow inbound HTTP traffic using the network security rule created in the previous step.</span></span>

## <a name="create-a-virtual-machine-on-a-subnet"></a><span data-ttu-id="270a2-120">Créer une machine virtuelle sur un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="270a2-120">Create a virtual machine on a subnet</span></span>
```java
// attach the new VM to the front end subnet on the virtual network
VirtualMachine frontEndVM = azure.virtualMachines().define(frontEndVmName)
                    .withRegion(Region.US_EAST)
                    .withExistingResourceGroup(rgName)
                    .withExistingPrimaryNetwork(virtualNetwork1) 
                    .withSubnet(vnet1FrontEndSubnetName)
                    .withPrimaryPrivateIpAddressDynamic()
                    .withNewPrimaryPublicIpAddress(publicIpAddressLeafDnsForFrontEndVm)
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();
```

<span data-ttu-id="270a2-121">`withExistingPrimaryNetwork()` et `withSubnet()` configurent la machine virtuelle pour se servir du sous-réseau frontal sur le réseau virtuel créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="270a2-121">`withExistingPrimaryNetwork()` and `withSubnet()` configure the virtual machine to use the front-end subnet on the virtual network created in the previous steps.</span></span>

## <a name="list-virtual-networks-in-a-resource-group"></a><span data-ttu-id="270a2-122">Répertorier des réseaux virtuels dans un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="270a2-122">List virtual networks in a resource group</span></span>
```java
// iterate over every virtual network in the resource group 
for (Network virtualNetwork : azure.networks().listByResourceGroup(rgName)) {
    // for each subnet on the virtual network, log the network address prefix 
    for (Map.Entry<String, Subnet> entry : virtualNetwork.subnets().entrySet()) {
        String subnetName = entry.getKey();
        Subnet subnet = entry.getValue();
        System.out.println("Address prefix for subnet " + subnetName + 
             " is " + subnet.addressPrefix());
    }
}
```       

<span data-ttu-id="270a2-123">Vous pouvez répertorier et inspecter l’objet `Network` avec la collection externe ou itérer les ressources enfant de chaque réseau avec la boucle imbriquée, comme indiqué dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="270a2-123">You can list and inspect `Network` object using the outer collection or iterate through each child resource for each network using the nested for-each loop as seen in this example.</span></span>

## <a name="delete-a-virtual-network"></a><span data-ttu-id="270a2-124">Supprimer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="270a2-124">Delete a virtual network</span></span>
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

<span data-ttu-id="270a2-125">La suppression d’un réseau virtuel supprime les sous-réseaux présents, mais ne supprime pas les règles de groupe de sécurité réseau qui leur sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="270a2-125">Removing a virtual network deletes the subnets on the network but does not delete the network security group rules applied to the subnets.</span></span> <span data-ttu-id="270a2-126">Ces définitions peuvent être réappliquées à d’autres sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="270a2-126">Those definitions can be reapplied to other subnets.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="270a2-127">Explication de l’exemple</span><span class="sxs-lookup"><span data-stu-id="270a2-127">Sample explanation</span></span>

<span data-ttu-id="270a2-128">Cet exemple crée un réseau virtuel avec deux sous-réseaux, sur lesquels se trouve une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="270a2-128">This sample creates a virtual network with two subnets and with one virtual machine on each subnet.</span></span> <span data-ttu-id="270a2-129">Le sous-réseau principal est coupé de l’Internet public.</span><span class="sxs-lookup"><span data-stu-id="270a2-129">The back subnet is cut off from the public Internet.</span></span> <span data-ttu-id="270a2-130">Le sous-réseau avant accepte le trafic HTTP entrant depuis Internet.</span><span class="sxs-lookup"><span data-stu-id="270a2-130">The front-facing subnet accepts inbound HTTP traffic from the Internet.</span></span> <span data-ttu-id="270a2-131">Les deux machines virtuelles du réseau virtuel communiquent entre elles via les règles par défaut du groupe de sécurité.</span><span class="sxs-lookup"><span data-stu-id="270a2-131">Both virtual machines in the virtual network communicate with each other through the default network security group rules.</span></span>

| <span data-ttu-id="270a2-132">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="270a2-132">Class used in sample</span></span> | <span data-ttu-id="270a2-133">Notes</span><span class="sxs-lookup"><span data-stu-id="270a2-133">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="270a2-134">Réseau</span><span class="sxs-lookup"><span data-stu-id="270a2-134">Network</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | <span data-ttu-id="270a2-135">Représentation locale sous forme d’objet d’un réseau virtuel créée à partir de `azure.networks().define()...create()`.</span><span class="sxs-lookup"><span data-stu-id="270a2-135">Local object representation of the virtual network created from `azure.networks().define()...create()` .</span></span> <span data-ttu-id="270a2-136">Utilisez la chaîne Fluent `update()...apply()` pour mettre à jour un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="270a2-136">Use the `update()...apply()` fluent chain to update an existing virtual network.</span></span>
| [<span data-ttu-id="270a2-137">Sous-réseau</span><span class="sxs-lookup"><span data-stu-id="270a2-137">Subnet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | <span data-ttu-id="270a2-138">Créez des sous-réseaux sur le réseau virtuel lors de la définition ou de la mise à jour du réseau avec `withSubnet()`.</span><span class="sxs-lookup"><span data-stu-id="270a2-138">Create subnets on the virtual network when defining or updating the network using `withSubnet()`.</span></span> <span data-ttu-id="270a2-139">Obtenez des représentations sous forme d’objet d’un sous-réseau à partir de `Network.subnets().get()` ou `Network.subnets().entrySet()`.</span><span class="sxs-lookup"><span data-stu-id="270a2-139">Get object representations of a subnet from `Network.subnets().get()` or `Network.subnets().entrySet()`.</span></span> <span data-ttu-id="270a2-140">Ces objets disposent de méthodes d’interrogation des propriétés de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="270a2-140">These objects have methods to query subnet properties.</span></span>
| [<span data-ttu-id="270a2-141">Groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="270a2-141">NetworkSecurityGroup</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | <span data-ttu-id="270a2-142">Créé avec la chaîne Fluent `azure.networkSecurityGroups().define()...create()` puis appliqué aux sous-réseaux via la mise à jour ou la création de sous-réseaux dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="270a2-142">Created using the `azure.networkSecurityGroups().define()...create()` fluent chain and then applied to subnets through the updating or creating subnets in a virtual network.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="270a2-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="270a2-143">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]