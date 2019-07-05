---
title: Configurer MicroProfile avec Azure Key Vault
description: Découvrez comment injecter des secrets dans un service web MicroProfile avec Azure Key Vault.
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533616"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a><span data-ttu-id="1fc3c-103">Configurer MicroProfile avec Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="1fc3c-103">Configure MicroProfile by using Azure Key Vault</span></span>

<span data-ttu-id="1fc3c-104">Cet article montre comment configurer une application [MicroProfile](http://microprofile.io) pour récupérer des secrets à partir d’[Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="1fc3c-104">This article demonstrates how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from an [Azure key vault](https://azure.microsoft.com/services/key-vault/).</span></span> <span data-ttu-id="1fc3c-105">Dans ce processus, vous allez utiliser les [API MicroProfile Config](https://microprofile.io/project/eclipse/microprofile-config) pour créer une connexion directe à Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-105">In this process, you use the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to an Azure key vault.</span></span> <span data-ttu-id="1fc3c-106">En tant que développeur, l’utilisation des API MicroProfile Config vous permet de bénéficier d’une API standard pour récupérer et injecter des données de configuration dans leurs microservices.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-106">As a developer, by using the MicroProfile Config APIs, you benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="1fc3c-107">Avant de rentrer dans le vif du sujet, jetons un rapide coup d’œil à ce que la combinaison d’Azure Key Vault et de l’API MicroProfile Config nous permet d’écrire dans notre code.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-107">Before you start, take a quick look at what a combination of Azure Key Vault and the MicroProfile Config API enables you to write in your code.</span></span> <span data-ttu-id="1fc3c-108">L’extrait de code suivant correspond à un champ au sein d’une classe annotée avec `@Inject` et `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-108">The following code snippet is of a field in a class that's annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="1fc3c-109">Le nom (*name*) spécifié dans l’annotation correspond au nom de la propriété à rechercher dans Azure Key Vault, et *defaultValue* correspond à ce qui sera configuré si la clé n’est pas découverte.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-109">The *name* that's specified in the annotation is the name of the property to look up in your key vault, and the *defaultValue* is what will be set if the key is not discovered.</span></span> <span data-ttu-id="1fc3c-110">De cette façon, la valeur qui est stockée dans le coffre de clés (c’est-à-dire, la valeur par défaut) est automatiquement injectée dans le champ lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-110">The result is that the value that's stored in the key vault, or the default value, is injected automatically into the field at runtime.</span></span> <span data-ttu-id="1fc3c-111">Cette action peut vous simplifier la vie, car vous n’avez plus besoin de passer des valeurs dans les constructeurs et les méthodes setter.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-111">This action can simplify your life, because you no longer need to pass values around in constructors and setter methods.</span></span> <span data-ttu-id="1fc3c-112">C’est MicroProfile qui s’en charge.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-112">Instead, MicroProfile handles this task.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="1fc3c-113">Pour demander des secrets, vous pouvez accéder directement à MicroProfile Config.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-113">To request secrets, as necessary, you can also access the MicroProfile config directly.</span></span> <span data-ttu-id="1fc3c-114">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="1fc3c-114">For example:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="1fc3c-115">Cet exemple de code utilise [Payara Micro](https://www.payara.fish/payara_micro) et [MicroProfile](https://microprofile.io/) pour créer un petit fichier Java au format WAR pouvant être exécuté localement sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-115">This sample code uses [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java web application requirement (WAR) file that you can run locally on your machine.</span></span> <span data-ttu-id="1fc3c-116">Il ne montre pas la procédure de dockerisation ni la poussé (push) de code vers Azure. Toutefois, la section située à la fin de cet article fournit des liens vers des tutoriels qui expliquent ces procédures.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-116">It doesn't demonstrate how to Dockerize or push the code to Azure, but the section at the end of this article has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="1fc3c-117">Cet exemple utilise une bibliothèque gratuite en open source qui crée une source de configuration (via l’API MicroProfile Config) dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-117">The sample uses a free and open source library that creates a config source (using the MicroProfile Config API) in your key vault.</span></span> <span data-ttu-id="1fc3c-118">Pour obtenir plus d’informations sur cette bibliothèque et passer en revue le code, consultez la [page GitHub du projet](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="1fc3c-118">To learn more about this library and review the code, see the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="1fc3c-119">Si vous utilisez la bibliothèque, le code de ce tutoriel peut se concentrer sur la configuration de la bibliothèque, puis injecter des clés dans votre code.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-119">If you use the library, the code in this tutorial can simply focus on the configuration of the library and then inject keys into your code.</span></span> <span data-ttu-id="1fc3c-120">Vous n’avez pas besoin d’écrire du code spécialement pour Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-120">You don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="1fc3c-121">Pour exécuter ce code sur votre ordinateur local, commencez par créer une ressource de coffre de clés, puis suivez les instructions des sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-121">To run this code on your local machine, starting with creating a key vault resource, follow the instructions in the next sections.</span></span>

## <a name="create-a-key-vault-resource"></a><span data-ttu-id="1fc3c-122">Créer une ressource de coffre de clés</span><span class="sxs-lookup"><span data-stu-id="1fc3c-122">Create a key vault resource</span></span>

<span data-ttu-id="1fc3c-123">Dans cette section, vous allez utiliser Azure CLI pour créer une ressource de coffre de clés et ajouter un secret à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-123">In this section, you use the Azure CLI to create a key vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="1fc3c-124">Créez un principal de service Azure.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-124">Create an Azure service principal.</span></span> <span data-ttu-id="1fc3c-125">Cette étape vous donne l’ID client et la clé dont vous avez besoin pour accéder à votre coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="1fc3c-125">This step gives you the client ID and key that you need to access your key vault:</span></span>

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    <span data-ttu-id="1fc3c-126">Nous allons utiliser *microprofile-keyvault-service-principal* pour remplacer *\<nom_principal_service>* dans l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-126">Let's use *microprofile-keyvault-service-principal* to replace *\<service_principal_name>* in the preceding step.</span></span> <span data-ttu-id="1fc3c-127">La réponse d’Azure ressemblera à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="1fc3c-127">The response from Azure would be similar to the following:</span></span>

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    <span data-ttu-id="1fc3c-128">Notez les valeurs *appId* et *password*.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-128">Of particular note here are the *appId* and *password* values.</span></span> <span data-ttu-id="1fc3c-129">Vous en aurez besoin plus loin dans cet article pour l’*ID client* et la *clé*.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-129">You'll use them later in this article as *client ID* and *key*.</span></span>

1. <span data-ttu-id="1fc3c-130">(Facultatif) Maintenant que vous avez créé un principal de service, vous pouvez créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-130">(Optional) Now that you've created a service principal, you can create a resource group.</span></span> <span data-ttu-id="1fc3c-131">Vous pouvez ignorer cette étape si vous disposez déjà d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-131">If you already have a resource group that you want to use, you can skip this step.</span></span> <span data-ttu-id="1fc3c-132">Pour obtenir la liste des emplacements des groupes de ressources, vous pouvez appeler `az account list-locations` et utiliser la valeur *name* de cette liste pour spécifier l’emplacement de création du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-132">To get a list of resource group locations, you can call `az account list-locations` and use the *name* value from that list to specify where the resource group should be created.</span></span>

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. <span data-ttu-id="1fc3c-133">Créez une ressource de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-133">Create a key vault resource.</span></span> <span data-ttu-id="1fc3c-134">Vous allez utiliser son nom pour faire référence au coffre de clés, veillez donc à choisir un nom facile à mémoriser.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-134">You'll use your key vault name to refer to the key vault later, so be sure to choose a memorable name.</span></span>

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. <span data-ttu-id="1fc3c-135">Accordez les autorisations nécessaires au principal de service que vous avez précédemment créé, de sorte qu’il puisse accéder aux secrets du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-135">Grant the appropriate permissions to the service principal that you created earlier, so that it can access the key vault secrets.</span></span> <span data-ttu-id="1fc3c-136">Dans le code suivant, la valeur appId correspond à la valeur *appId* de l’étape 1, lors de laquelle vous avez créé le principal du service.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-136">The appId value in the following code is the *appId* value from step 1, where you created the service principal.</span></span> <span data-ttu-id="1fc3c-137">Autrement dit, même si l’*appId* de l’étape 1 était *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, vous devez utiliser la valeur à partir de votre propre sortie de terminal.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-137">That is, the *appId* in step 1 was *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, but you should use the value from your own terminal output.</span></span>

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. <span data-ttu-id="1fc3c-138">Maintenant, vous pouvez pousser (push) un secret vers votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-138">Now you can push a secret into your key vault.</span></span> <span data-ttu-id="1fc3c-139">Utilisez le nom de clé *demo-key*, puis définissez la valeur de la clé sur *demo-value* :</span><span class="sxs-lookup"><span data-stu-id="1fc3c-139">Use the key name *demo-key*, and set the value of the key to *demo-value*:</span></span>

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

<span data-ttu-id="1fc3c-140">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="1fc3c-140">That's it!</span></span> <span data-ttu-id="1fc3c-141">Vous disposez à présent d’un coffre de clés fonctionnant dans Azure avec un secret.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-141">You now have a key vault running in Azure with a single secret.</span></span> <span data-ttu-id="1fc3c-142">Vous pouvez cloner ce dépôt et le configurer pour utiliser cette ressource dans votre application.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-142">You can now clone this repo and configure it to use this resource in your app.</span></span>

## <a name="get-up-and-running-locally"></a><span data-ttu-id="1fc3c-143">Mise en route et exécution locales</span><span class="sxs-lookup"><span data-stu-id="1fc3c-143">Get up and running locally</span></span>

<span data-ttu-id="1fc3c-144">Cet exemple se fonde sur un exemple d’application disponible sur GitHub. Vous allez donc cloner cette application puis parcourir le code pas à pas.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-144">This example is based on a sample application that's available on GitHub, so you'll clone that application and then step through the code.</span></span> 

1. <span data-ttu-id="1fc3c-145">Clonez le code sur votre ordinateur en entrant les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="1fc3c-145">Clone the code onto your machine by entering the following commands:</span></span>

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="1fc3c-146">Accédez à *src/main/resources/META-INF/microprofile-config.properties*, puis changez les propriétés du fichier *microprofile-config.Properties* en utilisant les valeurs des étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-146">Go to *src/main/resources/META-INF/microprofile-config.properties*, and then change the properties in the *microprofile-config.properties* file by using the values from the previous steps.</span></span>

1. <span data-ttu-id="1fc3c-147">Essayez d’exécuter le serveur en utilisant `mvn clean package payara-micro:start`.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-147">Try running the server by using `mvn clean package payara-micro:start`.</span></span>

1. <span data-ttu-id="1fc3c-148">Essayez d’accéder à [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-148">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser.</span></span> <span data-ttu-id="1fc3c-149">Vous devriez voir une réponse simple montrant les valeurs qui sont lues dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-149">You should see a simple response that demonstrates values that are being read from your key vault.</span></span>

## <a name="summary"></a><span data-ttu-id="1fc3c-150">Résumé</span><span class="sxs-lookup"><span data-stu-id="1fc3c-150">Summary</span></span>

<span data-ttu-id="1fc3c-151">Cet exemple d’application combine l’API de MicroProfile Config, Azure Key Vault et la bibliothèque gratuite et open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault), afin de faciliter l’injection des données de configuration et des secrets dans vos services web MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="1fc3c-151">This sample application combines the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into your MicroProfile web services.</span></span>
