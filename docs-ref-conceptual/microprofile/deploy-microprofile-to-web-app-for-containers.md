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
ms.openlocfilehash: 1eb0e7d7a718a1c106adebbf89011f6e3fa1504e
ms.sourcegitcommit: c2019ba6da6c7c28b17b5a85f89e49bb5e570ba4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "44040247"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a><span data-ttu-id="1c4d7-103">Déployez un service MicroProfile en Java vers Azure Web App pour conteneurs</span><span class="sxs-lookup"><span data-stu-id="1c4d7-103">Deploy a Java-based MicroProfile service to Azure Web App for Containers</span></span>

<span data-ttu-id="1c4d7-104">MicroProfile est un bon outil de génération d’applications Java extrêmement petites, qui peuvent être déployées rapidement et facilement vers des services tels qu’[Azure Web App pour conteneurs](https://azure.microsoft.com/services/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-104">MicroProfile is a great way to build exceedingly tiny Java applications that can be quickly and easily deployed to services such as [Azure Web App for Containers](https://azure.microsoft.com/services/app-service/containers/).</span></span> <span data-ttu-id="1c4d7-105">Dans ce tutoriel, nous allons créer un simple microservice basé sur MicroProfile que nous allons intégrer à un conteneur Docker, déployer dans un [ACR](https://azure.microsoft.com/services/container-registry/), et finalement héberger à l’aide d’Azure Web App pour conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-105">In this tutorial we will create a simple MicroProfile-based microservice that is then containerized into a Docker container, deployed into an [Azure Container Registry](https://azure.microsoft.com/services/container-registry/), and then hosted using Azure Web App for Containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="1c4d7-106">Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image du conteneur Docker s’exécute automatiquement (c’est-à-dire qu’elle inclue le runtime).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-106">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

<span data-ttu-id="1c4d7-107">Concrètement, cet exemple utilise [Payara Micro](https://www.payara.fish/payara_micro) et la version [MicroProfile 1.3](https://microprofile.io/) pour créer un petit fichier Java au format war (5,085 Ko sur l’ordinateur d’origine), avant de l’empaqueter dans une image Docker (qui pèse approximativement 174 Mo).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-107">More concretely, this sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile 1.3](https://microprofile.io/) to create a tiny Java war file (5,085 bytes on the authors machine), and then packages it up into a Docker image (which is approximately 174 megabytes).</span></span> <span data-ttu-id="1c4d7-108">Cette image Docker contient tout le nécessaire pour un déploiement de cette application web entièrement conteneurisée.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-108">This Docker image contains everything necessary for a fully-containerised deployment of this webapp.</span></span>

<span data-ttu-id="1c4d7-109">Étant donné le fonctionnement de Docker, il est fréquent que l’image Docker 174 Mo n’aient pas besoin d’être intégralement redéployée à chaque modification du code source, Docker ne téléchargeant que les parties modifiées (réduisant ainsi drastiquement le volume de données).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-109">Because of the way Docker works, it is often the case that the entire 174 megabyte Docker image does not need to be redeployed whenever the application source code is changed, as Docker will only upload the differences (which is significantly smaller).</span></span> <span data-ttu-id="1c4d7-110">Ce mode de fonctionnement permet de créer très rapidement et très efficacement de nouvelles versions d’une application MicroProfile via un pipeline CI/CD, en réduisant les conflits et assurant des itérations de développement rapides.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-110">This makes the process of executing a new release of a MicroProfile application via a CI/CD pipeline extremely efficient and quick, reducing friction and enabling rapid development iteration.</span></span>

<span data-ttu-id="1c4d7-111">Dans ce tutoriel, nous allons tout d’abord créer et exécuter un code en local, puis le déployer en tant qu’application web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-111">We will work through this tutorial firstly by creating and running the code locally, and then we will deploy this as a web app on Azure.</span></span> <span data-ttu-id="1c4d7-112">Dans les deux cas, il nous faudra compter sur Docker pour réduire et standardiser nos tâches.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-112">In both cases we will depend on Docker to simplify and standardize our efforts.</span></span> <span data-ttu-id="1c4d7-113">Avant de commencer, nous allons créer un ACR afin d’y stocker nos conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-113">Before we begin, we will create an Azure Container Registry to store our Docker containers in.</span></span>

## <a name="creating-an-azure-container-registry"></a><span data-ttu-id="1c4d7-114">Création d’un ACR</span><span class="sxs-lookup"><span data-stu-id="1c4d7-114">Creating an Azure Container Registry</span></span>

<span data-ttu-id="1c4d7-115">Pour créer l’ACR, nous utiliserons le [Portail Azure](http://portal.azure.com), mais notez qu’il existe d’autres possibilités, telles que l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-115">We will use the [Azure Portal](http://portal.azure.com) for creating the Azure Container Registry, but note that there are alternate choices such as the Azure CLI.</span></span> <span data-ttu-id="1c4d7-116">Suivez les étapes ci-dessous pour créer un nouvel ACR :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-116">Follow the steps below to create a new Azure Container Registry:</span></span>

1. <span data-ttu-id="1c4d7-117">Connectez-vous au [Portail Azure](http://portal.azure.com), puis créez une ressource ACR.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-117">Log in to the [Azure Portal](http://portal.azure.com) and create a new Azure Container Registry resource.</span></span> <span data-ttu-id="1c4d7-118">Entrez un nom de registre (notez qu’il s’agit du nom devant être défini en tant que nom de propriété `docker.registry` dans `pom.xml`).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-118">Provide a registry name (note that this is the name that should be set as the `docker.registry` property in `pom.xml`).</span></span> <span data-ttu-id="1c4d7-119">Modifiez les paramètres par défaut à votre guise, puis cliquez sur Créer.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-119">Change the defaults as you wish, and then click 'create'.</span></span>

1. <span data-ttu-id="1c4d7-120">Une fois le registre de conteneurs en ligne (c’est-à-dire environ 30 secondes après avoir cliqué sur Créer), cliquez sur ce dernier, puis sur le lien Clés d’accès situé dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-120">Once the container registry is live (which is about 30 seconds after clicking 'create'), click on the container registry, and click on the 'Access keys' link in the left-menu area.</span></span> <span data-ttu-id="1c4d7-121">À cette étape, vous devez activer le paramètre Utilisateur administrateur, de sorte que nous puissions accéder à ce registre de conteneurs depuis nos ordinateurs (afin d’y envoyer des conteneurs Docker), mais aussi autoriser l’accès depuis l’instance Web App pour conteneurs Azure que nous configurerons prochainement.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-121">In here, you need to enable the 'admin user' setting, so that this container registry can be accessed from our machines (to push docker containers into), and also to enable access from the Azure Web Apps for Containers instance we will setup soon.</span></span>

1. <span data-ttu-id="1c4d7-122">Pendant que vous vous trouvez dans la section Clés d’accès, remarquez les valeurs `username` et `password`.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-122">Whilst you are in the 'Access keys' area, note the `username` and `password` values.</span></span> <span data-ttu-id="1c4d7-123">Nous allons les copier/coller dans notre fichier Maven global `settings.xml` (pour plus d’informations sur les paramètres Maven, reportez-vous au site web du [projet Apache Maven](https://maven.apache.org/settings.html)).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-123">We will copy / paste these into our global Maven `settings.xml` file  (for more information on Maven settings, refer to the [Apache Maven Project](https://maven.apache.org/settings.html) website).</span></span> <span data-ttu-id="1c4d7-124">Pour référence, voici une version masquée du fichier `${user.home}/.m2/settings.xml` située sur le système d’origine :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-124">For reference, here is an obfuscated version of the `${user.home}/.m2/settings.xml` file on the authors system:</span></span>

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

<span data-ttu-id="1c4d7-125">Cette étape terminée, nous pouvons passer à la génération et à l’exécution de notre application MicroProfile en local.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-125">Now that this is complete, we can move on with building and running our MicroProfile application locally.</span></span>

## <a name="creating-our-microprofile-application"></a><span data-ttu-id="1c4d7-126">Création de notre application MicroProfile</span><span class="sxs-lookup"><span data-stu-id="1c4d7-126">Creating our MicroProfile application</span></span>

<span data-ttu-id="1c4d7-127">Cet exemple se fonde sur un exemple d’application disponible sur GitHub, nous pouvons donc le cloner et parcourir le code pas à pas.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-127">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="1c4d7-128">Suivez les étapes ci-dessous pour cloner le code sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-128">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

<span data-ttu-id="1c4d7-129">Ce répertoire comprend un fichier `pom.xml` servant à spécifier le projet au format utilisé par l’outil de génération Maven.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-129">In this directory there is a `pom.xml` file that is used to specify the project in the format used by the Maven build tool.</span></span> <span data-ttu-id="1c4d7-130">Ce fichier peut être modifié pour s’adapter à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-130">This file can be edited to suit your own needs.</span></span> <span data-ttu-id="1c4d7-131">Les propriétés `docker.registry` et `docker.name` doivent notamment être remplacées par les propriétés `docker.registry` et `docker.name` créées lors de la configuration de l’ACR.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-131">In particular, the `docker.registry` and `docker.name` properties should be changed to the `docker.registry` and `docker.name` created when the Azure Container Registry was setup.</span></span>

<span data-ttu-id="1c4d7-132">Un autre fichier d’importance dans ce répertoire est le Dockerfile, qui est reproduit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-132">Another file of note in this directory is the Dockerfile, which is reproduced below:</span></span>

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

<span data-ttu-id="1c4d7-133">Ce Dockerfile crée simplement un conteneur Docker fondé sur un conteneur Docker Payara Micro, puis copie le fichier .war créé pendant la génération.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-133">This Dockerfile simply creates a new Docker container based on the Payara Micro Docker Container, and copies in the .war file that is created as part of our build process.</span></span> <span data-ttu-id="1c4d7-134">Il expose également le port 8080, de sorte que nous puissions accéder au service une fois opérationnel dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-134">It also exposes port 8080 so that we may access the service once it is up and running within a Docker container.</span></span>

<span data-ttu-id="1c4d7-135">En explorant plus en profondeur le répertoire `src`, nous découvrirons finalement la classe `Application` reproduite ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-135">Diving into the `src` directory, we will eventually discover the `Application` class reproduced below:</span></span>

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

<span data-ttu-id="1c4d7-136">L’annotation `@ApplicationPath("/api")` indique le point de terminaison de base de ce microservice. Autrement dit, les URL servant à accéder aux points de terminaison REST seront toutes précédées de la mention `/api`.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-136">The `@ApplicationPath("/api")` annotation specifies the base endpoint for this microservice - that is, that all endpoints will have `/api` preceed the rest of the URL required to access any specific REST endpoint.</span></span>

<span data-ttu-id="1c4d7-137">À l’intérieur du package `api` se trouve une classe intitulée `API`, contenant le code suivant :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-137">Inside the `api` package is a class named `API`, which contains the following code:</span></span>

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

<span data-ttu-id="1c4d7-138">En utilisant l’annotation `@Path("/helloworld")`, nous pouvons voir que ce point de terminaison REST, une fois combiné avec le `/api` spécifié dans la classe `Application` deviendra `/api/helloworld`.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-138">Through the use of the `@Path("/helloworld")` annotation, we can see that this REST endpoint, when combined with the `/api` specified in the `Application` class, will be `/api/helloworld`.</span></span> <span data-ttu-id="1c4d7-139">Lorsque ce point de terminaison est appelé à l’aide d’une requête HTTP GET, on peut remarquer que la méthode produit du texte/html, et qu’il s’agit en réalité d’une simple chaîne de caractères « Hello world! » codée en dur.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-139">When this endpoint is called using an HTTP GET request, we can see that the method will produce text/html, and in fact it is simply a hard-coded string "Hello, world!".</span></span>

<span data-ttu-id="1c4d7-140">Nous avons à présent exploré tout le code nécessaire à la création d’un microservice à l’aide de MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-140">We have now covered all the code required to create a microservice using MicroProfile.</span></span> <span data-ttu-id="1c4d7-141">Nous pouvons à présent utiliser Maven pour le générer puis le conteneuriser dans un conteneur Docker, avant de l’exécuter en local.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-141">We can now use Maven to build it, containerize it into a Docker container, and run it locally.</span></span> <span data-ttu-id="1c4d7-142">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-142">We can do that with the following steps:</span></span>

1. <span data-ttu-id="1c4d7-143">Exécutez `mvn clean package` et attendez que son exécution soit menée à bien.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-143">Run `mvn clean package` and wait until it successfully completes.</span></span>

1. <span data-ttu-id="1c4d7-144">Exécutez `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, par exemple `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, si votre paramètre `docker.registry` a la valeur `jogilescr.azurecr.io` et que votre paramètre `docker.name` a la valeur `samples/docker-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-144">Run `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, for example, `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, if your `docker.registry` is `jogilescr.azurecr.io` and `docker.name` is `samples/docker-helloworld`.</span></span>

1. <span data-ttu-id="1c4d7-145">Essayez d’accéder à [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) et à [http://localhost:8080/health](http://localhost:8080/health) dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-145">Try accessing [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) and [http://localhost:8080/health](http://localhost:8080/health) in your web browser.</span></span> <span data-ttu-id="1c4d7-146">Si vous voyez la réponse attendue « Hello, world! »,</span><span class="sxs-lookup"><span data-stu-id="1c4d7-146">If you see the expected "Hello, world!"</span></span> <span data-ttu-id="1c4d7-147">(et les informations sur l’intégrité du point de terminaison [/intégrité ](http://localhost:8080/health)), cela signifie que vous avez correctement déployé l’application MicroProfile sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-147">response (and health-related information for the [/health](http://localhost:8080/health) endpoint), you have successfully deployed the MicroProfile application on your local machine.</span></span>

## <a name="pushing-to-the-azure-container-registry"></a><span data-ttu-id="1c4d7-148">Envoi vers l’ACR</span><span class="sxs-lookup"><span data-stu-id="1c4d7-148">Pushing to the Azure Container Registry</span></span>

<span data-ttu-id="1c4d7-149">À présent que nous avons généré et exécuté avec succès notre application MicroProfile sur notre ordinateur local, l’étape suivante consiste à envoyer ce conteneur dans notre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-149">Now that we have successfully built and run our MicroProfile application on our local machine, the next step is to push this container into our container registry.</span></span> <span data-ttu-id="1c4d7-150">Nous utilisons dans ce tutoriel Azure Container Registry, mais l’opération fonctionnera avec n’importe quel registre de conteneurs (du moment que le fichier `pom.xml` est configuré pour pointer vers l’emplacement approprié).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-150">In this tutorial we are using the Azure Container Registry, but any container registry will work (as long as the `pom.xml` file is edited to point to the relevant location).</span></span>

1. <span data-ttu-id="1c4d7-151">Exécutez `mvn clean package` pour effacer, compiler et créer une image Docker locale.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-151">Run `mvn clean package` to clean, compile, and create a local docker image.</span></span>
2. <span data-ttu-id="1c4d7-152">Exécutez `mvn dockerfile:push` pour envoyer à Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-152">Run `mvn dockerfile:push` to push to the Azure Container Registry.</span></span>

<span data-ttu-id="1c4d7-153">À ce stade, votre image de conteneur Docker est chargée sur l’ACR, mais elle n’est pas encore exécutée étant donné qu’il nous faut la déployer dans une instance Azure Web App pour conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-153">At this stage you now have your docker container image uploaded to the Azure Container Registry, but it is not yet running as we now have to deploy it into an Azure Web App for Containers instance.</span></span> <span data-ttu-id="1c4d7-154">C’est ce que nous allons faire à présent.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-154">We will now do that.</span></span>

## <a name="creating-an-azure-web-app-for-containers-instance"></a><span data-ttu-id="1c4d7-155">Création d’une instance Web App pour conteneurs</span><span class="sxs-lookup"><span data-stu-id="1c4d7-155">Creating an Azure Web App for Containers instance</span></span>

1. <span data-ttu-id="1c4d7-156">Retournez sur le [Portail Azure](http://portal.azure.com) et créez une instance Web App pour conteneurs (sous l’en-tête « Web + Mobile » du menu).</span><span class="sxs-lookup"><span data-stu-id="1c4d7-156">Return to the [Azure Portal](http://portal.azure.com) and create a new Web App for Containers instance (located under the 'Web + Mobile' heading in the menu).</span></span> <span data-ttu-id="1c4d7-157">Quelques pointeurs :</span><span class="sxs-lookup"><span data-stu-id="1c4d7-157">A few pointers:</span></span>

   1. <span data-ttu-id="1c4d7-158">Le nom que vous renseignez ici correspondra à l’URL publique de l’application web (bien qu’un domaine personnalisé puisse être ajouté plus tard si besoin), il peut donc être judicieux de choisir un nom que vous retiendrez facilement.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-158">The name you specify here will be the public URL of the web app (although a custom domain can be added later if desired), so it is a good idea to pick a name that you can easily remember.</span></span>

   1. <span data-ttu-id="1c4d7-159">Lorsque vous vous rendez sur la section « Configurer un conteneur » vous pouvez sélectionner « Azure Container Registry » pour la « Source de l’image », puis sélectionner l’image appropriée à partir des listes déroulantes.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-159">When you get to the 'Configure container' section, you can select 'Azure Container Registry' for the 'Image source', and then select the correct image from the drop-down lists.</span></span>

   1. <span data-ttu-id="1c4d7-160">Vous n’avez pas besoin de spécifier de valeur dans le champ « Fichier de démarrage ».</span><span class="sxs-lookup"><span data-stu-id="1c4d7-160">You do not need to specify any value in the 'Startup File' field.</span></span>

1. <span data-ttu-id="1c4d7-161">Une fois l’instance créée (encore une fois, le processus est très rapide), cliquez dessus, puis sur l’élément de menu « Paramètres de l’application ».</span><span class="sxs-lookup"><span data-stu-id="1c4d7-161">Once the instance is created (again, it is very quick), click on it and then click on the 'Application Settings' menu item.</span></span> <span data-ttu-id="1c4d7-162">Ici, vous devez ajouter un nouveau paramètre d’application, avec la clé `WEBSITES_PORT` et la valeur `8080`.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-162">In here you need to add a new application setting, where the key is `WEBSITES_PORT` and the value is `8080`.</span></span> <span data-ttu-id="1c4d7-163">Cette opération communique à Azure le port que vous souhaitez exposer dans le conteneur, et il sera mappé au port externe 80.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-163">This tells Azure which port you want to expose in the container, and it will be mapped to port 80 externally.</span></span>

1. <span data-ttu-id="1c4d7-164">Facultativement, vous pouvez cliquer sur le lien « Conteneur Docker », et autoriser le « Déploiement continu ». Ce choix permet d’appliquer automatiquement toute mise à jour de l’image ACR dans l’instance Web App pour conteneurs.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-164">Optionally, click on the 'Docker Container' link, and enable 'Continuous Deployment', so that whenever you update the Azure Container Registry image it is automatically updated in the Azure Web App for Containers instance.</span></span>

1. <span data-ttu-id="1c4d7-165">Vous devriez pouvoir accéder aux instances hébergées sur Azure à `http://<appname>.azurewebsites.net/microprofile/api/helloworld` et `http://<appname>.azurewebsites.net/health`.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-165">You should be able to access the Azure-hosted instances at `http://<appname>.azurewebsites.net/microprofile/api/helloworld` and `http://<appname>.azurewebsites.net/health`.</span></span>

## <a name="summary"></a><span data-ttu-id="1c4d7-166">Résumé</span><span class="sxs-lookup"><span data-stu-id="1c4d7-166">Summary</span></span>

<span data-ttu-id="1c4d7-167">Au cours de ce tutoriel, nous avons vu les différentes étapes de création d’un microservice sur MicroProfile simple, que nous avons conteneurisé dans un conteneur Docker, exécuté en local et publié sur Azure.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-167">Through this tutorial we have stepped through the process of creating a simple MicroProfile-based microservice, containerized it into a Docker container, and we have run it locally and published it to Azure.</span></span> <span data-ttu-id="1c4d7-168">Nous n’aborderons pas dans ce tutoriel l’ajout de fonctionnalités plus utiles à notre microservice. Toutefois, vous trouverez de nombreux tutoriels et conseils relatifs à MicroProfile sur internet. Nous encourageons également les lecteurs à consulter [MicroProfile.io](https://microprofile.io/) afin d’accéder à davantage de contenu.</span><span class="sxs-lookup"><span data-stu-id="1c4d7-168">Extending our microservice to provide more useful functionality is outside the scope of this tutorial, but there is a wealth of tutorials and advice on MicroProfile on the internet, and readers are encouraged to review [MicroProfile.io](https://microprofile.io/) for more content.</span></span>
