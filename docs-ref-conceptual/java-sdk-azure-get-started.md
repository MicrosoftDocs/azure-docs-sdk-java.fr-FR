---
title: "Prise en main des bibliothèques Azure pour Java"
description: "Découvrez comment créer des ressources cloud Azure et s’y connecter pour les utiliser dans vos applications Java."
keywords: "Azure, Java, SDK, API, s’authentifier, prise en main"
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 04/16/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.assetid: b1e10b79-f75e-4605-aecd-eed64873e2d3
ms.openlocfilehash: f069183c96cdc42d590d2e58a5a6a500be5ab69a
ms.sourcegitcommit: 720c2eaf66532d277015610ec375c71e934d9ee6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="get-started-with-cloud-development-using-the-azure-libraries-for-java"></a><span data-ttu-id="78344-104">Prise en main du développement cloud avec les bibliothèques Azure pour Java</span><span class="sxs-lookup"><span data-stu-id="78344-104">Get started with cloud development using the Azure libraries for Java</span></span>

<span data-ttu-id="78344-105">Ce guide vous présente la configuration d’un environnement pour le développement Azure dans Java.</span><span class="sxs-lookup"><span data-stu-id="78344-105">This guide walks you through setting up a development environment for Azure development in Java.</span></span> <span data-ttu-id="78344-106">Vous allez ensuite créer quelques ressources que vous allez connecter pour effectuer certaines tâches fondamentales, comme le chargement d’un fichier ou le déploiement d’une application web.</span><span class="sxs-lookup"><span data-stu-id="78344-106">You'll then create some Azure resources and connect them to to perform some basic tasks, like uploading a file or deploying a web application.</span></span> <span data-ttu-id="78344-107">Lorsque vous avez terminé, vous êtes prêt à utiliser les services Azure dans vos propres application Java.</span><span class="sxs-lookup"><span data-stu-id="78344-107">When you're done, you'll be ready to start using Azure services in your own Java applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78344-108">configuration requise</span><span class="sxs-lookup"><span data-stu-id="78344-108">Prerequisites</span></span>

- <span data-ttu-id="78344-109">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="78344-109">An Azure account.</span></span> <span data-ttu-id="78344-110">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="78344-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="78344-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) ou [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="78344-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="78344-112">[Java 8](https://www.azul.com/downloads/zulu/) (inclus dans Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="78344-112">[Java 8](https://www.azul.com/downloads/zulu/) (included in Azure Cloud Shell)</span></span>
- <span data-ttu-id="78344-113">[Maven 3](http://maven.apache.org/download.cgi) (inclus dans Azure Cloud Shell)</span><span class="sxs-lookup"><span data-stu-id="78344-113">[Maven 3](http://maven.apache.org/download.cgi) (included in Azure Cloud Shell)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="78344-114">Configurer l’authentification</span><span class="sxs-lookup"><span data-stu-id="78344-114">Set up authentication</span></span>

<span data-ttu-id="78344-115">Votre application Java doit lire et créer des autorisations dans votre abonnement Azure pour exécuter l’exemple de code de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78344-115">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="78344-116">Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="78344-116">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="78344-117">Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.</span><span class="sxs-lookup"><span data-stu-id="78344-117">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="78344-118">[Créez un principal de service à l’aide d’Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) et capturez la sortie.</span><span class="sxs-lookup"><span data-stu-id="78344-118">[Create a service principal using the Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli) and capture the output.</span></span> <span data-ttu-id="78344-119">Fournissez un [mot de passe sécurisé](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) dans l’argument de mot de passe, en lieu et place de `MY_SECURE_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="78344-119">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="78344-120">Votre mot de passe doit comporter entre 8 et 16 caractères et répondre à au moins 3 des 4 critères suivants :</span><span class="sxs-lookup"><span data-stu-id="78344-120">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="78344-121">Il comprend des caractères minuscules</span><span class="sxs-lookup"><span data-stu-id="78344-121">Include lowercase characters</span></span>
* <span data-ttu-id="78344-122">Il comprend des caractères majuscules</span><span class="sxs-lookup"><span data-stu-id="78344-122">Include uppercase characters</span></span>
* <span data-ttu-id="78344-123">Il comprend des nombres</span><span class="sxs-lookup"><span data-stu-id="78344-123">Include numbers</span></span>
* <span data-ttu-id="78344-124">Il comprend l’un des symboles suivants : @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="78344-124">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="78344-125">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="78344-125">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="78344-126">?</span><span class="sxs-lookup"><span data-stu-id="78344-126">?</span></span> <span data-ttu-id="78344-127">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="78344-127">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="78344-128">Qui vous fournit une réponse au format suivant :</span><span class="sxs-lookup"><span data-stu-id="78344-128">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="78344-129">Ensuite, copiez les éléments suivants dans un fichier texte sur votre système :</span><span class="sxs-lookup"><span data-stu-id="78344-129">Next, copy the following into a text file on your system:</span></span>

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

<span data-ttu-id="78344-130">Remplacez les quatre valeurs du haut par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="78344-130">Replace the top four values with the following:</span></span>

- <span data-ttu-id="78344-131">abonnement : utilisez la valeur *id* de `az account show` dans Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="78344-131">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="78344-132">client : utilisez la valeur *appId* de la sortie d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="78344-132">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="78344-133">clé : utilisez la valeur *password* de la sortie du principal de service.</span><span class="sxs-lookup"><span data-stu-id="78344-133">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="78344-134">abonné : utilisez la valeur *tenant* de la sortie du principal de service.</span><span class="sxs-lookup"><span data-stu-id="78344-134">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="78344-135">Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire.</span><span class="sxs-lookup"><span data-stu-id="78344-135">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="78344-136">Dans la mesure où vous pouvez utiliser ce fichier pour un code ultérieur, il est recommandé de le stocker à l’extérieur de l’application dans cet article.</span><span class="sxs-lookup"><span data-stu-id="78344-136">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="78344-137">Définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin complet du fichier d’authentification dans l’interpréteur de commande.</span><span class="sxs-lookup"><span data-stu-id="78344-137">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>   

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="78344-138">Si vous travaillez dans un environnement Windows, ajoutez la variable à vos propriétés système.</span><span class="sxs-lookup"><span data-stu-id="78344-138">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="78344-139">Ouvrez une fenêtre PowerShell disposant de privilèges d’administrateur et, après avoir remplacé la seconde variable par le chemin d’accès à votre fichier, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="78344-139">Open a PowerShell window with administrator privledges and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
setx AZURE_AUTH_LOCATION "C:\<fullpath>\azureauth.properties" /m
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="78344-140">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="78344-140">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="78344-141">Ce guide utilise un outil de build Maven pour générer et exécuter l’exemple de code, mais d’autres outils de build tels que Gradle fonctionnent aussi avec les bibliothèques Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="78344-141">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="78344-142">Créez un projet Maven à partir de la ligne de commande dans un nouveau répertoire sur votre système :</span><span class="sxs-lookup"><span data-stu-id="78344-142">Create a Maven project from the command line in a new directory on your system:</span></span>

```
mkdir java-azure-test
cd java-azure-test
mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=AzureApp  \ 
-DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

<span data-ttu-id="78344-143">Cette opération crée un projet de base Maven sous le dossier `testAzureApp`.</span><span class="sxs-lookup"><span data-stu-id="78344-143">This creates a basic Maven project under the `testAzureApp` folder.</span></span> <span data-ttu-id="78344-144">Ajoutez les entrées suivantes dans le fichier `pom.xml` du projet pour importer les bibliothèques utilisées dans l’exemple de code de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78344-144">Add the following entries into the project `pom.xml` to import the libraries used in the sample code in this tutorial.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
```

<span data-ttu-id="78344-145">Ajoutez une entrée `build` sous l’élément `project` de niveau supérieur pour utiliser l’exécutable [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) et exécuter l’exemple :</span><span class="sxs-lookup"><span data-stu-id="78344-145">Add a `build` entry under the top-level `project` element to use the [maven-exec-plugin](http://www.mojohaus.org/exec-maven-plugin/) to run the samples:</span></span>

```XML
<build>
    <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.AzureApp</mainClass>
            </configuration>
        </plugin>
    </plugins>
</build>
 ```
   
## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="78344-146">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="78344-146">Create a Linux virtual machine</span></span>

<span data-ttu-id="78344-147">Créez un fichier nommé `AzureApp.java` dans le répertoire `src/main/java/com/fabirkam` du projet et collez-y le bloc de code suivant.</span><span class="sxs-lookup"><span data-stu-id="78344-147">Create a new file named `AzureApp.java` in the project's `src/main/java/com/fabirkam` directory and paste in the following block of code.</span></span> <span data-ttu-id="78344-148">Mettez à jour les variables `userName` et `sshKey` avec des valeurs réelles pour votre machine.</span><span class="sxs-lookup"><span data-stu-id="78344-148">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="78344-149">Le code crée une nouvelle machine virtuelle Linux avec le nom `testLinuxVM` dans un groupe de ressources `sampleResourceGroup` qui s’exécute dans la région Azure Est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="78344-149">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

```java
package com.fabrikam;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```

<span data-ttu-id="78344-150">Exécutez l’exemple depuis la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="78344-150">Run the sample from the command line:</span></span>

```
mvn compile exec:java
```

<span data-ttu-id="78344-151">Des requêtes et des réponses REST apparaissent dans la console pendant que le kit de développement logiciel (SDK) effectue les appels sous-jacents à l’API REST d’Azure pour configurer la machine virtuelle et ses ressources.</span><span class="sxs-lookup"><span data-stu-id="78344-151">You'll see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="78344-152">Lorsque le programme se termine, vérifiez la machine virtuelle de votre abonnement avec Azure CLI 2.0 :</span><span class="sxs-lookup"><span data-stu-id="78344-152">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="78344-153">Après avoir vérifié que le code a fonctionné, utilisez l’interface CLI pour supprimer la machine virtuelle et ses ressources.</span><span class="sxs-lookup"><span data-stu-id="78344-153">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="78344-154">Déployer une application web à partir d’un référentiel GitHub</span><span class="sxs-lookup"><span data-stu-id="78344-154">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="78344-155">Remplacez la méthode principale dans `AzureApp.java` par la méthode ci-dessous pour mettre à jour la variable `appName` vers une valeur unique avant d’exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="78344-155">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="78344-156">Ce code déploie une application web à partir de la branche `master` d’un référentiel GitHub public vers une nouvelle [application web Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) s’exécutant au niveau tarifaire gratuit.</span><span class="sxs-lookup"><span data-stu-id="78344-156">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

<span data-ttu-id="78344-157">Exécutez le code comme précédemment avec Maven :</span><span class="sxs-lookup"><span data-stu-id="78344-157">Run the code as before using Maven:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="78344-158">Ouvrez un navigateur menant à l’application à l’aide de l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="78344-158">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="78344-159">Supprimez l’application web et le plan de votre abonnement après vérification du déploiement.</span><span class="sxs-lookup"><span data-stu-id="78344-159">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="78344-160">Se connecter à une instance Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="78344-160">Connect to an Azure SQL database</span></span>

<span data-ttu-id="78344-161">Remplacez la méthode principale actuelle dans `AzureApp.java` par le code ci-dessous, et définissez une valeur réelle pour la variable `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="78344-161">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="78344-162">Ce code crée une nouvelle base de données SQL avec une règle de pare-feu autorisant l’accès à distance, puis se connecte à l’aide du pilote JBDC de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="78344-162">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
<span data-ttu-id="78344-163">Exécutez l’exemple depuis la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="78344-163">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="78344-164">Effacez ensuite les ressources à l’aide de l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="78344-164">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="78344-165">Écrire un objet blob dans un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="78344-165">Write a blob into a new storage account</span></span>

<span data-ttu-id="78344-166">Remplacez la méthode principale actuelle dans `AzureApp.java` par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="78344-166">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="78344-167">Ce code crée un [compte de stockage Azure](https://docs.microsoft.com/azure/storage/storage-introduction), avant d’utiliser les bibliothèques de stockage Azure pour Java pour créer un fichier texte dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="78344-167">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

```java
public static void main(String[] args) {

    try {

        // use the properties file with the service principal information to authenticate
        // change the name of the environment variable if you used a different name in the previous step
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
                .withLogLevel(LogLevel.BASIC)
                .authenticate(credFile)
                .withDefaultSubscription();

        // create a new storage account
        String storageAccountName = SdkContext.randomResourceName("st",8);
        StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleStorageResourceGroup")
                    .create();

        // create a storage container to hold the file
        List<StorageAccountKey> keys = storage.getKeys();
        final String storageConnection = "DefaultEndpointsProtocol=https;"
                + "AccountName=" + storage.name()
                + ";AccountKey=" + keys.get(0).value()
                + ";EndpointSuffix=core.windows.net";

        CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
        CloudBlobClient serviceClient = account.createCloudBlobClient();

        // Container name must be lower case.
        CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
        container.createIfNotExists();

        // Make the container public
        BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
        containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
        container.uploadPermissions(containerPermissions);

        // write a blob to the container
        CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
        blob.uploadText("hello Azure");

    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
    }
}
```

<span data-ttu-id="78344-168">Exécutez l’exemple depuis la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="78344-168">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="78344-169">Vous pouvez rechercher le fichier `helloazure.txt` dans votre compte de stockage via le portail Azure ou avec l’[Explorateur de stockage Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="78344-169">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="78344-170">Effacez le compte de stockage à l’aide de l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="78344-170">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="78344-171">Explorez d’autres exemples</span><span class="sxs-lookup"><span data-stu-id="78344-171">Explore more samples</span></span>

<span data-ttu-id="78344-172">Pour savoir comment utiliser les bibliothèques de gestion Azure pour Java afin de gérer les ressources et d’automatiser des tâches, consultez notre exemple de code pour les [machines virtuelles](java-sdk-azure-virtual-machine-samples.md), [les applications web](java-sdk-azure-web-apps-samples.md) et [SQL Database](java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="78344-172">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](java-sdk-azure-virtual-machine-samples.md), [web apps](java-sdk-azure-web-apps-samples.md) and [SQL database](java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="78344-173">Références et notes de version</span><span class="sxs-lookup"><span data-stu-id="78344-173">Reference and release notes</span></span>

<span data-ttu-id="78344-174">Il existe une [référence](http://docs.microsoft.com/java/api) pour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="78344-174">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="78344-175">Obtenir de l’aide et donner son avis</span><span class="sxs-lookup"><span data-stu-id="78344-175">Get help and give feedback</span></span>

<span data-ttu-id="78344-176">Posez des questions à la communauté sur [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="78344-176">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="78344-177">Signalez des bogues et des problèmes concernant les bibliothèques Azure pour Java sur le [projet GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="78344-177">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
