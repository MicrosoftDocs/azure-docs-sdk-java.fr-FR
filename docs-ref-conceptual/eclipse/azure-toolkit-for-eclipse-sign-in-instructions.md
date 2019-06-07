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
ms.openlocfilehash: b4b13de38913ae6e7ae2bb09210ac742efc9d0ad
ms.sourcegitcommit: d18d9dce22b7f7af178f756bd341433d24e3c3b5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66575318"
---
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="d675b-103">Instructions de connexion pour le kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="d675b-103">Sign-in instructions for the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="d675b-104">Le kit de ressources Azure pour Eclipse propose deux méthodes pour vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="d675b-104">The Azure Toolkit for Eclipse provides two methods for signing into your Azure account:</span></span>

  - [<span data-ttu-id="d675b-105">Connexion à votre compte Azure par Connexion à l’appareil</span><span class="sxs-lookup"><span data-stu-id="d675b-105">Sign in to your Azure account by Device Login</span></span>](#sign-in-to-your-azure-account-by-device-login)
  - [<span data-ttu-id="d675b-106">Connexion à votre compte Azure par Principal du service</span><span class="sxs-lookup"><span data-stu-id="d675b-106">Sign in to your Azure account by Service Principal</span></span>](#sign-in-to-your-azure-account-by-service-principal)

<span data-ttu-id="d675b-107">Des méthodes de [**déconnexion**](#sign-out-of-your-azure-account) sont également fournies.</span><span class="sxs-lookup"><span data-stu-id="d675b-107">[**Sign out**](#sign-out-of-your-azure-account) methods are also provided.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a><span data-ttu-id="d675b-108">Connexion à votre compte Azure par Connexion à l’appareil</span><span class="sxs-lookup"><span data-stu-id="d675b-108">Sign in to your Azure account by Device Login</span></span>

<span data-ttu-id="d675b-109">Pour vous connecter dans Azure par Connexion à l’appareil, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d675b-109">To sign in Azure by device login, do the following:</span></span>

1. <span data-ttu-id="d675b-110">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d675b-110">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="d675b-111">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="d675b-111">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="d675b-112">![Menu d’Eclipse pour la connexion à Azure][I01]</span><span class="sxs-lookup"><span data-stu-id="d675b-112">![Eclipse Menu for Azure Sign In][I01]</span></span>

3. <span data-ttu-id="d675b-113">Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Connexion à l’appareil**, puis cliquez sur **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="d675b-113">In the **Azure Sign In** window, select **Device Login**, and then click **Sign in**.</span></span>

   ![Fenêtre Connexion à Microsoft Azure avec l’option Connexion à l’appareil activée][I02]

4. <span data-ttu-id="d675b-115">Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.</span><span class="sxs-lookup"><span data-stu-id="d675b-115">Click **Copy&Open** in **Azure Device Login** dialog .</span></span>

   ![Boîte de dialogue Connexion à Azure][I03]

> [!NOTE]
>
> <span data-ttu-id="d675b-117">Si le navigateur ne s’ouvre pas, configurez Eclipse pour utiliser un navigateur externe comme Internet Explorer, Firefox ou Chrome :</span><span class="sxs-lookup"><span data-stu-id="d675b-117">If the browser doesn't open, configure Eclipse to use an external browser like Internet Explorer, Firefox, or Chrome:</span></span>
>
> 1. <span data-ttu-id="d675b-118">Ouvrez Preferences -> General -> Web Browser -> Use external web browser in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d675b-118">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="d675b-119">Sélectionnez le navigateur que vous préférez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d675b-119">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="d675b-120">Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d675b-120">In the browser, paste your device code (which has been copied when you clicked **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Navigateur de connexion à l’appareil][I04]

6. <span data-ttu-id="d675b-122">Pour finir, dans la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d675b-122">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a><span data-ttu-id="d675b-124">Connexion à votre compte Azure par Principal du service</span><span class="sxs-lookup"><span data-stu-id="d675b-124">Sign in to your Azure account by Service Principal</span></span>

<span data-ttu-id="d675b-125">Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="d675b-125">This section walks you through creating a credentials file that contains your service principal data.</span></span> <span data-ttu-id="d675b-126">Une fois ce processus terminé, Eclipse utilise le fichier d’informations d’identification pour vous connecter automatiquement à Azure quand vous ouvrez votre projet.</span><span class="sxs-lookup"><span data-stu-id="d675b-126">After you have completed this process, Eclipse uses the credentials file to automatically sign you in to Azure when open your project.</span></span>

1. <span data-ttu-id="d675b-127">Ouvrez votre projet avec Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d675b-127">Open your project with Eclipse.</span></span>

2. <span data-ttu-id="d675b-128">Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="d675b-128">Click **Tools**, then click **Azure**, and then click **Sign In**.</span></span>
   <span data-ttu-id="d675b-129">![Commande Connexion à Azure dans Eclipse][A01]</span><span class="sxs-lookup"><span data-stu-id="d675b-129">![The Eclipse Azure Sign In command][A01]</span></span>

3. <span data-ttu-id="d675b-130">Dans la fenêtre **Connexion à Azure**, sélectionnez **Principal du service**.</span><span class="sxs-lookup"><span data-stu-id="d675b-130">In the **Azure Sign In** window, select **Service Principal**.</span></span> <span data-ttu-id="d675b-131">Si vous n’avez pas encore le fichier d’authentification de principal du service, cliquez sur **Nouveau** pour en créer un.</span><span class="sxs-lookup"><span data-stu-id="d675b-131">If you do not have the service principal authentication file yet, click **New** to create one.</span></span> <span data-ttu-id="d675b-132">Autrement, vous pouvez cliquer sur **Parcourir** pour l’ouvrir et passer à l’étape 8.</span><span class="sxs-lookup"><span data-stu-id="d675b-132">Otherwise you can click **Browse** to open it and jump to step 8.</span></span>

   ![La fenêtre Connexion à Azure avec principal du service sélectionné][A02]

4. <span data-ttu-id="d675b-134">Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.</span><span class="sxs-lookup"><span data-stu-id="d675b-134">Click **Copy&Open** in **Azure Device Login** dialog.</span></span>

   ![Boîte de dialogue Connexion à Azure][A08]

> [!NOTE]
>
> <span data-ttu-id="d675b-136">Si le navigateur ne s’ouvre pas, configurez Eclipse pour utiliser un navigateur externe comme Internet Explorer ou Chrome :</span><span class="sxs-lookup"><span data-stu-id="d675b-136">If the browser doesn't open, configure eclipse to use an external browser like IE or Chrome:</span></span>
>
> 1. <span data-ttu-id="d675b-137">Ouvrez Preferences -> General -> Web Browser -> Use external web browser in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d675b-137">Open Preferences -> General -> Web Browser -> Use external web browser in Eclipse</span></span>
>
> 2. <span data-ttu-id="d675b-138">Sélectionnez le navigateur que vous préférez utiliser.</span><span class="sxs-lookup"><span data-stu-id="d675b-138">Select the browser you prefer to use</span></span>
>

5. <span data-ttu-id="d675b-139">Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d675b-139">In the browser, paste your device code (which has been copied when you click **Copy&Open** in last step) and then click **Next**.</span></span>

   ![Navigateur de connexion à l’appareil][A03]

6. <span data-ttu-id="d675b-141">Dans la fenêtre **Créer les fichiers d’authentification**, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="d675b-141">In the **Create Authentication Files** window, select the subscriptions that you want to use, choose your destination directory, and then click **Start**.</span></span>

   ![Fenêtre Créer les fichiers d’authentification][A04]

7. <span data-ttu-id="d675b-143">Dans la boîte de dialogue **État de création du principal de service**, cliquez sur **OK** une fois vos fichiers créés.</span><span class="sxs-lookup"><span data-stu-id="d675b-143">In the **Service Principal Creation Status** dialog box, click **OK** after your files have been created successfully.</span></span>

   ![Boîte de dialogue État de création du principal de service][A05]

8. <span data-ttu-id="d675b-145">L’adresse du fichier créé est renseignée automatiquement dans la fenêtre **Connexion à Azure**. Maintenant, cliquez sur **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="d675b-145">Address of the created file will be automatically filled in the **Azure Sign In** window, now click **Sign in**.</span></span>

   ![Boîte de dialogue Connexion à Azure][A06]

9. <span data-ttu-id="d675b-147">Pour finir, dans la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d675b-147">Finally, in the **Select Subscriptions** dialog box, select the subscriptions that you want to use, then click **OK**.</span></span>

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="sign-out-of-your-azure-account"></a><span data-ttu-id="d675b-149">Déconnectez-vous de votre compte Azure</span><span class="sxs-lookup"><span data-stu-id="d675b-149">Sign out of your Azure account</span></span>

<span data-ttu-id="d675b-150">Après avoir configuré votre compte à l’aide des étapes précédentes, vous serez connecté automatiquement chaque fois que vous démarrerez Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d675b-150">After you have configured your account by preceding steps, you will be automatically signed in each time you start Eclipse.</span></span> <span data-ttu-id="d675b-151">Toutefois, si vous souhaitez vous déconnecter de votre compte Azure, effectuez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d675b-151">However, if you want to sign out of your Azure account, use the following steps.</span></span>

1. <span data-ttu-id="d675b-152">Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="d675b-152">In Eclipse, click **Tools**, then click **Azure**, and then click **Sign Out**.</span></span>

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

2. <span data-ttu-id="d675b-154">Lorsque la boîte de dialogue **Déconnexion d’Azure** s’affiche, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="d675b-154">When the **Azure Sign Out** dialog box appears, click **Yes**.</span></span>

   ![Boîte de dialogue Se déconnecter][L02]

## <a name="next-steps"></a><span data-ttu-id="d675b-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d675b-156">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->


<!-- IMG List -->

[I01]: media/azure-toolkit-for-eclipse-sign-in-instructions/I01.png
[I02]: media/azure-toolkit-for-eclipse-sign-in-instructions/I02.png
[I03]: media/azure-toolkit-for-eclipse-sign-in-instructions/I03.png
[I04]: media/azure-toolkit-for-eclipse-sign-in-instructions/I04.png
[I05]: media/azure-toolkit-for-eclipse-sign-in-instructions/I05.png

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
