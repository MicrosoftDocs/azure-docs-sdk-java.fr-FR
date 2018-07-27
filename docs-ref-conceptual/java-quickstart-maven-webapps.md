---
title: Déployer une application web Java dans Azure en cinq minutes avec Maven | Microsoft Docs
description: Créer et déployer une application Java générée avec Maven dans Azure
services: app-service\web
documentationcenter: ''
author: rloutlaw
manager: douge
editor: ''
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/17/2017
ms.author: routlaw
ms.openlocfilehash: 1adc0a104ba22bcd353664e68323165890e46c64
ms.sourcegitcommit: 30d502b3150fa14bcc1251f5f88c7c0dd83e531e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2017
ms.locfileid: "22033631"
---
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a>Créer et déployer une application Java dans Azure avec Maven

Ce démarrage rapide vous aide à créer et à déployer une application web Java simple dans [Azure App Service](/azure/app-service/app-service-value-prop-what-is) en quelques minutes à l’aide d’[Apache Maven](http://maven.apache.org) et d’Azure CLI.

## <a name="before-you-begin"></a>Avant de commencer

Avant de commencer, configurez comme suit :

- [Git](https://git-scm.com/)
- [Java 8](https://www.azul.com/downloads/zulu/)
- [Maven 3](http://maven.apache.org/download.cgi)
- [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="get-the-sample-code"></a>Obtention de l'exemple de code

Clonez le référentiel de l’exemple d’application sur votre ordinateur local. L’exemple est une application JSP simple avec une configuration Maven supplémentaire dans le projet `pom.xml` pour tester l’application en local et aider au déploiement de l’exemple sur Azure App Service.

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a>Exécutez l’application localement.

Ouvrez une invite de commandes et utilisez Maven pour générer l’application, puis exécutez-la dans un conteneur web [Tomcat](https://tomcat.apache.org) local. 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

Ouvrez un navigateur web et accédez à l’adresse http://localhost:8080 pour prévisualiser l’application :

  ![Sortie de Hello World à partir de l’exemple d’application Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a>Connexion à Azure

Connectez-vous à Azure CLI avec `az login`. Ce démarrage rapide utilise l’interface CLI pour interroger et créer les ressources Azure nécessaires à l’hébergement de l’application.
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources   

Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.

```azurecli
az group create --location "East US" --name myResourceGroup
```

Pour connaître les autres valeurs que vous pouvez utiliser pour `---location`, utilisez la commande [az appservice list-locations](/cli/azure/appservice#list-locations)

## <a name="create-an-app-service-plan"></a>Créer un plan App Service

Créez un [plan App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) **GRATUIT** avec la commande [az appservice plan create](/cli/azure/appservice/plan#create). Un plan App Service alloue des ressources partagées entre toutes les applications web en cours d’exécution dans ce même plan.


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

Lorsque le plan App Service est prêt, Azure CLI affiche des informations similaires à l’exemple suivant :

```json
{
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "location": "East US",
    "sku": {
    "capacity": 1,
    "family": "S",
    "name": "S1",
    "tier": "Standard"
    },
    "status": "Ready",
    "type": "Microsoft.Web/serverfarms"
}
```


## <a name="create-a-web-app"></a>Créer une application web

Créez une application web qui utilise les ressources du plan à l’aide de la commande [az webapp create](/cli/azure/appservice/web#create) dans Azure CLI. La définition de l’application web fournit un espace pour déployer le code et une URL pour accéder à l’application en cours d’exécution.

Dans la commande ci-dessous, indiquez le nom unique de votre propre application là où se trouve <appname> l’espace réservé. La commande <appname> est utilisée dans le nom d’hôte par défaut de l’application web. Si <appname> n’est pas une valeur unique, le message d’erreur « Un site Web nommé ainsi existe déjà » s’affiche.

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

Une fois l’application web créée, Azure CLI affiche des informations similaires à celles de l’exemple suivant.1

```json
{
    "clientAffinityEnabled": true,
    "defaultHostName": "<appname>.azurewebsites.net",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<appname>",
    "isDefaultContainer": null,
    "kind": "app",
    "location": "East US",
    "name": "<app_name>",
    "repositorySiteName": "<app_name>",
    "reserved": true,
    "resourceGroup": "myResourceGroup",
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/my-free-appservice-plan",
    "state": "Running",
    "type": "Microsoft.Web/sites",
}
```

## <a name="configure-java-and-tomcat"></a>Configurer Java et Tomcat

Configurez l’application web pour utiliser Java et Tomcat à l’aide de la commande [az webapp config](/cli/azure/appservice/web#config) dans Azure CLI. L’exemple suivant configure App Service pour exécuter Java 8 et [Apache Tomcat 8.5](http://tomcat.apache.org/) et ainsi exécuter l’application.

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a>Configurer Maven 

L’exemple Maven `pom.xml` inclut la configuration pour convertir l’exemple en FTP dans Azure, mais vous devez le personnaliser pour pouvoir le déployer sur votre application web. Récupérez vos informations d’identification App Service avec la commande [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles) :

```azurecli
az webapp deployment list-publishing-profiles  \
--name appname \ 
--resource-group myResourceGroup  \
--query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" 
```

```json
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "appname\\$appname"
  }
]
```

Remplacez les espaces réservés du fichier `az-settings.xml` par le mot de passe, le nom d’utilisateur et le nom d’hôte FTP de la sortie. Veillez à n’utiliser qu’un seul caractère `\` dans le nom d’utilisateur et non la valeur d’échappement de la sortie de l’interface CLI.
   
```XML
...
    <server>
      <id>azure-hello-world</id>
      <username>appname\$appname</username>
      <password>aBcDeFgHiJkLmNoPqRsTuVwXyZ</password>
    </server>
...
   <configuration>
     <fromFile>${basedir}/target/AzureAppDemo-0.0.1-SNAPSHOT.war</fromFile>
     <url>ftp://waws-prod-blu-045.ftp.azurewebsites.windows.net/site/wwwroot</url>
     <toFile>webapps/ROOT.war</toFile>
     <serverId>azure-hello-world</serverId>
   </configuration>
...
```

## <a name="deploy-the-sample-application"></a>Déployer l’exemple d’application

Déployez dans Azure avec l’exemple à l’aide du paramètre Maven `-s` pour utiliser la configuration du fichier `az-settings.xml`.

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a>Accéder à l’application web

Affichez l’exemple en cours d’exécution dans Azure :

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a>Mettre à jour l’application

Avec un éditeur de texte, ouvrez `src/main/webapp/index.jsp` et remplacez le fichier JSP existant par le fichier ci-dessous.

```html
<%--
  Copyright (c) Microsoft Corporation. All rights reserved.
  Licensed under the MIT License. See License.txt in the project root for
  license information.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java"  import="java.util.Date" %>
<html>
<head>
  <title>Azure Samples Hello World</title>
</head>
<body>
  <H1>Hello Azure!</H1>
   Current time is: <%= new Date() %>
</body>
</html>
```

Déployez la mise à jour avec Maven :

```
mvn clean package
mvn install -s az-settings.xml
```

Actualisez votre navigateur après le redéploiement de l’application pour afficher les modifications.

## <a name="manage-your-new-azure-app"></a>Gérer votre nouvelle application Azure

Accédez au portail Azure pour voir l’application web que vous venez de créer.

Pour ce faire, connectez-vous au portail : [https://portal.azure.com](https://portal.azure.com).

Dans le menu de gauche, cliquez sur **App Service**, puis cliquez sur le nom de votre application web Azure.

 ![Sélectionner votre application dans la liste des applications web dans le portail](media/azure-app-service-portal.png)

Tester la surveillance en exécutant `curl` sur l’application pour envoyer du trafic.

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

L’activité de la requête s’affiche dans la surveillance après quelques minutes.

 ![Surveillance dans le portail Azure](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a>Supprimer des ressources

Pour supprimer toutes les ressources créées dans ce guide, exécutez la commande suivante :

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Accédez à la liste complète des [exemples Azure Java](https://azure.microsoft.com/resources/samples/?term=java).