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
ms.openlocfilehash: ca788354d26964bd9f1e21a0d3a8005ff65ce4bc
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324345"
---
# <a name="deploy-a-spring-boot-app-to-the-cloud-using-the-maven-plugin-for-azure-app-service"></a>Déployer une application Spring Boot sur le cloud à l’aide du plug-in Maven pour Azure App Service

Cet article présente l’utilisation du plug-in Maven pour Azure App Service Web Apps afin de déployer un exemple d’application Spring Boot.

> [!NOTE]
> 
> Le [plug-in Maven pour Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web sur Azure App Service.

Avant d’utiliser le plugin Maven, consultez Maven Central et recherchez la dernière version du plugin disponible : [![Maven Central](https://img.shields.io/maven-central/v/com.microsoft.azure/azure-webapp-maven-plugin.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-webapp-maven-plugin%22) 

## <a name="prerequisites"></a>Prérequis

Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :

* Abonnement Azure ; si vous ne disposez pas d’un abonnement Azure, vous pouvez vous inscrire pour un [compte Azure gratuit].
* [Azure CLI].
* Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [Git].

## <a name="clone-the-sample-spring-boot-web-app"></a>Cloner l’exemple d’application web Spring Boot

Dans cette section, vous allez cloner une application Spring Boot terminée et la tester localement.

1. Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. Clonez l’exemple de projet [Spring Boot Getting Started] dans le répertoire que vous avez créé. Par exemple :
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. Accédez au répertoire du projet terminé. Par exemple :
   ```shell
   cd gs-spring-boot/complete
   ```

1. Générez le fichier JAR en utilisant Maven. Par exemple :
   ```shell
   mvn clean package
   ```

1. Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :
   ```shell
   mvn spring-boot:run
   ```

1. Testez l’application web en y accédant localement via un navigateur web. Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :
   ```shell
   curl http://localhost:8080
   ```

1. Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**

## <a name="adjust-project-for-war-based-deployment-on-azure-app-service"></a>Ajuster le projet pour un déploiement WAR sur Azure App Service

Dans cette section, nous ajusterons rapidement le projet Spring Boot afin de le déployer en tant fichier WAR sur Azure App Service, pour laquelle Tomcat est le runtime par défaut. Pour mener à bien cette tâche, deux fichiers doivent être modifiés :

- Le fichier Maven `pom.xml`
- La classe Java `Application`

Commençons par les paramètres Maven :

1. Ouvrez `pom.xml`

1. Ajoutez `<packaging>war</packaging>` juste après la définition `<artifactId>` en haut :
   ```xml
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.springframework</groupId>
    <artifactId>gs-spring-boot</artifactId>

    <packaging>war</packaging>
   ```

1. Ajoutez la dépendance suivante :
   ```xml
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
   ```

Ouvrez maintenant la classe `Application`, de préférence après que votre IDE ait intégré les nouvelles dépendances, et effectuez les modifications suivantes :

1. Transformez la classe Application en une sous-classe de `SpringBootServletInitializer` :
   ```java
   @SpringBootApplication
   public class Application extends SpringBootServletInitializer {
     // ...
   }
   ```

1. Ajoutez la méthode suivante à la classe Application :
   ```java
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           return application.sources(Application.class);
       }
   ```
1. Organisez vos imports pour garantir l’import de `SpringApplicationBuilder` et `SpringBootServletInitializer`.

Votre application est maintenant prête à être déployée vers Tomcat et tout autre runtime Servlet (p. ex. Jetty).

## <a name="add-the-maven-plugin-for-azure-app-service-web-apps"></a>Ajouter le plugin Maven pour Azure App Service Web Apps

Dans cette section, nous allons ajouter un plugin Maven qui automatise l’intégralité du déploiement de cette application dans Azure App Service Web Apps.

1. Ouvrez une autre fois `pom.xml`.

1. Dans `<properties>`, paramétrez un format de timestamp personnalisé avec la propriété `maven.build.timestamp.format`. Du fait qu’Azure App Service crée une URL publique pour votre application, ce paramètre sera utilisé pour générer le nom de votre déploiement, et éviter les conflits avec les déploiements en cours d’autres utilisateurs.
   ```xml
    <properties>
        <java.version>1.8</java.version>
        <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
    </properties>
   ```

1. Dans l’élément `<plugins>`, ajoutez l’extrait de code suivant :
   ```xml
    <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <!-- Check latest version on Maven Central -->
      <version>1.1.0</version>
    </plugin>
   ```

Grâce à ces paramètres, votre projet Maven est prêt pour la mise en ligne sur Azure App Service Web App.

## <a name="install-and-log-in-to-azure-cli"></a>Installer Azure CLI et se connecter

La façon la plus simple et la plus rapide que le Plugin Maven déploie votre application Spring Boot est d’utiliser[Azure CLI](https://docs.microsoft.com/cli/azure/). Assurez-vous de l’avoir installé.

1. Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :
   
   ```shell
   az login
   ```
   
   Suivez les instructions pour terminer le processus de connexion.

## <a name="optionally-customize-pomxml-before-deploying"></a>Vous pouvez personnaliser pom.xml avant le déploiement (facultatif)

Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`. Cet élément doit ressembler à l’exemple suivant :

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

Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Plug-in Maven pour Azure Web Apps] (Plug-in Maven pour Azure Web Apps). Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :

| Élément | Description |
|---|---|
| `<version>` | Spécifie la version du [plug-in Maven pour Azure Web Apps]. Vérifiez la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente. |
| `<resourceGroup>` | Spécifie le groupe de ressources cible, qui est `maven-plugin` dans cet exemple. Il est créé au cours du déploiement s’il n’existe pas. |
| `<appName>` | Spécifie le nom cible de votre application web. Dans cet exemple, le nom cible est `maven-web-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit. (L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.) |
| `<region>` | Spécifie la région cible, qui dans cet exemple est `westus`. (Une liste complète est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].) |
| `<javaVersion>` | Spécifie la version du runtime Java de votre application web. (Une liste complète est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].) |
| `<deploymentType>` | Spécifie le type de déploiement de votre application web. La valeur par défaut est `war`. |

## <a name="build-and-deploy-your-web-app-to-azure"></a>Créer et déployer votre application web dans Azure

Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre application web dans Azure. Pour ce faire, procédez comme suit :

1. À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :
   ```shell
   mvn clean package
   ```

1. Déployez votre application web dans Azure à l’aide de Maven ; par exemple :
   ```shell
   mvn azure-webapp:deploy
   ```

Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.

Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].

* Votre application web s’affichera dans **App Services** :

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :

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

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :

* [Plug-in Maven pour Azure Web Apps]

* [Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure](/azure/xplat-cli-connect)

* [Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot conteneurisée dans Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Référence des paramètres Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portail Azure]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in Maven pour Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
