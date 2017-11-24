---
title: "Déployer une application Spring Boot à l’aide du plug-in Fabric8 Maven"
description: "Ce didacticiel vous guide à travers les étapes pour déployer une application Spring Boot sur Microsoft Azure à l’aide du plug-in Fabric8 pour Apache Maven."
services: container-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 11/01/2017
ms.author: yuwzho;robmcm
ms.custom: 
ms.openlocfilehash: 6c0e0e233b44b2b54e869b443edf3a255e7fbfb4
ms.sourcegitcommit: 613c1ffd2e0279fc7a96fca98aa1809563f52ee1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2017
---
# <a name="deploy-a-spring-boot-app-using-the-fabric8-maven-plugin"></a>Déployer une application Spring Boot à l’aide du plug-in Fabric8 Maven

**[Fabric8]** est une solution open source qui repose sur **[Kubernetes]** et qui aide les développeurs à créer des applications dans les conteneurs Linux.

Ce didacticiel vous guide dans l’utilisation du plug-in Fabric8 pour Maven pour développer et déployer une application sur un hôte Linux dans [Azure Container Service (AKS)].

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

Les étapes suivantes vous guident à travers la création d’une application web Spring Boot et vous aident à effectuer le test en local.

1. Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :
   ```shell
   md /home/GenaSoto/SpringBoot
   cd /home/GenaSoto/SpringBoot
   ```
   - ou -
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```

1. Clonez l’exemple de projet [Spring Boot on Docker Getting Started] dans le répertoire.
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Accédez au répertoire du projet terminé. Par exemple :
   ```shell
   cd gs-spring-boot-docker/complete
   ```
   - ou -
   ```shell
   cd gs-spring-boot-docker\complete
   ```

1. Utilisez Maven pour créer et exécuter l’exemple d’application.
   ```shell
   mvn clean package spring-boot:run
   ```

1. Testez l’application web en accédant à l’URL http://localhost:8080, ou avec la commande `curl` suivante :
   ```shell
   curl http://localhost:8080
   ```

   Vous devez normalement voir le message **Hello Docker World** s’afficher.

   ![Parcourir l’exemple d’application localement][SB01]


## <a name="install-the-kubernetes-command-line-interface-and-create-an-azure-resource-group-using-the-azure-cli"></a>Installer l’interface de ligne de commande Kubernetes et créer un groupe de ressources Azure à l’aide de l’interface Azure CLI

1. Ouvrez une invite de commandes.

1. Tapez la commande suivante pour vous connecter à votre compte Azure :
   ```azurecli
   az login
   ```
   Suivez les instructions pour terminer le processus de connexion
   
   L’interface Azure CLI affiche une liste de vos comptes ; par exemple :

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "00000000-0000-0000-0000-000000000000",
       "isDefault": false,
       "name": "Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "00000000-0000-0000-0000-000000000000",
       "user": {
         "name": "Gena.Soto@wingtiptoys.com",
         "type": "user"
       }
     }
   ]
   ```

1. Si vous n’avez pas encore installé l’interface de ligne de commande Kubernetes (`kubectl`), vous pouvez l’installer à l’aide de l’interface Azure CLI ; par exemple :
   ```azurecli
   az acs kubernetes install-cli
   ```

   > [!NOTE]
   >
   > Les utilisateurs Linux doivent ajouter cette commande en préfixe sur `sudo` car elle déploie l’interface de ligne de commande Kubernetes dans `/usr/local/bin`.
   >
   > Si `kubectl` est déjà installé et que votre version de `kubectl` est trop ancienne, un message d’erreur semblable à l’exemple suivant peut s’afficher lorsque vous tentez d’effectuer les étapes indiquées plus loin dans cet article :
   >
   > ```
   > error: group map[autoscaling:0x0000000000 batch:0x0000000000 certificates.k8s.io
   > :0x0000000000 extensions:0x0000000000 storage.k8s.io:0x0000000000 apps:0x0000000
   > 000 authentication.k8s.io:0x0000000000 policy:0x0000000000 rbac.authorization.k8
   > s.io:0x0000000000 federation:0x0000000000 authorization.k8s.io:0x0000000000 comp
   > onentconfig:0x0000000000] is already registered
   > ```
   >
   > Dans ce cas, vous devrez réinstaller `kubectl` pour mettre à jour votre version.
   >

1. Créez un groupe de ressources pour les ressources Azure que vous utiliserez dans ce didacticiel ; par exemple :
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=westeurope
   ```
   Où :  
      * *wingtiptoys-kubernetes* est un nom unique pour votre groupe de ressources  
      * *westeurope* est un emplacement géographique approprié pour votre application  

   L’interface Azure CLI affiche les résultats de la création de votre groupe de ressources ; par exemple :  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes",
     "location": "westeurope",
     "managedBy": null,
     "name": "wingtiptoys-kubernetes",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```


## <a name="create-a-kubernetes-cluster-using-the-azure-cli"></a>Créer un cluster Kubernetes à l’aide de l’interface Azure CLI

1. Créez un cluster Kubernetes dans votre nouveau groupe de ressources ; par exemple :  
   ```azurecli 
   az acs create --orchestrator-type kubernetes --resource-group wingtiptoys-kubernetes --name wingtiptoys-cluster --generate-ssh-keys --dns-prefix=wingtiptoys
   ```
   Où :  
      * *wingtiptoys-kubernetes* est le nom de votre groupe de ressources tel que spécifié plus haut dans cet article  
      * *wingtiptoys-kubernetes* est un nom unique pour votre cluster Kubernetes
      * *wingtiptoys* est un nom DNS unique pour votre application

   L’interface Azure CLI affiche les résultats de la création de votre cluster ; par exemple :  

   ```json
   {
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.Resources/deployments/azurecli0000000000.00000000000",
     "name": "azurecli0000000000.00000000000",
     "properties": {
       "correlationId": "00000000-0000-0000-0000-000000000000",
       "debugSetting": null,
       "dependencies": [],
       "mode": "Incremental",
       "outputs": {
         "masterFQDN": {
           "type": "String",
           "value": "wingtiptoysmgmt.westeurope.cloudapp.azure.com"
         },
         "sshMaster0": {
           "type": "String",
           "value": "ssh azureuser@wingtiptoysmgmt.westeurope.cloudapp.azure.com -A -p 22"
         }
       },
       "parameters": {
         "clientSecret": {
           "type": "SecureString"
         }
       },
       "parametersLink": null,
       "providers": [
         {
           "id": null,
           "namespace": "Microsoft.ContainerService",
           "registrationState": null,
           "resourceTypes": [
             {
               "aliases": null,
               "apiVersions": null,
               "locations": [
                 "westeurope"
               ],
               "properties": null,
               "resourceType": "containerServices"
             }
           ]
         }
       ],
       "provisioningState": "Succeeded",
       "template": null,
       "templateLink": null,
       "timestamp": "2017-09-15T01:00:00.000000+00:00"
     },
     "resourceGroup": "wingtiptoys-kubernetes"
   }
   ```

1. Téléchargez vos informations d’identification pour votre nouveau cluster Kubernetes ; par exemple :  
   ```azurecli 
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes --name wingtiptoys-cluster
   ```

1. Vérifiez votre connexion avec la commande suivante :
   ```shell 
   kubectl get nodes
   ```

   Vous devez voir une liste de nœuds et d’états semblable à l’exemple suivant :

   ```shell
   NAME                    STATUS                     AGE       VERSION
   k8s-agent-00000000-0    Ready                      5h        v1.6.6
   k8s-agent-00000000-1    Ready                      5h        v1.6.6
   k8s-agent-00000000-2    Ready                      5h        v1.6.6
   k8s-master-00000000-0   Ready,SchedulingDisabled   5h        v1.6.6
   ```


## <a name="create-a-private-azure-container-registry-using-the-azure-cli"></a>Créer un registre de conteneurs Azure (Azure Container Registry) privé à l’aide de l’interface Azure CLI

1. Créez un registre de conteneurs Azure privé dans votre groupe de ressources pour héberger votre image Docker ; par exemple :
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes --location westeurope --name wingtiptoysregistry --sku Basic
   ```
   Où :  
      * *wingtiptoys-kubernetes* est le nom de votre groupe de ressources tel que spécifié plus haut dans cet article  
      * *wingtiptoysregistry* est un nom unique pour votre registre privé
      * *westeurope* est un emplacement géographique approprié pour votre application  

   L’interface Azure CLI affiche les résultats de la création de votre registre ; par exemple :  

   ```json
   {
     "adminUserEnabled": true,
     "creationDate": "2017-09-15T01:00:00.000000+00:00",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/wingtiptoys-kubernetes/providers/Microsoft.ContainerRegistry/registries/wingtiptoysregistry",
     "location": "westeurope",
     "loginServer": "wingtiptoysregistry.azurecr.io",
     "name": "wingtiptoysregistry",
     "provisioningState": "Succeeded",
     "resourceGroup": "wingtiptoys-kubernetes",
     "sku": {
       "name": "Basic",
       "tier": "Basic"
     },
     "storageAccount": {
       "name": "wingtiptoysregistr000000"
     },
     "tags": {},
     "type": "Microsoft.ContainerRegistry/registries"
   }
   ```

1. Récupérez le mot de passe pour votre registre de conteneurs à partir de l’interface de ligne de commande Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   L’interface Azure CLI affiche le mot de passe de votre registre ; par exemple :  

   ```json
   {
     "name": "password",
     "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Accédez au répertoire de configuration de l’installation de Maven (par défaut sous ~/.m2/ ou C:\Users\username\.m2) et ouvrez le fichier *settings.xml* avec un éditeur de texte.

1. Ajoutez l’URL, votre nom d’utilisateur et votre mot de passe de votre Azure Container Registry à une nouvelle collection `<server>` dans le fichier *settings.xml*.
Le `id` et `username` correspondent au nom du registre. Utilisez la valeur `password` de la commande précédente (sans guillemets).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry.azurecr.io</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.

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
     <artifactId>dockerfile-maven-plugin</artifactId>
     <version>1.3.4</version>
     <configuration>
       <repository>${docker.image.prefix}/${project.artifactId}</repository>
       <serverId>${docker.image.prefix}</serverId>
       <registryUrl>https://${docker.image.prefix}</registryUrl>
     </configuration>
   </plugin>
   ```

1. Pour créer le conteneur Docker et envoyer l’image dans votre registre, accédez au répertoire de projet terminé de votre application Spring Boot et exécutez la commande Maven suivante :

   ```shell
   mvn package dockerfile:build -DpushImage
   ```

   Maven affiche les résultats de la génération ; par exemple :  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 38.113 s
   [INFO] Finished at: 2017-09-15T02:00:00-07:00
   [INFO] Final Memory: 47M/338M
   [INFO] ----------------------------------------------------
   ```


## <a name="configure-your-spring-boot-app-to-use-the-fabric8-maven-plugin"></a>Configurer votre application Spring Boot pour utiliser le plug-in Fabric8 Maven

1. Accédez au répertoire de projet terminé de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete* » ou « */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete* ») et ouvrez le fichier *pom.xml* avec un éditeur de texte.

1. Mettez à jour la collection `<plugins>` dans le fichier *pom.xml* pour ajouter le plug-in Fabric8 Maven :

   ```xml
   <plugin>
     <groupId>io.fabric8</groupId>
     <artifactId>fabric8-maven-plugin</artifactId>
     <version>3.5.30</version>
     <configuration>
       <ignoreServices>false</ignoreServices>
       <registry>${docker.image.prefix}</registry>
     </configuration>
   </plugin>
   ```

1. Accédez au répertoire source principal de votre application Spring Boot (par exemple : « *C:\SpringBoot\gs-spring-boot-docker\complete\src\main* » ou « */home/GenaSoto/SpringBoot/gs-spring-boot-docker/complete/src/main* ») et créez un dossier nommé « *fabric8* ».

1. Créez trois fichiers fragmentés YAML dans le nouveau dossier *fabric8* :

   a. Créez un fichier intitulé **deployment.yml** avec le contenu suivant :
      ```yaml
      apiVersion: extensions/v1beta1
      kind: Deployment
      metadata:
        name: ${project.artifactId}
        labels:
          run: gs-spring-boot-docker
      spec:
        replicas: 1
        selector:
          matchLabels:
            run: gs-spring-boot-docker
        strategy:
          rollingUpdate:
            maxSurge: 1
            maxUnavailable: 1
          type: RollingUpdate
        template:
          metadata:
            labels:
              run: gs-spring-boot-docker
          spec:
            containers:
            - image: ${docker.image.prefix}/${project.artifactId}:latest
              name: gs-spring-boot-docker
              imagePullPolicy: Always
              ports:
              - containerPort: 8080
            imagePullSecrets:
              - name: mysecrets
      ```

   b. Créez un fichier intitulé **secrets.yml** avec le contenu suivant :
      ```yaml
      apiVersion: v1
      kind: Secret
      metadata:
        name: mysecrets
        namespace: default
        annotations:
          maven.fabric8.io/dockerServerId:  ${docker.image.prefix}
      type: kubernetes.io/dockercfg
      ```

   c. Créez un fichier intitulé **service.yml** avec le contenu suivant :
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        name: ${project.artifactId}
        labels:
          expose: "true"
      spec:
        ports:
        - port: 80
          targetPort: 8080
        type: LoadBalancer
      ```

1. Exécutez la commande Maven suivante pour générer le fichier de liste des ressources Kubernetes :

   ```shell
   mvn fabric8:resource
   ```

   Cette commande fusionne tous les fichiers yaml des ressources Kubernetes du dossier *src/main/fabric8* dans un fichier YAML qui contient une liste des ressources Kubernetes, qui peut être appliquée directement au cluster Kubernetes ou exportée dans un graphique Helm.

   Maven affiche les résultats de la génération ; par exemple :  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 16.744 s
   [INFO] Finished at: 2017-09-15T02:35:00-07:00
   [INFO] Final Memory: 30M/290M
   [INFO] ----------------------------------------------------
   ```

1. Exécutez la commande Maven suivante pour appliquer le fichier de liste des ressources à votre cluster Kubernetes :

   ```shell
   mvn fabric8:apply
   ```

   Maven affiche les résultats de la génération ; par exemple :  

   ```shell
   [INFO] ----------------------------------------------------
   [INFO] BUILD SUCCESS
   [INFO] ----------------------------------------------------
   [INFO] Total time: 14.814 s
   [INFO] Finished at: 2017-09-15T02:41:00-07:00
   [INFO] Final Memory: 35M/288M
   [INFO] ----------------------------------------------------
   ```

1. Une fois que l’application est déployée sur le cluster, interrogez l’adresse IP externe à l’aide de l’application `kubectl` ; par exemple :
   ```shell
   kubectl get svc -w
   ```

   `kubectl` affiche vos adresses IP internes et externes ; par exemple :
   
   ```shell
   NAME                    CLUSTER-IP   EXTERNAL-IP   PORT(S)        AGE
   kubernetes              10.0.0.1     <none>        443/TCP        19h
   gs-spring-boot-docker   10.0.242.8   13.65.196.3   80:31215/TCP   3m
   ```
   
   Vous pouvez utiliser l’adresse IP externe pour ouvrir votre application dans un navigateur web.

   ![Parcourir l’exemple d’application en externe][SB02]

## <a name="delete-your-kubernetes-cluster"></a>Supprimer votre cluster Kubernetes

Lorsque vous n’avez plus besoin de votre cluster Kubernetes, vous pouvez utiliser la commande `az group delete` pour supprimer le groupe de ressources, ce qui supprime toutes ses ressources associées ; par exemple :

   ```azurecli
   az group delete --name wingtiptoys-kubernetes --yes --no-wait
   ```

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)
* [Déployer une application Spring Boot sur Linux dans Azure Container Service](deploy-spring-boot-java-app-on-linux.md)
* [Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur l’exemple de projet Spring Boot on Docker, consultez [Spring Boot on Docker Getting Started].

Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse <https://start.spring.io/>.

Pour plus d’informations sur la création d’une application Spring Boot simple, consultez « Spring Initializr » à l’adresse <https://start.spring.io/>.

Pour obtenir des exemples supplémentaires sur l’utilisation d’images Docker personnalisées avec Azure, consultez [Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux].

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Container Service (AKS)]: https://azure.microsoft.com/services/container-service/
[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Comment utiliser une image Docker personnalisée pour Azure Web App sur Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[client Docker]: https://www.docker.com/
[Fabric8]: https://fabric8.io/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB01.png
[SB02]: ./media/deploy-spring-boot-java-app-using-fabric8-maven-plugin/SB02.png
