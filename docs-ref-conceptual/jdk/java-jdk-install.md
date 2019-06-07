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
# <a name="install-the-jdk-for-azure-and-azure-stack"></a>Installer le JDK pour Azure et Azure Stack

Les builds Azul Zulu Enterprise d’OpenJDK sont une distribution gratuite, multiplateforme et prête pour la production d’OpenJDK pour Azure et Azure Stack pris en charge par Microsoft et Azul Systems. Elles contiennent tous les composants nécessaires pour générer et exécuter des applications Java SE.

Il existe [plusieurs types de packages de téléchargement pris en charge pour chaque système d’exploitation client](https://www.azul.com/downloads/azure-only/zulu/). Vous pouvez également obtenir une image de machine virtuelle à partir de la galerie de la Place de marché Azure pour les plateformes suivantes :

  * [Azul Zulu : Java 8 sur Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-ubuntu-1804)
  * [Azul Zulu : Java 8 sur Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu8-windows-2019)
  
  * [Azul Zulu : Java 11 sur Ubuntu 18.04](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-ubuntu-1804)
  * [Azul Zulu : Java 11 sur Windows Server 2019](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/azul.azul-zulu11-windows-2019)


> [!NOTE]
> Ces instructions ciblent la version Java 8 64 bits du JDK. Azul fournit également l’environnement JRE (Java Run-time Environment) en tant qu’installation autonome. L’environnement JRE est inclus avec l’installation du JDK.
>
>  Les packages Java 11 sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).

## <a name="download-and-install-the-azul-zulu-jdks-for-windows"></a>Télécharger et installer les JDK Azul Zulu pour Windows 

1. [Téléchargez le JDK 8 Azul Zulu 64 bits en tant que fichier MSI](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-win_x64.msi) sur un emplacement de votre client, tel que `C:\Users\<your_login>\Downloads`. (Des packages .ZIP sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).)

2. Accédez au répertoire et double-cliquez sur le fichier MSI téléchargé pour commencer l’installation.

## <a name="download-and-install-the-azul-zulu-jdks-for-mac"></a>Télécharger et installer les JDK Azul Zulu pour Mac 

Ces étapes permettent de télécharger un fichier ZIP sur votre Mac. Une version DMG est également disponible.

1. [Téléchargez le JDK 8 Azul Zulu 64 bits en tant que fichier ZIP](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-macosx_x64.zip) vers un emplacement sur votre client, tel que `/Library/Java/JavaVirtualMachines/`. (Des packages .DMG sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).)

2. Lancez Finder, accédez au répertoire de téléchargement, puis double-cliquez sur le fichier ZIP. Vous pouvez aussi lancer une fenêtre de terminal de commande, accéder au répertoire et exécuter :

```cli
unzip <name_of_zulu_package>.zip
```

## <a name="download-and-install-the-azul-zulu-jdks-for-alpine-linux"></a>Télécharger et installer les JDK Azul Zulu pour Alpine Linux

1. [Téléchargez le JDK 8 Azul Zulu 64 bits en tant que fichier TAR](https://repos.azul.com/azure-only/zulu/packages/zulu-11/11.0.3/zulu-11-azure-jdk_11.31.11-11.0.3-linux_x64.tar.gz) vers un emplacement sur votre client, tel que `/usr/lib/jvm`. (Des packages .RPM et .DEB sont également disponibles dans la [page de téléchargement Azure d’Azul](https://www.azul.com/downloads/azure-only/zulu/).)

2. Accédez à votre répertoire et exécutez la commande suivante pour décompresser et développer le fichier :

    ```cli
    tar -xvf <name_of_zulu_package>.tar
    ```

## <a name="confirm-your-installation"></a>Confirmer l’installation

Pour confirmer l’installation, accédez à la ligne de commande et exécutez `java -version`.

La commande doit retourner ce qui suit :

```cli
$ java -version

openjdk version "1.8.0_212"
OpenJDK Runtime Environment (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM (Zulu 8.38.0.13-macosx)-Microsoft-Azure-restricted (build 25.212-b04, mixed mode)

```

## <a name="download-and-install-the-azul-zulu-jdks-from-a-yum-repository"></a>Télécharger et installer les JDK Azul Zulu à partir d’un référentiel Yuml

Les JDK Azul Zulu sont fournis dans un [référentiel Yum](http://repos.azul.com/azure-only/zulu-azure.repo) par Azul.

**Pour installer le JDK Azul Zulu pour Java 8, exécutez les commandes suivantes à partir de votre interface CLI :**

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-8-azure-jdk
```

Pour Java 11, exécutez :

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-11-azure-jdk
```

Pour Java 12 (préversion), exécutez :

```cli
sudo rpm --import http://repos.azul.com/azul-repo.key
sudo curl http://repos.azul.com/azure-only/zulu-azure.repo -o /etc/yum.repos.d/zulu-azure.repo
sudo yum -q -y update
sudo yum -q -y install zulu-12-azure-jdk
```

**Pour mettre à jour un package Zulu JDK 8 à partir d’un référentiel Yum :**

```cli
sudo yum -q -y install zulu-8-azure-jdk
```

(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).

**Pour supprimer un package Zulu JDK 8 à partir d’un référentiel Yum :**

```cli
sudo yum -y erase zulu-8-azure-jdk
```
(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).

## <a name="download-and-install-the-azul-zulu-jdks-from-an-apt-get-repository"></a>Télécharger et installer les JDK Azul Zulu à partir d’un référentiel apt-get

Les JDK Azul Zulu sont aussi fournis dans un [référentiel apt-get](http://repos.azul.com/azure-only/zulu/apt) par Azul.

**Pour installer le JDK Azul Zulu pour Java 8 avec apt-get, exécutez les commandes suivantes à partir de votre interface CLI :**

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

Pour Java 11, exécutez :

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-11-azure-jdk
```

Pour Java 12 (préversion), exécutez :

```cli
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 0xB1998361219BD9C9
sudo apt-add-repository "deb http://repos.azul.com/azure-only/zulu/apt stable main"
sudo apt-get -q update
sudo apt-get -y install zulu-12-azure-jdk
```

**Pour mettre à jour un package Zulu JDK 8 à partir d’un référentiel apt-get :**

```cli
sudo apt-get -q update
sudo apt-get -y install zulu-8-azure-jdk
```

La version précédente sera automatiquement supprimée.
(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).

**Pour supprimer un package Zulu JDK 8 à partir d’un référentiel apt-get :**

```cli
sudo apt-get -y purge zulu-8-azure-jdk
```

(Changez le numéro de version dans la commande ci-dessus si vous utilisez la version 11 ou 12).

Pour plus d’informations sur la préparation, l’installation et la gestion de vos JDK Azul Zulu pour le développement Azure, lisez [la documentation officielle Zulu](https://docs.azul.com/zulu/zuludocs/index.htm).

