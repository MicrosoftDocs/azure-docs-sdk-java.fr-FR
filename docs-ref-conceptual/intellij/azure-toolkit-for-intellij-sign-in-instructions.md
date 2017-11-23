---
title: Instructions de connexion pour le Kit de ressources Azure pour IntelliJ
description: "Découvrez comment vous connecter à Microsoft Azure à l’aide du Kit de ressources Azure pour IntelliJ."
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
ms.date: 11/01/2017
ms.author: robmcm
ms.openlocfilehash: 25c25e58b079c1e08d62feff389b899b26e82b5e
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-intellij"></a><span data-ttu-id="1cdce-103">Instructions de connexion pour le Kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="1cdce-103">Sign-in instructions for the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="1cdce-104">Le Kit de ressources Azure pour IntelliJ vous permet de vous connecter à votre compte Azure à l’aide de deux méthodes :</span><span class="sxs-lookup"><span data-stu-id="1cdce-104">The Azure Toolkit for IntelliJ provides two methods for signing in to your Azure account:</span></span>

  * <span data-ttu-id="1cdce-105">**Automatisée** : vous créez un fichier d’informations d’identification que vous pouvez utiliser pour vous connecter automatiquement à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdce-105">**Automated**: You create a credentials file that you can use to automatically sign in to your Azure account.</span></span>
  * <span data-ttu-id="1cdce-106">**Interactive**: vous entrez vos informations d’identification Azure chaque fois que vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="1cdce-106">**Interactive**: You enter your Azure credentials each time you sign in to your Azure account.</span></span>

<span data-ttu-id="1cdce-107">Les sections suivantes décrivent comment utiliser chaque méthode.</span><span class="sxs-lookup"><span data-stu-id="1cdce-107">The following sections describe how to use each method.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-automatically"></a><span data-ttu-id="1cdce-108">Connexion automatique à votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="1cdce-108">Sign in to your Azure account automatically</span></span>

<span data-ttu-id="1cdce-109">Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="1cdce-109">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="1cdce-110">Une fois ce processus terminé, Eclipse utilise le fichier d’informations d’identification pour vous connecter automatiquement à Azure chaque fois que vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="1cdce-110">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure each time you open your project.</span></span>

1. <span data-ttu-id="1cdce-111">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1cdce-111">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="1cdce-112">Dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-112">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Commande IntelliJ de connexion à Azure][A01]

1. <span data-ttu-id="1cdce-114">Dans la fenêtre **Connexion à Microsoft Azure**, sélectionnez **Automatisée**, puis cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-114">In the **Azure Sign In** window, select **Automated**, and then click **New**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A02]

1. <span data-ttu-id="1cdce-116">Dans la boîte de dialogue **Connexion à Azure** qui s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-116">In the **Azure Login Dialog** window, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A03]

1. <span data-ttu-id="1cdce-118">Dans la fenêtre **Créer les fichiers d’authentification**, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-118">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Fenêtre Créer les fichiers d’authentification][A04]

1. <span data-ttu-id="1cdce-120">Dans la boîte de dialogue **État de création du principal de service** qui s’affiche, une fois vos fichiers créés, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-120">In the **Service Principal Creation Status** dialog box, after your files have been created successfully, click **OK**.</span></span>

   ![Boîte de dialogue État de création du principal de service][A05]

1. <span data-ttu-id="1cdce-122">Dans la fenêtre **Connexion à Microsoft Azure**, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-122">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

1. <span data-ttu-id="1cdce-124">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-124">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-automatically"></a><span data-ttu-id="1cdce-126">Déconnexion de votre compte Azure après vous être connecté automatiquement</span><span class="sxs-lookup"><span data-stu-id="1cdce-126">Sign out of your Azure account after you have signed in automatically</span></span>

<span data-ttu-id="1cdce-127">Après que vous avez configuré votre compte en suivant la procédure précédente, le Kit de ressources Azure vous connecte automatiquement à votre compte Azure chaque fois que vous redémarrez IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1cdce-127">After you have configured your account by using the preceding steps, the Azure Toolkit automatically signs you in to your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="1cdce-128">Toutefois, pour vous déconnecter de votre compte Azure et empêcher le Kit de ressources Azure de vous connecter automatiquement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1cdce-128">However, to sign out of your Azure account and prevent the Azure Toolkit from signing you in automatically, do the following:</span></span>

1. <span data-ttu-id="1cdce-129">Dans IntelliJ IDEA, dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Déconnexion de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-129">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Commande IntelliJ de déconnexion d’Azure][L01]

1. <span data-ttu-id="1cdce-131">Dans la fenêtre de confirmation **e déconnecter de Microsoft Azure**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-131">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de déconnexion d’Azure][L03]

## <a name="sign-in-to-your-azure-account-automatically-by-using-an-existing-credentials-file"></a><span data-ttu-id="1cdce-133">Connexion automatique à votre compte Azure à l’aide d’un fichier d’informations d’identification existant</span><span class="sxs-lookup"><span data-stu-id="1cdce-133">Sign in to your Azure account automatically by using an existing credentials file</span></span>

<span data-ttu-id="1cdce-134">Si vous vous déconnectez de votre compte Azure alors que vous utilisez IntelliJ IDEA, vous devez utiliser un fichier d’informations d’identification existant pour vous reconnecter automatiquement au compte.</span><span class="sxs-lookup"><span data-stu-id="1cdce-134">If you sign out of your Azure account when you are using IntelliJ IDEA, you must use an existing credentials file to automatically sign back in to the account.</span></span> <span data-ttu-id="1cdce-135">Pour configurer le Kit de ressources Azure pour Eclipse afin d’utiliser un fichier d’informations d’identification existant, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1cdce-135">To configure the Azure Toolkit for Eclipse to use an existing credentials file, do the following:</span></span>

1. <span data-ttu-id="1cdce-136">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1cdce-136">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="1cdce-137">Dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-137">On the **Tools** menu, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Commande IntelliJ de connexion à Azure][A01]

1. <span data-ttu-id="1cdce-139">Dans la fenêtre **Connexion à Microsoft Azure**, sélectionnez **Automatisée**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-139">In the **Azure Sign In** window, select **Automated**, and then click **Browse**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A02]

1. <span data-ttu-id="1cdce-141">Dans la boîte de dialogue **Sélectionner le fichier d’authentification**, choisissez un fichier d’informations d’identification créé précédemment, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-141">In the **Select Authentication File** dialog box, select a previously created credentials file, and then click **Select**.</span></span>

   ![Boîte de dialogue Sélectionner le fichier d’authentification][A08]

1. <span data-ttu-id="1cdce-143">Dans la fenêtre **Connexion à Microsoft Azure**, cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-143">In the **Azure Sign In** window, click **Sign in**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Automatique activée][A06]

1. <span data-ttu-id="1cdce-145">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-145">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="sign-in-to-your-azure-account-interactively"></a><span data-ttu-id="1cdce-147">Connexion à votre compte Azure de façon interactive</span><span class="sxs-lookup"><span data-stu-id="1cdce-147">Sign in to your Azure account interactively</span></span>

<span data-ttu-id="1cdce-148">Pour vous connecter à Azure en entrant manuellement vos informations d’identification, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1cdce-148">To sign in to Azure by manually entering your Azure credentials, do the following:</span></span>

1. <span data-ttu-id="1cdce-149">Ouvrez votre projet avec IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1cdce-149">Open your project with IntelliJ IDEA.</span></span>

1. <span data-ttu-id="1cdce-150">Cliquez sur **Outils**, pointez sur **Azure**, puis cliquez sur **Connexion à Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-150">Click **Tools**, point to **Azure**, and then click **Azure Sign In**.</span></span>

   ![Commande IntelliJ de connexion à Azure][I01]

1. <span data-ttu-id="1cdce-152">Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Interactive**, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-152">In the **Azure Sign In** window, select **Interactive**, and then click **Sign in**.</span></span>

   ![Fenêtre Connexion à Azure avec l’option Interactive activée][I02]

1. <span data-ttu-id="1cdce-154">Dans la boîte de dialogue **Connexion à Azure** qui s’affiche, entrez vos informations d’identification Azure, puis cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-154">In the **Azure Log In** dialog box appears, enter your Azure credentials, and then click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

1. <span data-ttu-id="1cdce-156">Lorsque la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-156">In the **Select Subscriptions** dialog box, select the subscriptions that you want to use, and then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I04]

## <a name="sign-out-of-your-azure-account-after-you-have-signed-in-interactively"></a><span data-ttu-id="1cdce-158">Déconnexion de votre compte Azure après vous être connecté de manière interactive</span><span class="sxs-lookup"><span data-stu-id="1cdce-158">Sign out of your Azure account after you have signed in interactively</span></span>

<span data-ttu-id="1cdce-159">Après que vous avez configuré votre compte en procédant de la manière décrite les étapes précédentes, vous êtes automatiquement déconnecté de votre compte Azure à chaque redémarrage d’IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="1cdce-159">After you have configured your account by using the preceding steps, you will be automatically signed out of your Azure account each time you restart IntelliJ IDEA.</span></span> <span data-ttu-id="1cdce-160">En revanche, si vous souhaitez vous déconnecter de votre compte Azure *sans* redémarrer IntelliJ IDEA, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="1cdce-160">However, if you want to sign out of your Azure account *without* restarting IntelliJ IDEA, do the following.</span></span>

1. <span data-ttu-id="1cdce-161">Dans IntelliJ IDEA, dans le menu **Outils**, pointez sur **Azure**, puis cliquez sur **Déconnexion de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-161">In IntelliJ IDEA, on the **Tools** menu, point to **Azure**, and then click **Azure Sign Out**.</span></span>

   ![Commande IntelliJ de déconnexion d’Azure][L01]

1. <span data-ttu-id="1cdce-163">Dans la fenêtre de confirmation **e déconnecter de Microsoft Azure**, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="1cdce-163">In the **Azure Sign Out** confirmation window, click **Yes**.</span></span>

   ![Fenêtre de confirmation de déconnexion d’Azure][L02]

## <a name="next-steps"></a><span data-ttu-id="1cdce-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1cdce-165">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

<!-- IMG List -->

[I01]: media/azure-toolkit-for-intellij-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-intellij-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-intellij-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-intellij-sign-in-instructions/I04.png

[A01]: media/azure-toolkit-for-intellij-sign-in-instructions/A01.png
[A02]: media/azure-toolkit-for-intellij-sign-in-instructions/A02.png
[A03]: media/azure-toolkit-for-intellij-sign-in-instructions/A03.png
[A04]: media/azure-toolkit-for-intellij-sign-in-instructions/A04.png
[A05]: media/azure-toolkit-for-intellij-sign-in-instructions/A05.png
[A06]: media/azure-toolkit-for-intellij-sign-in-instructions/A06.png
[A07]: media/azure-toolkit-for-intellij-sign-in-instructions/A07.png
[A08]: media/azure-toolkit-for-intellij-sign-in-instructions/A08.png

[L01]: media/azure-toolkit-for-intellij-sign-in-instructions/L01.png
[L02]: media/azure-toolkit-for-intellij-sign-in-instructions/L02.png
[L03]: media/azure-toolkit-for-intellij-sign-in-instructions/L03.png
