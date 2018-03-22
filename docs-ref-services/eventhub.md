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
ms.openlocfilehash: 076906ff3cafcb4eba97b0a022e5214d7834517c
ms.sourcegitcommit: 02b70b9f5d34415c337601f0b818f7e0985fd884
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/22/2018
---
# <a name="azure-event-hub-libraries-for-java"></a><span data-ttu-id="5803f-104">Bibliothèques Azure Event Hub pour Java</span><span class="sxs-lookup"><span data-stu-id="5803f-104">Azure Event Hub libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="5803f-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5803f-105">Overview</span></span>

<span data-ttu-id="5803f-106">Collectez et gérez des millions d’événements par seconde à partir d’appareils IoT connectés et d’applications avec [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="5803f-106">Collect and manage millions of events per second from connected IoT devices and applications with [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>

<span data-ttu-id="5803f-107">Pour découvrir Azure Event Hubs, consultez l’article [Recevoir des événements d’Azure Event Hubs avec Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span><span class="sxs-lookup"><span data-stu-id="5803f-107">To get started with Azure Event Hubs, see [Receive events from Azure Event Hubs using Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).</span></span>


## <a name="client-library"></a><span data-ttu-id="5803f-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="5803f-108">Client library</span></span>

<span data-ttu-id="5803f-109">Envoyez des événements dans un concentrateur d’événements, utilisez-les puis traitez-les avec un concentrateur d’événements à l’aide de la bibliothèque cliente Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5803f-109">Send events to an Azure Event Hub and consume and process events from an Event Hub using the Event Hubs client library.</span></span>

<span data-ttu-id="5803f-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="5803f-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a><span data-ttu-id="5803f-111">Exemples</span><span class="sxs-lookup"><span data-stu-id="5803f-111">Example</span></span>

<span data-ttu-id="5803f-112">Envoyez un événement à un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="5803f-112">Send an event to an event hub.</span></span>

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5803f-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="5803f-113">Explore the Client APIs</span></span>](/java/api/overview/azure/eventhub/client)


## <a name="samples"></a><span data-ttu-id="5803f-114">Exemples</span><span class="sxs-lookup"><span data-stu-id="5803f-114">Samples</span></span>

<span data-ttu-id="5803f-115">[Écrire dans Event Hub via JMS et lire depuis Apache Storm][1]
[Écrire et lire depuis Event Hubs à l’aide d’une topologie hybride .NET/Java][2]</span><span class="sxs-lookup"><span data-stu-id="5803f-115">[Write to Event Hub via JMS and read from Apache Storm][1]
[Read and write from EventHubs using a hybrid .NET/Java topology][2]</span></span> 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

<span data-ttu-id="5803f-116">Explorez davantage d’[exemples de code Java pour Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="5803f-116">Explore more [sample Java code for Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) you can use in your apps.</span></span>

