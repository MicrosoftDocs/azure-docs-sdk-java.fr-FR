---
title: Déployer une application Spring Boot sur Kubernetes dans Azure Kubernetes Service
description: Ce didacticiel vous guidera à travers les étapes à suivre pour déployer une application Spring Boot dans un cluster Kubernetes sur Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 9ab781d27e8968ab867efc65f3ac422ac6253a6a
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270856"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a><span data-ttu-id="613fd-103">Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="613fd-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Kubernetes Service</span></span>

<span data-ttu-id="613fd-104">**[Kubernetes]** et **[Docker]** sont des solutions open source qui aident les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications en cours d’exécution dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="613fd-104">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications running in containers.</span></span>

<span data-ttu-id="613fd-105">Ce didacticiel vous guide tout au long de la combinaison de ces deux technologies open source populaires pour développer et déployer une application Spring Boot sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="613fd-105">This tutorial walks you through combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="613fd-106">Plus précisément, *[Spring Boot]* sert au développement d’applications, *[Kubernetes]* au déploiement de conteneurs et [Azure Kubernetes Service (AKS)] à l’hébergement de votre application.</span><span class="sxs-lookup"><span data-stu-id="613fd-106">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Kubernetes Service (AKS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="613fd-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="613fd-107">Prerequisites</span></span>

* <span data-ttu-id="613fd-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="613fd-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="613fd-109">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="613fd-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="613fd-110">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="613fd-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="613fd-111">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="613fd-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="613fd-112">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="613fd-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="613fd-113">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="613fd-113">A [Git] client.</span></span>
* <span data-ttu-id="613fd-114">Un client [Docker].</span><span class="sxs-lookup"><span data-stu-id="613fd-114">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="613fd-115">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="613fd-115">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="613fd-116">Créer l’application web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="613fd-116">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="613fd-117">Les étapes suivantes vous guident à travers la création d’une application web Spring Boot et vous aident à effectuer le test en local.</span><span class="sxs-lookup"><span data-stu-id="613fd-117">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="613fd-118">Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="613fd-118">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="613fd-119">- ou -</span><span class="sxs-lookup"><span data-stu-id="613fd-119">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="613fd-120">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="613fd-120">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="613fd-121">Accédez au répertoire du projet terminé.</span><span class="sxs-lookup"><span data-stu-id="613fd-121">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="613fd-122">Utilisez Maven pour créer et exécuter l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="613fd-122">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="613fd-123">Testez l’application web en accédant à l’URL `http://localhost:8080`, ou avec la commande `curl` suivante :</span><span class="sxs-lookup"><span data-stu-id="613fd-123">Test the web app by browsing to `http://localhost:8080`, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="613fd-124">Vous devriez voir le message suivant : **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="613fd-124">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="613fd-126">Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="613fd-126">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="613fd-127">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="613fd-127">Open a command prompt.</span></span>

1. <span data-ttu-id="613fd-128">Connectez-vous à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="613fd-128">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="613fd-129">Choisissez votre abonnement Azure :</span><span class="sxs-lookup"><span data-stu-id="613fd-129">Choose your Azure Subscription:</span></span>
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. <span data-ttu-id="613fd-130">Créer un groupe de ressources pour les ressources Azure utilisées dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="613fd-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="613fd-131">Créez un registre de conteneurs Azure privé dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="613fd-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="613fd-132">Au cours des dernières étapes, le didacticiel envoie au registre l’exemple d’application en tant qu’image Docker.</span><span class="sxs-lookup"><span data-stu-id="613fd-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="613fd-133">Remplacez `wingtiptoysregistry` par un nom unique pour votre registre.</span><span class="sxs-lookup"><span data-stu-id="613fd-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a><span data-ttu-id="613fd-134">Envoyer l’application dans le registre de conteneurs via Jib</span><span class="sxs-lookup"><span data-stu-id="613fd-134">Push your app to the container registry via Jib</span></span>

1. <span data-ttu-id="613fd-135">Connectez-vous à votre instance Azure Container Registry depuis l’interface Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="613fd-135">Log in to your Azure Container Registry from the Azure CLI.</span></span>
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. <span data-ttu-id="613fd-136">Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple, « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou «  */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="613fd-136">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="613fd-137">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec le nom du registre de votre instance Azure Container Registry et la dernière version de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="613fd-137">Update the `<properties>` collection in the *pom.xml* file with the registry name for your Azure Container Registry and the latest version of [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="613fd-138">Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* pour que `<plugin>` contienne `jib-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="613fd-138">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the `jib-maven-plugin`.</span></span>

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
        </to>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="613fd-139">Pour créer l’image Docker et la pousser dans le registre, accédez au répertoire de projet terminé de votre application Spring Boot et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="613fd-139">Navigate to the completed project directory for your Spring Boot application and run the following command to build the image and push the image to the registry:</span></span>

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> <span data-ttu-id="613fd-140">En raison du problème de sécurité lié à Azure CLI et Azure Container Registry, les informations d’identification créées par `az acr login` sont valides pendant une heure. Si vous obtenez l’erreur *401 Non autorisé*, vous pouvez exécuter la commande `az acr login -n <your registry name>` pour vous réauthentifier.</span><span class="sxs-lookup"><span data-stu-id="613fd-140">Due to the security concern of Azure Cli and Azure Container Registry, the credential created by `az acr login` is valid for 1 hour, if you meet *401 Unauthorized* error, you can run the `az acr login -n <your registry name>` command again to reauthenticate.</span></span>
>

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a><span data-ttu-id="613fd-141">Créer un cluster Kubernetes sur AKS à l’aide d’Azure CLI</span><span class="sxs-lookup"><span data-stu-id="613fd-141">Create a Kubernetes Cluster on AKS using the Azure CLI</span></span>

1. <span data-ttu-id="613fd-142">Créez un cluster Kubernetes dans Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="613fd-142">Create a Kubernetes cluster in Azure Kubernetes Service.</span></span> <span data-ttu-id="613fd-143">La commande suivante crée un cluster *kubernetes* dans le groupe de ressources *wingtiptoys-kubernetes* avec *wingtiptoys-akscluster* comme nom de cluster, et *wingtiptoys-kubernetes* comme préfixe DNS :</span><span class="sxs-lookup"><span data-stu-id="613fd-143">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-akscluster* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   <span data-ttu-id="613fd-144">Cette commande peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="613fd-144">This command may take a while to complete.</span></span>

1. <span data-ttu-id="613fd-145">Lorsque vous utilisez Azure Container Registry (ACR) avec Azure Kubernetes Service (AKS), vous devez accorder l’accès de tirage d’Azure Kubernetes Service à Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="613fd-145">When you're using Azure Container Registry (ACR) with Azure Kubernetes Service (AKS), you need to grant Azure Kubernetes Service pull access to Azure Container Registry.</span></span> <span data-ttu-id="613fd-146">Azure crée un principal de service par défaut quand vous créez Azure Kubernetes Service.</span><span class="sxs-lookup"><span data-stu-id="613fd-146">Azure creates a default service principal when you are creating Azure Kubernetes Service.</span></span> <span data-ttu-id="613fd-147">Exécutez les scripts suivants dans bash ou Powershell pour accorder un accès à AKS à ACR et découvrez plus de détails dans [S’authentifier avec Azure Container Registry à partir d’Azure Kubernetes Service].</span><span class="sxs-lookup"><span data-stu-id="613fd-147">Please run the following scripts in bash or Powershell to grant AKS access to ACR, see more details at [Authenticate with Azure Container Registry from Azure Kubernetes Service].</span></span>

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  <span data-ttu-id="613fd-148">- ou -</span><span class="sxs-lookup"><span data-stu-id="613fd-148">-- or --</span></span>

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. <span data-ttu-id="613fd-149">Installez `kubectl` à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="613fd-149">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="613fd-150">Les utilisateurs Linux doivent ajouter cette commande en préfixe sur `sudo` car elle déploie l’interface de ligne de commande Kubernetes dans `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="613fd-150">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az aks install-cli
   ```

1. <span data-ttu-id="613fd-151">Téléchargez les informations de configuration du cluster afin de pouvoir gérer votre cluster à partir de l’interface web Kubernetes et de `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="613fd-151">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="613fd-152">Déployer l’image sur votre cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="613fd-152">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="613fd-153">Ce didacticiel déploie l’application à l’aide de `kubectl`, puis vous permet d’explorer le déploiement via l’interface web Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="613fd-153">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-kubectl"></a><span data-ttu-id="613fd-154">Déployer avec kubectl</span><span class="sxs-lookup"><span data-stu-id="613fd-154">Deploy with kubectl</span></span>

1. <span data-ttu-id="613fd-155">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="613fd-155">Open a command prompt.</span></span>

1. <span data-ttu-id="613fd-156">Exécutez votre conteneur dans le cluster Kubernetes en utilisant la commande `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="613fd-156">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="613fd-157">Donnez un nom de service à votre application dans Kubernetes et saisissez le nom complet de l’image.</span><span class="sxs-lookup"><span data-stu-id="613fd-157">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="613fd-158">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="613fd-158">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="613fd-159">Dans cette commande :</span><span class="sxs-lookup"><span data-stu-id="613fd-159">In this command:</span></span>

   * <span data-ttu-id="613fd-160">Le nom du conteneur `gs-spring-boot-docker` est spécifié directement après la commande `run`.</span><span class="sxs-lookup"><span data-stu-id="613fd-160">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="613fd-161">Le paramètre `--image` spécifie le nom combiné du nom de serveur et du nom de l’image en tant que `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="613fd-161">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="613fd-162">Exposez votre cluster Kubernetes en externe à l’aide de la commande `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="613fd-162">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="613fd-163">Spécifiez le nom de votre service, le port TCP destiné au public permettant d’accéder à l’application, et le port cible interne que votre application écoutera.</span><span class="sxs-lookup"><span data-stu-id="613fd-163">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="613fd-164">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="613fd-164">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="613fd-165">Dans cette commande :</span><span class="sxs-lookup"><span data-stu-id="613fd-165">In this command:</span></span>

   * <span data-ttu-id="613fd-166">Le nom du conteneur `gs-spring-boot-docker` est spécifié directement après la commande `expose deployment`.</span><span class="sxs-lookup"><span data-stu-id="613fd-166">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="613fd-167">Le paramètre `--type` spécifie que le cluster utilise l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="613fd-167">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="613fd-168">Le paramètre `--port` spécifie le port TCP 80 destiné au public.</span><span class="sxs-lookup"><span data-stu-id="613fd-168">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="613fd-169">Vous accédez à l’application sur ce port.</span><span class="sxs-lookup"><span data-stu-id="613fd-169">You access the app on this port.</span></span>

   * <span data-ttu-id="613fd-170">Le paramètre `--target-port` spécifie le port TCP interne 8080.</span><span class="sxs-lookup"><span data-stu-id="613fd-170">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="613fd-171">L’équilibreur de charge transmet les demandes à votre application sur ce port.</span><span class="sxs-lookup"><span data-stu-id="613fd-171">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="613fd-172">Une fois que l’application est déployée sur le cluster, faites la demande de l’adresse IP externe et ouvrez-la dans votre navigateur web :</span><span class="sxs-lookup"><span data-stu-id="613fd-172">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Parcourir l’exemple d’application sur Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="613fd-174">Déployer avec l’interface web de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="613fd-174">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="613fd-175">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="613fd-175">Open a command prompt.</span></span>

1. <span data-ttu-id="613fd-176">Ouvrez le site web de configuration de votre cluster Kubernetes dans votre navigateur par défaut :</span><span class="sxs-lookup"><span data-stu-id="613fd-176">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. <span data-ttu-id="613fd-177">Lorsque le site web de configuration Kubernetes s’ouvre dans votre navigateur, cliquez sur le lien afin de **déployer une application en conteneur** :</span><span class="sxs-lookup"><span data-stu-id="613fd-177">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Site web de configuration Kubernetes][KB01]

1. <span data-ttu-id="613fd-179">Lorsque la page **Création de ressources** s’affiche, spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="613fd-179">When the **Resource Creation** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="613fd-180">a.</span><span class="sxs-lookup"><span data-stu-id="613fd-180">a.</span></span> <span data-ttu-id="613fd-181">Sélectionnez **CRÉER UNE APPLICATION**.</span><span class="sxs-lookup"><span data-stu-id="613fd-181">Select **CREATE AN APP**.</span></span>

   <span data-ttu-id="613fd-182">b.</span><span class="sxs-lookup"><span data-stu-id="613fd-182">b.</span></span> <span data-ttu-id="613fd-183">Entrez votre nom d’application Spring Boot comme **Nom de l’application**, par exemple : « *gs-spring-boot-docker* ».</span><span class="sxs-lookup"><span data-stu-id="613fd-183">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="613fd-184">c.</span><span class="sxs-lookup"><span data-stu-id="613fd-184">c.</span></span> <span data-ttu-id="613fd-185">Entrez votre serveur de connexion et votre conteneur d’image vus précédemment dans la catégorie **Conteneur d’image**, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* ».</span><span class="sxs-lookup"><span data-stu-id="613fd-185">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="613fd-186">d.</span><span class="sxs-lookup"><span data-stu-id="613fd-186">d.</span></span> <span data-ttu-id="613fd-187">Choisissez **Externe** pour le **Service**.</span><span class="sxs-lookup"><span data-stu-id="613fd-187">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="613fd-188">e.</span><span class="sxs-lookup"><span data-stu-id="613fd-188">e.</span></span> <span data-ttu-id="613fd-189">Spécifiez les ports internes et externes dans les zones de texte **Port** et **Port cible**.</span><span class="sxs-lookup"><span data-stu-id="613fd-189">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Site web de configuration Kubernetes][KB02]


1. <span data-ttu-id="613fd-191">Cliquez sur **Déployer** pour déployer le conteneur.</span><span class="sxs-lookup"><span data-stu-id="613fd-191">Click **Deploy** to deploy the container.</span></span>

   ![Déploiement de Kubernetes][KB05]

1. <span data-ttu-id="613fd-193">Une fois que votre application a été déployée, vous verrez votre application Spring Boot répertoriée sous **Services**.</span><span class="sxs-lookup"><span data-stu-id="613fd-193">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Services Kubernetes][KB06]

1. <span data-ttu-id="613fd-195">Si vous cliquez sur le lien **Point de terminaison d’entrée**, vous pouvez voir votre application Spring Boot fonctionner sur Azure.</span><span class="sxs-lookup"><span data-stu-id="613fd-195">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Services Kubernetes][KB07]

   ![Parcourir l’exemple d’application sur Azure][SB02]

## <a name="next-steps"></a><span data-ttu-id="613fd-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="613fd-198">Next steps</span></span>

<span data-ttu-id="613fd-199">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="613fd-199">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="613fd-200">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="613fd-200">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="613fd-201">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="613fd-201">Additional Resources</span></span>

<span data-ttu-id="613fd-202">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez l’article suivant :</span><span class="sxs-lookup"><span data-stu-id="613fd-202">For more information about using Spring Boot on Azure, see the following article:</span></span>

* [<span data-ttu-id="613fd-203">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="613fd-203">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

<span data-ttu-id="613fd-204">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="613fd-204">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="613fd-205">Pour plus d’informations sur le déploiement d’une application Java sur Kubernetes avec Visual Studio Code, consultez les [didacticiels de Visual Studio Code Java].</span><span class="sxs-lookup"><span data-stu-id="613fd-205">For more information about deploying a Java application to Kubernetes with Visual Studio Code, see [Visual Studio Code Java Tutorials].</span></span>

<span data-ttu-id="613fd-206">Pour plus d’informations sur l’exemple de projet Spring Boot sur Docker, consultez [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="613fd-206">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="613fd-207">Les liens suivants fournissent des informations supplémentaires sur la création d’applications Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="613fd-207">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="613fd-208">Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="613fd-208">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="613fd-209">Les liens suivants fournissent des informations supplémentaires sur l’utilisation de Kubernetes avec Azure :</span><span class="sxs-lookup"><span data-stu-id="613fd-209">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="613fd-210">Démarrer avec un cluster Kubernetes dans Azure Kubernetes Service</span><span class="sxs-lookup"><span data-stu-id="613fd-210">Get started with a Kubernetes cluster in Azure Kubernetes Service</span></span>](/azure/aks/intro-kubernetes)

<span data-ttu-id="613fd-211">Plus d’informations sur l’utilisation d’interface de ligne de commande Kubernetes sont disponibles dans le guide d’utilisateur **kubectl** à l’adresse <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="613fd-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="613fd-212">Le site web Kubernetes comporte plusieurs articles traitant de l’utilisation d’images dans les registres privés :</span><span class="sxs-lookup"><span data-stu-id="613fd-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="613fd-213">[Configuration des comptes de service pour des pods]</span><span class="sxs-lookup"><span data-stu-id="613fd-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="613fd-214">[Espaces de noms]</span><span class="sxs-lookup"><span data-stu-id="613fd-214">[Namespaces]</span></span>
* <span data-ttu-id="613fd-215">[Extraction d’une image à partir d’un registre privé]</span><span class="sxs-lookup"><span data-stu-id="613fd-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="613fd-216">Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].</span><span class="sxs-lookup"><span data-stu-id="613fd-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<span data-ttu-id="613fd-217">Pour plus d’informations sur l’exécution et le débogage itératifs des conteneurs directement dans Azure Kubernetes Service (AKS) avec Azure Dev Spaces, consultez [Bien démarrer avec l’utilisation d’Azure Dev Spaces conjointement à Java]</span><span class="sxs-lookup"><span data-stu-id="613fd-217">For more information about iteratively running and debugging containers directly in Azure Kubernetes Service (AKS) with Azure Dev Spaces, see [Get started on Azure Dev Spaces with Java]</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Utilisation d’Azure DevOps et Java]: /azure/devops/java/
[Working with Azure DevOps and Java]: /azure/devops/java/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configuration des comptes de service pour des pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Espaces de noms]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extraction d’une image à partir d’un registre privé]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[S’authentifier avec Azure Container Registry à partir d’Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Authenticate with Azure Container Registry from Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Didacticiels de Visual Studio Code Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Visual Studio Code Java Tutorials]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Bien démarrer avec l’utilisation d’Azure Dev Spaces conjointement à Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
[Get started on Azure Dev Spaces with Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
