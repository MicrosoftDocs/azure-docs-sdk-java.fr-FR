---
title: Bibliothèques Service Bus pour Java
description: Consulter la documentation sur les bibliothèques de client et de gestion Java pour Service Bus
keywords: Azure, Java, SDK, API, messagerie, amqp, qpid, JMS, pubsub, pub-sub, répartiteur de messages
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: service-bus
ms.openlocfilehash: ed830b4f7ffa104174205f75ea2923235029ea80
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33887759"
---
# <a name="service-bus-libraries-for-java"></a>Bibliothèques Service Bus pour Java

## <a name="overview"></a>Vue d'ensemble

Service Bus est une plateforme professionnelle de service de messagerie transactionnel qui fournit des files d’attentes extrêmement fiables et des rubriques de publication/abonnement avec des fonctionnalités complexes telles que la livraison chronologique des messages, les sessions, le partitionnement, la planification, les abonnements complexes, mais aussi la gestion des transactions et des flux de travail.

Les fonctionnalités de Service Bus sont similaires, voire supérieures, à celles de répartiteurs de messages locaux hérités et haut de gamme. Les fonctionnalités de Service Bus sont disponibles via les protocoles standard tels que AMQP 1.0 et HTTPS, et tous les mouvements de protocole sont intégralement documentés, offrant ainsi une interopérabilité importante. 

En mettant l’accent sur une messagerie durable disponible et fiable, Service Bus Premium offre une performance de débit concurrentielle même pour des déploiements de centre de données locaux importants, et vous épargne des tâches telles que la sélection de matériel informatique et leur processus d’acquisition, la planification et l’exécution de déploiement, et les sessions d’optimisation des performances qui n’en finissent jamais. 

Service Bus Premium est une offre entièrement gérée avec une capacité dédiée et réservée de ressources à chaque abonné qui interrompt la prévisibilité des performances via un modèle tarifaire basé sur la capacité et à un coût global beaucoup plus faible que d’autres répartiteurs locaux commercialisés. Pour de nombreux clients, Service Bus Premium est aujourd’hui capable de remplacer des clusters locaux dédiés de messagerie, même lorsque les charges de travail associées ne s’exécutent pas dans le cloud. 

En savoir plus sur les concepts de Service Bus [dans la section documentation de la messagerie](https://docs.microsoft.com/azure/service-bus-messaging/) 

Pour les développeurs Java, Service Bus fournit une API native prise en charge par Microsoft, et peut également être utilisé avec des bibliothèques conformes d’AMQP 1.0 telles que le fournisseur JMS d’Apache Qpid Proton.

## <a name="client-library"></a>Bibliothèque cliente

Le client officiel Service Bus est disponible sous [forme de code source sur GitHub](https://github.com/azure/azure-service-bus-java) et les binaires et packages de sources [sont disponibles sur Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).

**Le [référentiel de code exemple](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contient des exemples pour :**
* Comment utiliser [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)
* Comment utiliser [TopicClient et SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)
* Comment utiliser les messages [MessageSender et MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) de Service Bus.

Ajoutez une dépendance au fichier `pom.xml` de votre projet Maven pour utiliser la bibliothèque dans votre projet. Précisez la version de votre choix.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-servicebus</artifactId>
    <version>1.0.0</version>
</dependency>
```

```java
public class BasicSendReceiveWithQueueClient {
    // Connection String for the namespace can be obtained from the Azure portal under the
    // 'Shared Access policies' section.
    private static final String connectionString = "{connection string}";
    private static final String queueName = "{queue name}";
    private static IQueueClient queueClient;
    private static int totalSend = 100;
    private static int totalReceived = 0;

    public static void main(String[] args) throws Exception {

        Log.log("Starting BasicSendReceiveWithQueueClient sample");

        // create client
        Log.log("Create queue client.");
        queueClient = new QueueClient(new ConnectionStringBuilder(connectionString, queueName), ReceiveMode.PeekLock);

        // send and receive
        queueClient.registerMessageHandler(new MessageHandler(queueClient), new MessageHandlerOptions(1, false, Duration.ofMinutes(1)));
        for (int i = 0; i < totalSend; i++) {
            int j = i;
            Log.log("Sending message #%d.", j);
            queueClient.sendAsync(new Message("" + i)).thenRunAsync(() -> { Log.log("Sent message #%d.", j);});
        }

        while(totalReceived != totalSend) {
            Thread.sleep(1000);
        }

        Log.log("Received all messages, exiting the sample.");
        Log.log("Closing queue client.");
        queueClient.close();
    }

    static class MessageHandler implements IMessageHandler {
        private IQueueClient client;

        public MessageHandler(IQueueClient client) {
            this.client = client;
        }

        @Override
        public CompletableFuture<Void> onMessageAsync(IMessage iMessage) {
            Log.log("Received message with sq#: %d and lock token: %s.", iMessage.getSequenceNumber(), iMessage.getLockToken());
            return this.client.completeAsync(iMessage.getLockToken()).thenRunAsync(() -> {
                Log.log("Completed message sq#: %d and locktoken: %s", iMessage.getSequenceNumber(), iMessage.getLockToken());
                totalReceived++;
            });
        }

        @Override
        public void notifyException(Throwable throwable, ExceptionPhase exceptionPhase) {
            Log.log(exceptionPhase + "-" + throwable.getMessage());
        }
    }
}
```

> [!div class="nextstepaction"]
> [Explorer les API Client](/java/api/overview/azure/servicebus/client)
> [Trouver plus d’exemples ici (voir également ci-dessus pour plus de détails)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)

## <a name="management-api"></a>API de gestion

Créez et gérez des espaces de noms, des rubriques, des files d’attente et des abonnements avec l’API de gestion.

**Trouvez quelques exemples ici :**
* [Gérer des files d’attente Service Bus](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [Créer et s’abonner à des rubriques Service Bus](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

**Utiliser l’API de gestion dans votre projet :**
\
[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorer les API de gestion](/java/api/overview/azure/servicebus/management)

Explorez davantage d’[exemples de code Java pour Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) à utiliser avec vos applications.
