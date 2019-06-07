---
title: Utiliser des images Docker avec un JDK pour le développement Java Azure
description: ''
author: bmitchell287
manager: douge
ms.author: brendm
ms.date: 4/9/2019
ms.devlang: java
ms.topic: conceptual
ms.openlocfilehash: ee8df2a08b23d090965cb42e2c15b934d4785e7c
ms.sourcegitcommit: 03379369346974c6e80f86e7129b885112b5c1a9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910232"
---
# <a name="use-docker-with-a-jdk-for-azure"></a>Utiliser Docker avec un JDK pour Azure 

Des images Docker préconfigurées pour Java 7, 8 et 11 sont disponibles dans [Docker Hub](https://hub.docker.com/_/microsoft-java-se).

Des images conteneur Docker certifiées pour Zulu JDK, JRE et JRE avec administration à distance sur plusieurs images de système d’exploitation de base sont disponibles dans Docker Hub :

* [JDK](https://hub.docker.com/_/microsoft-java-jdk)
* [JRE](https://hub.docker.com/_/microsoft-java-jre)
* [JRE avec administration à distance](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a>Exécution d’une image Docker

Les images docker peuvent être exécutées à l’aide de la syntaxe `$ docker run mcr.microsoft.com/java/jdk:tag java` comme indiqué dans l’exemple suivant.

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a>Création d’une image Docker

Vous pouvez créer une image à l’aide des images Docker Hub officielles de Microsoft comme indiqué dans les exemples suivants.

### <a name="create-a-docker-file"></a>Créer un fichier Docker

```cli
FROM mcr.microsoft.com/java/jdk:8u212-zulu-alpine 
  
RUN echo $' \
  
public class HelloWorld { \
   public static void main(String[] args) { \
      // Prints "Hello, World" in the terminal window. \
      System.out.println("Hello, World - From Microsoft Azure !!!"); \
   } \
}' > HelloWorld.java
  
RUN javac HelloWorld.java
  
CMD ["java", "HelloWorld"]
```

### <a name="build-a-docker-image"></a>Générer une image Docker

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a>Exécuter la nouvelle image

```cli
docker run hello-world
```

La sortie suivante s’affiche :

```output
Hello World - From Microsoft Azure !!!
```
