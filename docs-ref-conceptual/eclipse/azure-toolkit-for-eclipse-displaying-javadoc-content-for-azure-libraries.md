---
title: "Affichage du contenu Javadoc dans Eclipse pour le package de bibliothèques Azure pour Java"
description: "Comment afficher le contenu Javadoc pour les bibliothèques Azure dans Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 2d1f03f993f0c88401efaa9985f773b9a4b92cc4
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a>Affichage du contenu Javadoc dans Eclipse pour le package de bibliothèques Azure pour Java

Vous pouvez afficher le contenu Javadoc pour les bibliothèques Azure pour Java dans votre environnement Eclipse en associant ce contenu aux bibliothèques Azure pour Java. Les étapes suivantes montrent comment utiliser cette fonctionnalité dans Eclipse.

Cette procédure part du principe que vous avez déjà ajouté la bibliothèque Azure pour Java à votre chemin de build.

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a>Pour afficher le contenu Javadoc dans Eclipse pour les bibliothèques Azure pour Java

1. Dans l’Explorateur de projets d’Eclipse, dans la section **Bibliothèques référencées** de votre projet, ouvrez le menu contextuel de la bibliothèque Azure pour Java JAR. Par exemple, **microsoft-Microsoft Azure-api-0.1.0.jar** (le numéro de version peut différer en fonction de la version que vous avez installée).

1. Cliquez sur **Propriétés**.

1. Dans la boîte de dialogue **Propriétés**, dans le volet gauche, cliquez sur **Emplacement Javadoc**. La boîte de dialogue **Emplacement Javadoc** s’affiche.

1. Vous pouvez spécifier une **URL Javadoc** ou un **Javadoc dans archive**.

   * Si vous choisissez de spécifier une **URL Javadoc**, utilisez une URL du type **http://dl.windowsazure.com/javadoc** ou **http://dl.windowsazure.com/storage/javadoc**.

   * Si vous choisissez d’utiliser **Javadoc dans archive**, vous pouvez spécifier un fichier externe ou un fichier d’espace de travail.

   Faites votre choix et parcourez/validez en fonction des besoins. L’exemple suivant associe les bibliothèques Azure pour Java au JAR Javadoc correspondant téléchargé localement dans un dossier nommé **c:\MyAzureJARs**.

   ![Affichez le contenu du fichier Javadoc.][ic553487]

1. *Étape facultative* : cliquez sur **Valider**. Des problèmes potentiels avec le JAR Javadoc peuvent apparaître ici.

1. Cliquez sur **OK**.

Une fois associé à la bibliothèque, le contenu Javadoc doit s’afficher dans votre IDE Eclipse. Par exemple, si `blob` est défini comme étant de type `CloudBlockBlob` dans votre code, ce qui suit est un exemple de contenu Javadoc qui apparaît lorsque vous tapez `blob.acquireLease` dans le code :

![Affichez le contenu du fichier Javadoc.][ic553488]

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->

<!-- IMG List -->

[ic553487]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png
