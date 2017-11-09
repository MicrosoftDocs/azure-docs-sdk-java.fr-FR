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
# <a name="azure-iot-libraries-for-java"></a>Bibliothèques Azure IoT pour Java

Connectez, surveillez et contrôlez des ressources IoT (Internet of Things, Internet des objets) avec [Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-what-is-iot-hub).

Pour découvrir Azure IoT Hub, consultez [Connecter votre appareil à votre IoT Hub à l’aide de Java](/azure/iot-hub/iot-hub-java-java-getstarted).

## <a name="iot-service-library"></a>Bibliothèque de services IoT

Enregistrez des appareils et envoyez des messages du cloud vers des appareils enregistrés à l’aide de la bibliothèque de services IoT.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-service-client</artifactId>
    <version>1.6.23</version>
</dependency>
```   

## <a name="iot-device-library"></a>Bibliothèque d’appareils IoT

Envoyez des messages sur le cloud et recevez des messages sur des appareils avec la bibliothèque d’appareils IoT.

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.  

```XML
<dependency>
    <groupId>com.microsoft.azure.sdk.iot</groupId>
    <artifactId>iot-device-client</artifactId>
    <version>1.3.31</version>
</dependency>
```

> [!div class="nextstepaction"]
> [Explorer les API clientes](/java/api/overview/azure/iot/clientlibrary)   

## <a name="example"></a>Exemple

Envoyez un message depuis Azure IoT Hub vers un appareil.

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


## <a name="samples"></a>Exemples

[Exemples d’appareils IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/device/iot-device-samples)     
[Exemples de services IoT](https://github.com/Azure/azure-iot-sdk-java/tree/master/service/iot-service-samples)

Explorez davantage d’[exemples de code Java pour Azure IoT](https://azure.microsoft.com/resources/samples/?platform=java&term=iot) à utiliser avec vos applications.
