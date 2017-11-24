---
title: "Déployer une application web Spring Boot sur Linux dans Azure Container Service"
description: "Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot en tant qu’application web Linux sur Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework
ms.assetid: 
ms.service: container-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 8f7b2cbf66c9ceda6f723a9c9d423d94586fc777
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a>Déployer une application Spring Boot sur Linux dans Azure Container Service

**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.

**[client Docker]** est une solution open source qui aide les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.

Ce didacticiel vous guide dans l’utilisation de Docker pour développer et déployer une application Spring Boot sur un hôte Linux dans [Azure Container Service (AKS)].

## <a name="prerequisites"></a>Composants requis

Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* [Azure CLI].
* Un [JDK (Java Developer Kit)] à jour.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [client Git].
* Un [client Docker].

> [!NOTE]
>
> En raison des nécessités liées à la virtualisation de ce didacticiel, vous ne pouvez pas suivre les étapes de cet article sur une machine virtuelle : vous devez utiliser un ordinateur physique où les fonctionnalités de virtualisation sont activées.
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a>Créer l’application web Spring Boot on Docker Getting Started

La procédure suivante vous guide à travers les étapes nécessaires pour créer une application web Spring Boot simple et pour la tester localement.

1. Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire que vous venez de créer. Par exemple :
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Accédez au répertoire du projet terminé. Par exemple :
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Générez le fichier JAR en utilisant Maven. Par exemple :
   ```
   mvn package
   ```

1. Une fois l’application web créée, accédez au répertoire `target` où se trouve fichier JAR et démarrez l’application web. Par exemple :
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Testez l’application web en y accédant localement via un navigateur web. Par exemple, si curl est disponible et que vous configuré le serveur Tomcat pour s’exécuter sur le port 80 :
   ```
   curl http://localhost
   ```

1. Vous devez normalement voir le message suivant : **Hello Docker World!**

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a>Créer un registre de conteneurs Azure à utiliser comme registre Docker privé

Les étapes suivantes vous guident dans l’utilisation du portail Azure pour créer un registre de conteneurs Azure.

> [!NOTE]
>
> Si vous souhaitez utiliser Azure CLI au lieu du portail Azure, suivez les étapes décrites dans [Créer un registre de conteneurs Docker privé à l’aide d’Azure CLI 2.0](/azure/container-registry/container-registry-get-started-azure-cli).
>

1. Accédez au [portail Azure] et connectez-vous.

   Une fois que vous êtes connecté à votre compte sur le portail Azure, vous pouvez suivre les étapes décrites dans l’article [Créer un registre de conteneurs Docker privé à l’aide du portail Azure], qui sont formulées différemment ci-après pour la circonstance.

1. Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Conteneurs** puis cliquez sur **Registre de conteneurs Azure**.
   
   ![Créer un registre de conteneurs Azure][AR01]

1. Quand la page d’informations pour le modèle de registre de conteneurs Azure s’affiche, cliquez sur **Créer**. 

   ![Créer un registre de conteneurs Azure][AR02]

1. Quand la page **Créer un registre de conteneurs** s’affiche, entrez votre **Nom du registre** et votre **Groupe de ressources**, choisissez **Activer** pour **l’utilisateur administrateur**, puis cliquez sur **Créer**.

   ![Configurer les paramètres du registre de conteneurs Azure][AR03]

1. Une fois votre registre de conteneurs créé, accédez à celui-ci dans le portail Azure puis cliquez sur **Clés d’accès**. Notez le nom d’utilisateur et le mot de passe pour les étapes suivantes.

   ![Clés d’accès du registre de conteneurs Azure][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a>Configurer Maven pour utiliser les clés d’accès de votre registre de conteneurs Azure

1. Accédez au répertoire de configuration de votre installation de Maven et ouvrez le fichier *settings.xml* avec un éditeur de texte.

1. Ajoutez les paramètres d’accès de votre registre de conteneurs Azure de la section précédente de ce didacticiel à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.

1. Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion pour votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* de façon à ce que le `<plugin>` contienne l’adresse du serveur de connexion et le nom de registre de votre registre de conteneurs Azure de la section précédente de ce didacticiel. Par exemple :

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Quand vous placez votre conteneur Docker dans Azure, vous pouvez recevoir un message d’erreur similaire à un de ceux-ci, même si votre conteneur Docker a été créé correctement :
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Dans ce cas, vous pouvez être amené à vous connecter à votre compte Azure à partir de la ligne de commande de Docker. Par exemple :
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Vous pouvez ensuite placer votre conteneur à partir de la ligne de commande. Par exemple :
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Créer une application web sur Linux sur Azure App Service en utilisant votre image de conteneur

1. Accédez au [portail Azure] et connectez-vous.

1. Cliquez sur l’icône de menu pour **+ Nouveau**, cliquez sur **Web + Mobile** puis cliquez sur **Application web sur Linux**.
   
   ![Créer une application web dans le portail Azure][LX01]

1. Quand la page **Application web sur Linux** s’affiche, entrez les informations suivantes :

   a. Entrez un nom unique pour le **Nom de l’application**, par exemple : « *wingtiptoyslinux* ».

   b. Choisissez votre **abonnement** dans la liste déroulante.

   c. Choisissez un **Groupe de ressources** existant ou spécifiez un nom pour en créer un.

   d. Cliquez sur **Configurer le conteneur** et entrez les informations suivantes :

      * Choisissez **Registre privé**.

      * **Image et étiquette facultative** : spécifiez le nom de votre conteneur utilisé plus haut, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* »

      * **URL du serveur**: spécifiez l’URL du registre déclaré plus haut, par exemple : « *https://wingtiptoysregistry.azurecr.io* »

      * **Nom d’utilisateur de connexion** et **Mot de passe** : spécifiez vos informations d’identification de connexion des **clés d’accès** que vous avez utilisées dans les étapes précédentes.
   
   e. Après avoir entré toutes les informations ci-dessus, cliquez sur **OK**.

   ![Configurer les paramètres de l’application web][LX02]

1. Cliquez sur **Créer**.

> [!NOTE]
>
> Azure mappera automatiquement les demandes Internet au serveur Tomcat incorporé qui s’exécute sur les ports standard 80 ou 8080. Cependant, si vous avez configuré votre serveur Tomcat incorporé pour qu’il s’exécute sur un port personnalisé, vous devez ajouter une variable d’environnement à votre application web qui définit le port pour votre serveur Tomcat incorporé. Pour ce faire, procédez comme suit :
>
> 1. Accédez au [portail Azure] et connectez-vous.
> 
> 2. Cliquez sur l’icône pour **App Services**. (Voir l’élément 1 de l’image ci-dessous.)
>
> 3. Sélectionnez votre application web dans la liste. (Élément 2 de l’image ci-dessous.)
>
> 4. Cliquez sur **Paramètres de l’application**. (Élément 3 de l’image ci-dessous.)
>
> 5. Dans la section **Paramètres de l’application**, ajoutez une nouvelle variable d’environnement nommée **PORT** et entrez comme valeur votre numéro de port personnalisé. (Élément 4 de l’image ci-dessous.)
>
> 6. Cliquez sur **Save**. (Élément 5 de l’image ci-dessous.)
>
> ![Enregistrement d’un numéro de port personnalisé dans le portail Azure][LX03]
>

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

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur l’exemple de projet Spring Boot on Docker, consultez [Spring Boot on Docker Getting Started].

Pour de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.

Pour plus d’informations sur la création d’une application Spring Boot simple, consultez « Spring Initializr » à l’adresse https://start.spring.io/.

Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-linux/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-linux/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-linux/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-linux/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-linux/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-linux/AR04.png

[LX01]: ./media/deploy-spring-boot-java-app-on-linux/LX01.png
[LX02]: ./media/deploy-spring-boot-java-app-on-linux/LX02.png
[LX03]: ./media/deploy-spring-boot-java-app-on-linux/LX03.png
