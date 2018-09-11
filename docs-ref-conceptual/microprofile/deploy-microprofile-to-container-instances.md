---
title: Déployer une application MicroProfile sur le cloud avec Docker et Azure
description: Découvrez comment déployer une application MicroProfile sur le cloud à l’aide de Docker et d’Azure Container Instances.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 336af51bbdf5d2f843c3868ebc2358e128daaeaa
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324325"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a><span data-ttu-id="9d243-103">Déployer une application MicroProfile sur le cloud avec Docker et Azure</span><span class="sxs-lookup"><span data-stu-id="9d243-103">Deploy a MicroProfile application to the cloud with Docker and Azure</span></span>

<span data-ttu-id="9d243-104">Cet article explique comment placer une application [MicroProfile.io] dans un conteneur Docker et l’exécuter sur Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="9d243-104">This article demonstrates how to pack a [MicroProfile.io] application in a Docker container and run it on Azure Container Instances.</span></span>

> [!NOTE]
>
> <span data-ttu-id="9d243-105">Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image du conteneur Docker s’exécute automatiquement (c’est-à-dire qu’elle inclue le runtime).</span><span class="sxs-lookup"><span data-stu-id="9d243-105">This procedure works with any implementation of MicroProfile.io as long the Docker container image is self-executable (i.e. includes the runtime).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d243-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="9d243-106">Prerequisites</span></span>

<span data-ttu-id="9d243-107">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9d243-107">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="9d243-108">Abonnement Azure ; si vous ne disposez pas d’un abonnement Azure, vous pouvez vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="9d243-108">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9d243-109">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="9d243-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="9d243-110">Un [Kit de développement Java (JDK)] à jour, d’une version 1.8 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9d243-110">An up-to-date [Java Development Kit (JDK)], version 1.8 or later.</span></span>
* <span data-ttu-id="9d243-111">L’outil de génération [Maven] (version 3+) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="9d243-111">Apache's [Maven] build tool (version 3+).</span></span>
* <span data-ttu-id="9d243-112">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="9d243-112">A [Git] client.</span></span>

## <a name="microprofile-hello-azure-sample"></a><span data-ttu-id="9d243-113">Exemple MicroProfile Hello Azure</span><span class="sxs-lookup"><span data-stu-id="9d243-113">MicroProfile Hello Azure sample</span></span>

<span data-ttu-id="9d243-114">Pour cet article, nous utiliserons l’exemple de [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) :</span><span class="sxs-lookup"><span data-stu-id="9d243-114">For this article, we will use the [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) sample:</span></span>

### <a name="clone-build-and-run-locally"></a><span data-ttu-id="9d243-115">Cloner, générer, et exécuter en local</span><span class="sxs-lookup"><span data-stu-id="9d243-115">Clone, build, and run locally</span></span>

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

<span data-ttu-id="9d243-116">Vous pouvez tester l’application avec un appel `curl` ou en la consultant dans un [navigateur](http://localhost:8080/api/hello) :</span><span class="sxs-lookup"><span data-stu-id="9d243-116">You can test the application by calling `curl` or visiting through a [browser](http://localhost:8080/api/hello):</span></span>

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a><span data-ttu-id="9d243-117">Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="9d243-117">Deploy to Azure</span></span>

<span data-ttu-id="9d243-118">Chargeons à présent cette application sur le cloud avec les services [Azure Container Instances] et [Azure Container Registry].</span><span class="sxs-lookup"><span data-stu-id="9d243-118">Now let's bring this application to the cloud using [Azure Container Instances] and [Azure Container Registry] services.</span></span>

### <a name="build-a-docker-image"></a><span data-ttu-id="9d243-119">Générer une image Docker</span><span class="sxs-lookup"><span data-stu-id="9d243-119">Build a Docker image</span></span>

<span data-ttu-id="9d243-120">L’exemple de projet met à votre disposition un fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="9d243-120">The sample project already provides a Dockerfile you can use.</span></span> <span data-ttu-id="9d243-121">Vous n’avez pas besoin d’installer le logiciel Docker, étant donné que nous utiliserons la fonctionnalité de génération d’Azure Container Registry pour générer l’image dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="9d243-121">You don't need Docker installed though, as we will use Azure Container Registry Build feature to build the image in the cloud.</span></span>

<span data-ttu-id="9d243-122">Pour générer l’image et la rendre exécutable sur Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9d243-122">To build the image and be ready to run on Azure, you will have to follow these steps:</span></span>

1. <span data-ttu-id="9d243-123">Installer et se connecter avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9d243-123">Install and log in with Azure CLI</span></span>
1. <span data-ttu-id="9d243-124">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="9d243-124">Create an Azure Resource Group</span></span>
1. <span data-ttu-id="9d243-125">Créer un ACR (Azure Container Registry)</span><span class="sxs-lookup"><span data-stu-id="9d243-125">Create an Azure Container Registry (ACR)</span></span>
1. <span data-ttu-id="9d243-126">Créer l’image Docker</span><span class="sxs-lookup"><span data-stu-id="9d243-126">Build the Docker image</span></span>
1. <span data-ttu-id="9d243-127">Publier l’image de Docker sur l’ACR précédemment créé</span><span class="sxs-lookup"><span data-stu-id="9d243-127">Publish the Docker image to the ACR created before</span></span>
1. <span data-ttu-id="9d243-128">(Facultatif) Générer et publier sur ACR en une seule commande</span><span class="sxs-lookup"><span data-stu-id="9d243-128">(Optionally) Build and publish to ACR in one command</span></span>


#### <a name="set-up-azure-cli"></a><span data-ttu-id="9d243-129">Configuration de l’interface de ligne de commande Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9d243-129">Set up Azure CLI</span></span>

<span data-ttu-id="9d243-130">Vérifiez que vous disposez d’un abonnement Azure, que l’interface [Azure CLI est bien installée](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), et que vous êtes bien authentifié sur votre compte :</span><span class="sxs-lookup"><span data-stu-id="9d243-130">Make sure you have an Azure subscription, [Azure CLI installed](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), and that you are authenticated to your account:</span></span>

```bash
az login
```

#### <a name="create-a-resource-group"></a><span data-ttu-id="9d243-131">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="9d243-131">Create a Resource Group</span></span>

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a><span data-ttu-id="9d243-132">Créer une instance Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="9d243-132">Create an Azure Container Registry instance</span></span>

<span data-ttu-id="9d243-133">Cette commande devrait créer un registre de conteneurs global et unique utilisant un nom de base accompagné d’un nombre aléatoire.</span><span class="sxs-lookup"><span data-stu-id="9d243-133">This command will create a globally unique (hopefully) container registry using a basic name with a random number.</span></span>

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a><span data-ttu-id="9d243-134">Créer l’image Docker</span><span class="sxs-lookup"><span data-stu-id="9d243-134">Build the Docker image</span></span>

<span data-ttu-id="9d243-135">Même si vous pouvez facilement générer une image Docker locale à l’aide du logiciel Docker lui-même, vous pouvez également la générer dans le cloud, et ce pour diverses raisons :</span><span class="sxs-lookup"><span data-stu-id="9d243-135">While you can easily build the Docker image locally using Docker itself, you may want to consider building it in the Cloud for few reasons:</span></span>

1. <span data-ttu-id="9d243-136">Vous n’avez pas besoin d’installer Docker en local</span><span class="sxs-lookup"><span data-stu-id="9d243-136">No need to install Docker locally</span></span>
1. <span data-ttu-id="9d243-137">Le temps d’exécution est beaucoup plus rapide grâce à la génération à distance (à l’exception du temps de chargement en contexte)</span><span class="sxs-lookup"><span data-stu-id="9d243-137">Much faster since build will happen elsewhere (except for context upload time)</span></span>
1. <span data-ttu-id="9d243-138">Le traitement dans le cloud dispose d’une connexion internet plus rapide, optimisant ainsi la vitesse des téléchargements</span><span class="sxs-lookup"><span data-stu-id="9d243-138">Process in the Cloud has access to faster Internet, therefore faster downloads</span></span>
1. <span data-ttu-id="9d243-139">L’image est directement acheminée dans Container Registry</span><span class="sxs-lookup"><span data-stu-id="9d243-139">Image goes directly into the Container Registry</span></span>

<span data-ttu-id="9d243-140">Pour toutes ces raisons, nous générerons l’image à l’aide de la fonctionnalité de génération d’[Générer ACR] :</span><span class="sxs-lookup"><span data-stu-id="9d243-140">Because of these reasons, we will build the image using the [Azure Container Registry Build] feature:</span></span>

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a><span data-ttu-id="9d243-141">Déployer une image Docker depuis Azure Container Registry (ACR) vers Azure Container Instances (ACI)</span><span class="sxs-lookup"><span data-stu-id="9d243-141">Deploy Docker Image from Azure Container Registry (ACR) into Container Instances (ACI)</span></span>

<span data-ttu-id="9d243-142">Maintenant que l’image est disponible sur votre ACR, essayons d’envoyer et d’instancier une instance de conteneur sur ACI.</span><span class="sxs-lookup"><span data-stu-id="9d243-142">Now that the image is available on your ACR, let's push and instanciate a container instance on ACI.</span></span> <span data-ttu-id="9d243-143">Mais avant toute chose, il faut nous assurer que nous pouvons nous authentifier dans l’ACR :</span><span class="sxs-lookup"><span data-stu-id="9d243-143">But first, we need to make sure we can authenticate into the ACR:</span></span>

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a><span data-ttu-id="9d243-144">Testez votre application MicroProfile déployée</span><span class="sxs-lookup"><span data-stu-id="9d243-144">Test Your Deployed MicroProfile Application</span></span>

<span data-ttu-id="9d243-145">Votre application devrait à présent être fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="9d243-145">Your application should now be up and running.</span></span> <span data-ttu-id="9d243-146">Pour la tester depuis l’interface de ligne de commande, essayez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9d243-146">To test it from the command-line, try the following command:</span></span>

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

<span data-ttu-id="9d243-147">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9d243-147">Congratulations!</span></span> <span data-ttu-id="9d243-148">Vous avez généré et déployé avec succès une application MicroProfile comme conteneur Docker sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9d243-148">You have successfuly built and deployed a MicroProfile application as a Docker container onto Microsoft Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d243-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d243-149">Next steps</span></span>

<span data-ttu-id="9d243-150">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="9d243-150">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* [<span data-ttu-id="9d243-151">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="9d243-151">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

<!-- URL List -->

[Générer ACR]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[Azure Container Registry Build]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Kit de développement Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Java Development Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry