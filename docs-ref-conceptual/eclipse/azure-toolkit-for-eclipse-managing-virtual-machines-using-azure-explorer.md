---
title: Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour Eclipse
description: Découvrez comment gérer vos machines virtuelles Azure à l’aide de l’Explorateur Azure pour Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: ec67ed44ec570da7b826c12a9f8a24a5b0170e99
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2018
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a>Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour Eclipse

L’Explorateur Azure, qui fait partie du Kit de ressources Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour gérer les machines virtuelles de leur compte Azure à partir de l’environnement de développement intégré (IDE) Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a>Création d’une machine virtuelle dans Eclipse

Pour créer une machine virtuelle à l’aide de l’Explorateur Azure, procédez comme suit :

1. Connectez-vous à votre compte Azure en suivant les [Instructions de connexion pour le Kit de ressources Azure pour Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).

1. Dans l’affichage **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Machines virtuelles**, puis cliquez sur **Créer une machine virtuelle**.

   ![Commande Créer une machine virtuelle][CR01]  

   L’**Assistant Créer une machine virtuelle** s’ouvre.

1. Dans la fenêtre **Choisir un abonnement**, sélectionnez votre abonnement, puis cliquez sur **Suivant**.

   ![Fenêtre Choisir un abonnement][CR02]

1. Dans la fenêtre **Sélectionner une image de machine virtuelle**, entrez les informations suivantes :

   * **Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*).

   * **Éditeur** : spécifie l’éditeur qui a créé l’image et que vous allez utiliser pour créer votre machine virtuelle, par exemple *Microsoft*.

   * **Offre** : spécifie la machine virtuelle et l’offre de l’éditeur sélectionné à utiliser (par exemple, *JDK*).

   * **Référence (SKU)**  : spécifie l’unité de gestion de stock (SKU) de l’offre sélectionnée à utiliser (par exemple, *JDK_8*).

   * **N° de version** : spécifie la version de la référence (SKU) sélectionnée à utiliser.

   ![Fenêtre Sélectionner une image de machine virtuelle][CR03]

1. Cliquez sur **Suivant**.

1. Dans la fenêtre **Paramètres de base de la machine virtuelle**, entrez les informations suivantes :

   * **Nom de la machine virtuelle** : spécifie le nom de votre nouvelle machine virtuelle, qui doit commencer par une lettre et contenir uniquement des lettres, des chiffres et des traits d’union.

   * **Taille** : spécifie le nombre de cœurs et la quantité de mémoire à allouer à votre machine virtuelle.

   * **Nom d’utilisateur** : spécifie le compte administrateur à créer pour la gestion de votre machine virtuelle.

   * **Mot de passe** et **Confirmer** : spécifient le mot de passe pour votre compte administrateur.

   ![Fenêtre Paramètres de base de la machine virtuelle][CR04]

1. Cliquez sur **Suivant**.

1. Dans la fenêtre **Créer un nouveau compte de stockage**, saisissez les informations suivantes :

   * **Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle. Sélectionnez l’une des options suivantes :
      * **Créer** : spécifie que vous souhaitez créer un groupe de ressources.
      * **Utiliser l’existant** : spécifie que vous souhaitez sélectionner un groupe de ressources déjà associé à votre compte Azure.

      ![La boîte de dialogue Créer un compte de stockage][CR05]

   * **Compte de stockage** : spécifie le compte de stockage à utiliser pour le stockage de votre machine virtuelle. Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.

   * **Réseau virtuel** et **sous-réseau** : spécifient le réseau virtuel et le sous-réseau auquel se connectera votre machine virtuelle. Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau. Si vous sélectionnez **Créer**, la boîte de dialogue suivante s’affiche :

      ![La boîte de dialogue Créer un réseau virtuel][CR06]

1. Dans la fenêtre **Ressources associées**, entrez les informations suivantes :

   * **Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle. Vous pouvez choisir de créer une adresse IP ou, si votre machine virtuelle n’a pas besoin d’adresse IP publique, vous pouvez sélectionner **(Aucune)**.

   * **Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle. Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**.

   * **Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir. Vous pouvez sélectionner un groupe à haute disponibilité, créer un groupe à haute disponibilité ou, si votre machine virtuelle ne doit pas appartenir à un groupe à haute disponibilité, vous pouvez sélectionner **(Aucun)**.

   ![Fenêtre ressources associées][CR07]

1. Cliquez sur **Terminer**.  

   Votre nouvelle machine virtuelle s’affiche dans la fenêtre de l’outil Explorateur Azure.

   ![Nouvelle machine virtuelle][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a>Redémarrage d’une machine virtuelle dans Eclipse

Pour redémarrer une machine virtuelle à l’aide de l’Explorateur Azure dans Eclipse, procédez comme suit :

1. Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Redémarrer**.

   ![Commande Redémarrer de la machine virtuelle][RE01]

1. Dans la fenêtre de confirmation, cliquez sur **Oui**.

   ![La fenêtre de confirmation de redémarrage][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a>Arrêt d’une machine virtuelle dans Eclipse

Pour arrêter une machine virtuelle en cours d’exécution à l’aide de l’Explorateur Azure dans Eclipse, procédez comme suit :

1. Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Arrêter**.

   ![Commande Arrêter de la machine virtuelle][SH01]

1. Dans la fenêtre de confirmation, cliquez sur **Oui**.

   ![La fenêtre de confirmation d’arrêt de machine virtuelle][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a>Suppression d’une machine virtuelle dans Eclipse

Pour supprimer une machine virtuelle à l’aide de l’Explorateur Azure dans Eclipse, procédez comme suit :

1. Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Supprimer**.

   ![Commande Supprimer de la machine virtuelle][DE01]

1. Dans la fenêtre de confirmation, cliquez sur **Oui**.

   ![La fenêtre de confirmation de suppression de machine virtuelle][DE02]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les tailles et tarifications des machines virtuelles Azure, voir les ressources suivantes :

* Tailles des machines virtuelles Azure
  * [Tailles des machines virtuelles Windows dans Azure]
  * [Tailles des machines virtuelles Linux dans Azure]
* Tarification des machines virtuelles Azure
  * [Tarification des machines virtuelles Windows]
  * [Tarification des machines virtuelles Linux]

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
