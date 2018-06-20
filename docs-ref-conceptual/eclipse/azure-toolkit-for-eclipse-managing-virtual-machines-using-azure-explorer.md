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
ms.locfileid: "34283047"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="e3b42-103">Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="e3b42-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="e3b42-104">L’Explorateur Azure, qui fait partie du Kit de ressources Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour gérer les machines virtuelles de leur compte Azure à partir de l’environnement de développement intégré (IDE) Eclipse.</span><span class="sxs-lookup"><span data-stu-id="e3b42-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e3b42-105">Création d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="e3b42-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="e3b42-106">Pour créer une machine virtuelle à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b42-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="e3b42-107">Connectez-vous à votre compte Azure en suivant les [Instructions de connexion pour le Kit de ressources Azure pour Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="e3b42-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

1. <span data-ttu-id="e3b42-108">Dans l’affichage **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Machines virtuelles**, puis cliquez sur **Créer une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   ![Commande Créer une machine virtuelle][CR01]  

   <span data-ttu-id="e3b42-110">L’**Assistant Créer une machine virtuelle** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e3b42-110">The **Create new Virtual Machine** wizard opens.</span></span>

1. <span data-ttu-id="e3b42-111">Dans la fenêtre **Choisir un abonnement**, sélectionnez votre abonnement, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Fenêtre Choisir un abonnement][CR02]

1. <span data-ttu-id="e3b42-113">Dans la fenêtre **Sélectionner une image de machine virtuelle**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3b42-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="e3b42-114">**Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*).</span><span class="sxs-lookup"><span data-stu-id="e3b42-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="e3b42-115">**Éditeur** : spécifie l’éditeur qui a créé l’image et que vous allez utiliser pour créer votre machine virtuelle, par exemple *Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="e3b42-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="e3b42-116">**Offre** : spécifie la machine virtuelle et l’offre de l’éditeur sélectionné à utiliser (par exemple, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="e3b42-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="e3b42-117">**Référence (SKU)**  : spécifie l’unité de gestion de stock (SKU) de l’offre sélectionnée à utiliser (par exemple, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="e3b42-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="e3b42-118">**N° de version** : spécifie la version de la référence (SKU) sélectionnée à utiliser.</span><span class="sxs-lookup"><span data-stu-id="e3b42-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Fenêtre Sélectionner une image de machine virtuelle][CR03]

1. <span data-ttu-id="e3b42-120">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-120">Click **Next**.</span></span>

1. <span data-ttu-id="e3b42-121">Dans la fenêtre **Paramètres de base de la machine virtuelle**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3b42-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="e3b42-122">**Nom de la machine virtuelle** : spécifie le nom de votre nouvelle machine virtuelle, qui doit commencer par une lettre et contenir uniquement des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="e3b42-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="e3b42-123">**Taille** : spécifie le nombre de cœurs et la quantité de mémoire à allouer à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="e3b42-124">**Nom d’utilisateur** : spécifie le compte administrateur à créer pour la gestion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="e3b42-125">**Mot de passe** et **Confirmer** : spécifient le mot de passe pour votre compte administrateur.</span><span class="sxs-lookup"><span data-stu-id="e3b42-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Fenêtre Paramètres de base de la machine virtuelle][CR04]

1. <span data-ttu-id="e3b42-127">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-127">Click **Next**.</span></span>

1. <span data-ttu-id="e3b42-128">Dans la fenêtre **Créer un nouveau compte de stockage**, saisissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3b42-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="e3b42-129">**Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="e3b42-130">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3b42-130">Select one of the following options:</span></span>
      * <span data-ttu-id="e3b42-131">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="e3b42-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="e3b42-132">**Utiliser l’existant** : spécifie que vous souhaitez sélectionner un groupe de ressources déjà associé à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b42-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![La boîte de dialogue Créer un compte de stockage][CR05]

   * <span data-ttu-id="e3b42-134">**Compte de stockage** : spécifie le compte de stockage à utiliser pour le stockage de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="e3b42-135">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="e3b42-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="e3b42-136">**Réseau virtuel** et **sous-réseau** : spécifient le réseau virtuel et le sous-réseau auquel se connectera votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="e3b42-137">Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="e3b42-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="e3b42-138">Si vous sélectionnez **Créer**, la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="e3b42-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![La boîte de dialogue Créer un réseau virtuel][CR06]

1. <span data-ttu-id="e3b42-140">Dans la fenêtre **Ressources associées**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3b42-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="e3b42-141">**Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="e3b42-142">Vous pouvez choisir de créer une adresse IP ou, si votre machine virtuelle n’a pas besoin d’adresse IP publique, vous pouvez sélectionner **(Aucune)**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="e3b42-143">**Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e3b42-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="e3b42-144">Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="e3b42-145">**Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir.</span><span class="sxs-lookup"><span data-stu-id="e3b42-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="e3b42-146">Vous pouvez sélectionner un groupe à haute disponibilité, créer un groupe à haute disponibilité ou, si votre machine virtuelle ne doit pas appartenir à un groupe à haute disponibilité, vous pouvez sélectionner **(Aucun)**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![Fenêtre ressources associées][CR07]

1. <span data-ttu-id="e3b42-148">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-148">Click **Finish**.</span></span>  

   <span data-ttu-id="e3b42-149">Votre nouvelle machine virtuelle s’affiche dans la fenêtre de l’outil Explorateur Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b42-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Nouvelle machine virtuelle][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e3b42-151">Redémarrage d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="e3b42-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="e3b42-152">Pour redémarrer une machine virtuelle à l’aide de l’Explorateur Azure dans Eclipse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b42-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="e3b42-153">Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Commande Redémarrer de la machine virtuelle][RE01]

1. <span data-ttu-id="e3b42-155">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-155">In the confirmation window, click **Yes**.</span></span>

   ![La fenêtre de confirmation de redémarrage][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e3b42-157">Arrêt d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="e3b42-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="e3b42-158">Pour arrêter une machine virtuelle en cours d’exécution à l’aide de l’Explorateur Azure dans Eclipse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b42-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="e3b42-159">Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Commande Arrêter de la machine virtuelle][SH01]

1. <span data-ttu-id="e3b42-161">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-161">In the confirmation window, click **Yes**.</span></span>

   ![La fenêtre de confirmation d’arrêt de machine virtuelle][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e3b42-163">Suppression d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="e3b42-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="e3b42-164">Pour supprimer une machine virtuelle à l’aide de l’Explorateur Azure dans Eclipse, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e3b42-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="e3b42-165">Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Commande Supprimer de la machine virtuelle][DE01]

1. <span data-ttu-id="e3b42-167">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="e3b42-167">In the confirmation window, click **Yes**.</span></span>

   ![La fenêtre de confirmation de suppression de machine virtuelle][DE02]

## <a name="next-steps"></a><span data-ttu-id="e3b42-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e3b42-169">Next steps</span></span>

<span data-ttu-id="e3b42-170">Pour plus d’informations sur les tailles et tarifications des machines virtuelles Azure, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="e3b42-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="e3b42-171">Tailles des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e3b42-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="e3b42-172">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="e3b42-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="e3b42-173">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="e3b42-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="e3b42-174">Tarification des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="e3b42-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="e3b42-175">[Tarification des machines virtuelles Windows]</span><span class="sxs-lookup"><span data-stu-id="e3b42-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="e3b42-176">[Tarification des machines virtuelles Linux]</span><span class="sxs-lookup"><span data-stu-id="e3b42-176">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

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
