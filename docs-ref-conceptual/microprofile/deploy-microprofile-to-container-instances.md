---
title: Déployer une application MicroProfile dans le cloud avec Docker et Azure
description: Découvrez comment déployer une application MicroProfile dans le cloud à l’aide de Docker et d’Azure Container Instances.
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533601"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a><span data-ttu-id="9b60e-103">Déployer une application MicroProfile dans le cloud avec Docker et Azure</span><span class="sxs-lookup"><span data-stu-id="9b60e-103">Deploy a MicroProfile app to the cloud by using Docker and Azure</span></span>

<span data-ttu-id="9b60e-104">Cet article explique comment placer une application [MicroProfile.io] dans un conteneur Docker et l’exécuter sur Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="9b60e-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
> <span data-ttu-id="9b60e-105">Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image conteneur Docker est auto-exécutable (c’est-à-dire qu’elle inclut le runtime).</span><span class="sxs-lookup"><span data-stu-id="9b60e-105">This procedure works with any implementation of MicroProfile.io, as long as the Docker container image is self-executable (that is, the image includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b60e-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="9b60e-106">Prerequisites</span></span>

<span data-ttu-id="9b60e-107">Pour effectuer ce didacticiel, vous avez besoin de ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="9b60e-107">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="9b60e-108">Un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="9b60e-108">An Azure subscription.</span></span> <span data-ttu-id="9b60e-109">Si vous n’avez pas d’abonnement Azure, vous pouvez vous inscrire pour obtenir un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="9b60e-109">If you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9b60e-110">[Interface de ligne de commande Azure] installé.</span><span class="sxs-lookup"><span data-stu-id="9b60e-110">The [Azure CLI], installed.</span></span>
* <span data-ttu-id="9b60e-111">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9b60e-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="9b60e-112">Pour plus d’informations sur les JDK qui peuvent être utilisés lorsque vous développez dans Azure, consultez [Prise en charge à long terme de Java pour Azure et Azure Stack](https://aka.ms/azure-jdks).</span><span class="sxs-lookup"><span data-stu-id="9b60e-112">For more information about the JDKs that are available to use when you develop on Azure, see [Java long-term support for Azure and Azure Stack](https://aka.ms/azure-jdks).</span></span>
* <span data-ttu-id="9b60e-113">L’outil de génération [Apache Maven] (version 3 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="9b60e-113">The [Apache Maven] build tool (version 3 or later).</span></span>
* <span data-ttu-id="9b60e-114">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="9b60e-114">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="9b60e-115">Exemple MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="9b60e-115">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="9b60e-116">Pour cet article, vous allez utiliser l’exemple [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure).</span><span class="sxs-lookup"><span data-stu-id="9b60e-116">In this article, you use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample.</span></span> <span data-ttu-id="9b60e-117">Clonez, générez, puis exécutez-le localement en utilisant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9b60e-117">Clone, build, and run it locally by using the following commands:</span></span>

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

<span data-ttu-id="9b60e-118">Vous pouvez tester l’application en appelant `curl` ou à l’aide d’un [navigateur](http://localhost:8080/api/hello) :</span><span class="sxs-lookup"><span data-stu-id="9b60e-118">You can test the application by calling `curl` or by using a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="9b60e-119">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="9b60e-119">Deploy the app to Azure</span></span>

<span data-ttu-id="9b60e-120">Chargeons à présent cette application dans Azure avec les services [Azure Container Instances] et [Azure Container Registry].</span><span class="sxs-lookup"><span data-stu-id="9b60e-120">Now bring this application to Azure by using the [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="9b60e-121">Générer une image Docker</span><span class="sxs-lookup"><span data-stu-id="9b60e-121">Build a Docker image</span></span>

<span data-ttu-id="9b60e-122">L’exemple de projet met à votre disposition un fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="9b60e-122">The sample project provides a Dockerfile that you can use.</span></span> <span data-ttu-id="9b60e-123">Vous n’avez pas besoin d’installer le logiciel Docker, étant donné que nous utiliserons la fonctionnalité de génération d’Azure Container Registry pour générer l’image dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="9b60e-123">You don't need to have Docker installed, though, because you'll use the Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="9b60e-124">Pour créer l’image et préparer son exécution dans Azure, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9b60e-124">To build the image and prepare to run it on Azure, do the following:</span></span>

1. <span data-ttu-id="9b60e-125">Installez Azure CLI, puis connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="9b60e-125">Install and sign in to the Azure CLI.</span></span>
1. <span data-ttu-id="9b60e-126">Création d’un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="9b60e-126">Create an Azure resource group.</span></span>
1. <span data-ttu-id="9b60e-127">Créez une instance de registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="9b60e-127">Create an Azure container registry instance.</span></span>
1. <span data-ttu-id="9b60e-128">Générez une image Docker.</span><span class="sxs-lookup"><span data-stu-id="9b60e-128">Build a Docker image.</span></span>
1. <span data-ttu-id="9b60e-129">Publiez l’image Docker dans l’instance de registre de conteneurs créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="9b60e-129">Publish the Docker image to the previously created container registry instance.</span></span>
1. <span data-ttu-id="9b60e-130">(Facultatif) Générez et publiez l’image dans l’instance de registre de conteneurs à l’aide d’une seule commande.</span><span class="sxs-lookup"><span data-stu-id="9b60e-130">(Optional) Build and publish the image to the container registry instance in one command.</span></span>


#### <a name="set-up-the-azure-cli"></a><span data-ttu-id="9b60e-131">Configuration de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="9b60e-131">Set up the Azure CLI</span></span>

<span data-ttu-id="9b60e-132">Vérifiez que vous avez un abonnement Azure, que vous avez installé [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) et que vous êtes bien connecté à votre compte :</span><span class="sxs-lookup"><span data-stu-id="9b60e-132">Make sure that you have an Azure subscription, that you've installed [the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you're authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="9b60e-133">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9b60e-133">Create a resource group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a><span data-ttu-id="9b60e-134">Créer une instance de registre de conteneurs</span><span class="sxs-lookup"><span data-stu-id="9b60e-134">Create a container registry instance</span></span>

<span data-ttu-id="9b60e-135">Cette commande doit créer un registre de conteneurs global et unique avec un nom de base et un numéro aléatoire.</span><span class="sxs-lookup"><span data-stu-id="9b60e-135">This command should create a globally unique container registry instance with a basic name and a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="9b60e-136">Créer l’image Docker</span><span class="sxs-lookup"><span data-stu-id="9b60e-136">Build the Docker image</span></span>

<span data-ttu-id="9b60e-137">Même si vous pouvez facilement générer une image Docker locale à l’aide du logiciel Docker, vous pouvez également choisir de la générer dans le cloud, et ce pour diverses raisons :</span><span class="sxs-lookup"><span data-stu-id="9b60e-137">Although you can easily build the Docker image locally by using Docker itself, you might consider building it in the cloud for few reasons:</span></span>

* <span data-ttu-id="9b60e-138">Il n’est pas nécessaire d’installer Docker localement.</span><span class="sxs-lookup"><span data-stu-id="9b60e-138">You don't have to install Docker locally.</span></span>
* <span data-ttu-id="9b60e-139">Le temps d’exécution est beaucoup plus rapide grâce à la génération à distance (à l’exception du temps de chargement en contexte).</span><span class="sxs-lookup"><span data-stu-id="9b60e-139">It's much faster, because the build happens elsewhere (except for context upload time).</span></span>
* <span data-ttu-id="9b60e-140">Le traitement dans le cloud dispose d’une connexion Internet plus rapide, optimisant ainsi la vitesse des téléchargements.</span><span class="sxs-lookup"><span data-stu-id="9b60e-140">The process in the cloud has faster access to the internet and, therefore, faster downloads.</span></span>
* <span data-ttu-id="9b60e-141">L’image est directement acheminée vers l’instance de registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="9b60e-141">The image goes directly into the container registry instance.</span></span>

<span data-ttu-id="9b60e-142">Pour toutes ces raisons, vous allez générer l’image à l’aide de la fonctionnalité de génération d’[Générer ACR] :</span><span class="sxs-lookup"><span data-stu-id="9b60e-142">For these reasons, you build the image by using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a><span data-ttu-id="9b60e-143">Déployer l’image dans Container Instances à partir de l’instance de registre de conteneurs Azure</span><span class="sxs-lookup"><span data-stu-id="9b60e-143">Deploy the Docker image from the Azure container registry instance to Container Instances</span></span>

<span data-ttu-id="9b60e-144">Maintenant que l’image est disponible dans votre instance de registre de conteneurs, poussez (push) puis instanciez une instance de conteneur dans Container Instances.</span><span class="sxs-lookup"><span data-stu-id="9b60e-144">Now that the image is available on your container registry instance, push and instantiate a container instance on Container Instances.</span></span> <span data-ttu-id="9b60e-145">Mais d’abord, vérifiez que vous pouvez vous authentifier auprès de l’instance de registre de conteneurs :</span><span class="sxs-lookup"><span data-stu-id="9b60e-145">But first, make sure that you can authenticate into the container registry instance:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="9b60e-146">Tester l’application MicroProfile déployée</span><span class="sxs-lookup"><span data-stu-id="9b60e-146">Test your deployed MicroProfile application</span></span>

<span data-ttu-id="9b60e-147">Votre application devrait à présent être fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="9b60e-147">Your application should now be up and running.</span></span> <span data-ttu-id="9b60e-148">Pour la tester dans l’interface de ligne de commande, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9b60e-148">To test it from the command-line interface, use the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="9b60e-149">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9b60e-149">Congratulations!</span></span> <span data-ttu-id="9b60e-150">Vous avez généré une application MicroProfile comme conteneur Docker et l’avez déployée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9b60e-150">You've successfully built a MicroProfile application as a Docker container and deployed it to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b60e-151">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b60e-151">Next steps</span></span>

<span data-ttu-id="9b60e-152">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez :</span><span class="sxs-lookup"><span data-stu-id="9b60e-152">For more information about the various technologies discussed in this article, see:</span></span>

* [<span data-ttu-id="9b60e-153">Se connecter à Azure à partir d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b60e-153">Sign in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Générer ACR]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Interface de ligne de commande Azure]: /cli/azure/overview
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
