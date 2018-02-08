---
title: "Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour IntelliJ"
description: "Découvrez comment gérer vos comptes de stockage Azure à l’aide de l’Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4edb8c1ceef508dd251db693ccc3b98d77ec452b
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="8ffb2-103">Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8ffb2-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="8ffb2-104">L’Explorateur Azure, qui fait partie du Kit de ressources Azure pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour gérer les comptes de stockage de leur compte Azure à partir de l’environnement de développement intégré (IDE) IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="8ffb2-105">Créer un compte de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8ffb2-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="8ffb2-106">Pour créer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8ffb2-107">Connectez-vous à votre compte Azure en suivant les [Instructions de connexion pour le kit de ressources Azure pour IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="8ffb2-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for IntelliJ].</span></span> 

2. <span data-ttu-id="8ffb2-108">Dans la vue **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Comptes de stockage** puis cliquez sur **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Commande Créer un compte de stockage][CS01]

3. <span data-ttu-id="8ffb2-110">Dans la boîte de dialogue **Créer un compte de stockage**, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Boîte de dialogue Créer un compte de stockage][CS02]

   * <span data-ttu-id="8ffb2-112">**Nom** : spécifie le nom du nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="8ffb2-113">**Type de compte** : spécifie le type de compte de stockage à créer (par exemple, « Stockage Blob »).</span><span class="sxs-lookup"><span data-stu-id="8ffb2-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="8ffb2-114">Pour plus d’informations, consultez la rubrique [À propos des comptes de stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="8ffb2-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="8ffb2-115">**Performances** : spécifie l’offre de compte de stockage de l’éditeur sélectionné qu’il faut utiliser (par exemple « Premium »).</span><span class="sxs-lookup"><span data-stu-id="8ffb2-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="8ffb2-116">Pour plus d’informations, voir [Objectifs de scalabilité et de performances de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="8ffb2-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="8ffb2-117">**Réplication** : spécifie la réplication pour le compte de stockage (par exemple, « Redondant dans une zone »).</span><span class="sxs-lookup"><span data-stu-id="8ffb2-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="8ffb2-118">Pour plus d’informations, voir [Réplication de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="8ffb2-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="8ffb2-119">**Abonnement** : spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="8ffb2-120">**Emplacement** : spécifie l’emplacement où votre compte de stockage sera créé (par exemple « États-Unis de l’Ouest »).</span><span class="sxs-lookup"><span data-stu-id="8ffb2-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="8ffb2-121">**Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="8ffb2-122">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-122">Select one of the following options:</span></span>
      * <span data-ttu-id="8ffb2-123">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="8ffb2-124">**Utiliser l’existant** : spécifie que vous allez opérer un choix dans une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="8ffb2-125">Après avoir spécifié toutes les options ci-dessus, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="8ffb2-126">Créer un conteneur de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8ffb2-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="8ffb2-127">Pour créer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8ffb2-128">Dans l’Explorateur Azure, cliquez avec le bouton droit sur le compte de stockage dans lequel vous souhaitez créer un conteneur, puis cliquez sur **Créer un conteneur d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Commande de création d’un conteneur d’objets blob][CC01]

2. <span data-ttu-id="8ffb2-130">Dans la boîte de dialogue **Créer un conteneur d’objets blob**, spécifiez le nom de votre conteneur puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="8ffb2-131">Pour plus d’informations sur l’affectation de noms aux conteneurs de stockage, voir [Affectation de noms et de références aux conteneurs, objets blob et métadonnées].</span><span class="sxs-lookup"><span data-stu-id="8ffb2-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Boîte de dialogue de création d’un conteneur d’objets blob][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="8ffb2-133">Supprimer un conteneur de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8ffb2-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="8ffb2-134">Pour supprimer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8ffb2-135">Dans l’Explorateur Azure, cliquez avec le bouton droit sur le conteneur de stockage, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Commande de suppression d’un conteneur de stockage][DC01]

2. <span data-ttu-id="8ffb2-137">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-137">In the confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un conteneur de stockage][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="8ffb2-139">Supprimer un compte de stockage dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="8ffb2-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="8ffb2-140">Pour supprimer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="8ffb2-141">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le compte de stockage, puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Menu de suppression d’un compte de stockage][DS01]

2. <span data-ttu-id="8ffb2-143">Dans la fenêtre de confirmation, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="8ffb2-143">In the confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un compte de stockage][DS02]

## <a name="next-steps"></a><span data-ttu-id="8ffb2-145">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ffb2-145">Next steps</span></span>

<span data-ttu-id="8ffb2-146">Pour plus d’informations sur les comptes de stockage Azure, leurs tailles et leurs tarifications, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="8ffb2-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="8ffb2-147">[Introduction à Stockage Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="8ffb2-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="8ffb2-148">[À propos des comptes de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="8ffb2-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="8ffb2-149">Tailles des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8ffb2-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="8ffb2-150">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="8ffb2-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="8ffb2-151">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="8ffb2-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="8ffb2-152">Tarification des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8ffb2-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="8ffb2-153">[Tarification des comptes de stockage Windows]</span><span class="sxs-lookup"><span data-stu-id="8ffb2-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="8ffb2-154">[Tarification des comptes de stockage Linux]</span><span class="sxs-lookup"><span data-stu-id="8ffb2-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Instructions de connexion pour le kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Introduction à Stockage Microsoft Azure]: /azure/storage/storage-introduction
[À propos des comptes de stockage Azure]: /azure/storage/storage-create-storage-account
[Réplication de Stockage Azure]: /azure/storage/storage-redundancy
[Objectifs de scalabilité et de performances de Stockage Azure]: /azure/storage/storage-scalability-targets
[Affectation de noms et de références aux conteneurs, objets blob et métadonnées]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des comptes de stockage Windows]: /pricing/details/virtual-machines/windows/
[Tarification des comptes de stockage Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
