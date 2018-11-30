---
title: Déployer le fichier JAR d’une application Spring Boot sur le cloud avec Maven et Azure
description: Découvrez comment déployer une application Spring Boot sur le cloud à l’aide du plug-in Maven pour Azure Web App pour Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 11/21/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 066ac30697c6adccc0c6a7b9d57205de488bdc53
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52339003"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Déployer le fichier JAR d’une application web Spring Boot sur Azure App Service sur Linux

Cet article présente l’utilisation du [plug-in Maven pour Azure App Service Web Apps](https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) afin de déployer un package d’application Java SE JAR sur [Azure App Service sur Linux](https://docs.microsoft.com/en-us/azure/app-service/containers/). Choisissez le déploiement Java SE sur les [fichiers Tomcat et WAR](/azure/app-service/containers/quickstart-java) lorsque vous voulez consolider les dépendances de vos applications, ainsi que leur runtime et leur configuration dans un seul artefact déployable.


Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="prerequisites"></a>Prérequis

Pour effectuer les étapes de ce didacticiel, les éléments suivants doivent être installés et configurés :

* [Azure CLI](/cli/azure/), en local ou via [Azure Cloud Shell](https://shell.azure.com).
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* Apache [Maven](https://maven.apache.org/), version 3.
* Un client [Git](https://git-scm.com/downloads).

## <a name="install-and-sign-in-to-azure-cli"></a>Installer Azure CLI et se connecter

La façon la plus simple et la plus rapide que le Plugin Maven déploie votre application Spring Boot est d’utiliser[Azure CLI](https://docs.microsoft.com/cli/azure/).

Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :
   
   ```shell
   az login
   ```
   
Suivez les instructions pour terminer le processus de connexion.

## <a name="clone-the-sample-app"></a>Clonage de l’exemple d’application

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

## <a name="configure-maven-plugin-for-azure-app-service"></a>Configurer le plug-in Maven pour Azure App Service

Dans cette section, vous allez configurer le projet Spring Boot `pom.xml` pour que Maven puisse déployer l’application sur Azure App Service sur Linux.

1. Ouvrez `pom.xml` dans un éditeur de code.

2. Dans la section `<build>` du fichier pom.xml, ajoutez l’entrée suivante `<plugin>` dans la balise `<plugins>`.

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. Mettez à jour les espaces réservés suivants dans la configuration du plug-in :

| Placeholder | Description |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | Nom du nouveau groupe de ressources dans lequel créer votre application web. En plaçant toutes les ressources d’une application dans un groupe, vous pouvez les gérer ensemble. Par exemple, si vous supprimez le groupe de ressources, vous supprimez également toutes les ressources associées à l’application. Mettez à jour cette valeur avec un nouveau nom de groupe de ressources unique, par exemple, *TestResources*. Vous utiliserez ce nom de groupe de ressources pour nettoyer toutes les ressources Azure dans une section ultérieure. |
| `WEBAPP_NAME` | Le nom d’application fera partie du nom d’hôte pour l’application web lors du déploiement vers Azure (WEBAPP_NAME.azurewebsites.net). Mettez à jour cette valeur avec un nom unique pour la nouvelle application web Azure, qui va héberger votre application Java, par exemple *contoso*. |
| `REGION` | Une région Azure où l’application web est hébergée, par exemple `westus2`. Vous pouvez obtenir une liste de régions à partir du Cloud Shell ou de l’interface CLI à l’aide de la commande `az account list-locations`. |

Une liste complète de configuration est disponible dans les [références du plug-in Maven sur GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).

## <a name="deploy-the-app-to-azure"></a>Déploiement de l’application dans Azure

Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre application web dans Azure. Pour ce faire, procédez comme suit :

1. À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :
   ```shell
   mvn clean package
   ```

1. Déployez votre application web dans Azure à l’aide de Maven ; par exemple :
   ```shell
   mvn azure-webapp:deploy
   ```

Maven déploie votre application web dans Azure. Si l’application web ou le plan de l’application web n’existe pas déjà, il ou elle sera créé(e).

Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].

* Votre application web s’affichera dans **App Services** :

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :

   ![Détermination de l’URL de votre application web][AP02]

Vérifiez que le déploiement a été effectué en utilisant la même commande cURL qu’auparavant, en utilisant l’URL de votre application web du portail au lieu de `localhost`. Vous devez normalement voir le message suivant : **Greetings from Spring Boot!** 

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :

* [Plug-in Maven pour Azure Web Apps]

* [Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot conteneurisée dans Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Référence des paramètres Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portail Azure]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in Maven pour Azure Web Apps]: https://docs.microsoft.com/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
