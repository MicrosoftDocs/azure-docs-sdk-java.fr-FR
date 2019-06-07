---
title: Java Flight Recorder et Mission Control
description: Conseils d’utilisation de Java Flight Recorder et Mission Control afin de recueillir et d’examiner les données d’application.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: b27e0f741f1322b7e8e1df363dbb2f40a3d34d53
ms.sourcegitcommit: 04cff6e3c6d3a9c15f7d88d5d3c238f0bdc787fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2019
ms.locfileid: "64568562"
---
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a><span data-ttu-id="f5fe8-103">Utilisation de Java Flight Recorder (JFR) et Mission Control</span><span class="sxs-lookup"><span data-stu-id="f5fe8-103">Using Java Flight Recorder (JFR) and Mission Control</span></span>

<span data-ttu-id="f5fe8-104">Zulu Mission Control est une build entièrement testée de JDK Mission Control, publiée en open source par Oracle en 2018 et gérée en tant que projet sous l’égide OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="f5fe8-105">Associé à Flight Recorder, Mission Control offre des fonctionnalités de gestion et de supervision interactives et à faible charge pour les charges de travail Java.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-105">Coupled with Flight Recorder, Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="f5fe8-106">Zulu Mission Control est compatible avec les JDK/JRE suivants :</span><span class="sxs-lookup"><span data-stu-id="f5fe8-106">Zulu Mission Control is compatible with the following JDKs/JREs:</span></span>

* <span data-ttu-id="f5fe8-107">Zulu 12.1 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="f5fe8-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="f5fe8-108">Zulu 11.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="f5fe8-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="f5fe8-109">Zulu 8u202 (8.36) et ultérieur</span><span class="sxs-lookup"><span data-stu-id="f5fe8-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="f5fe8-110">Oracle OpenJDK 11+15 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="f5fe8-110">Oracle OpenJDK 11+15 and later</span></span>
* <span data-ttu-id="f5fe8-111">Oracle Java 11.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="f5fe8-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="f5fe8-112">Oracle Java 8.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="f5fe8-112">Oracle Java 8.0 and later</span></span>

<span data-ttu-id="f5fe8-113">Suivez les étapes ci-dessous pour installer Zulu Mission Control, vous connecter à une machine virtuelle Java (JVM) et obtenir une visibilité en temps réel de tous les aspects d’une application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-113">Follow the steps below to install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application.</span></span>

1.  <span data-ttu-id="f5fe8-114">[Installez un JDK/JRE compatible avec Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="f5fe8-114">[Install a Zulu Mission Control compatible JDK/JRE](java-jdk-install.md).</span></span>

2.  <span data-ttu-id="f5fe8-115">Téléchargez Zulu Mission Control à partir du [site de téléchargement Azul](https://www.azul.com/products/zulu-mission-control/), choisissez la version appropriée pour votre système, enregistrez-la localement et accédez à ce répertoire.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-115">Download Zulu Mission Control from [the Azul download site](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

3.  <span data-ttu-id="f5fe8-116">Développez le fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-116">Expand the downloaded file.</span></span>

    <span data-ttu-id="f5fe8-117">**Linux :**</span><span class="sxs-lookup"><span data-stu-id="f5fe8-117">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="f5fe8-118">**Windows :**</span><span class="sxs-lookup"><span data-stu-id="f5fe8-118">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="f5fe8-119">**MacOS :**</span><span class="sxs-lookup"><span data-stu-id="f5fe8-119">**MacOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

4.  <span data-ttu-id="f5fe8-120">Démarrez votre application Java à l’aide de l’un des JDK compatibles.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-120">Start your Java application using one of the compatible JDKs.</span></span> <span data-ttu-id="f5fe8-121">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f5fe8-121">E.g.:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  <span data-ttu-id="f5fe8-122">Démarrez Zulu Mission Control</span><span class="sxs-lookup"><span data-stu-id="f5fe8-122">Start Zulu Mission Control</span></span>

    <span data-ttu-id="f5fe8-123">**Linux :**</span><span class="sxs-lookup"><span data-stu-id="f5fe8-123">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="f5fe8-124">**Windows :**</span><span class="sxs-lookup"><span data-stu-id="f5fe8-124">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="f5fe8-125">**MacOS :**</span><span class="sxs-lookup"><span data-stu-id="f5fe8-125">**MacOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

6.  <span data-ttu-id="f5fe8-126">Basculez l’installation de JVM pour Mission Control (facultatif)</span><span class="sxs-lookup"><span data-stu-id="f5fe8-126">Switch the JVM installation for Mission Control (Optional)</span></span>

    <span data-ttu-id="f5fe8-127">Sur Windows, *zmc.exe* utilisera l’installation de JVM par défaut configurée dans le Registre.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-127">On Windows, *zmc.exe* will use the default JVM installation configured in the registry.</span></span> <span data-ttu-id="f5fe8-128">Zulu Mission Control doit être lancé à partir d’un JDK complet afin de pouvoir détecter automatiquement les instances locales de JVM.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-128">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="f5fe8-129">S’il s’agit d’un environnement JRE, vous verrez l’avertissement ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f5fe8-129">If this is a JRE, you will see the warning below:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f5fe8-130">![Avertissement si l’installation de JDK est JRE uniquement](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="f5fe8-130">![Warning if JDK install is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="f5fe8-131">Pour changer la JVM utilisée par Mission Control, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5fe8-131">To change the JVM used by Mission Control, follow these steps:</span></span> 
    1.  <span data-ttu-id="f5fe8-132">Ouvrez le fichier de configuration *zmc.ini*, qui se trouve dans le même répertoire que *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-132">Open *zmc.ini* configuration file, located in the same directory as the *zmc.exe*</span></span>
    2.  <span data-ttu-id="f5fe8-133">Avant la ligne `-vmargs`, ajoutez deux lignes :</span><span class="sxs-lookup"><span data-stu-id="f5fe8-133">Before the line `-vmargs`, add two lines:</span></span>
        * <span data-ttu-id="f5fe8-134">Sur la première ligne, écrivez `–vm`.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-134">On the first line, write `–vm`</span></span>
        * <span data-ttu-id="f5fe8-135">Sur la deuxième ligne, écrivez le chemin de votre installation de JDK.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-135">On the second line, write the path to your JDK installation.</span></span> <span data-ttu-id="f5fe8-136">(Par exemple `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`.)</span><span class="sxs-lookup"><span data-stu-id="f5fe8-136">(For example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

7.  <span data-ttu-id="f5fe8-137">Recherchez la JVM exécutant votre application</span><span class="sxs-lookup"><span data-stu-id="f5fe8-137">Locate the JVM running your application</span></span>
    1.  <span data-ttu-id="f5fe8-138">Dans le volet supérieur gauche de la fenêtre Zulu Mission Control, cliquez sur l’onglet étiqueté **JVM Browser**.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-138">In the upper left pane of the Zulu Mission Control window click on the tab labelled **JVM Browser**.</span></span>
    2.  <span data-ttu-id="f5fe8-139">Sélectionnez et développez l’élément de liste en haut à gauche pour l’instance de JVM exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-139">Select and expand the list item in the upper left for your the JVM instance running your application.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f5fe8-140">![Développez l’élément de liste en haut à gauche de votre instance de JVM](../media/jdk/azul-jfr-2.png)</span><span class="sxs-lookup"><span data-stu-id="f5fe8-140">![Expand the list item in the upper-left for your JVM instance](../media/jdk/azul-jfr-2.png)</span></span>


8.  <span data-ttu-id="f5fe8-141">Démarrer un Flight Recording, si nécessaire</span><span class="sxs-lookup"><span data-stu-id="f5fe8-141">Start a Flight Recording, if necessary</span></span>
    1.  <span data-ttu-id="f5fe8-142">Si le Flight Recorder affiche « No Recordings » (Aucun enregistrement), démarrez-en un en cliquant sur la ligne Flight Recorder sous l’onglet du navigateur de JVM et en sélectionnant **Start Flight Recording...** .</span><span class="sxs-lookup"><span data-stu-id="f5fe8-142">If the Flight Recorder displays "No Recordings", start one by right-clicking on the Flight Recorder line in the JVM Browser tab and selecting **Start Flight Recording...**</span></span>
    2.  <span data-ttu-id="f5fe8-143">Sélectionnez un enregistrement de durée fixe ou un enregistrement continu, et une configuration de profilage (affinée) ou une configuration continue (charge réduite), puis cliquez sur **Finish**.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-143">Select either a fixed duration recording or a continuous recording, and either a Profiling configuration (fine-grained) or a Continuous configuration (lower overhead), then click **Finish**.</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f5fe8-144">![Démarrez un Flight Recording](../media/jdk/azul-jfr-3.png)</span><span class="sxs-lookup"><span data-stu-id="f5fe8-144">![Start a Flight Recording](../media/jdk/azul-jfr-3.png)</span></span>

9.  <span data-ttu-id="f5fe8-145">Videz le Flight Recording</span><span class="sxs-lookup"><span data-stu-id="f5fe8-145">Dump the Flight Recording</span></span>
    1.  <span data-ttu-id="f5fe8-146">Un Flight Recording doit apparaître sous la ligne Flight Recorder dans le navigateur de JVM.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-146">A Flight Recording should appear below the Flight Recorder line in the JVM Browser.</span></span> <span data-ttu-id="f5fe8-147">Cliquez avec le bouton droit sur la ligne représentant le Flight Recording et sélectionnez **Dump whole recording** (Vider tout l’enregistrement).</span><span class="sxs-lookup"><span data-stu-id="f5fe8-147">Right-click on the line representing the Flight Recording and select **Dump whole recording**.</span></span>
    2.  <span data-ttu-id="f5fe8-148">Un nouvel onglet s’affiche dans le grand volet sur le côté droit de la fenêtre Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-148">A new tab will appear in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="f5fe8-149">Ce volet représente le Flight Recording qui vient d’être supprimé de la JVM exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-149">This pane represents the Flight Recording just dumped from the JVM running your application.</span></span>

10. <span data-ttu-id="f5fe8-150">Examinez le Flight Recording à l’aide de Zulu Mission Control</span><span class="sxs-lookup"><span data-stu-id="f5fe8-150">Examine the Flight Recording using Zulu Mission Control</span></span>
    1.  <span data-ttu-id="f5fe8-151">S’il n’est pas activé, sélectionnez l’onglet **Outline** dans le volet gauche de la fenêtre Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-151">If not already activated, select the tab labelled **Outline** in the left pane of the Zulu Mission Control Window.</span></span> <span data-ttu-id="f5fe8-152">Cet onglet contient différentes vues des données recueillies dans le Flight Recording.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-152">This tab contains different views of the data collected in the Flight Recording.</span></span>
 
    > [!div class="mx-imgBorder"]
    <span data-ttu-id="f5fe8-153">![Passez en revue le Flight Recording](../media/jdk/azul-jfr-4.png)</span><span class="sxs-lookup"><span data-stu-id="f5fe8-153">![Review the Fliight Recording](../media/jdk/azul-jfr-4.png)</span></span>

## <a name="resources"></a><span data-ttu-id="f5fe8-154">Ressources</span><span class="sxs-lookup"><span data-stu-id="f5fe8-154">Resources</span></span>

<span data-ttu-id="f5fe8-155">Nous avons également réalisée une [vidéo de démonstration](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) commentée par Simon Ritter, directeur technique adjoint d’Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-155">We have also prepared a [demonstration video](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="f5fe8-156">Cette vidéo explique comment configurer et installer Flight Recorder et Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-156">The video walks you through the configuration and setup of both Flight Recorder and Zulu Mission Control.</span></span> <span data-ttu-id="f5fe8-157">La discussion sur Flight Recorder commence à 31:30.</span><span class="sxs-lookup"><span data-stu-id="f5fe8-157">The Flight Recorder discussion starts at 31:30.</span></span>

