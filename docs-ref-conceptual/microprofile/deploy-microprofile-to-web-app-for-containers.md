---
title: Déployez un service MicroProfile en Java vers Azure Web App pour conteneurs
description: Découvrez comment déployer un service MicroProfile en utilisant Docker et Azure Web App pour conteneurs
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533599"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="cb28c-103">Déployez un service MicroProfile en Java vers Azure Web App pour conteneurs</span><span class="sxs-lookup"><span data-stu-id="cb28c-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="cb28c-104">MicroProfile est un bon outil de génération pour les applications Java extrêmement petites, qui peuvent être déployées rapidement et facilement sur des services tels qu’[Azure Web App pour conteneurs](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="cb28c-104">MicroProfile is a great way to build exceedingly small Java applications that you can quickly and easily deploy to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="cb28c-105">Dans ce tutoriel, vous allez créer un microservice simple basé sur MicroProfile que vous allez intégrer à un conteneur Docker, déployer sur une [instance de registre de conteurs Azure](https://azure.microsoft.com/services/container-registry/), et finalement héberger à l’aide d’Azure Web App pour conteneurs.</span><span class="sxs-lookup"><span data-stu-id="cb28c-105">In this tutorial, you create a simple, MicroProfile-based microservice that you containerize into a Docker container, deploy to an [Azure container registry instance](https://azure.microsoft.com/services/container-registry/), and then host by using Azure Web App for Containers.</span></span>

> [!NOTE]
> <span data-ttu-id="cb28c-106">Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image conteneur Docker est auto-exécutable (c’est-à-dire qu’elle inclut le runtime).</span><span class="sxs-lookup"><span data-stu-id="cb28c-106">This procedure works with any implementation of MicroProfile.io, as long the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

<span data-ttu-id="cb28c-107">Dans cet exemple, vous allez utiliser [Payara Micro](https://www.payara.fish/payara_micro) et [MicroProfile 1.3](https://microprofile.io/) pour créer un petit fichier WAR Java (d’environ 5 000 octets), puis pour l’empaqueter dans une image Docker d’environ 174 Mo.</span><span class="sxs-lookup"><span data-stu-id="cb28c-107">In this sample, you use [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a small (approximately 5,000 bytes) Java web application requirement (WAR) file, and then package it into a Docker image of approximately 174 megabytes (MB).</span></span> <span data-ttu-id="cb28c-108">L’image Docker contient tout le nécessaire pour un déploiement entièrement conteneurisé de l’application web.</span><span class="sxs-lookup"><span data-stu-id="cb28c-108">The Docker image contains everything necessary for a fully containerized deployment of the web app.</span></span>

<span data-ttu-id="cb28c-109">Il n’est pas nécessaire de redéployer l’intégralité d’une image Docker de 174 Mo à chaque changement du code source de l’application, car Docker charge uniquement les modifications (dont la taille est beaucoup plus petite).</span><span class="sxs-lookup"><span data-stu-id="cb28c-109">An entire 174 MB Docker image doesn't need to be redeployed whenever the application source code is changed, because Docker uploads only the differences (which are significantly smaller).</span></span> <span data-ttu-id="cb28c-110">Par conséquent, ce mode de fonctionnement permet de créer très rapidement et très efficacement de nouvelles versions d’une application MicroProfile via un pipeline CI/CD, ce qui réduit le nombre de conflits et garantit des itérations de développement rapides.</span><span class="sxs-lookup"><span data-stu-id="cb28c-110">Consequently, the process of executing a new release of a MicroProfile application via a CI/CD pipeline is extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="cb28c-111">Dans ce tutoriel, vous allez d’abord créer et exécuter du code localement, puis vous allez le déployer en tant qu’application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cb28c-111">You'll work through this tutorial by first creating and running the code locally and then deploying it as a web app on Azure.</span></span> <span data-ttu-id="cb28c-112">Durant ces deux phases, vous pouvez compter sur Docker pour simplifier et standardiser vos tâches.</span><span class="sxs-lookup"><span data-stu-id="cb28c-112">In both phases, you can depend on Docker to simplify and standardize your efforts.</span></span> <span data-ttu-id="cb28c-113">Avant de commencer, vous allez créer une instance de registre de conteneurs Azure pour stocker vos conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="cb28c-113">Before you begin, you'll create an Azure container registry instance for storing your Docker containers.</span></span>

## <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="cb28c-114">Créer une instance de registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="cb28c-114">Create an Azure container registry instance</span></span>

<span data-ttu-id="cb28c-115">Pour créer l’instance de registre de conteneurs Azure, vous pouvez utiliser le [portail Azure](http://portal.azure.com), mais vous avez aussi d’autres options comme Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cb28c-115">You can use the [Azure portal](http://portal.azure.com) to create the Azure container registry instance, but there are other choices also, such as the Azure CLI.</span></span> <span data-ttu-id="cb28c-116">Pour créer une instance de registre de conteneurs Azure, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb28c-116">To create a new Azure container registry instance, do the following:</span></span>

1. <span data-ttu-id="cb28c-117">Connectez-vous au [portail Azure](http://portal.azure.com), puis créez une ressource de registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="cb28c-117">Sign in to the [Azure portal](http://portal.azure.com) and create a new Azure container registry resource.</span></span> <span data-ttu-id="cb28c-118">Entrez un nom de registre (ce nom doit correspondre à la propriété `docker.registry` du fichier *pom.xml*).</span><span class="sxs-lookup"><span data-stu-id="cb28c-118">Provide a registry name (this name should be set as the `docker.registry` property in the *pom.xml* file).</span></span> <span data-ttu-id="cb28c-119">Changez les paramètres par défaut selon vos besoins, puis sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="cb28c-119">Change the defaults as you want, and then select **Create**.</span></span>

1. <span data-ttu-id="cb28c-120">Au bout d’environ 30 secondes, lorsque l’instance de registre de conteneurs est en ligne, sélectionnez-la, puis, dans le volet gauche, sélectionnez le lien **Clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="cb28c-120">In about 30 seconds, when the container registry instance is live, select the container registry instance and then, in the left pane, select the **Access keys** link.</span></span> 

    <span data-ttu-id="cb28c-121">Activez le paramètre *Utilisateur administrateur* afin de pouvoir accéder à l’instance de registre de conteneurs à partir de vos ordinateurs et pousser (push) les conteneurs Docker vers celle-ci.</span><span class="sxs-lookup"><span data-stu-id="cb28c-121">Be sure to enable the *admin user* setting, so that you can access this container registry instance from your machines and push Docker containers into it.</span></span> <span data-ttu-id="cb28c-122">Vous pouvez également y accéder à partir de l’instance Azure Web App pour conteneurs que vous allez bientôt configurer.</span><span class="sxs-lookup"><span data-stu-id="cb28c-122">Doing so also enables access from the Azure Web App for Containers instance that you'll set up soon.</span></span>

1. <span data-ttu-id="cb28c-123">Dans le volet **Clés d’accès**, copiez les valeurs de **nom d’utilisateur** et de **mot de passe**, puis collez-les dans le fichier global *settings.xml* Maven.</span><span class="sxs-lookup"><span data-stu-id="cb28c-123">In the **Access keys** pane, copy the **username** and **password** values and paste them into your global Maven *settings.xml* file.</span></span> <span data-ttu-id="cb28c-124">Pour plus d’informations sur les paramètres Maven, consultez le site web [Apache Maven Project](https://maven.apache.org/settings.html).</span><span class="sxs-lookup"><span data-stu-id="cb28c-124">For more information about Maven settings, go to the [Apache Maven Project](https://maven.apache.org/settings.html) website.</span></span> 

   <span data-ttu-id="cb28c-125">Pour référence, voici un exemple tiré du fichier *${user.home}/.m2/settings.xml* :</span><span class="sxs-lookup"><span data-stu-id="cb28c-125">For your reference, here's an example of the *${user.home}/.m2/settings.xml* file:</span></span>

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

<span data-ttu-id="cb28c-126">Maintenant que vous avez créé votre instance de registre de conteneurs, vous pouvez créer votre application MicroProfile et l’exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="cb28c-126">Now that you've created your container registry instance, you can move on to building and running your MicroProfile application locally.</span></span>

## <a name="create-your-microprofile-application"></a><span data-ttu-id="cb28c-127">Créer votre application MicroProfile</span><span class="sxs-lookup"><span data-stu-id="cb28c-127">Create your MicroProfile application</span></span>

<span data-ttu-id="cb28c-128">Cet exemple de code est basé sur un exemple d’application disponible sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb28c-128">This example code is based on a sample application that's available on GitHub.</span></span> <span data-ttu-id="cb28c-129">Pour cloner le code sur votre ordinateur, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb28c-129">To clone the code onto your machine, enter the following commands:</span></span>

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

<span data-ttu-id="cb28c-130">Ce répertoire contient un fichier *pom.xml* que vous pouvez utiliser pour spécifier le projet au format utilisé par l’outil de build Maven.</span><span class="sxs-lookup"><span data-stu-id="cb28c-130">This directory contains a *pom.xml* file that you use to specify the project in the format that's used by the Maven build tool.</span></span> <span data-ttu-id="cb28c-131">Vous pouvez modifier le fichier selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="cb28c-131">You can edit the file to suit your own needs.</span></span> <span data-ttu-id="cb28c-132">Les propriétés `docker.registry` et `docker.name` doivent notamment être remplacées par les propriétés `docker.registry` et `docker.name` qui ont été créées lors de la configuration de l’instance de registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="cb28c-132">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` properties that were created when you set up the Azure container registry instance.</span></span>

<span data-ttu-id="cb28c-133">Un autre fichier d’importance dans ce répertoire est le Dockerfile, qui est reproduit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="cb28c-133">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="cb28c-134">Le fichier Dockerfile crée un conteneur Docker qui est basé sur le conteneur Docker Payara Micro.</span><span class="sxs-lookup"><span data-stu-id="cb28c-134">The Dockerfile creates a new Docker container that's based on the Payara Micro Docker Container.</span></span> <span data-ttu-id="cb28c-135">Il est copié dans le fichier WAR qui a été créé lors du processus de build.</span><span class="sxs-lookup"><span data-stu-id="cb28c-135">It copies in the WAR file that was created as part of your build process.</span></span> <span data-ttu-id="cb28c-136">Il expose également le port 8080, ce qui permet d’accéder au service (une fois celui-ci opérationnel) à l’intérieur du conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="cb28c-136">It also exposes port 8080 so that you can access the service after it's up and running within a Docker container.</span></span>

<span data-ttu-id="cb28c-137">Lorsque vous ouvrirez le répertoire *src*, vous découvrirez la classe `Application` qui est reproduite ici :</span><span class="sxs-lookup"><span data-stu-id="cb28c-137">When you open the *src* directory, you'll eventually discover the `Application` class that's reproduced here:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="cb28c-138">L’annotation *@ApplicationPath("/api")* spécifie le point de terminaison de base de ce microservice.</span><span class="sxs-lookup"><span data-stu-id="cb28c-138">The *@ApplicationPath("/api")* annotation specifies the base endpoint for this microservice.</span></span> <span data-ttu-id="cb28c-139">Autrement dit, pour tous les points de terminaison, */api* précède le reste de l’URL qui est nécessaire pour accéder à n’importe quel point de terminaison REST.</span><span class="sxs-lookup"><span data-stu-id="cb28c-139">That is, for all endpoints, */api* precedes the rest of the URL that's required to access any specific REST endpoint.</span></span>

<span data-ttu-id="cb28c-140">À l’intérieur du package *api* se trouve une classe intitulée `API`, qui contient le code suivant :</span><span class="sxs-lookup"><span data-stu-id="cb28c-140">Inside the *api* package is a class named `API`, which contains the following code:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

<span data-ttu-id="cb28c-141">Avec l’annotation *@Path("/helloworld")* , vous voyez que ce point de terminaison REST, une fois associé au */api* spécifié dans la classe `Application`, devient */api/helloworld*.</span><span class="sxs-lookup"><span data-stu-id="cb28c-141">Through the use of the *@Path("/helloworld")* annotation, you can see that this REST endpoint, when it's combined with the */api* that's specified in the `Application` class, will be */api/helloworld*.</span></span> <span data-ttu-id="cb28c-142">Lorsque vous appelez ce point de terminaison à l’aide d’une requête HTTP GET, vous voyez que la méthode produit du texte (HTML), qui correspond en fait à la chaîne de caractères codée en dur « Hello world! ».</span><span class="sxs-lookup"><span data-stu-id="cb28c-142">When you call this endpoint by using an HTTP GET request, you can see that the method produces text/html and, in fact, it's simply a hard-coded string, "Hello, world!"</span></span>

<span data-ttu-id="cb28c-143">Jusqu’à maintenant, cet article a expliqué tout le code nécessaire à la création d’un microservice à l’aide de MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="cb28c-143">So far, this article has covered all the code that's required for you to create a microservice by using MicroProfile.</span></span> <span data-ttu-id="cb28c-144">Vous pouvez à présent utiliser Maven pour le générer puis le conteneuriser dans un conteneur Docker, avant de l’exécuter localement. Pour cela, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb28c-144">You can now use Maven to build it, containerize it into a Docker container, and run it locally by doing the following:</span></span>

1. <span data-ttu-id="cb28c-145">Exécutez `mvn clean package` et attendez la fin de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="cb28c-145">Run `mvn clean package`, and wait until it is complete.</span></span>

1. <span data-ttu-id="cb28c-146">Exécutez `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span><span class="sxs-lookup"><span data-stu-id="cb28c-146">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`.</span></span> <span data-ttu-id="cb28c-147">Par exemple, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, où *\<registre.docker>* est *jogilescr.azurecr.io* et *\<nom.docker>* est *samples/docker-helloworld*.</span><span class="sxs-lookup"><span data-stu-id="cb28c-147">For example, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, where *\<docker.registry>* is *jogilescr.azurecr.io* and *\<docker.name>* is *samples/docker-helloworld*.</span></span>

1. <span data-ttu-id="cb28c-148">Essayez d’accéder à [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) et à [http://localhost:8080/health](http://localhost:8080/health) dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="cb28c-148">Try to access [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="cb28c-149">Si vous voyez la réponse attendue « Hello, world! »,</span><span class="sxs-lookup"><span data-stu-id="cb28c-149">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="cb28c-150">(et les informations sur l’intégrité du point de terminaison [/health](http://localhost:8080/health)), cela signifie que l’application MicroProfile a été correctement déployée sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="cb28c-150">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you've successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="push-the-container-to-the-azure-container-registry-instance"></a><span data-ttu-id="cb28c-151">Poussée (push) du conteneur vers une instance de registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="cb28c-151">Push the container to the Azure container registry instance</span></span>

<span data-ttu-id="cb28c-152">À présent que vous avez généré et exécuté votre application MicroProfile sur votre ordinateur local, l’étape suivante consiste à pousser (push) ce conteneur vers votre instance de registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="cb28c-152">Now that you've successfully built and run your MicroProfile application on your local machine, push this container to your container registry instance.</span></span> 

> [!NOTE]
> <span data-ttu-id="cb28c-153">Même si cet article utilise une instance de registre de conteneurs Azure, vous pouvez utiliser n’importe quelle instance de registre de conteneurs, tant que le fichier *pom.xml* est modifié de façon à pointer vers l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="cb28c-153">Although this article uses an Azure container registry instance, any container registry instance should work, as long as the *pom.xml* file is edited to point to the relevant location.</span></span>

1. <span data-ttu-id="cb28c-154">Pour nettoyer, compiler et créer une image Docker locale, exécutez `mvn clean package`.</span><span class="sxs-lookup"><span data-stu-id="cb28c-154">To clean, compile, and create a local Docker image, run `mvn clean package`.</span></span>
2. <span data-ttu-id="cb28c-155">Pour pousser (push) le conteneur vers l’instance de registre de conteneurs Azure, exécutez `mvn dockerfile:push`.</span><span class="sxs-lookup"><span data-stu-id="cb28c-155">To push the container to the Azure container registry instance, run `mvn dockerfile:push`.</span></span>

<span data-ttu-id="cb28c-156">Votre image conteneur Docker est désormais chargée dans l’instance de registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="cb28c-156">You now have your Docker container image uploaded to the Azure container registry instance.</span></span> <span data-ttu-id="cb28c-157">Toutefois, son exécution n’a pas encore démarré.</span><span class="sxs-lookup"><span data-stu-id="cb28c-157">However, it's not yet running.</span></span> <span data-ttu-id="cb28c-158">Vous devez maintenant la déployer sur une instance Azure Web App pour conteneurs.</span><span class="sxs-lookup"><span data-stu-id="cb28c-158">You now have to deploy it to an Azure Web App for Containers instance.</span></span> 

## <a name="create-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="cb28c-159">Créer une instance Azure Web App pour conteneurs</span><span class="sxs-lookup"><span data-stu-id="cb28c-159">Create an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="cb28c-160">Dans le [portail Azure](http://portal.azure.com), dans le volet gauche, sélectionnez **Web + Mobile**, puis effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="cb28c-160">In the [Azure portal](http://portal.azure.com), in the left pane, select **Web + Mobile**, and then do the following:</span></span>

   <span data-ttu-id="cb28c-161">a.</span><span class="sxs-lookup"><span data-stu-id="cb28c-161">a.</span></span> <span data-ttu-id="cb28c-162">Spécifiez un nom.</span><span class="sxs-lookup"><span data-stu-id="cb28c-162">Specify a name.</span></span> <span data-ttu-id="cb28c-163">Le nom devient l’URL publique de l’application web. Il est donc préférable de choisir un nom facile à mémoriser.</span><span class="sxs-lookup"><span data-stu-id="cb28c-163">The name will become the public URL of the web app, so it's a good idea to pick a name that you can easily remember.</span></span> <span data-ttu-id="cb28c-164">Si vous le souhaitez, vous pourrez ajouter un nom de domaine personnalisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="cb28c-164">You can add a custom domain name later, if you want.</span></span>

   <span data-ttu-id="cb28c-165">b.</span><span class="sxs-lookup"><span data-stu-id="cb28c-165">b.</span></span> <span data-ttu-id="cb28c-166">Dans la section **Configurer le conteneur** située sous **Source d’image**, sélectionnez **Azure Container Registry**, puis, dans la liste déroulante, sélectionnez l’image dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="cb28c-166">In the **Configure container** section, under **Image source**, select **Azure Container Registry** and then, in the drop-down list, select the correct image.</span></span>

   <span data-ttu-id="cb28c-167">c.</span><span class="sxs-lookup"><span data-stu-id="cb28c-167">c.</span></span> <span data-ttu-id="cb28c-168">Vous n’avez pas besoin de spécifier de valeur dans le champ **Fichier de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="cb28c-168">You don't need to specify a value in the **Startup File** field.</span></span>

1. <span data-ttu-id="cb28c-169">Une fois que vous avez créé l’instance, sélectionnez-la, puis sélectionnez **Paramètres d’application**.</span><span class="sxs-lookup"><span data-stu-id="cb28c-169">After you've created the instance, select it, and then select **Application Settings**.</span></span> <span data-ttu-id="cb28c-170">Pour la **clé**, entrez **WEBSITES_PORT**, et pour la **valeur**, entrez **8080**.</span><span class="sxs-lookup"><span data-stu-id="cb28c-170">For **Key**, enter **WEBSITES_PORT**, and for **Value**, enter **8080**.</span></span> <span data-ttu-id="cb28c-171">Ces paramètres indiquent à Azure le port qui doit être exposé dans le conteneur et qui doit être mappé au port 80 en externe.</span><span class="sxs-lookup"><span data-stu-id="cb28c-171">These settings tell Azure which port to expose in the container and to map it to port 80 externally.</span></span>

1. <span data-ttu-id="cb28c-172">(Facultatif) Sélectionnez le lien **Conteneur Docker**, puis activez **Déploiement continu**.</span><span class="sxs-lookup"><span data-stu-id="cb28c-172">(Optional) Select the **Docker Container** link, and then enable **Continuous Deployment**.</span></span> <span data-ttu-id="cb28c-173">En procédant ainsi, chaque fois que vous mettez à jour l’image de l’instance de registre de conteneurs Azure, celle-ci est automatiquement mise à jour dans l’instance Azure Web App pour conteneurs.</span><span class="sxs-lookup"><span data-stu-id="cb28c-173">By doing so, whenever you update the Azure container registry instance image, it's automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="cb28c-174">Vous devriez pouvoir accéder aux instances hébergées dans Azure, aux emplacements `http://<appname>.azurewebsites.net/microprofile/api/helloworld` et `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="cb28c-174">You should now be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="cb28c-175">Résumé</span><span class="sxs-lookup"><span data-stu-id="cb28c-175">Summary</span></span>

<span data-ttu-id="cb28c-176">Dans ce tutoriel, vous avez vu les différentes étapes de création d’un microservice simple sur MicroProfile, vous avez conteneurisé ce microservice dans un conteneur Docker, puis vous l’avez exécuté localement et publié dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cb28c-176">In this tutorial, you've stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, run it locally, and published it to Azure.</span></span> <span data-ttu-id="cb28c-177">Vous pouvez étendre votre microservice pour ajouter d’autres fonctionnalités utiles.</span><span class="sxs-lookup"><span data-stu-id="cb28c-177">You can extend your microservice to provide additional useful functionality.</span></span> <span data-ttu-id="cb28c-178">Pour plus d’informations, consultez [MicroProfile.io](https://microprofile.io/).</span><span class="sxs-lookup"><span data-stu-id="cb28c-178">For more information, go to [MicroProfile.io](https://microprofile.io/).</span></span>
