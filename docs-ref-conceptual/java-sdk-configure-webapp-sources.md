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
# <a name="configure-azure-app-service-deployment-sources-from-your-java-applications"></a><span data-ttu-id="edab8-103">Configurer des sources de déploiement d’Azure App Service depuis vos applications Java</span><span class="sxs-lookup"><span data-stu-id="edab8-103">Configure Azure App Service deployment sources from your Java applications</span></span>

<span data-ttu-id="edab8-104">[Cet exemple](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) déploie un code pour quatre applications en un seul plan [Azure App Service](https://docs.microsoft.com/azure/app-service/), et chacune d’elles utilise une source de déploiement différente.</span><span class="sxs-lookup"><span data-stu-id="edab8-104">[This sample](https://github.com/Azure-Samples/compute-java-create-virtual-machines-across-regions-in-parallel) deploys code to four applications in a single [Azure App Service](https://docs.microsoft.com/azure/app-service/) plan, each using a different deployment source.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="edab8-105">Exécution de l'exemple</span><span class="sxs-lookup"><span data-stu-id="edab8-105">Run the sample</span></span>

<span data-ttu-id="edab8-106">Créez un [fichier d’authentification](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) et définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin d’accès complet au fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="edab8-106">Create an [authentication file](https://github.com/Azure/azure-sdk-for-java/blob/master/AUTH.md) and set an environment variable `AZURE_AUTH_LOCATION` with the full path to the file on your computer.</span></span> <span data-ttu-id="edab8-107">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="edab8-107">Then run:</span></span>

```
git clone https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps.git
cd app-service-java-configure-deployment-sources-for-web-apps
mvn clean compile exec:java
```

<span data-ttu-id="edab8-108">Affichez l’[exemple de code complet sur GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span><span class="sxs-lookup"><span data-stu-id="edab8-108">View the [complete sample code on GitHub](https://github.com/Azure-Samples/app-service-java-configure-deployment-sources-for-web-apps/blob/master/src/main/java/com/microsoft/azure/management/appservice/samples/ManageWebAppSourceControl.java).</span></span>

## <a name="authenticate-with-azure"></a><span data-ttu-id="edab8-109">S’authentifier avec Azure</span><span class="sxs-lookup"><span data-stu-id="edab8-109">Authenticate with Azure</span></span>

[!INCLUDE [auth-include](includes/java-auth-include.md)]

## <a name="create-a-app-service-app-running-apache-tomcat"></a><span data-ttu-id="edab8-110">Créer une application App Service qui exécute Apache Tomcat</span><span class="sxs-lookup"><span data-stu-id="edab8-110">Create a App Service app running Apache Tomcat</span></span>

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

<span data-ttu-id="edab8-111">`withJavaVersion()` et `withWebContainer()` configurent App Service de sorte qu’il traite les requêtes HTTP avec Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="edab8-111">`withJavaVersion()` and `withWebContainer()` configure App Service to serve HTTP requests using Tomcat 8.</span></span>

## <a name="deploy-a-java-application-using-ftp"></a><span data-ttu-id="edab8-112">Déployer une application Java à l’aide de FTP</span><span class="sxs-lookup"><span data-stu-id="edab8-112">Deploy a Java application using FTP</span></span>
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

<span data-ttu-id="edab8-113">Ce code charge un fichier WAR dans le répertoire `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="edab8-113">This code uploads a WAR file to the `/site/wwwroot/webapps` directory.</span></span> <span data-ttu-id="edab8-114">Tomcat déploie les fichiers WAR placés dans ce répertoire par défaut dans App Service.</span><span class="sxs-lookup"><span data-stu-id="edab8-114">Tomcat deploys WAR files placed in this directory by default in App Service.</span></span>

## <a name="deploy-a-java-application-from-a-local-git-repo"></a><span data-ttu-id="edab8-115">Déployer une application Java à partir d’un référentiel Git local</span><span class="sxs-lookup"><span data-stu-id="edab8-115">Deploy a Java application from a local Git repo</span></span>

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

<span data-ttu-id="edab8-116">Ce code utilise les bibliothèques [JGit](https://eclipse.org/jgit/) pour créer un référentiel Git dans le dossier `src/main/resources/azure-samples-appservice-helloworld`.</span><span class="sxs-lookup"><span data-stu-id="edab8-116">This code uses the [JGit](https://eclipse.org/jgit/) libraries to create a new Git repo in the `src/main/resources/azure-samples-appservice-helloworld` folder.</span></span> <span data-ttu-id="edab8-117">L’exemple ajoute ensuite tous les fichiers du dossier pour une validation initiale et envoie la validation dans Azure à l’aide des informations de déploiement Git présentes dans le `PublishingProfile` de l’application web.</span><span class="sxs-lookup"><span data-stu-id="edab8-117">The sample then adds all files in the folder to an initial commit and pushes the commit to Azure using Git deployment information from the webapp's `PublishingProfile`.</span></span> 

>[!NOTE]
> <span data-ttu-id="edab8-118">La disposition des fichiers dans le référentiel doit correspondre précisément à la façon dont vous souhaitez que les fichiers dans le répertoire `/site/wwwroot/` d’Azure App Service soient déployés.</span><span class="sxs-lookup"><span data-stu-id="edab8-118">The layout of the files in the repo must match exactly how you want the files deployed under the `/site/wwwroot/` directory in Azure App Service.</span></span>

## <a name="deploy-an-application-from-a-public-git-repo"></a><span data-ttu-id="edab8-119">Déployer une application à partir d’un référentiel Git public</span><span class="sxs-lookup"><span data-stu-id="edab8-119">Deploy an application from a public Git repo</span></span>

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

 <span data-ttu-id="edab8-120">Le runtime d’App Service génère et déploie automatiquement le projet .NET à l’aide du dernier code présent sur la branche `master` du référentiel.</span><span class="sxs-lookup"><span data-stu-id="edab8-120">The App Service runtime automatically builds and deploys the .NET project using the latest code on the `master` branch of the repo.</span></span>

## <a name="continuous-deployment-from-a-github-repo"></a><span data-ttu-id="edab8-121">Déploiement continu à partir d’un référentiel GitHub</span><span class="sxs-lookup"><span data-stu-id="edab8-121">Continuous deployment from a GitHub repo</span></span>

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

<span data-ttu-id="edab8-122">Les valeurs `username` et `reponame` sont utilisées dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="edab8-122">The `username` and `reponame` values are the ones used in GitHub.</span></span> <span data-ttu-id="edab8-123">[Créez un jeton d’accès personnel GitHub](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) avec autorisation de lecture du référentiel et transmettez-le à `withGitHubAccessToken`.</span><span class="sxs-lookup"><span data-stu-id="edab8-123">[Create a GitHub personal access token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/) with repo read permissions and pass it to `withGitHubAccessToken`.</span></span> 


## <a name="sample-explanation"></a><span data-ttu-id="edab8-124">Explication de l’exemple</span><span class="sxs-lookup"><span data-stu-id="edab8-124">Sample explanation</span></span>

<span data-ttu-id="edab8-125">L’exemple crée la première application à l’aide de Java 8 et Tomcat 8 en cours d’exécution dans un plan [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service créé récemment.</span><span class="sxs-lookup"><span data-stu-id="edab8-125">The sample creates the first application using Java 8 and Tomcat 8 running in a newly created [Standard](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview) App Service plan.</span></span> <span data-ttu-id="edab8-126">Le code convertit ensuite le fichier WAR en FTP à l’aide des informations présentes dans l’objet `PublishingProfile`, et Tomcat procède au déploiement.</span><span class="sxs-lookup"><span data-stu-id="edab8-126">The code then FTPs a WAR file using the information in the `PublishingProfile` object and Tomcat deploys it.</span></span>

<span data-ttu-id="edab8-127">La deuxième application se sert du même plan que la première, et est aussi configurée comme application Java 8/Tomcat 8.</span><span class="sxs-lookup"><span data-stu-id="edab8-127">The second application uses in the same plan as the first and is also configured as a Java 8/Tomcat 8 application.</span></span> <span data-ttu-id="edab8-128">Les bibliothèques JGit créent un référentiel Git dans un dossier qui contient une application web Java décompressée dans une structure de répertoires mappée sur App Service.</span><span class="sxs-lookup"><span data-stu-id="edab8-128">The JGit libraries create a new Git repository in a folder that contains an unpacked Java web application in a directory structure that maps to App Service.</span></span> <span data-ttu-id="edab8-129">Une nouvelle validation ajoute les fichiers du dossier dans le nouveau référentiel Git. Git envoie la validation à Azure avec une URL distante et un nom d’utilisateur/mot de passe fournis par le `PublishingProfile` de l’application web.</span><span class="sxs-lookup"><span data-stu-id="edab8-129">A new commit adds the files in the folder to the new Git repo, and Git pushes the commit to Azure with a remote URL and username/password provided by the webapp's `PublishingProfile`.</span></span>

<span data-ttu-id="edab8-130">La troisième application n’est pas configurée pour Java et Tomcat.</span><span class="sxs-lookup"><span data-stu-id="edab8-130">The third application is not configured for Java and Tomcat.</span></span> <span data-ttu-id="edab8-131">À la place, un exemple .NET dans un référentiel GitHub public est déployé directement depuis la source.</span><span class="sxs-lookup"><span data-stu-id="edab8-131">Instead, a .NET sample in a public GitHub repo is deployed directly from source.</span></span>

<span data-ttu-id="edab8-132">La quatrième application déploie le code dans la branche principale chaque fois que vous effectuez des modifications par push ou que vous fusionnez une demande de tirage (pull request) avec la branche principale du référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="edab8-132">The fourth application deploys the code in your master branch every time you push changes or merge a pull request into the GitHub repo's master branch.</span></span>

| <span data-ttu-id="edab8-133">Classe utilisée dans l’exemple</span><span class="sxs-lookup"><span data-stu-id="edab8-133">Class used in sample</span></span> | <span data-ttu-id="edab8-134">Notes</span><span class="sxs-lookup"><span data-stu-id="edab8-134">Notes</span></span>
|-------|-------|
| [<span data-ttu-id="edab8-135">WebApp</span><span class="sxs-lookup"><span data-stu-id="edab8-135">WebApp</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_app) | <span data-ttu-id="edab8-136">Créé à partir de la chaîne Fluent `azure.webApps().define()....create()`.</span><span class="sxs-lookup"><span data-stu-id="edab8-136">Created from the `azure.webApps().define()....create()` fluent chain.</span></span> <span data-ttu-id="edab8-137">Crée une application web App Service et toutes les ressources dont elle a besoin.</span><span class="sxs-lookup"><span data-stu-id="edab8-137">Creates a App Service web app and any resources needed for the app.</span></span> <span data-ttu-id="edab8-138">La plupart des méthodes interrogent l’objet pour obtenir des détails de configuration, mais les méthodes verbales comme `restart()` modifient l’état de l’application web.</span><span class="sxs-lookup"><span data-stu-id="edab8-138">Most methods query the object for configuration details, but verb methods like `restart()` change the state of the webapp.</span></span>
| [<span data-ttu-id="edab8-139">WebContainer</span><span class="sxs-lookup"><span data-stu-id="edab8-139">WebContainer</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._web_container) | <span data-ttu-id="edab8-140">Classe avec des champs publics statiques utilisée en tant que paramètres de l’élément `withWebContainer()` lors de la définition d’une application web exécutant un conteneur web Java.</span><span class="sxs-lookup"><span data-stu-id="edab8-140">Class with static public fields used as paramters to `withWebContainer()` when defining a WebApp running a Java webcontainer.</span></span> <span data-ttu-id="edab8-141">Dispose de choix pour les versions Jetty et Tomcat.</span><span class="sxs-lookup"><span data-stu-id="edab8-141">Has choices for both Jetty and Tomcat versions.</span></span>
| [<span data-ttu-id="edab8-142">PublishingProfile</span><span class="sxs-lookup"><span data-stu-id="edab8-142">PublishingProfile</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._publishing_profile) | <span data-ttu-id="edab8-143">Obtenu via un objet d’application web à l’aide de la méthode `getPublishingProfile()`.</span><span class="sxs-lookup"><span data-stu-id="edab8-143">Obtained through a WebApp object using the `getPublishingProfile()` method.</span></span> <span data-ttu-id="edab8-144">Contient des informations de déploiement FTP et Git, notamment le nom d’utilisateur et le mot de passe du déploiement (différentes de celles du compte Azure ou des informations d’identification du principal de service).</span><span class="sxs-lookup"><span data-stu-id="edab8-144">Contains FTP and Git deployment information, including deployment username and password (which is separate from Azure account or service principal credentials).</span></span>
| [<span data-ttu-id="edab8-145">AppServicePlan</span><span class="sxs-lookup"><span data-stu-id="edab8-145">AppServicePlan</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_plan) | <span data-ttu-id="edab8-146">Retourné par `azure.appServices().appServicePlans().getByResourceGroup()`.</span><span class="sxs-lookup"><span data-stu-id="edab8-146">Returned by `azure.appServices().appServicePlans().getByResourceGroup()`.</span></span> <span data-ttu-id="edab8-147">Les méthodes sont disponibles pour vérifier la capacité, le niveau et le nombre des applications web en cours d’exécution dans le plan.</span><span class="sxs-lookup"><span data-stu-id="edab8-147">Methods are availble to check the capacity, tier, and number of web apps running in the plan.</span></span>
| [<span data-ttu-id="edab8-148">AppServicePricingTier</span><span class="sxs-lookup"><span data-stu-id="edab8-148">AppServicePricingTier</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._app_service_pricing_tier) | <span data-ttu-id="edab8-149">Classe avec des champs publics statiques qui représentent les niveaux d’App Service.</span><span class="sxs-lookup"><span data-stu-id="edab8-149">Class with static public fields representing App Service tiers.</span></span> <span data-ttu-id="edab8-150">Permet de définir un niveau plan correspondant lors de la création d’applications avec `withPricingTier()` ou directement lors de la définition d’un plan via `azure.appServices().appServicePlans().define()`</span><span class="sxs-lookup"><span data-stu-id="edab8-150">Used to define a plan tier in-line during app creation with `withPricingTier()` or directly when defining a plan via `azure.appServices().appServicePlans().define()`</span></span>
| [<span data-ttu-id="edab8-151">JavaVersion</span><span class="sxs-lookup"><span data-stu-id="edab8-151">JavaVersion</span></span>](https://docs.microsoft.com/java/api/com.microsoft.azure.management.appservice._java_version) | <span data-ttu-id="edab8-152">Classe avec des champs publics statiques qui représentent les versions Java prises en charge par App Service.</span><span class="sxs-lookup"><span data-stu-id="edab8-152">Class with static public fields representing Java versions supported by App Service.</span></span> <span data-ttu-id="edab8-153">Utilisée avec `withJavaVersion()` pendant la chaîne `define()...create()` au moment de la création d’une application web.</span><span class="sxs-lookup"><span data-stu-id="edab8-153">Used with `withJavaVersion()` during the `define()...create()` chain when creating a new webapp.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edab8-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="edab8-154">Next steps</span></span>

[!INCLUDE [next-steps](includes/java-next-steps.md)]