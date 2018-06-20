---
title: Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour IntelliJ
description: Découvrez comment gérer vos machines virtuelles Azure à l’aide de l’Explorateur Azure pour IntelliJ.
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
ms.openlocfilehash: 213efa7fc31705b0ffcba6f2fe40e7186a365fae
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
ms.locfileid: "28954870"
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="fee52-103">Gérer des machines virtuelles à l’aide de l’Explorateur Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="fee52-103">Manage virtual machines by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="fee52-104">L’Explorateur Azure, qui fait partie du Kit de ressources Azure pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour gérer les machines virtuelles de leur compte Azure à partir de l’environnement de développement intégré (IDE) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="fee52-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="fee52-105">Suppression d’une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="fee52-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="fee52-106">Pour créer une machine virtuelle à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fee52-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span> 

1. <span data-ttu-id="fee52-107">Connectez-vous à votre compte Azure en procédant de la manière décrite dans l’article [Instructions de connexion pour le Kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="fee52-107">Sign in to your Azure account by using the steps in the [Sign-in instructions for the Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="fee52-108">Dans l’affichage **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Machines virtuelles**, puis cliquez sur **Créer une machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="fee52-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="fee52-109">![Commande Créer une machine virtuelle][CR01]</span><span class="sxs-lookup"><span data-stu-id="fee52-109">![The Create VM command][CR01]</span></span>  
    <span data-ttu-id="fee52-110">L’**Assistant Créer une machine virtuelle** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="fee52-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="fee52-111">Dans la fenêtre **Choisir un abonnement**, sélectionnez votre abonnement, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fee52-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Fenêtre Choisir un abonnement][CR02]

4. <span data-ttu-id="fee52-113">Dans la fenêtre **Sélectionner une image de machine virtuelle**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee52-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="fee52-114">**Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*).</span><span class="sxs-lookup"><span data-stu-id="fee52-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="fee52-115">**Image recommandée** : spécifie que vous allez choisir une image dans une liste abrégée d’images couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="fee52-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="fee52-116">**Image personnalisée** : spécifie que vous allez choisir une image personnalisée en fournissant les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee52-116">**Custom image**: Specifies that you will choose a custom image by providing the following information:</span></span>

      * <span data-ttu-id="fee52-117">**Éditeur**: spécifie l’éditeur qui a créé l’image que vous allez utiliser pour votre machine virtuelle (par exemple, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="fee52-117">**Publisher**: Specifies the publisher that created the image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="fee52-118">**Offre** : spécifie la machine virtuelle et l’offre de l’éditeur sélectionné à utiliser (par exemple, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="fee52-118">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="fee52-119">**Référence (SKU)**  : spécifie l’unité de gestion de stock (SKU) de l’offre sélectionnée à utiliser (par exemple, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="fee52-119">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="fee52-120">**N° de version** : spécifie la version de la référence (SKU) sélectionnée à utiliser.</span><span class="sxs-lookup"><span data-stu-id="fee52-120">**Version #**: Specifies which version of the selected SKU to use.</span></span>

   ![Fenêtre Sélectionner une image de machine virtuelle][CR03]

5. <span data-ttu-id="fee52-122">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fee52-122">Click **Next**.</span></span> 

6. <span data-ttu-id="fee52-123">Dans la fenêtre **Paramètres de base de la machine virtuelle**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee52-123">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="fee52-124">**Nom de la machine virtuelle**: spécifie le nom de votre nouvelle machine virtuelle, qui doit commencer par une lettre et ne peut contenir que des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="fee52-124">**Virtual machine name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="fee52-125">**Taille** : spécifie le nombre de cœurs et la quantité de mémoire à allouer à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-125">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="fee52-126">**Nom d’utilisateur** : spécifie le compte administrateur à créer pour la gestion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-126">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="fee52-127">**Mot de passe** et **Confirmer** : spécifient le mot de passe pour votre compte administrateur.</span><span class="sxs-lookup"><span data-stu-id="fee52-127">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

   ![Fenêtre Paramètres de base de la machine virtuelle][CR04]

7. <span data-ttu-id="fee52-129">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fee52-129">Click **Next**.</span></span> 

8. <span data-ttu-id="fee52-130">Dans la fenêtre **Ressources associées**, entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee52-130">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="fee52-131">**Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-131">**Resource group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="fee52-132">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee52-132">Select one of the following options:</span></span>
      * <span data-ttu-id="fee52-133">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fee52-133">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="fee52-134">**Utiliser l’existant** : spécifie que vous souhaitez opérer une sélection dans la liste des groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="fee52-134">**Use existing**: Specifies that you want to select from a list of resource groups that are associated with your Azure account.</span></span>

       ![Fenêtre ressources associées][CR07]

   * <span data-ttu-id="fee52-136">**Compte de stockage** : spécifie le compte de stockage à utiliser pour le stockage de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-136">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="fee52-137">Vous pouvez choisir un compte de stockage ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="fee52-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="fee52-138">Si vous choisissez **Créer**, la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="fee52-138">If you choose **Create New**, the following dialog box appears:</span></span>

      ![Boîte de dialogue Créer un compte de stockage][CR05]

   * <span data-ttu-id="fee52-140">**Réseau virtuel** et **sous-réseau** : spécifient le réseau virtuel et le sous-réseau auquel se connectera votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-140">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="fee52-141">Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="fee52-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="fee52-142">Si vous sélectionnez **Créer**, la boîte de dialogue suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="fee52-142">If you select **Create new**, the following dialog box appears:</span></span>

      ![Boîte de dialogue Créer un réseau virtuel][CR06]

   * <span data-ttu-id="fee52-144">**Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="fee52-145">Vous pouvez choisir de créer une adresse IP ou, si votre machine virtuelle n’a pas besoin d’adresse IP publique, vous pouvez sélectionner **(Aucune)**.</span><span class="sxs-lookup"><span data-stu-id="fee52-145">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="fee52-146">**Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fee52-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="fee52-147">Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**.</span><span class="sxs-lookup"><span data-stu-id="fee52-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="fee52-148">**Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir.</span><span class="sxs-lookup"><span data-stu-id="fee52-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="fee52-149">Vous pouvez sélectionner un groupe à haute disponibilité, créer un groupe à haute disponibilité ou, si votre machine virtuelle ne doit pas appartenir à un groupe à haute disponibilité, sélectionner **(Aucun)**.</span><span class="sxs-lookup"><span data-stu-id="fee52-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong to an availability set, select **(None)**.</span></span>

9. <span data-ttu-id="fee52-150">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="fee52-150">Click **Finish**.</span></span>  
    <span data-ttu-id="fee52-151">Votre nouvelle machine virtuelle apparaît dans la fenêtre de l’outil Explorateur Azure.</span><span class="sxs-lookup"><span data-stu-id="fee52-151">Your new virtual machine appears in the Azure Explorer tool window.</span></span> 

   ![Nouvel machine virtuelle dans l’affichage de l’Explorateur Azure][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="fee52-153">Redémarrer une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="fee52-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="fee52-154">Pour redémarrer une machine virtuelle à l’aide de l’Explorateur Azure dans IntelliJ, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fee52-154">To restart a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="fee52-155">Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="fee52-155">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Commande Redémarrer de la machine virtuelle][RE01]

2. <span data-ttu-id="fee52-157">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="fee52-157">In the confirmation window, click **Yes**.</span></span> 

   ![Fenêtre de confirmation de redémarrage de machine virtuelle][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="fee52-159">Arrêter une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="fee52-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="fee52-160">Pour arrêter une machine virtuelle en cours d’exécution à l’aide de l’Explorateur Azure dans IntelliJ, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fee52-160">To shut down a running virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="fee52-161">Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Arrêter**.</span><span class="sxs-lookup"><span data-stu-id="fee52-161">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Commande Arrêter de la machine virtuelle][SH01]

2. <span data-ttu-id="fee52-163">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="fee52-163">In the confirmation window, click **Yes**.</span></span> 

   ![Fenêtre de confirmation d’arrêt de la machine virtuelle][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="fee52-165">Supprimer une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="fee52-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="fee52-166">Pour supprimer une machine virtuelle à l’aide de l’Explorateur Azure dans IntelliJ, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fee52-166">To delete a virtual machine by using the Azure Explorer in IntelliJ, do the following:</span></span>

1. <span data-ttu-id="fee52-167">Dans l’affichage **Explorateur Azure**, cliquez avec le bouton droit sur la machine virtuelle, puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="fee52-167">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Commande Supprimer de la machine virtuelle][DE01]

2. <span data-ttu-id="fee52-169">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="fee52-169">In the confirmation window, click **Yes**.</span></span> 

   ![Fenêtre de confirmation de suppression de machine virtuelle][DE02]

## <a name="next-steps"></a><span data-ttu-id="fee52-171">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fee52-171">Next steps</span></span>

<span data-ttu-id="fee52-172">Pour plus d’informations sur les tailles et tarifications des machines virtuelles Azure, voir les ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="fee52-172">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="fee52-173">Tailles des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="fee52-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="fee52-174">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="fee52-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="fee52-175">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="fee52-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="fee52-176">Tarification des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="fee52-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="fee52-177">[Tarification des machines virtuelles Windows]</span><span class="sxs-lookup"><span data-stu-id="fee52-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="fee52-178">[Tarification des machines virtuelles Linux]</span><span class="sxs-lookup"><span data-stu-id="fee52-178">[Linux virtual-machine pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Instructions de connexion pour le Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/
[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/

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
