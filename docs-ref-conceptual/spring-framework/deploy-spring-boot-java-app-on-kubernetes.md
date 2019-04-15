---
title: Déployer une application Spring Boot sur Kubernetes dans Azure Kubernetes Service
description: Ce didacticiel vous guidera à travers les étapes à suivre pour déployer une application Spring Boot dans un cluster Kubernetes sur Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.custom: mvc
ms.openlocfilehash: 42bb030a916cc5aaf1e20242518a0a400b8baa88
ms.sourcegitcommit: 3b10fe30dcc83e4c2e4c94d5b55e37ddbaa23c7a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59071008"
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-kubernetes-service"></a>Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Kubernetes Service

**[Kubernetes]** et **[Docker]** sont des solutions open source qui aident les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications en cours d’exécution dans des conteneurs.

Ce didacticiel vous guide tout au long de la combinaison de ces deux technologies open source populaires pour développer et déployer une application Spring Boot sur Microsoft Azure. Plus précisément, *[Spring Boot]* sert au développement d’applications, *[Kubernetes]* au déploiement de conteneurs et [Azure Kubernetes Service (AKS)] à l’hébergement de votre application.

### <a name="prerequisites"></a>Prérequis

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

1. Testez l’application web en accédant à l’URL `http://localhost:8080`, ou avec la commande `curl` suivante :
   ```
   curl http://localhost:8080
   ```

1. Vous devriez voir le message suivant : **Hello Docker World**

   ![Parcourir l’exemple d’application en local][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a>Créer un registre de conteneurs Azure à l’aide de l’interface de ligne de commande Azure

1. Ouvrez une invite de commandes.

1. Connectez-vous à votre compte Azure :
   ```azurecli
   az login
   ```

1. Choisissez votre abonnement Azure :
   ```azurecli
   az account set -s <YourSubscriptionID>
   ```

1. Créer un groupe de ressources pour les ressources Azure utilisées dans ce didacticiel.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Créez un registre de conteneurs Azure privé dans le groupe de ressources. Au cours des dernières étapes, le didacticiel envoie au registre l’exemple d’application en tant qu’image Docker. Remplacez `wingtiptoysregistry` par un nom unique pour votre registre.
   ```azurecli
   az acr create --resource-group wingtiptoys-kubernetes --location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry-via-jib"></a>Envoyer l’application dans le registre de conteneurs via Jib

1. Connectez-vous à votre instance Azure Container Registry depuis l’interface Azure CLI.
   ```azurecli
   # set the default name for Azure Container Registry, otherwise you will need to specify the name in "az acr login"
   az configure --defaults acr=wingtiptoysregistry
   az acr login
   ```

1. Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple, « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou «  */users/robert/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.

1. Mettez à jour la collection `<properties>` dans le fichier *pom.xml* avec le nom du registre de votre instance Azure Container Registry et la dernière version de [jib-maven-plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <jib-maven-plugin.version>1.0.2</jib-maven-plugin.version>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* pour que `<plugin>` contienne `jib-maven-plugin`.

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
        </to>
     </configuration>
   </plugin>
   ```

1. Pour créer l’image Docker et la pousser dans le registre, accédez au répertoire de projet terminé de votre application Spring Boot et exécutez la commande suivante :

   ```
   mvn compile jib:build
   ```

## <a name="create-a-kubernetes-cluster-on-aks-using-the-azure-cli"></a>Créer un cluster Kubernetes sur AKS à l’aide d’Azure CLI

1. Créez un cluster Kubernetes dans Azure Kubernetes Service. La commande suivante crée un cluster *kubernetes* dans le groupe de ressources *wingtiptoys-kubernetes* avec *wingtiptoys-akscluster* comme nom de cluster, et *wingtiptoys-kubernetes* comme préfixe DNS :
   ```azurecli
   az aks create --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster \ 
    --dns-name-prefix=wingtiptoys-kubernetes --generate-ssh-keys
   ```
   Cette commande peut prendre un certain temps.

1. Lorsque vous utilisez Azure Container Registry (ACR) avec Azure Kubernetes Service (AKS), vous devez accorder l’accès de tirage d’Azure Kubernetes Service à Azure Container Registry. Azure crée un principal de service par défaut quand vous créez Azure Kubernetes Service. Exécutez les scripts suivants dans bash ou Powershell pour accorder un accès à AKS à ACR et découvrez plus de détails dans [S’authentifier avec Azure Container Registry à partir d’Azure Kubernetes Service].

```bash
   # Get the id of the service principal configured for AKS
   CLIENT_ID=$(az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv)
   
   # Get the ACR registry resource id
   ACR_ID=$(az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv)
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

  - ou -

```PowerShell
   # Get the id of the service principal configured for AKS
   $CLIENT_ID = az aks show -g wingtiptoys-kubernetes -n wingtiptoys-akscluster --query "servicePrincipalProfile.clientId" --output tsv
   
   # Get the ACR registry resource id
   $ACR_ID = az acr show -g wingtiptoys-kubernetes -n wingtiptoysregistry --query "id" --output tsv
   
   # Create role assignment
   az role assignment create --assignee $CLIENT_ID --role acrpull --scope $ACR_ID
```

1. Installez `kubectl` à l’aide de l’interface de ligne de commande Azure. Les utilisateurs Linux doivent ajouter cette commande en préfixe sur `sudo` car elle déploie l’interface de ligne de commande Kubernetes dans `/usr/local/bin`.
   ```azurecli
   az aks install-cli
   ```

1. Téléchargez les informations de configuration du cluster afin de pouvoir gérer votre cluster à partir de l’interface web Kubernetes et de `kubectl`. 
   ```azurecli
   az aks get-credentials --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a>Déployer l’image sur votre cluster Kubernetes

Ce didacticiel déploie l’application à l’aide de `kubectl`, puis vous permet d’explorer le déploiement via l’interface web Kubernetes.

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
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=default
   ```

   ![Parcourir l’exemple d’application sur Azure][SB02]



### <a name="deploy-with-the-kubernetes-web-interface"></a>Déployer avec l’interface web de Kubernetes

1. Ouvrez une invite de commandes.

1. Ouvrez le site web de configuration de votre cluster Kubernetes dans votre navigateur par défaut :
   ```
   az aks browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-akscluster
   ```

1. Lorsque le site web de configuration Kubernetes s’ouvre dans votre navigateur, cliquez sur le lien afin de **déployer une application en conteneur** :

   ![Site web de configuration Kubernetes][KB01]

1. Lorsque la page **Création de ressources** s’affiche, spécifiez les options suivantes :

   a. Sélectionnez **CRÉER UNE APPLICATION**.

   b. Entrez votre nom d’application Spring Boot comme **Nom de l’application**, par exemple : « *gs-spring-boot-docker* ».

   c. Entrez votre serveur de connexion et votre conteneur d’image vus précédemment dans la catégorie **Conteneur d’image**, par exemple : « *wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest* ».

   d. Choisissez **Externe** pour le **Service**.

   e. Spécifiez les ports internes et externes dans les zones de texte **Port** et **Port cible**.

   ![Site web de configuration Kubernetes][KB02]


1. Cliquez sur **Déployer** pour déployer le conteneur.

   ![Déploiement de Kubernetes][KB05]

1. Une fois que votre application a été déployée, vous verrez votre application Spring Boot répertoriée sous **Services**.

   ![Services Kubernetes][KB06]

1. Si vous cliquez sur le lien **Point de terminaison d’entrée**, vous pouvez voir votre application Spring Boot fonctionner sur Azure.

   ![Services Kubernetes][KB07]

   ![Parcourir l’exemple d’application sur Azure][SB02]

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez l’article suivant :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

Pour plus d’informations sur le déploiement d’une application Java sur Kubernetes avec Visual Studio Code, consultez les [didacticiels de Visual Studio Code Java].

Pour plus d’informations sur l’exemple de projet Spring Boot sur Docker, consultez [Spring Boot on Docker Getting Started].

Les liens suivants fournissent des informations supplémentaires sur la création d’applications Spring Boot :

* Pour plus d’informations sur la création d’une application Spring Boot simple, consultez Spring Initializr à l’adresse https://start.spring.io/.

Les liens suivants fournissent des informations supplémentaires sur l’utilisation de Kubernetes avec Azure :

* [Démarrer avec un cluster Kubernetes dans Azure Kubernetes Service](/azure/aks/intro-kubernetes)

Plus d’informations sur l’utilisation d’interface de ligne de commande Kubernetes sont disponibles dans le guide d’utilisateur **kubectl** à l’adresse <https://kubernetes.io/docs/user-guide/kubectl/>.

Le site web Kubernetes comporte plusieurs articles traitant de l’utilisation d’images dans les registres privés :

* [Configuration des comptes de service pour des pods]
* [Espaces de noms]
* [Extraction d’une image à partir d’un registre privé]

Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].

Pour plus d’informations sur l’exécution et le débogage itératifs des conteneurs directement dans Azure Kubernetes Service (AKS) avec Azure Dev Spaces, consultez [Bien démarrer avec l’utilisation d’Azure Dev Spaces conjointement à Java]

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Kubernetes Service (AKS)]: https://azure.microsoft.com/services/kubernetes-service/
[Azure pour les développeurs Java]: /java/azure/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Utilisation d’Azure DevOps et Java]: /azure/devops/java/
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

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- Newly added -->
[S’authentifier avec Azure Container Registry à partir d’Azure Kubernetes Service]: /azure/container-registry/container-registry-auth-aks/
[Didacticiels de Visual Studio Code Java]: https://code.visualstudio.com/docs/java/java-kubernetes/
[Bien démarrer avec l’utilisation d’Azure Dev Spaces conjointement à Java]: https://docs.microsoft.com/en-us/azure/dev-spaces/get-started-java
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
