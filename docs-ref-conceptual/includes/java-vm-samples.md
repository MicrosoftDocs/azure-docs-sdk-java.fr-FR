---
ms.openlocfilehash: 4b70a81f5b59fd6e26ad18fdf58b3d932cf2a897
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893800"
---
| <span data-ttu-id="9012b-101">**Créer des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="9012b-101">**Create virtual machines**</span></span> || 
|---|---|
| <span data-ttu-id="9012b-102">[Gérer des machines virtuelles][1]</span><span class="sxs-lookup"><span data-stu-id="9012b-102">[Manage virtual machines][1]</span></span> | <span data-ttu-id="9012b-103">Créez, modifiez, démarrez, arrêtez et supprimez des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9012b-103">Create, modify, start, stop, and delete virtual machines.</span></span> |
| <span data-ttu-id="9012b-104">[Créer une machine virtuelle à partir d’une image personnalisée][2]</span><span class="sxs-lookup"><span data-stu-id="9012b-104">[Create a virtual machine from a custom image][2]</span></span> | <span data-ttu-id="9012b-105">Créez une image de machine virtuelle personnalisée et utilisez-la pour créer de nouvelles machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9012b-105">Create a custom virtual machine image and use it to create new virtual machines.</span></span> | 
| <span data-ttu-id="9012b-106">[Créer une machine virtuelle à l’aide d’un VHD spécialisé à partir d’une capture instantanée][3]</span><span class="sxs-lookup"><span data-stu-id="9012b-106">[Create a virtual machine using specialized VHD from a snapshot][3]</span></span> | <span data-ttu-id="9012b-107">Créez une capture instantanée à partir du système d’exploitation de la machine virtuelle et des disques de données, créez des disques managés à partir des captures instantanées, puis créez une machine virtuelle en joignant les disques managés.</span><span class="sxs-lookup"><span data-stu-id="9012b-107">Create snapshot from the virtual machine's OS and data disks, create managed disks from the snapshots, and then create a virtual machine by attaching the managed disks.</span></span> |  
| <span data-ttu-id="9012b-108">[Créer des machines virtuelles en parallèle dans le même réseau][4]</span><span class="sxs-lookup"><span data-stu-id="9012b-108">[Create virtual machines in parallel in the same network][4]</span></span> | <span data-ttu-id="9012b-109">Créez des machines virtuelles dans la même région sur le même réseau virtuel avec deux sous-réseaux en parallèle.</span><span class="sxs-lookup"><span data-stu-id="9012b-109">Create virtual machines in the same region on the same virtual network with two subnets in parallel.</span></span> |
| <span data-ttu-id="9012b-110">[Créer des machines virtuelles entre des régions en parallèle][5]</span><span class="sxs-lookup"><span data-stu-id="9012b-110">[Create virtual machines across regions in parallel][5]</span></span> | <span data-ttu-id="9012b-111">Créez et équilibrez la charge d’un ensemble de machines virtuelles entre plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="9012b-111">Create and load-balance a set of virtual machines across multiple Azure regions.</span></span> |
| <span data-ttu-id="9012b-112">**Mettre en réseau des machines virtuelles**</span><span class="sxs-lookup"><span data-stu-id="9012b-112">**Network virtual machines**</span></span> || 
| <span data-ttu-id="9012b-113">[Gérer des réseaux virtuels][6]</span><span class="sxs-lookup"><span data-stu-id="9012b-113">[Manage virtual networks][6]</span></span> | <span data-ttu-id="9012b-114">Configurez un réseau virtuel avec deux sous-réseaux et restreignez l’accès à Internet vers ces deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="9012b-114">Set up a virtual network with two subnets and restrict Internet access to them.</span></span> |
| <span data-ttu-id="9012b-115">**Créer des groupes identiques**</span><span class="sxs-lookup"><span data-stu-id="9012b-115">**Create scale sets**</span></span> ||
| <span data-ttu-id="9012b-116">[Créer un groupe de machines virtuelles identiques avec un équilibreur de charge][7]</span><span class="sxs-lookup"><span data-stu-id="9012b-116">[Create a virtual machine scale set with a load balancer][7]</span></span> | <span data-ttu-id="9012b-117">Créez un groupe de machines virtuelles identiques, configurez un équilibreur de charge et apportez des chaînes de connexion SSH aux machines virtuelles du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="9012b-117">Create a VM scale set, set up a load balancer, and get SSH connection strings to the scale set VMs.</span></span> |

[1]: ../java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[3]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-specialized-disk-from-vhd/
[4]: https://azure.microsoft.com/resources/samples/compute-java-manage-virtual-machines-in-parallel/
[5]: ../java-sdk-virtual-machines-in-parallel.md
[6]: ../java-sdk-manage-virtual-networks.md
[7]: ../java-sdk-manage-vm-scalesets.md