---
title: Comment utiliser le démarreur Spring Boot pour Apache Kafka avec Azure Event Hubs
description: Découvrez comment configurer une application créée avec Spring Boot Initializr pour utiliser Apache Kafka avec Azure Event Hubs.
services: event-hubs
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: event-hubs
ms.tgt_pltfrm: na
ms.topic: article
ms.workload: na
ms.openlocfilehash: f2cf66a4e0ac113406781b4859869ff4edab527e
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991533"
---
# <a name="how-to-use-the-spring-boot-starter-for-apache-kafka-with-azure-event-hubs"></a>Comment utiliser le démarreur Spring Boot pour Apache Kafka avec Azure Event Hubs

## <a name="overview"></a>Vue d’ensemble

Cet article vous explique comment configurer un Stream Binder Spring Cloud basé sur Java développé avec l’initialiseur Spring Boot pour utiliser [Apache Kafka] avec Azure Event Hubs.

## <a name="prerequisites"></a>Prérequis

Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

> [!IMPORTANT]
>
> Spring Boot 2.0 ou version ultérieure est requis pour effectuer les différentes étapes de cet article.
>

## <a name="create-an-azure-event-hub-using-the-azure-portal"></a>Créer un hub Azure Event Hub à l’aide du portail Azure

### <a name="create-an-azure-event-hub-namespace"></a>Créer un espace de noms Azure Event Hub

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/> et connectez-vous.

1. Cliquez sur **+Créer une ressource**, puis sur **Internet des objets**, et cliquez ensuite sur **Event Hubs**.

   ![Créer un espace de noms Azure Event Hub][IMG01]

1. Sur la page **Créer un espace de noms**, saisissez les informations suivantes :

   * Saisissez un **Nom** unique qui fera partie de l’URI de l’espace de noms de votre Event Hub. Par exemple : si vous saisissez **wingtiptoys** comme **Nom**, votre URI sera *wingtiptoys.servicebus.windows.net*.
   * Choisissez un **Niveau tarifaire** pour l’espace de noms de votre Event Hub.
   * Spécifiez **Activer Kafka** pour votre espace de noms.
   * Choisissez l’**Abonnement** que vous souhaitez utiliser pour votre espace de noms.
   * Indiquez si vous souhaitez créer un nouveau **Groupe de ressources** pour votre espace de noms ou choisissez un groupe de ressources déjà existant.
   * Précisez l’**Emplacement** de l’espace de noms de votre Event Hub.

   ![Spécifier les options de l’espace de noms de votre Event Hub Azure][IMG02]

1. Une fois les options ci-dessus définies, cliquez sur **Créer** pour créer votre espace de noms.

### <a name="create-an-azure-event-hub-in-your-namespace"></a>Créer un Hub d’événements Azure dans votre espace de noms

1. Accédez au portail Azure à l’adresse <https://portal.azure.com/>.

1. Cliquez sur **Toutes les ressources**, puis sur l’espace de noms que vous avez créé.

   ![Sélectionnez l’espace de noms de votre Event Hub Azure][IMG03]

1. Cliquez sur **Event Hubs**, puis sur **+Event Hub**.

   ![Ajoutez un nouvel hub Azure Event Hub][IMG04]

1. Sur la page **Créer un Event Hub**, saisissez un **Nom** unique pour votre Event Hub, puis cliquez sur **Créer**.

   ![Créer un Event Hub Azure][IMG05]

1. Lorsque votre Hub d’événements est créé, il sera répertorié sur la page **Event Hubs**.

   ![Créer un Event Hub Azure][IMG06]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a>Créer une application Spring Boot simple avec Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Spécifiez les options suivantes :

   * Générez un projet **Maven** avec **Java**.
   * Spécifiez une version de **Spring Boot** égale ou supérieure à 2.0.
   * Indiquez les noms du **Groupe** et de l’**Artefact** de votre application.
   * Ajoutez la dépendance **Web**.

      ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Le Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.wingtiptoys.kafka*.
   >

1. Une fois les options ci-dessus définies, cliquez sur **Générer le projet**.

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

   ![Télécharger le projet Spring][SI02]

1. Après avoir extrait les fichiers sur votre système local, votre application Spring Boot simple est prête à être modifiée.

## <a name="configure-your-spring-boot-app-to-use-the-spring-cloud-kafka-stream-and-azure-event-hub-starters"></a>Configurez votre application Spring Boot pour utiliser le flux Kafka Spring Cloud et les démarreurs d’Event Hub Azure

1. Localisez le fichier *pom.xml* dans le répertoire racine de votre application. Par exemple :

   `C:\SpringBoot\kafka\pom.xml`

   -ou-

   `/users/example/home/kafka/pom.xml`

1. Ouvrez le fichier *pom.xml* dans un éditeur de texte, et ajoutez le flux Kafka Spring Cloud et les démarreurs Event Hub Azure à la liste des `<dependencies>` :

   ```xml
   <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-stream-kafka</artifactId>
      <version>2.0.1.RELEASE</version>
   </dependency>
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>spring-cloud-azure-starter-eventhub</artifactId>
      <version>1.0.0.M2</version>
   </dependency>
   ```

   ![Modifier le fichier pom.xml][SI03]

1. Enregistrez et fermez le fichier *pom.xml*.

## <a name="create-an-azure-credential-file"></a>Créer un fichier d’informations d’identification Azure

1. Ouvrez une invite de commandes.

1. Accédez au répertoire des *ressources* de votre application Spring Boot, par exemple :

   ```shell
   cd C:\SpringBoot\eventhub\src\main\resources
   ```

   -ou-

   ```shell
   cd /users/example/home/eventhub/src/main/resources
   ```

1. Connectez-vous à votre compte Azure :

   ```azurecli
   az login
   ```

1. Répertoriez vos abonnements :

   ```azurecli
   az account list
   ```
   Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "11111111-1111-1111-1111-111111111111",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "22222222-2222-2222-2222-222222222222",
       "user": {
         "name": "gena.soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```
   
1. Spécifiez le GUID de l’abonnement que vous souhaitez utiliser avec Azure, par exemple :

   ```azurecli
   az account set -s 11111111-1111-1111-1111-111111111111
   ```

1. Créez votre fichier d’informations d’identification Azure :

   ```azurecli
   az ad sp create-for-rbac --sdk-auth > my.azureauth
   ```

   Cette commande créera un fichier *my.azureauth* dans votre répertoire des *ressources* avec un contenu similaire à l’exemple suivant :

   ```json
   {
     "clientId": "33333333-3333-3333-3333-333333333333",
     "clientSecret": "44444444-4444-4444-4444-444444444444",
     "subscriptionId": "11111111-1111-1111-1111-111111111111",
     "tenantId": "22222222-2222-2222-2222-222222222222",
     "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
     "resourceManagerEndpointUrl": "https://management.azure.com/",
     "activeDirectoryGraphResourceId": "https://graph.windows.net/",
     "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
     "galleryEndpointUrl": "https://gallery.azure.com/",
     "managementEndpointUrl": "https://management.core.windows.net/"
   }
   ```

## <a name="configure-your-spring-boot-app-to-use-your-azure-event-hub"></a>Configurer votre application Spring Boot pour utiliser Azure Event Hub

1. Localisez le fichier *application.properties* dans le répertoire des *ressources* de votre application. Par exemple :

   `C:\SpringBoot\eventhub\src\main\resources\application.properties`

   -ou-

   `/users/example/home/eventhub/src/main/resources/application.properties`

2. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées à votre Event Hub :

   ```yaml
   spring.cloud.azure.credential-file-path=my.azureauth
   spring.cloud.azure.resource-group=wingtiptoysresources
   spring.cloud.azure.region=West US
   spring.cloud.azure.eventhub.namespace=wingtiptoysnamespace

   spring.cloud.stream.bindings.input.destination=wingtiptoyshub
   spring.cloud.stream.bindings.input.group=$Default
   spring.cloud.stream.bindings.output.destination=wingtiptoyshub
   ```
   Où :

   |                       Champ                       |                                                                                   Description                                                                                    |
   |---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `spring.cloud.azure.credential-file-path`     |                                                    Spécifie le fichier d’informations d’identification Azure que vous avez précédemment créé dans ce didacticiel.                                                    |
   |        `spring.cloud.azure.resource-group`        |                                                      Spécifie le groupe de ressources Azure qui contient votre Event Hub Azure.                                                      |
   |            `spring.cloud.azure.region`            |                                           Spécifie la région géographique que vous avez indiquée lors de la création de votre Hub d’événements Azure.                                            |
   |      `spring.cloud.azure.eventhub.namespace`      |                                          Spécifie le nom unique que vous avez choisi lors de la création de l’espace de noms de votre Event Hub Azure.                                           |
   | `spring.cloud.stream.bindings.input.destination`  |                            Spécifie l’Event Hub Azure qui servira de destination d’entrée. Dans le cas présent, il s’agit du hub que vous avez précédemment créé dans ce didacticiel.                            |
   |    `spring.cloud.stream.bindings.input.group `    | Spécifie un groupe de consommateurs d’un Event Hub Azure, qui peut être défini comme « $Default » afin d’utiliser le groupe de consommateurs de base généré lors de la création de votre Event Hub Azure. |
   | `spring.cloud.stream.bindings.output.destination` |                               Spécifie l’Event Hub Azure qui servira de destination de sortie. Dans le cas présent, il sera identique à la destination d’entrée.                               |


3. Enregistrez et fermez le fichier *application.properties*.

## <a name="add-sample-code-to-implement-basic-event-hub-functionality"></a>Ajouter un exemple de code pour implémenter une fonctionnalité Event Hub de base

Dans cette section, vous créez les classes Java nécessaires à l’envoi d’événements dans votre hub d’événements.

### <a name="modify-the-main-application-class"></a>Modifiez la classe d’application principale

1. Recherchez le fichier Java principal de l’application dans le répertoire de package de votre application. Par exemple :

   `C:\SpringBoot\kafka\src\main\java\com\wingtiptoys\kafka\KafkaApplication.java`

   -ou-

   `/users/example/home/kafka/src/main/java/com/wingtiptoys/kafka/KafkaApplication.java`

1. Ouvrez le fichier Java principal de l’application dans un éditeur de texte, puis ajoutez-y les lignes suivantes :

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class KafkaApplication {
      public static void main(String[] args) {
         SpringApplication.run(KafkaApplication.class, args);
      }
   }
   ```

1. Enregistrez et fermez le fichier Java principal de l’application.


### <a name="create-a-new-class-for-the-source-connector"></a>Créer une nouvelle classe pour le connecteur source

1. Créez un nouveau ficher Java intitulé *KafkaSource.java* dans le répertoire de package de votre application. Ouvrez ensuite ce fichier dans un éditeur de texte et ajoutez-y les lignes suivantes :

   ```java
   package com.wingtiptoys.kafka;

   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.messaging.Source;
   import org.springframework.messaging.support.GenericMessage;
   import org.springframework.web.bind.annotation.PostMapping;
   import org.springframework.web.bind.annotation.RequestBody;
   import org.springframework.web.bind.annotation.RequestParam;
   import org.springframework.web.bind.annotation.RestController;

   @EnableBinding(Source.class)
   @RestController
   public class KafkaSource {
      @Autowired
      private Source source;

      @PostMapping("/messages")
      public String sendMessage(@RequestBody String message) {
         this.source.output().send(new GenericMessage<>(message));
         return message;
      }
   }
   ```

1. Enregistrez et fermez le fichier *KafkaSource.java*.

### <a name="create-a-new-class-for-the-sink-connector"></a>Créez une nouvelle classe pour le connecteur récepteur

1. Créez un nouveau ficher Java intitulé *KafkaSink.java* dans le répertoire de package de votre application. Ouvrez ensuite ce fichier dans un éditeur de texte et ajoutez-y les lignes suivantes :

   ```java
   package com.wingtiptoys.kafka;

   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import org.springframework.cloud.stream.annotation.EnableBinding;
   import org.springframework.cloud.stream.annotation.StreamListener;
   import org.springframework.cloud.stream.messaging.Sink;

   @EnableBinding(Sink.class)
   public class KafkaSink {
      private static final Logger LOGGER = LoggerFactory.getLogger(KafkaSink.class);

      @StreamListener(Sink.INPUT)
      public void handleMessage(String message) {
         LOGGER.info("New message received: " + message);
      }
   }
   ```

1. Enregistrez et fermez le fichier *KafkaSink.java*.

## <a name="build-and-test-your-application"></a>Générez et testez votre application

1. Ouvrez une invite de commandes, puis accédez au dossier contenant votre fichier *pom.xml*. Par exemple :

   `cd C:\SpringBoot\kafka`

   -ou-

   `cd /users/example/home/kafka`

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Une fois votre application exécutée, vous pouvez utiliser *curl* pour tester votre application. Par exemple :

   ```shell
   curl -X POST -H "Content-Type: text/plain" -d "hello" http://localhost:8080/messages
   ```
   Vous devriez voir « hello » publié dans les journaux de votre application. Par exemple : 

   ```shell
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka version : 1.0.2
   [http-nio-8080-exec-2] INFO org.apache.kafka.common.utils.AppInfoParser - Kafka commitId : 2a121f7b1d402825
   [wingtiptoyshub.container-0-C-1] INFO com.wingtiptoys.kafka.KafkaSink - New message received: hello
   ```


> [!NOTE]
> 
> Afin de tester votre application, vous pouvez modifier votre fichier *KafkaSource.java* pour qu’il contienne un formulaire HTML simple comme dans l’exemple suivant :
> 
> ```java
> package com.wingtiptoys.kafka;
>    
> import org.springframework.beans.factory.annotation.Autowired;
> import org.springframework.cloud.stream.annotation.EnableBinding;
> import org.springframework.cloud.stream.messaging.Source;
> import org.springframework.messaging.support.GenericMessage;
> import org.springframework.web.bind.annotation.GetMapping;
> import org.springframework.web.bind.annotation.PostMapping;
> import org.springframework.web.bind.annotation.RequestBody;
> import org.springframework.web.bind.annotation.RequestParam;
> import org.springframework.web.bind.annotation.RestController;
> 
> @EnableBinding(Source.class)
> @RestController
> public class KafkaSource {
>   @Autowired
>   private Source source;
> 
>   @GetMapping("/")
>   public String sendForm() {
>     return "<html><body>" +
>       "<form action=\"/messages\" method=\"post\">" +
>       "<input type=\"text\" name=\"text\">" +
>       "<input type=\"submit\">" +
>       "</form></body><html>";
>     }
> 
>   @PostMapping("/messages")
>   public String sendMessage(@RequestBody String message) {
>     this.source.output().send(new GenericMessage<>(message));
>     return message;
>   }
> }
> ```
> 
> Cela vous permettra d’utiliser un navigateur web pour tester votre application :
> 
> ![Tester votre application à l’aide d’un navigateur web][TB01]
> 
> Lorsque vous envoyez le formulaire, votre application affiche les résultats :
> 
> ![Réponse de l’application dans un navigateur web][TB02]
> 

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur la prise en charge Azure pour le Stream Binder Event Hub Apache Kafka, consultez les articles suivants :

* [Nouveautés des concentrateurs d’événements Azure ?](/azure/event-hubs/event-hubs-about)

* [Azure Event Hubs pour Apache Kafka](/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview)

* [Créer un espace de noms Event Hubs et un concentrateur d’événements avec le portail Azure](/azure/event-hubs/event-hubs-create)

* [Créer des Event Hubs prenant en charge Apache Kafka](/azure/event-hubs/event-hubs-create-kafka-enabled)

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes. Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>. En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.

<!-- URL List -->

[Apache Kafka]: http://kafka.apache.org
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[IMG01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-01.png
[IMG02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-02.png
[IMG03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-03.png
[IMG04]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-04.png
[IMG05]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-05.png
[IMG06]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-06.png
[IMG07]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-07.png
[IMG08]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-kafka-event-hub-08.png

[SI01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-01.png
[SI02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-02.png
[SI03]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/create-project-03.png

[TB01]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-01.png
[TB02]: ./media/configure-spring-cloud-stream-binder-java-app-kafka-azure-event-hub/test-browser-02.png
