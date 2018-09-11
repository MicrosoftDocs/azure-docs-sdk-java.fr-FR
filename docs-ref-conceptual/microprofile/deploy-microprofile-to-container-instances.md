---
title: Déployer une application MicroProfile sur le cloud avec Docker et Azure
description: Découvrez comment déployer une application MicroProfile sur le cloud à l’aide de Docker et d’Azure Container Instances.
services: container-instances;container-retistry
documentationcenter: java
author: brunoborges
manager: routlaw
editor: brunoborges
ms.assetid: ''
ms.author: brborges
ms.date: 07/30/2018
ms.devlang: java
ms.service: container-instances
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 336af51bbdf5d2f843c3868ebc2358e128daaeaa
ms.sourcegitcommit: 280d13b43cef94177d95e03879a5919da234a23c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43324325"
---
# <a name="deploy-a-microprofile-application-to-the-cloud-with-docker-and-azure"></a>Déployer une application MicroProfile sur le cloud avec Docker et Azure

Cet article explique comment placer une application [MicroProfile.io] dans un conteneur Docker et l’exécuter sur Azure Container Instances.

> [!NOTE]
>
> Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image du conteneur Docker s’exécute automatiquement (c’est-à-dire qu’elle inclue le runtime).

## <a name="prerequisites"></a>Prérequis

Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :

* Abonnement Azure ; si vous ne disposez pas d’un abonnement Azure, vous pouvez vous inscrire pour un [compte Azure gratuit].
* [Azure CLI].
* Un [Kit de développement Java (JDK)] à jour, d’une version 1.8 ou ultérieure.
* L’outil de génération [Maven] (version 3+) d’Apache.
* Un client [Git].

## <a name="microprofile-hello-azure-sample"></a>Exemple MicroProfile Hello Azure

Pour cet article, nous utiliserons l’exemple de [MicroProfile Hello Azure](https://github.com/azure-samples/microprofile-hello-azure) :

### <a name="clone-build-and-run-locally"></a>Cloner, générer, et exécuter en local

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

Vous pouvez tester l’application avec un appel `curl` ou en la consultant dans un [navigateur](http://localhost:8080/api/hello) :

```bash
$ curl http://localhost:8080/api/hello
Hello, Azure!
```

## <a name="deploy-to-azure"></a>Déployer dans Azure

Chargeons à présent cette application sur le cloud avec les services [Azure Container Instances] et [Azure Container Registry].

### <a name="build-a-docker-image"></a>Générer une image Docker

L’exemple de projet met à votre disposition un fichier Dockerfile. Vous n’avez pas besoin d’installer le logiciel Docker, étant donné que nous utiliserons la fonctionnalité de génération d’Azure Container Registry pour générer l’image dans le cloud.

Pour générer l’image et la rendre exécutable sur Azure, procédez comme suit :

1. Installer et se connecter avec Azure CLI
1. Créer un groupe de ressources Azure
1. Créer un ACR (Azure Container Registry)
1. Créer l’image Docker
1. Publier l’image de Docker sur l’ACR précédemment créé
1. (Facultatif) Générer et publier sur ACR en une seule commande


#### <a name="set-up-azure-cli"></a>Configuration de l’interface de ligne de commande Azure CLI

Vérifiez que vous disposez d’un abonnement Azure, que l’interface [Azure CLI est bien installée](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest), et que vous êtes bien authentifié sur votre compte :

```bash
az login
```

#### <a name="create-a-resource-group"></a>Création d’un groupe de ressources

```bash
export ARG=microprofileRG
export ADCL=eastus
az group create --name $ARG --location $ADCL
```

#### <a name="create-an-azure-container-registry-instance"></a>Créer une instance Azure Container Registry

Cette commande devrait créer un registre de conteneurs global et unique utilisant un nom de base accompagné d’un nombre aléatoire.

```bash
export RANDINT=`date +"%m%d%y$RANDOM"`
export ACR=mydockerrepo$RANDINT
az acr create --name $ACR -g $ARG --sku Basic --admin-enabled
```

#### <a name="build-the-docker-image"></a>Créer l’image Docker

Même si vous pouvez facilement générer une image Docker locale à l’aide du logiciel Docker lui-même, vous pouvez également la générer dans le cloud, et ce pour diverses raisons :

1. Vous n’avez pas besoin d’installer Docker en local
1. Le temps d’exécution est beaucoup plus rapide grâce à la génération à distance (à l’exception du temps de chargement en contexte)
1. Le traitement dans le cloud dispose d’une connexion internet plus rapide, optimisant ainsi la vitesse des téléchargements
1. L’image est directement acheminée dans Container Registry

Pour toutes ces raisons, nous générerons l’image à l’aide de la fonctionnalité de génération d’[Générer ACR] :

```bash
export IMG_NAME="mympapp:latest"
az acr build -r $ACR -t $IMG_NAME -g $ARG .
...
Build complete
Build ID: aa1 was successful after 1m2.674577892s
```

#### <a name="deploy-docker-image-from-azure-container-registry-acr-into-container-instances-aci"></a>Déployer une image Docker depuis Azure Container Registry (ACR) vers Azure Container Instances (ACI)

Maintenant que l’image est disponible sur votre ACR, essayons d’envoyer et d’instancier une instance de conteneur sur ACI. Mais avant toute chose, il faut nous assurer que nous pouvons nous authentifier dans l’ACR :

```bash
export ACR_REPO=`az acr show --name $ACR -g $ARG --query loginServer -o tsv`
export ACR_PASS=`az acr credential show --name $ACR -g $ARG --query "passwords[0].value" -o tsv`
export ACI_INSTANCE=myapp`date +"%m%d%y$RANDOM"`

az container create --resource-group $ARG --name $ACR --image $ACR_REPO/$IMG_NAME --cpu 1 --memory 1 --registry-login-server $ACR_REPO --registry-username $ACR --registry-password $ACR_PASS --dns-name-label $ACI_INSTANCE --ports 8080
```

#### <a name="test-your-deployed-microprofile-application"></a>Testez votre application MicroProfile déployée

Votre application devrait à présent être fonctionnelle. Pour la tester depuis l’interface de ligne de commande, essayez la commande suivante :

```bash
curl http://$ACI_INSTANCE.$ADCL.azurecontainer.io:8080/api/hello
````

Félicitations ! Vous avez généré et déployé avec succès une application MicroProfile comme conteneur Docker sur Microsoft Azure.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :

* [Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure](/azure/xplat-cli-connect)

<!-- URL List -->

[Générer ACR]: https://docs.microsoft.com/azure/container-registry/container-registry-build-overview
[MicroProfile.io]: https://microprofile.io
[Azure CLI]: /cli/azure/overview
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Azure portal]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Maven]: http://maven.apache.org/
[Kit de développement Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
[Azure Container Instances]: https://docs.microsoft.com/azure/container-instances/
[Azure Container Registry]:  https://docs.microsoft.com/azure/container-registry