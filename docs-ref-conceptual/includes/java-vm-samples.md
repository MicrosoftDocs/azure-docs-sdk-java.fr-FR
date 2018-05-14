| **Créer des machines virtuelles** || 
|---|---|
| [Gérer des machines virtuelles][1] | Créez, modifiez, démarrez, arrêtez et supprimez des machines virtuelles. |
| [Créer une machine virtuelle à partir d’une image personnalisée][2] | Créez une image de machine virtuelle personnalisée et utilisez-la pour créer de nouvelles machines virtuelles. | 
| [Créer une machine virtuelle à l’aide d’un VHD spécialisé à partir d’une capture instantanée][3] | Créez une capture instantanée à partir du système d’exploitation de la machine virtuelle et des disques de données, créez des disques gérés à partir des captures instantanées, puis créez une machine virtuelle en joignant les disques gérés. |  
| [Créer des machines virtuelles en parallèle dans le même réseau][4] | Créez des machines virtuelles dans la même région sur le même réseau virtuel avec deux sous-réseaux en parallèle. |
| [Créer des machines virtuelles entre des régions en parallèle][5] | Créez et équilibrez la charge d’un ensemble de machines virtuelles entre plusieurs régions Azure. |
| **Mettre en réseau des machines virtuelles** || 
| [Gérer des réseaux virtuels][6] | Configurez un réseau virtuel avec deux sous-réseaux et restreignez l’accès à Internet vers ces deux sous-réseaux. |
| **Créer des groupes identiques** ||
| [Créer un groupe de machines virtuelles identiques avec un équilibreur de charge][7] | Créez un groupe de machines virtuelles identiques, configurez un équilibreur de charge et apportez des chaînes de connexion SSH aux machines virtuelles du groupe identique. |

[1]: ../java-sdk-manage-virtual-machines.md
[2]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-custom-image/
[3]: https://azure.microsoft.com/resources/samples/managed-disk-java-create-virtual-machine-using-specialized-disk-from-vhd/
[4]: https://azure.microsoft.com/resources/samples/compute-java-manage-virtual-machines-in-parallel/
[5]: ../java-sdk-virtual-machines-in-parallel.md
[6]: ../java-sdk-manage-virtual-networks.md
[7]: ../java-sdk-manage-vm-scalesets.md