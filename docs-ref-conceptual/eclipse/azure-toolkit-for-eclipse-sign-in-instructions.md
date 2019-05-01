---
title: Instructions de connexion pour le kit de ressources Azure pour Eclipse
description: Découvrez comment vous connecter à Microsoft Azure à l’aide du kit de ressources Azure pour Eclipse.
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
ms.openlocfilehash: 79f6cfd3b21d68c131a3f0052d86e4bcb3254e55
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61591003"
---
# <a name="azure-sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="09c47-103">Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="09c47-103">Azure Sign In Instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="09c47-104">Le kit de ressources Azure pour Eclipse propose deux méthodes pour vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="09c47-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  * <span data-ttu-id="09c47-105">**Automatisée** : si vous utilisez cette méthode, vous devez créer un fichier d’informations d’identification qui contiendra vos données de principal de service, après quoi vous pourrez utiliser le fichier d’informations d’identification pour vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="09c47-105">**Automated** - when you are using this method, you will create a credentials file which contains your service principal data, after which you can use the credentials file to automatically sign into your Azure account.</span></span>
  * <span data-ttu-id="09c47-106">**Interactive** : si vous utilisez cette méthode, vous devez entrer vos informations d’identification Azure à chaque fois que vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="09c47-106">**Interactive** - when you are using this method, you will enter your Azure credentials each time you sign into your Azure account.</span></span>

<span data-ttu-id="09c47-107">Les étapes décrites dans les sections suivantes décrivent l’utilisation de chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="09c47-107">The steps in the following sections will describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="signing-into-your-azure-account-automatically-and-creating-a-credentials-file-to-use-in-the-future"></a><span data-ttu-id="09c47-108">Connexion automatique à votre compte Azure et création d’un fichier d’informations d’identification à utiliser à l’avenir</span><span class="sxs-lookup"><span data-stu-id="09c47-108">Signing into your Azure account automatically and creating a credentials file to use in the future</span></span>

<span data-ttu-id="09c47-109">La procédure suivante vous guide dans la création d’un fichier d’informations d’identification qui contient vos données de principal de service.</span><span class="sxs-lookup"><span data-stu-id="09c47-109">The following steps will walk you through creating a credentials file which contains your service principal data.</span></span> <span data-ttu-id="09c47-110">Une fois que vous avez effectué ces étapes, Eclipse utilise automatiquement le fichier d’informations d’identification pour vous connecter automatiquement à Azure à chaque fois que vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="09c47-110">Once you have completed these steps, Eclipse will automatically use the credentials file to automatically sign you into Azure each time you open your project.</span></span>

1. <span data-ttu-id="09c47-111">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="09c47-111">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="09c47-112">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-112">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. <span data-ttu-id="09c47-114">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, sélectionnez **Automatisée**, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="09c47-114">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **New**.</span></span>

   ![Boîte de dialogue Se connecter][A02]

1. <span data-ttu-id="09c47-116">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-116">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A03]

1. <span data-ttu-id="09c47-118">Lorsque la boîte de dialogue **Create authentication files (Créer des fichiers d’authentification)** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="09c47-118">When the **Create authentication files** dialog box appears, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A04]

1. <span data-ttu-id="09c47-120">La boîte de dialogue **Service Principal Creation Status (État de création du principal de service)** s’affiche, et une fois que vos fichiers ont été créés, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="09c47-120">The **Service Principal Creatation Status** dialog box will be displayed, and after your files have been created successfully, click **OK**.</span></span>

   ![Boîte de dialogue Service Principal Creation Status (État de création du principal de service)][A05]

1. <span data-ttu-id="09c47-122">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-122">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="09c47-124">Lorsque la boîte de dialogue **Sélectionner des abonnements** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="09c47-124">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-automatically"></a><span data-ttu-id="09c47-126">Déconnexion de votre compte Azure lorsque vous vous êtes connecté automatiquement</span><span class="sxs-lookup"><span data-stu-id="09c47-126">Signing out of your Azure account when you signed in automatically</span></span>

<span data-ttu-id="09c47-127">Après avoir configuré les étapes indiquées dans la section précédente, le kit de ressources Azure vous connecte automatiquement à votre compte Azure à chaque redémarrage d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="09c47-127">After you have configured the steps in the previous section, the Azure Toolkit will automatically sign you into your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="09c47-128">Toutefois, pour vous déconnecter de votre compte Azure et empêcher le kit de ressources Azure de vous connecter automatiquement, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="09c47-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, use the following steps.</span></span>

1. <span data-ttu-id="09c47-129">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-129">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. <span data-ttu-id="09c47-131">Lorsque la boîte de dialogue **Déconnexion d’Azure** s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="09c47-131">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L03]

## <a name="signing-into-your-azure-account-automatically-using-a-credentials-file-which-you-have-already-created"></a><span data-ttu-id="09c47-133">Connexion automatique à votre compte Azure et utilisation d’un fichier d’informations d’identification que vous avez déjà créé</span><span class="sxs-lookup"><span data-stu-id="09c47-133">Signing into your Azure account automatically using a credentials file which you have already created</span></span>

<span data-ttu-id="09c47-134">Si vous vous déconnectez d’Azure lorsque vous utilisez Eclipse, vous devez reconfigurer le kit de ressources Azure pour Eclipse afin d’utiliser un fichier d’informations d’identification qui a été créé pour pouvoir vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="09c47-134">If you sign out of Azure when you are using Eclipse, you will need to reconfigure the Azure Toolkit for Eclipse to use a credentials file which have created before you can automatically sign into your Azure acccount.</span></span> <span data-ttu-id="09c47-135">La procédure suivante vous guide dans la configuration du kit de ressources Azure pour utiliser un fichier d’informations d’identification existant.</span><span class="sxs-lookup"><span data-stu-id="09c47-135">The following steps will walk you through configuring the Azure Toolkit to use an existing credentials file.</span></span>

1. <span data-ttu-id="09c47-136">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="09c47-136">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="09c47-137">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-137">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][A01]

1. <span data-ttu-id="09c47-139">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, sélectionnez **Automatisée**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="09c47-139">When the **Azure Sign In** dialog box appears, select **Automated**, and then click **Browse**.</span></span>

   ![Boîte de dialogue Se connecter][A02]

1. <span data-ttu-id="09c47-141">Lorsque la boîte de dialogue **Sélectionner un fichier authentifié** s’affiche, sélectionnez un fichier d’informations d’identification que vous avez créé précédemment, puis cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="09c47-141">When the **Select Authenticated File** dialog box appears, select a credentials file which you created earlier, and then click **Open**.</span></span>

   ![Boîte de dialogue Se connecter][A08]

1. <span data-ttu-id="09c47-143">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-143">When the **Azure Sign In** dialog box appears, click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="09c47-145">Lorsque la boîte de dialogue **Sélectionner des abonnements** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="09c47-145">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="signing-into-your-azure-account-interactively"></a><span data-ttu-id="09c47-147">Connexion interactive à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="09c47-147">Signing into your Azure account interactively</span></span>

<span data-ttu-id="09c47-148">La procédure suivante indique comment vous connecter à Azure en entrant manuellement vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="09c47-148">The following steps will illustrate how to sign into Azure by manually entering your Azure credentials.</span></span>

1. <span data-ttu-id="09c47-149">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="09c47-149">Open your project with Eclipse.</span></span>

1. <span data-ttu-id="09c47-150">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-150">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>

   ![Menu d’Eclipse pour la connexion à Azure][I01]

1. <span data-ttu-id="09c47-152">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, sélectionnez **Interactive**, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-152">When the **Azure Sign In** dialog box appears, select **Interactive**, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Se connecter][I02]

1. <span data-ttu-id="09c47-154">Lorsque la boîte de dialogue **Connexion à Azure** s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-154">When the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign In**.</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

1. <span data-ttu-id="09c47-156">Lorsque la boîte de dialogue **Sélectionner des abonnements** s’affiche, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="09c47-156">When the **Select Subscriptions** dialog box appears, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="signing-out-of-your-azure-account-when-you-signed-in-interactively"></a><span data-ttu-id="09c47-158">Déconnexion de votre compte Azure lorsque vous vous êtes connecté de manière interactive</span><span class="sxs-lookup"><span data-stu-id="09c47-158">Signing out of your Azure account when you signed in interactively</span></span>

<span data-ttu-id="09c47-159">Après avoir configuré les étapes indiquées dans la section précédente, vous êtes déconnecté automatiquement de votre compte Azure à chaque redémarrage d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="09c47-159">After you have configured the steps in the previous section, you will automatically signed out of your Azure account each time you restart Eclipse.</span></span> <span data-ttu-id="09c47-160">Toutefois, si vous souhaitez vous déconnecter de votre compte Azure sans redémarrer Eclipse, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="09c47-160">However, if you want to sign out of your Azure account without restarting Eclipse, use the following steps.</span></span>

1. <span data-ttu-id="09c47-161">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="09c47-161">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

1. <span data-ttu-id="09c47-163">Lorsque la boîte de dialogue **Déconnexion d’Azure** s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="09c47-163">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L02]

## <a name="next-steps"></a><span data-ttu-id="09c47-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09c47-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-eclipse-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-eclipse-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-eclipse-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-eclipse-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-eclipse-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-eclipse-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-eclipse-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-eclipse-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-eclipse-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-eclipse-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-eclipse-sign-in-instructions/L03.png
