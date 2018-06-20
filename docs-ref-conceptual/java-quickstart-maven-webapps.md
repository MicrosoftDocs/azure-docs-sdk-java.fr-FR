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
# <a name="create-and-deploy-a-java-app-to-azure-with-maven"></a><span data-ttu-id="8379f-103">Créer et déployer une application Java dans Azure avec Maven</span><span class="sxs-lookup"><span data-stu-id="8379f-103">Create and deploy a Java app to Azure with Maven</span></span>

<span data-ttu-id="8379f-104">Ce démarrage rapide vous aide à créer et à déployer une application web Java simple dans [Azure App Service](/azure/app-service/app-service-value-prop-what-is) en quelques minutes à l’aide d’[Apache Maven](http://maven.apache.org) et d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8379f-104">This quickstart helps you create and deploy a simple Java web app to [Azure App Service](/azure/app-service/app-service-value-prop-what-is) in just a few minutes using [Apache Maven](http://maven.apache.org) and the Azure CLI.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8379f-105">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8379f-105">Before you begin</span></span>

<span data-ttu-id="8379f-106">Avant de commencer, configurez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8379f-106">Before you start, set up the following:</span></span>

- [<span data-ttu-id="8379f-107">Git</span><span class="sxs-lookup"><span data-stu-id="8379f-107">Git</span></span>](https://git-scm.com/)
- [<span data-ttu-id="8379f-108">Java 8</span><span class="sxs-lookup"><span data-stu-id="8379f-108">Java 8</span></span>](https://www.azul.com/downloads/zulu/)
- [<span data-ttu-id="8379f-109">Maven 3</span><span class="sxs-lookup"><span data-stu-id="8379f-109">Maven 3</span></span>](http://maven.apache.org/download.cgi)
- [<span data-ttu-id="8379f-110">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8379f-110">Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-az-cli2)

<span data-ttu-id="8379f-111">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="8379f-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="get-the-sample-code"></a><span data-ttu-id="8379f-112">Obtention de l'exemple de code</span><span class="sxs-lookup"><span data-stu-id="8379f-112">Get the sample code</span></span>

<span data-ttu-id="8379f-113">Clonez le référentiel de l’exemple d’application sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="8379f-113">Clone the sample app repository to your local machine.</span></span> <span data-ttu-id="8379f-114">L’exemple est une application JSP simple avec une configuration Maven supplémentaire dans le projet `pom.xml` pour tester l’application en local et aider au déploiement de l’exemple sur Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8379f-114">The sample is a simple JSP application with additional Maven configuration in the project `pom.xml` to test the app locally and help deploy the sample to Azure App Service.</span></span>

```
git clone https://github.com/Azure-Samples/app-service-maven
```

## <a name="run-the-app-locally"></a><span data-ttu-id="8379f-115">Exécutez l’application localement.</span><span class="sxs-lookup"><span data-stu-id="8379f-115">Run the app locally</span></span>

<span data-ttu-id="8379f-116">Ouvrez une invite de commandes et utilisez Maven pour générer l’application, puis exécutez-la dans un conteneur web [Tomcat](https://tomcat.apache.org) local.</span><span class="sxs-lookup"><span data-stu-id="8379f-116">Open a command prompt and use Maven to build the app and run it in a local [Tomcat](https://tomcat.apache.org) web container.</span></span> 

```
cd app-service-maven
mvn package
mvn tomcat7:run-war
```

<span data-ttu-id="8379f-117">Ouvrez un navigateur web et accédez à l’adresse http://localhost:8080 pour prévisualiser l’application :</span><span class="sxs-lookup"><span data-stu-id="8379f-117">Open a web browser and navigate to http://localhost:8080 to preview the app:</span></span>

  ![Sortie de Hello World à partir de l’exemple d’application Java](media/maven-quickstart/java-app-hello-world-output.png)

## <a name="log-in-to-azure"></a><span data-ttu-id="8379f-119">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="8379f-119">Log in to Azure</span></span>

<span data-ttu-id="8379f-120">Connectez-vous à Azure CLI avec `az login`.</span><span class="sxs-lookup"><span data-stu-id="8379f-120">Log in to the Azure CLI with `az login`.</span></span> <span data-ttu-id="8379f-121">Ce démarrage rapide utilise l’interface CLI pour interroger et créer les ressources Azure nécessaires à l’hébergement de l’application.</span><span class="sxs-lookup"><span data-stu-id="8379f-121">This quickstart uses the CLI to query and create the Azure resources needed to host the app.</span></span>
   
```azurecli
az login
```

## <a name="create-a-resource-group"></a><span data-ttu-id="8379f-122">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8379f-122">Create a resource group</span></span>   

<span data-ttu-id="8379f-123">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8379f-123">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8379f-124">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="8379f-124">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

```azurecli
az group create --location "East US" --name myResourceGroup
```

<span data-ttu-id="8379f-125">Pour connaître les autres valeurs que vous pouvez utiliser pour `---location`, utilisez la commande [az appservice list-locations](/cli/azure/appservice#list-locations)</span><span class="sxs-lookup"><span data-stu-id="8379f-125">To see other possible values you can use for `---location`, use [az appservice list-locations](/cli/azure/appservice#list-locations)</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="8379f-126">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="8379f-126">Create an App Service plan</span></span>

<span data-ttu-id="8379f-127">Créez un [plan App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) **GRATUIT** avec la commande [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="8379f-127">Create a **FREE** [App Service plan](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) using [az appservice plan create](/cli/azure/appservice/plan#create).</span></span> <span data-ttu-id="8379f-128">Un plan App Service alloue des ressources partagées entre toutes les applications web en cours d’exécution dans ce même plan.</span><span class="sxs-lookup"><span data-stu-id="8379f-128">App Service plans allocate resources shared across all web apps running in the plan.</span></span>


```azurecli
az appservice plan create --name my-free-appservice-plan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="8379f-129">Lorsque le plan App Service est prêt, Azure CLI affiche des informations similaires à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8379f-129">When the App Service Plan is ready, the Azure CLI shows information similar to the following example:</span></span>

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


## <a name="create-a-web-app"></a><span data-ttu-id="8379f-130">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="8379f-130">Create a web app</span></span>

<span data-ttu-id="8379f-131">Créez une application web qui utilise les ressources du plan à l’aide de la commande [az webapp create](/cli/azure/appservice/web#create) dans Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8379f-131">Create a web app that uses the plan's resources using the Azure CLI [az webapp create](/cli/azure/appservice/web#create) command.</span></span> <span data-ttu-id="8379f-132">La définition de l’application web fournit un espace pour déployer le code et une URL pour accéder à l’application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8379f-132">The web app definition provides a space to deploy the code to and a URL to access the app once it's running.</span></span>

<span data-ttu-id="8379f-133">Dans la commande ci-dessous, indiquez le nom unique de votre propre application là où se trouve <appname> l’espace réservé.</span><span class="sxs-lookup"><span data-stu-id="8379f-133">In the command below substitute your own unique app name where you see the <appname> placeholder.</span></span> <span data-ttu-id="8379f-134">La commande <appname> est utilisée dans le nom d’hôte par défaut de l’application web.</span><span class="sxs-lookup"><span data-stu-id="8379f-134">The <appname> is used in the default hostname for the web app.</span></span> <span data-ttu-id="8379f-135">Si <appname> n’est pas une valeur unique, le message d’erreur « Un site Web nommé ainsi existe déjà » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8379f-135">If <appname> is not unique, you get the friendly error message "Website with given name already exists."</span></span>

```azurecli
az webapp create --name appname --resource-group myResourceGroup --plan my-free-appservice-plan
```

<span data-ttu-id="8379f-136">Une fois l’application web créée, Azure CLI affiche des informations similaires à celles de l’exemple suivant.1</span><span class="sxs-lookup"><span data-stu-id="8379f-136">When the Web App has been created, the Azure CLI shows information similar to the following example.1</span></span>

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

## <a name="configure-java-and-tomcat"></a><span data-ttu-id="8379f-137">Configurer Java et Tomcat</span><span class="sxs-lookup"><span data-stu-id="8379f-137">Configure Java and Tomcat</span></span>

<span data-ttu-id="8379f-138">Configurez l’application web pour utiliser Java et Tomcat à l’aide de la commande [az webapp config](/cli/azure/appservice/web#config) dans Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8379f-138">Configure the web app to use Java and Tomcat using the Azure CLI's [az webapp config](/cli/azure/appservice/web#config) command.</span></span> <span data-ttu-id="8379f-139">L’exemple suivant configure App Service pour exécuter Java 8 et [Apache Tomcat 8.5](http://tomcat.apache.org/) et ainsi exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="8379f-139">The example below configures App Service to run Java 8 and [Apache Tomcat 8.5](http://tomcat.apache.org/) to run the app.</span></span>

```azurecli
az webapp config set \ 
--name appname \
--resource-group myResourceGroup \
--java-container TOMCAT \
--java-version 1.8.0_73  \
--java-container-version 8.5
```

## <a name="configure-maven"></a><span data-ttu-id="8379f-140">Configurer Maven</span><span class="sxs-lookup"><span data-stu-id="8379f-140">Configure Maven</span></span> 

<span data-ttu-id="8379f-141">L’exemple Maven `pom.xml` inclut la configuration pour convertir l’exemple en FTP dans Azure, mais vous devez le personnaliser pour pouvoir le déployer sur votre application web.</span><span class="sxs-lookup"><span data-stu-id="8379f-141">The sample's Maven `pom.xml` includes configuration to FTP the sample into Azure, but you'll need to customize it to deploy to your own web app.</span></span> <span data-ttu-id="8379f-142">Récupérez vos informations d’identification App Service avec la commande [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles) :</span><span class="sxs-lookup"><span data-stu-id="8379f-142">Retreive your App Seevice credentials with [az appservice web deployment list-publishing-profiles](/cli/azure/appservice/web/deployment#list-publishing-profiles):</span></span>

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

<span data-ttu-id="8379f-143">Remplacez les espaces réservés du fichier `az-settings.xml` par le mot de passe, le nom d’utilisateur et le nom d’hôte FTP de la sortie.</span><span class="sxs-lookup"><span data-stu-id="8379f-143">Replace the placeholders in the `az-settings.xml` file with password, username, and FTP hostname from the output.</span></span> <span data-ttu-id="8379f-144">Veillez à n’utiliser qu’un seul caractère `\` dans le nom d’utilisateur et non la valeur d’échappement de la sortie de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="8379f-144">Make sure to only use one `\` character in the username instead of the escaped value from the CLI output.</span></span>
   
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

## <a name="deploy-the-sample-application"></a><span data-ttu-id="8379f-145">Déployer l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="8379f-145">Deploy the sample application</span></span>

<span data-ttu-id="8379f-146">Déployez dans Azure avec l’exemple à l’aide du paramètre Maven `-s` pour utiliser la configuration du fichier `az-settings.xml`.</span><span class="sxs-lookup"><span data-stu-id="8379f-146">Deploy with sample to Azure, using Maven's `-s` parameter to use the configuration in the `az-settings.xml` file.</span></span>

```
mvn install -s az-settings.xml
```

## <a name="browse-to-web-app"></a><span data-ttu-id="8379f-147">Accéder à l’application web</span><span class="sxs-lookup"><span data-stu-id="8379f-147">Browse to web app</span></span>

<span data-ttu-id="8379f-148">Affichez l’exemple en cours d’exécution dans Azure :</span><span class="sxs-lookup"><span data-stu-id="8379f-148">View the sample running in Azure:</span></span>

```azurecli
az webapp browse --name appname --resource-group myResourceGroup
```

## <a name="update-the-app"></a><span data-ttu-id="8379f-149">Mettre à jour l’application</span><span class="sxs-lookup"><span data-stu-id="8379f-149">Update the app</span></span>

<span data-ttu-id="8379f-150">Avec un éditeur de texte, ouvrez `src/main/webapp/index.jsp` et remplacez le fichier JSP existant par le fichier ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8379f-150">Using a text editor, open `src/main/webapp/index.jsp`, and replace the existing JSP with the one below.</span></span>

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

<span data-ttu-id="8379f-151">Déployez la mise à jour avec Maven :</span><span class="sxs-lookup"><span data-stu-id="8379f-151">Deploy the update with Maven:</span></span>

```
mvn clean package
mvn install -s az-settings.xml
```

<span data-ttu-id="8379f-152">Actualisez votre navigateur après le redéploiement de l’application pour afficher les modifications.</span><span class="sxs-lookup"><span data-stu-id="8379f-152">Refresh your browser after the app redeploys to view your changes.</span></span>

## <a name="manage-your-new-azure-app"></a><span data-ttu-id="8379f-153">Gérer votre nouvelle application Azure</span><span class="sxs-lookup"><span data-stu-id="8379f-153">Manage your new Azure app</span></span>

<span data-ttu-id="8379f-154">Accédez au portail Azure pour voir l’application web que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="8379f-154">Go to the Azure portal to take a look at the web app you just created.</span></span>

<span data-ttu-id="8379f-155">Pour ce faire, connectez-vous au portail : [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8379f-155">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="8379f-156">Dans le menu de gauche, cliquez sur **App Service**, puis cliquez sur le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="8379f-156">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

 ![Sélectionner votre application dans la liste des applications web dans le portail](media/azure-app-service-portal.png)

<span data-ttu-id="8379f-158">Tester la surveillance en exécutant `curl` sur l’application pour envoyer du trafic.</span><span class="sxs-lookup"><span data-stu-id="8379f-158">Test the monitoring by running `curl` against the app to send some traffic.</span></span>

```bash
curl http://<appname>.azurewebsites.net/?[1-30]
```

<span data-ttu-id="8379f-159">L’activité de la requête s’affiche dans la surveillance après quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="8379f-159">You'll see the request activity in the monitoring after a couple of minutes.</span></span>

 ![Surveillance dans le portail Azure](media/java-app-monitoring.png)

## <a name="clean-up-resources"></a><span data-ttu-id="8379f-161">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="8379f-161">Clean up resources</span></span>

<span data-ttu-id="8379f-162">Pour supprimer toutes les ressources créées dans ce guide, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8379f-162">To remove all the resources created in this guide, run the following command:</span></span>

```azurecli
az group delete --name myResrouceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8379f-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8379f-163">Next steps</span></span>

<span data-ttu-id="8379f-164">Accédez à la liste complète des [exemples Azure Java](https://azure.microsoft.com/resources/samples/?term=java).</span><span class="sxs-lookup"><span data-stu-id="8379f-164">Browse the full list of [Azure Java samples](https://azure.microsoft.com/resources/samples/?term=java).</span></span>