---
title: JDK Java et prise en charge à long terme pour le développement Azure
description: Téléchargements et instruction de la prise en charge d’Azure pour le développement et l’exécution d’applications Java.
author: bmitchell287
manager: douge
ms.devlang: java
ms.topic: conceptual
ms.date: 04/09/2019
ms.author: brendm
ms.openlocfilehash: 340f6149ffe39ccbb2d7de534ed63b8784d1f63a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270883"
---
# <a name="java-long-term-support-for-azure-and-azure-stack"></a><span data-ttu-id="048df-103">Prise en charge à long terme de Java pour Azure et Azure Stack</span><span class="sxs-lookup"><span data-stu-id="048df-103">Java Long-Term Support for Azure and Azure Stack</span></span>

<span data-ttu-id="048df-104">Les développeurs Java sur Azure et Azure Stack peuvent générer et exécuter des applications de production Java grâce à [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) sans entraîner de frais supplémentaires de support.</span><span class="sxs-lookup"><span data-stu-id="048df-104">Java developers on Azure and Azure Stack can build and run production Java applications using [Azul Zulu Enterprise for Azure](https://www.azul.com/downloads/azure-only/zulu/) without incurring additional support costs.</span></span> <span data-ttu-id="048df-105">Vous pouvez utiliser le runtime Java que vous souhaitez sur Azure, mais quand vous utilisez Zulu, vous obtenez des mises à jour de maintenance gratuites et vous pouvez poser des questions de prise en charge avec Microsoft.</span><span class="sxs-lookup"><span data-stu-id="048df-105">You can use any Java runtime you want on Azure, but when you use Zulu you get free maintenance updates and can create support issues with Microsoft.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="048df-106">Télécharger et installer Java</span><span class="sxs-lookup"><span data-stu-id="048df-106">Download and install Java</span></span>](java-jdk-install.md)

## <a name="long-term-support-lts"></a><span data-ttu-id="048df-107">Prise en charge à long terme (LTS)</span><span class="sxs-lookup"><span data-stu-id="048df-107">Long-term support (LTS)</span></span>

* [<span data-ttu-id="048df-108">Java 11</span><span class="sxs-lookup"><span data-stu-id="048df-108">Java 11</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java11)
* [<span data-ttu-id="048df-109">Java 8</span><span class="sxs-lookup"><span data-stu-id="048df-109">Java 8</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java8)
* [<span data-ttu-id="048df-110">Java 7</span><span class="sxs-lookup"><span data-stu-id="048df-110">Java 7</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java7)

## <a name="technical-preview"></a><span data-ttu-id="048df-111">Préversion technique</span><span class="sxs-lookup"><span data-stu-id="048df-111">Technical preview</span></span>

* [<span data-ttu-id="048df-112">Java 12</span><span class="sxs-lookup"><span data-stu-id="048df-112">Java 12</span></span>](https://www.azul.com/downloads/azure-only/zulu/#java12)

## <a name="what-is-the-zulu-openjdk-for-azure"></a><span data-ttu-id="048df-113">Qu’est-ce que l’OpenJDK Zulu pour Azure ?</span><span class="sxs-lookup"><span data-stu-id="048df-113">What is the Zulu OpenJDK for Azure?</span></span>

<span data-ttu-id="048df-114">Les builds Azul Zulu Enterprise d’OpenJDK sont une distribution gratuite, multiplateforme et prête pour la production d’OpenJDK pour Azure et Azure Stack pris en charge par Microsoft et Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="048df-114">Azul Zulu Enterprise builds of OpenJDK are a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure and Azure Stack backed by Microsoft and Azul Systems.</span></span> <span data-ttu-id="048df-115">Ces distributions sont :</span><span class="sxs-lookup"><span data-stu-id="048df-115">These distributions are:</span></span>

* <span data-ttu-id="048df-116">Des builds 100 % open source d’OpenJDK empaquetées en tant que Kits de développement Java (JDK), environnements d’exécution Java (JRE) et environnements JRE avec administration à distance.</span><span class="sxs-lookup"><span data-stu-id="048df-116">100% open source builds of OpenJDK packaged as Java Development Kits (JDKs), Java Runtime Environments (JREs), and Headless JREs.</span></span> <span data-ttu-id="048df-117">Ces binaires sont des builds commerciales entièrement compatibles et conformes de Java Standard Edition (SE) qui peuvent être utilisées avec des applications ou des composants Java sur Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="048df-117">These binaries are fully compatible and compliant commercial builds of Java Standard Edition (SE) that can be used with Java applications or components on Azure and Azure Stack.</span></span>
* <span data-ttu-id="048df-118">Fournies avec une prise en charge à long terme comprenant des correctifs de bogues, des améliorations de performances et des correctifs de sécurité.</span><span class="sxs-lookup"><span data-stu-id="048df-118">Provided with long-term support including bug fixes, performance enhancements, and security patches.</span></span>
* <span data-ttu-id="048df-119">Disponibles pour le développement et l’exécution d’applications Java sur Windows, Linux et MacOS.</span><span class="sxs-lookup"><span data-stu-id="048df-119">Available for developing and running Java applications on Windows, Linux, and MacOS.</span></span>
* <span data-ttu-id="048df-120">Disponibles en tant qu’images conteneur sur Docker Hub et en tant que machines virtuelles (Windows et Linux) sur la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="048df-120">Available as container images on Docker Hub and as virtual machines (Windows and Linux) on Azure Marketplace.</span></span>
* <span data-ttu-id="048df-121">Utilisées par Microsoft Azure pour alimenter de nombreux services Azure tels que :</span><span class="sxs-lookup"><span data-stu-id="048df-121">Used by Microsoft Azure to power many Azure services, such as:</span></span>
  * <span data-ttu-id="048df-122">App Service Windows</span><span class="sxs-lookup"><span data-stu-id="048df-122">App Service Windows</span></span>
  * <span data-ttu-id="048df-123">App Service Linux</span><span class="sxs-lookup"><span data-stu-id="048df-123">App Service Linux</span></span>
  * <span data-ttu-id="048df-124">Fonctions</span><span class="sxs-lookup"><span data-stu-id="048df-124">Functions</span></span>
  * <span data-ttu-id="048df-125">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="048df-125">Service Fabric</span></span>
  * <span data-ttu-id="048df-126">HDInsight</span><span class="sxs-lookup"><span data-stu-id="048df-126">HDInsight</span></span>
  * <span data-ttu-id="048df-127">Recherche</span><span class="sxs-lookup"><span data-stu-id="048df-127">Search</span></span>
  * <span data-ttu-id="048df-128">Azure DevOps</span><span class="sxs-lookup"><span data-stu-id="048df-128">Azure DevOps</span></span>
  * <span data-ttu-id="048df-129">Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="048df-129">Cloud Shell</span></span>  

## <a name="supported-java-versions-and-update-schedule"></a><span data-ttu-id="048df-130">Versions de Java prises en charge et planification de la mise à jour</span><span class="sxs-lookup"><span data-stu-id="048df-130">Supported Java versions and update schedule</span></span>

<span data-ttu-id="048df-131">Azul Systems fournit des [versions OpenJDK de Zulu Entreprise pour Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) entièrement prises en charge, pour toutes les versions LTS de Java, à compter de Java SE 7, 8 et 11.</span><span class="sxs-lookup"><span data-stu-id="048df-131">Azul Systems provides fully-supported [Zulu Enterprise builds of OpenJDK for Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) for all long-term support (LTS) versions of Java, starting with Java SE 7, 8, and 11.</span></span> <span data-ttu-id="048df-132">Le [communiqué de presse Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack) peut vous fournir plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="048df-132">More information can be found in the [Azul press release](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack).</span></span>

|<span data-ttu-id="048df-133">Java SE LTS</span><span class="sxs-lookup"><span data-stu-id="048df-133">Java SE LTS</span></span>  |<span data-ttu-id="048df-134">Prise en charge jusque</span><span class="sxs-lookup"><span data-stu-id="048df-134">Support until</span></span>  |
|---------|----------|
|<span data-ttu-id="048df-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span><span class="sxs-lookup"><span data-stu-id="048df-135">[![Java 7](../media/jdk/java-7.png)](https://www.azul.com/downloads/azure-only/zulu/#java7)</span></span> |<span data-ttu-id="048df-136">Juillet 2023</span><span class="sxs-lookup"><span data-stu-id="048df-136">July 2023</span></span> |
|<span data-ttu-id="048df-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span><span class="sxs-lookup"><span data-stu-id="048df-137">[![Java 8](../media/jdk/java-8.png)](https://www.azul.com/downloads/azure-only/zulu/#java8)</span></span> |<span data-ttu-id="048df-138">Mars 2025</span><span class="sxs-lookup"><span data-stu-id="048df-138">March 2025</span></span>|
|<span data-ttu-id="048df-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span><span class="sxs-lookup"><span data-stu-id="048df-139">[![Java 11](../media/jdk/java-11.png)](https://www.azul.com/downloads/azure-only/zulu/#java11)</span></span> |<span data-ttu-id="048df-140">Septembre 2026</span><span class="sxs-lookup"><span data-stu-id="048df-140">Sept. 2026</span></span>|
|<span data-ttu-id="048df-141">[![Java 12](../media/jdk/java-12.png)]()</span><span class="sxs-lookup"><span data-stu-id="048df-141">[![Java 12](../media/jdk/java-12.png)]()</span></span> |<span data-ttu-id="048df-142">**PRÉVERSION**</span><span class="sxs-lookup"><span data-stu-id="048df-142">**PREVIEW**</span></span>|

<span data-ttu-id="048df-143">Ces versions de JDK disposent de mises à jour de sécurité et de correctifs de bogues tous les trimestres, ainsi que de mises à jour et correctifs hors bande critiques en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="048df-143">These JDK releases have quarterly security updates, bug fixes, and critical out-of-band updates and patches as needed.</span></span>  <span data-ttu-id="048df-144">Cette prise en charge inclut le rétroportage des mises à jour de sécurité et des correctifs de bogues pour Java 7 et 8 signalés dans les versions plus récentes de Java, comme Java 11, qui garantit la stabilité continue et la sécurité des versions antérieures de Java.</span><span class="sxs-lookup"><span data-stu-id="048df-144">This support includes back ports of security updates and bug fixes to Java 7 and 8 reported in newer versions of Java such as Java 11, which ensures the continued stability and security of older versions of Java.</span></span>  <span data-ttu-id="048df-145">Les clients Azure peuvent obtenir ces mises à jour de sécurité et correctifs de bogues de plateforme sans entraîner de frais imprévus d’abonnement Java SE.</span><span class="sxs-lookup"><span data-stu-id="048df-145">Azure customers can get these security updates and platform bug fixes without incurring any unplanned Java SE subscription fees.</span></span>

<span data-ttu-id="048df-146">Azul Systems conserve une [feuille de route Java SE](https://www.azul.com/products/azul_support_roadmap/) pour ces versions.</span><span class="sxs-lookup"><span data-stu-id="048df-146">Azul Systems maintains a [Java SE roadmap](https://www.azul.com/products/azul_support_roadmap/) for these releases.</span></span>

## <a name="benefits-for-developers"></a><span data-ttu-id="048df-147">Avantages pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="048df-147">Benefits for developers</span></span>

<span data-ttu-id="048df-148">Les versions des JDK Azul Zulu sont :</span><span class="sxs-lookup"><span data-stu-id="048df-148">The Azul Zulu JDK releases are:</span></span>

1. <span data-ttu-id="048df-149">Supportées et prises en charge par Microsoft et Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="048df-149">Backed and supported by both Microsoft and Azul Systems</span></span>

   * <span data-ttu-id="048df-150">Les binaires Zulu sont prêts pour la production et pris en charge par Microsoft et Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="048df-150">Zulu binaries are production-ready and backed by Microsoft and Azul Systems</span></span>
   * <span data-ttu-id="048df-151">Zulu offre une prise en charge à long terme (LTS) sans frais pour Java 7, 8 et 11.</span><span class="sxs-lookup"><span data-stu-id="048df-151">Zulu comes with zero-cost long-term support (LTS) for Java 7, 8, and 11.</span></span> <span data-ttu-id="048df-152">(La prise en charge à long terme sera également fournie pour Java 17.)</span><span class="sxs-lookup"><span data-stu-id="048df-152">(LTS will be provided for Java 17, as well).</span></span> <span data-ttu-id="048df-153">Vous pouvez mettre à niveau les versions de Java uniquement quand vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="048df-153">You can upgrade Java versions only when you need to.</span></span>
   * <span data-ttu-id="048df-154">Java 7 est pris en charge jusqu’à juillet 2023.</span><span class="sxs-lookup"><span data-stu-id="048df-154">Java 7 supported until July 2023.</span></span> <span data-ttu-id="048df-155">Java 8 et 11 sont pris en charge au-delà de 2024.</span><span class="sxs-lookup"><span data-stu-id="048df-155">Java 8 and 11 are supported beyond 2024.</span></span>
   * <span data-ttu-id="048df-156">Microsoft s’engage à exécuter Zulu en interne sur des ordinateurs qui alimentent de nombreux services Azure.</span><span class="sxs-lookup"><span data-stu-id="048df-156">Microsoft is committed to running Zulu internally on machines that power many Azure services.</span></span>

2. <span data-ttu-id="048df-157">Prêtes pour la production</span><span class="sxs-lookup"><span data-stu-id="048df-157">Production-ready</span></span>

   * <span data-ttu-id="048df-158">100 % open source pour ses builds d’OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="048df-158">100% open-source for its builds of OpenJDK.</span></span>
   * <span data-ttu-id="048df-159">Substituts pour de nombreuses distributions de Java SE.</span><span class="sxs-lookup"><span data-stu-id="048df-159">Drop-in replacements for many Java SE distributions.</span></span>
   * <span data-ttu-id="048df-160">JDK, JRE et JRE avec administration à distance</span><span class="sxs-lookup"><span data-stu-id="048df-160">JDK, JRE, and JRE-headless</span></span>
   * <span data-ttu-id="048df-161">Java 7, 8 et 11</span><span class="sxs-lookup"><span data-stu-id="048df-161">Java 7, 8, and 11</span></span>
   * <span data-ttu-id="048df-162">Conformité vérifiée avec les spécifications Java SE utilisant le Kit TCK (Technology Compatibility Kit) de la Communauté OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="048df-162">Verified compliant with the Java SE  specifications using the OpenJDK Community Technology Compatibility Kit (TCK).</span></span>
   * <span data-ttu-id="048df-163">Les développeurs continueront à recevoir des mises à jour de production pour Java SE, notamment des correctifs de bogues, des améliorations des performances et des correctifs de sécurité pour Java SE 7, 8 et 11.</span><span class="sxs-lookup"><span data-stu-id="048df-163">Developers will continue to receive production updates for Java SE, including bug fixes, performance enhancements, and security patches for Java SE 7, 8, and 11.</span></span>

3. <span data-ttu-id="048df-164">Prises en charge sur plusieurs plateformes.</span><span class="sxs-lookup"><span data-stu-id="048df-164">Supported for multi-platform.</span></span> <span data-ttu-id="048df-165">Zulu prend en charge les binaires pour plusieurs plateformes et versions, notamment :</span><span class="sxs-lookup"><span data-stu-id="048df-165">Zulu supports binaries for multiple platforms and versions, including:</span></span>

   * <span data-ttu-id="048df-166">Client Windows</span><span class="sxs-lookup"><span data-stu-id="048df-166">Windows Client</span></span>
     * <span data-ttu-id="048df-167">10</span><span class="sxs-lookup"><span data-stu-id="048df-167">10</span></span>
     * <span data-ttu-id="048df-168">8.1</span><span class="sxs-lookup"><span data-stu-id="048df-168">8.1</span></span>
     * <span data-ttu-id="048df-169">8, 7</span><span class="sxs-lookup"><span data-stu-id="048df-169">8, 7</span></span>
   * <span data-ttu-id="048df-170">Windows Server</span><span class="sxs-lookup"><span data-stu-id="048df-170">Windows Server</span></span>
     * <span data-ttu-id="048df-171">2016R2</span><span class="sxs-lookup"><span data-stu-id="048df-171">2016R2</span></span>
     * <span data-ttu-id="048df-172">2016</span><span class="sxs-lookup"><span data-stu-id="048df-172">2016</span></span>
     * <span data-ttu-id="048df-173">2012 R2</span><span class="sxs-lookup"><span data-stu-id="048df-173">2012 R2</span></span>
     * <span data-ttu-id="048df-174">2012</span><span class="sxs-lookup"><span data-stu-id="048df-174">2012</span></span>
     * <span data-ttu-id="048df-175">2008 R2</span><span class="sxs-lookup"><span data-stu-id="048df-175">2008 R2</span></span>
   * <span data-ttu-id="048df-176">Linux, notamment</span><span class="sxs-lookup"><span data-stu-id="048df-176">Linux, including</span></span>
     * <span data-ttu-id="048df-177">RHEL</span><span class="sxs-lookup"><span data-stu-id="048df-177">RHEL</span></span>
     * <span data-ttu-id="048df-178">CentOS</span><span class="sxs-lookup"><span data-stu-id="048df-178">CentOS</span></span>
     * <span data-ttu-id="048df-179">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="048df-179">Ubuntu</span></span>
     * <span data-ttu-id="048df-180">SLES</span><span class="sxs-lookup"><span data-stu-id="048df-180">SLES</span></span>
     * <span data-ttu-id="048df-181">Debian</span><span class="sxs-lookup"><span data-stu-id="048df-181">Debian</span></span>
     * <span data-ttu-id="048df-182">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="048df-182">Oracle Linux</span></span>
   * <span data-ttu-id="048df-183">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="048df-183">Mac OS X</span></span>
   * <span data-ttu-id="048df-184">Délivrées dans plusieurs types de packages :</span><span class="sxs-lookup"><span data-stu-id="048df-184">delivered in multiple package types:</span></span>
     * <span data-ttu-id="048df-185">MSI, ZIP, TAR, DEB, RPM et DMG</span><span class="sxs-lookup"><span data-stu-id="048df-185">MSI, ZIP, TAR, DEB, RPM, and DMG</span></span>

    <span data-ttu-id="048df-186">Des images conteneur Docker certifiées pour Zulu JDK, JRE et JRE avec administration à distance sur plusieurs images de système d’exploitation de base sont disponibles dans Docker.</span><span class="sxs-lookup"><span data-stu-id="048df-186">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker.</span></span>

    <span data-ttu-id="048df-187">Hub :</span><span class="sxs-lookup"><span data-stu-id="048df-187">Hub:</span></span>

    * [<span data-ttu-id="048df-188">JDK</span><span class="sxs-lookup"><span data-stu-id="048df-188">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
    * [<span data-ttu-id="048df-189">JRE</span><span class="sxs-lookup"><span data-stu-id="048df-189">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
    * [<span data-ttu-id="048df-190">JRE avec administration à distance</span><span class="sxs-lookup"><span data-stu-id="048df-190">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

4. <span data-ttu-id="048df-191">Aucun coût</span><span class="sxs-lookup"><span data-stu-id="048df-191">No cost</span></span>

   * <span data-ttu-id="048df-192">Microsoft fournit tout ce dont vous avez besoin pour concevoir et développer gratuitement des applications Java sur Azure.</span><span class="sxs-lookup"><span data-stu-id="048df-192">Microsoft provides everything you need to build and scale Java apps on Azure at no cost to you.</span></span> <span data-ttu-id="048df-193">Vous recevrez par le biais de Zulu des mises à jour de sécurité et des correctifs de bogues de plateforme gratuits pour les applications Java.</span><span class="sxs-lookup"><span data-stu-id="048df-193">Through Zulu you'll receive free security updates and platform bug fixes for Java apps without any fees.</span></span>
   * <span data-ttu-id="048df-194">[Java Flight Recorder et Mission Control](java-jdk-flight-recorder-and-mission-control.md) sont disponibles dans Java Zulu 8, 11 et 12 (préversion).</span><span class="sxs-lookup"><span data-stu-id="048df-194">[Java Flight Recorder and Mission Control](java-jdk-flight-recorder-and-mission-control.md) are available in Zulu Java 8, 11, and 12 (Preview).</span></span>

5. <span data-ttu-id="048df-195">Préversions techniques des versions non-LTS</span><span class="sxs-lookup"><span data-stu-id="048df-195">Tech Preview of Non-LTS versions</span></span>

   * <span data-ttu-id="048df-196">Les préversions techniques offrent l’opportunité de tester progressivement de nouvelles fonctionnalités à mesure qu’elles sont disponibles dans les versions à court terme, fonctionnalités destinées à être publiées dans Java 17 LTS.</span><span class="sxs-lookup"><span data-stu-id="048df-196">Tech previews provide you with opportunities to progressively test new features as they are delivered in short-term versions that will eventually graduate to Java 17 LTS.</span></span>

6. <span data-ttu-id="048df-197">Les modifications apportées à OpenJDK sont publiées en amont</span><span class="sxs-lookup"><span data-stu-id="048df-197">Changes to OpenJDK are up-streamed</span></span>

   * <span data-ttu-id="048df-198">Azul Systems publie les modifications apportées par Zulu à OpenJDK, ce qui rend le dépôt en amont complet et inclusif.</span><span class="sxs-lookup"><span data-stu-id="048df-198">Azul Systems committers push Zulu changes to OpenJDK which makes the upstream repo comprehensive and inclusive.</span></span>

<span data-ttu-id="048df-199">Comme toujours, les développeurs Java peuvent disposer de leur propre runtime Java (Oracle JDK et Red Hat JDK compris) sur Azure et utiliser les services d’infrastructure sécurisée et riches en fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="048df-199">As always, Java developers can bring their own Java run-times, including Oracle JDK and Red Hat JDK, to Azure and use  the secure infrastructure and feature-rich services.</span></span> <span data-ttu-id="048df-200">L’édition de production d’Oracle Java SE est également accessible aux développeurs Java pour exécuter des charges de travail Java sur Azure, sur des machines virtuelles Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="048df-200">The production edition of Oracle Java SE is also available to Java developers for running Java workloads in Windows or Linux virtual machines on Azure.</span></span>

## <a name="use-for-local-development"></a><span data-ttu-id="048df-201">Utilisation pour le développement local</span><span class="sxs-lookup"><span data-stu-id="048df-201">Use for local development</span></span> 

<span data-ttu-id="048df-202">Les développeurs peuvent [télécharger](https://www.azul.com/downloads/azure-only/zulu/) des JDK Java pour Azure et Azure Stack afin de les utiliser dans des environnements de développement locaux.</span><span class="sxs-lookup"><span data-stu-id="048df-202">Developers can [download](https://www.azul.com/downloads/azure-only/zulu/) Java JDKs for Azure and Azure Stack for use in local development environments.</span></span> <span data-ttu-id="048df-203">Les téléchargements sont disponibles pour Windows, Linux et MacOS.</span><span class="sxs-lookup"><span data-stu-id="048df-203">Downloads are available for Windows, Linux, and macOS.</span></span> <span data-ttu-id="048df-204">Les développeurs qui travaillent sur Linux peuvent aussi obtenir des packages par l’intermédiaire des gestionnaires de package [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) et [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).</span><span class="sxs-lookup"><span data-stu-id="048df-204">Developers working on Linux can also get packages through the [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) and [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo) package managers.</span></span>

<span data-ttu-id="048df-205">Pour plus d’informations, consultez [Images Docker pour Azure](java-jdk-docker-images.md).</span><span class="sxs-lookup"><span data-stu-id="048df-205">For additional guidance see [Docker images for Azure](java-jdk-docker-images.md).</span></span>