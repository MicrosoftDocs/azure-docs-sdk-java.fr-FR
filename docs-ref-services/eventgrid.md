---
title: Bibliothèques Azure Event Grid pour Java
description: Documentation sur les bibliothèques Azure Event Grid pour Java
keywords: Azure, Java, SDK, API, Event Grid, messagerie, basé sur les événements
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 07/11/2017
ms.topic: managed-reference
ms.devlang: java
ms.service: event-grid
ms.openlocfilehash: 35acbdeede2fbc541128029ad43f149209a057c4
ms.sourcegitcommit: db36eeb667a0bfe6d113953bb0583240db61b0f4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50134627"
---
# <a name="azure-event-grid-libraries-for-java"></a><span data-ttu-id="e7572-104">Bibliothèques Azure Event Grid pour Java</span><span class="sxs-lookup"><span data-stu-id="e7572-104">Azure Event Grid libraries for Java</span></span>

<span data-ttu-id="e7572-105">Créez des applications pilotées par des événements, qui écoutent et réagissent aux événements venant des services Azure et de sources personnalisées à l’aide d’une gestion simple des événements basés sur HTTP avec Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e7572-105">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="e7572-106">[En savoir plus](/azure/event-grid/overview) sur Azure Event Grid et la prise en main avec le [didacticiel des événements de stockage d’objets Blob Azure](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="e7572-106">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="e7572-107">Kit de développement logiciel (SDK) client</span><span class="sxs-lookup"><span data-stu-id="e7572-107">Client SDK</span></span>

<span data-ttu-id="e7572-108">Créez des événements, authentifiez-vous et faites des publications dans des rubriques à l’aide du kit de développement logiciel client d’Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e7572-108">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="e7572-109">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e7572-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventgrid</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="publish-events"></a><span data-ttu-id="e7572-110">Publier des événements</span><span class="sxs-lookup"><span data-stu-id="e7572-110">Publish events</span></span>

<span data-ttu-id="e7572-111">Le code suivant s’authentifie auprès d’Azure et publie un `List` d’événements `EventGridEvent` d’un type personnalisé (dans cet exemple, `Contoso.Items.ItemsReceived` ) sur une rubrique.</span><span class="sxs-lookup"><span data-stu-id="e7572-111">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceived` ) to a topic.</span></span> <span data-ttu-id="e7572-112">La clé de la rubrique et l’adresse du point de terminaison utilisées dans cet exemple peuvent être récupérées à partir d’Azure CLI :</span><span class="sxs-lookup"><span data-stu-id="e7572-112">The topic key and endpoint address used in the sample can be retrieved from the Azure CLI:</span></span>

```azurecli-interactive
az eventgrid topic show -g gridResourceGroup -n topicName
az eventgrid topic key list -g gridResourceGroup -n topicName
```

```java
// Create an event grid client.
TopicCredentials topicCredentials = new TopicCredentials(System.getenv("EVENTGRID_TOPIC_KEY"));
EventGridClient client = new EventGridClientImpl(topicCredentials);

// Publish custom events to the EventGrid.
System.out.println("Publish custom events to the EventGrid");
List<EventGridEvent> eventsList = new ArrayList<>();
for (int i = 0; i < 5; i++) {
    eventsList.add(new EventGridEvent(
        UUID.randomUUID().toString(),
        String.format("Door%d", i),
        new ContosoItemReceivedEventData("Contoso Item SKU #1"),
        "Contoso.Items.ItemReceived",
        DateTime.now(),
        "2.0"
    ));
}

String eventGridEndpoint = String.format("https://%s/", new URI(System.getenv("EVENTGRID_TOPIC_ENDPOINT")).getHost());

client.publishEvents(eventGridEndpoint, eventsList);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7572-113">Explorer les API clientes Event Grid</span><span class="sxs-lookup"><span data-stu-id="e7572-113">Explore the Event Grid Client APIs</span></span>](/java/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="e7572-114">Kit de développement logiciel (SDK) de gestion</span><span class="sxs-lookup"><span data-stu-id="e7572-114">Management SDK</span></span>

<span data-ttu-id="e7572-115">Créez, mettez à jour et supprimez des instances, des rubriques et des abonnements avec le kit de développement logiciel (SDK) de gestion Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e7572-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the Event Grid management SDK.</span></span>

<span data-ttu-id="e7572-116">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="e7572-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.16.0</version>
</dependency>
```   

<span data-ttu-id="e7572-117">L’exemple suivant crée un abonnement Event Grid, tiré des [exemples EventGrid Java](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span><span class="sxs-lookup"><span data-stu-id="e7572-117">The following example creates an Event Grid subscription, taken from the [EventGrid Java samples](https://github.com/Azure-Samples/event-grid-java-publish-consume-events)</span></span>

```java
// Create an event grid subscription.
//
System.out.println("Creating an Azure EventGrid Subscription");

EventSubscription eventSubscription = eventGridManager.eventSubscriptions().define(eventSubscriptionName)
    .withScope(eventGridTopic.id())
    .withDestination(new EventHubEventSubscriptionDestination()
        .withResourceId(eventHub.id()))
    .withFilter(new EventSubscriptionFilter()
        .withIsSubjectCaseSensitive(false)
        .withSubjectBeginsWith("")
        .withSubjectEndsWith(""))
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7572-118">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="e7572-118">Explore the management APIs</span></span>](/java/api/overview/azure/eventgrid/management)