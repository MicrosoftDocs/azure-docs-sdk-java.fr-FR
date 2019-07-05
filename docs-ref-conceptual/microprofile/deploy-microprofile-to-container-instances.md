---
title: Déployer une application MicroProfile dans le cloud avec Docker et Azure
description: Découvrez comment déployer une application MicroProfile dans le cloud à l’aide de Docker et d’Azure Container Instances.
services: container-instances;container-registry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 11/21/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 6ba12bb183969103676fa988199603df6cf36bba
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533601"
---
# <a name="deploy-a-microprofile-app-to-the-cloud-by-using-docker-and-azure"></a>Déployer une application MicroProfile dans le cloud avec Docker et Azure

Cet article explique comment placer une application [MicroProfile.io] dans un conteneur Docker et l’exécuter sur Azure Container Instances.

> [!NOTE]
> Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image conteneur Docker est auto-exécutable (c’est-à-dire qu’elle inclut le runtime).

## <a name="prerequisites"></a>Prérequis

Pour effectuer ce didacticiel, vous avez besoin de ce qui suit :

* Un abonnement Azure. Si vous n’avez pas d’abonnement Azure, vous pouvez vous inscrire pour obtenir un [compte Azure gratuit].
* [Interface de ligne de commande Azure] installé.
* Un kit de développement Java (JDK) pris en charge. Pour plus d’informations sur les JDK qui peuvent être utilisés lorsque vous développez dans Azure, consultez [Prise en charge à long terme de Java pour Azure et Azure Stack](https://aka.ms/azure-jdks).
* L’outil de génération [Apache Maven] (version 3 ou ultérieure).
* Un client [Git].

## <a name="microprofile-hello-azure-sample"></a>Exemple MicroProfile Hello Azure

Pour cet article, vous allez utiliser l’exemple [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure). Clonez, générez, puis exécutez-le localement en utilisant les commandes suivantes :

```bash
$ git clone https://github.com/Azure-Samples/microprofile-hello-azure.git
$ mvn clean package
...
[INFO] BUILD SUCCESS
...
$ mvn payara-micro:start
...
[2018-07-30T13:34:51.553-0700] [] [INFO] [] [PayaraMicro] [tid: _ThreadID=1 _ThreadName=main] [timeMillis: 1532982891553] [levelValue: 800] Payara Micro  5.182 #badassmicrofish (build 303) ready in 10,304 (ms)
...
```

Vous pouvez tester l’application en appelant `curl` ou à l’aide d’un [navigateur](http://localhost:8080/api/hello) :

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-the-app-to-azure"></a>Déploiement de l’application dans Azure

Chargeons à présent cette application dans Azure avec les services [Azure Container Instances] et [Azure Container Registry].

### <a name="build-a-docker-image"></a>Générer une image Docker

L’exemple de projet met à votre disposition un fichier Dockerfile. Vous n’avez pas besoin d’installer le logiciel Docker, étant donné que nous utiliserons la fonctionnalité de génération d’Azure Container Registry pour générer l’image dans le cloud.

Pour créer l’image et préparer son exécution dans Azure, effectuez les étapes suivantes :

1. Installez Azure CLI, puis connectez-vous.
1. Création d’un groupe de ressources Azure.
1. Créez une instance de registre de conteneurs Azure.
1. Générez une image Docker.
1. Publiez l’image Docker dans l’instance de registre de conteneurs créée précédemment.
1. (Facultatif) Générez et publiez l’image dans l’instance de registre de conteneurs à l’aide d’une seule commande.


#### <a name="set-up-the-azure-cli"></a>Configuration de l’interface de ligne de commande Azure

Vérifiez que vous avez un abonnement Azure, que vous avez installé [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) et que vous êtes bien connecté à votre compte :

```bash
az login
```

#### <a name="create-a-resource-group"></a>Créer un groupe de ressources

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-a-container-registry-instance"></a>Créer une instance de registre de conteneurs

Cette commande doit créer un registre de conteneurs global et unique avec un nom de base et un numéro aléatoire.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Créer l’image Docker

Même si vous pouvez facilement générer une image Docker locale à l’aide du logiciel Docker, vous pouvez également choisir de la générer dans le cloud, et ce pour diverses raisons :

* Il n’est pas nécessaire d’installer Docker localement.
* Le temps d’exécution est beaucoup plus rapide grâce à la génération à distance (à l’exception du temps de chargement en contexte).
* Le traitement dans le cloud dispose d’une connexion Internet plus rapide, optimisant ainsi la vitesse des téléchargements.
* L’image est directement acheminée vers l’instance de registre de conteneurs.

Pour toutes ces raisons, vous allez générer l’image à l’aide de la fonctionnalité de génération d’[Générer ACR] :

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-the-docker-image-from-the-azure-container-registry-instance-to-container-instances"></a>Déployer l’image dans Container Instances à partir de l’instance de registre de conteneurs Azure

Maintenant que l’image est disponible dans votre instance de registre de conteneurs, poussez (push) puis instanciez une instance de conteneur dans Container Instances. Mais d’abord, vérifiez que vous pouvez vous authentifier auprès de l’instance de registre de conteneurs :

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Tester l’application MicroProfile déployée

Votre application devrait à présent être fonctionnelle. Pour la tester dans l’interface de ligne de commande, utilisez la commande suivante :

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Félicitations ! Vous avez généré une application MicroProfile comme conteneur Docker et l’avez déployée dans Azure.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez :

* [Se connecter à Azure à partir d’Azure CLI](/azure/xplat-cli-connect)

<!-- URL List -->

[Générer ACR]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Interface de ligne de commande Azure]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Apache Maven]: http://maven.apache.org/
[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry
