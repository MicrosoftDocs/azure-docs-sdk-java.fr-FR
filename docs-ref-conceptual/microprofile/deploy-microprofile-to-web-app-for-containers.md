---
title: Déployez un service MicroProfile en Java vers Azure Web App pour conteneurs
description: Découvrez comment déployer un service MicroProfile en utilisant Docker et Azure Web App pour conteneurs
services: container-registry;app-service
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: container-registry;app-service
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: 4ecfbf92bc30bc491c991e30111cce8375da7f1a
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533599"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Déployez un service MicroProfile en Java vers Azure Web App pour conteneurs

MicroProfile est un bon outil de génération pour les applications Java extrêmement petites, qui peuvent être déployées rapidement et facilement sur des services tels qu’[Azure Web App pour conteneurs](https://azure.microsoft.com/services/app-service/containers/). Dans ce tutoriel, vous allez créer un microservice simple basé sur MicroProfile que vous allez intégrer à un conteneur Docker, déployer sur une [instance de registre de conteurs Azure](https://azure.microsoft.com/services/container-registry/), et finalement héberger à l’aide d’Azure Web App pour conteneurs.

> [!NOTE]
> Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image conteneur Docker est auto-exécutable (c’est-à-dire qu’elle inclut le runtime).

Dans cet exemple, vous allez utiliser [Payara Micro](https://www.payara.fish/payara_micro) et [MicroProfile 1.3](https://microprofile.io/) pour créer un petit fichier WAR Java (d’environ 5 000 octets), puis pour l’empaqueter dans une image Docker d’environ 174 Mo. L’image Docker contient tout le nécessaire pour un déploiement entièrement conteneurisé de l’application web.

Il n’est pas nécessaire de redéployer l’intégralité d’une image Docker de 174 Mo à chaque changement du code source de l’application, car Docker charge uniquement les modifications (dont la taille est beaucoup plus petite). Par conséquent, ce mode de fonctionnement permet de créer très rapidement et très efficacement de nouvelles versions d’une application MicroProfile via un pipeline CI/CD, ce qui réduit le nombre de conflits et garantit des itérations de développement rapides.

Dans ce tutoriel, vous allez d’abord créer et exécuter du code localement, puis vous allez le déployer en tant qu’application web dans Azure. Durant ces deux phases, vous pouvez compter sur Docker pour simplifier et standardiser vos tâches. Avant de commencer, vous allez créer une instance de registre de conteneurs Azure pour stocker vos conteneurs Docker.

## <a name="create-an-azure-container-registry-instance"></a>Créer une instance de registre de conteneurs Azure

Pour créer l’instance de registre de conteneurs Azure, vous pouvez utiliser le [portail Azure](http://portal.azure.com), mais vous avez aussi d’autres options comme Azure CLI. Pour créer une instance de registre de conteneurs Azure, effectuez les étapes suivantes :

1. Connectez-vous au [portail Azure](http://portal.azure.com), puis créez une ressource de registre de conteneurs Azure. Entrez un nom de registre (ce nom doit correspondre à la propriété `docker.registry` du fichier *pom.xml*). Changez les paramètres par défaut selon vos besoins, puis sélectionnez **Créer**.

1. Au bout d’environ 30 secondes, lorsque l’instance de registre de conteneurs est en ligne, sélectionnez-la, puis, dans le volet gauche, sélectionnez le lien **Clés d’accès**. 

    Activez le paramètre *Utilisateur administrateur* afin de pouvoir accéder à l’instance de registre de conteneurs à partir de vos ordinateurs et pousser (push) les conteneurs Docker vers celle-ci. Vous pouvez également y accéder à partir de l’instance Azure Web App pour conteneurs que vous allez bientôt configurer.

1. Dans le volet **Clés d’accès**, copiez les valeurs de **nom d’utilisateur** et de **mot de passe**, puis collez-les dans le fichier global *settings.xml* Maven. Pour plus d’informations sur les paramètres Maven, consultez le site web [Apache Maven Project](https://maven.apache.org/settings.html). 

   Pour référence, voici un exemple tiré du fichier *${user.home}/.m2/settings.xml* :

    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
        <servers>
          <server>
            <id>jogilescr.azurecr.io</id>
            <username>jogilescr</username>
            <password>ojoirshois.this-isn't-real.hrihslirhlishrglih</password>
          </server>
        </servers>
    </settings>
    ```

Maintenant que vous avez créé votre instance de registre de conteneurs, vous pouvez créer votre application MicroProfile et l’exécuter localement.

## <a name="create-your-microprofile-application"></a>Créer votre application MicroProfile

Cet exemple de code est basé sur un exemple d’application disponible sur GitHub. Pour cloner le code sur votre ordinateur, entrez les commandes suivantes :

```
git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git

cd microprofile-docker-helloworld
```

Ce répertoire contient un fichier *pom.xml* que vous pouvez utiliser pour spécifier le projet au format utilisé par l’outil de build Maven. Vous pouvez modifier le fichier selon vos besoins. Les propriétés `docker.registry` et `docker.name` doivent notamment être remplacées par les propriétés `docker.registry` et `docker.name` qui ont été créées lors de la configuration de l’instance de registre de conteneurs Azure.

Un autre fichier d’importance dans ce répertoire est le Dockerfile, qui est reproduit ci-dessous :

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Le fichier Dockerfile crée un conteneur Docker qui est basé sur le conteneur Docker Payara Micro. Il est copié dans le fichier WAR qui a été créé lors du processus de build. Il expose également le port 8080, ce qui permet d’accéder au service (une fois celui-ci opérationnel) à l’intérieur du conteneur Docker.

Lorsque vous ouvrirez le répertoire *src*, vous découvrirez la classe `Application` qui est reproduite ici :

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

L’annotation *@ApplicationPath("/api")* spécifie le point de terminaison de base de ce microservice. Autrement dit, pour tous les points de terminaison, */api* précède le reste de l’URL qui est nécessaire pour accéder à n’importe quel point de terminaison REST.

À l’intérieur du package *api* se trouve une classe intitulée `API`, qui contient le code suivant :

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld.api;

import javax.enterprise.context.ApplicationScoped;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
import javax.ws.rs.Produces;

import static javax.ws.rs.core.MediaType.TEXT_HTML;

@ApplicationScoped
@Path("/")
public class API {

    @GET
    @Path("/helloworld")
    @Produces(TEXT_HTML)
    public String info() {
        return "Hello, world!";
    }
}
```

Avec l’annotation *@Path("/helloworld")* , vous voyez que ce point de terminaison REST, une fois associé au */api* spécifié dans la classe `Application`, devient */api/helloworld*. Lorsque vous appelez ce point de terminaison à l’aide d’une requête HTTP GET, vous voyez que la méthode produit du texte (HTML), qui correspond en fait à la chaîne de caractères codée en dur « Hello world! ».

Jusqu’à maintenant, cet article a expliqué tout le code nécessaire à la création d’un microservice à l’aide de MicroProfile. Vous pouvez à présent utiliser Maven pour le générer puis le conteneuriser dans un conteneur Docker, avant de l’exécuter localement. Pour cela, effectuez les étapes suivantes :

1. Exécutez `mvn clean package` et attendez la fin de l’exécution.

1. Exécutez `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`. Par exemple, *docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest*, où *\<registre.docker>* est *jogilescr.azurecr.io* et *\<nom.docker>* est *samples/docker-helloworld*.

1. Essayez d’accéder à [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) et à [http://localhost:8080/health](http://localhost:8080/health) dans votre navigateur web. Si vous voyez la réponse attendue « Hello, world! », (et les informations sur l’intégrité du point de terminaison [/health](http://localhost:8080/health)), cela signifie que l’application MicroProfile a été correctement déployée sur votre ordinateur local.

## <a name="push-the-container-to-the-azure-container-registry-instance"></a>Poussée (push) du conteneur vers une instance de registre de conteneurs Azure

À présent que vous avez généré et exécuté votre application MicroProfile sur votre ordinateur local, l’étape suivante consiste à pousser (push) ce conteneur vers votre instance de registre de conteneurs. 

> [!NOTE]
> Même si cet article utilise une instance de registre de conteneurs Azure, vous pouvez utiliser n’importe quelle instance de registre de conteneurs, tant que le fichier *pom.xml* est modifié de façon à pointer vers l’emplacement approprié.

1. Pour nettoyer, compiler et créer une image Docker locale, exécutez `mvn clean package`.
2. Pour pousser (push) le conteneur vers l’instance de registre de conteneurs Azure, exécutez `mvn dockerfile:push`.

Votre image conteneur Docker est désormais chargée dans l’instance de registre de conteneurs Azure. Toutefois, son exécution n’a pas encore démarré. Vous devez maintenant la déployer sur une instance Azure Web App pour conteneurs. 

## <a name="create-an-azure-web-app-for-containers-instance"></a>Créer une instance Azure Web App pour conteneurs

1. Dans le [portail Azure](http://portal.azure.com), dans le volet gauche, sélectionnez **Web + Mobile**, puis effectuez les étapes suivantes :

   a. Spécifiez un nom. Le nom devient l’URL publique de l’application web. Il est donc préférable de choisir un nom facile à mémoriser. Si vous le souhaitez, vous pourrez ajouter un nom de domaine personnalisé ultérieurement.

   b. Dans la section **Configurer le conteneur** située sous **Source d’image**, sélectionnez **Azure Container Registry**, puis, dans la liste déroulante, sélectionnez l’image dont vous avez besoin.

   c. Vous n’avez pas besoin de spécifier de valeur dans le champ **Fichier de démarrage**.

1. Une fois que vous avez créé l’instance, sélectionnez-la, puis sélectionnez **Paramètres d’application**. Pour la **clé**, entrez **WEBSITES_PORT**, et pour la **valeur**, entrez **8080**. Ces paramètres indiquent à Azure le port qui doit être exposé dans le conteneur et qui doit être mappé au port 80 en externe.

1. (Facultatif) Sélectionnez le lien **Conteneur Docker**, puis activez **Déploiement continu**. En procédant ainsi, chaque fois que vous mettez à jour l’image de l’instance de registre de conteneurs Azure, celle-ci est automatiquement mise à jour dans l’instance Azure Web App pour conteneurs.

1. Vous devriez pouvoir accéder aux instances hébergées dans Azure, aux emplacements `http://<appname>.azurewebsites.net/microprofile/api/helloworld` et `http://<appname>.azurewebsites.net/health`.

## <a name="summary"></a>Résumé

Dans ce tutoriel, vous avez vu les différentes étapes de création d’un microservice simple sur MicroProfile, vous avez conteneurisé ce microservice dans un conteneur Docker, puis vous l’avez exécuté localement et publié dans Azure. Vous pouvez étendre votre microservice pour ajouter d’autres fonctionnalités utiles. Pour plus d’informations, consultez [MicroProfile.io](https://microprofile.io/).
