---
title: Guide des développeurs Java des bibliothèques de gestion Azure
description: Modèles et concepts d’utilisation des bibliothèques de gestion Java pour la gestion par Java de vos ressources cloud dans Azure.
keywords: Azure, Java, SDK, API, Maven, Gradle, authentification, Active Directory, principal du service
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: f452468b-7aae-4944-abad-0b1aaf19170d
ms.openlocfilehash: 8b52981ddfaadb7227cea4c7df014011196339cb
ms.sourcegitcommit: 1f6a80e067a8bdbbb4b2da2e2145fda73d5fe65a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/05/2017
ms.locfileid: "26184643"
---
# <a name="patterns-and-best-practices-for-development-with-the-azure-libraries-for-java"></a><span data-ttu-id="68e06-104">Modèles et meilleures pratiques pour le développement avec les bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="68e06-104">Patterns and best practices for development with the Azure libraries for Java</span></span> 

<span data-ttu-id="68e06-105">Cet article répertorie une série de modèles et de meilleures pratiques relatifs à l’utilisation des bibliothèques Azure pour Java dans vos projets.</span><span class="sxs-lookup"><span data-stu-id="68e06-105">This article lists a series of patterns and best practices when using the Azure libraries for Java in your projects.</span></span> <span data-ttu-id="68e06-106">Appuyez-vous sur ces modèles et meilleures pratiques lors de votre développement afin de réduire la quantité de code à gérer et de faciliter l’ajout ou la configuration des ressources supplémentaires dans le cadre des mises à jour futures de vos bibliothèques de gestion.</span><span class="sxs-lookup"><span data-stu-id="68e06-106">Develop with these patterns and guidelines to reduce the amount of code to maintain and make it easier to add or configure additional resources in future updates to the management libraries.</span></span>

## <a name="build-resources-through-a-fluent-interface"></a><span data-ttu-id="68e06-107">Créer des ressources via une interface Fluent</span><span class="sxs-lookup"><span data-stu-id="68e06-107">Build resources through a fluent interface</span></span>

<span data-ttu-id="68e06-108">Une interface Fluent est un modèle qui crée des objets avec une chaîne de méthode qui configure correctement les attributs de l’objet.</span><span class="sxs-lookup"><span data-stu-id="68e06-108">A fluent interface is a pattern that creates objects using a method chain that correctly configures the object's attributes.</span></span> <span data-ttu-id="68e06-109">Pour créer un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="68e06-109">For example, to create a new Azure Storage account</span></span>

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

<span data-ttu-id="68e06-110">Lors de l’utilisation de la chaîne de méthode, votre environnement IDE conseille la méthode suivante pour invoquer la conversation Fluent.</span><span class="sxs-lookup"><span data-stu-id="68e06-110">As you go through the method chain, your IDE suggests the next method to call in the fluent conversation.</span></span>   

![La saisie semi-automatique de commande GIF d’IntelliJ fonctionne via une chaîne Fluent](media/intelliJFluent.gif)

<span data-ttu-id="68e06-112">Enchaînez les méthodes conseillées par l’environnement IDE tant qu’elles restent cohérentes pour la ressource Azure définie.</span><span class="sxs-lookup"><span data-stu-id="68e06-112">Chain the methods suggested by the IDE as long as they make sense for the Azure resource being defined.</span></span> <span data-ttu-id="68e06-113">S’il vous manque une méthode requise dans la chaîne, votre environnement IDE affiche l’erreur en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="68e06-113">If you are missing a required method in the chain your IDE will highlight it with an error.</span></span>

## <a name="resource-collections"></a><span data-ttu-id="68e06-114">Collections de ressources</span><span class="sxs-lookup"><span data-stu-id="68e06-114">Resource collections</span></span>

<span data-ttu-id="68e06-115">La bibliothèque de gestion dispose d’un unique point d’entrée via l’objet `com.microsoft.azure.management.Azure` de niveau supérieur pour créer et mettre à jour les ressources.</span><span class="sxs-lookup"><span data-stu-id="68e06-115">The management library has a single point of entry through the top-level `com.microsoft.azure.management.Azure` object to create and update resources.</span></span> <span data-ttu-id="68e06-116">Sélectionnez le type de ressources à utiliser avec les méthodes de collection de ressources définies dans l’objet `Azure`.</span><span class="sxs-lookup"><span data-stu-id="68e06-116">Select which type of resources to work with using the resource collection methods defined in the `Azure` object.</span></span> <span data-ttu-id="68e06-117">Par exemple, SQL Database :</span><span class="sxs-lookup"><span data-stu-id="68e06-117">For example, SQL Database:</span></span>

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a><span data-ttu-id="68e06-118">Listes et itérations</span><span class="sxs-lookup"><span data-stu-id="68e06-118">Lists and iterations</span></span>

<span data-ttu-id="68e06-119">Chaque collection de ressources possède une méthode `list()` pour renvoyer chaque instance de cette ressource dans votre abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="68e06-119">Each resource collection has a `list()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="68e06-120">Par exemple, `azure.sqlServers().list()` renvoie toutes les bases de données SQL dans l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="68e06-120">For example, `azure.sqlServers().list()` returns all SQL databases in the subscription.</span></span>

<span data-ttu-id="68e06-121">Utilisez la méthode `listByResourceGroup(String groupname)` pour étendre la liste renvoyée à un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) spécifique.</span><span class="sxs-lookup"><span data-stu-id="68e06-121">Use the `listByResourceGroup(String groupname)` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="68e06-122">Recherchez et itérez sur la collection `PagedList<T>` renvoyée, comme vous le feriez pour un élément normal `List<T>` :</span><span class="sxs-lookup"><span data-stu-id="68e06-122">Search and iterate over the returned `PagedList<T>` collection just as you would a normal `List<T>`:</span></span>

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a><span data-ttu-id="68e06-123">Collections renvoyées par des requêtes</span><span class="sxs-lookup"><span data-stu-id="68e06-123">Collections returned from queries</span></span>

<span data-ttu-id="68e06-124">Les bibliothèques de gestion retournent des types de collection spécifiques des requêtes, en fonction de la structure des résultats.</span><span class="sxs-lookup"><span data-stu-id="68e06-124">The management libraries return specific collection types from queries based on the structure of the results.</span></span>

- <span data-ttu-id="68e06-125">`List<T>` : données non triées faciles à chercher et à itérer.</span><span class="sxs-lookup"><span data-stu-id="68e06-125">`List<T>`: Unordered data that is easy to search and iterate over.</span></span>
- <span data-ttu-id="68e06-126">`Map<T>` : les mappages sont des paires clé-valeur dont les clés sont uniques, mais pas forcément les valeurs.</span><span class="sxs-lookup"><span data-stu-id="68e06-126">`Map<T>`: Maps are key/value pairs with unique keys, but not necessarily unique values.</span></span> <span data-ttu-id="68e06-127">Exemple de mappage : des paramètres d’application d’une application web d’App Service.</span><span class="sxs-lookup"><span data-stu-id="68e06-127">An example of a Map would be app settings for an App Service Web App.</span></span>
- <span data-ttu-id="68e06-128">`Set<T>` : les ensembles possèdent des valeurs et des clés uniques.</span><span class="sxs-lookup"><span data-stu-id="68e06-128">`Set<T>`: Sets have unique keys and values.</span></span> <span data-ttu-id="68e06-129">Exemple d’ensemble : des réseaux attachés à une machine virtuelle, dont l’identificateur (la clé) et la configuration (la valeur) sont uniques.</span><span class="sxs-lookup"><span data-stu-id="68e06-129">An example of a Set would be networks attached to a virtual machine, which would have both an unique identifier (the key) and a unique network configuration (the value).</span></span>

## <a name="actionable-verbs"></a><span data-ttu-id="68e06-130">Verbes actionnables</span><span class="sxs-lookup"><span data-stu-id="68e06-130">Actionable verbs</span></span>

<span data-ttu-id="68e06-131">Les méthodes dont les noms contiennent des verbes prennent effet immédiatement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="68e06-131">Methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="68e06-132">Ces méthodes fonctionnent de façon synchrone et empêchent l’exécution dans le thread actuel jusqu’à ce qu’elles se terminent.</span><span class="sxs-lookup"><span data-stu-id="68e06-132">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="68e06-133">Verbe</span><span class="sxs-lookup"><span data-stu-id="68e06-133">Verb</span></span>   |  <span data-ttu-id="68e06-134">Exemple d’utilisation</span><span class="sxs-lookup"><span data-stu-id="68e06-134">Sample Usage</span></span> |
|--------|---------------|
| <span data-ttu-id="68e06-135">create</span><span class="sxs-lookup"><span data-stu-id="68e06-135">create</span></span> | `azure.virtualMachines().create(listOfVMCreatables)` |
| <span data-ttu-id="68e06-136">apply</span><span class="sxs-lookup"><span data-stu-id="68e06-136">apply</span></span>  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| <span data-ttu-id="68e06-137">delete</span><span class="sxs-lookup"><span data-stu-id="68e06-137">delete</span></span> | `azure.disks().deleteById(id)` | 
| <span data-ttu-id="68e06-138">list</span><span class="sxs-lookup"><span data-stu-id="68e06-138">list</span></span>   | `azure.sqlServers().list()` | 
| <span data-ttu-id="68e06-139">get</span><span class="sxs-lookup"><span data-stu-id="68e06-139">get</span></span>    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="68e06-140">`define()` et `update()` sont des verbes mais ne bloquent pas, sauf s’ils sont suivis par `create()` ou `apply()`.</span><span class="sxs-lookup"><span data-stu-id="68e06-140">`define()` and `update()` are verbs but do not block unless followed by a `create()` or `apply()`.</span></span>
 
<span data-ttu-id="68e06-141">Les versions asynchrones de certaines de ces méthodes peuvent apparaître avec le suffixe `Async` à l’aide d’[extensions réactives](https://github.com/ReactiveX/RxJava).</span><span class="sxs-lookup"><span data-stu-id="68e06-141">Asynchronous versions of some of these  methods exist with the `Async` suffix using [Reactive extensions](https://github.com/ReactiveX/RxJava).</span></span> 

<span data-ttu-id="68e06-142">Certains objets disposent d’autres méthodes qui modifient l’état de la ressource dans Azure.</span><span class="sxs-lookup"><span data-stu-id="68e06-142">Some objects have other methods with that change the state of the resource in Azure.</span></span> <span data-ttu-id="68e06-143">Par exemple, la méthode `restart()` sur une `VirtualMachine`.</span><span class="sxs-lookup"><span data-stu-id="68e06-143">For example, `restart()` on a `VirtualMachine`.</span></span>

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
<span data-ttu-id="68e06-144">Ces méthodes ne disposent pas toujours de versions asynchrones et bloquent l’exécution sur leur thread jusqu’à ce qu’elles se terminent.</span><span class="sxs-lookup"><span data-stu-id="68e06-144">These methods do not always have asynchronous versions and will block execution on their thread until they complete.</span></span>

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a><span data-ttu-id="68e06-145">Création de ressources différées</span><span class="sxs-lookup"><span data-stu-id="68e06-145">Lazy resource creation</span></span>

<span data-ttu-id="68e06-146">La création de ressources Azure peut constituer un défi lorsqu’une nouvelle ressource dépend d’une autre ressource qui n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="68e06-146">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="68e06-147">Exemple : la réservation d’une adresse IP publique et la configuration d’un disque lors de la création d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="68e06-147">An example of this scenario is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="68e06-148">Vous ne souhaitez pas vérifier la réservation d’adresse ou la création du disque, vous souhaitez juste vous assurer que la machine virtuelle dispose de ces ressources à sa création.</span><span class="sxs-lookup"><span data-stu-id="68e06-148">You don't want to verify reserving the address or the creating the disk, you just want to ensure the virtual machine has those resources when it is created.</span></span>

<span data-ttu-id="68e06-149">Les objets `Creatable<T>` vous permettent de définir des ressources Azure à utiliser dans votre code sans attendre leur création dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="68e06-149">`Creatable<T>` objects let you define Azure resources for use in your code without waiting around for them to be created in your subscription.</span></span> <span data-ttu-id="68e06-150">Les bibliothèques de gestion reportent la création d’objets `Creatable<T>` tant qu’ils ne sont pas nécessaires.</span><span class="sxs-lookup"><span data-stu-id="68e06-150">The management libraries defer creating  `Creatable<T>` objects until they are needed.</span></span>

<span data-ttu-id="68e06-151">Générez des objets `Creatable<T>` pour des ressources Azure via le verbe `define()` :</span><span class="sxs-lookup"><span data-stu-id="68e06-151">Generate `Creatable<T>` objects for Azure resources through the `define()` verb:</span></span>

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

<span data-ttu-id="68e06-152">Dans cet exemple, la ressource Azure définie par l’objet `Creatable<PublicIPAddress>` n’existe pas encore dans votre abonnement lors de l’exécution du code.</span><span class="sxs-lookup"><span data-stu-id="68e06-152">The Azure resource defined by the `Creatable<PublicIPAddress>` in this example does not yet exist in your subscription when this code executes.</span></span>  <span data-ttu-id="68e06-153">Utilisez l’objet `publicIPAddressCreatable` pour créer d’autres ressources Azure avec cette adresse IP.</span><span class="sxs-lookup"><span data-stu-id="68e06-153">Use the `publicIPAddressCreatable` object to create other Azure resources with this IP address.</span></span> 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

<span data-ttu-id="68e06-154">Les ressources `Creatable<T>` sont générées dans votre abonnement à chaque fois qu’une ressource utilisant l’objet est créée dans Azure à l’aide de la méthode `create()`.</span><span class="sxs-lookup"><span data-stu-id="68e06-154">The `Creatable<T>` resources are generated in your subscription when any resource that is defined using the object is built in Azure using `create()`.</span></span> <span data-ttu-id="68e06-155">Suite de l’exemple avec l’adresse IP et la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="68e06-155">Continuing the IP address and virtual machine example:</span></span>

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

<span data-ttu-id="68e06-156">L’utilisation des appels `create()` sur un objet `Creatable<T>` renvoie un objet `CreatedResources` et non un objet de ressource unique.</span><span class="sxs-lookup"><span data-stu-id="68e06-156">Passing the `Creatable<T>` to `create()` calls returns a `CreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="68e06-157">L’objet `CreatedResources<T>` vous permet d’accéder à toutes les ressources créées par l’appel `create()`, pas uniquement à la ressource définie dans l’appel.</span><span class="sxs-lookup"><span data-stu-id="68e06-157">The `CreatedResources<T>` object lets you access all resources created by the `create()` call, not just the typed resource in the call.</span></span> <span data-ttu-id="68e06-158">Pour accéder à l’adresse IP publique créée dans Azure pour la machine virtuelle créée dans l’exemple ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="68e06-158">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a><span data-ttu-id="68e06-159">Gestion des exceptions</span><span class="sxs-lookup"><span data-stu-id="68e06-159">Exception handling</span></span>

<span data-ttu-id="68e06-160">Étendue des classes d’exception des bibliothèques de gestion sur `com.microsoft.rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="68e06-160">The management libraries' Exception classes extend `com.microsoft.rest.RestException`.</span></span> <span data-ttu-id="68e06-161">Interceptez des exceptions générées par les bibliothèques de gestion avec un bloc `catch (RestException exception)` après l’instruction pertinente `try`.</span><span class="sxs-lookup"><span data-stu-id="68e06-161">Catch exceptions generated by the management libraries with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-trace"></a><span data-ttu-id="68e06-162">Journaux et suivi</span><span class="sxs-lookup"><span data-stu-id="68e06-162">Logs and trace</span></span>

<span data-ttu-id="68e06-163">Configurez la quantité de journalisation de la bibliothèque de gestion lorsque vous créez l’objet de point d’entrée `Azure` à l’aide de `withLogLevel()`.</span><span class="sxs-lookup"><span data-stu-id="68e06-163">Configure the amount of logging from the management library when you build the entry point `Azure` object using `withLogLevel()`.</span></span> <span data-ttu-id="68e06-164">Voici les niveaux de trace existants :</span><span class="sxs-lookup"><span data-stu-id="68e06-164">The following trace levels exist:</span></span>

| <span data-ttu-id="68e06-165">Niveau de trace</span><span class="sxs-lookup"><span data-stu-id="68e06-165">Trace level</span></span> | <span data-ttu-id="68e06-166">Journalisation activée</span><span class="sxs-lookup"><span data-stu-id="68e06-166">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="68e06-167">com.microsoft.rest.LogLevel.NONE</span><span class="sxs-lookup"><span data-stu-id="68e06-167">com.microsoft.rest.LogLevel.NONE</span></span> | <span data-ttu-id="68e06-168">Aucune sortie</span><span class="sxs-lookup"><span data-stu-id="68e06-168">No output</span></span>
| <span data-ttu-id="68e06-169">com.microsoft.rest.LogLevel.BASIC</span><span class="sxs-lookup"><span data-stu-id="68e06-169">com.microsoft.rest.LogLevel.BASIC</span></span> | <span data-ttu-id="68e06-170">Consigne les URL vers des appels REST sous-jacents, des codes de réponse et des durées</span><span class="sxs-lookup"><span data-stu-id="68e06-170">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="68e06-171">com.microsoft.rest.LogLevel.BODY</span><span class="sxs-lookup"><span data-stu-id="68e06-171">com.microsoft.rest.LogLevel.BODY</span></span> | <span data-ttu-id="68e06-172">Fonctions du niveau de consignation BASIC, ajoutées à des corps de demande et de réponse aux appels REST</span><span class="sxs-lookup"><span data-stu-id="68e06-172">Everything in BASIC plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="68e06-173">com.microsoft.rest.LogLevel.HEADERS</span><span class="sxs-lookup"><span data-stu-id="68e06-173">com.microsoft.rest.LogLevel.HEADERS</span></span> | <span data-ttu-id="68e06-174">Fonctions du niveau de consignation BASIC, ajoutées aux en-têtes de demande et de réponse aux appels REST</span><span class="sxs-lookup"><span data-stu-id="68e06-174">Everything in BASIC plus the request and response headers REST calls</span></span>
| <span data-ttu-id="68e06-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span><span class="sxs-lookup"><span data-stu-id="68e06-175">com.microsoft.rest.LogLevel.BODY_AND_HEADERS</span></span> | <span data-ttu-id="68e06-176">Fonction des niveaux de consignation BODY et HEADERS</span><span class="sxs-lookup"><span data-stu-id="68e06-176">Everything in both BODY and HEADERS log level</span></span>

<span data-ttu-id="68e06-177">Liez une [implémentation de journalisation SLF4J](https://www.slf4j.org/manual.html) si vous avez besoin de consigner une sortie dans un framework de journalisation tel que [Log4J 2](https://logging.apache.org/log4j/2.x/).</span><span class="sxs-lookup"><span data-stu-id="68e06-177">Bind a [SLF4J logging implementation](https://www.slf4j.org/manual.html) if you need to log output to a logging framework like [Log4J 2](https://logging.apache.org/log4j/2.x/).</span></span>