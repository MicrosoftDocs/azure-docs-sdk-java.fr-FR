---
title: Déployer une application web Spring Boot sur Azure App Service pour conteneur
description: Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot en tant qu’application web Linux sur Microsoft Azure.
services: azure app service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: azure app service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 407b852e24ef88d2fb075bd064f1acf2b107ddc1
ms.sourcegitcommit: 394521c47ac9895d00d9f97535cc9d1e27d08fe9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270865"
---
# <a name="deploy-a-spring-boot-application-on-azure-app-service-for-container"></a>Déployer une application Spring Boot sur Azure App Service pour conteneur

Ce tutoriel vous guide dans l’utilisation de [Docker] pour conteneuriser votre application [Spring Boot] et déployer votre propre image docker sur un hôte Linux dans [Azure App Service](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).

## <a name="prerequisites"></a>Prérequis

Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* [Azure CLI].
* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un client [Git].
* Un client [Docker].

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

1. Vous devriez voir le message suivant : **Hello Docker World!**

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

1. Accédez au répertoire du projet terminé pour votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.

1. Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la dernière version de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) ainsi que la valeur du serveur de connexion et les paramètres d’accès pour votre registre de conteneurs Azure obtenus à la section précédente de ce tutoriel. Par exemple :

   ```xml
   <properties>
      <jib-maven-plugin.version>1.2.0</jib-maven-plugin.version>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <username>wingtiptoysregistry</username>
      <password>{put your Azure Container Registry access key here}</password>
   </properties>
   ```

1. Ajoutez [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin) à la collection `<plugins>` dans le fichier *pom.xml*, spécifiez l’image de base à `<from>/<image>` et le nom de l’image finale `<to>/<image>`, puis spécifiez le nom d’utilisateur et le mot de passe de la section précédente à `<to>/<auth>`. Par exemple :

   ```xml
   <plugin>
     <artifactId>jib-maven-plugin</artifactId>
     <groupId>com.google.cloud.tools</groupId>
     <version>${jib-maven-plugin.version}</version>
     <configuration>
        <from>
            <image>openjdk:8-jre-alpine</image>
        </from>
        <to>
            <image>${docker.image.prefix}/${project.artifactId}</image>
            <auth>
               <username>${username}</username>
               <password>${password}</password>
            </auth>
        </to>
     </configuration>
   </plugin>
   ```

1. Accédez au répertoire du projet terminé de votre application Spring Boot, et exécutez la commande suivante pour régénérer l’application et placer le conteneur dans votre registre de conteneurs Azure :

   ```cmd
   mvn compile jib:build
   ```

> [!NOTE]
>
> Quand vous utilisez Jib pour envoyer votre image à Azure Container Registry, l’image ne respecte pas *Dockerfile*. Pour plus d’informations, consultez [ce](https://cloudplatform.googleblog.com/2018/07/introducing-jib-build-java-docker-images-better.html) document.
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Créer une application web sur Linux sur Azure App Service en utilisant votre image de conteneur

1. Accédez au [portail Azure] et connectez-vous.

2. Cliquez sur l’icône de menu pour **+ Créer une ressource**, cliquez sur **Web**, puis sur **Web App pour conteneurs**.
   
   ![Créer une application web dans le portail Azure][LX01]

3. Quand la page **Application web sur Linux** s’affiche, entrez les informations suivantes :

   a. Entrez un nom unique pour le **Nom de l’application**, par exemple « *wingtiptoyslinux* ».

   b. Choisissez votre **abonnement** dans la liste déroulante.

   c. Choisissez un **Groupe de ressources** existant ou spécifiez un nom pour en créer un.

   d. Choisissez *Linux* comme **Système d’exploitation**.

   e. Cliquez sur **Plan App Service/Emplacement** et choisissez un plan App Service existant, ou cliquez sur **Créer** pour créer un nouveau plan App Service.

   f. Cliquez sur **Configurer le conteneur** et entrez les informations suivantes :

   * Choisissez **Conteneur unique** et **Azure Container Registry**.

   * **Registry** : choisissez le nom du conteneur que vous avez créé, par exemple « *wingtiptoysregistry* ».

   * **Image** : choisissez le nom de l’image, par exemple « *gs-spring-boot-docker* ».
   
   * **Balise** : choisissez l’étiquette de l’image, par exemple « *latest* ».
   
   * **Fichier de démarrage** : laissez vide, car l’image a déjà la commande de démarrage.
   
   e. Après avoir entré toutes les informations ci-dessus, cliquez sur **Appliquer**.

   ![Configurer les paramètres de l’application web][LX02]

4. Cliquez sur **Créer**.

> [!NOTE]
>
> Azure mappera automatiquement les demandes Internet au serveur Tomcat incorporé qui s’exécute sur les ports standard 80 ou 8080. Cependant, si vous avez configuré votre serveur Tomcat incorporé pour qu’il s’exécute sur un port personnalisé, vous devez ajouter une variable d’environnement à votre application web qui définit le port pour votre serveur Tomcat incorporé. Pour ce faire, procédez comme suit :
>
> 1. Accédez au [portail Azure] et connectez-vous.
> 
> 2. Cliquez sur l’icône pour **App Services**, puis sélectionnez votre application web dans la liste.
>
> 4. Cliquez sur **Configuration**. (Élément 1 de l’image ci-dessous.)
>
> 5. Dans la section **Paramètres de l’application**, ajoutez un nouveau paramètre nommé **PORT** et entrez comme valeur votre numéro de port personnalisé. (Éléments 2, 3 et 4 de l’image ci-dessous.)
>
> 6. Cliquez sur **Enregistrer**. (Élément 5 de l’image ci-dessous.)
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

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

Pour plus d’informations sur l’exemple de projet Spring Boot on Docker, consultez [Spring Boot on Docker Getting Started].

Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.

Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse https://start.spring.io/.

Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Azure pour les développeurs Java]: /java/azure/
[Portail Azure]: https://portal.azure.com/
[Créer un registre de conteneurs Docker privé à l’aide du portail Azure]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Utilisation d’Azure DevOps et Java]: /azure/devops/java/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

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
