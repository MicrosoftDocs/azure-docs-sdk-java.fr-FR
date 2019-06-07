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
# <a name="using-java-flight-recorder-jfr-and-mission-control"></a>Utilisation de Java Flight Recorder (JFR) et Mission Control

Zulu Mission Control est une build entièrement testée de JDK Mission Control, publiée en open source par Oracle en 2018 et gérée en tant que projet sous l’égide OpenJDK. Associé à Flight Recorder, Mission Control offre des fonctionnalités de gestion et de supervision interactives et à faible charge pour les charges de travail Java.

Zulu Mission Control est compatible avec les JDK/JRE suivants :

* Zulu 12.1 et ultérieur
* Zulu 11.0 et ultérieur
* Zulu 8u202 (8.36) et ultérieur
* Oracle OpenJDK 11+15 et ultérieur
* Oracle Java 11.0 et ultérieur
* Oracle Java 8.0 et ultérieur

Suivez les étapes ci-dessous pour installer Zulu Mission Control, vous connecter à une machine virtuelle Java (JVM) et obtenir une visibilité en temps réel de tous les aspects d’une application en cours d’exécution.

1.  [Installez un JDK/JRE compatible avec Zulu Mission Control](java-jdk-install.md).

2.  Téléchargez Zulu Mission Control à partir du [site de téléchargement Azul](https://www.azul.com/products/zulu-mission-control/), choisissez la version appropriée pour votre système, enregistrez-la localement et accédez à ce répertoire.

3.  Développez le fichier téléchargé.

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

4.  Démarrez votre application Java à l’aide de l’un des JDK compatibles. Par exemple :

    ```cli
    $JAVA_HOME/bin/java -jar MyApplication.jar
    ```

5.  Démarrez Zulu Mission Control

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

6.  Basculez l’installation de JVM pour Mission Control (facultatif)

    Sur Windows, *zmc.exe* utilisera l’installation de JVM par défaut configurée dans le Registre. Zulu Mission Control doit être lancé à partir d’un JDK complet afin de pouvoir détecter automatiquement les instances locales de JVM. S’il s’agit d’un environnement JRE, vous verrez l’avertissement ci-dessous :

    > [!div class="mx-imgBorder"]
    ![Avertissement si l’installation de JDK est JRE uniquement](../media/jdk/azul-jfr-1.png)

    Pour changer la JVM utilisée par Mission Control, effectuez les étapes suivantes : 
    1.  Ouvrez le fichier de configuration *zmc.ini*, qui se trouve dans le même répertoire que *zmc.exe*.
    2.  Avant la ligne `-vmargs`, ajoutez deux lignes :
        * Sur la première ligne, écrivez `–vm`.
        * Sur la deuxième ligne, écrivez le chemin de votre installation de JDK. (Par exemple `C:\Program Files\Java\jdk1.8.0_212\bin\javaw.exe`.)

7.  Recherchez la JVM exécutant votre application
    1.  Dans le volet supérieur gauche de la fenêtre Zulu Mission Control, cliquez sur l’onglet étiqueté **JVM Browser**.
    2.  Sélectionnez et développez l’élément de liste en haut à gauche pour l’instance de JVM exécutant votre application.

    > [!div class="mx-imgBorder"]
    ![Développez l’élément de liste en haut à gauche de votre instance de JVM](../media/jdk/azul-jfr-2.png)


8.  Démarrer un Flight Recording, si nécessaire
    1.  Si le Flight Recorder affiche « No Recordings » (Aucun enregistrement), démarrez-en un en cliquant sur la ligne Flight Recorder sous l’onglet du navigateur de JVM et en sélectionnant **Start Flight Recording...** .
    2.  Sélectionnez un enregistrement de durée fixe ou un enregistrement continu, et une configuration de profilage (affinée) ou une configuration continue (charge réduite), puis cliquez sur **Finish**.

    > [!div class="mx-imgBorder"]
    ![Démarrez un Flight Recording](../media/jdk/azul-jfr-3.png)

9.  Videz le Flight Recording
    1.  Un Flight Recording doit apparaître sous la ligne Flight Recorder dans le navigateur de JVM. Cliquez avec le bouton droit sur la ligne représentant le Flight Recording et sélectionnez **Dump whole recording** (Vider tout l’enregistrement).
    2.  Un nouvel onglet s’affiche dans le grand volet sur le côté droit de la fenêtre Zulu Mission Control. Ce volet représente le Flight Recording qui vient d’être supprimé de la JVM exécutant votre application.

10. Examinez le Flight Recording à l’aide de Zulu Mission Control
    1.  S’il n’est pas activé, sélectionnez l’onglet **Outline** dans le volet gauche de la fenêtre Zulu Mission Control. Cet onglet contient différentes vues des données recueillies dans le Flight Recording.
 
    > [!div class="mx-imgBorder"]
    ![Passez en revue le Flight Recording](../media/jdk/azul-jfr-4.png)

## <a name="resources"></a>Ressources

Nous avons également réalisée une [vidéo de démonstration](https://www.azul.com/presentation/azul-webinar-open-source-flight-recorder-and-mission-control-managing-and-measuring-openjdk-8-performance/) commentée par Simon Ritter, directeur technique adjoint d’Azul Systems. Cette vidéo explique comment configurer et installer Flight Recorder et Zulu Mission Control. La discussion sur Flight Recorder commence à 31:30.

