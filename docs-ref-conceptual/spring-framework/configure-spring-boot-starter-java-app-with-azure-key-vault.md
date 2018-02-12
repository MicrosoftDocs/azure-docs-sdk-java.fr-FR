---
title: Comment utiliser Spring Boot Starter pour Azure Key Vault
description: "Découvrez comment configurer une application d’initialisation Spring Boot avec l’application de démarrage Azure Key Vault."
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 52e7dc3f84ea96f22d8e478a597452c76ed8bf22
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a><span data-ttu-id="d1f7a-103">Comment utiliser Spring Boot Starter pour Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="d1f7a-103">How to use the Spring Boot Starter for Azure Key Vault</span></span>

## <a name="overview"></a><span data-ttu-id="d1f7a-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d1f7a-104">Overview</span></span>

<span data-ttu-id="d1f7a-105">Cet article vous explique comment créer une application avec l’instance **[Spring Initializr]**, qui utilise la solution Spring Boot Starter pour Azure Key Vault pour récupérer une chaîne de connexion stockée comme secrète dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Key Vault to retrieve a connection string that is stored as a secret in a key vault.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1f7a-106">configuration requise</span><span class="sxs-lookup"><span data-stu-id="d1f7a-106">Prerequisites</span></span>

<span data-ttu-id="d1f7a-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="d1f7a-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="d1f7a-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="d1f7a-109">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="d1f7a-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-the-spring-initialzr"></a><span data-ttu-id="d1f7a-111">Créer une application à l’aide de Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="d1f7a-111">Create an app using the Spring Initialzr</span></span>

1. <span data-ttu-id="d1f7a-112">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="d1f7a-113">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Spécifiez les noms de groupes et d’artefacts.][secrets-01]

1. <span data-ttu-id="d1f7a-115">Faites défiler jusqu’à la section **Azure**, puis cochez la case **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-115">Scroll down to the **Azure** section and check the box for **Azure Key Vault**.</span></span>

   ![Sélectionnez l’application de démarrage Azure Key Vault.][secrets-02]

1. <span data-ttu-id="d1f7a-117">Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-117">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Générez le projet Spring Boot.][secrets-03]

1. <span data-ttu-id="d1f7a-119">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-119">When prompted, download the project to a path on your local computer.</span></span>

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a><span data-ttu-id="d1f7a-120">Se connecter à Azure et sélectionner l’abonnement à utiliser</span><span class="sxs-lookup"><span data-stu-id="d1f7a-120">Sign into Azure and select the subscription to use</span></span>

1. <span data-ttu-id="d1f7a-121">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-121">Open a command prompt.</span></span>

1. <span data-ttu-id="d1f7a-122">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-122">Sign into your Azure account by using the Azure CLI:</span></span>

   ```azurecli
   az login
   ```
   <span data-ttu-id="d1f7a-123">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-123">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="d1f7a-124">Répertoriez vos abonnements :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-124">List your subscriptions:</span></span>

   ```azurecli
   az account list
   ```
   <span data-ttu-id="d1f7a-125">Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-125">Azure will return a list of your subscriptions, and you will need to copy the GUID for the subscription that you want to use; for example:</span></span>

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]

1. Specify the GUID for the account you want to use with Azure; for example:

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a><span data-ttu-id="d1f7a-126">Créez et configurez une nouvelle instance Azure Key Vault à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-126">Create and configure a new Azure Key Vault using the Azure CLI</span></span>

1. <span data-ttu-id="d1f7a-127">Créez un groupe de ressources pour les ressources Azure que vous utiliserez avec votre coffre de clés, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-127">Create a resource group for the Azure resources you will use for your key vault; for example:</span></span>
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   <span data-ttu-id="d1f7a-128">Où :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-128">Where:</span></span>
   | <span data-ttu-id="d1f7a-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1f7a-129">Parameter</span></span> | <span data-ttu-id="d1f7a-130">Description</span><span class="sxs-lookup"><span data-stu-id="d1f7a-130">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="d1f7a-131">Spécifie un nom unique pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-131">Specifies a unique name for your resource group.</span></span> |
   | `location` | <span data-ttu-id="d1f7a-132">Spécifie la [Région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-132">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |

   <span data-ttu-id="d1f7a-133">L’interface Azure CLI affiche les résultats de la création de votre groupe de ressources ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-133">The Azure CLI will display the results of your resource group creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. <span data-ttu-id="d1f7a-134">Créez un principal de service Azure pour votre inscription d’application, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-134">Create an Azure service principal from your application registration; for example:</span></span>
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   <span data-ttu-id="d1f7a-135">Où :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-135">Where:</span></span>
   | <span data-ttu-id="d1f7a-136">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1f7a-136">Parameter</span></span> | <span data-ttu-id="d1f7a-137">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="d1f7a-137">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="d1f7a-138">Spécifie le nom de votre principal de service Azure.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-138">Specifies the name for your Azure service principal.</span></span> |

   <span data-ttu-id="d1f7a-139">L’interface de ligne de commande Azure renvoie un message d’état JSON comportant les éléments *appId* et *password*, que vous utiliserez plus tard en tant que l’ID et le mot de passe client, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-139">The Azure CLI will return a JSON status message that contains the *appId* and *password*, which you will use later as the client id and client password; for example:</span></span>

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. <span data-ttu-id="d1f7a-140">Créez un nouveau coffre de clé dans le groupe de ressources, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-140">Create a new key vault in the resource group; for example:</span></span>
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   <span data-ttu-id="d1f7a-141">Où :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-141">Where:</span></span>
   | <span data-ttu-id="d1f7a-142">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1f7a-142">Parameter</span></span> | <span data-ttu-id="d1f7a-143">Description</span><span class="sxs-lookup"><span data-stu-id="d1f7a-143">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="d1f7a-144">Spécifie un nom unique à associer au coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-144">Specifies a unique name for your key vault.</span></span> |
   | `location` | <span data-ttu-id="d1f7a-145">Spécifie la [Région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-145">Specifies the [Azure region](https://azure.microsoft.com/regions/) where your resource group will be hosted.</span></span> |
   | `enabled-for-deployment` | <span data-ttu-id="d1f7a-146">Spécifie l’[option de déploiement du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="d1f7a-146">Specifies the [key vault deployment option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-disk-encryption` | <span data-ttu-id="d1f7a-147">Spécifie l’[option de chiffrement du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="d1f7a-147">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `enabled-for-template-deployment` | <span data-ttu-id="d1f7a-148">Spécifie l’[option de chiffrement du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="d1f7a-148">Specifies the [key vault encryption option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `sku` | <span data-ttu-id="d1f7a-149">Spécifie l’[option de référence SKU du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="d1f7a-149">Specifies the [key vault SKU option](https://docs.microsoft.com/en-us/cli/azure/keyvault).</span></span> |
   | `query` | <span data-ttu-id="d1f7a-150">Spécifie une valeur à récupérer de la réponse, qui est l’URI du coffre de clés dont vous aurez besoin pour effectuer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-150">Specifies a value to retrieve from the response, which is the key vault URI that you will need to complete this tutorial.</span></span> |

   <span data-ttu-id="d1f7a-151">L’interface de ligne de commande Azure affiche l’URI associé au coffre de clés, que vous utiliserez ultérieurement, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-151">The Azure CLI will display the URI for key vault, which you will use later; for example:</span></span>  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. <span data-ttu-id="d1f7a-152">Définissez la stratégie d’accès du principal de service Azure créé précédemment, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-152">Set the access policy for the Azure service principal you created earlier; for example:</span></span>
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   <span data-ttu-id="d1f7a-153">Où :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-153">Where:</span></span>
   | <span data-ttu-id="d1f7a-154">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1f7a-154">Parameter</span></span> | <span data-ttu-id="d1f7a-155">Description</span><span class="sxs-lookup"><span data-stu-id="d1f7a-155">Description</span></span> |
   |---|---|
   | `name` | <span data-ttu-id="d1f7a-156">Spécifie le nom du coffre de clés créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-156">Specifies your key vault name from earlier.</span></span> |
   | `secret-permission` | <span data-ttu-id="d1f7a-157">Spécifie les [stratégies de sécurité](https://docs.microsoft.com/en-us/cli/azure/keyvault) de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-157">Specifies the [security policies](https://docs.microsoft.com/en-us/cli/azure/keyvault) for your key vault.</span></span> |
   | `spn` | <span data-ttu-id="d1f7a-158">Spécifie l’identificateur unique de votre inscription d’application antérieure.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-158">Specifies the GUID for your application registration from earlier.</span></span> |

   <span data-ttu-id="d1f7a-159">L’interface de ligne de commande Azure affiche les résultats de votre création de stratégie de sécurité, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-159">The Azure CLI will display the results of your security policy creation; for example:</span></span>  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

1. <span data-ttu-id="d1f7a-160">Stockez une instance secrète dans votre nouveau coffre de clés, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-160">Store a secret in your new key vault; for example:</span></span>
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   <span data-ttu-id="d1f7a-161">Où :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-161">Where:</span></span>
   | <span data-ttu-id="d1f7a-162">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1f7a-162">Parameter</span></span> | <span data-ttu-id="d1f7a-163">Description</span><span class="sxs-lookup"><span data-stu-id="d1f7a-163">Description</span></span> |
   |---|---|
   | `vault-name` | <span data-ttu-id="d1f7a-164">Spécifie le nom du coffre de clés créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-164">Specifies your key vault name from earlier.</span></span> |
   | `name` | <span data-ttu-id="d1f7a-165">Spécifie le nom de votre instance secrète.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-165">Specifies the name of your secret.</span></span> |
   | `value` | <span data-ttu-id="d1f7a-166">Spécifie la valeur de votre instance secrète.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-166">Specifies the value of your secret.</span></span> |

   <span data-ttu-id="d1f7a-167">L’interface de ligne de commande Azure affiche les résultats de votre création d’instance secrète, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-167">The Azure CLI will display the results of your secret creation; for example:</span></span>  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="d1f7a-168">Configurer et compiler votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="d1f7a-168">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="d1f7a-169">Extrayez les fichiers des fichiers d’archive du projet Spring Boot que vous avez téléchargés précédemment dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-169">Extract the files from the Spring Boot project archive files that you downloaded earlier into a directory.</span></span>

1. <span data-ttu-id="d1f7a-170">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-170">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="d1f7a-171">Ajoutez les valeurs associées à votre coffre de clés à l’aide des données de la procédure exécutée plus tôt dans ce didacticiel, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-171">Add the values for your key vault using values from the steps that you completed earlier in this tutorial; for example:</span></span>
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   <span data-ttu-id="d1f7a-172">Où :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-172">Where:</span></span>
   | <span data-ttu-id="d1f7a-173">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d1f7a-173">Parameter</span></span> | <span data-ttu-id="d1f7a-174">Description</span><span class="sxs-lookup"><span data-stu-id="d1f7a-174">Description</span></span> |
   |---|---|
   | `azure.keyvault.uri` | <span data-ttu-id="d1f7a-175">Spécifie l’URI de l’emplacement de création de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-175">Specifies the URI from when you created your key vault.</span></span> |
   | `azure.keyvault.client-id` | <span data-ttu-id="d1f7a-176">Spécifie l’identificateur unique *appId* généré lors de la création de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-176">Specifies the *appId* GUID from when you created your service principal.</span></span> |
   | `azure.keyvault.client-key` | <span data-ttu-id="d1f7a-177">Spécifie l’identificateur unique *password* généré lors de la création de votre principal de service.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-177">Specifies the *password* GUID from when you created your service principal.</span></span> |

1. <span data-ttu-id="d1f7a-178">Accédez au fichier source principal de code de votre projet, par exemple : */src/main/java/com/wingtiptoys/secrets*.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-178">Navigate to the main source code file of your project; for example: */src/main/java/com/wingtiptoys/secrets*.</span></span>

1. <span data-ttu-id="d1f7a-179">Ouvrez le fichier Java principal de l’application dans un fichier d’un éditeur de texte, par exemple : *SecretsApplication.java*, puis ajoutez les lignes suivantes au fichier :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-179">Open the application's main Java file in a file in a text editor; for example: *SecretsApplication.java*, and add the following lines to the file:</span></span>

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   <span data-ttu-id="d1f7a-180">Cet exemple de code récupère la chaîne de connexion du coffre de clés et l’affiche dans une ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-180">This code example retrieves the connection string from the key vault and displays it to the command line.</span></span>

1. <span data-ttu-id="d1f7a-181">Enregistrez et fermez le fichier Java.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-181">Save and close the Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="d1f7a-182">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="d1f7a-182">Build and test your app</span></span>

1. <span data-ttu-id="d1f7a-183">Accédez au répertoire dans lequel est hébergé le fichier *pom.xml* de votre application Spring Boot :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-183">Navigate to the directory where the *pom.xml* file for your Spring Boot app is located:</span></span>

1. <span data-ttu-id="d1f7a-184">Générez votre application Spring Boot avec Maven, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-184">Build your Spring Boot application with Maven; for example:</span></span>

   ```bash
   mvn clean package
   ```

   <span data-ttu-id="d1f7a-185">Maven affiche les résultats de la génération.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-185">Maven will display the results of your build.</span></span>

   ![État de génération de l’application Spring Boot][build-application-01]

1. <span data-ttu-id="d1f7a-187">Exécutez votre application Spring Boot avec Maven ; l’application affiche la chaîne de connexion de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d1f7a-187">Run your Spring Boot application with Maven; the application will display the connection string from your key vault.</span></span> <span data-ttu-id="d1f7a-188">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-188">For example:</span></span>

   ```bash
   mvn spring-boot:run
   ```

   ![Message d’exécution Spring Boot][build-application-02]

## <a name="next-steps"></a><span data-ttu-id="d1f7a-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d1f7a-190">Next steps</span></span>

<span data-ttu-id="d1f7a-191">Pour en savoir plus sur l’utilisation d’Azure Key Vault, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-191">For more information about using Azure Key Vaults, see the following articles:</span></span>

* <span data-ttu-id="d1f7a-192">[Documentation Key Vault].</span><span class="sxs-lookup"><span data-stu-id="d1f7a-192">[Key Vault Documentation].</span></span>

* <span data-ttu-id="d1f7a-193">[Bien démarrer avec Azure Key Vault]</span><span class="sxs-lookup"><span data-stu-id="d1f7a-193">[Get started with Azure Key Vault]</span></span>

<span data-ttu-id="d1f7a-194">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="d1f7a-194">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="d1f7a-195">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d1f7a-195">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="d1f7a-196">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d1f7a-196">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="d1f7a-197">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="d1f7a-197">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Documentation Key Vault]: /azure/key-vault/
[Bien démarrer avec Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
