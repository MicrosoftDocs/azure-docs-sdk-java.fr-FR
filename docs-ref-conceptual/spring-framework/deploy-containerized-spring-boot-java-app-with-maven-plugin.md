---
title: Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot en conteneur dans Azure
description: Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot dans Azure.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm;kevinzha
ms.date: 02/01/2018
ms.devlang: java
ms.service: app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: d9f2cf5c15bb8f990c8e82fddd6455ecbf8cc02c
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48892690"
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-containerized-spring-boot-app-to-azure"></a>Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot en conteneur dans Azure

Cet article présente l’utilisation du [plug-in Maven pour Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) afin de déployer un exemple d’application Spring Boot dans un conteneur Docker dans Azure App Services.

> [!NOTE]
> 
> Le plug-in Maven pour Azure Web Apps pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web dans Azure App Services.
> 
> Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire. Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.
> 

## <a name="prerequisites"></a>Prérequis

Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* [Azure CLI].
* Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [Git].
* Un [Docker].

> [!NOTE]
>
> En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.
>

## <a name="clone-the-sample-spring-boot-on-docker-web-app"></a>Cloner l’exemple Spring Boot sur l’application web Docker

Dans cette section, vous clonez une application Spring Boot en conteneur et vous la testez localement.

1. Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker
   ```

1. Accédez au répertoire du projet terminé. Par exemple :
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Vous devez normalement voir le message suivant : **Hello Docker World**

## <a name="create-an-azure-service-principal"></a>Créer un principal du service Azure

Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre conteneur dans Azure.

1. Ouvrez une invite de commandes.

2. Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :
   ```shell
   az login
   ```
   Suivez les instructions pour terminer le processus de connexion.

3. Créez un principal du service Azure :
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Où :

   | Paramètre  |                    Description                     |
   |------------|----------------------------------------------------|
   | `uuuuuuuu` | Spécifie le nom d’utilisateur pour le principal de service. |
   | `pppppppp` | Spécifie le mot de passe pour le principal de service.  |


4. Azure répond avec un texte JSON similaire à l’exemple suivant :
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre conteneur dans Azure. `aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a>Configurer Maven pour utiliser votre principal du service Azure

Dans cette section, vous utilisez les valeurs de votre principal du service Azure pour configurer l’authentification qui sera utilisée par Maven lors du déploiement de votre conteneur dans Azure.

1. Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

2. Ajoutez les paramètres de votre principal du service Azure de la section précédente de ce didacticiel à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Où :

   |     Élément     |                                                                                   Description                                                                                   |
   |-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |     `<id>`      |                                Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.                                |
   |   `<client>`    |                                                             Contient la valeur `appId` de votre principal du service.                                                             |
   |   `<tenant>`    |                                                            Contient la valeur `tenant` de votre principal du service.                                                             |
   |     `<key>`     |                                                           Contient la valeur `password` de votre principal du service.                                                            |
   | `<environment>` | Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple. (Une liste complète des environnements est disponible dans la documentation [Plug-in Maven pour Azure Web Apps]) |


3. Enregistrez et fermez le fichier *settings.xml*.

## <a name="optional-deploy-your-local-docker-file-to-docker-hub"></a>FACULTATIF : Déployer votre fichier Docker local dans Docker Hub

Si vous avez un compte Docker, vous pouvez générer votre image de conteneur Docker localement et la placer dans Docker Hub. Pour ce faire, procédez comme suit.

1. Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte.

1. Recherchez l’élément `<imageName>` enfant de l’élément `<containerSettings>`.

1. Mettez à jour la valeur `${docker.image.prefix}` avec le nom de votre compte Docker :
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. Choisissez l’une des méthodes de déploiement suivantes :

   * Générez votre image de conteneur localement avec Maven, puis utilisez Docker pour placer votre conteneur dans Docker Hub :
      ```shell
      mvn clean package docker:build
      docker push
      ```

   * Si vous avez le [plug-in Docker pour Maven] installé, vous pouvez générer automatiquement votre image de conteneur dans Docker Hub à l’aide du paramètre `-DpushImage` :
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-to-azure"></a>FACULTATIF : Personnaliser votre fichier pom.xml avant de déployer votre conteneur dans Azure

Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`. Cet élément doit ressembler à l’exemple suivant :

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Plug-in Maven pour Azure Web Apps] (Plug-in Maven pour Azure Web Apps). Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :

| Élément | Description |
|---|---|
| `<version>` | Spécifie la version du [plug-in Maven pour Azure Web Apps]. Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente. |
| `<authentication>` | Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article. |
| `<resourceGroup>` | Spécifie le groupe de ressources cible, qui est `maven-plugin` dans cet exemple. Il sera créé au cours du déploiement s’il n’existe pas. |
| `<appName>` | Spécifie le nom cible de votre application web. Dans cet exemple, le nom cible est `maven-linux-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit. (L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.) |
| `<region>` | Spécifie la région cible, qui dans cet exemple est `westus`. (Une liste complète est disponible dans la documentation [Plug-in Maven pour Azure Web Apps].) |
| `<appSettings>` | Spécifie des paramètres uniques que Maven utilisera lors du déploiement de votre application web dans Azure. Dans cet exemple, un élément `<property>` contient une paire nom/valeur d’éléments enfants qui spécifie le port pour votre application. |

> [!NOTE]
>
> Les paramètres de modification du numéro de port fournis dans cet exemple sont nécessaires uniquement lorsque vous modifiez le port à partir de la valeur par défaut.
>

## <a name="build-and-deploy-your-container-to-azure"></a>Créer et déployer votre conteneur dans Azure

Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre conteneur dans Azure. Pour ce faire, procédez comme suit :

1. À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :
   ```shell
   mvn clean package
   ```

1. Déployez votre application web dans Azure à l’aide de Maven ; par exemple :
   ```shell
   mvn azure-webapp:deploy
   ```

Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.

> [!NOTE]
>
> Si la région que vous spécifiez dans l’élément `<region>` de votre fichier *pom.xml* n’a pas suffisamment de serveurs disponibles lorsque vous démarrez votre déploiement, vous pouvez voir un message d’erreur similaire à l’exemple suivant :
>
> ```
> [INFO] Start deploying to Web App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed to execute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Dans ce cas, vous pouvez spécifier une autre région et ré-exécuter la commande Maven pour déployer votre application.
>
>

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

* [Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot dans Azure App Services ](deploy-spring-boot-java-app-with-maven-plugin.md)

* [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Référence des paramètres Maven](https://maven.apache.org/settings.html)

* [Plug-in Docker pour Maven]

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portail Azure]: https://portal.azure.com/
[Docker]: https://www.docker.com/
[Plug-in Docker pour Maven]: https://github.com/spotify/docker-maven-plugin
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Plug-in Maven pour Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-containerized-spring-boot-java-app-with-maven-plugin/AP02.png
