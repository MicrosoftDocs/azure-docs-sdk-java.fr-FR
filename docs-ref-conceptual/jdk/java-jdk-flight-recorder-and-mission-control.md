---
title: Java Flight Recorder et Mission Control
description: Conseils d’utilisation de Java Flight Recorder et Mission Control afin de recueillir et d’examiner les données d’application.
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: 64f64f2e5891fccf9d62510f39bd99d73457d590
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533623"
---
# <a name="use-java-flight-recorder-and-mission-control"></a><span data-ttu-id="00c61-103">Utiliser Java Flight Recorder et Mission Control</span><span class="sxs-lookup"><span data-stu-id="00c61-103">Use Java Flight Recorder and Mission Control</span></span>

<span data-ttu-id="00c61-104">Zulu Mission Control est une build entièrement testée de JDK Mission Control, publiée en open source par Oracle en 2018 et gérée en tant que projet sous l’égide OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="00c61-104">Zulu Mission Control is a fully-tested build of JDK Mission Control, which was open-sourced by Oracle in 2018 and is managed as a project under the OpenJDK umbrella.</span></span> <span data-ttu-id="00c61-105">Associé à Java Flight Recorder (JFR), Mission Control offre des fonctionnalités de gestion et de supervision interactives et à faible charge pour les charges de travail Java.</span><span class="sxs-lookup"><span data-stu-id="00c61-105">Coupled with Java Flight Recorder (JFR), Mission Control delivers low-overhead, interactive monitoring and management capabilities for Java workloads.</span></span>

<span data-ttu-id="00c61-106">Zulu Mission Control est compatible avec les JDK (Java Development Kit) et les environnements JRE suivants :</span><span class="sxs-lookup"><span data-stu-id="00c61-106">Zulu Mission Control is compatible with the following Java Development Kits (JDKs) and Java Runtime Environments (JREs):</span></span>

* <span data-ttu-id="00c61-107">Zulu 12.1 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="00c61-107">Zulu 12.1 and later</span></span>
* <span data-ttu-id="00c61-108">Zulu 11.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="00c61-108">Zulu 11.0 and later</span></span>
* <span data-ttu-id="00c61-109">Zulu 8u202 (8.36) et ultérieur</span><span class="sxs-lookup"><span data-stu-id="00c61-109">Zulu 8u202 (8.36) and later</span></span>
* <span data-ttu-id="00c61-110">Oracle OpenJDK 11 et 15 (et ultérieur)</span><span class="sxs-lookup"><span data-stu-id="00c61-110">Oracle OpenJDK 11 and 15 and later</span></span>
* <span data-ttu-id="00c61-111">Oracle Java 11.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="00c61-111">Oracle Java 11.0 and later</span></span>
* <span data-ttu-id="00c61-112">Oracle Java 8.0 et ultérieur</span><span class="sxs-lookup"><span data-stu-id="00c61-112">Oracle Java 8.0 and later</span></span>

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a><span data-ttu-id="00c61-113">Installer Zulu Mission Control et se connecter à une machine virtuelle Java</span><span class="sxs-lookup"><span data-stu-id="00c61-113">Install Zulu Mission Control and connect to a JVM</span></span>

<span data-ttu-id="00c61-114">Pour installer Zulu Mission Control, vous connecter à une machine virtuelle Java (JVM) et obtenir une visibilité en temps réel de tous les aspects d’une application en cours d’exécution, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="00c61-114">To install Zulu Mission Control, connect to a Java Virtual Machine (JVM), and gain real-time visibility into all aspects of a running application, do the following:</span></span>

1.  <span data-ttu-id="00c61-115">[Installez un JDK et un JRE compatibles avec Zulu Mission Control](java-jdk-install.md).</span><span class="sxs-lookup"><span data-stu-id="00c61-115">[Install a Zulu Mission Control-compatible JDK and JRE](java-jdk-install.md).</span></span>

1.  <span data-ttu-id="00c61-116">[Téléchargez Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choisissez la version correspondant à votre système, enregistrez-la localement, puis accédez au répertoire.</span><span class="sxs-lookup"><span data-stu-id="00c61-116">[Download Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choose the appropriate version for your system, save it locally, and change to that directory.</span></span>

1.  <span data-ttu-id="00c61-117">Développez le fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="00c61-117">Expand the downloaded file.</span></span>

    <span data-ttu-id="00c61-118">**Linux :**</span><span class="sxs-lookup"><span data-stu-id="00c61-118">**Linux:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    <span data-ttu-id="00c61-119">**Windows :**</span><span class="sxs-lookup"><span data-stu-id="00c61-119">**Windows:**</span></span>

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    <span data-ttu-id="00c61-120">**MacOS :**</span><span class="sxs-lookup"><span data-stu-id="00c61-120">**macOS:**</span></span>

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  <span data-ttu-id="00c61-121">Démarrez votre application Java à l’aide de l’un des JDK compatibles.</span><span class="sxs-lookup"><span data-stu-id="00c61-121">Start your Java application by using one of the compatible JDKs.</span></span> <span data-ttu-id="00c61-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="00c61-122">For example:</span></span>

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  <span data-ttu-id="00c61-123">Démarrez Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="00c61-123">Start Zulu Mission Control.</span></span>

    <span data-ttu-id="00c61-124">**Linux :**</span><span class="sxs-lookup"><span data-stu-id="00c61-124">**Linux:**</span></span>

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    <span data-ttu-id="00c61-125">**Windows :**</span><span class="sxs-lookup"><span data-stu-id="00c61-125">**Windows:**</span></span>

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    <span data-ttu-id="00c61-126">**MacOS :**</span><span class="sxs-lookup"><span data-stu-id="00c61-126">**macOS:**</span></span>

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  <span data-ttu-id="00c61-127">(Facultatif) Basculez de l’installation de JVM vers Mission Control.</span><span class="sxs-lookup"><span data-stu-id="00c61-127">(Optional) Switch the JVM installation for Mission Control.</span></span>

    <span data-ttu-id="00c61-128">Sur les appareils Windows, *zmc.exe* utilisera l’installation de JVM par défaut qui est configurée dans le Registre.</span><span class="sxs-lookup"><span data-stu-id="00c61-128">On Windows devices, *zmc.exe* uses the default JVM installation that's configured in the registry.</span></span> <span data-ttu-id="00c61-129">Zulu Mission Control doit être lancé à partir d’un JDK complet afin de pouvoir détecter automatiquement les instances locales de JVM.</span><span class="sxs-lookup"><span data-stu-id="00c61-129">Zulu Mission Control must be launched from a full JDK to be able to detect local JVM instances automatically.</span></span> <span data-ttu-id="00c61-130">Si l’installation est un environnement JRE, aucune machine virtuelle Java n’est détectée et vous recevez l’avertissement suivant :</span><span class="sxs-lookup"><span data-stu-id="00c61-130">If the installation is a JRE, no JVM will be detected, and you will receive the following warning:</span></span>

    > [!div class="mx-imgBorder"]
    <span data-ttu-id="00c61-131">![Avertissement si l’installation de JDK est pour JRE uniquement](../media/jdk/azul-jfr-1.png)</span><span class="sxs-lookup"><span data-stu-id="00c61-131">![Warning if JDK installation is JRE-only](../media/jdk/azul-jfr-1.png)</span></span>

    <span data-ttu-id="00c61-132">Pour changer la machine virtuelle Java utilisée par Mission Control, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="00c61-132">To change the JVM that's used by Mission Control, do the following:</span></span> 

    <span data-ttu-id="00c61-133">a.</span><span class="sxs-lookup"><span data-stu-id="00c61-133">a.</span></span> <span data-ttu-id="00c61-134">Ouvrez le fichier de configuration *zmc.ini*, qui se trouve dans le même répertoire que le fichier *zmc.exe*.</span><span class="sxs-lookup"><span data-stu-id="00c61-134">Open the *zmc.ini* configuration file, which is in the same directory as the *zmc.exe* file.</span></span>

    <span data-ttu-id="00c61-135">b.</span><span class="sxs-lookup"><span data-stu-id="00c61-135">b.</span></span> <span data-ttu-id="00c61-136">Avant la ligne `-vmargs`, ajoutez deux lignes :</span><span class="sxs-lookup"><span data-stu-id="00c61-136">Before the line `-vmargs`, add two lines:</span></span>  

       * <span data-ttu-id="00c61-137">Sur la première ligne, entrez `–vm`.</span><span class="sxs-lookup"><span data-stu-id="00c61-137">On the first line, enter `–vm`.</span></span>  
       * <span data-ttu-id="00c61-138">Sur la deuxième ligne, entrez le chemin de votre installation de JDK (par exemple, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span><span class="sxs-lookup"><span data-stu-id="00c61-138">On the second line, enter the path to your JDK installation (for example, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).</span></span>

1.  <span data-ttu-id="00c61-139">Recherchez la machine virtuelle Java qui exécute votre application en effectuant les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="00c61-139">Locate the JVM that's running your application by doing the following:</span></span>

    <span data-ttu-id="00c61-140">a.</span><span class="sxs-lookup"><span data-stu-id="00c61-140">a.</span></span> <span data-ttu-id="00c61-141">Dans le volet gauche de la fenêtre Zulu Mission Control, sélectionnez l’onglet **JVM Browser**.</span><span class="sxs-lookup"><span data-stu-id="00c61-141">In the left pane of the Zulu Mission Control window, select the **JVM Browser** tab.</span></span>

    <span data-ttu-id="00c61-142">b.</span><span class="sxs-lookup"><span data-stu-id="00c61-142">b.</span></span> <span data-ttu-id="00c61-143">Dans la liste, sélectionnez et développez l’instance de machine virtuelle Java qui exécute votre application.</span><span class="sxs-lookup"><span data-stu-id="00c61-143">In the list, select and expand the JVM instance that's running your application.</span></span>

    ![L’instance de machine virtuelle Java dans la liste développée](../media/jdk/azul-jfr-2.png)


1.  <span data-ttu-id="00c61-145">Démarrez un Flight Recording, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="00c61-145">Start a flight recording, if necessary.</span></span>

    <span data-ttu-id="00c61-146">a.</span><span class="sxs-lookup"><span data-stu-id="00c61-146">a.</span></span> <span data-ttu-id="00c61-147">Dans le volet gauche, sous **Flight Recorder**, si le message *No Recordings* s’affiche, démarrez un enregistrement en double-cliquant sur **Flight Recorder**, puis en sélectionnant **Start Flight Recording**.</span><span class="sxs-lookup"><span data-stu-id="00c61-147">In the left pane, under **Flight Recorder**, if a *No Recordings* message is displayed, start a recording by right-clicking **Flight Recorder** and then selecting **Start Flight Recording**.</span></span>

    <span data-ttu-id="00c61-148">b.</span><span class="sxs-lookup"><span data-stu-id="00c61-148">b.</span></span> <span data-ttu-id="00c61-149">Sélectionnez un enregistrement de durée fixe (**Time fixed recording**) ou un enregistrement continu (**Continuous recording**), et une configuration de profilage affinée (**Profiling**) ou une configuration continue à charge réduite (**Continuous**), puis cliquez sur **Finish**.</span><span class="sxs-lookup"><span data-stu-id="00c61-149">Select either **Time fixed recording** or **Continuous recording**, and either a **Profiling** configuration (fine-grained) or a **Continuous** configuration (lower overhead), and then select **Finish**.</span></span>

    ![Démarrer un Flight Recording](../media/jdk/azul-jfr-3.png)

    <span data-ttu-id="00c61-151">Un Flight Recording doit apparaître sous la ligne **Flight Recorder** dans le navigateur de JVM.</span><span class="sxs-lookup"><span data-stu-id="00c61-151">A flight recording should appear below the **Flight Recorder** line in the JVM browser.</span></span>

1. <span data-ttu-id="00c61-152">Videz le Flight Recording.</span><span class="sxs-lookup"><span data-stu-id="00c61-152">Dump the flight recording.</span></span> <span data-ttu-id="00c61-153">Pour cela, cliquez avec le bouton droit sur la ligne représentant l’enregistrement Flight Recording, puis sélectionnez **Dump whole recording** (Vider tout l’enregistrement).</span><span class="sxs-lookup"><span data-stu-id="00c61-153">To do so, right-click the line that represents the flight recording, and then select **Dump whole recording**.</span></span>

    <span data-ttu-id="00c61-154">Un nouvel onglet s’affiche dans le grand volet sur le côté droit de la fenêtre Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="00c61-154">A new tab appears in the large pane on the right side of the Zulu Mission Control window.</span></span> <span data-ttu-id="00c61-155">Ce volet représente le Flight Recording qui vient d’être supprimé de la JVM qui exécute votre application.</span><span class="sxs-lookup"><span data-stu-id="00c61-155">This pane represents the flight recording that was just dumped from the JVM that's running your application.</span></span>

1. <span data-ttu-id="00c61-156">Examinez l’enregistrement Flight Recording à l’aide de Zulu Mission Control.</span><span class="sxs-lookup"><span data-stu-id="00c61-156">Examine the flight recording by using Zulu Mission Control.</span></span> <span data-ttu-id="00c61-157">Pour cela, dans le volet gauche de la fenêtre Zulu Mission Control, sélectionnez l’onglet **Outline** (Structure).</span><span class="sxs-lookup"><span data-stu-id="00c61-157">To do so, select the **Outline** tab in the left pane of the Zulu Mission Control window.</span></span> <span data-ttu-id="00c61-158">Cet onglet contient différentes vues des données recueillies dans le Flight Recording.</span><span class="sxs-lookup"><span data-stu-id="00c61-158">This tab displays various views of the data that's collected in the flight recording.</span></span>
 
    ![Passer en revue le Flight Recording](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a><span data-ttu-id="00c61-160">Ressources</span><span class="sxs-lookup"><span data-stu-id="00c61-160">Resources</span></span>

<span data-ttu-id="00c61-161">Pour plus d’informations, accédez au site d’Azul Systems et lisez [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span><span class="sxs-lookup"><span data-stu-id="00c61-161">To learn more, go to the Azul Systems site and view [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/).</span></span> <span data-ttu-id="00c61-162">La vidéo est commentée par Simon Ritter, directeur technique adjoint chez Azul Systems.</span><span class="sxs-lookup"><span data-stu-id="00c61-162">The video is narrated by Azul Systems Deputy CTO Simon Ritter.</span></span> <span data-ttu-id="00c61-163">La discussion sur Flight Recorder commence à 31:30.</span><span class="sxs-lookup"><span data-stu-id="00c61-163">The Flight Recorder discussion starts at 31:30.</span></span>

