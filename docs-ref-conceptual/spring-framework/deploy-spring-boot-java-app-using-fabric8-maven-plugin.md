---
title: Déployer une application Spring Boot à l’aide du plug-in Fabric8 Maven
description: Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot sur Microsoft Azure à l’aide du plug-in Fabric8 pour Apache Maven.
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: yuwzho;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: f05dca50f84b27f157892d63cda02286c6755795
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090812"
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a><span data-ttu-id="d6963-103">Déployer une application Spring Boot à l’aide du plug-in Fabric8 Maven</span><span class="sxs-lookup"><span data-stu-id="d6963-103">Deploy a Spring Boot app using the Fabric8 Maven Plugin</span></span>

<span data-ttu-id="d6963-104">**[Fabric8]** est une solution open source qui repose sur **[Kubernetes]** et qui aide les développeurs à créer des applications dans les conteneurs Linux.</span><span class="sxs-lookup"><span data-stu-id="d6963-104">**[Fabric8]** is an open-source solution that is built on **[Kubernetes]**, which helps developers create applications in Linux containers.</span></span>

<span data-ttu-id="d6963-105">Ce didacticiel vous guide dans l’utilisation du plug-in Fabric8 pour Maven pour développer et déployer une application sur un hôte Linux dans [Azure Container Service (AKS)].</span><span class="sxs-lookup"><span data-stu-id="d6963-105">This tutorial walks you through using the Fabric8 plugin for Maven to develop to deploy an application to a Linux host in the [Azure Container Service (AKS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6963-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="d6963-106">Prerequisites</span></span>

<span data-ttu-id="d6963-107">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d6963-107">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="d6963-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [Avantages pour les abonnés MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="d6963-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d6963-109">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="d6963-109">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="d6963-110">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="d6963-110">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="d6963-111">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="d6963-111">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="d6963-112">Un [Git].</span><span class="sxs-lookup"><span data-stu-id="d6963-112">A [Git] client.</span></span>
* <span data-ttu-id="d6963-113">Un [Docker].</span><span class="sxs-lookup"><span data-stu-id="d6963-113">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="d6963-114">En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.</span><span class="sxs-lookup"><span data-stu-id="d6963-114">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="d6963-115">Créer l’application web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="d6963-115">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="d6963-116">Les étapes suivantes vous guident à travers la création d’une application web Spring Boot et vous aident à effectuer le test en local.</span><span class="sxs-lookup"><span data-stu-id="d6963-116">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="d6963-117">Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-117">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   <span data-ttu-id="d6963-118">- ou -</span><span class="sxs-lookup"><span data-stu-id="d6963-118">-- or --</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. <span data-ttu-id="d6963-119">Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="d6963-119">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="d6963-120">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-120">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   <span data-ttu-id="d6963-121">- ou -</span><span class="sxs-lookup"><span data-stu-id="d6963-121">-- or --</span></span>
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. <span data-ttu-id="d6963-122">Utilisez Maven pour créer et exécuter l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="d6963-122">Use Maven to build and run the sample app.</span></span>
   ```shell
   mvn clean package spring-boot:run
   ```

1. <span data-ttu-id="d6963-123">Testez l’application web en accédant à l’URL http://localhost:8080, ou avec la commande `curl` suivante :</span><span class="sxs-lookup"><span data-stu-id="d6963-123">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="d6963-124">Vous devez normalement voir le message **Hello Docker World** s’afficher.</span><span class="sxs-lookup"><span data-stu-id="d6963-124">You should see a **Hello Docker World** message displayed.</span></span>

   ![Parcourir l’exemple d’application localement][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a><span data-ttu-id="d6963-126">Installer l’interface de ligne de commande Kubernetes et créer un groupe de ressources Azure à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6963-126">Install the Kubernetes command-line interface and create an Azure resource group using the Azure CLI</span></span>

1. <span data-ttu-id="d6963-127">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="d6963-127">Open a command prompt.</span></span>

1. <span data-ttu-id="d6963-128">Tapez la commande suivante pour vous connecter à votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="d6963-128">Type the following command to log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="d6963-129">Suivez les instructions pour terminer le processus de connexion</span><span class="sxs-lookup"><span data-stu-id="d6963-129">Follow the instructions to complete the login process</span></span>

   <span data-ttu-id="d6963-130">L’interface Azure CLI affiche une liste de vos comptes ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-130">The Azure CLI will display a list of your accounts; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. <span data-ttu-id="d6963-131">Si vous n’avez pas encore installé l’interface de ligne de commande Kubernetes (`kubectl`), vous pouvez l’installer à l’aide de l’interface Azure CLI ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-131">If you do not already have the Kubernetes command-line interface (`kubectl`) installed, you can install using the Azure CLI; for example:</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="d6963-132">Les utilisateurs Linux doivent ajouter cette commande en préfixe sur `sudo` car elle déploie l’interface de ligne de commande Kubernetes dans `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="d6963-132">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   >
   > <span data-ttu-id="d6963-133">Si `kubectl` est déjà installé et que votre version de `kubectl` est trop ancienne, un message d’erreur semblable à l’exemple suivant peut s’afficher lorsque vous tentez d’effectuer les étapes indiquées plus loin dans cet article :</span><span class="sxs-lookup"><span data-stu-id="d6963-133">If you already have `kubectl`) installed and your version of `kubectl` is too old, you may see an error message similar to the following example when you attempt to complete the steps listed later in this article:</span></span>
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > <span data-ttu-id="d6963-134">Dans ce cas, vous devrez réinstaller `kubectl` pour mettre à jour votre version.</span><span class="sxs-lookup"><span data-stu-id="d6963-134">If this happens, you will need to reinstall `kubectl` to update your version.</span></span>
   >

1. <span data-ttu-id="d6963-135">Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans ce didacticiel ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-135">Create a resource group for the Azure resources that you will use in this tutorial; for example:</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   <span data-ttu-id="d6963-136">Où :</span><span class="sxs-lookup"><span data-stu-id="d6963-136">Where:</span></span>  
      * <span data-ttu-id="d6963-137">*wingtiptoys-kubernetes* est un nom unique pour votre groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="d6963-137">*wingtiptoys-kubernetes* is a unique name for your resource group</span></span>  
      * <span data-ttu-id="d6963-138">*westeurope* est un emplacement géographique approprié pour votre application</span><span class="sxs-lookup"><span data-stu-id="d6963-138">*westeurope* is an appropriate geographic location for your application</span></span>  

   <span data-ttu-id="d6963-139">L’interface Azure CLI affiche les résultats de la création de votre groupe de ressources ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-139">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a><span data-ttu-id="d6963-140">Créer un cluster Kubernetes à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6963-140">Create a Kubernetes cluster using the Azure CLI</span></span>

1. <span data-ttu-id="d6963-141">Créez un cluster Kubernetes dans votre nouveau groupe de ressources ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-141">Create a Kubernetes cluster in your new resource group; for example:</span></span>  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   <span data-ttu-id="d6963-142">Où :</span><span class="sxs-lookup"><span data-stu-id="d6963-142">Where:</span></span>  
      * <span data-ttu-id="d6963-143">*wingtiptoys-kubernetes* est le nom de votre groupe de ressources tel que spécifié plus haut dans cet article</span><span class="sxs-lookup"><span data-stu-id="d6963-143">*wingtiptoys-kubernetes* is the name of your resource group from earlier in this article</span></span>  
      * <span data-ttu-id="d6963-144">*wingtiptoys-kubernetes* est un nom unique pour votre cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d6963-144">*wingtiptoys-cluster* is a unique name for your Kubernetes cluster</span></span>
      * <span data-ttu-id="d6963-145">*wingtiptoys* est un nom DNS unique pour votre application</span><span class="sxs-lookup"><span data-stu-id="d6963-145">*wingtiptoys* is a unique name DNS name for your application</span></span>

   <span data-ttu-id="d6963-146">L’interface Azure CLI affiche les résultats de la création de votre cluster ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-146">The Azure CLI will display the results of your cluster creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. <span data-ttu-id="d6963-147">Téléchargez vos informations d’identification pour votre nouveau cluster Kubernetes ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-147">Download your credentials for your new Kubernetes cluster; for example:</span></span>  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. <span data-ttu-id="d6963-148">Vérifiez votre connexion avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d6963-148">Verify your connection with the following command:</span></span>
   ```shell 
   kubectl get nodes
   ```

   <span data-ttu-id="d6963-149">Vous devez voir une liste de nœuds et d’états semblable à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d6963-149">You should see a list of nodes and statuses like the following example:</span></span>

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="d6963-150">Créer un registre de conteneurs Azure (Azure Container Registry) privé à l’aide de l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6963-150">Create a private Azure container registry using the Azure CLI</span></span>

1. <span data-ttu-id="d6963-151">Créez un registre de conteneurs Azure privé dans votre groupe de ressources pour héberger votre image Docker ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-151">Create a private Azure container registry in your resource group to host your Docker image; for example:</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="d6963-152">Où :</span><span class="sxs-lookup"><span data-stu-id="d6963-152">Where:</span></span>

   | <span data-ttu-id="d6963-153">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d6963-153">Parameter</span></span> | <span data-ttu-id="d6963-154">Description</span><span class="sxs-lookup"><span data-stu-id="d6963-154">Description</span></span> |
   |---|---|
   | `wingtiptoys-kubernetes` | <span data-ttu-id="d6963-155">Spécifie le nom de votre groupe de ressources tel que spécifié plus haut dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d6963-155">Specifies the name of your resource group from earlier in this article.</span></span> |
   | `wingtiptoysregistry` | <span data-ttu-id="d6963-156">Spécifie un nom unique pour votre registre privée.</span><span class="sxs-lookup"><span data-stu-id="d6963-156">Specifies a unique name for your private registry.</span></span> |
   | `westeurope` | <span data-ttu-id="d6963-157">Spécifie un emplacement géographique approprié pour votre application.</span><span class="sxs-lookup"><span data-stu-id="d6963-157">Specifies an appropriate geographic location for your application.</span></span> |

   <span data-ttu-id="d6963-158">L’interface Azure CLI affiche les résultats de la création de votre registre ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-158">The Azure CLI will display the results of your registry creation; for example:</span></span>  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

2. <span data-ttu-id="d6963-159">Récupérez le mot de passe pour votre registre de conteneurs à partir de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="d6963-159">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   <span data-ttu-id="d6963-160">L’interface Azure CLI affiche le mot de passe de votre registre ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-160">The Azure CLI will display the password for your registry; for example:</span></span>  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

3. <span data-ttu-id="d6963-161">Accédez au répertoire de configuration de l’installation de Maven (par défaut sous ~/.m2/ ou C:\Users\username\.m2) et ouvrez le fichier *settings.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d6963-161">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

4. <span data-ttu-id="d6963-162">Ajoutez l’URL, votre nom d’utilisateur et votre mot de passe de votre Azure Container Registry à une nouvelle collection `<server>` dans le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="d6963-162">Add your Azure Container Registry URL, username and password to a new `<server>` collection in the *settings.xml* file.</span></span>
   <span data-ttu-id="d6963-163">Le `id` et `username` correspondent au nom du registre.</span><span class="sxs-lookup"><span data-stu-id="d6963-163">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="d6963-164">Utilisez la valeur `password` de la commande précédente (sans guillemets).</span><span class="sxs-lookup"><span data-stu-id="d6963-164">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

5. <span data-ttu-id="d6963-165">Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou «  */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d6963-165">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

6. <span data-ttu-id="d6963-166">Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion de votre registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="d6963-166">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

7. <span data-ttu-id="d6963-167">Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* de manière que `<plugin>` contienne l’adresse du serveur de connexion et le nom de registre de votre registre de conteneurs Azure.</span><span class="sxs-lookup"><span data-stu-id="d6963-167">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
     <groupId>com.spotify</groupId>
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

8. <span data-ttu-id="d6963-168">Pour créer le conteneur Docker et envoyer l’image dans votre registre, accédez au répertoire de projet terminé de votre application Spring Boot et exécutez la commande Maven suivante :</span><span class="sxs-lookup"><span data-stu-id="d6963-168">Navigate to the completed project directory for your Spring Boot application, and run the following Maven command to build the Docker container and push the image to your registry:</span></span>

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   <span data-ttu-id="d6963-169">Maven affiche les résultats de la génération ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-169">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a><span data-ttu-id="d6963-170">Configurer votre application Spring Boot pour utiliser le plug-in Fabric8 Maven</span><span class="sxs-lookup"><span data-stu-id="d6963-170">Configure your Spring Boot app to use the Fabric8 Maven plugin</span></span>

1. <span data-ttu-id="d6963-171">Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou «  */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d6963-171">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="d6963-172">Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* pour ajouter le plug-in Fabric8 Maven :</span><span class="sxs-lookup"><span data-stu-id="d6963-172">Update the `<plugins>` collection in the *pom.xml* file to add the Fabric8 Maven plugin:</span></span>

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. <span data-ttu-id="d6963-173">Accédez au répertoire source principal de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete\src\main* » ou «  */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main* ») et créez un dossier nommé « *fabric8* ».</span><span class="sxs-lookup"><span data-stu-id="d6963-173">Navigate to the main source directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete\src\main*" or "*/home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main*"), and create a new folder named "*fabric8*".</span></span>

1. <span data-ttu-id="d6963-174">Créez trois fichiers fragmentés YAML dans le nouveau dossier *fabric8* :</span><span class="sxs-lookup"><span data-stu-id="d6963-174">Create three YAML fragment files in the new *fabric8* folder:</span></span>

   <span data-ttu-id="d6963-175">a.</span><span class="sxs-lookup"><span data-stu-id="d6963-175">a.</span></span> <span data-ttu-id="d6963-176">Créez un fichier intitulé **deployment.yml** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="d6963-176">Create a file named **deployment.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   <span data-ttu-id="d6963-177">b.</span><span class="sxs-lookup"><span data-stu-id="d6963-177">b.</span></span> <span data-ttu-id="d6963-178">Créez un fichier intitulé **secrets.yml** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="d6963-178">Create a file named **secrets.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   <span data-ttu-id="d6963-179">c.</span><span class="sxs-lookup"><span data-stu-id="d6963-179">c.</span></span> <span data-ttu-id="d6963-180">Créez un fichier intitulé **service.yml** avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="d6963-180">Create a file named **service.yml** with the following contents:</span></span>
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. <span data-ttu-id="d6963-181">Exécutez la commande Maven suivante pour générer le fichier de liste des ressources Kubernetes :</span><span class="sxs-lookup"><span data-stu-id="d6963-181">Run the following Maven command to build the Kubernetes resource list file:</span></span>

   ```shell
   mvn fabric8:resource
   ```

   <span data-ttu-id="d6963-182">Cette commande fusionne tous les fichiers yaml des ressources Kubernetes du dossier *src/main/fabric8* dans un fichier YAML qui contient une liste des ressources Kubernetes, qui peut être appliquée directement au cluster Kubernetes ou exportée dans un graphique Helm.</span><span class="sxs-lookup"><span data-stu-id="d6963-182">This command merges all Kubernetes resource yaml files under the *src/main/fabric8* folder to a YAML file that contains a Kubernetes resource list, which can be applied to Kubernetes cluster directly or export to a helm chart.</span></span>

   <span data-ttu-id="d6963-183">Maven affiche les résultats de la génération ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-183">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="d6963-184">Exécutez la commande Maven suivante pour appliquer le fichier de liste des ressources à votre cluster Kubernetes :</span><span class="sxs-lookup"><span data-stu-id="d6963-184">Run the following Maven command to apply the resource list file to your Kubernetes cluster:</span></span>

   ```shell
   mvn fabric8:apply
   ```

   <span data-ttu-id="d6963-185">Maven affiche les résultats de la génération ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-185">Maven will display the results of your build; for example:</span></span>  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. <span data-ttu-id="d6963-186">Une fois que l’application est déployée sur le cluster, interrogez l’adresse IP externe à l’aide de l’application `kubectl` ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-186">Once the app is deployed to the cluster, query the external IP address using the `kubectl` application; for example:</span></span>
   ```shell
   kubectl get svc -w
   ```

   <span data-ttu-id="d6963-187">`kubectl` affiche vos adresses IP internes et externes ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-187">`kubectl` will display your internal and external IP addresses; for example:</span></span>

   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```

   <span data-ttu-id="d6963-188">Vous pouvez utiliser l’adresse IP externe pour ouvrir votre application dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="d6963-188">You can use the external IP address to open your application in a web browser.</span></span>

   ![Parcourir l’exemple d’application en externe][SB02]

## <a name="delete-your-kubernetes-cluster"></a><span data-ttu-id="d6963-190">Supprimer votre cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d6963-190">Delete your Kubernetes cluster</span></span>

<span data-ttu-id="d6963-191">Lorsque vous n’avez plus besoin de votre cluster Kubernetes, vous pouvez utiliser la commande `az group delete` pour supprimer le groupe de ressources, ce qui supprime toutes ses ressources associées ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6963-191">When your Kubernetes cluster is no longer needed, you can use the `az group delete` command to remove the resource group, which will remove all of its related resources; for example:</span></span>

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a><span data-ttu-id="d6963-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6963-192">Next steps</span></span>

<span data-ttu-id="d6963-193">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d6963-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="d6963-194">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d6963-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)
* [<span data-ttu-id="d6963-195">Déployer une application Spring Boot sur Linux dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d6963-195">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)
* [<span data-ttu-id="d6963-196">Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d6963-196">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="d6963-197">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d6963-197">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="d6963-198">Pour plus d’informations sur l’exemple de projet Spring Boot on Docker, consultez [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="d6963-198">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="d6963-199">Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="d6963-199">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at <https://start.spring.io/>.</span></span>

<span data-ttu-id="d6963-200">Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="d6963-200">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at <https://start.spring.io/>.</span></span>

<span data-ttu-id="d6963-201">Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].</span><span class="sxs-lookup"><span data-stu-id="d6963-201">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[Avantages pour les abonnés MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
