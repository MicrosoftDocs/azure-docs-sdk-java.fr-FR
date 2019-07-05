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
# <a name="use-java-flight-recorder-and-mission-control"></a>Utiliser Java Flight Recorder et Mission Control

Zulu Mission Control est une build entièrement testée de JDK Mission Control, publiée en open source par Oracle en 2018 et gérée en tant que projet sous l’égide OpenJDK. Associé à Java Flight Recorder (JFR), Mission Control offre des fonctionnalités de gestion et de supervision interactives et à faible charge pour les charges de travail Java.

Zulu Mission Control est compatible avec les JDK (Java Development Kit) et les environnements JRE suivants :

* Zulu 12.1 et ultérieur
* Zulu 11.0 et ultérieur
* Zulu 8u202 (8.36) et ultérieur
* Oracle OpenJDK 11 et 15 (et ultérieur)
* Oracle Java 11.0 et ultérieur
* Oracle Java 8.0 et ultérieur

## <a name="install-zulu-mission-control-and-connect-to-a-jvm"></a>Installer Zulu Mission Control et se connecter à une machine virtuelle Java

Pour installer Zulu Mission Control, vous connecter à une machine virtuelle Java (JVM) et obtenir une visibilité en temps réel de tous les aspects d’une application en cours d’exécution, effectuez les étapes suivantes :

1.  [Installez un JDK et un JRE compatibles avec Zulu Mission Control](java-jdk-install.md).

1.  [Téléchargez Zulu Mission Control](https://www.azul.com/products/zulu-mission-control/), choisissez la version correspondant à votre système, enregistrez-la localement, puis accédez au répertoire.

1.  Développez le fichier téléchargé.

    **Linux :**

    ```cli
    tar -xzvf zmc7.0.0-EA-linux_x64.tar.gz
    ```

    **Windows :**

    ```cli
    unzip -zxvf zmc7.0.0-EA-win_x64.zip 
    ```

    **MacOS :**

    ```cli
    tar -xzvf zmc7.0.0-EA-macosx_x64.tar.gz
    ```

1.  Démarrez votre application Java à l’aide de l’un des JDK compatibles. Par exemple :

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

1.  Démarrez Zulu Mission Control.

    **Linux :**

    ```cli
    zmc7.0.0-EA-linux_x64/zmc
    ```

    **Windows :**

    ```cli
    zmc7.0.0-EA-win_x64\zmc.exe 
    ```

    **MacOS :**

    ```cli
    zmc7.0.0-EA-macosx_x64/Zulu\ Mission\ Control.app/Contents/MacOS/zmc
    ```

1.  (Facultatif) Basculez de l’installation de JVM vers Mission Control.

    Sur les appareils Windows, *zmc.exe* utilisera l’installation de JVM par défaut qui est configurée dans le Registre. Zulu Mission Control doit être lancé à partir d’un JDK complet afin de pouvoir détecter automatiquement les instances locales de JVM. Si l’installation est un environnement JRE, aucune machine virtuelle Java n’est détectée et vous recevez l’avertissement suivant :

    > [!div class="mx-imgBorder"]
    ![Avertissement si l’installation de JDK est pour JRE uniquement](../media/jdk/azul-jfr-1.png)

    Pour changer la machine virtuelle Java utilisée par Mission Control, effectuez les étapes suivantes : 

    a. Ouvrez le fichier de configuration *zmc.ini*, qui se trouve dans le même répertoire que le fichier *zmc.exe*.

    b. Avant la ligne `-vmargs`, ajoutez deux lignes :  

       * Sur la première ligne, entrez `–vm`.  
       * Sur la deuxième ligne, entrez le chemin de votre installation de JDK (par exemple, `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`).

1.  Recherchez la machine virtuelle Java qui exécute votre application en effectuant les étapes suivantes :

    a. Dans le volet gauche de la fenêtre Zulu Mission Control, sélectionnez l’onglet **JVM Browser**.

    b. Dans la liste, sélectionnez et développez l’instance de machine virtuelle Java qui exécute votre application.

    ![L’instance de machine virtuelle Java dans la liste développée](../media/jdk/azul-jfr-2.png)


1.  Démarrez un Flight Recording, si nécessaire.

    a. Dans le volet gauche, sous **Flight Recorder**, si le message *No Recordings* s’affiche, démarrez un enregistrement en double-cliquant sur **Flight Recorder**, puis en sélectionnant **Start Flight Recording**.

    b. Sélectionnez un enregistrement de durée fixe (**Time fixed recording**) ou un enregistrement continu (**Continuous recording**), et une configuration de profilage affinée (**Profiling**) ou une configuration continue à charge réduite (**Continuous**), puis cliquez sur **Finish**.

    ![Démarrer un Flight Recording](../media/jdk/azul-jfr-3.png)

    Un Flight Recording doit apparaître sous la ligne **Flight Recorder** dans le navigateur de JVM.

1. Videz le Flight Recording. Pour cela, cliquez avec le bouton droit sur la ligne représentant l’enregistrement Flight Recording, puis sélectionnez **Dump whole recording** (Vider tout l’enregistrement).

    Un nouvel onglet s’affiche dans le grand volet sur le côté droit de la fenêtre Zulu Mission Control. Ce volet représente le Flight Recording qui vient d’être supprimé de la JVM qui exécute votre application.

1. Examinez l’enregistrement Flight Recording à l’aide de Zulu Mission Control. Pour cela, dans le volet gauche de la fenêtre Zulu Mission Control, sélectionnez l’onglet **Outline** (Structure). Cet onglet contient différentes vues des données recueillies dans le Flight Recording.
 
    ![Passer en revue le Flight Recording](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Ressources

Pour plus d’informations, accédez au site d’Azul Systems et lisez [Azul Webinar: Open Source Flight Recorder and Mission Control - Managing and Measuring OpenJDK 8 Performance](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/). La vidéo est commentée par Simon Ritter, directeur technique adjoint chez Azul Systems. La discussion sur Flight Recorder commence à 31:30.

