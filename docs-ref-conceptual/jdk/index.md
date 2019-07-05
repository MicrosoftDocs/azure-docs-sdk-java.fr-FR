---
title: JDK Java et prise en charge à long terme pour le développement Azure
description: Cet article comprend des liens de téléchargement ainsi qu’une présentation de la prise en charge Azure pour le développement et l’exécution d’applications Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 1bb93f775686b5b0f127c586dda802f4eb5f775d
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533640"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a>Prise en charge à long terme de Java pour Azure et Azure Stack

En tant que développeur Java sur Microsoft Azure et Azure Stack, vous pouvez générer et exécuter des applications de production Java avec [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/), sans entraîner de frais de prise en charge supplémentaires. Vous pouvez utiliser le runtime Java que vous souhaitez dans Azure. Notez toutefois que lorsque vous utilisez Zulu, vous bénéficiez de mises à jour de maintenance gratuites et vous pouvez résoudre vos problèmes de prise en charge avec Microsoft.

> [!div class="nextstepaction"]
> [Télécharger et installer Java](java-jdk-install.md)

## <a name="long-term-support"></a>Prise en charge à long terme

* [Java 11](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [Java 8](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [Java 7](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a>Préversion technique

* [Java 12](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a>Qu’est-ce que l’OpenJDK Zulu pour Azure ?

Les builds Azul Zulu Enterprise d’OpenJDK sont une distribution gratuite, multiplateforme et prête pour la production d’OpenJDK pour Azure et Azure Stack. Elles sont prises en charge par Microsoft et Azul Systems. Ces distributions sont :

* Des builds 100 % open source d’OpenJDK, empaquetées sous la forme de JDK, de JRE et de JRE avec administration à distance. Ces binaires sont des builds commerciales entièrement compatibles et conformes de Java Standard Edition (SE) qui peuvent être utilisées avec des applications ou des composants Java sur Azure et Azure Stack.
* Fournies avec une prise en charge à long terme (LTS) comprenant des correctifs de bogues, des améliorations de performances et des correctifs de sécurité.
* Disponibles pour le développement et l’exécution d’applications Java sur Windows, Linux et MacOS.
* Disponibles en tant qu’images conteneur sur Docker Hub et en tant que machines virtuelles (Windows et Linux) sur la Place de marché Azure.
* Utilisées par Azure pour alimenter de nombreux services Azure tels que :
  * Azure App Service (Windows)
  * Azure App Service (Linux)
  * Azure Functions
  * Azure Service Fabric
  * Azure HDInsight
  * Recherche Azure
  * Azure DevOps
  * Azure Cloud Shell  

## <a name="supported-java-versions-and-update-schedule"></a>Versions de Java prises en charge et planification de la mise à jour

Azul Systems fournit des [versions OpenJDK de Zulu Enterprise pour Azure](https://www.azul.com/downloads/azure-only/zulu/) entièrement prises en charge, pour toutes les versions LTS de Java, à compter de Java SE 7, 8 et 11. Pour plus d’informations, lisez le [communiqué de presse Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).

|Java SE LTS  |Prise en charge jusque  |
|---------|----------|
|[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7) |Juillet 2023 |
|[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8) |Mars 2025|
|[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11) |Septembre 2026|
|[![Java 12](../media/jdk/java-12.png)]() |**Préversion**|

Ces versions de JDK disposent de mises à jour de sécurité et de correctifs de bogues tous les trimestres, ainsi que de mises à jour et correctifs hors bande critiques en fonction des besoins. Cette prise en charge inclut des ports pour les mises à jour de sécurité ainsi que des correctifs de bogues pour Java 7 et 8, qui sont signalés dans les versions plus récentes de Java, comme Java 11. La prise en charge garantit la stabilité et la sécurité des versions antérieures de Java. Les clients Azure peuvent obtenir ces mises à jour de sécurité et correctifs de bogues de plateforme sans entraîner de frais imprévus d’abonnement Java SE.

Azul Systems conserve une [feuille de route Java SE](https://www.azul.com/products/azul_support_roadmap/) pour ces versions.

## <a name="benefits-for-developers"></a>Avantages pour les développeurs

Les versions des JDK Azul Zulu sont :

* Supportées et prises en charge par Microsoft et Azul Systems.

   * Les binaires Zulu sont prêts pour la production et pris en charge par Microsoft et Azul Systems.
   * Zulu est fourni avec une version LTS gratuite de Java 7, 8 et 11 (la version LTS sera fournie pour Java 17 également). Vous pouvez mettre à niveau les versions de Java uniquement quand vous en avez besoin.
   * Java 7 est pris en charge jusqu’en juillet 2023. Java 8 et 11 sont pris en charge au-delà de 2024.
   * Microsoft s’engage à exécuter Zulu en interne sur des ordinateurs qui alimentent de nombreux services Azure.

* Prêtes pour la production.

   * 100 % open source pour ses builds d’OpenJDK.
   * Substituts pour de nombreuses distributions de Java SE.
   * JDK, JRE et JRE avec administration à distance.
   * Java 7, 8 et 11.
   * Conformité vérifiée aux spécifications Java SE qui utilisent le Kit TCK (Technology Compatibility Kit) de la communauté OpenJDK.
   * En tant que développeur, vous continuerez de recevoir des mises à jour de production pour Java SE, notamment des correctifs de bogues, des améliorations des performances et des correctifs de sécurité pour Java SE 7, 8 et 11.

* Prises en charge sur plusieurs plateformes. Zulu prend en charge les binaires pour plusieurs plateformes et versions, notamment :

   * Client Windows
     * 10
     * 8.1
     * 8, 7
   * Windows Server
     * 2016 R2
     * 2016
     * 2012 R2
     * 2012
     * 2008 R2
   * Linux, notamment
     * RHEL
     * CentOS
     * Ubuntu
     * SLES
     * Debian
     * Oracle Linux
   * macOS X
   * Livrées sous la forme de plusieurs types de packages :
     * MSI, ZIP, TAR, DEB, RPM et DMG

    Des images conteneur Docker certifiées pour Zulu JDK, JRE et JRE avec administration à distance sur plusieurs images de système d’exploitation de base sont disponibles dans Docker.

    Hub :

    * [JDK](https://hub.docker.com/_/microsoft-java-jdk)
    * [JRE](https://hub.docker.com/_/microsoft-java-jre)
    * [JRE avec administration à distance](https://hub.docker.com/_/microsoft-java-jre-headless)

* Aucun coût.

   * Microsoft fournit tout ce dont vous avez besoin pour concevoir et développer gratuitement des applications Java sur Azure. Vous recevrez par le biais de Zulu des mises à jour de sécurité et des correctifs de bogues de plateforme gratuits pour les applications Java.
   * [Java Flight Recorder et Mission Control](java-jdk-flight-recorder-and-mission-control.md) sont disponibles dans Java Zulu 8, 11 et 12 (préversion).

* Disponibles sous la forme d’une préversion technique des versions non LTS.

   * Avec les préversions techniques, vous pouvez tester progressivement les nouvelles fonctionnalités à mesure qu’elles sont publiées, dans les versions à court terme destinées à devenir des versions Java 17 LTS.

* Les modifications apportées à OpenJDK sont publiées en amont.

   * Azul Systems pousse (push) les modifications apportées par Zulu vers OpenJDK, ce qui rend le dépôt en amont complet et inclusif.

Comme toujours, en tant que développeur Java, vous pouvez importer dans Azure vos propres runtimes Java, y compris le JDK Oracle et le JDK Red Hat. Vous pouvez également utiliser son infrastructure sécurisée et ses services riches en fonctionnalités. L’édition de production d’Oracle Java SE vous permet d’exécuter des charges de travail Java dans Azure, sur des machines virtuelles Windows ou Linux.

## <a name="use-java-jdks-for-local-development"></a>Utiliser les JDK Java pour le développement local 

Vous pouvez [télécharger des JDK Java pour Azure et Azure Stack](https://www.azul.com/downloads/azure-only/zulu/) en vue de les utiliser dans un environnement de développement local. Les téléchargements sont disponibles pour Windows, Linux et MacOS. Si vous travaillez sur Linux, vous pouvez également obtenir des packages par l’intermédiaire des gestionnaires de package [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) et [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

Pour plus d’informations, consultez [Images Docker pour Azure](java-jdk-docker-images.md).
