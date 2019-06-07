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
# <a name="sign-in-instructions-for-the-azure-toolkit-for-eclipse"></a>Instructions de connexion pour le kit de ressources Azure pour Eclipse

Le kit de ressources Azure pour Eclipse propose deux méthodes pour vous connecter à votre compte Azure :

  - [Connexion à votre compte Azure par Connexion à l’appareil](#sign-in-to-your-azure-account-by-device-login)
  - [Connexion à votre compte Azure par Principal du service](#sign-in-to-your-azure-account-by-service-principal)

Des méthodes de [**déconnexion**](#sign-out-of-your-azure-account) sont également fournies.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="sign-in-to-your-azure-account-by-device-login"></a>Connexion à votre compte Azure par Connexion à l’appareil

Pour vous connecter dans Azure par Connexion à l’appareil, effectuez les étapes suivantes :

1. Ouvrez votre projet avec Eclipse.

2. Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.
   ![Menu d’Eclipse pour la connexion à Azure][I01]

3. Dans la fenêtre **Connexion à Azure** qui s’affiche, sélectionnez **Connexion à l’appareil**, puis cliquez sur **Connexion**.

   ![Fenêtre Connexion à Microsoft Azure avec l’option Connexion à l’appareil activée][I02]

4. Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.

   ![Boîte de dialogue Connexion à Azure][I03]

> [!NOTE]
>
> Si le navigateur ne s’ouvre pas, configurez Eclipse pour utiliser un navigateur externe comme Internet Explorer, Firefox ou Chrome :
>
> 1. Ouvrez Preferences -> General -> Web Browser -> Use external web browser in Eclipse.
>
> 2. Sélectionnez le navigateur que vous préférez utiliser.
>

5. Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.

   ![Navigateur de connexion à l’appareil][I04]

6. Pour finir, dans la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][I05]

## <a name="sign-in-to-your-azure-account-by-service-principal"></a>Connexion à votre compte Azure par Principal du service

Cette section vous guide dans la création d’un fichier d’informations d’identification contenant les données de votre principal de service. Une fois ce processus terminé, Eclipse utilise le fichier d’informations d’identification pour vous connecter automatiquement à Azure quand vous ouvrez votre projet.

1. Ouvrez votre projet avec Eclipse.

2. Cliquez successivement sur **Outils**, **Azure** et **Se connecter**.
   ![Commande Connexion à Azure dans Eclipse][A01]

3. Dans la fenêtre **Connexion à Azure**, sélectionnez **Principal du service**. Si vous n’avez pas encore le fichier d’authentification de principal du service, cliquez sur **Nouveau** pour en créer un. Autrement, vous pouvez cliquer sur **Parcourir** pour l’ouvrir et passer à l’étape 8.

   ![La fenêtre Connexion à Azure avec principal du service sélectionné][A02]

4. Cliquez sur **Copier et ouvrir** dans la boîte de dialogue **Connexion à l’appareil Azure**.

   ![Boîte de dialogue Connexion à Azure][A08]

> [!NOTE]
>
> Si le navigateur ne s’ouvre pas, configurez Eclipse pour utiliser un navigateur externe comme Internet Explorer ou Chrome :
>
> 1. Ouvrez Preferences -> General -> Web Browser -> Use external web browser in Eclipse.
>
> 2. Sélectionnez le navigateur que vous préférez utiliser.
>

5. Dans le navigateur, collez le code de votre appareil (qui a été copié quand vous avez cliqué sur **Copier et ouvrir** à la dernière étape), puis cliquez sur **Suivant**.

   ![Navigateur de connexion à l’appareil][A03]

6. Dans la fenêtre **Créer les fichiers d’authentification**, sélectionnez les abonnements que vous souhaitez utiliser, choisissez votre répertoire de destination, puis cliquez sur **Démarrer**.

   ![Fenêtre Créer les fichiers d’authentification][A04]

7. Dans la boîte de dialogue **État de création du principal de service**, cliquez sur **OK** une fois vos fichiers créés.

   ![Boîte de dialogue État de création du principal de service][A05]

8. L’adresse du fichier créé est renseignée automatiquement dans la fenêtre **Connexion à Azure**. Maintenant, cliquez sur **Connexion**.

   ![Boîte de dialogue Connexion à Azure][A06]

9. Pour finir, dans la boîte de dialogue **Sélectionner des abonnements**, sélectionnez les abonnements que vous souhaitez utiliser, puis cliquez sur **OK**.

   ![Boîte de dialogue Sélectionner des abonnements][A07]

## <a name="sign-out-of-your-azure-account"></a>Déconnectez-vous de votre compte Azure

Après avoir configuré votre compte à l’aide des étapes précédentes, vous serez connecté automatiquement chaque fois que vous démarrerez Eclipse. Toutefois, si vous souhaitez vous déconnecter de votre compte Azure, effectuez les étapes suivantes.

1. Dans Eclipse, cliquez successivement sur **Outils**, **Azure** et **Se déconnecter**.

   ![Menu d’Eclipse pour la déconnexion d’Azure][L01]

2. Lorsque la boîte de dialogue **Déconnexion d’Azure** s’affiche, cliquez sur **Oui**.

   ![Boîte de dialogue Se déconnecter][L02]

## <a name="next-steps"></a>Étapes suivantes

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
