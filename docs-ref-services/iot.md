---
title: "Bibliothèques Azure IoT Hub pour Java"
description: "Consulter la documentation sur les bibliothèques Azure IoT Hub Java"
keywords: "Azure, Java, SDK, API, événement, IoT, flux, appareils, IoT Hub"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: iot-hub
ms.openlocfilehash: c1af3dae0fe37eb4919db02da87beed193c547a7
ms.sourcegitcommit: acc83bb537d77568b2a5427479d6354d6ae30885
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2017
---
# <a name="azure-iot-libraries-for-java"></a><span data-ttu-id="9ae45-104">Bibliothèques Azure IoT pour Java</span><span class="sxs-lookup"><span data-stu-id="9ae45-104">Azure IoT libraries for Java</span></span>

<span data-ttu-id="9ae45-105">Connectez, surveillez et contrôlez des ressources IoT (Internet of Things, Internet des objets) avec [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).</span><span class="sxs-lookup"><span data-stu-id="9ae45-105">Connect, monitor, and control Internet of Things assets with [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).</span></span>

<span data-ttu-id="9ae45-106">Pour découvrir Azure IoT Hub, consultez [Connecter votre appareil à votre IoT Hub à l’aide de Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span><span class="sxs-lookup"><span data-stu-id="9ae45-106">To get started with Azure IoT Hub, see [Connect your device to your IoT hub using Java](/azure/iot-hub/iot-hub-java-java-getstarted).</span></span>

## <a name="iot-service-library"></a><span data-ttu-id="9ae45-107">Bibliothèque de services IoT</span><span class="sxs-lookup"><span data-stu-id="9ae45-107">IoT Service library</span></span>

<span data-ttu-id="9ae45-108">Enregistrez des appareils et envoyez des messages du cloud vers des appareils enregistrés à l’aide de la bibliothèque de services IoT.</span><span class="sxs-lookup"><span data-stu-id="9ae45-108">Register devices and send messages from the cloud to registered devices using the IoT Service library.</span></span>

<span data-ttu-id="9ae45-109">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="9ae45-109">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a><span data-ttu-id="9ae45-110">Bibliothèque d’appareils IoT</span><span class="sxs-lookup"><span data-stu-id="9ae45-110">Iot Device library</span></span>

<span data-ttu-id="9ae45-111">Envoyez des messages sur le cloud et recevez des messages sur des appareils avec la bibliothèque d’appareils IoT.</span><span class="sxs-lookup"><span data-stu-id="9ae45-111">Send messages to the cloud and receive messages on devices using the IoT Device library.</span></span>

<span data-ttu-id="9ae45-112">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="9ae45-112">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9ae45-113">Explorer les API clientes</span><span class="sxs-lookup"><span data-stu-id="9ae45-113">Explore the Client APIs</span></span>](/java/api/overview/azure/iot/clientlibrary)   

## <a name="example"></a><span data-ttu-id="9ae45-114">Exemple</span><span class="sxs-lookup"><span data-stu-id="9ae45-114">Example</span></span>

<span data-ttu-id="9ae45-115">Envoyez un message depuis Azure IoT Hub vers un appareil.</span><span class="sxs-lookup"><span data-stu-id="9ae45-115">Send a message from Azure IoT Hub to a device.</span></span>

```java
Message messageToSend = new Message(messageText);
messageToSend.setDeliveryAcknowledgement(DeliveryAcknowledgement.Full);
messageToSend.setMessageId(java.util.UUID.randomUUID().toString());

// set message properties
Map<String, String> propertiesToSend = new HashMap<String, String>();
propertiesToSend.put(messagePropertyKey,messagePropertyKey);
messageToSend.setProperties(propertiesToSend);

CompletableFuture<Void> future = serviceClient.sendAsync(deviceId, messageToSend);
try {
    future.get();
}
catch (ExecutionException e) {
    System.out.println("Exception : " + e.getMessage());
}
```


## <a name="samples"></a><span data-ttu-id="9ae45-116">Exemples</span><span class="sxs-lookup"><span data-stu-id="9ae45-116">Samples</span></span>

<span data-ttu-id="9ae45-117">[Exemples d’appareils IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span><span class="sxs-lookup"><span data-stu-id="9ae45-117">[IoT Device samples](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)   </span></span>  
[<span data-ttu-id="9ae45-118">Exemples de services IoT</span><span class="sxs-lookup"><span data-stu-id="9ae45-118">IoT Service samples</span></span>](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

<span data-ttu-id="9ae45-119">Explorez davantage d’[exemples de code Java pour Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="9ae45-119">Explore more [sample Java code for Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) you can use in your apps.</span></span>
