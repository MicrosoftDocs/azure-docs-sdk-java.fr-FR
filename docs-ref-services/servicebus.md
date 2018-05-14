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
---
# <a name="service-bus-libraries-for-java"></a><span data-ttu-id="8218a-104">Bibliothèques Service Bus pour Java</span><span class="sxs-lookup"><span data-stu-id="8218a-104">Service Bus libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="8218a-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8218a-105">Overview</span></span>

<span data-ttu-id="8218a-106">Service Bus est une plateforme professionnelle de service de messagerie transactionnel qui fournit des files d’attentes extrêmement fiables et des rubriques de publication/abonnement avec des fonctionnalités complexes telles que la livraison chronologique des messages, les sessions, le partitionnement, la planification, les abonnements complexes, mais aussi la gestion des transactions et des flux de travail.</span><span class="sxs-lookup"><span data-stu-id="8218a-106">Service Bus is an enterprise-class, transactional messaging platform service that provides highly reliable queues and publish/subscribe topics with deep feature capabilities such as ordered delivery, sessions, partitioning, scheduling, complex subscriptions, as well as workflow and transaction handling.</span></span>

<span data-ttu-id="8218a-107">Les fonctionnalités de Service Bus sont similaires, voire supérieures, à celles de répartiteurs de messages locaux hérités et haut de gamme.</span><span class="sxs-lookup"><span data-stu-id="8218a-107">The Service Bus feature capabilities are comparable and often exceed those of high-end, on-premises legacy message brokers.</span></span> <span data-ttu-id="8218a-108">Les fonctionnalités de Service Bus sont disponibles via les protocoles standard tels que AMQP 1.0 et HTTPS, et tous les mouvements de protocole sont intégralement documentés, offrant ainsi une interopérabilité importante.</span><span class="sxs-lookup"><span data-stu-id="8218a-108">The Service Bus features are available via standards-based protocols like AMQP 1.0 and HTTPS and all protocol gestures are fully documented, allowing for broad interoperability.</span></span> 

<span data-ttu-id="8218a-109">En mettant l’accent sur une messagerie durable disponible et fiable, Service Bus Premium offre une performance de débit concurrentielle même pour des déploiements de centre de données locaux importants, et vous épargne des tâches telles que la sélection de matériel informatique et leur processus d’acquisition, la planification et l’exécution de déploiement, et les sessions d’optimisation des performances qui n’en finissent jamais.</span><span class="sxs-lookup"><span data-stu-id="8218a-109">Focusing on highly available and reliable durable messaging, the Service Bus Premium provides competitive throughput performance even with substantial local datacenter deployments, but without hardware selection and acquisition processes, deployment planning and execution, and endless performance optimization sessions.</span></span> 

<span data-ttu-id="8218a-110">Service Bus Premium est une offre entièrement gérée avec une capacité dédiée et réservée de ressources à chaque abonné qui interrompt la prévisibilité des performances via un modèle tarifaire basé sur la capacité et à un coût global beaucoup plus faible que d’autres répartiteurs locaux commercialisés.</span><span class="sxs-lookup"><span data-stu-id="8218a-110">Service Bus Premium is a fully managed offering with dedicated capacity reserved for each tenant that yields predictable performance with a simple, capacity-oriented pricing model and at extremely lower overall cost than commercial on-premises brokers.</span></span> <span data-ttu-id="8218a-111">Pour de nombreux clients, Service Bus Premium est aujourd’hui capable de remplacer des clusters locaux dédiés de messagerie, même lorsque les charges de travail associées ne s’exécutent pas dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="8218a-111">For many customers, Service Bus Premium can replace dedicated on-premises messaging clusters today, even if the attached workloads do not run in the cloud.</span></span> 

<span data-ttu-id="8218a-112">En savoir plus sur les concepts de Service Bus [dans la section documentation de la messagerie](https://docs.microsoft.com/azure/service-bus-messaging/)</span><span class="sxs-lookup"><span data-stu-id="8218a-112">Learn more about Service Bus concepts [in the messaging documentation section](https://docs.microsoft.com/azure/service-bus-messaging/)</span></span> 

<span data-ttu-id="8218a-113">Pour les développeurs Java, Service Bus fournit une API native prise en charge par Microsoft, et peut également être utilisé avec des bibliothèques conformes d’AMQP 1.0 telles que le fournisseur JMS d’Apache Qpid Proton.</span><span class="sxs-lookup"><span data-stu-id="8218a-113">For Java developers, Service Bus provides a Microsoft supported native API and Service Bus can also be used with AMQP 1.0 compliant libraries such as Apache Qpid Proton's JMS provider.</span></span>

## <a name="client-library"></a><span data-ttu-id="8218a-114">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="8218a-114">Client library</span></span>

<span data-ttu-id="8218a-115">Le client officiel Service Bus est disponible sous [forme de code source sur GitHub](https://github.com/azure/azure-service-bus-java) et les binaires et packages de sources [sont disponibles sur Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span><span class="sxs-lookup"><span data-stu-id="8218a-115">The official Service Bus client is available in [source code form on GitHub](https://github.com/azure/azure-service-bus-java) and binaries and packaged sources [are available on Maven Central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-servicebus%22).</span></span>

<span data-ttu-id="8218a-116">**Le [référentiel de code exemple](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contient des exemples pour :**</span><span class="sxs-lookup"><span data-stu-id="8218a-116">**The [sample code repository](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/) contains samples for:**</span></span>
* <span data-ttu-id="8218a-117">Comment utiliser [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)</span><span class="sxs-lookup"><span data-stu-id="8218a-117">How to use the [QueueClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithQueueClient.java)</span></span>
* <span data-ttu-id="8218a-118">Comment utiliser [TopicClient et SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)</span><span class="sxs-lookup"><span data-stu-id="8218a-118">How to use the [TopicClient and SubscriptionClient](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/BasicSendReceiveWithTopicSubscriptionClient.java)</span></span>
* <span data-ttu-id="8218a-119">Comment utiliser les messages [MessageSender et MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8218a-119">How to use [MessageSender and MessageReceiver](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/src/com/microsoft/azure/servicebus/samples/SendReceiveWithMessageSenderReceiver.java) messages from Service Bus.</span></span>

<span data-ttu-id="8218a-120">Ajoutez une dépendance au fichier `pom.xml` de votre projet Maven pour utiliser la bibliothèque dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="8218a-120">Add a dependency to your Maven project's `pom.xml` file to use the library in your own project.</span></span> <span data-ttu-id="8218a-121">Précisez la version de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8218a-121">Specify the version as desired.</span></span>

<span data-ttu-id="8218a-122">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="8218a-122">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

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
> <span data-ttu-id="8218a-123">[Explorer les API Client](/java/api/overview/azure/servicebus/client)
> [Trouver plus d’exemples ici (voir également ci-dessus pour plus de détails)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)</span><span class="sxs-lookup"><span data-stu-id="8218a-123">[Explore the Client APIs](/java/api/overview/azure/servicebus/client)
[Find more examples here (See also above for more details)](https://github.com/Azure/azure-service-bus/blob/master/samples/Java/)</span></span>

## <a name="management-api"></a><span data-ttu-id="8218a-124">API de gestion</span><span class="sxs-lookup"><span data-stu-id="8218a-124">Management API</span></span>

<span data-ttu-id="8218a-125">Créez et gérez des espaces de noms, des rubriques, des files d’attente et des abonnements avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="8218a-125">Create and manage namespaces, topics, queues, and subscriptions with the management API.</span></span>

<span data-ttu-id="8218a-126">**Trouvez quelques exemples ici :**</span><span class="sxs-lookup"><span data-stu-id="8218a-126">**Please find some examples here:**</span></span>
* [<span data-ttu-id="8218a-127">Gérer des files d’attente Service Bus</span><span class="sxs-lookup"><span data-stu-id="8218a-127">Manage Service Bus queues</span></span>](https://github.com/Azure-Samples/service-bus-java-manage-queue-with-basic-features)
* [<span data-ttu-id="8218a-128">Créer et s’abonner à des rubriques Service Bus</span><span class="sxs-lookup"><span data-stu-id="8218a-128">Create and subscribe to Service Bus topics</span></span>](https://github.com/Azure-Samples/service-bus-java-manage-publish-subscribe-with-basic-features)

<span data-ttu-id="8218a-129">**Utiliser l’API de gestion dans votre projet :**
\\</span><span class="sxs-lookup"><span data-stu-id="8218a-129">**Use the Management API in your project:**
\\</span></span>
<span data-ttu-id="8218a-130">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="8218a-130">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-servicebus</artifactId>
    <version>1.3.0</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8218a-131">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="8218a-131">Explore the Management APIs</span></span>](/java/api/overview/azure/servicebus/management)

<span data-ttu-id="8218a-132">Explorez davantage d’[exemples de code Java pour Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="8218a-132">Explore more [sample Java code for Azure Service Bus](https://azure.microsoft.com/resources/samples/?platform=java&term=bus) you can use in your apps.</span></span>
