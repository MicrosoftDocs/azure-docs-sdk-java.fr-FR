---
title: "Concepts et modèles d’utilisation des bibliothèques de gestion Azure pour Java"
description: 
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
ms.openlocfilehash: 052c4de1e8f9ff0ece5f36d1c3514bad8c04cfec
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-concepts"></a>Concepts de la bibliothèque de gestion Azure

## <a name="build-resources-through-a-fluent-interface"></a>Créer des ressources via une interface Fluent

Une interface Fluent est un modèle qui crée des objets avec une chaîne de méthode qui configure correctement les attributs de l’objet. Pour créer un compte de stockage Azure

```java
StorageAccount storage = azure.storageAccounts().define(storageAccountName)
    .withRegion(region)
    .withNewResourceGroup(resourceGroup)
    .create();
```

Lors de l’utilisation de la chaîne de méthode, votre environnement IDE conseille la méthode suivante pour invoquer la conversation Fluent.   

![La saisie semi-automatique de commande GIF d’IntelliJ fonctionne via une chaîne Fluent](media/intelliJFluent.gif)

Enchaînez les méthodes conseillées par l’environnement IDE tant qu’elles restent cohérentes pour la ressource Azure définie. S’il vous manque une méthode requise dans la chaîne, votre environnement IDE affiche l’erreur en surbrillance.

## <a name="resource-collections"></a>Collections de ressources

La bibliothèque de gestion dispose d’un unique point d’entrée via l’objet `com.microsoft.azure.management.Azure` de niveau supérieur pour créer et mettre à jour les ressources. Sélectionnez le type de ressources à utiliser avec les méthodes de collection de ressources définies dans l’objet `Azure`. Par exemple, SQL Database :

```java
SqlServer sqlServer = azure.sqlServers().define(sqlServerName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName)
    .withAdministratorLogin(administratorLogin)
    .withAdministratorPassword(administratorPassword)
    .create();
```

## <a name="lists-and-iterations"></a>Listes et itérations

Chaque collection de ressources possède une méthode `list()` pour renvoyer chaque instance de cette ressource dans votre abonnement actuel. Par exemple, `azure.sqlServers().list()` renvoie toutes les bases de données SQL dans l’abonnement.

Utilisez la méthode `listByResourceGroup(String groupname)` pour étendre la liste renvoyée à un [groupe de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups) spécifique.  

Recherchez et itérez sur la collection `PagedList<T>` renvoyée, comme vous le feriez pour un élément normal `List<T>` :

```java
PagedList<VirtualMachine> vms = azure.virtualMachines().list();
for (VirtualMachine vm : vms) {
    System.out.println("Found virtual machine with ID " + vm.id());
}
```   

## <a name="collections-returned-from-queries"></a>Collections renvoyées par des requêtes

Les bibliothèques de gestion retournent des types de collection spécifiques des requêtes, en fonction de la structure des résultats.

- `List<T>` : données non triées faciles à chercher et à itérer.
- `Map<T>` : les mappages sont des paires clé-valeur dont les clés sont uniques, mais pas forcément les valeurs. Exemple de mappage : des paramètres d’application d’une application web d’App Service.
- `Set<T>` : les ensembles possèdent des valeurs et des clés uniques. Exemple d’ensemble : des réseaux attachés à une machine virtuelle, dont l’identificateur (la clé) et la configuration (la valeur) sont uniques.

## <a name="actionable-verbs"></a>Verbes actionnables

Les méthodes dont les noms contiennent des verbes prennent effet immédiatement dans Azure. Ces méthodes fonctionnent de façon synchrone et empêchent l’exécution dans le thread actuel jusqu’à ce qu’elles se terminent. 

| Verbe   |  Exemple d’utilisation |
|--------|---------------|
| create | `azure.virtualMachines().create(listOfVMCreatables)` |
| apply  | `virtualMachineScaleSet.update().withCapacity(6).apply()` |
| delete | `azure.disks().deleteById(id)` | 
| list   | `azure.sqlServers().list()` | 
| get    | `VirtualMachine vm  = azure.virtualMachines().getByResourceGroup(group, vmName)` |

>[!NOTE]
> `define()` et `update()` sont des verbes mais ne bloquent pas, sauf s’ils sont suivis par `create()` ou `apply()`.
 
Les versions asynchrones de certaines de ces méthodes peuvent apparaître avec le suffixe `Async` à l’aide d’[extensions réactives](https://github.com/ReactiveX/RxJava). 

Certains objets disposent d’autres méthodes qui modifient l’état de la ressource dans Azure. Par exemple, la méthode `restart()` sur une `VirtualMachine`.

```java
VirtualMachine vmToRestart = azure.getVirtualMachines().getById(id);
vmToRestart.restart();
```
Ces méthodes ne disposent pas toujours de versions asynchrones et bloquent l’exécution sur leur thread jusqu’à ce qu’elles se terminent.

<a name="Creatables"></a>

## <a name="lazy-resource-creation"></a>Création de ressources différées

La création de ressources Azure peut constituer un défi lorsqu’une nouvelle ressource dépend d’une autre ressource qui n’existe pas. Exemple : la réservation d’une adresse IP publique et la configuration d’un disque lors de la création d’une machine virtuelle. Vous ne souhaitez pas vérifier la réservation d’adresse ou la création du disque, vous souhaitez juste vous assurer que la machine virtuelle dispose de ces ressources à sa création.

Les objets `Creatable<T>` vous permettent de définir des ressources Azure à utiliser dans votre code sans attendre leur création dans votre abonnement. Les bibliothèques de gestion reportent la création d’objets `Creatable<T>` tant qu’ils ne sont pas nécessaires.

Générez des objets `Creatable<T>` pour des ressources Azure via le verbe `define()` :

```java
Creatable<PublicIPAddress> publicIPAddressCreatable = azure.publicIPAddresses().define(publicIPAddressName)
    .withRegion(Region.US_EAST)
    .withNewResourceGroup(rgName);
```

Dans cet exemple, la ressource Azure définie par l’objet `Creatable<PublicIPAddress>` n’existe pas encore dans votre abonnement lors de l’exécution du code.  Utilisez l’objet `publicIPAddressCreatable` pour créer d’autres ressources Azure avec cette adresse IP. 

```java
Creatable<VirtualMachine> vmCreatable = azure.virtualMachines().define("creatableVM")
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
```

Les ressources `Creatable<T>` sont générées dans votre abonnement à chaque fois qu’une ressource utilisant l’objet est créée dans Azure à l’aide de la méthode `create()`. Suite de l’exemple avec l’adresse IP et la machine virtuelle :

```java
CreatedResources<VirtualMachine> virtualMachine = azure.virtualMachines().create(vmCreatable);
```

L’utilisation des appels `create()` sur un objet `Creatable<T>` renvoie un objet `CreatedResources` et non un objet de ressource unique.  L’objet `CreatedResources<T>` vous permet d’accéder à toutes les ressources créées par l’appel `create()`, pas uniquement à la ressource définie dans l’appel. Pour accéder à l’adresse IP publique créée dans Azure pour la machine virtuelle créée dans l’exemple ci-dessus :

```java
PublicIPAddress pip = (PublicIPAddress) virtualMachine.createdRelatedResource(publicIPAddressCreatable.key());
```    

## <a name="exception-handling"></a>Gestion des exceptions

Étendue des classes d’exception des bibliothèques de gestion sur `com.microsoft.rest.RestException`. Interceptez des exceptions générées par les bibliothèques de gestion avec un bloc `catch (RestException exception)` après l’instruction pertinente `try`.

## <a name="logs-and-trace"></a>Journaux et suivi

Configurez la quantité de journalisation de la bibliothèque de gestion lorsque vous créez l’objet de point d’entrée `Azure` à l’aide de `withLogLevel()`. Voici les niveaux de trace existants :

| Niveau de trace | Journalisation activée 
| ------------ | ---------------
| com.microsoft.rest.LogLevel.NONE | Aucune sortie
| com.microsoft.rest.LogLevel.BASIC | Consigne les URL vers des appels REST sous-jacents, des codes de réponse et des durées
| com.microsoft.rest.LogLevel.BODY | Fonctions du niveau de consignation BASIC, ajoutées à des corps de demande et de réponse aux appels REST
| com.microsoft.rest.LogLevel.HEADERS | Fonctions du niveau de consignation BASIC, ajoutées aux en-têtes de demande et de réponse aux appels REST
| com.microsoft.rest.LogLevel.BODY_AND_HEADERS | Fonction des niveaux de consignation BODY et HEADERS

Liez une [implémentation de journalisation SLF4J](https://www.slf4j.org/manual.html) si vous avez besoin de consigner une sortie dans un framework de journalisation tel que [Log4J 2](https://logging.apache.org/log4j/2.x/).