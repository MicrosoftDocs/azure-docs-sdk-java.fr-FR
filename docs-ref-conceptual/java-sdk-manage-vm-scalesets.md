---
title: Gérer des groupes de machines virtuelles identiques avec Java | Microsoft Docs
description: Exemple de code pour gérer des groupes de machines virtuelles identiques Azure avec le kit de développement logiciel (SDK) pour Java
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 3/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 4653726b387369c18942b6c11392f15b9f0351f3
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893490"
---
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a>Gérer les groupes de machines virtuelles identiques Azure à partir de vos applications Java

[Cet exemple](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) crée un [groupe de machines virtuelles identiques](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) à l’aide des [bibliothèques de gestion Java](https://github.com/Azure/azure-sdk-for-java). 

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a>Créer un réseau virtuel pour le groupe identique

```java
Network network = azure.networks().define(vnetName)
                    .withRegion(region)
                    .withNewResourceGroup(rgName)
                    .withAddressSpace("172.16.0.0/16")
                    .defineSubnet("Front-end")
                    .withAddressPrefix("172.16.1.0/24")
                    .attach()
                    .create();
```

Configurez un réseau virtuel et un équilibreur de charge avant de définir le groupe identique. Le groupe identique utilise ces ressources lors de sa configuration initiale.

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a>Créer un équilibreur de charge pour répartir la charge dans le groupe identique

```java
LoadBalancer loadBalancer1 = azure.loadBalancers().define(loadBalancerName1)
                    .withRegion(region)
                    .withExistingResourceGroup(rgName)
                    // assign a public IP address to the load balancer
                    .definePublicFrontend(frontendName)
                        .withExistingPublicIPAddress(publicIPAddress)
                        .attach()
                    // Add two backend address pools
                    .defineBackend(backendPoolName1)
                        .attach()
                    .defineBackend(backendPoolName2)
                        .attach()
                    // Add two health probes on 80 and 443
                    .defineHttpProbe(httpProbe)
                        .withRequestPath("/")
                        .withPort(80)
                        .attach()
                    .defineHttpProbe(httpsProbe)
                        .withRequestPath("/")
                        .withPort(443)
                        .attach()

                    // balance HTTP and HTTPs traffic
                    .defineLoadBalancingRule(httpLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(80)
                        .withProbe(httpProbe)
                        .withBackend(backendPoolName1)
                        .attach()
                    .defineLoadBalancingRule(httpsLoadBalancingRule)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPort(443)
                        .withProbe(httpsProbe)
                        .withBackend(backendPoolName2)
                        .attach()

                    // Add NAT definitions to enable SSH and telnet to the VMs 
                    .defineInboundNatPool(natPool50XXto22)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(5000, 5099)
                        .withBackendPort(22)
                        .attach()
                    .defineInboundNatPool(natPool60XXto23)
                        .withProtocol(TransportProtocol.TCP)
                        .withFrontend(frontendName)
                        .withFrontendPortRange(6000, 6099)
                        .withBackendPort(23)
                        .attach()
                    .create();
```

 L’équilibreur de charge définit deux pools de réseaux principaux ; un réseau pour équilibrer la charge dans le protocole HTTP (`backendPoolName1`) et un autre pour équilibrer la charge dans le protocole HTTPS (`backendPoolName2`).  La méthode `defineHttpProbe()` configure des [points de terminaison de sondes d’intégrité](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) sur les équilibreurs de charges. Les règles NAT exposent les ports 22 et 23 d’un groupe de machines virtuelles identiques à un accès telnet et SSH.

## <a name="create-a-scale-set"></a>Créer un groupe identique
 
```java
 // Create a virtual machine scale set with three virtual machines
 // And, install Apache Web servers on them
VirtualMachineScaleSet virtualMachineScaleSet = azure.virtualMachineScaleSets()
       .define(vmssName)
                .withRegion(region)
                .withExistingResourceGroup(rgName)
                .withSku(VirtualMachineScaleSetSkuTypes.STANDARD_D3_V2)
                .withExistingPrimaryNetworkSubnet(network, "Front-end")
                .withExistingPrimaryInternetFacingLoadBalancer(loadBalancer1)
                .withPrimaryInternetFacingLoadBalancerBackends(backendPoolName1, backendPoolName2)
                .withPrimaryInternetFacingLoadBalancerInboundNatPools(natPool50XXto22, natPool60XXto23)
                .withoutPrimaryInternalLoadBalancer()
                .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                .withRootUsername(userName)
                .withSsh(sshKey)
                .withNewDataDisk(100)
                .withNewDataDisk(100, 1, CachingTypes.READ_WRITE)
                .withNewDataDisk(100, 2, 
                     CachingTypes.READ_WRITE, StorageAccountTypes.STANDARD_LRS)
                .withCapacity(3)
                // Use a VM extension to install Apache Web servers
                .defineNewExtension("CustomScriptForLinux")
                    .withPublisher("Microsoft.OSTCExtensions")
                    .withType("CustomScriptForLinux")
                    .withVersion("1.4")
                    .withMinorVersionAutoUpgrade()
                    .withPublicSetting("fileUris", fileUris)
                    .withPublicSetting("commandToExecute", installCommand)
                    .attach()
                .create();
```

Utilisez la définition du réseau virtuel et celles de l’équilibreur de charge créées dans l’étape précédente pour créer un groupe identique de trois instances Linux (`withCapacity(3)`) et de trois disques de données chacun d’une taille de 100 Go. La chaîne de méthode `defineNewExtension()` installe le serveur web Apache sur chaque machine virtuelle.

## <a name="list-virtual-machine-scale-set-network-interfaces"></a>Répertorier les interfaces réseau d’un groupe de machines virtuelles identiques

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a>Obtenir des chaînes de connexion SSH pour chaque groupe de machines virtuelles identiques

```java
for (VirtualMachineScaleSetVM instance : virtualMachineScaleSet.virtualMachines().list()) {
    System.out.println("Scale set virtual machine instance #" + instance.instanceId());
    System.out.println(instance.id());
    PagedList<VirtualMachineScaleSetNetworkInterface> networkInterfaces = 
         instance.listNetworkInterfaces();
    // Pick the first NIC on the instance and use its primary IP address
    VirtualMachineScaleSetNetworkInterface networkInterface = networkInterfaces.get(0);
    for (VirtualMachineScaleSetNicIPConfiguration ipConfig : networkInterface.ipConfigurations().values()) {
        if (ipConfig.isPrimary()) {
            List<LoadBalancerInboundNatRule> natRules = ipConfig.listAssociatedLoadBalancerInboundNatRules();
            for (LoadBalancerInboundNatRule natRule : natRules) {
                // find rule matching the inbound SSH port on the backend for the IP address
                // and return the SSH connection string to that port on the load balancer
                if (natRule.backendPort() == 22) {
                    System.out.println("SSH connection string: " + userName + 
                        "@" + publicIPAddress.fqdn() + ":" + natRule.frontendPort());
                break;
                }
            }
            break;
        }
    }
}
```

Le pool NAT créé précédemment a mappé les ports SSH et telnet (22 et 23, respectivement) des machines virtuelles jusqu’aux ports de l’équilibreur de charge. Ce code génère la chaîne de connexion SSH pour chaque machine virtuelle.

## <a name="stop-the-virtual-machine-scale-set"></a>Arrêter le groupe de machines virtuelles identiques

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

Les machines virtuelles arrêtées continuent de consommer des ressources réservées. Utilisez la méthode `deallocate()` pour arrêter le système d’exploitation d’une machine virtuelle et ainsi libérer leurs ressources de calcul.

## <a name="deallocate-the-virtual-machine-scale-set"></a>Libérer un groupe de machines virtuelles identiques

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

Deallocate() : arrête le système d’exploitation d’une machine virtuelle et libère les ressources réseau et de calcul (telles que les adresses IP) utilisées par les instances du groupe identique. Vous continuez à accumuler des frais de stockage pour tous les disques (y compris le système d’exploitation) attachés aux machines virtuelles.

## <a name="start-a-virtual-machine-scale-set"></a>Démarrer un groupe de machines virtuelles identiques

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a>Mettre à jour le nombre d’instances de machines virtuelles présentes dans le groupe identique
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

Mettez à l’échelle le nombre de machines virtuelles présentes dans le groupe identique à l’aide de la méthode `withCapacity()`, puis la capacité de chaque machine virtuelle à l’aide de la méthode `withSku()`.

## <a name="sample-explanation"></a>Explication de l’exemple

[L’exemple de code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) crée d’abord un réseau virtuel pour permettre au groupe identique de communiquer et un équilibreur de charge pour répartir le trafic dans les machines virtuelles. La chaîne de méthode `azure.virtualMachineScaleSets().define()...create()` crée un groupe identique composé de trois instances Linux exécutant le serveur web Apache.    
   
| Classe utilisée dans l’exemple | Notes
|-------|-------|
| [VirtualMachineScaleSet](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | Pour interroger, démarrer, arrêter, mettre à jour et supprimer toutes les machines virtuelles du groupe identique.
| [VirtualMachineScaleSetVM](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | Récupérée à partir de `virtualMachineScaleSet.virtualMachines().get()` ou `list()`, elle vous permet d’interroger, de démarrer, d’arrêter, de configurer et de supprimer les machines virtuelles du groupe identique.
| [VirtualMachineScaleSetNetworkInterface](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | Renvoyée par `virtualMachineScaleSet.listNetworkInterfaces()`, une représentation en lecture seule de l’interface réseau d’une machine virtuelle dans un groupe identique.
| [VirtualMachineScaleSetSkuTypes](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | Classe de champs statiques utilisée pour déterminer le [niveau du groupe de machines virtuelles identiques](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) qui définit la quantité de ressources que les membres d’un groupe identique peuvent consommer.
| [VirtualMachineScaleSetNicIpConfiguration](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | Utilisée pour interroger la configuration IP associée à l’interface réseau d’une machine virtuelle dans un groupe identique.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]