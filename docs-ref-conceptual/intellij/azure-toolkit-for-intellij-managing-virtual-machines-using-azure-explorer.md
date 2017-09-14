---
title: "Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour IntelliJ"
description: "Découvrez comment gérer vos machines virtuelles Azure à l’aide de l’Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: fb175a44235a8ff27675dd42905237a8826f91fe
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a>Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour IntelliJ

L’Explorateur Azure, qui fait partie du Kit de ressources Azure pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour gérer les machines virtuelles de leur compte Azure à partir de l’environnement de développement intégré (IDE) IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a>Suppression d’une machine virtuelle dans IntelliJ

Pour créer une machine virtuelle à l’aide de l’Explorateur Azure, procédez comme suit : 

1. Connectez-vous à votre compte Azure en procédant de la manière décrite dans l’article [Instructions de connexion pour le Kit de ressources Azure pour IntelliJ].

2. Dans l’affichage **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Machines virtuelles**, puis cliquez sur **Créer une machine virtuelle**. 

   ![Commande Créer une machine virtuelle][CR01]  
    L’**Assistant Créer une machine virtuelle** s’ouvre.

3. Dans la fenêtre **Choisir un abonnement**, sélectionnez votre abonnement, puis cliquez sur **Suivant**. 

   ![Fenêtre Choisir un abonnement][CR02]

4. Dans la fenêtre **Sélectionner une image de machine virtuelle**, entrez les informations suivantes :

   * **Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*). 

   * **Image recommandée** : spécifie que vous allez choisir une image dans une liste abrégée d’images couramment utilisées.

   * **Image personnalisée** : spécifie que vous allez choisir une image personnalisée en fournissant les informations suivantes :

      * **Éditeur**: spécifie l’éditeur qui a créé l’image que vous allez utiliser pour votre machine virtuelle (par exemple, *Microsoft*).

      * **Offre** : spécifie la machine virtuelle et l’offre de l’éditeur sélectionné à utiliser (par exemple, *JDK*).

      * **Référence (SKU)** : spécifie l’unité de gestion de stock (SKU) de l’offre sélectionnée à utiliser (par exemple, *JDK_8*).

      * **N° de version** : spécifie la version de la référence (SKU) sélectionnée à utiliser.

   ![Fenêtre Sélectionner une image de machine virtuelle][CR03]

5. Cliquez sur **Suivant**. 

6. Dans la fenêtre **Paramètres de base de la machine virtuelle**, entrez les informations suivantes :

   * **Nom de la machine virtuelle**: spécifie le nom de votre nouvelle machine virtuelle, qui doit commencer par une lettre et ne peut contenir que des lettres, des chiffres et des traits d’union.

   * **Taille** : spécifie le nombre de cœurs et la quantité de mémoire à allouer à votre machine virtuelle.

   * **Nom d’utilisateur** : spécifie le compte administrateur à créer pour la gestion de votre machine virtuelle.

   * **Mot de passe** et **Confirmer** : spécifient le mot de passe pour votre compte administrateur.

   ![Fenêtre Paramètres de base de la machine virtuelle][CR04]

7. Cliquez sur **Suivant**. 

8. Dans la fenêtre **Ressources associées**, entrez les informations suivantes :

   * **Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle. Sélectionnez l’une des options suivantes :
      * **Créer** : spécifie que vous souhaitez créer un groupe de ressources.
      * **Utiliser l’existant** : spécifie que vous souhaitez opérer une sélection dans la liste des groupes de ressources associés à votre compte Azure.

       ![Fenêtre ressources associées][CR07]

   * **Compte de stockage** : spécifie le compte de stockage à utiliser pour le stockage de votre machine virtuelle. Vous pouvez choisir un compte de stockage ou en créer un. Si vous choisissez **Créer**, la boîte de dialogue suivante s’affiche :

      ![Boîte de dialogue Créer un compte de stockage][CR05]

   * **Réseau virtuel** et **sous-réseau** : spécifient le réseau virtuel et le sous-réseau auquel se connectera votre machine virtuelle. Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau. Si vous sélectionnez **Créer**, la boîte de dialogue suivante s’affiche :

      ![Boîte de dialogue Créer un réseau virtuel][CR06]

   * **Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle. Vous pouvez choisir de créer une adresse IP ou, si votre machine virtuelle n’a pas besoin d’adresse IP publique, vous pouvez sélectionner **(Aucune)**. 

   * **Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle. Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**. 

   * **Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir. Vous pouvez sélectionner un groupe à haute disponibilité, créer un groupe à haute disponibilité ou, si votre machine virtuelle ne doit pas appartenir à un groupe à haute disponibilité, sélectionner **(Aucun)**.

9. Cliquez sur **Terminer**.  
    Votre nouvelle machine virtuelle apparaît dans la fenêtre de l’outil Explorateur Azure. 

   ![Nouvel machine virtuelle dans l’affichage de l’Explorateur Azure][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a>Redémarrer une machine virtuelle dans IntelliJ

Pour redémarrer une machine virtuelle à l’aide de l’Explorateur Azure dans IntelliJ, procédez comme suit :

1. Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Redémarrer**.

   ![Commande Redémarrer de la machine virtuelle][RE01]

2. Dans la fenêtre de confirmation, cliquez sur **Oui**. 

   ![Fenêtre de confirmation de redémarrage de machine virtuelle][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a>Arrêter une machine virtuelle dans IntelliJ

Pour arrêter une machine virtuelle en cours d’exécution à l’aide de l’Explorateur Azure dans IntelliJ, procédez comme suit :

1. Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Arrêter**.

   ![Commande Arrêter de la machine virtuelle][SH01]

2. Dans la fenêtre de confirmation, cliquez sur **Oui**. 

   ![Fenêtre de confirmation d’arrêt de la machine virtuelle][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a>Supprimer une machine virtuelle dans IntelliJ

Pour supprimer une machine virtuelle à l’aide de l’Explorateur Azure dans IntelliJ, procédez comme suit :

1. Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Supprimer**.

   ![Commande Supprimer de la machine virtuelle][DE01]

2. Dans la fenêtre de confirmation, cliquez sur **Oui**. 

   ![Fenêtre de confirmation de suppression de machine virtuelle][DE02]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les tailles et tarifications des machines virtuelles Azure, voir les ressources suivantes :

* Tailles des machines virtuelles Azure
  * [Tailles des machines virtuelles Windows dans Azure]
  * [Tailles des machines virtuelles Linux dans Azure]
* Tarification des machines virtuelles Azure
  * [Tarification des machines virtuelles Windows]
  * [Tarification des machines virtuelles Linux]

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
