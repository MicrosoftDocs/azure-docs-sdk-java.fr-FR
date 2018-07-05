---
title: Déployer une application Spring Boot sur le cloud avec Maven et Azure
description: Découvrez comment déployer une application Spring Boot sur le cloud à l’aide du plug-in Maven pour Azure Web Apps.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: brborges
ms.assetid: ''
ms.author: robmcm;kevinzha;brborges
ms.date: 06/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 3610312ed17301131967bd2c047c86656de070e7
ms.sourcegitcommit: f313c14e92f38c54a3a583270ee85cc928cd39d7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34689422"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a><span data-ttu-id="3e436-103">Déployer une application Spring Boot sur le cloud à l’aide du plug-in Maven pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3e436-103">Deploy a Spring Boot app to the cloud using the Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="3e436-104">Cet article présente l’utilisation du plug-in Maven pour Azure App Service Web Apps afin de déployer un exemple d’application Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="3e436-104">This article demonstrates using the Maven Plugin for Azure App Service Web Apps to deploy a sample Spring Boot application.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="3e436-105">Le [plug-in Maven pour Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web sur Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="3e436-105">The [Maven Plugin for Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="3e436-106">Avant d’utiliser le plugin Maven, consultez Maven Central et recherchez la dernière version du plugin disponible : [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span><span class="sxs-lookup"><span data-stu-id="3e436-106">Before using the Maven plugin, check on Maven Central for the latest available version of the plugin: [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22)</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3e436-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="3e436-107">Prerequisites</span></span>

<span data-ttu-id="3e436-108">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3e436-108">In order to complete the steps in this tutorial, you will need to have the following prerequisites:</span></span>

* <span data-ttu-id="3e436-109">Abonnement Azure ; si vous ne disposez pas d’un abonnement Azure, vous pouvez vous inscrire pour [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="3e436-109">An Azure subscription; if you don't already have an Azure subscription, you can sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3e436-110">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="3e436-110">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="3e436-111">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3e436-111">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="3e436-112">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="3e436-112">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3e436-113">Un [Git].</span><span class="sxs-lookup"><span data-stu-id="3e436-113">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="3e436-114">Cloner l’exemple d’application web Spring Boot</span><span class="sxs-lookup"><span data-stu-id="3e436-114">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="3e436-115">Dans cette section, vous allez cloner une application Spring Boot terminée et la tester localement.</span><span class="sxs-lookup"><span data-stu-id="3e436-115">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="3e436-116">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-116">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3e436-117">- ou -</span><span class="sxs-lookup"><span data-stu-id="3e436-117">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="3e436-118">Clonez l’exemple de projet [Spring Boot Getting Started] dans le répertoire que vous avez créé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-118">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="3e436-119">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-119">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="3e436-120">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-120">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="3e436-121">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-121">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="3e436-122">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="3e436-122">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="3e436-123">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="3e436-123">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="3e436-124">Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="3e436-124">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a><span data-ttu-id="3e436-125">Ajuster le projet pour un déploiement WAR sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3e436-125">Adjust project for WAR-based deployment on Azure App Service</span></span>

<span data-ttu-id="3e436-126">Dans cette section, nous ajusterons rapidement le projet Spring Boot afin de le déployer en tant fichier WAR sur Azure App Service, pour laquelle Tomcat est le runtime par défaut.</span><span class="sxs-lookup"><span data-stu-id="3e436-126">In this section we will quickly adjust the Spring Boot project to be deployed as a WAR file on Azure App Service, which provides Tomcat as the runtime by default.</span></span> <span data-ttu-id="3e436-127">Pour mener à bien cette tâche, deux fichiers doivent être modifiés :</span><span class="sxs-lookup"><span data-stu-id="3e436-127">For this to work, there are two files to be modified:</span></span>

- <span data-ttu-id="3e436-128">Le fichier Maven `pom.xml`</span><span class="sxs-lookup"><span data-stu-id="3e436-128">The Maven `pom.xml` file</span></span>
- <span data-ttu-id="3e436-129">La classe Java `Application`</span><span class="sxs-lookup"><span data-stu-id="3e436-129">The `Application` Java class</span></span>

<span data-ttu-id="3e436-130">Commençons par les paramètres Maven :</span><span class="sxs-lookup"><span data-stu-id="3e436-130">Let's start with the Maven settings:</span></span>

1. <span data-ttu-id="3e436-131">Ouvrez `pom.xml`</span><span class="sxs-lookup"><span data-stu-id="3e436-131">Open `pom.xml`</span></span>

1. <span data-ttu-id="3e436-132">Ajoutez `<packaging>war</packaging>` juste après la définition `<artifactId>` en haut :</span><span class="sxs-lookup"><span data-stu-id="3e436-132">Add `<packaging>war</packaging>` right after the `<artifactId>` definition at the top:</span></span>
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. <span data-ttu-id="3e436-133">Ajoutez la dépendance suivante :</span><span class="sxs-lookup"><span data-stu-id="3e436-133">Add the following dependency:</span></span>
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

<span data-ttu-id="3e436-134">Ouvrez maintenant la classe `Application`, de préférence après que votre IDE ait intégré les nouvelles dépendances, et effectuez les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e436-134">Now open the class `Application`, hopefully after your IDE has already picked up the new dependencies, and proceed with the following modifications:</span></span>

1. <span data-ttu-id="3e436-135">Transformez la classe Application en une sous-classe de `SpringBootServletInitializer` :</span><span class="sxs-lookup"><span data-stu-id="3e436-135">Make class Application a subclass of `SpringBootServletInitializer`:</span></span>
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. <span data-ttu-id="3e436-136">Ajoutez la méthode suivante à la classe Application :</span><span class="sxs-lookup"><span data-stu-id="3e436-136">Add the following method to the Application class:</span></span>
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```

<span data-ttu-id="3e436-137">Votre application est maintenant prête à être déployée vers Tomcat et tout autre runtime Servlet (p. ex. Jetty).</span><span class="sxs-lookup"><span data-stu-id="3e436-137">Your application is now ready to be deployed to Tomcat and any other Servlet runtime (e.g. Jetty).</span></span>

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a><span data-ttu-id="3e436-138">Ajouter le plugin Maven pour Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="3e436-138">Add the Maven Plugin for Azure App Service Web Apps</span></span>

<span data-ttu-id="3e436-139">Dans cette section, nous allons ajouter un plugin Maven qui automatise l’intégralité du déploiement de cette application dans Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="3e436-139">In this section, we will add a Maven plugin that will automate the entire deployment of this application into Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="3e436-140">Ouvrez une autre fois `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="3e436-140">Open `pom.xml` once again.</span></span>

1. <span data-ttu-id="3e436-141">Dans `<properties>`, paramétrez un format de timestamp personnalisé avec la propriété `maven.build.timestamp.format`.</span><span class="sxs-lookup"><span data-stu-id="3e436-141">Inside `<properties>`, set a custom timestamp format with the property `maven.build.timestamp.format`.</span></span> <span data-ttu-id="3e436-142">Du fait qu’Azure App Service crée une URL publique pour votre application, ce paramètre sera utilisé pour générer le nom de votre déploiement, et éviter les conflits avec les déploiements en cours d’autres utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3e436-142">Because Azure App Service creates a public URL for your application, this setting will be used to generate the name of your deployment, and avoid conflict with other users' live deployments.</span></span>
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. <span data-ttu-id="3e436-143">Dans l’élément `<plugins>`, ajoutez l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="3e436-143">In the `<plugins>` element, add the following:</span></span>
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

<span data-ttu-id="3e436-144">Grâce à ces paramètres, votre projet Maven est prêt pour la mise en ligne sur Azure App Service Web App.</span><span class="sxs-lookup"><span data-stu-id="3e436-144">With these settings, your Maven project is now ready for live deployment to Azure App Service Web App.</span></span>

## <a name="install-and-log-in-to-azure-cli"></a><span data-ttu-id="3e436-145">Installer Azure CLI et se connecter</span><span class="sxs-lookup"><span data-stu-id="3e436-145">Install and log in to Azure CLI</span></span>

<span data-ttu-id="3e436-146">La façon la plus simple et la plus rapide que le Plugin Maven déploie votre application Spring Boot est d’utiliser[Azure CLI](https://docs.microsoft.com/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="3e436-146">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](https://docs.microsoft.com/cli/azure/).</span></span> <span data-ttu-id="3e436-147">Assurez-vous de l’avoir installé.</span><span class="sxs-lookup"><span data-stu-id="3e436-147">Make sure you have it installed.</span></span>

1. <span data-ttu-id="3e436-148">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="3e436-148">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="3e436-149">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="3e436-149">Follow the instructions to complete the sign-in process.</span></span>

## <a name="optionally-customize-pomxml-before-deploying"></a><span data-ttu-id="3e436-150">Vous pouvez personnaliser pom.xml avant le déploiement (facultatif)</span><span class="sxs-lookup"><span data-stu-id="3e436-150">Optionally, customize pom.xml before deploying</span></span>

<span data-ttu-id="3e436-151">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="3e436-151">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="3e436-152">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3e436-152">This element should resemble the following example:</span></span>

   ```xml
  <plugins>
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
      <configuration>
         <resourceGroup>maven-projects</resourceGroup>
         <appName>${project.artifactId}-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>war</deploymentType>
      </configuration>
    </plugin>
  </plugins>
   ```

<span data-ttu-id="3e436-153">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Plug-in Maven pour Azure Web Apps] (Plug-in Maven pour Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="3e436-153">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="3e436-154">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="3e436-154">That being said, there are several values that are worth highlighting in this article:</span></span>

| <span data-ttu-id="3e436-155">Élément</span><span class="sxs-lookup"><span data-stu-id="3e436-155">Element</span></span> | <span data-ttu-id="3e436-156">Description</span><span class="sxs-lookup"><span data-stu-id="3e436-156">Description</span></span> |
|---|---|
| `<version>` | <span data-ttu-id="3e436-157">Spécifie la version du [plug-in Maven pour Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="3e436-157">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="3e436-158">Vérifiez la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="3e436-158">Verify the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span> |
| `<resourceGroup>` | <span data-ttu-id="3e436-159">Spécifie le groupe de ressources cible, qui est `maven-plugin` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="3e436-159">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="3e436-160">Il est créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="3e436-160">The resource group is created during deployment if it does not already exist.</span></span> |
| `<appName>` | <span data-ttu-id="3e436-161">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3e436-161">Specifies the target name for your web app.</span></span> <span data-ttu-id="3e436-162">Dans cet exemple, le nom cible est `maven-web-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="3e436-162">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="3e436-163">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="3e436-163">(The timestamp is optional; you can specify any unique string for the app name.)</span></span> |
| `<region>` | <span data-ttu-id="3e436-164">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="3e436-164">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="3e436-165">(Une liste complète est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="3e436-165">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<javaVersion>` | <span data-ttu-id="3e436-166">Spécifie la version du runtime Java de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3e436-166">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="3e436-167">(Une liste complète est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="3e436-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span> |
| `<deploymentType>` | <span data-ttu-id="3e436-168">Spécifie le type de déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3e436-168">Specifies deployment type for your web app.</span></span> <span data-ttu-id="3e436-169">La valeur par défaut est `war`.</span><span class="sxs-lookup"><span data-stu-id="3e436-169">Default is `war`.</span></span> |

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="3e436-170">Créer et déployer votre application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="3e436-170">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="3e436-171">Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3e436-171">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="3e436-172">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e436-172">To do so, use the following steps:</span></span>

1. <span data-ttu-id="3e436-173">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-173">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="3e436-174">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="3e436-174">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="3e436-175">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="3e436-175">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="3e436-176">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="3e436-176">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="3e436-177">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="3e436-177">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="3e436-179">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="3e436-179">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="3e436-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e436-181">Next steps</span></span>

<span data-ttu-id="3e436-182">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="3e436-182">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="3e436-183">[Plug-in Maven pour Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="3e436-183">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="3e436-184">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="3e436-184">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="3e436-185">Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot conteneurisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="3e436-185">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="3e436-186">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3e436-186">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="3e436-187">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="3e436-187">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in Maven pour Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
