---
title: Configurer une application Spring Boot Initializer pour utiliser Azure Application Insights SpringBoot Starter
description: Configurez une application Spring Boot créée avec Spring Initializr pour utiliser Application Insights SpringBoot Starter.
services: Application-Insights
documentationcenter: java
author: dhaval24
manager: alexklim
editor: ''
ms.assetid: ''
ms.author: dhdoshi
ms.date: 12/19/2018
ms.devlang: java
ms.service: Azure Monitor
ms.tgt_pltfrm: application-insights
ms.topic: article
ms.workload: na
ms.openlocfilehash: bf4f7e51f3108d684503465050d69461240f17e3
ms.sourcegitcommit: 9df42bd342ef2d25d56a6045f1ab1baf6f2c250e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/11/2019
ms.locfileid: "54237290"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a>Configurer une application Spring Boot Initializer pour utiliser Application Insights

Cet article vous explique comment créer une application Spring Boot à l’aide de  **[Spring Initializr]**, qui utilise Azure Application Insights SpringBoot Starter pour la surveillance de bout en bout des applications Java sur le cloud.

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.
* Les API Web Flux et Netty **ne sont pas pris en charge actuellement** avec Spring Boot Starter d’Application Insights.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Créer une application personnalisée à l’aide de Spring Initializr

1. Accédez à [https://start.spring.io/](https://start.spring.io/).

1. Spécifiez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis sélectionnez dépendance Web dans la section Dépendances.

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.example.demo*.
   >

1. Cliquez sur le bouton pour **générer le projet**.

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

1. Une fois que vous avez extrait les fichiers sur votre système local, votre application Spring Boot personnalisée est prête à être modifiée.

   ![Fichiers de projet Spring Boot personnalisé][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a>Créer une ressource Application Insights sur Azure

1. Accédez au Portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+Nouveau**.

   ![Portail Azure][AZ01]

1. Cliquez sur **outils de gestion**, puis cliquez sur **Application Insights**.

   ![Portail Azure][AZ02]

1. Sur la page **Nouvelle ressource Application Insights**, spécifiez les informations suivantes :

   * Entrez le **Nom** de votre ressource Application Insights.
   * Définissez le **Type d’Application** sur l’Application web Java.
   * Sélectionnez votre **abonnement**, votre **groupe de ressources** et l’**emplacement**.
   * Sélectionnez l’option Épingler au tableau de bord si vous souhaitez épingler la ressource sur votre portail Azure.

   Une fois ces options définies, cliquez sur **Créer** pour créer votre ressource Application Insights.

   ![Portail Azure][AZ03]

1. Une fois votre ressource créée, elle est répertoriée dans votre **Tableau de bord** Azure et dans les pages **Toutes les ressources**. Vous pouvez cliquer sur votre ressource sur l’un de ces emplacements pour ouvrir la page Vue d’ensemble de la ressource Application Insights. À partir de cette page de vue d’ensemble, copiez la **clé d’instrumentation**.

   ![Portail Azure][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a>Configurer votre application téléchargée Spring Boot pour utiliser Application Insights

1. Recherchez le fichier *POM.xml* dans le répertoire racine de votre application, puis ajoutez la dépendance suivante dans la section de ses dépendances. 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```

1. Recherchez le fichier *application.properties* dans le répertoire *resources* de votre application, ou créez le fichier s’il n’existe pas.

   ![Localiser le fichier application.properties][RE01]

1. Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées avec les informations d'identification appropriées :

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   Pour connaître plus de façons d’ajuster Application Insights, consultez [le fichier readme de démarrage d’Application Insights Springboot](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).

   > [!NOTE]
   > 
   > Vous pouvez utiliser différentes clés d’instrumentation Application Insights (p. ex. différentes ressources) pour les différents profils tels que PROD, DEV, etc. Reportez-vous à la page [Propriétés spécifiques du profil Spring Boot] pour plus d’informations. 

1. Enregistrez et fermez le fichier *application.properties*.

1. Créez un dossier nommé *controller* sous le dossier source de votre package, par exemple :

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   -ou-

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. Créez un fichier nommé *TestController.java* dans le dossier *controller*. Ouvrez le fichier dans un éditeur de texte, puis ajoutez-y le code suivant :

   ```java
    package com.example.demo;

    import com.microsoft.applicationinsights.TelemetryClient;
    import java.io.IOException;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;
    import com.microsoft.applicationinsights.telemetry.Duration;

    @RestController
    @RequestMapping("/sample")
    public class TestController {

        @Autowired
        TelemetryClient telemetryClient;

        @GetMapping("/hello")
        public String hello() {

            //track a custom event  
            telemetryClient.trackEvent("Sending a custom event...");

            //trace a custom trace
            telemetryClient.trackTrace("Sending a custom trace....");

            //track a custom metric
            telemetryClient.trackMetric("custom metric", 1.0);

            //track a custom dependency
            telemetryClient.trackDependency("SQL", "Insert", new Duration(0, 0, 1, 1, 1), true);

            return "hello";
        }
    }
   ```

   Où vous devez remplacer `com.example.demo` par le nom du package de votre projet.

1. Enregistrez et fermez le fichier *TestController.java*.

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Testez l’application web en accédant à http://localhost:8080/sample/hello avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   Le message « Hello ! » de votre exemple de contrôleur devrait s’afficher. Application Insights collectera automatiquement cette requête et l’enverra sous forme d’élément de télémétrie avec son événement personnalisé, sa métrique personnalisée, sa dépendance personnalisée et sa trace personnalisé associées telles que spécifiées dans la logique du contrôleur. 

   Après quelques secondes, vous devez voir les données sur le portail Azure. 

   ![Portail Azure][AZ05]

   Vous pouvez cliquer sur la mosaïque de cartographie d’application pour afficher les composants de niveau élevé et leurs interactions. Il s’agit d’un emplacement recommandé pour obtenir une vue d’ensemble détaillée de l’ensemble de l’application. Chaque microservice Spring Boot est reconnue par le nom de l’application spring. Pensez à le définir.

   ![Portail Azure][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a>Configurer l’application Springboot pour envoyer les journaux log4j à Application Insights

1. Modifiez le fichier POM.xml du projet et ajoutez/modifiez la section dépendances avec les éléments suivants. 

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-log4j2</artifactId>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-spring-boot-starter</artifactId>
        <version>1.1.1</version>
    </dependency>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-logging-log4j2</artifactId>
        <version>2.1.1</version>
    </dependency>
</dependencies>
```

2. Enregistrez et fermez le fichier *POM.xml*.

3. Dans le dossier \src\main\resources, créez un nouveau fichier *log4j2.xml* et configurez-le. Par exemple : 

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<Configuration packages="com.microsoft.applicationinsights.log4j.v2">
  <Properties>
    <Property name="LOG_PATTERN">
      %d{yyyy-MM-dd HH:mm:ss.SSS} %5p ${hostName} --- [%15.15t] %-40.40c{1.} : %m%n%ex
    </Property>
  </Properties>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
    <ApplicationInsightsAppender name="aiAppender">
    </ApplicationInsightsAppender>
  </Appenders>
  <Loggers>
    <Root level="trace">
      <AppenderRef ref="Console"  />
      <AppenderRef ref="aiAppender"  />
    </Root>
  </Loggers>
</Configuration>
```
4. Générez et exécutez à nouveau l’application Spring Boot comme indiqué ci-dessus. 

Au bout de quelques secondes, vous devriez voir tous les journaux spring disponibles sur le portail Azure. 

![Portail Azure][AZ06]

Vous pouvez même consulter les messages de journal détaillés et effectuer une analyse sur le Portail Analytics. 

![Portail Azure][AZ07]

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Application Insights prend en charge la collecte automatique des dépendances externes et leur corrélation avec les requêtes entrantes. Actuellement, nous prenons en charge la collection automatique d’Oracle, MsSQL, MySQL et Redis. Pour plus d’informations sur l’activation de la collection automatique, suivez l’article [how to use Application Insights Java agent](/azure/application-insights/app-insights-java-agent) (Comment utiliser l’agent Java Application Insights).

Pour plus d’informations sur Azure Application Insights et ses fonctionnalités de surveillance, consultez la page d’accueil  **[Application Insights]**.

Pour plus d’informations sur les détails de configuration supplémentaires d’Application Insights Spring Boot Starter, consultez ce [lien](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).

Pour les demandes de fonctionnalités et les bogues éventuels, faites-le-nous savoir sur notre référentiel [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues).

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes. Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse [https://github.com/spring-guides/](https://github.com/spring-guides/). En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Propriétés spécifiques du profil Spring Boot]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Application Insights]: /azure/application-insights/

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource.png
[AZ02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_2.png
[AZ03]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Create_resource_3.png
[AZ04]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Get_IKey.png
[AZ05]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/OverviewBladeResults.png
[AZ06]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/Search_and_traces.png
[AZ07]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/traces_details.png
[AZ08]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/AppMap.png

[SI01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/spring_start.png
[SI02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/After_extract.png

[RE01]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationproperties_loc.png
[RE02]: ./media/configure-spring-boot-starter-java-app-with-azure-application-insights/applicationinsightsproperties.png
