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
# <a name="manage-azure-virtual-machine-scale-sets-from-your-java-applications"></a><span data-ttu-id="80b26-103">Gérer les groupes de machines virtuelles identiques Azure à partir de vos applications Java</span><span class="sxs-lookup"><span data-stu-id="80b26-103">Manage Azure virtual machine scale sets from your Java applications</span></span>

<span data-ttu-id="80b26-104">[Cet exemple](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) crée un [groupe de machines virtuelles identiques](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) à l’aide des [bibliothèques de gestion Java](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="80b26-104">[This sample](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets) creates a  [virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-overview) using the [Java management libraries](https://github.com/Azure/azure-sdk-for-java).</span></span> 

## <a name="run-the-sample"></a><span data-ttu-id="80b26-105">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="80b26-105">Run the sample</span></span>

<span data-ttu-id="80b26-106">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="80b26-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="80b26-107">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80b26-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets.git
cd compute-java-manage-virtual-machine-scale-sets
mvn clean compile exec:java
```

<span data-ttu-id="80b26-108">Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span><span class="sxs-lookup"><span data-stu-id="80b26-108">View the [complete code sample on GitHub](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="80b26-109">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="80b26-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-virtual-network-for-the-scale-set"></a><span data-ttu-id="80b26-110">Créer un réseau virtuel pour le groupe identique</span><span class="sxs-lookup"><span data-stu-id="80b26-110">Create a virtual network for the scale set</span></span>

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

<span data-ttu-id="80b26-111">Configurez un réseau virtuel et un équilibreur de charge avant de définir le groupe identique.</span><span class="sxs-lookup"><span data-stu-id="80b26-111">Set up a virtual network and load balancer before creating the scale set definition.</span></span> <span data-ttu-id="80b26-112">Le groupe identique utilise ces ressources lors de sa configuration initiale.</span><span class="sxs-lookup"><span data-stu-id="80b26-112">The scale set uses these resources for its initial configuration.</span></span>

## <a name="create-a-load-balancer-to-distribute-load-across-the-scale-set"></a><span data-ttu-id="80b26-113">Créer un équilibreur de charge pour répartir la charge dans le groupe identique</span><span class="sxs-lookup"><span data-stu-id="80b26-113">Create a load balancer to distribute load across the scale set</span></span>

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

 <span data-ttu-id="80b26-114">L’équilibreur de charge définit deux pools de réseaux principaux ; un réseau pour équilibrer la charge dans le protocole HTTP (`backendPoolName1`) et un autre pour équilibrer la charge dans le protocole HTTPS (`backendPoolName2`).</span><span class="sxs-lookup"><span data-stu-id="80b26-114">The load balancer defines two backend network address pools-one to balance load across HTTP (`backendPoolName1`) and the other to balance load across HTTPS (`backendPoolName2`).</span></span>  <span data-ttu-id="80b26-115">La méthode `defineHttpProbe()` configure des [points de terminaison de sondes d’intégrité](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) sur les équilibreurs de charges.</span><span class="sxs-lookup"><span data-stu-id="80b26-115">The `defineHttpProbe()` methods set up [health probe endpoints](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) on the load balancers.</span></span> <span data-ttu-id="80b26-116">Les règles NAT exposent les ports 22 et 23 d’un groupe de machines virtuelles identiques à un accès telnet et SSH.</span><span class="sxs-lookup"><span data-stu-id="80b26-116">NAT rules expose ports 22 and 23 on the scale set virtual machines for telnet and SSH access.</span></span>

## <a name="create-a-scale-set"></a><span data-ttu-id="80b26-117">Créer un groupe identique</span><span class="sxs-lookup"><span data-stu-id="80b26-117">Create a scale set</span></span>
 
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

<span data-ttu-id="80b26-118">Utilisez la définition du réseau virtuel et celles de l’équilibreur de charge créées dans l’étape précédente pour créer un groupe identique de trois instances Linux (`withCapacity(3)`) et de trois disques de données chacun d’une taille de 100 Go.</span><span class="sxs-lookup"><span data-stu-id="80b26-118">Use the virtual network definition and load balancer definitions created in the previous step to create a scale set with three Linux instances (`withCapacity(3)`) and three 100GB data disks each.</span></span> <span data-ttu-id="80b26-119">La chaîne de méthode `defineNewExtension()` installe le serveur web Apache sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80b26-119">The `defineNewExtension()` method chain installs the Apache web server on each VM.</span></span>

## <a name="list-virtual-machine-scale-set-network-interfaces"></a><span data-ttu-id="80b26-120">Répertorier les interfaces réseau d’un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="80b26-120">List virtual machine scale set network interfaces</span></span>

```java
// List network interfaces on the scale set and iterate through them
PagedList<VirtualMachineScaleSetNetworkInterface> vmssNics = 
     virtualMachineScaleSet.listNetworkInterfaces();
for (VirtualMachineScaleSetNetworkInterface vmssNic : vmssNics) {
    System.out.println(vmssNic.id());
}
```

## <a name="get-ssh-connection-strings-for-each-scale-set-virtual-machine"></a><span data-ttu-id="80b26-121">Obtenir des chaînes de connexion SSH pour chaque groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="80b26-121">Get SSH connection strings for each scale set virtual machine</span></span>

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

<span data-ttu-id="80b26-122">Le pool NAT créé précédemment a mappé les ports SSH et telnet (22 et 23, respectivement) des machines virtuelles jusqu’aux ports de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="80b26-122">The NAT pool created earlier mapped the SSH and telnet ports (22 and 23, respectively) on the virtual machines to ports on the load balancer.</span></span> <span data-ttu-id="80b26-123">Ce code génère la chaîne de connexion SSH pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80b26-123">This code builds the SSH connection string for each virtual machine.</span></span>

## <a name="stop-the-virtual-machine-scale-set"></a><span data-ttu-id="80b26-124">Arrêter le groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="80b26-124">Stop the virtual machine scale set</span></span>

```java
// stop (not deallocate) all scale set instances
virtualMachineScaleSet.powerOff();
```

<span data-ttu-id="80b26-125">Les machines virtuelles arrêtées continuent de consommer des ressources réservées.</span><span class="sxs-lookup"><span data-stu-id="80b26-125">Stopped virtual machines continue to consume reserved resources.</span></span> <span data-ttu-id="80b26-126">Utilisez la méthode `deallocate()` pour arrêter le système d’exploitation d’une machine virtuelle et ainsi libérer leurs ressources de calcul.</span><span class="sxs-lookup"><span data-stu-id="80b26-126">Use `deallocate()` to stop the operating system on the virtual machines and release their compute resources.</span></span>

## <a name="deallocate-the-virtual-machine-scale-set"></a><span data-ttu-id="80b26-127">Libérer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="80b26-127">Deallocate the virtual machine scale set</span></span>

```java
// deallocate the virtual machine scale set
virtualMachineScaleSet.deallocate();
```

<span data-ttu-id="80b26-128">Deallocate() : arrête le système d’exploitation d’une machine virtuelle et libère les ressources réseau et de calcul (telles que les adresses IP) utilisées par les instances du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="80b26-128">Deallocate() shuts down the operating system on the virtual machines and frees up the compute and network resources (such as IP addresses) used by the scale set instances.</span></span> <span data-ttu-id="80b26-129">Vous continuez à accumuler des frais de stockage pour tous les disques (y compris le système d’exploitation) attachés aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="80b26-129">You continue to accrue storage charges for any disks (including the OS) attached to the virtual machines.</span></span>

## <a name="start-a-virtual-machine-scale-set"></a><span data-ttu-id="80b26-130">Démarrer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="80b26-130">Start a virtual machine scale set</span></span>

```java
// start a deallocated or stopped virtual machine scale set
virtualMachineScaleSet.start();
```

## <a name="update-the-number-of-virtual-machines-instances-in-the-scale-set"></a><span data-ttu-id="80b26-131">Mettre à jour le nombre d’instances de machines virtuelles présentes dans le groupe identique</span><span class="sxs-lookup"><span data-stu-id="80b26-131">Update the number of virtual machines instances in the scale set</span></span>
```java
// increase the number of virtual machine scale set instances from three to six
virtualMachineScaleSet.update()
                    .withCapacity(6)
                    .apply();
```

<span data-ttu-id="80b26-132">Mettez à l’échelle le nombre de machines virtuelles présentes dans le groupe identique à l’aide de la méthode `withCapacity()`, puis la capacité de chaque machine virtuelle à l’aide de la méthode `withSku()`.</span><span class="sxs-lookup"><span data-stu-id="80b26-132">Scale the number of virtual machines in the scale set using `withCapacity()` and scale the capacity of each virtual machine using `withSku()`.</span></span>

## <a name="sample-explanation"></a><span data-ttu-id="80b26-133">Explication de l’exemple</span><span class="sxs-lookup"><span data-stu-id="80b26-133">Sample explanation</span></span>

<span data-ttu-id="80b26-134">[L’exemple de code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) crée d’abord un réseau virtuel pour permettre au groupe identique de communiquer et un équilibreur de charge pour répartir le trafic dans les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="80b26-134">[The sample code](https://github.com/Azure-Samples/compute-java-manage-virtual-machine-scale-sets/blob/master/src/main/java/com/microsoft/azure/management/compute/samples/ManageVirtualMachineScaleSet.java) first creates a virtual network for the scale set to communicate across and a load balancer to distribute traffic across the virtual machines.</span></span> <span data-ttu-id="80b26-135">La chaîne de méthode `azure.virtualMachineScaleSets().define()...create()` crée un groupe identique composé de trois instances Linux exécutant le serveur web Apache.</span><span class="sxs-lookup"><span data-stu-id="80b26-135">The `azure.virtualMachineScaleSets().define()...create()` method chain creates the scale set with three Linux instances running the Apache web server.</span></span>    
   
| <span data-ttu-id="80b26-136">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="80b26-136">Class used in sample</span></span> | <span data-ttu-id="80b26-137">Notes</span><span class="sxs-lookup"><span data-stu-id="80b26-137">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="80b26-138">VirtualMachineScaleSet</span><span class="sxs-lookup"><span data-stu-id="80b26-138">VirtualMachineScaleSet</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set) | <span data-ttu-id="80b26-139">Pour interroger, démarrer, arrêter, mettre à jour et supprimer toutes les machines virtuelles du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="80b26-139">Query, start, stop, update and delete all virtual machines in the scale set.</span></span>
| [<span data-ttu-id="80b26-140">VirtualMachineScaleSetVM</span><span class="sxs-lookup"><span data-stu-id="80b26-140">VirtualMachineScaleSetVM</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_v_m) | <span data-ttu-id="80b26-141">Récupérée à partir de `virtualMachineScaleSet.virtualMachines().get()` ou `list()`, elle vous permet d’interroger, de démarrer, d’arrêter, de configurer et de supprimer les machines virtuelles du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="80b26-141">Retrieved from `virtualMachineScaleSet.virtualMachines().get()` or `list()`, allows you to query, start, stop, configure and delete virtual machines in the scale set.</span></span>
| [<span data-ttu-id="80b26-142">VirtualMachineScaleSetNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="80b26-142">VirtualMachineScaleSetNetworkInterface</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_network_interface) | <span data-ttu-id="80b26-143">Renvoyée par `virtualMachineScaleSet.listNetworkInterfaces()`, une représentation en lecture seule de l’interface réseau d’une machine virtuelle dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="80b26-143">Returned from `virtualMachineScaleSet.listNetworkInterfaces()`, read-only representation of a network interface on a virtual machine in a scale set.</span></span>
| [<span data-ttu-id="80b26-144">VirtualMachineScaleSetSkuTypes</span><span class="sxs-lookup"><span data-stu-id="80b26-144">VirtualMachineScaleSetSkuTypes</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.compute._virtual_machine_scale_set_sku_types) | <span data-ttu-id="80b26-145">Classe de champs statiques utilisée pour déterminer le [niveau du groupe de machines virtuelles identiques](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) qui définit la quantité de ressources que les membres d’un groupe identique peuvent consommer.</span><span class="sxs-lookup"><span data-stu-id="80b26-145">Class of static fields used to set the [virtual machine scale set tier](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) used to define how much resources scale set members can consume.</span></span>
| [<span data-ttu-id="80b26-146">VirtualMachineScaleSetNicIpConfiguration</span><span class="sxs-lookup"><span data-stu-id="80b26-146">VirtualMachineScaleSetNicIpConfiguration</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.network._virtual_machine_scale_set_nic_i_p_configuration) | <span data-ttu-id="80b26-147">Utilisée pour interroger la configuration IP associée à l’interface réseau d’une machine virtuelle dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="80b26-147">Used to query the IP configuration associated with a network interface on a scale set virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80b26-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80b26-148">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]