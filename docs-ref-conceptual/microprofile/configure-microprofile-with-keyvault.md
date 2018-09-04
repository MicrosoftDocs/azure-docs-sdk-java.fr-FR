---
title: Configurer MicroProfile avec Azure Key Vault
description: Découvrez comment injecter des clés secrètes dans un service web de MicroProfile avec Azure Key Vault
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
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240822"
---
# <a name="configure-microprofile-with-azure-key-vault"></a><span data-ttu-id="65dfc-103">Configurer MicroProfile avec Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="65dfc-103">Configure MicroProfile with Azure Key Vault</span></span>

<span data-ttu-id="65dfc-104">Ce tutoriel vous présentera comment configurer une application [MicroProfile](http://microprofile.io) pour extraire des clés secrètes à partir d’[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) à l’aide des [API MicroProfile Config](https://microprofile.io/project/eclipse/microprofile-config) pour créer une connexion directe vers Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-104">This tutorial will demonstrate how to configure a [MicroProfile](http://microprofile.io) application to retrieve secrets from [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) using the [MicroProfile Config APIs](https://microprofile.io/project/eclipse/microprofile-config) to create a direct connection to Azure Key Vault.</span></span> <span data-ttu-id="65dfc-105">Avec les API MicroProfile Config, les développeurs bénéficient d’une API standard pour extraire et injecter des données de configuration dans leurs microservices.</span><span class="sxs-lookup"><span data-stu-id="65dfc-105">By using the MicroProfile Config APIs, developers benefit from a standard API for retrieving and injecting configuration data into their microservices.</span></span>

<span data-ttu-id="65dfc-106">Avant de rentrer dans le vif du sujet, jetons un rapide coup d’œil à ce que la combinaison d’Azure Key Vault et de l’API MicroProfile Config nous permet d’écrire dans notre code.</span><span class="sxs-lookup"><span data-stu-id="65dfc-106">Before we dive in, lets quickly take a look at what a combination of Azure Key Vault and the MicroProfile Config API enables us to write in our code.</span></span> <span data-ttu-id="65dfc-107">Voici un extrait de code d’un champ au sein d’une classe annotée avec `@Inject` et `@ConfigProperty`.</span><span class="sxs-lookup"><span data-stu-id="65dfc-107">Here's a code snippet of a field in a class that has been annotated with `@Inject` and `@ConfigProperty`.</span></span> <span data-ttu-id="65dfc-108">Le `name` spécifié dans l’annotation correspond au nom de la propriété à rechercher dans Azure Key Vault, et le `defaultValue` correspond à ce qui sera configuré si la clé n’est pas découverte.</span><span class="sxs-lookup"><span data-stu-id="65dfc-108">The `name` specified in the annotation is the name of the property to look up in Azure Key Vault, and the `defaultValue` is what will be set if the key is not discovered.</span></span> <span data-ttu-id="65dfc-109">À la fin de l’opération, la valeur stockée dans Azure Key Vault, ou la valeur par défaut, est automatiquement injectée dans le champ lors de l’exécution, ce qui simplifie la tâche des développeurs, leur évitant ainsi le transfert de valeurs pour les méthodes constructors et setter, désormais prise en charge par MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="65dfc-109">The end result is that the value stored in Azure Key Vault, or the default value, will be injected automatically into the field at runtime, simplifying the life of developers as they no longer need to pass values around in constuctors and setter methods, instead leaving it to MicroProfile to handle.</span></span>

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

<span data-ttu-id="65dfc-110">Il est également possible d’accéder directement à MicroProfile Config, afin d’effectuer des requêtes de clés secrètes si nécessaire, par exemple :</span><span class="sxs-lookup"><span data-stu-id="65dfc-110">It is also possible to access the MicroProfile config directly, to request secrets as necessary, e.g.:</span></span>

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

<span data-ttu-id="65dfc-111">Cet exemple utilise [Payara Micro](https://www.payara.fish/payara_micro) et [MicroProfile](https://microprofile.io/) pour créer un petit fichier Java au format war pouvant être exécuté localement sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="65dfc-111">This sample makes use of [Payara Micro](https://www.payara.fish/payara_micro) and [MicroProfile](https://microprofile.io/) to create a tiny Java war file that can be run locally on your machine.</span></span> <span data-ttu-id="65dfc-112">Il n’illustre pas la procédure d’ancrage ni l’envoi de code vers Azure. Vous trouverez en fin de tutoriel une section de liens renvoyant vers d’autres tutoriels vous expliquant ces opérations.</span><span class="sxs-lookup"><span data-stu-id="65dfc-112">It does not demonstrate how to dockerise or push the code to Azure, but the links section at the end of this tutorial has links to other useful tutorials that explain this.</span></span>

<span data-ttu-id="65dfc-113">Cet exemple utilise une bibliothèque gratuite en open source créant une source de configuration (via l’API MicroProfile Config) pour Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-113">This sample makes use of a free and open source library that creats a config source (using the MicroProfile Config API) for Azure Key Vault.</span></span> <span data-ttu-id="65dfc-114">Pour en apprendre davantage sur cette bibliothèque et passer en revue le code, consultez la [page du projet GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span><span class="sxs-lookup"><span data-stu-id="65dfc-114">You can learn more about this library, and review the code, on the [project GitHub page](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault).</span></span> <span data-ttu-id="65dfc-115">Grâce à cette bibliothèque, vous pouvez utiliser le code de ce tutoriel pour configurer la bibliothèque et injecter des clés à votre code, sans qu’il n’y ait besoin de rédiger un code spécifique à Azure.</span><span class="sxs-lookup"><span data-stu-id="65dfc-115">By using this library, the code in this tutorial can simply focus on configuration of the library, followed by injecting keys into your code, and we don't need to write any Azure-specific code.</span></span>

<span data-ttu-id="65dfc-116">Voici les étapes nécessaires à l’exécution de ce code sur votre ordinateur local, la première consistant à créer une ressource pour Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-116">Here are the steps required to run this code on your local machine, starting with creating an Azure Key Vault resource.</span></span>

## <a name="creating-an-azure-key-vault-resource"></a><span data-ttu-id="65dfc-117">Création d’une ressource Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="65dfc-117">Creating an Azure Key Vault resource</span></span>

<span data-ttu-id="65dfc-118">Nous utiliserons l’interface Azure CLI pour créer la ressource Azure Key Vault et remplir cette dernière avec une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="65dfc-118">We will use the Azure CLI to create the Azure Key Vault resource and populate it with one secret.</span></span>

1. <span data-ttu-id="65dfc-119">Tout d’abord, il nous faut créer un principal de service Azure.</span><span class="sxs-lookup"><span data-stu-id="65dfc-119">Firstly, lets create an Azure service principal.</span></span> <span data-ttu-id="65dfc-120">Celui-ci nous fournira l’ID client ainsi que sa clé qui permettront d’accéder à Key Vault :</span><span class="sxs-lookup"><span data-stu-id="65dfc-120">This will provide us with the client ID and key we need to access Key Vault:</span></span>

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

<span data-ttu-id="65dfc-121">Commençons par utiliser `microprofile-keyvault-service-principal` comme nom du principal de service de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="65dfc-121">Lets say we use `microprofile-keyvault-service-principal` for the service principal name in the previous step.</span></span> <span data-ttu-id="65dfc-122">La réponse d’Azure à cette action s’affichera sous la forme suivante (affichage partiel) :</span><span class="sxs-lookup"><span data-stu-id="65dfc-122">The response from Azure for doing this will be in the following, slightly censored, form:</span></span>

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

<span data-ttu-id="65dfc-123">Remarquez particulièrement les valeurs `appID` et `password`. Nous les utiliserons plus tard, respectivement comme `client ID` et `key`.</span><span class="sxs-lookup"><span data-stu-id="65dfc-123">Of particular note here is the `appID` and `password` values - these are what we will use later on as `client ID` and `key`, respectively.</span></span>

<span data-ttu-id="65dfc-124">À présent que nous avons créé un principal de service, nous pouvons éventuellement créer un groupe de ressources (si vous disposez déjà d’un groupe que vous souhaitez utiliser, vous pouvez passer cette étape).</span><span class="sxs-lookup"><span data-stu-id="65dfc-124">Now that we have created a service principal, we can optionally create a resource group (if you already have one you want to use, you can skip this step).</span></span> <span data-ttu-id="65dfc-125">Notez que vous pouvez obtenir une liste des emplacements des groupes de ressources à l’aide de la requête `az account list-locations` et utiliser la valeur `name` de cette liste pour spécifier l’emplacement de création du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="65dfc-125">Note that to get a list of resource group locations, you can call `az account list-locations` and use the `name` value from that list to specify where the resource group should be created.</span></span>

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

<span data-ttu-id="65dfc-126">Nous allons désormais créer une ressource Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-126">We now create an Azure Key Vault resource.</span></span> <span data-ttu-id="65dfc-127">Notez que le nom du Key Vault nous servira plus tard pour nous référer au coffre de clés, nous vous conseillons donc de choisir un nom facile à retenir.</span><span class="sxs-lookup"><span data-stu-id="65dfc-127">Note that the Key Vault name is what you will use to reference the key vault later, so choose something memorable.</span></span>

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

<span data-ttu-id="65dfc-128">Nous avons également besoin d’accorder les autorisations appropriées au principal de service que nous avons précédemment créé, de sorte qu’il puisse accéder aux clés secrètes Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-128">We also need to grant the appropriate permissions to the service principal we created earlier, so that it may access the Key Vault secrets.</span></span> <span data-ttu-id="65dfc-129">Notez que la valeur de l’ID de l’application correspond à la valeur `appId` attribuée en amont de la création du principal de service (à savoir `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`, mais utilisez la valeur indiquée en sortie sur votre terminal).</span><span class="sxs-lookup"><span data-stu-id="65dfc-129">Note that the appID value is the `appId` value from above where we created the service principal (that is, `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79` - but use the value from your terminal output).</span></span>

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

<span data-ttu-id="65dfc-130">C’est le moment pour nous d’envoyer une clé secrète dans Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-130">We are now at the point where we can push a secret into Key Vault.</span></span> <span data-ttu-id="65dfc-131">Utilisons le nom de clé `demo-key`, puis définissons la valeur de la clé sur `demo-value` :</span><span class="sxs-lookup"><span data-stu-id="65dfc-131">Lets use the key name `demo-key`, and set the value of the key to be `demo-value`:</span></span>

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

<span data-ttu-id="65dfc-132">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="65dfc-132">That's it!</span></span> <span data-ttu-id="65dfc-133">Nous disposons à présent d’un Key Vault fonctionnant sur Azure avec une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="65dfc-133">We now have Key Vault running in Azure with a single secret.</span></span> <span data-ttu-id="65dfc-134">Nous pouvons à présent cloner ce référentiel et le configurer pour utiliser cette ressource dans notre application.</span><span class="sxs-lookup"><span data-stu-id="65dfc-134">We can now clone this repo and configure it to use this resource in our app.</span></span>

## <a name="getting-up-and-running-locally"></a><span data-ttu-id="65dfc-135">Mise en route et exécution en local</span><span class="sxs-lookup"><span data-stu-id="65dfc-135">Getting up and running locally</span></span>

<span data-ttu-id="65dfc-136">Cet exemple se fonde sur un exemple d’application disponible sur GitHub, nous pouvons donc le cloner et parcourir le code pas à pas.</span><span class="sxs-lookup"><span data-stu-id="65dfc-136">This example is based on a sample application available on GitHub, so we will clone that and then step through the code.</span></span> <span data-ttu-id="65dfc-137">Suivez les étapes ci-dessous pour cloner le code sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="65dfc-137">Follow the steps below to get the code cloned onto your machine:</span></span>

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. <span data-ttu-id="65dfc-138">Accédez à `src/main/resources/META-INF/microprofile-config.properties` et modifiez les propriétés dans le fichier microprofile-config.properties avec les détails renseignés plus haut.</span><span class="sxs-lookup"><span data-stu-id="65dfc-138">Navigate to `src/main/resources/META-INF/microprofile-config.properties` and change the properties in microprofile-config.properties file with details from above.</span></span>

1. <span data-ttu-id="65dfc-139">Essayez de faire fonctionner le serveur en utilisant `mvn clean package payara-micro:start`</span><span class="sxs-lookup"><span data-stu-id="65dfc-139">Try running the server using `mvn clean package payara-micro:start`</span></span>

1. <span data-ttu-id="65dfc-140">Essayez d’accéder à [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) dans votre navigateur web. Vous devriez voir une réponse simple illustrant les valeurs lues depuis Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="65dfc-140">Try accessing [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) in your web browser - you should see a simple response that demonstrates values being read from Azure Key Vault.</span></span>

## <a name="summary"></a><span data-ttu-id="65dfc-141">Résumé</span><span class="sxs-lookup"><span data-stu-id="65dfc-141">Summary</span></span>

<span data-ttu-id="65dfc-142">Cet exemple d’application mêle l’API de MicroProfile Config, d’Azure Key Vault et de la bibliothèque gratuite et open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault), afin de faciliter l’injection de données de configuration et de clés secrètes dans nos services web MicroProfile.</span><span class="sxs-lookup"><span data-stu-id="65dfc-142">This sample application bakes together the MicroProfile Config API, Azure Key Vault, and the free and open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault) library to enable easy injection of configuration data and secrets into our MicroProfile web services.</span></span>
