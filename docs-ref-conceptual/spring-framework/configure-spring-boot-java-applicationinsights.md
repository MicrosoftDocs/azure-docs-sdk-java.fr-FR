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
ms.openlocfilehash: f69cdcc5b479e83b230f23a8a76f96284a1b785b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991433"
---
# <a name="configure-a-spring-boot-initializer-app-to-use-application-insights"></a><span data-ttu-id="abef4-103">Configurer une application Spring Boot Initializer pour utiliser Application Insights</span><span class="sxs-lookup"><span data-stu-id="abef4-103">Configure a Spring Boot Initializer app to use Application Insights</span></span>

<span data-ttu-id="abef4-104">Cet article vous explique comment créer une application Spring Boot à l’aide de  **[Spring Initializr]**, qui utilise Azure Application Insights SpringBoot Starter pour la surveillance de bout en bout des applications Java sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="abef4-104">This article walks you through creating a Spring Boot application using **[Spring Initializr]**, that uses Azure Application Insights Spring Boot Starter for end-to-end monitoring of Java applications on cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abef4-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="abef4-105">Prerequisites</span></span>

<span data-ttu-id="abef4-106">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="abef4-106">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="abef4-107">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="abef4-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="abef4-108">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="abef4-108">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="abef4-109">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="abef4-109">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="abef4-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="abef4-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="abef4-111">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="abef4-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="abef4-112">Accédez à [https://start.spring.io/](https://start.spring.io/).</span><span class="sxs-lookup"><span data-stu-id="abef4-112">Browse to [https://start.spring.io/](https://start.spring.io/).</span></span>

1. <span data-ttu-id="abef4-113">Spécifiez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis sélectionnez dépendance Web dans la section Dépendances.</span><span class="sxs-lookup"><span data-stu-id="abef4-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select web dependency in the dependenies section.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="abef4-115">Spring Initializr utilise les noms de **Groupe** et d’**Artefact** pour créer le nom du package. Par exemple, *com.example.demo*.</span><span class="sxs-lookup"><span data-stu-id="abef4-115">The Spring Initializr will use the **Group** and **Artifact** names to create the package name; for example: *com.example.demo*.</span></span>
   >

1. <span data-ttu-id="abef4-116">Cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="abef4-116">Click the button to **Generate Project**.</span></span>

1. <span data-ttu-id="abef4-117">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="abef4-117">When prompted, download the project to a path on your local computer.</span></span>

1. <span data-ttu-id="abef4-118">Une fois que vous avez extrait les fichiers sur votre système local, votre application Spring Boot personnalisée est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="abef4-118">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI02]

## <a name="create-an-application-insights-resource-on-azure"></a><span data-ttu-id="abef4-120">Créer une ressource Application Insights sur Azure</span><span class="sxs-lookup"><span data-stu-id="abef4-120">Create an Application Insights Resource on Azure</span></span>

1. <span data-ttu-id="abef4-121">Accédez au Portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="abef4-121">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="abef4-123">Cliquez sur **outils de gestion**, puis cliquez sur **Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="abef4-123">Click **Management Tools**, and then click **Application Insights**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="abef4-125">Sur la page **Nouvelle ressource Application Insights**, spécifiez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="abef4-125">On the **New Application Insights Resource** page, specify the following information:</span></span>

   * <span data-ttu-id="abef4-126">Entrez le **Nom** de votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="abef4-126">Enter the **Name** for your Application Insights resource.</span></span>
   * <span data-ttu-id="abef4-127">Définissez le **Type d’Application** sur l’Application web Java.</span><span class="sxs-lookup"><span data-stu-id="abef4-127">Choose the **Application Type** to Java Web Application.</span></span>
   * <span data-ttu-id="abef4-128">Sélectionnez votre **abonnement**, votre **groupe de ressources** et l’**emplacement**.</span><span class="sxs-lookup"><span data-stu-id="abef4-128">Specify your **Subscription**, **Resource group** and **Location**.</span></span>
   * <span data-ttu-id="abef4-129">Sélectionnez l’option Épingler au tableau de bord si vous souhaitez épingler la ressource sur votre portail Azure.</span><span class="sxs-lookup"><span data-stu-id="abef4-129">Select Pin to dashboard option, if you would like to pin the resource on your Azure portal.</span></span>

   <span data-ttu-id="abef4-130">Une fois ces options définies, cliquez sur **Créer** pour créer votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="abef4-130">When you have specified these options, click **Create** to create your Application Insights resource.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="abef4-132">Une fois votre ressource créée, elle est répertoriée dans votre **Tableau de bord** Azure et dans les pages **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="abef4-132">Once your resource has been created, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources** pages.</span></span> <span data-ttu-id="abef4-133">Vous pouvez cliquer sur votre ressource sur l’un de ces emplacements pour ouvrir la page Vue d’ensemble de la ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="abef4-133">You can click on your resource on any of those locations to open the overview page of the Application Insights resource.</span></span> <span data-ttu-id="abef4-134">À partir de cette page de vue d’ensemble, copiez la **clé d’instrumentation**.</span><span class="sxs-lookup"><span data-stu-id="abef4-134">From this overview page please copy the **instrumentation key**.</span></span>

   ![Portail Azure][AZ04]

## <a name="configure-your-downloaded-spring-boot-application-to-use-application-insights"></a><span data-ttu-id="abef4-136">Configurer votre application téléchargée Spring Boot pour utiliser Application Insights</span><span class="sxs-lookup"><span data-stu-id="abef4-136">Configure your downloaded Spring Boot Application to use Application Insights</span></span>

1. <span data-ttu-id="abef4-137">Recherchez le fichier *POM.xml* dans le répertoire racine de votre application, puis ajoutez la dépendance suivante dans la section de ses dépendances.</span><span class="sxs-lookup"><span data-stu-id="abef4-137">Locate the *POM.xml* file in the root directory of your app, and add the following dependency in its dependencies section.</span></span> 

```XML
 <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>applicationinsights-spring-boot-starter</artifactId>
    <version>1.1.1</version>
</dependency>
```

1. <span data-ttu-id="abef4-138">Recherchez le fichier *application.properties* dans le répertoire *resources* de votre application, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="abef4-138">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Localiser le fichier application.properties][RE01]

1. <span data-ttu-id="abef4-140">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez-y les lignes suivantes, puis remplacez les exemples de valeurs par les propriétés appropriées avec les informations d'identification appropriées :</span><span class="sxs-lookup"><span data-stu-id="abef4-140">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties with appropriate credentials:</span></span>

   ```yaml
   # Specify the instrumentation key of your Application Insights resource.
   azure.application-insights.instrumentation-key=[your ikey from the resource]
   # Specify the name of your springboot application. This can be any logical name you would like to give to your app.
   spring.application.name=[your app name]
   ```

   <span data-ttu-id="abef4-141">Pour connaître plus de façons d’ajuster Application Insights, consultez [le fichier readme de démarrage d’Application Insights Springboot](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="abef4-141">For more ways to fine tune Application Insights please refer to [Application Insights Springboot starter readme](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="abef4-142">Vous pouvez utiliser différentes clés d’instrumentation Application Insights (p. ex.</span><span class="sxs-lookup"><span data-stu-id="abef4-142">You can use different Application Insights instrumentation keys (i.e</span></span> <span data-ttu-id="abef4-143">différentes ressources) pour les différents profils tels que PROD, DEV, etc. Reportez-vous à la page [Propriétés spécifiques du profil Spring Boot] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="abef4-143">different resources) for different profiles like PROD, DEV etc. Please refer to [Spring Boot Profile Specific Properties] for additional information.</span></span> 

1. <span data-ttu-id="abef4-144">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="abef4-144">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="abef4-145">Créez un dossier nommé *controller* sous le dossier source de votre package, par exemple :</span><span class="sxs-lookup"><span data-stu-id="abef4-145">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `D:\Microsoft\demo\src\main\java\com\example\demo\controller`

   <span data-ttu-id="abef4-146">-ou-</span><span class="sxs-lookup"><span data-stu-id="abef4-146">-or-</span></span>

   `/users/example/home/demo/src/main/java/com/example/demo/controller`

1. <span data-ttu-id="abef4-147">Créez un fichier nommé *TestController.java* dans le dossier *controller*.</span><span class="sxs-lookup"><span data-stu-id="abef4-147">Create a new file named *TestController.java* in the *controller* folder.</span></span> <span data-ttu-id="abef4-148">Ouvrez le fichier dans un éditeur de texte, puis ajoutez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="abef4-148">Open the file in a text editor and add the following code to it:</span></span>

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

   <span data-ttu-id="abef4-149">Où vous devez remplacer `com.example.demo` par le nom du package de votre projet.</span><span class="sxs-lookup"><span data-stu-id="abef4-149">Where you will need to replace `com.example.demo` with the package name for your project.</span></span>

1. <span data-ttu-id="abef4-150">Enregistrez et fermez le fichier *TestController.java*.</span><span class="sxs-lookup"><span data-stu-id="abef4-150">Save and close the *TestController.java* file.</span></span>

1. <span data-ttu-id="abef4-151">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="abef4-151">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="abef4-152">Testez l’application web en accédant à http://localhost:8080/sample/hello avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :</span><span class="sxs-lookup"><span data-stu-id="abef4-152">Test the web app by browsing to http://localhost:8080/sample/hello using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080/sample/hello
   ```

   <span data-ttu-id="abef4-153">Le message « Hello ! » de votre exemple de contrôleur</span><span class="sxs-lookup"><span data-stu-id="abef4-153">You should see the "hello!"</span></span> <span data-ttu-id="abef4-154">devrait s’afficher.</span><span class="sxs-lookup"><span data-stu-id="abef4-154">message from your sample controller displayed.</span></span> <span data-ttu-id="abef4-155">Application Insights collectera automatiquement cette requête et l’enverra sous forme d’élément de télémétrie avec son événement personnalisé, sa métrique personnalisée, sa dépendance personnalisée et sa trace personnalisé associées telles que spécifiées dans la logique du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="abef4-155">Application Insights will automatically collect this request and send it as a telemetry item with it's associated custom event, custom metric, custom dependency and custom trace as specified in the controller logic.</span></span> 

   <span data-ttu-id="abef4-156">Après quelques secondes, vous devez voir les données sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="abef4-156">After a few seconds you should see the data on Azure portal.</span></span> 

   ![Portail Azure][AZ05]

   <span data-ttu-id="abef4-158">Vous pouvez cliquer sur la mosaïque de cartographie d’application pour afficher les composants de niveau élevé et leurs interactions.</span><span class="sxs-lookup"><span data-stu-id="abef4-158">You can click on Application Map tile to view high level components and their interaction with each other.</span></span> <span data-ttu-id="abef4-159">Il s’agit d’un emplacement recommandé pour obtenir une vue d’ensemble détaillée de l’ensemble de l’application.</span><span class="sxs-lookup"><span data-stu-id="abef4-159">This is a recommended place to get a high level overview of entire application.</span></span> <span data-ttu-id="abef4-160">Chaque microservice Spring Boot est reconnue par le nom de l’application spring.</span><span class="sxs-lookup"><span data-stu-id="abef4-160">Each Spring Boot Microservice is recognized by the spring application name.</span></span> <span data-ttu-id="abef4-161">Pensez à le définir.</span><span class="sxs-lookup"><span data-stu-id="abef4-161">Please remember to set it.</span></span>

   ![Portail Azure][AZ08] 

## <a name="configure-springboot-application-to-send-log4j-logs-to-application-insights"></a><span data-ttu-id="abef4-163">Configurer l’application Springboot pour envoyer les journaux log4j à Application Insights</span><span class="sxs-lookup"><span data-stu-id="abef4-163">Configure Springboot Application to send log4j logs to Application Insights</span></span>

1. <span data-ttu-id="abef4-164">Modifiez le fichier POM.xml du projet et ajoutez/modifiez la section dépendances avec les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="abef4-164">Modify the POM.xml file of the project and add/modify the dependencies section with following.</span></span> 

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

2. <span data-ttu-id="abef4-165">Enregistrez et fermez le fichier *POM.xml*.</span><span class="sxs-lookup"><span data-stu-id="abef4-165">Save and close the *POM.xml* file.</span></span>

3. <span data-ttu-id="abef4-166">Dans le dossier \src\main\resources, créez un nouveau fichier *log4j2.xml* et configurez-le.</span><span class="sxs-lookup"><span data-stu-id="abef4-166">In \src\main\resources folder, create a new file *log4j2.xml* and configure it.</span></span> <span data-ttu-id="abef4-167">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="abef4-167">For example:</span></span>

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
4. <span data-ttu-id="abef4-168">Générez et exécutez à nouveau l’application Spring Boot comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="abef4-168">Build and run the Spring Boot application again as shown above.</span></span> 

<span data-ttu-id="abef4-169">Au bout de quelques secondes, vous devriez voir tous les journaux spring disponibles sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="abef4-169">Within few seconds, you should see all the spring logs being available on Azure Portal.</span></span> 

![Portail Azure][AZ06]

<span data-ttu-id="abef4-171">Vous pouvez même consulter les messages de journal détaillés et effectuer une analyse sur le Portail Analytics.</span><span class="sxs-lookup"><span data-stu-id="abef4-171">You can even look at the detailed log messages and do analysis on Analytics Portal.</span></span> 

![Portail Azure][AZ07]

## <a name="next-steps"></a><span data-ttu-id="abef4-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="abef4-173">Next steps</span></span>

<span data-ttu-id="abef4-174">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="abef4-174">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abef4-175">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="abef4-175">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="abef4-176">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="abef4-176">Additional Resources</span></span>

<span data-ttu-id="abef4-177">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="abef4-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="abef4-178">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="abef4-178">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="abef4-179">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="abef4-179">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="abef4-180">Application Insights prend en charge la collecte automatique des dépendances externes et leur corrélation avec les requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="abef4-180">Application Insights supports automatic collection of external dependencies and its correlation with incoming requests.</span></span> <span data-ttu-id="abef4-181">Actuellement, nous prenons en charge la collection automatique d’Oracle, MsSQL, MySQL et Redis.</span><span class="sxs-lookup"><span data-stu-id="abef4-181">Currently we support autocollection of Oracle, MsSQL, MySQL and Redis.</span></span> <span data-ttu-id="abef4-182">Pour plus d’informations sur l’activation de la collection automatique, suivez l’article [how to use Application Insights Java agent](/azure/application-insights/app-insights-java-agent) (Comment utiliser l’agent Java Application Insights).</span><span class="sxs-lookup"><span data-stu-id="abef4-182">For more details on enabling autocollection please follow the article [how to use Application Insights Java agent](/azure/application-insights/app-insights-java-agent).</span></span>

<span data-ttu-id="abef4-183">Pour plus d’informations sur Azure Application Insights et ses fonctionnalités de surveillance, consultez la page d’accueil  **[Application Insights]**.</span><span class="sxs-lookup"><span data-stu-id="abef4-183">For more information about Azure Application Insights, and it's monitoring capabilities, see the **[Application Insights]** home page.</span></span>

<span data-ttu-id="abef4-184">Pour plus d’informations sur les détails de configuration supplémentaires d’Application Insights Spring Boot Starter, consultez ce [lien](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span><span class="sxs-lookup"><span data-stu-id="abef4-184">For more information about additional configuration details of Application Insights Spring Boot Starter, please refer to this [link](https://github.com/Microsoft/ApplicationInsights-Java/blob/master/azure-application-insights-spring-boot-starter/README.md).</span></span>

<span data-ttu-id="abef4-185">Pour les demandes de fonctionnalités et les bogues éventuels, faites-le-nous savoir sur notre référentiel [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues).</span><span class="sxs-lookup"><span data-stu-id="abef4-185">For feature requests and potential bugs, please open issues on our [GitHub](https://github.com/Microsoft/ApplicationInsights-Java/issues) repository.</span></span>

<span data-ttu-id="abef4-186">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="abef4-186">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="abef4-187">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="abef4-187">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="abef4-188">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="abef4-188">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="abef4-189">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse [https://github.com/spring-guides/](https://github.com/spring-guides/).</span><span class="sxs-lookup"><span data-stu-id="abef4-189">To help developers get started with Spring Boot, several sample Spring Boot packages are available at [https://github.com/spring-guides/](https://github.com/spring-guides/).</span></span> <span data-ttu-id="abef4-190">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="abef4-190">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Propriétés spécifiques du profil Spring Boot]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
[Spring Boot Profile Specific Properties]: https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html#boot-features-external-config-profile-specific-properties
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
