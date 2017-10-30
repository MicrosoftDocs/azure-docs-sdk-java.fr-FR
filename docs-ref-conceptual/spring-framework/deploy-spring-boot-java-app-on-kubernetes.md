---
title: "Déployer une application Spring Boot sur Kubernetes dans Azure Container Service"
description: "Ce didacticiel vous guidera à travers les étapes à suivre pour déployer une application Spring Boot dans un cluster Kubernetes sur Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Kubernetes
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 44c20e9084d53fa366137fc191726aaa4be177f2
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a>Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service

Le **[Spring Framework]** est une infrastructure open source populaire qui aide les développeurs Java à créer des applications web, mobiles et API. Ce didacticiel utilise un exemple d’application créé à l’aide de [Spring Boot], une approche orientée par une convention permettant de prendre en main et d’utiliser Spring rapidement.

**[Kubernetes]** et **[client Docker]** sont des solutions open source qui aident les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications s’exécutant dans des conteneurs.

Ce didacticiel vous guidera à travers le processus de combinaison de ces deux technologies open source populaires afin de développer et de déployer une application Spring Boot sur Microsoft Azure. Plus précisément, vous utilisez *[Spring Boot]* pour le développement d’applications, *[Kubernetes]* pour le déploiement du conteneur, et [Azure Container Service (ACS)] pour l’hébergement votre application.

### <a name="prerequisites"></a>Composants requis

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

Les étapes suivantes vous guident à travers la création d’une application web Spring Boot et vous aident à effectuer le test en local.

1. Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Accédez au répertoire du projet terminé.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Utilisez Maven pour créer et exécuter l’exemple d’application.
   ```
   mvn package spring-boot:run
   ```

1. Testez l’application web en accédant à l’URL http://localhost:8080, ou avec la commande `curl` suivante :
   ```
   curl http://localhost:8080
   ```

1. Vous devez normalement voir le message suivant : **Hello Docker World**

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure

1. Ouvrez une invite de commandes.

1. Connectez-vous à votre compte Azure :
   ```azurecli
   az login
   ```

1. Créer un groupe de ressources pour les ressources Azure utilisées dans ce didacticiel.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Créez un registre de conteneurs Azure privé dans le groupe de ressources. Au cours des dernières étapes, le didacticiel envoie au registre l’exemple d’application en tant qu’image Docker. Remplacez `wingtiptoysregistry` par un nom unique pour votre registre.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a>Envoyer l’application dans le registre de conteneurs

1. Accédez au répertoire de configuration de l’installation de Maven (par défaut sous ~/.m2/ ou C:\Users\username\.m2) et ouvrez le fichier *settings.xml* avec un éditeur de texte.

1. Récupérez le mot de passe pour votre registre de conteneurs à partir de l’interface de ligne de commande Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Ajoutez votre identifiant de registre de conteneurs Azure et votre mot de passe à une nouvelle collection `<server>` dans le fichier *settings.xml*.
Le `id` et `username` correspondent au nom du registre. Utilisez la valeur `password` de la commande précédente (sans guillemets).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple, « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.

1. Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec la valeur du serveur de connexion de votre registre de conteneurs Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* de manière que `<plugin>` contienne l’adresse du serveur de connexion et le nom de registre de votre registre de conteneurs Azure.

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

1. Pour créer le conteneur Docker et envoyer l’image dans le registre, accédez au répertoire de projet terminé de votre application Spring Boot et exécutez la commande suivante :

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Lorsque Maven envoie l’image vers Azure, vous pouvez recevoir un message d’erreur semblable au message suivant :
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Si vous obtenez cette erreur, connectez-vous à Azure à partir de la ligne de commande Docker.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Envoyez ensuite votre conteneur :
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a>Créer un cluster Kubernetes sur ACS à l’aide de l’interface de ligne de commande Azure

1. Créez un cluster Kubernetes dans Azure Container Service. La commande suivante crée un cluster *kubernetes* dans le groupe de ressources *wingtiptoys-kubernetes*, avec *wingtiptoys-containerservice* comme nom du cluster et *wingtiptoys-kubernetes* comme préfixe du serveur DNS :
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Cette commande peut prendre un certain temps.

1. Installez `kubectl` à l’aide de l’interface de ligne de commande Azure. Les utilisateurs Linux doivent ajouter cette commande en préfixe sur `sudo` car elle déploie l’interface de ligne de commande Kubernetes dans `/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Téléchargez les informations de configuration du cluster afin de pouvoir gérer votre cluster à partir de l’interface web Kubernetes et de `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Déployer l’image sur votre cluster Kubernetes

Ce didacticiel déploie l’application à l’aide de `kubectl`, puis vous permet d’explorer le déploiement via l’interface web Kubernetes.

### <a name="deploy-with-the-kubernetes-web-interface"></a>Déployer avec l’interface web de Kubernetes

1. Ouvrez une invite de commandes.

1. Ouvrez le site web de configuration de votre cluster Kubernetes dans votre navigateur par défaut :
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Lorsque le site web de configuration Kubernetes s’ouvre dans votre navigateur, cliquez sur le lien afin de **déployer une application en conteneur** :

   ![Site web de configuration Kubernetes][KB01]

1. Lorsque la page **Déployer une application en conteneur** s’affiche, spécifiez les options suivantes :

   a. Sélectionnez **Spécifier les détails de l’application ci-dessous**.

   b. Entrez votre nom d’application Spring Boot comme **Nom de l’application**, par exemple : « *gs-spring-boot-docker* ».

   c. Entrez votre serveur de connexion et votre conteneur d’image vus précédemment dans la catégorie **Conteneur d’image**, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* ».

   d. Choisissez **Externe** pour le **Service**.

   e. Spécifiez les ports internes et externes dans les zones de texte **Port** et **Port cible**.

   ![Site web de configuration Kubernetes][KB02]


1. Cliquez sur **Déployer** pour déployer le conteneur.

   ![Déployer le conteneur][KB05]

1. Une fois que votre application a été déployée, vous verrez votre application Spring Boot répertoriée sous **Services**.

   ![Services Kubernetes][KB06]

1. Si vous cliquez sur le lien **Point de terminaison d’entrée**, vous pouvez voir votre application Spring Boot fonctionner sur Azure.

   ![Services Kubernetes][KB07]

   ![Parcourir l’exemple d’application sur Azure][SB02]


### <a name="deploy-with-kubectl"></a>Déployer avec kubectl

1. Ouvrez une invite de commandes.

1. Exécutez votre conteneur dans le cluster Kubernetes en utilisant la commande `kubectl run`. Donnez un nom de service à votre application dans Kubernetes et saisissez le nom complet de l’image. Par exemple :
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   Dans cette commande :

   * Le nom du conteneur `gs-spring-boot-docker` est spécifié directement après la commande `run`.

   * Le paramètre `--image` spécifie le nom combiné du nom de serveur et du nom de l’image en tant que `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Exposez votre cluster Kubernetes en externe à l’aide de la commande `kubectl expose`. Spécifiez le nom de votre service, le port TCP destiné au public permettant d’accéder à l’application, et le port cible interne que votre application écoutera. Par exemple :
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   Dans cette commande :

   * Le nom du conteneur `gs-spring-boot-docker` est spécifié directement après la commande `expose deployment`.

   * Le paramètre `--type` spécifie que le cluster utilise l’équilibreur de charge.

   * Le paramètre `--port` spécifie le port TCP 80 destiné au public. Vous accédez à l’application sur ce port.

   * Le paramètre `--target-port` spécifie le port TCP interne 8080. L’équilibreur de charge transmet les demandes à votre application sur ce port.

1. Une fois que l’application est déployée sur le cluster, faites la demande de l’adresse IP externe et ouvrez-la dans votre navigateur web :

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Parcourir l’exemple d’application sur Azure][SB02]


## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Déployer une application Spring Boot sur Linux dans Azure Container Service](deploy-spring-boot-java-app-on-linux.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur l’exemple de projet Spring Boot sur Docker, consultez [Spring Boot on Docker Getting Started].

Les liens suivants fournissent des informations supplémentaires sur la création d’applications Spring Boot :

* Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse https://start.spring.io/.

Les liens suivants fournissent des informations supplémentaires sur l’utilisation de Kubernetes avec Azure :

* [Prise en main d’un cluster Kubernetes dans Container Service](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Utilisation de l’interface utilisateur Web Kubernetes avec Azure Container Service](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Plus d’informations sur l’utilisation de l’interface de ligne de commande Kubernetes sont disponibles dans le guide de l’utilisateur **kubectl** à l’adresse <https://kubernetes.io/docs/user-guide/kubectl/>.

Le site web Kubernetes comporte plusieurs articles traitant de l’utilisation d’images dans les registres privés :

* [Configuration des comptes de service pour des pods]
* [Espaces de noms]
* [Extraction d’une image à partir d’un registre privé]

Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configuration des comptes de service pour des pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Espaces de noms]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Extraction d’une image à partir d’un registre privé]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/SB02.png

[AR01]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR01.png
[AR02]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR02.png
[AR03]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR03.png
[AR04]: ./media/deploy-spring-boot-java-app-on-kubernetes/AR04.png

[KB01]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB01.png
[KB02]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB02.png
[KB03]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB03.png
[KB04]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB04.png
[KB05]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB05.png
[KB06]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB06.png
[KB07]: ./media/deploy-spring-boot-java-app-on-kubernetes/KB07.png
