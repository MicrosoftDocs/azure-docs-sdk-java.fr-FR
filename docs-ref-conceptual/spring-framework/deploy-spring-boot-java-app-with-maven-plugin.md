---
title: Déployer le fichier JAR d’une application Spring Boot sur le cloud avec Maven et Azure
description: Découvrez comment déployer une application Spring Boot sur le cloud à l’aide du plug-in Maven pour Azure Web App pour Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: b133290d1f14429cbf36d6ed5a67d27e1a637593
ms.sourcegitcommit: 599405a9ce892d75073ef0776befa2fa22407b4c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67237598"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a>Déployer le fichier JAR d’une application web Spring Boot sur Azure App Service sur Linux

Cet article présente l’utilisation du [plug-in Maven pour Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) afin de déployer un package d’application Java SE JAR sur [Azure App Service sur Linux](/azure/app-service/containers/). Choisissez le déploiement Java SE sur les [fichiers Tomcat et WAR](/azure/app-service/containers/quickstart-java) lorsque vous voulez consolider les dépendances de vos applications, ainsi que leur runtime et leur configuration dans un seul artefact déployable.


Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="prerequisites"></a>Prérequis

Pour effectuer les étapes de ce didacticiel, les éléments suivants doivent être installés et configurés :

* [Azure CLI](/cli/azure/), en local ou via [Azure Cloud Shell](https://shell.azure.com).
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* Apache [Maven](https://maven.apache.org/), version 3.
* Un client [Git](https://git-scm.com/downloads).

## <a name="install-and-sign-in-to-azure-cli"></a>Installer Azure CLI et se connecter

La façon la plus simple et la plus rapide que le Plugin Maven déploie votre application Spring Boot est d’utiliser[Azure CLI](/cli/azure/).

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
   \- ou -
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

1. Vous devriez voir le message suivant : **Greetings from Spring Boot!**

## <a name="configure-maven-plugin-for-azure-app-service"></a>Configurer le plug-in Maven pour Azure App Service

Dans cette section, vous allez configurer le projet Spring Boot `pom.xml` pour que Maven puisse déployer l’application sur Azure App Service sur Linux.

1. Ouvrez `pom.xml` dans un éditeur de code.

2. Dans la section `<build>` du fichier pom.xml, ajoutez l’entrée suivante `<plugin>` dans la balise `<plugins>`.

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.6.0</version>
   </plugin>
   ```

3. Vous pouvez ensuite configurer le déploiement, exécuter la commande maven `mvn azure-webapp:config` à l’invite de commandes et utiliser le **nombre** pour choisir ces options dans l’invite :
    * **Système d’exploitation** : linux  
    * **javaVersion** : jre8
    * **runtimeStack** : jre8

Si vous obtenez l’invite **Confirmer (O/N)** , appuyez sur **'y'** et la configuration est terminée.

```cmd
~@Azure:~/gs-spring-boot/complete$ mvn azure-webapp:config
[INFO] Scanning for projects...
[INFO]
[INFO] -----------------< org.springframework:gs-spring-boot >-----------------
[INFO] Building gs-spring-boot 0.1.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- azure-webapp-maven-plugin:1.6.0:config (default-cli) @ gs-spring-boot ---
[WARNING] The plugin may not work if you change the os of an existing webapp.
Define value for OS(Default: Linux):
1. linux [*]
2. windows
3. docker
Enter index to use:
Define value for javaVersion(Default: jre8):
1. jre8 [*]
2. java11
Enter index to use:
Define value for runtimeStack(Default: TOMCAT 8.5):
1. TOMCAT 9.0
2. jre8
3. TOMCAT 8.5 [*]
4. WILDFLY 14
Enter index to use: 2
Please confirm webapp properties
AppName : gs-spring-boot-1559091271202
ResourceGroup : gs-spring-boot-1559091271202-rg
Region : westeurope
PricingTier : Premium_P1V2
OS : Linux
RuntimeStack : JAVA 8-jre8
Deploy to slot : false
Confirm (Y/N)? : Y
```

4. Ajoutez la section `<appSettings>` à la section `<configuration>` de `<azure-webapp-maven-plugin>` pour écouter sur le port *80*.

    ```xml
   <plugin>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-webapp-maven-plugin</artifactId>
       <version>1.6.0</version>
       <configuration>
          <schemaVersion>V2</schemaVersion>
          <resourceGroup>gs-spring-boot-1559091271202-rg</resourceGroup>
          <appName>gs-spring-boot-1559091271202</appName>
          <region>westeurope</region>
          <pricingTier>P1V2</pricingTier>

          <!-- Begin of App Settings  -->
          <appSettings>
             <property>
                   <name>JAVA_OPTS</name>
                   <value>-Dserver.port=80</value>
             </property>
          </appSettings>
          <!-- End of App Settings  -->
          ...
         </configuration>
   </plugin>
   ```

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

Vérifiez que le déploiement a été effectué en utilisant la même commande cURL qu’auparavant, en utilisant l’URL de votre application web du portail au lieu de `localhost`. Vous devriez voir le message suivant : **Greetings from Spring Boot!** 

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :

* [Plug-in Maven pour Azure Web Apps]

* [Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot conteneurisée dans Azure](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Référence des paramètres Maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Portail Azure]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in Maven pour Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
