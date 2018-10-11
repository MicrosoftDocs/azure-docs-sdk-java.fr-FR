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
ms.openlocfilehash: 3d21cdd890912c1fc58fc65a79ba972b8327edeb
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892540"
---
# <a name="create-and-manage-azure-virtual-networks-from-your-java-apps"></a>Créer et gérer des réseaux virtuels Azure à partir de vos applications Java

[Cet exemple](https://github.com/Azure-Samples/network-java-manage-virtual-network) crée un [réseau virtuel](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) pour isoler vos ressources Azure sur un segment de réseau que vous contrôlez.

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/network-java-manage-virtual-network.git
cd network-java-manage-virtual-network
mvn clean compile exec:java
```

Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/network-java-manage-virtual-network/blob/master/src/main/java/com/microsoft/azure/management/network/samples/ManageVirtualNetwork.java).

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-network-security-group-to-block-internet-traffic"></a>Créer un groupe de sécurité réseau pour bloquer le trafic Internet

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

Cette [règle de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) bloque tout trafic Internet public entrant et sortant. Ce groupe de sécurité réseau n’aura d’effet qu’une fois appliqué à un sous-réseau de votre réseau virtuel.

## <a name="create-a-virtual-network-with-two-subnets"></a>Créer un réseau virtuel avec deux sous-réseaux

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

Le sous-réseau principal refuse l’accès à Internet, selon les règles définies dans le groupe de sécurité réseau. Le sous-réseau frontal utilise les [règles par défaut](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) permettant le trafic Internet sortant.

## <a name="create-a-network-security-group-to-allow-inbound-http-traffic"></a>Créer une règle de groupe de sécurité réseau visant à autoriser le trafic HTTP entrant
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

Cette règle de sécurité réseau ouvre un trafic entrant sur le port 80 depuis l’Internet public, et bloque tout trafic sortant du réseau vers l’Internet public. 

## <a name="update-a-virtual-network"></a>Mettre à jour un réseau virtuel
```java
// update the front end subnet to use the rules in the new network security group
virtualNetwork1.update()
          .updateSubnet(vnet1FrontEndSubnetName)
          .withExistingNetworkSecurityGroup(frontEndSubnetNsg)
          .parent()
          .apply();
```

Mettez à jour le sous-réseau frontal pour autoriser le trafic HTTP entrant avec la règle de sécurité réseau créée précédemment.

## <a name="create-a-virtual-machine-on-a-subnet"></a>Créer une machine virtuelle sur un sous-réseau
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

`withExistingPrimaryNetwork()` et `withSubnet()` configurent la machine virtuelle pour se servir du sous-réseau frontal sur le réseau virtuel créé précédemment.

## <a name="list-virtual-networks-in-a-resource-group"></a>Répertorier des réseaux virtuels dans un groupe de ressources
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

Vous pouvez répertorier et inspecter l’objet `Network` avec la collection externe ou itérer les ressources enfant de chaque réseau avec la boucle imbriquée, comme indiqué dans cet exemple.

## <a name="delete-a-virtual-network"></a>Supprimer un réseau virtuel
```java
// if you already have the virtual network object it is easiest to delete by ID
azure.networks().deleteById(virtualNetwork1.id());

// Delete by resource group and name if you don't have the VirtualMachine object
azure.networks().deleteByResourceGroup(rgName,vnetName1);
```

La suppression d’un réseau virtuel supprime les sous-réseaux présents, mais ne supprime pas les règles de groupe de sécurité réseau qui leur sont appliquées. Ces définitions peuvent être réappliquées à d’autres sous-réseaux.

## <a name="sample-explanation"></a>Explication de l’exemple

Cet exemple crée un réseau virtuel avec deux sous-réseaux, sur lesquels se trouve une machine virtuelle. Le sous-réseau principal est coupé de l’Internet public. Le sous-réseau avant accepte le trafic HTTP entrant depuis Internet. Les deux machines virtuelles du réseau virtuel communiquent entre elles via les règles par défaut du groupe de sécurité.

| Classe utilisée dans l’exemple | Notes
|-------|-------|
| [Réseau](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network) | Représentation locale sous forme d’objet d’un réseau virtuel créée à partir de `azure.networks().define()...create()`. Utilisez la chaîne Fluent `update()...apply()` pour mettre à jour un réseau virtuel existant.
| [Sous-réseau](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._subnet) | Créez des sous-réseaux sur le réseau virtuel lors de la définition ou de la mise à jour du réseau avec `withSubnet()`. Obtenez des représentations sous forme d’objet d’un sous-réseau à partir de `Network.subnets().get()` ou `Network.subnets().entrySet()`. Ces objets disposent de méthodes d’interrogation des propriétés de sous-réseau.
| [Groupe de sécurité réseau](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._network_security_group) | Créé avec la chaîne Fluent `azure.networkSecurityGroups().define()...create()` puis appliqué aux sous-réseaux via la mise à jour ou la création de sous-réseaux dans un réseau virtuel. 

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]