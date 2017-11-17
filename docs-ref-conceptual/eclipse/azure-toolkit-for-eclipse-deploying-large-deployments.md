---
title: "Réalisation de déploiements volumineux"
description: "Découvrez comment déployer des déploiements volumineux à l’aide de la Boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm
ms.openlocfilehash: 0e367e74d038043f1626dbf19aab87db6451bc02
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="a7d75-103">Réalisation de déploiements volumineux</span><span class="sxs-lookup"><span data-stu-id="a7d75-103">Deploying Large Deployments</span></span>

<span data-ttu-id="a7d75-104">Si votre déploiement est trop volumineux pour être contenu dans le dossier approot par défaut, vous pouvez utiliser une ressource de stockage local comme dossier racine de déploiement pour votre JDK et serveur d’applications.</span><span class="sxs-lookup"><span data-stu-id="a7d75-104">If your deployment is too large to be contained in the default approot folder, you can use a local storage resource as the deployment root folder for your JDK and application server.</span></span>

## <a name="to-use-a-local-storage-resource-as-the-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="a7d75-105">Pour utiliser une ressource de stockage local comme dossier racine de déploiement pour les déploiements à grande échelle</span><span class="sxs-lookup"><span data-stu-id="a7d75-105">To use a local storage resource as the deployment root folder for large deployments</span></span>

1. <span data-ttu-id="a7d75-106">Créez une ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="a7d75-106">Create a new local storage resource.</span></span> <span data-ttu-id="a7d75-107">Le nom de la ressource n’a pas d’importance.</span><span class="sxs-lookup"><span data-stu-id="a7d75-107">The name of the resource does not matter.</span></span> <span data-ttu-id="a7d75-108">Les ressources de stockage sont définies au niveau du rôle.</span><span class="sxs-lookup"><span data-stu-id="a7d75-108">Storage resources are defined at the role level.</span></span> <span data-ttu-id="a7d75-109">Pour accéder à la boîte de dialogue de configuration du stockage local, à partir de laquelle vous pouvez créer une ressource de stockage local, le plus rapide est de procéder comme suit : cliquez avec le bouton droit sur le rôle dans la vue **Explorateur de projets** (développez le nœud de votre projet Azure si le rôle n’est pas visible), cliquez sur **Azure**, puis sur **Stockage Local**.</span><span class="sxs-lookup"><span data-stu-id="a7d75-109">The quickest way to access the local storage configuration dialog, from which you could create a new local storage resource, is by using the following steps: Right-click the role in the **Project Explorer** view (expand your Azure project node if you don't see the role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="a7d75-110">Dans la boîte de dialogue **Stockage Local**, cliquez sur **Ajouter** pour créer une ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="a7d75-110">Within the **Local Storage** dialog, click **Add** to create a new local storage resource.</span></span>

1. <span data-ttu-id="a7d75-111">Définissez une taille d’au moins 2 048 Mo (une valeur inférieure peut provoquer les mêmes problèmes de taille de fichier que ceux que vous rencontreriez dans approot).</span><span class="sxs-lookup"><span data-stu-id="a7d75-111">Set the desired size to at least 2048 MB (anything less may cause the same file size problems as you would encounter in the approot).</span></span>

1. <span data-ttu-id="a7d75-112">Vérifiez que l’option **Nettoyer le contenu lorsque l’instance de rôle est recyclée** est activée. Elle empêchera la logique de démarrage du déploiement d’entrer en conflit avec les fichiers existants dans la ressource lors du recyclage de l’instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="a7d75-112">Ensure that **Clean the contents when the role instance is recycled** is checked; this will help prevent the deployment's startup logic from running into conflicts with pre-existing files in the resource when the role instance is recycled.</span></span>

1. <span data-ttu-id="a7d75-113">Assurez-vous que **Variable d’environnement stockant le chemin d’accès au répertoire de la ressource après le déploiement** a la valeur **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="a7d75-113">Ensure that the **Environment variable storing the resource's directory path after deployment** value is set to the string **DEPLOYROOT**.</span></span> <span data-ttu-id="a7d75-114">La boîte de dialogue de ressource de stockage local doit avoir l’aspect suivant.</span><span class="sxs-lookup"><span data-stu-id="a7d75-114">Your local storage resource dialog will look similar to the following.</span></span>

   ![][ic667943]

<span data-ttu-id="a7d75-115">En guise d’alternative, si vous utilisez **DEPLOYROOT** comme *nom* de votre ressource locale et que vous ne modifiez pas le nom de variable d’environnement généré automatiquement (à savoir, ici, **DEPLOYROOT_PATH**), cela fonctionnera également pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a7d75-115">Alternatively, if you use **DEPLOYROOT** as the *name* of your local resource and you do not change the automatically-generated environment variable name (which will be set to **DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="a7d75-116">Vous trouverez des informations supplémentaires sur la création d’une ressource de stockage local dans [Propriétés de stockage local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="a7d75-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7d75-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7d75-117">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
