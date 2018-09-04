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
ms.openlocfilehash: 323ae247c3df8c7d7b180d9d60b9014e4e2d7382
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240959"
---
# <a name="deploy-a-java-based-microprofile-service-to-azure-web-app-for-containers"></a>Déployez un service MicroProfile en Java vers Azure Web App pour conteneurs

MicroProfile est un bon outil de génération d’applications Java extrêmement petites, qui peuvent être déployées rapidement et facilement vers des services tels qu’[Azure Web App pour conteneurs](https://azure.microsoft.com/services/app-service/containers/). Dans ce tutoriel, nous allons créer un simple microservice basé sur MicroProfile que nous allons intégrer à un conteneur Docker, déployer dans un [ACR](https://azure.microsoft.com/services/container-registry/), et finalement héberger à l’aide d’Azure Web App pour conteneurs.

> [!NOTE]
>
> Cette procédure fonctionne avec n’importe quelle implémentation de MicroProfile.io tant que l’image du conteneur Docker s’exécute automatiquement (c’est-à-dire qu’elle inclue le runtime).

Concrètement, cet exemple utilise [Payara Micro](https://www.payara.fish/payara_micro) et la version [MicroProfile 1.3](https://microprofile.io/) pour créer un petit fichier Java au format war (5,085 Ko sur l’ordinateur d’origine), avant de l’empaqueter dans une image Docker (qui pèse approximativement 174 Mo). Cette image Docker contient tout le nécessaire pour un déploiement de cette application web entièrement conteneurisée.

Étant donné le fonctionnement de Docker, il est fréquent que l’image Docker 174 Mo n’aient pas besoin d’être intégralement redéployée à chaque modification du code source, Docker ne téléchargeant que les parties modifiées (réduisant ainsi drastiquement le volume de données). Ce mode de fonctionnement permet de créer très rapidement et très efficacement de nouvelles versions d’une application MicroProfile via un pipeline CI/CD, en réduisant les conflits et assurant des itérations de développement rapides.

Dans ce tutoriel, nous allons tout d’abord créer et exécuter un code en local, puis le déployer en tant qu’application web sur Azure. Dans les deux cas, il nous faudra compter sur Docker pour réduire et standardiser nos tâches. Avant de commencer, nous allons créer un ACR afin d’y stocker nos conteneurs Docker.

## <a name="creating-an-azure-container-registry"></a>Création d’un ACR

Pour créer l’ACR, nous utiliserons le [Portail Azure](http://portal.azure.com), mais notez qu’il existe d’autres possibilités, telles que l’interface Azure CLI. Suivez les étapes ci-dessous pour créer un nouvel ACR :

1. Connectez-vous au [Portail Azure](http://portal.azure.com), puis créez une ressource ACR. Entrez un nom de registre (notez qu’il s’agit du nom devant être défini en tant que nom de propriété `docker.registry` dans `pom.xml`). Modifiez les paramètres par défaut à votre guise, puis cliquez sur Créer.

1. Une fois le registre de conteneurs en ligne (c’est-à-dire environ 30 secondes après avoir cliqué sur Créer), cliquez sur ce dernier, puis sur le lien Clés d’accès situé dans le menu de gauche. À cette étape, vous devez activer le paramètre Utilisateur administrateur, de sorte que nous puissions accéder à ce registre de conteneurs depuis nos ordinateurs (afin d’y envoyer des conteneurs Docker), mais aussi autoriser l’accès depuis l’instance Web App pour conteneurs Azure que nous configurerons prochainement.

1. Pendant que vous vous trouvez dans la section Clés d’accès, remarquez les valeurs `username` et `password`. Nous allons les copier/coller dans notre fichier Maven global `settings.xml` (pour plus d’informations sur les paramètres Maven, reportez-vous au site web du [projet Apache Maven](https://maven.apache.org/settings.html)). Pour référence, voici une version masquée du fichier `${user.home}/.m2/settings.xml` située sur le système d’origine :

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

Cette étape terminée, nous pouvons passer à la génération et à l’exécution de notre application MicroProfile en local.

## <a name="creating-our-microprofile-application"></a>Création de notre application MicroProfile

Cet exemple se fonde sur un exemple d’application disponible sur GitHub, nous pouvons donc le cloner et parcourir le code pas à pas. Suivez les étapes ci-dessous pour cloner le code sur votre ordinateur :

1. `git clone https://github.com/Azure-Samples/microprofile-docker-helloworld.git`
1. `cd microprofile-docker-helloworld`

Ce répertoire comprend un fichier `pom.xml` servant à spécifier le projet au format utilisé par l’outil de génération Maven. Ce fichier peut être modifié pour s’adapter à vos besoins. Les propriétés `docker.registry` et `docker.name` doivent notamment être remplacées par les propriétés `docker.registry` et `docker.name` créées lors de la configuration de l’ACR.

Un autre fichier d’importance dans ce répertoire est le Dockerfile, qui est reproduit ci-dessous :

```dockerfile
FROM payara/micro

ARG WAR_FILE
COPY target/${WAR_FILE} $DEPLOY_DIR

EXPOSE 8080
```

Ce Dockerfile crée simplement un conteneur Docker fondé sur un conteneur Docker Payara Micro, puis copie le fichier .war créé pendant la génération. Il expose également le port 8080, de sorte que nous puissions accéder au service une fois opérationnel dans un conteneur Docker.

En explorant plus en profondeur le répertoire `src`, nous découvrirons finalement la classe `Application` reproduite ci-dessous :

```java
package com.microsoft.azure.samples.microprofile.docker.helloworld;

import javax.ws.rs.ApplicationPath;

@ApplicationPath("/api")
public class Application extends javax.ws.rs.core.Application { }
```

L’annotation `@ApplicationPath("/api")` indique le point de terminaison de base de ce microservice. Autrement dit, les URL servant à accéder aux points de terminaison REST seront toutes précédées de la mention `/api`.

À l’intérieur du package `api` se trouve une classe intitulée `API`, contenant le code suivant :

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

En utilisant l’annotation `@Path("/helloworld")`, nous pouvons voir que ce point de terminaison REST, une fois combiné avec le `/api` spécifié dans la classe `Application` deviendra `/api/helloworld`. Lorsque ce point de terminaison est appelé à l’aide d’une requête HTTP GET, on peut remarquer que la méthode produit du texte/html, et qu’il s’agit en réalité d’une simple chaîne de caractères « Hello world! » codée en dur.

Nous avons à présent exploré tout le code nécessaire à la création d’un microservice à l’aide de MicroProfile. Nous pouvons à présent utiliser Maven pour le générer puis le conteneuriser dans un conteneur Docker, avant de l’exécuter en local. Pour ce faire, procédez comme suit :

1. Exécutez `mvn clean package` et attendez que son exécution soit menée à bien.

1. Exécutez `docker run -it --rm -p 8080:8080 <docker.registry>/<docker.name>:latest`, par exemple `docker run -it --rm -p 8080:8080 jogilescr.azurecr.io/samples/docker-helloworld:latest`, si votre paramètre `docker.registry` a la valeur `jogilescr.azurecr.io` et que votre paramètre `docker.name` a la valeur `samples/docker-helloworld`.

1. Essayez d’accéder à [http://localhost:8080/microprofile/api/helloworld](http://localhost:8080/microprofile/api/helloworld) et à [http://localhost:8080/health](http://localhost:8080/health) dans votre navigateur web. Si vous voyez la réponse attendue « Hello, world! », (et les informations sur l’intégrité du point de terminaison [/intégrité ](http://localhost:8080/health)), cela signifie que vous avez correctement déployé l’application MicroProfile sur votre ordinateur local.

## <a name="pushing-to-the-azure-container-registry"></a>Envoi vers l’ACR

À présent que nous avons généré et exécuté avec succès notre application MicroProfile sur notre ordinateur local, l’étape suivante consiste à envoyer ce conteneur dans notre registre de conteneurs. Nous utilisons dans ce tutoriel Azure Container Registry, mais l’opération fonctionnera avec n’importe quel registre de conteneurs (du moment que le fichier `pom.xml` est configuré pour pointer vers l’emplacement approprié).

1. Exécutez `mvn clean package` pour effacer, compiler et créer une image Docker locale.
2. Exécutez `mvn dockerfile:push` pour l’envoyer vers Azure Container Repository.

À ce stade, votre image de conteneur Docker est chargée sur l’ACR, mais elle n’est pas encore exécutée étant donné qu’il nous faut la déployer dans une instance Azure Web App pour conteneurs. C’est ce que nous allons faire à présent.

## <a name="creating-an-azure-web-app-for-containers-instance"></a>Création d’une instance Web App pour conteneurs

1. Retournez sur le [Portail Azure](http://portal.azure.com) et créez une instance Web App pour conteneurs (sous l’en-tête « Web + Mobile » du menu). Quelques pointeurs :

   1. Le nom que vous renseignez ici correspondra à l’URL publique de l’application web (bien qu’un domaine personnalisé puisse être ajouté plus tard si besoin), il peut donc être judicieux de choisir un nom que vous retiendrez facilement.

   1. Lorsque vous vous rendez sur la section « Configurer un conteneur » vous pouvez sélectionner « Azure Container Registry » pour la « Source de l’image », puis sélectionner l’image appropriée à partir des listes déroulantes.

   1. Vous n’avez pas besoin de spécifier de valeur dans le champ « Fichier de démarrage ».

1. Une fois l’instance créée (encore une fois, le processus est très rapide), cliquez dessus, puis sur l’élément de menu « Paramètres de l’application ». Ici, vous devez ajouter un nouveau paramètre d’application, avec la clé `WEBSITES_PORT` et la valeur `8080`. Cette opération communique à Azure le port que vous souhaitez exposer dans le conteneur, et il sera mappé au port externe 80.

1. Facultativement, vous pouvez cliquer sur le lien « Conteneur Docker », et autoriser le « Déploiement continu ». Ce choix permet d’appliquer automatiquement toute mise à jour de l’image ACR dans l’instance Web App pour conteneurs.

1. Vous devriez pouvoir accéder aux instances hébergées sur Azure à `http://<appname>.azurewebsites.net/microprofile/api/helloworld` et `http://<appname>.azurewebsites.net/health`.

## <a name="summary"></a>Résumé

Au cours de ce tutoriel, nous avons vu les différentes étapes de création d’un microservice sur MicroProfile simple, que nous avons conteneurisé dans un conteneur Docker, exécuté en local et publié sur Azure. Nous n’aborderons pas dans ce tutoriel l’ajout de fonctionnalités plus utiles à notre microservice. Toutefois, vous trouverez de nombreux tutoriels et conseils relatifs à MicroProfile sur internet. Nous encourageons également les lecteurs à consulter [MicroProfile.io](https://microprofile.io/) afin d’accéder à davantage de contenu.