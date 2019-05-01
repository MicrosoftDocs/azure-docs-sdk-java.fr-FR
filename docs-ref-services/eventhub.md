---
title: Bibliothèques Azure Event Hub pour Java
description: Consulter la documentation sur les bibliothèques Event Hub Java
keywords: Azure, Java, SDK, API, concentrateur d’événements, IoT, traitement de flux
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 06/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: event-hub
ms.openlocfilehash: 9e2ae18f98083cb35bb076a5f84726b669cbf81e
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61593355"
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="10b13-104">Bibliothèques Azure Event Hub pour Java</span><span class="sxs-lookup"><span data-stu-id="10b13-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="10b13-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="10b13-105">Overview</span></span>

<span data-ttu-id="10b13-106">Collectez et gérez des millions d’événements par seconde à partir d’appareils IoT connectés et d’applications avec [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="10b13-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="10b13-107">Pour découvrir Azure Event Hubs, consultez l’article [Recevoir des événements d’Azure Event Hubs avec Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="10b13-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="10b13-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="10b13-108">Client library</span></span>

<span data-ttu-id="10b13-109">Envoyez des événements dans un concentrateur d’événements, utilisez-les puis traitez-les avec un concentrateur d’événements à l’aide de la bibliothèque cliente Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="10b13-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="10b13-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la [bibliothèque cliente](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="10b13-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the [client library](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) in your project.</span></span>
 

## <a name="example"></a><span data-ttu-id="10b13-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="10b13-111">Example</span></span>

<span data-ttu-id="10b13-112">Envoyez un événement à un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="10b13-112">Send an event to an event hub.</span></span>

```java
final ConnectionStringBuilder connStr = new ConnectionStringBuilder()
                                            .setNamespaceName(namespaceName)
                                            .setEventHubName(eventHubName)
                                            .setSasKeyName(sasKeyName)
                                            .setSasKey(sasKey);
final EventHubClient ehClient = EventHubClient.createSync(connStr.toString());

final byte[] payloadBytes = "Test AMQP message".getBytes("UTF-8");
final EventData sendEvent = new EventData(payloadBytes);

ehClient.sendSync(sendEvent);
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="10b13-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="10b13-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a><span data-ttu-id="10b13-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="10b13-114">Samples</span></span>

<span data-ttu-id="10b13-115">[Explorer l’API de plan de données Event Hub à l’aide d’exemples][1]</span><span class="sxs-lookup"><span data-stu-id="10b13-115">[Explore Event Hub data-plane API using samples][1]</span></span>

<span data-ttu-id="10b13-116">[Écrire à Event Hub via JMS et lire à partir d’Apache Storm][2]</span><span class="sxs-lookup"><span data-stu-id="10b13-116">[Write to Event Hub via JMS and read from Apache Storm][2]</span></span>

<span data-ttu-id="10b13-117">[Lire et écrire à partir d’EventHubs à l’aide d’une topologie .NET/Java hybride][3]</span><span class="sxs-lookup"><span data-stu-id="10b13-117">[Read and write from EventHubs using a hybrid .NET/Java topology][3]</span></span> 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="10b13-118">Explorez davantage d’[exemples de code Java pour Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="10b13-118">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

