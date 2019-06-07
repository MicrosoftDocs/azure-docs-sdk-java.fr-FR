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
# <a name="use-docker-with-a-jdk-for-azure"></a><span data-ttu-id="13e21-102">Utiliser Docker avec un JDK pour Azure</span><span class="sxs-lookup"><span data-stu-id="13e21-102">Use Docker with a JDK for Azure</span></span> 

<span data-ttu-id="13e21-103">Des images Docker préconfigurées pour Java 7, 8 et 11 sont disponibles dans [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span><span class="sxs-lookup"><span data-stu-id="13e21-103">Pre-built Docker images for Java 7, 8, and 11 are available through [Docker Hub](https://hub.docker.com/_/microsoft-java-se).</span></span>

<span data-ttu-id="13e21-104">Des images conteneur Docker certifiées pour Zulu JDK, JRE et JRE avec administration à distance sur plusieurs images de système d’exploitation de base sont disponibles dans Docker Hub :</span><span class="sxs-lookup"><span data-stu-id="13e21-104">Certified Docker container images for Zulu JDK, JRE, and JRE-headless on multiple base OS images are available at Docker Hub:</span></span>

* [<span data-ttu-id="13e21-105">JDK</span><span class="sxs-lookup"><span data-stu-id="13e21-105">JDK</span></span>](https://hub.docker.com/_/microsoft-java-jdk)
* [<span data-ttu-id="13e21-106">JRE</span><span class="sxs-lookup"><span data-stu-id="13e21-106">JRE</span></span>](https://hub.docker.com/_/microsoft-java-jre)
* [<span data-ttu-id="13e21-107">JRE avec administration à distance</span><span class="sxs-lookup"><span data-stu-id="13e21-107">JRE-headless</span></span>](https://hub.docker.com/_/microsoft-java-jre-headless)

## <a name="running-a-docker-image"></a><span data-ttu-id="13e21-108">Exécution d’une image Docker</span><span class="sxs-lookup"><span data-stu-id="13e21-108">Running a Docker image</span></span>

<span data-ttu-id="13e21-109">Les images docker peuvent être exécutées à l’aide de la syntaxe `$ docker run mcr.microsoft.com/java/jdk:tag java` comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="13e21-109">Docker images can be run using the syntax `$ docker run mcr.microsoft.com/java/jdk:tag java` as shown in the following example.</span></span>

```cli
docker run mcr.microsoft.com/java/jdk:8u212-zulu-alpine java -version 
```

## <a name="creating-a-docker-image"></a><span data-ttu-id="13e21-110">Création d’une image Docker</span><span class="sxs-lookup"><span data-stu-id="13e21-110">Creating a Docker image</span></span>

<span data-ttu-id="13e21-111">Vous pouvez créer une image à l’aide des images Docker Hub officielles de Microsoft comme indiqué dans les exemples suivants.</span><span class="sxs-lookup"><span data-stu-id="13e21-111">You can create an image using Microsoft's official Docker Hub images as shown in the following examples.</span></span>

### <a name="create-a-docker-file"></a><span data-ttu-id="13e21-112">Créer un fichier Docker</span><span class="sxs-lookup"><span data-stu-id="13e21-112">Create a Docker file</span></span>

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

### <a name="build-a-docker-image"></a><span data-ttu-id="13e21-113">Générer une image Docker</span><span class="sxs-lookup"><span data-stu-id="13e21-113">Build a Docker image</span></span>

```cli
docker build -t hello-world
```

### <a name="run-the-new-image"></a><span data-ttu-id="13e21-114">Exécuter la nouvelle image</span><span class="sxs-lookup"><span data-stu-id="13e21-114">Run the new image</span></span>

```cli
docker run hello-world
```

<span data-ttu-id="13e21-115">La sortie suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="13e21-115">You will see the following output:</span></span>

```output
Hello World - From Microsoft Azure !!!
```
