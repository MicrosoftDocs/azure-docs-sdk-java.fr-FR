---
title: Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour Eclipse
description: Découvrez comment gérer vos comptes de stockage Azure à l’aide de l’Explorateur Azure pour Eclipse.
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
ms.openlocfilehash: dc39298d88f2fb0b2f56d6fbc0071b68b8d27989
ms.sourcegitcommit: 24f037d133875f86761ec893dfa74e723de040b9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53636655"
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="0989a-103">Gérer des comptes de stockage à l’aide de l’Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="0989a-103">Manage storage accounts by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="0989a-104">L’Explorateur Azure, qui fait partie du kit de ressources Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour gérer les comptes de stockage de leur compte Azure à partir de l’environnement de développement intégré (IDE) Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0989a-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="0989a-105">Créer un compte de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="0989a-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="0989a-106">Pour créer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0989a-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0989a-107">Connectez-vous à votre compte Azure en suivant les [Instructions de connexion pour le kit de ressources Azure pour Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span><span class="sxs-lookup"><span data-stu-id="0989a-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse](https://docs.microsoft.com/java/azure/eclipse/azure-toolkit-for-eclipse-sign-in-instructions).</span></span>

1. <span data-ttu-id="0989a-108">Dans la vue **Explorateur Azure**, développez le nœud **Azure**, cliquez avec le bouton droit sur **Comptes de stockage** puis cliquez sur **Créer un compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="0989a-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Commande Créer un compte de stockage][CS01]

1. <span data-ttu-id="0989a-110">Dans la boîte de dialogue **Créer un compte de stockage**, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="0989a-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Boîte de dialogue Créer un compte de stockage][CS02]

   * <span data-ttu-id="0989a-112">**Nom** : spécifie le nom du nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0989a-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="0989a-113">**Abonnement**: spécifie l’abonnement Azure que vous voulez utiliser pour le nouveau compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="0989a-113">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="0989a-114">**Groupe de ressources** : spécifie le groupe de ressources pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0989a-114">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="0989a-115">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="0989a-115">Select one of the following options:</span></span>
      * <span data-ttu-id="0989a-116">**Créer** : spécifie que vous souhaitez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0989a-116">**Create New**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="0989a-117">**Utiliser l’existant** : spécifie que vous allez opérer un choix dans une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="0989a-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="0989a-118">**Région** : spécifie l’emplacement où votre compte de stockage sera créé (par exemple, « USA Ouest »).</span><span class="sxs-lookup"><span data-stu-id="0989a-118">**Region**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="0989a-119">**Type de compte** : spécifie le type de compte de stockage à créer (par exemple, « Stockage Blob »).</span><span class="sxs-lookup"><span data-stu-id="0989a-119">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="0989a-120">Pour plus d’informations, consultez la rubrique [À propos des comptes de stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="0989a-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="0989a-121">**Performances** : spécifie l’offre de compte de stockage de l’éditeur sélectionné qu’il faut utiliser (par exemple, « Premium »).</span><span class="sxs-lookup"><span data-stu-id="0989a-121">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="0989a-122">Pour plus d’informations, voir [Objectifs de scalabilité et de performances de Stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="0989a-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="0989a-123">**Réplication** : spécifie la réplication pour le compte de stockage (par exemple, « Redondant interzone »).</span><span class="sxs-lookup"><span data-stu-id="0989a-123">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="0989a-124">Pour plus d’informations, consultez [Réplication du stockage Azure].</span><span class="sxs-lookup"><span data-stu-id="0989a-124">For more information, see [Azure storage replication].</span></span>

1. <span data-ttu-id="0989a-125">Après avoir spécifié toutes les options ci-dessus, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0989a-125">When you have specified all of the preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="0989a-126">Créer un conteneur de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="0989a-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="0989a-127">Pour créer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0989a-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0989a-128">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le compte de stockage où vous voulez créer un conteneur puis cliquez sur **Créer un conteneur d’objets blob**.</span><span class="sxs-lookup"><span data-stu-id="0989a-128">In the **Azure Explorer** view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![Commande Créer un conteneur d’objets blob][CC01]

1. <span data-ttu-id="0989a-130">Dans la boîte de dialogue **Créer un conteneur d’objets blob**, spécifiez le nom de votre conteneur puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0989a-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="0989a-131">Pour plus d’informations sur l’affectation de noms aux conteneurs de stockage, consultez [Affectation de noms et références aux conteneurs, objets blob et métadonnées].</span><span class="sxs-lookup"><span data-stu-id="0989a-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Boîte de dialogue Créer un conteneur d’objets blob][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="0989a-133">Supprimer un conteneur de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="0989a-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="0989a-134">Pour supprimer un conteneur de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0989a-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0989a-135">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le conteneur de stockage puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="0989a-135">In the **Azure Explorer** view, right-click the storage container, and then click **Delete**.</span></span>

   ![Commande Supprimer un conteneur de stockage][DC01]

1. <span data-ttu-id="0989a-137">Dans la fenêtre de confirmation, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0989a-137">In the confirmation window, click **OK**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un conteneur de stockage][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="0989a-139">Supprimer un compte de stockage dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="0989a-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="0989a-140">Pour supprimer un compte de stockage à l’aide de l’Explorateur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0989a-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="0989a-141">Dans l’**Explorateur Azure**, cliquez avec le bouton droit sur le compte de stockage puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="0989a-141">In the **Azure Explorer** view, right-click the storage account, and then click **Delete**.</span></span>

   ![Commande Supprimer un compte de stockage][DS01]

1. <span data-ttu-id="0989a-143">Dans la fenêtre de confirmation, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0989a-143">In the confirmation window, click **OK**.</span></span>

   ![Fenêtre de confirmation de la suppression d’un compte de stockage][DS02]

## <a name="next-steps"></a><span data-ttu-id="0989a-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0989a-145">Next steps</span></span>

<span data-ttu-id="0989a-146">Pour plus d’informations sur les comptes de stockage Azure, leurs tailles et leurs tarifications, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="0989a-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="0989a-147">[Introduction à Microsoft Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="0989a-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="0989a-148">[À propos des comptes de stockage Azure]</span><span class="sxs-lookup"><span data-stu-id="0989a-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="0989a-149">Tailles des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0989a-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="0989a-150">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="0989a-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="0989a-151">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="0989a-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="0989a-152">Tarification des comptes de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0989a-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="0989a-153">[Tarification des comptes de stockage Windows]</span><span class="sxs-lookup"><span data-stu-id="0989a-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="0989a-154">[Tarification des comptes de stockage Linux]</span><span class="sxs-lookup"><span data-stu-id="0989a-154">[Linux storage-account pricing]</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

[Introduction à Microsoft Azure Storage]: /azure/storage/storage-introduction
[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction
[À propos des comptes de stockage Azure]: /azure/storage/storage-create-storage-account
[About Azure storage accounts]: /azure/storage/storage-create-storage-account
[Réplication du stockage Azure]: /azure/storage/storage-redundancy
[Azure storage replication]: /azure/storage/storage-redundancy
[Objectifs de scalabilité et de performances de Stockage Azure]: /azure/storage/storage-scalability-targets
[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets
[Affectation de noms et références aux conteneurs, objets blob et métadonnées]: http://go.microsoft.com/fwlink/?LinkId=255555
[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des comptes de stockage Windows]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Windows storage-account pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/windows/
[Tarification des comptes de stockage Linux]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/
[Linux storage-account pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
