---
title: Installer Azul Zulu JDK pour Azure et Azure Stack
description: Découvrez comment installer les kits Azul Zulu Java Development Kits (JDK) pour le développement Azure avec Windows, Linux et Mac.
author: erickson-doug
manager: douge
ms.author: douge
ms.date: 4/19/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 33d2206f9a0a1cc9fadc60b17c1a93f66c592fe3
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568592"
---
# <a name="install-the-jdk-for-azure-and-azure-stack"></a><span data-ttu-id="65d90-103">Installer le JDK pour Azure et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="65d90-103">Install the JDK for Azure and Azure Stack</span></span>

<span data-ttu-id="65d90-104">Les builds Azul Zulu Enterprise d’OpenJDK sont une distribution gratuite, multiplateforme et prête pour la production d’OpenJDK pour Azure et Azure Stack pris en charge par Microsoft et Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="65d90-104">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="65d90-105">Elles contiennent tous les composants nécessaires pour générer et exécuter des applications Java SE.</span><span class="sxs-lookup"><span data-stu-id="65d90-105">They contain all the components for building and running Java SE applications.</span></span>

<span data-ttu-id="65d90-106">Il existe [plusieurs types de packages de téléchargement pris en charge pour chaque système d’exploitation client](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="65d90-106">There are [multiple download package types supported for each client OS](https://www.azul.com/downloads/azure-only/zulu/).</span></span> <span data-ttu-id="65d90-107">Vous pouvez également obtenir une image de machine virtuelle à partir de la galerie de la Place de marché Azure pour les plateformes suivantes :</span><span class="sxs-lookup"><span data-stu-id="65d90-107">You can also get a virtual machine image from the Azure Marketplace Gallery for the following platforms:</span></span>

  * [<span data-ttu-id="65d90-108">Azul Zulu : Java 8 sur Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="65d90-108">Azul Zulu: Java 8 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [<span data-ttu-id="65d90-109">Azul Zulu : Java 8 sur Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="65d90-109">Azul Zulu: Java 8 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [<span data-ttu-id="65d90-110">Azul Zulu : Java 11 sur Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="65d90-110">Azul Zulu: Java 11 on Ubuntu 18.04</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [<span data-ttu-id="65d90-111">Azul Zulu : Java 11 sur Windows Server 2019</span><span class="sxs-lookup"><span data-stu-id="65d90-111">Azul Zulu: Java 11 on Windows Server 2019</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> <span data-ttu-id="65d90-112">Ces instructions ciblent la version Java 8 64 bits du JDK.</span><span class="sxs-lookup"><span data-stu-id="65d90-112">These instructions target the 64-bit Java 8 version of the JDK.</span></span> <span data-ttu-id="65d90-113">Azul fournit également l’environnement JRE (Java Run-time Environment) en tant qu’installation autonome.</span><span class="sxs-lookup"><span data-stu-id="65d90-113">Azul also provides the Java Run-time Environment (JRE) as a stand-alone installation.</span></span> <span data-ttu-id="65d90-114">L’environnement JRE est inclus avec l’installation du JDK.</span><span class="sxs-lookup"><span data-stu-id="65d90-114">The JRE is included with the JDK install.</span></span>
>
>  <span data-ttu-id="65d90-115">Les packages Java 11 sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).</span><span class="sxs-lookup"><span data-stu-id="65d90-115">Java 11 packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a><span data-ttu-id="65d90-116">Télécharger et installer les JDK Azul Zulu pour Windows</span><span class="sxs-lookup"><span data-stu-id="65d90-116">Download and install the Azul Zulu JDKs for Windows</span></span> 

1. <span data-ttu-id="65d90-117">[Téléchargez le JDK 8 Azul Zulu 64 bits en tant que fichier MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) sur un emplacement de votre client, tel que `C:\Users\<your_login>\Downloads`.</span><span class="sxs-lookup"><span data-stu-id="65d90-117">[Download the 64-bit Azul Zulu JDK 8 as an MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) to a location on your client, such as `C:\Users\<your_login>\Downloads`.</span></span> <span data-ttu-id="65d90-118">(Des packages .ZIP sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="65d90-118">(.ZIP packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="65d90-119">Accédez au répertoire et double-cliquez sur le fichier MSI téléchargé pour commencer l’installation.</span><span class="sxs-lookup"><span data-stu-id="65d90-119">Navigate to the directory and double-click the downloaded MSI file to begin installation.</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a><span data-ttu-id="65d90-120">Télécharger et installer les JDK Azul Zulu pour Mac</span><span class="sxs-lookup"><span data-stu-id="65d90-120">Download and install the Azul Zulu JDKs for Mac</span></span> 

<span data-ttu-id="65d90-121">Ces étapes permettent de télécharger un fichier ZIP sur votre Mac.</span><span class="sxs-lookup"><span data-stu-id="65d90-121">These steps download a ZIP file to your Mac.</span></span> <span data-ttu-id="65d90-122">Une version DMG est également disponible.</span><span class="sxs-lookup"><span data-stu-id="65d90-122">There is also a DMG version available.</span></span>

1. <span data-ttu-id="65d90-123">[Téléchargez le JDK 8 Azul Zulu 64 bits en tant que fichier ZIP](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) vers un emplacement sur votre client, tel que `/Library/Java/JavaVirtualMachines/`.</span><span class="sxs-lookup"><span data-stu-id="65d90-123">[Download the 64-bit Azul Zulu JDK 8 as a ZIP file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) to a location on your client, such as `/Library/Java/JavaVirtualMachines/`.</span></span> <span data-ttu-id="65d90-124">(Des packages .DMG sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="65d90-124">(.DMG packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="65d90-125">Lancez Finder, accédez au répertoire de téléchargement, puis double-cliquez sur le fichier ZIP.</span><span class="sxs-lookup"><span data-stu-id="65d90-125">Launch Finder, navigate to the download directory, and double-click the ZIP file.</span></span> <span data-ttu-id="65d90-126">Vous pouvez aussi lancer une fenêtre de terminal de commande, accéder au répertoire et exécuter :</span><span class="sxs-lookup"><span data-stu-id="65d90-126">Alternatively, you can launch a terminal command window, navigate to the directory, and run:</span></span>

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a><span data-ttu-id="65d90-127">Télécharger et installer les JDK Azul Zulu pour Alpine Linux</span><span class="sxs-lookup"><span data-stu-id="65d90-127">Download and install the Azul Zulu JDKs for Alpine Linux</span></span>

1. <span data-ttu-id="65d90-128">[Téléchargez le JDK 8 Azul Zulu 64 bits en tant que fichier TAR](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) vers un emplacement sur votre client, tel que `/usr/lib/jvm`.</span><span class="sxs-lookup"><span data-stu-id="65d90-128">[Download the 64-bit Azul Zulu JDK 8 as a TAR file](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) to a location on your client, such as `/usr/lib/jvm`.</span></span> <span data-ttu-id="65d90-129">(Des packages .RPM et .DEB sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).)</span><span class="sxs-lookup"><span data-stu-id="65d90-129">(.RPM and .DEB packages are also provided on [Azul's Azure downloads page](https://www.azul.com/downloads/azure-only/zulu/).)</span></span>

2. <span data-ttu-id="65d90-130">Accédez à votre répertoire et exécutez la commande suivante pour décompresser et développer le fichier :</span><span class="sxs-lookup"><span data-stu-id="65d90-130">Go to your directory and run the following command to unzip and expand the file:</span></span>

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a><span data-ttu-id="65d90-131">Confirmer l’installation</span><span class="sxs-lookup"><span data-stu-id="65d90-131">Confirm your installation</span></span>

<span data-ttu-id="65d90-132">Pour confirmer l’installation, accédez à la ligne de commande et exécutez `java -version`.</span><span class="sxs-lookup"><span data-stu-id="65d90-132">To confirm your installation, go to the command-line and run `java -version`.</span></span>

<span data-ttu-id="65d90-133">La commande doit retourner ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="65d90-133">The output of the command should be:</span></span>

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a><span data-ttu-id="65d90-134">Télécharger et installer les JDK Azul Zulu à partir d’un référentiel Yuml</span><span class="sxs-lookup"><span data-stu-id="65d90-134">Download and install the Azul Zulu JDKs from a Yum repository</span></span>

<span data-ttu-id="65d90-135">Les JDK Azul Zulu sont fournis dans un [référentiel Yum](http://repos.azul.com/azure-only/zulu-azure.repo) par Azul.</span><span class="sxs-lookup"><span data-stu-id="65d90-135">The Azul Zulu JDKs are provided in a [Yum repository](http://repos.azul.com/azure-only/zulu-azure.repo) by Azul.</span></span>

<span data-ttu-id="65d90-136">**Pour installer le JDK Azul Zulu pour Java 8, exécutez les commandes suivantes à partir de votre interface CLI :**</span><span class="sxs-lookup"><span data-stu-id="65d90-136">**To install the Azul Zulu JDK for Java 8, run the following commands from your CLI:**</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="65d90-137">Pour Java 11, exécutez :</span><span class="sxs-lookup"><span data-stu-id="65d90-137">For Java 11, run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

<span data-ttu-id="65d90-138">Pour Java 12 (préversion), exécutez :</span><span class="sxs-lookup"><span data-stu-id="65d90-138">For Java 12 (Preview), run:</span></span>

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

<span data-ttu-id="65d90-139">**Pour mettre à jour un package Zulu JDK 8 à partir d’un référentiel Yum :**</span><span class="sxs-lookup"><span data-stu-id="65d90-139">**To update a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

<span data-ttu-id="65d90-140">(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).</span><span class="sxs-lookup"><span data-stu-id="65d90-140">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="65d90-141">**Pour supprimer un package Zulu JDK 8 à partir d’un référentiel Yum :**</span><span class="sxs-lookup"><span data-stu-id="65d90-141">**To remove a Zulu JDK 8 package from a Yum repository:**</span></span>

```cli
sudo yum -y erase zulu-8-azure-jdk
```
<span data-ttu-id="65d90-142">(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).</span><span class="sxs-lookup"><span data-stu-id="65d90-142">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a><span data-ttu-id="65d90-143">Télécharger et installer les JDK Azul Zulu à partir d’un référentiel apt-get</span><span class="sxs-lookup"><span data-stu-id="65d90-143">Download and install the Azul Zulu JDKs from an apt-get repository</span></span>

<span data-ttu-id="65d90-144">Les JDK Azul Zulu sont aussi fournis dans un [référentiel apt-get](http://repos.azul.com/azure-only/zulu/apt) par Azul.</span><span class="sxs-lookup"><span data-stu-id="65d90-144">The Azul Zulu JDKs are also provided in an [apt-get repository](http://repos.azul.com/azure-only/zulu/apt) by Azul.</span></span>

<span data-ttu-id="65d90-145">**Pour installer le JDK Azul Zulu pour Java 8 avec apt-get, exécutez les commandes suivantes à partir de votre interface CLI :**</span><span class="sxs-lookup"><span data-stu-id="65d90-145">**To install the Azul Zulu JDK for Java 8 with apt-get, run the following commands from your CLI:**</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="65d90-146">Pour Java 11, exécutez :</span><span class="sxs-lookup"><span data-stu-id="65d90-146">For Java 11, run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

<span data-ttu-id="65d90-147">Pour Java 12 (préversion), exécutez :</span><span class="sxs-lookup"><span data-stu-id="65d90-147">For Java 12 (Preview), run:</span></span>

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

<span data-ttu-id="65d90-148">**Pour mettre à jour un package Zulu JDK 8 à partir d’un référentiel apt-get :**</span><span class="sxs-lookup"><span data-stu-id="65d90-148">**To update a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

<span data-ttu-id="65d90-149">La version précédente sera automatiquement supprimée.</span><span class="sxs-lookup"><span data-stu-id="65d90-149">The previous release will be automatically removed.</span></span>
<span data-ttu-id="65d90-150">(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).</span><span class="sxs-lookup"><span data-stu-id="65d90-150">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="65d90-151">**Pour supprimer un package Zulu JDK 8 à partir d’un référentiel apt-get :**</span><span class="sxs-lookup"><span data-stu-id="65d90-151">**To remove a Zulu JDK 8 package from an apt-get repository:**</span></span>

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

<span data-ttu-id="65d90-152">(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).</span><span class="sxs-lookup"><span data-stu-id="65d90-152">(Change the version number in the command above if you are using versions 11 or 12.)</span></span>

<span data-ttu-id="65d90-153">Pour plus d’informations sur la préparation, l’installation et la gestion de vos JDK Azul Zulu pour le développement Azure, lisez [la documentation officielle Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).</span><span class="sxs-lookup"><span data-stu-id="65d90-153">For more detailed guidance on preparing, installing, and managing your Azul Zulu JDKs for Azure development, read [the official Zulu docs](https://docs.azul.com/zulu/zuludocs/index.htm).</span></span>

