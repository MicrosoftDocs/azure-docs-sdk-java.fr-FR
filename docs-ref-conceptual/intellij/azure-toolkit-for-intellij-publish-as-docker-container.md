---
title: Publier un conteneur Docker avec le kit de ressources Azure pour IntelliJ
description: Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 64cefc1ace5d0377dea25fdbdc83d8dada31ddf7
ms.sourcegitcommit: ed130145f9e5c2d803791d96bb118023175e644a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2018
ms.locfileid: "30223376"
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="db22d-103">Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="db22d-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="db22d-104">Les conteneurs Docker constituent une méthode largement utilisée pour déployer des applications web.</span><span class="sxs-lookup"><span data-stu-id="db22d-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="db22d-105">En utilisant des conteneurs Docker, les développeurs peuvent regrouper tous les fichiers et dépendances de leur projet en un même package pour un déploiement sur un serveur.</span><span class="sxs-lookup"><span data-stu-id="db22d-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="db22d-106">Le kit de ressources Azure pour IntelliJ simplifie ce processus pour les développeurs Java en ajoutant des fonctionnalités pour *publier en tant que conteneur Docker* permettant le déploiement sur Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="db22d-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="db22d-107">Cet article vous guide à travers les étapes nécessaires à la publication de vos applications sur Azure en tant que conteneurs Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="db22d-108">Vous pouvez trouver plus d’informations sur Docker sur le [site web de Docker].</span><span class="sxs-lookup"><span data-stu-id="db22d-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="db22d-109">Publier votre application web sur Azure en utilisant un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="db22d-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="db22d-110">Pour publier votre application web, vous devrez créer un artefact prêt pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="db22d-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="db22d-111">Pour plus d’informations, consultez la section [Informations supplémentaires sur la création d’artefacts](#artifacts).</span><span class="sxs-lookup"><span data-stu-id="db22d-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="db22d-112">Une fois que vous avez utilisé l’Assistant de déploiement au moins une fois, la plupart de vos paramètres sont utilisés comme valeurs par défaut quand vous réexécutez l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="db22d-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="db22d-113">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="db22d-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="db22d-114">Pour démarrer l’Assistant **Publish as Docker Container** (Publication en tant que conteneur Docker), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="db22d-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="db22d-115">Dans la fenêtre de l’outil **Project** (Projet), cliquez avec le bouton droit sur votre projet, cliquez sur **Azure** puis sur **Publish as Docker Container** (Publier en tant que conteneur Docker) :</span><span class="sxs-lookup"><span data-stu-id="db22d-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Commande Publish as Docker Container (Publier en tant que conteneur Docker)][PUB01]

   * <span data-ttu-id="db22d-117">Dans la barre d’outils IntelliJ, cliquez sur le bouton **Publish Group** (Publier le groupe) puis cliquez sur **Publish as Docker Container** (Publier en tant que conteneur Docker) :</span><span class="sxs-lookup"><span data-stu-id="db22d-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="db22d-118">![Commande Publish as Docker Container (Publier en tant que conteneur Docker)][PUB02]</span><span class="sxs-lookup"><span data-stu-id="db22d-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="db22d-119">L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="db22d-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB03]

3. <span data-ttu-id="db22d-121">Dans la fenêtre **Type an image name, select the artifact’s path and check a Docker host to be used** (Tapez un nom d’image, sélectionnez le chemin de l’artefact et indiquez un hôte Docker à utiliser), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="db22d-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="db22d-122">a.</span><span class="sxs-lookup"><span data-stu-id="db22d-122">a.</span></span> <span data-ttu-id="db22d-123">Dans la zone **Docker image name** (Nom de l’image Docker), entrez un nom unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="db22d-124">(L’Assistant crée automatiquement un nom, mais vous pouvez le modifier.)</span><span class="sxs-lookup"><span data-stu-id="db22d-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="db22d-125">b.</span><span class="sxs-lookup"><span data-stu-id="db22d-125">b.</span></span> <span data-ttu-id="db22d-126">La zone **Hosts** (Hôtes) affiche tous les hôtes Docker que vous avez déjà créés.</span><span class="sxs-lookup"><span data-stu-id="db22d-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="db22d-127">Effectuez l’une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-127">Do either of the following:</span></span> 
      * <span data-ttu-id="db22d-128">Si vous avez un hôte Docker existant, vous pouvez déployer votre application web sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="db22d-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="db22d-129">Pour créer un hôte Docker, cliquez sur le signe plus de couleur verte (**+**).</span><span class="sxs-lookup"><span data-stu-id="db22d-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="db22d-130">La boîte de dialogue **Create Docker Host** (Créer un hôte Docker) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="db22d-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB04a]

4. <span data-ttu-id="db22d-132">Dans la fenêtre **Configure the new virtual machine** (Configurer la nouvelle machine virtuelle), fournissez les informations suivantes sur votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="db22d-133">(L’Assistant génère automatiquement la plupart des informations pour vous, mais vous pouvez les modifier.)</span><span class="sxs-lookup"><span data-stu-id="db22d-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="db22d-134">a.</span><span class="sxs-lookup"><span data-stu-id="db22d-134">a.</span></span> <span data-ttu-id="db22d-135">Dans la zone **Name** (Nom), entrez un nom unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="db22d-136">(Ce n’est pas le même que le nom de l’image Docker que vous avez spécifié précédemment.)</span><span class="sxs-lookup"><span data-stu-id="db22d-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="db22d-137">b.</span><span class="sxs-lookup"><span data-stu-id="db22d-137">b.</span></span> <span data-ttu-id="db22d-138">Dans la zone **Subscription** (Abonnement), entrez l’abonnement Azure que vous utilisez pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="db22d-139">c.</span><span class="sxs-lookup"><span data-stu-id="db22d-139">c.</span></span> <span data-ttu-id="db22d-140">Dans la zone **Region** (Région), entrez la région géographique où se trouve votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="db22d-141">d.</span><span class="sxs-lookup"><span data-stu-id="db22d-141">d.</span></span> <span data-ttu-id="db22d-142">Sous l’onglet **OS and Size** (Système d’exploitation et taille), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="db22d-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="db22d-143">**Host OS** (Système d’exploitation de l’hôte) : entrez le système d’exploitation de la machine virtuelle qui contient votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="db22d-144">**Size** (Taille) : entrez la taille de la machine virtuelle de votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="db22d-145">e.</span><span class="sxs-lookup"><span data-stu-id="db22d-145">e.</span></span> <span data-ttu-id="db22d-146">Sous l’onglet **Resource Group** (Groupe de ressources), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="db22d-147">**New resource group** (Nouveau groupe de ressources) : créez un groupe de ressources pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="db22d-148">**Existing resource group** (Groupe de ressources existant) : spécifiez un groupe de ressources existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="db22d-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="db22d-149">f.</span><span class="sxs-lookup"><span data-stu-id="db22d-149">f.</span></span> <span data-ttu-id="db22d-150">Sous l’onglet **Network** (Réseau), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="db22d-151">**New virtual network** (Nouveau réseau virtuel) : créez un réseau virtuel pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="db22d-152">**Existing virtual network** (Réseau virtuel existant) : spécifiez un réseau virtuel existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="db22d-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="db22d-153">g.</span><span class="sxs-lookup"><span data-stu-id="db22d-153">g.</span></span> <span data-ttu-id="db22d-154">Sous l’onglet **Storage** (Stockage), sélectionnez une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="db22d-155">**New storage account** (Nouveau compte de stockage) : créez un compte de stockage pour votre hôte.</span><span class="sxs-lookup"><span data-stu-id="db22d-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="db22d-156">**Compte de stockage existant** : spécifiez un compte de stockage existant dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="db22d-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="db22d-157">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="db22d-157">Click **Next**.</span></span>  
     <span data-ttu-id="db22d-158">La fenêtre **Configure log in credentials and port settings** (Configurer les informations d’identification de connexion et les paramètres de port) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="db22d-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![La fenêtre Configure log in credentials and port settings (Configurer les informations d’identification de connexion et les paramètres de port)][PUB05]

6. <span data-ttu-id="db22d-160">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-160">Select one of the following options:</span></span>

      * <span data-ttu-id="db22d-161">**Import credentials from Azure Key Vault** (Importer des informations d’identification depuis Azure Key Vault) : spécifiez un ensemble d’informations d’identification précédemment enregistré et stocké dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="db22d-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="db22d-162">Un coffre de clés Azure créé avec un compte ou un principal de service spécifique n’est pas automatiquement accessible par un autre compte ou principal de service qui partage l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="db22d-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="db22d-163">Pour permettre à un autre compte ou principal de service d’utiliser le coffre de clés, vous devez utiliser le portail Azure pour ajouter le compte ou le principal de service.</span><span class="sxs-lookup"><span data-stu-id="db22d-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="db22d-164">**New log in credentials** (Nouvelles informations d’identification de connexion) : créez un nouvel ensemble d’informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="db22d-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="db22d-165">Si vous sélectionnez cette option, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="db22d-165">If you select this option, do the following:</span></span>

    <span data-ttu-id="db22d-166">a.</span><span class="sxs-lookup"><span data-stu-id="db22d-166">a.</span></span> <span data-ttu-id="db22d-167">Sous l’onglet **VM Credentials** (Informations d’identification de machine virtuelle), indiquez les informations d’identification de connexion de la machine virtuelle de votre hôte Docker :</span><span class="sxs-lookup"><span data-stu-id="db22d-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host:</span></span>

    * <span data-ttu-id="db22d-168">**Username** (Nom d’utilisateur) : entrez le nom d’utilisateur des informations d’identification de connexion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db22d-168">**Username**: Enter the username for your virtual-machine login credentials.</span></span>

    * <span data-ttu-id="db22d-169">**Password** (Mot de passe) et **Confirm** (Confirmer) : entrez le mot de passe pour les informations d’identification de connexion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="db22d-169">**Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>

    * <span data-ttu-id="db22d-170">**SSH** : entrez les paramètres SSH (Secure Shell) pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-170">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="db22d-171">Vous pouvez sélectionner l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-171">You can select one of the following options:</span></span>

        * <span data-ttu-id="db22d-172">**None** (Aucun) : spécifie que votre machine virtuelle n’autorisera pas les connexions SSH.</span><span class="sxs-lookup"><span data-stu-id="db22d-172">**None**: Specifies that your virtual machine does not allow SSH connections.</span></span>

        * <span data-ttu-id="db22d-173">**Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaire pour la connexion via SSH.</span><span class="sxs-lookup"><span data-stu-id="db22d-173">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>

        * <span data-ttu-id="db22d-174">**Import from directory** (Importer à partir du répertoire) : vous permet de spécifier un répertoire qui contient un jeu de paramètres SSH précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="db22d-174">**Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="db22d-175">Le répertoire doit contenir les deux fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="db22d-175">The directory must contain the following two files:</span></span>

            * <span data-ttu-id="db22d-176">*id_rsa* : contient l’identification RSA d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db22d-176">*id_rsa*: Contains the RSA identification for a user.</span></span>

            * <span data-ttu-id="db22d-177">*id_rsa.pub* : contient la clé publique RSA qui est utilisée pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="db22d-177">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>

    <span data-ttu-id="db22d-178">b.</span><span class="sxs-lookup"><span data-stu-id="db22d-178">b.</span></span> <span data-ttu-id="db22d-179">Sous l’onglet **Docker Daemon Access** (Accès au démon Docker), fournissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-179">On the **Docker Daemon Access** tab, provide the following information:</span></span>

    ![Créer un hôte Docker][PUB06]
    
    * <span data-ttu-id="db22d-181">**Docker Daemon port** (Port du démon Docker) : entrez le port TCP unique pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-181">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
    
    * <span data-ttu-id="db22d-182">**TLS Security** (Sécurité TLS) : entrez les paramètres TLS (Transport Layer Security) pour votre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-182">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="db22d-183">Vous pouvez choisir parmi les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-183">You can choose from the following options:</span></span>
    
        * <span data-ttu-id="db22d-184">**None** (Aucun) : spécifie que votre machine virtuelle n’autorise pas les connexions TLS.</span><span class="sxs-lookup"><span data-stu-id="db22d-184">**None**: Specifies that your virtual machine does not allow TLS connections.</span></span>
        
        * <span data-ttu-id="db22d-185">**Auto-generate** (Générer automatiquement) : crée automatiquement les paramètres nécessaire pour la connexion via TLS.</span><span class="sxs-lookup"><span data-stu-id="db22d-185">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
        
        * <span data-ttu-id="db22d-186">**Import from directory** (Importer à partir du répertoire) : spécifie un répertoire qui contient un jeu de paramètres TLS précédemment enregistrés.</span><span class="sxs-lookup"><span data-stu-id="db22d-186">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="db22d-187">Le répertoire doit contenir les six fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="db22d-187">The directory must contain the following six files:</span></span>
        
            * <span data-ttu-id="db22d-188">*ca.pem* et *ca-key.pem* : contiennent le certificat et la clé publique de l’autorité de certification TLS.</span><span class="sxs-lookup"><span data-stu-id="db22d-188">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
            
            * <span data-ttu-id="db22d-189">*cert.pem* et *key.pem* : contiennent le certificat client et la clé publique qui seront utilisés pour l’authentification TLS.</span><span class="sxs-lookup"><span data-stu-id="db22d-189">*cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.</span></span>
            
            * <span data-ttu-id="db22d-190">*server.pem* et *server-key.pem* : contiennent le certificat client et la clé publique qui sont utilisés pour l’authentification TLS.</span><span class="sxs-lookup"><span data-stu-id="db22d-190">*server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>

7. <span data-ttu-id="db22d-191">Après avoir entré les informations nécessaires, cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="db22d-191">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="db22d-192">L’Assistant **Deploy Docker Container on Azure** (Déploiement d’un conteneur Docker sur Azure) réapparaît.</span><span class="sxs-lookup"><span data-stu-id="db22d-192">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Assistant Deploy Docker Container on Azure (Déploiement d’un conteneur Docker sur Azure)][PUB07]

8. <span data-ttu-id="db22d-194">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="db22d-194">Click **Next**.</span></span>  
    <span data-ttu-id="db22d-195">La fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer) s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="db22d-195">The **Configure the Docker container to be created** window opens.</span></span>

   ![La fenêtre Configure the Docker container to be created (Configurer le conteneur Docker à créer)][PUB08]

9. <span data-ttu-id="db22d-197">Dans la fenêtre **Configure the Docker container to be created** (Configurer le conteneur Docker à créer), fournissez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-197">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="db22d-198">a.</span><span class="sxs-lookup"><span data-stu-id="db22d-198">a.</span></span> <span data-ttu-id="db22d-199">Dans la zone **Docker container name** (Nom du conteneur Docker), entrez un nom unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-199">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="db22d-200">b.</span><span class="sxs-lookup"><span data-stu-id="db22d-200">b.</span></span> <span data-ttu-id="db22d-201">Choisissez l’une des images Docker suivantes :</span><span class="sxs-lookup"><span data-stu-id="db22d-201">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="db22d-202">**Predefined Docker image** (Image Docker prédéfinie) : spécifiez une image Docker préexistante dans Azure.</span><span class="sxs-lookup"><span data-stu-id="db22d-202">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="db22d-203">La liste des images Docker dans cette zone est constituée de plusieurs images configurées pour application d’un correctif par le kit de ressources Azure afin que votre artefact soit déployé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="db22d-203">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="db22d-204">**Custom Dockerfile** (Fichier Dockerfile personnalisé) : spécifiez un fichier Dockerfile précédemment enregistré sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="db22d-204">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="db22d-205">Il s’agit d’une fonctionnalité plus avancée destinée aux développeurs qui veulent déployer leur propre fichier Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="db22d-205">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="db22d-206">Toutefois, les développeurs qui utilisent cette option doivent s’assurer que leur fichier Docker est construit correctement.</span><span class="sxs-lookup"><span data-stu-id="db22d-206">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="db22d-207">Comme le kit de ressources Azure ne valide pas le contenu d’un fichier Dockerfile personnalisé, le déploiement peut échouer si le fichier Dockerfile présente des problèmes.</span><span class="sxs-lookup"><span data-stu-id="db22d-207">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="db22d-208">En outre, comme la boîte à outils Azure attend que le fichier Dockerfile personnalisé contienne un artefact d’application web, il tente d’ouvrir une connexion HTTP.</span><span class="sxs-lookup"><span data-stu-id="db22d-208">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="db22d-209">Si les développeurs publier un autre type d’artefact, ils peuvent recevoir des erreurs sans effet après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="db22d-209">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="db22d-210">c.</span><span class="sxs-lookup"><span data-stu-id="db22d-210">c.</span></span> <span data-ttu-id="db22d-211">Dans la zone **Port settings** (Paramètres de port), entrez la liaison de port TCP unique pour votre conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-211">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="db22d-212">Après avoir terminé les étapes précédentes, cliquez sur **Finish** (Terminer).</span><span class="sxs-lookup"><span data-stu-id="db22d-212">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="db22d-213">Le kit de ressources Azure commence le déploiement de votre application web sur Azure dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="db22d-213">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="db22d-214">Sauf si vous avez configuré le déploiement d’IntelliJ en arrière-plan, une barre de progression **Deploying to Azure** (Déploiement sur Azure) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="db22d-214">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![La barre de progression du déploiement][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="db22d-216">Informations supplémentaires sur la création d’artefacts</span><span class="sxs-lookup"><span data-stu-id="db22d-216">Additional information about creating artifacts</span></span>

<span data-ttu-id="db22d-217">Pour créer un artefact prêt pour le déploiement, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="db22d-217">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="db22d-218">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="db22d-218">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="db22d-219">Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.</span><span class="sxs-lookup"><span data-stu-id="db22d-219">Click **File**, and then click **Project Structure**.</span></span>

   ![La commande Structure de projet][ART01]

3. <span data-ttu-id="db22d-221">Pour ajouter un artefact, cliquez sur le signe plus de couleur verte (**+**) puis cliquez sur **Web Application: Archive** (Application web : Archive).</span><span class="sxs-lookup"><span data-stu-id="db22d-221">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![La commande Web Application: Archive (Application web : Archive)][ART02]

4. <span data-ttu-id="db22d-223">Dans la zone **Name** (Nom), entrez un nom pour votre artefact (n’incluez pas l’extension *.war*) puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="db22d-223">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![La zone Name (Nom) de l’artefact][ART03]

<span data-ttu-id="db22d-225">Pour plus d’informations sur la création d’artefacts dans IntelliJ, consultez [Configuring artifacts] sur le site web de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="db22d-225">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db22d-226">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db22d-226">Next steps</span></span>

<span data-ttu-id="db22d-227">Pour obtenir des ressources supplémentaires pour Docker, consultez le [site web de Docker].</span><span class="sxs-lookup"><span data-stu-id="db22d-227">For additional resources for Docker, see the official [Docker website].</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[site web de Docker]: https://www.docker.com/
[Docker website]: https://www.docker.com/
[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
