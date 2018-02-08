---
title: "Affichage du contenu Javadoc dans Eclipse pour le package de bibliothèques Azure pour Java"
description: "Comment afficher le contenu Javadoc pour les bibliothèques Azure dans Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 6f1edcc1411e8ec716dbfe41271d21d2397515c5
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="1a3c6-103">Affichage du contenu Javadoc dans Eclipse pour le package de bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="1a3c6-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>

<span data-ttu-id="1a3c6-104">Vous pouvez afficher le contenu Javadoc pour les bibliothèques Azure pour Java dans votre environnement Eclipse en associant ce contenu aux bibliothèques Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="1a3c6-105">Les étapes suivantes montrent comment utiliser cette fonctionnalité dans Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="1a3c6-106">Cette procédure part du principe que vous avez déjà ajouté la bibliothèque Azure pour Java à votre chemin de build.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="1a3c6-107">Pour afficher le contenu Javadoc dans Eclipse pour les bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="1a3c6-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>

1. <span data-ttu-id="1a3c6-108">Dans l’Explorateur de projets d’Eclipse, dans la section **Bibliothèques référencées** de votre projet, ouvrez le menu contextuel de la bibliothèque Azure pour Java JAR.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="1a3c6-109">Par exemple, **microsoft-Microsoft Azure-api-0.1.0.jar** (le numéro de version peut différer en fonction de la version que vous avez installée).</span><span class="sxs-lookup"><span data-stu-id="1a3c6-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

1. <span data-ttu-id="1a3c6-110">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-110">Click **Properties**.</span></span>

1. <span data-ttu-id="1a3c6-111">Dans la boîte de dialogue **Propriétés**, dans le volet gauche, cliquez sur **Emplacement Javadoc**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="1a3c6-112">La boîte de dialogue **Emplacement Javadoc** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-112">The **Javadoc Location** dialog is displayed.</span></span>

1. <span data-ttu-id="1a3c6-113">Vous pouvez spécifier une **URL Javadoc** ou un **Javadoc dans archive**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="1a3c6-114">Si vous choisissez de spécifier une **URL Javadoc**, utilisez une URL du type **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="1a3c6-115">Si vous choisissez d’utiliser **Javadoc dans archive**, vous pouvez spécifier un fichier externe ou un fichier d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="1a3c6-116">Faites votre choix et parcourez/validez en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="1a3c6-117">L’exemple suivant associe les bibliothèques Azure pour Java au JAR Javadoc correspondant téléchargé localement dans un dossier nommé **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![Affichez le contenu du fichier Javadoc.][ic553487]

1. <span data-ttu-id="1a3c6-119">*Étape facultative* : cliquez sur **Valider**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-119">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="1a3c6-120">Des problèmes potentiels avec le JAR Javadoc peuvent apparaître ici.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-120">Potential issues with the Javadoc JAR could be displayed here.</span></span>

1. <span data-ttu-id="1a3c6-121">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-121">Click **OK**.</span></span>

<span data-ttu-id="1a3c6-122">Une fois associé à la bibliothèque, le contenu Javadoc doit s’afficher dans votre IDE Eclipse.</span><span class="sxs-lookup"><span data-stu-id="1a3c6-122">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="1a3c6-123">Par exemple, si `blob` est défini comme étant de type `CloudBlockBlob` dans votre code, ce qui suit est un exemple de contenu Javadoc qui apparaît lorsque vous tapez `blob.acquireLease` dans le code :</span><span class="sxs-lookup"><span data-stu-id="1a3c6-123">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![Affichez le contenu du fichier Javadoc.][ic553488]

## <a name="next-steps"></a><span data-ttu-id="1a3c6-125">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a3c6-125">Next steps</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-additional-resources](../includes/azure-toolkit-for-eclipse-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

<!-- IMG List -->

[ic553487]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png
