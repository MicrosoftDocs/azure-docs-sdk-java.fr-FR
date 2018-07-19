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
ms.openlocfilehash: b6646ef27edace4247090e749c9a52cd6a33a82c
ms.sourcegitcommit: 3d3460289ab6b9165c2cf6a3dd56eafd0692501e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34283023"
---
# <a name="azure-event-hub-libraries-for-java"></a>Bibliothèques Azure Event Hub pour Java

## <a name="overview"></a>Vue d'ensemble

Collectez et gérez des millions d’événements par seconde à partir d’appareils IoT connectés et d’applications avec [Azure Event Hubs](/azure/event-hubs/event-hubs-what-is-event-hubs).

Pour découvrir Azure Event Hubs, consultez l’article [Recevoir des événements d’Azure Event Hubs avec Java](/azure/event-hubs/event-hubs-java-get-started-receive-eph).


## <a name="client-library"></a>Bibliothèque cliente

Envoyez des événements dans un concentrateur d’événements, utilisez-les puis traitez-les avec un concentrateur d’événements à l’aide de la bibliothèque cliente Event Hubs.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la [bibliothèque cliente](https://mvnrepository.com/artifact/com.microsoft.azure/azure-eventhubs) dans votre projet.
 

## <a name="example"></a>Exemples

Envoyez un événement à un concentrateur d’événements.

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
> [Explorer les API clientes](/java/api/overview/azure/eventhubs/client)



## <a name="samples"></a>Exemples

[Explorer l’API de plan de données Event Hub à l’aide d’exemples][1]

[Écrire à Event Hub via JMS et lire à partir d’Apache Storm][2]

[Lire et écrire à partir d’EventHubs à l’aide d’une topologie .NET/Java hybride][3] 

[1]: https://github.com/Azure/azure-event-hubs/tree/master/samples/Java
[2]: https://github.com/Azure-Samples/event-hubs-java-storm-sender-jms-receiver
[3]: https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub

Explorez davantage d’[exemples de code Java pour Azure Event Hubs](https://azure.microsoft.com/resources/samples/?platform=java&term=event) à utiliser avec vos applications.

