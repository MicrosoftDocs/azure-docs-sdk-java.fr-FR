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
# <a name="azure-event-hub-libraries-for-java"></a>Bibliothèques Azure Event Hub pour Java

## <a name="overview"></a>Vue d'ensemble

Collectez et gérez des millions d’événements par seconde à partir d’appareils IoT connectés et d’applications avec [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).

Pour découvrir Azure Event Hubs, consultez l’article [Recevoir des événements d’Azure Event Hubs avec Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Bibliothèque cliente

Envoyez des événements dans un concentrateur d’événements, utilisez-les puis traitez-les avec un concentrateur d’événements à l’aide de la bibliothèque cliente Event Hubs.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>0.14.3</version>
</dependency>
```   

## <a name="example"></a>Exemples

Envoyez un événement à un concentrateur d’événements.

```java
ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName,sasKeyName, sasKey);

byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
EventData sendEvent = new EventData(payloadBytes);
EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
ehClient.sendSync(sendEvent);
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/eventhub/client)


## <a name="samples"></a>Exemples

[Écrire dans Event Hub via JMS et lire depuis Apache Storm][1]
[Écrire et lire depuis Event Hubs à l’aide d’une topologie hybride .NET/Java][2] 

[1]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[2]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Explorez davantage d’[exemples de code Java pour Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) à utiliser avec vos applications.

