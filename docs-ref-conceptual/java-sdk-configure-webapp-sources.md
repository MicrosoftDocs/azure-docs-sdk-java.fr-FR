---
title: Configurer des déploiements d’applications web avec Java | Microsoft Docs
description: Exemple de code Java pour la configuration de déploiements Git ou FTP d’Azure App Service à l’aide du kit de développement logiciel (SDK) Azure pour Java
author: rloutlaw
manager: douge
ms.assetid: 833e9c78-1e50-4c23-a611-f73a2f0c2983
ms.service: Azure
ms.devlang: java
ms.topic: article
ms.date: 03/30/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: c416cb871ac8264cd6da2045d1ffdd50607fb092
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592624"
---
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a>Configurer des sources de déploiement d’Azure App Service depuis vos applications Java

[Cet exemple](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) déploie un code pour quatre applications en un seul plan [Azure App Service](https://docs.microsoft.com/azure/app-service/), et chacune d’elles utilise une source de déploiement différente.

## <a name="run-the-sample"></a>Exécution de l'exemple

Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur. Exécutez ensuite la commande suivante :

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).

## <a name="authenticate-with-azure"></a>S’authentifier avec Azure

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a>Créer une application App Service qui exécute Apache Tomcat

```java
// create a new Standard app service plan and create a single Java 8/Tomcat 8 app in it
WebApp app1 = azure.webApps().define(app1Name)
             .withNewResourceGroup(rgName)
             .withNewAppServicePlan(planName)
             .withRegion(Region.US_WEST)
             .withPricingTier(AppServicePricingTier.STANDARD_S1)
             .withJavaVersion(JavaVersion.JAVA_8_NEWEST)
             .withWebContainer(WebContainer.TOMCAT_8_0_NEWEST)
             .create();
```

`withJavaVersion()` et `withWebContainer()` configurent App Service de sorte qu’il traite les requêtes HTTP avec Tomcat 8.

## <a name="deploy-a-java-application-using-ftp"></a>Déployer une application Java à l’aide de FTP
```java
// pass the PublishingProfile that contains FTP information to a helper method 
uploadFileToFtp(app1.getPublishingProfile(), "helloworld.war", 
      ManageWebAppSourceControl.class.getResourceAsStream("/helloworld.war"));

// Use the FTP classes in the Apache Commons library to connect to Azure using 
// the information from the PublishingProfile
private static void uploadFileToFtp(PublishingProfile profile, String fileName, InputStream file) throws Exception {
        FTPClient ftpClient = new FTPClient();
        String[] ftpUrlSegments = profile.ftpUrl().split("/", 2);
        String server = ftpUrlSegments[0];
        // Tomcat will deploy WAR files uploaded to this directory.
        String path = "./site/wwwroot/webapps"; 

        // FTP the build WAR to Azure
        ftpClient.connect(server);
        ftpClient.login(profile.ftpUsername(), profile.ftpPassword());
        ftpClient.setFileType(FTP.BINARY_FILE_TYPE);
        ftpClient.changeWorkingDirectory(path);
        ftpClient.storeFile(fileName, file);
        ftpClient.disconnect();
}
```

Ce code charge un fichier WAR dans le répertoire `/site/wwwroot/webapps`. Tomcat déploie les fichiers WAR placés dans ce répertoire par défaut dans App Service.

## <a name="deploy-a-java-application-from-a-local-git-repo"></a>Déployer une application Java à partir d’un référentiel Git local

```java
// get the publishing profile from the App Service webapp
PublishingProfile profile = app2.getPublishingProfile();

// create a new Git repo in the sample directory under src/main/resources 
Git git = Git
    .init()
    .setDirectory(new File(ManageWebAppSourceControl.class.getResource("/azure-samples-appservice-helloworld/").getPath()))
    .call();
git.add().addFilepattern(".").call();
// add the files in the sample app to an initial commit
git.commit().setMessage("Initial commit").call(); 

// push the commit using the Azure Git remote URL and credentials in the publishing profile
PushCommand command = git.push();
command.setRemote(profile.gitUrl()); 
command.setCredentialsProvider(new UsernamePasswordCredentialsProvider(profile.gitUsername(), profile.gitPassword()));
command.setRefSpecs(new RefSpec("master:master")); 
command.setForce(true);
command.call();
```      

Ce code utilise les bibliothèques [JGit](https://eclipse.org/jgit/) pour créer un référentiel Git dans le dossier `src/main/resources/azure-samples-appservice-helloworld`. L’exemple ajoute ensuite tous les fichiers du dossier pour une validation initiale et envoie la validation dans Azure à l’aide des informations de déploiement Git présentes dans le `PublishingProfile` de l’application web. 

>[!NOTE]
> La disposition des fichiers dans le référentiel doit correspondre précisément à la façon dont vous souhaitez que les fichiers dans le répertoire `/site/wwwroot/` d’Azure App Service soient déployés.

## <a name="deploy-an-application-from-a-public-git-repo"></a>Déployer une application à partir d’un référentiel Git public

```java
// deploy a .NET sample app from a public GitHub repo into a new webapp
WebApp app3 = azure.webApps().define(app3Name)
                .withNewResourceGroup(rgName)
                .withExistingAppServicePlan(plan)
                .defineSourceControl()
                .withPublicGitRepository(
                   "https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
                .withBranch("master")
                .attach()
                .create();
 ```

 Le runtime d’App Service génère et déploie automatiquement le projet .NET à l’aide du dernier code présent sur la branche `master` du référentiel.

## <a name="continuous-deployment-from-a-github-repo"></a>Déploiement continu à partir d’un référentiel GitHub

```java
// deploy the application whenever you push a new commit or merge a pull request into your master branch
WebApp app4 = azure.webApps()
                    .define(app4Name)
                    .withExistingResourceGroup(rgName)
                    .withExistingAppServicePlan(plan)
                    // Uncomment the following lines to turn on continuous deployment scenario
                    //.defineSourceControl()
                    //    .withContinuouslyIntegratedGitHubRepository("username", "reponame")
                    //    .withBranch("master")
                    //    .withGitHubAccessToken("YOUR GITHUB PERSONAL TOKEN")
                    //    .attach()
                    .create();
```  

Les valeurs `username` et `reponame` sont utilisées dans GitHub. [Créez un jeton d’accès personnel GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) avec autorisation de lecture du référentiel et transmettez-le à `withGitHubAccessToken`. 


## <a name="sample-explanation"></a>Explication de l’exemple

L’exemple crée la première application à l’aide de Java 8 et Tomcat 8 en cours d’exécution dans un plan [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service créé récemment. Le code convertit ensuite le fichier WAR en FTP à l’aide des informations présentes dans l’objet `PublishingProfile`, et Tomcat procède au déploiement.

La deuxième application se sert du même plan que la première, et est aussi configurée comme application Java 8/Tomcat 8. Les bibliothèques JGit créent un référentiel Git dans un dossier qui contient une application web Java décompressée dans une structure de répertoires mappée sur App Service. Une nouvelle validation ajoute les fichiers du dossier dans le nouveau référentiel Git. Git envoie la validation à Azure avec une URL distante et un nom d’utilisateur/mot de passe fournis par le `PublishingProfile` de l’application web.

La troisième application n’est pas configurée pour Java et Tomcat. À la place, un exemple .NET dans un référentiel GitHub public est déployé directement depuis la source.

La quatrième application déploie le code dans la branche principale chaque fois que vous effectuez des modifications par push ou que vous fusionnez une demande de tirage (pull request) avec la branche principale du référentiel GitHub.

| Classe utilisée dans l’exemple | Notes
|-------|-------|
| [WebApp](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | Créé à partir de la chaîne Fluent `azure.webApps().define()....create()`. Crée une application web App Service et toutes les ressources dont elle a besoin. La plupart des méthodes interrogent l’objet pour obtenir des détails de configuration, mais les méthodes verbales comme `restart()` modifient l’état de l’application web.
| [WebContainer](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | Classe avec des champs publics statiques utilisée en tant que paramètres de l’élément `withWebContainer()` lors de la définition d’une application web exécutant un conteneur web Java. Dispose de choix pour les versions Jetty et Tomcat.
| [PublishingProfile](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | Obtenu via un objet d’application web à l’aide de la méthode `getPublishingProfile()`. Contient des informations de déploiement FTP et Git, notamment le nom d’utilisateur et le mot de passe du déploiement (différentes de celles du compte Azure ou des informations d’identification du principal de service).
| [AppServicePlan](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | Retourné par `azure.appServices().appServicePlans().getByResourceGroup()`. Les méthodes sont disponibles pour vérifier la capacité, le niveau et le nombre des applications web en cours d’exécution dans le plan.
| [AppServicePricingTier](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | Classe avec des champs publics statiques qui représentent les niveaux d’App Service. Permet de définir un niveau plan correspondant lors de la création d’applications avec `withPricingTier()` ou directement lors de la définition d’un plan via `azure.appServices().appServicePlans().define()`
| [JavaVersion](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | Classe avec des champs publics statiques qui représentent les versions Java prises en charge par App Service. Utilisée avec `withJavaVersion()` pendant la chaîne `define()...create()` au moment de la création d’une application web.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [next-steps](includes/java-next-steps.md)]