---
title: "Prise en main d’Azure pour Java à l’aide d’Eclipse"
description: "Prise en main des fonctions de base des bibliothèques Azure pour Java avec votre propre abonnement Azure."
keywords: "Azure, Java, SDK, API, s’authentifier, prise en main"
services: 
documentationcenter: java
author: roygara
manager: timlt
editor: 
ms.author: v-rogara
ms.date: 02/01/2018
ms.devlang: java
ms.prod: azure
ms.technology: azure
ms.topic: get-started-article
ms.service: multiple
ms.openlocfilehash: 7903b84f013fea07feee04419b1773f38494d4d0
ms.sourcegitcommit: 151aaa6ccc64d94ed67f03e846bab953bde15b4a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2018
---
# <a name="get-started-with-the-azure-libraries-using-eclipse"></a><span data-ttu-id="51193-104">Prise en main des blibliothèques Azure à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="51193-104">Get started with the Azure libraries using Eclipse</span></span>

<span data-ttu-id="51193-105">Ce guide vous présente la configuration d’un environnement de développement et l’utilisation des bibliothèques Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="51193-105">This guide walks you through setting up a development environment and using the Azure libraries for Java.</span></span> <span data-ttu-id="51193-106">Vous créez un principal de service afin de vous authentifier auprès d’Azure et exécutez un exemple de code qui génère et utilise les ressources Azure dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="51193-106">You'll create a service principal to authenticate with Azure and run some sample code that creates and uses Azure resources in your subscription.</span></span> <span data-ttu-id="51193-107">L’utilisation d’Eclipse pour le développement Java avec Azure est facultative.</span><span class="sxs-lookup"><span data-stu-id="51193-107">Using Eclipse is optional for Java development with Azure.</span></span> <span data-ttu-id="51193-108">Tout environnement de développement intégré affichant une intégration Maven est adapté.</span><span class="sxs-lookup"><span data-stu-id="51193-108">Any IDE that has Maven integration works.</span></span> <span data-ttu-id="51193-109">Sinon, vous pouvez exécuter votre code à partir de la ligne de commande à l’aide de Maven, si vous préférez n’utiliser aucun environnement de développement intégré.</span><span class="sxs-lookup"><span data-stu-id="51193-109">Alternatively, you can run your code from the commandline using Maven if you prefer not to use any IDE.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51193-110">configuration requise</span><span class="sxs-lookup"><span data-stu-id="51193-110">Prerequisites</span></span>

- <span data-ttu-id="51193-111">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="51193-111">An Azure account.</span></span> <span data-ttu-id="51193-112">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="51193-112">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>
- <span data-ttu-id="51193-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) ou [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="51193-113">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>
- <span data-ttu-id="51193-114">La dernière version stable d’[Eclipse](http://www.eclipse.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="51193-114">The latest stable version of [Eclipse](http://www.eclipse.org/downloads/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="51193-115">Configurer l’authentification</span><span class="sxs-lookup"><span data-stu-id="51193-115">Set up authentication</span></span>

<span data-ttu-id="51193-116">Votre application Java doit lire et créer des autorisations dans votre abonnement Azure pour exécuter l’exemple de code de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="51193-116">Your Java application needs read and create permissions in your Azure subscription to run the sample code in this tutorial.</span></span> <span data-ttu-id="51193-117">Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="51193-117">Create a service principal and configure your application to run with its credentials.</span></span> <span data-ttu-id="51193-118">Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.</span><span class="sxs-lookup"><span data-stu-id="51193-118">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="51193-119">[Créez un principal de service](/cli/azure/create-an-azure-service-principal-azure-cli) afin d’octroyer votre autorisation de code pour créer et mettre à jour les ressources de votre abonnement sans utiliser directement les informations d’identification de votre compte.</span><span class="sxs-lookup"><span data-stu-id="51193-119">[Create a service principal](/cli/azure/create-an-azure-service-principal-azure-cli) to grant your code permission to create and update resources in your subscription without using your account credentials directly.</span></span> <span data-ttu-id="51193-120">Assurez-vous de capturer la sortie.</span><span class="sxs-lookup"><span data-stu-id="51193-120">Make sure to capture the output.</span></span> <span data-ttu-id="51193-121">Fournissez un [mot de passe sécurisé](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) dans l’argument de mot de passe, en lieu et place de `MY_SECURE_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="51193-121">Provide a [secure password](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) in the password argument instead of `MY_SECURE_PASSWORD`.</span></span> <span data-ttu-id="51193-122">Votre mot de passe doit comporter entre 8 et 16 caractères et répondre à au moins 3 des 4 critères suivants :</span><span class="sxs-lookup"><span data-stu-id="51193-122">Your password must be 8 to 16 characters and match at least 3 out of the 4 following criteria:</span></span>

* <span data-ttu-id="51193-123">Il comprend des caractères minuscules</span><span class="sxs-lookup"><span data-stu-id="51193-123">Include lowercase characters</span></span>
* <span data-ttu-id="51193-124">Il comprend des caractères majuscules</span><span class="sxs-lookup"><span data-stu-id="51193-124">Include uppercase characters</span></span>
* <span data-ttu-id="51193-125">Il comprend des nombres</span><span class="sxs-lookup"><span data-stu-id="51193-125">Include numbers</span></span>
* <span data-ttu-id="51193-126">Il comprend l’un des symboles suivants : @ # $ % ^ & \* - _ !</span><span class="sxs-lookup"><span data-stu-id="51193-126">Include one of the following symbols: @ # $ % ^ & \* - _ !</span></span> <span data-ttu-id="51193-127">+ = [ ] { } | \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="51193-127">+ = [ ] { } | \ : ‘ , .</span></span> <span data-ttu-id="51193-128">?</span><span class="sxs-lookup"><span data-stu-id="51193-128">?</span></span> <span data-ttu-id="51193-129">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="51193-129">/ \` ~ “ ( ) ;</span></span>


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

<span data-ttu-id="51193-130">Qui vous fournit une réponse au format suivant :</span><span class="sxs-lookup"><span data-stu-id="51193-130">Which gives you a reply in the following format:</span></span>

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

<span data-ttu-id="51193-131">Ensuite, copiez les éléments suivants dans un fichier texte sur votre système :</span><span class="sxs-lookup"><span data-stu-id="51193-131">Next, copy the following into a text file on your system:</span></span>

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

<span data-ttu-id="51193-132">Remplacez les quatre valeurs du haut par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="51193-132">Replace the top four values with the following:</span></span>

- <span data-ttu-id="51193-133">abonnement : utilisez la valeur *id* de `az account show` dans Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="51193-133">subscription: use the *id* value from `az account show` in the Azure CLI 2.0.</span></span>
- <span data-ttu-id="51193-134">client : utilisez la valeur *appId* de la sortie d’un principal de service.</span><span class="sxs-lookup"><span data-stu-id="51193-134">client: use the *appId* value from the output taken from a service principal output.</span></span>
- <span data-ttu-id="51193-135">clé : utilisez la valeur *password* de la sortie du principal de service.</span><span class="sxs-lookup"><span data-stu-id="51193-135">key: use the *password* value from the service principal output.</span></span>
- <span data-ttu-id="51193-136">abonné : utilisez la valeur *tenant* de la sortie du principal de service.</span><span class="sxs-lookup"><span data-stu-id="51193-136">tenant: use the *tenant* value from the service principal output.</span></span>

<span data-ttu-id="51193-137">Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire.</span><span class="sxs-lookup"><span data-stu-id="51193-137">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="51193-138">Dans la mesure où vous pouvez utiliser ce fichier pour un code ultérieur, il est recommandé de le stocker à l’extérieur de l’application dans cet article.</span><span class="sxs-lookup"><span data-stu-id="51193-138">You may use this file for future code so it's recommended to store it somewhere external to the application in this article.</span></span>

<span data-ttu-id="51193-139">Définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin complet du fichier d’authentification dans l’interpréteur de commande.</span><span class="sxs-lookup"><span data-stu-id="51193-139">Set an environment variable `AZURE_AUTH_LOCATION` with the full path to the authentication file in your shell.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

<span data-ttu-id="51193-140">Si vous travaillez dans un environnement Windows, ajoutez la variable à vos propriétés système.</span><span class="sxs-lookup"><span data-stu-id="51193-140">If you're working in a windows environment, add the variable to your system properties.</span></span> <span data-ttu-id="51193-141">Ouvrez PowerShell, et après avoir remplacé la seconde variable par le chemin d’accès à votre fichier, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="51193-141">Open PowerShell and, after replacing the second variable with the path to your file, enter the following command:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\<fullpath>\azureauth.properties", "Machine")
```

## <a name="create-a-new-maven-project"></a><span data-ttu-id="51193-142">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="51193-142">Create a new Maven project</span></span>

> [!NOTE]
> <span data-ttu-id="51193-143">Ce guide utilise un outil de build Maven pour générer et exécuter l’exemple de code, mais d’autres outils de build tels que Gradle fonctionnent aussi avec les bibliothèques Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="51193-143">This guide uses Maven build tool to build and run the sample code, but other build tools such as Gradle also work with the Azure libraries for Java.</span></span> 

<span data-ttu-id="51193-144">Ouvrez Eclipse, sélectionnez **File** -> **New** (Fichier > Nouveau).</span><span class="sxs-lookup"><span data-stu-id="51193-144">Open Eclipse, select **File** -> **New**.</span></span> <span data-ttu-id="51193-145">Dans la nouvelle fenêtre qui s’affiche, ouvrez le dossier Maven, puis sélectionnez le projet Maven.</span><span class="sxs-lookup"><span data-stu-id="51193-145">In the new window that appears open the Maven folder then select Maven Project.</span></span> 

<span data-ttu-id="51193-146">Laissez les sélections par défaut sur l’écran suivant, puis sélectionnez **Next** (Suivant).</span><span class="sxs-lookup"><span data-stu-id="51193-146">Leave the selections on the next screen defaults, and select **Next**.</span></span> <span data-ttu-id="51193-147">Procédez de même pour les archétypes de cet écran.</span><span class="sxs-lookup"><span data-stu-id="51193-147">Do the same for this screen regarding archetypes.</span></span>

<span data-ttu-id="51193-148">Lorque vous arrivez sur l’écran vous demandant les éléments groupID, ArtifactID, etc. Saisissez « com.fabrikam » pour groupID et « AzureApp » pour artifactID.</span><span class="sxs-lookup"><span data-stu-id="51193-148">When you come to the screen asking for groupID, ArtifactID, etc. Enter "com.fabrikam" for the groupID and enter "AzureApp" for the artifactID.</span></span>

<span data-ttu-id="51193-149">Ouvrez maintenant le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="51193-149">Now, open the pom.xml file.</span></span> <span data-ttu-id="51193-150">Dans la base `dependencies`, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="51193-150">Inside the `dependencies` tag add the following code:</span></span>

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

<span data-ttu-id="51193-151">Maintenant, enregistrez le fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="51193-151">Now, save the pom.xml.</span></span> <span data-ttu-id="51193-152">Ce faisant, vous invitez Eclipse à télécharger l’ensemble des dépendances spécifiées.</span><span class="sxs-lookup"><span data-stu-id="51193-152">This prompts Eclipse to download all the specified dependencies.</span></span> <span data-ttu-id="51193-153">Cette opération peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="51193-153">This may take a moment.</span></span>
   
## <a name="install-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="51193-154">Installer le Kit de ressources Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="51193-154">Install the azure toolkit for Eclipse</span></span>

<span data-ttu-id="51193-155">Le [kit de ressources Azure](azure-toolkit-for-eclipse.md) est nécessaire si vous avez l’intention de déployer des applications web ou des API par programmation, cependant il n’est actuellement utilisé pour aucune autre opération de développement.</span><span class="sxs-lookup"><span data-stu-id="51193-155">The [Azure toolkit](azure-toolkit-for-eclipse.md) is necessary if you're going to be deploying web apps or APIs programmatically but is not currently used for any other kinds of development.</span></span> <span data-ttu-id="51193-156">Les instructions suivantes sont un résumé du processus d’installation.</span><span class="sxs-lookup"><span data-stu-id="51193-156">The following is a summary of the installation process.</span></span> <span data-ttu-id="51193-157">Pour une procédure détaillée, consultez la section [Installation du kit de ressources Azure pour Eclipse](azure-toolkit-for-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="51193-157">For detailed stpes, visit [Installing the Azure Toolkit for Eclipse](azure-toolkit-for-eclipse.md).</span></span>

<span data-ttu-id="51193-158">Accédez au menu **Help** (Aide), puis sélectionnez **Install New software** (Installer un nouveau logiciel).</span><span class="sxs-lookup"><span data-stu-id="51193-158">Select the **Help** menu and then select **Install New software**.</span></span>

<span data-ttu-id="51193-159">Dans le champ **Work with:** (Travailler avec :), saisissez `http://dl.microsoft.com/eclipse`, puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="51193-159">In the **Work with:** field enter `http://dl.microsoft.com/eclipse` and press enter.</span></span>

<span data-ttu-id="51193-160">Ensuite, cochez la case en regard de **Azure toolkit for Java** (Kit de ressources Azure pour Java), puis décochez la case **Contact all update sites during install to find required software** (Contacter l’ensemble des sites de mise à jour durant l’installation pour trouver le logiciel adapté).</span><span class="sxs-lookup"><span data-stu-id="51193-160">Then, select the checkbox next to **Azure toolkit for Java** and uncheck the checkbox for **Contact all update sites during install to find required software**.</span></span> <span data-ttu-id="51193-161">Ensuite, sélectionnez Next (Suivant).</span><span class="sxs-lookup"><span data-stu-id="51193-161">Then select next.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="51193-162">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="51193-162">Create a Linux virtual machine</span></span>

<span data-ttu-id="51193-163">Créez un fichier nommé `AzureApp.java` dans le répertoire `src/main/java` du projet et collez-y le bloc de code suivant.</span><span class="sxs-lookup"><span data-stu-id="51193-163">Create a new file named `AzureApp.java` in the project's `src/main/java` directory and paste in the following block of code.</span></span> <span data-ttu-id="51193-164">Mettez à jour les variables `userName` et `sshKey` avec des valeurs réelles pour votre machine.</span><span class="sxs-lookup"><span data-stu-id="51193-164">Update the `userName` and `sshKey` variables with real values for your machine.</span></span> <span data-ttu-id="51193-165">Le code crée une nouvelle machine virtuelle Linux avec le nom `testLinuxVM` dans un groupe de ressources `sampleResourceGroup` qui s’exécute dans la région Azure Est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="51193-165">The code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="51193-166">Pour créer un élément `sshkey`, ouvrez l’interpréteur de commande Azure, puis entrez `ssh-keygen -t rsa -b 2048`.</span><span class="sxs-lookup"><span data-stu-id="51193-166">In order to create an `sshkey`, open the azure cloud shell and enter `ssh-keygen -t rsa -b 2048`.</span></span> <span data-ttu-id="51193-167">Nommez le fichier, puis accédez au fichier .public pour obtenir la clé, que vous utilisez dans le code suivant ; copiez et collez le tout dans votre variable `sshKey`.</span><span class="sxs-lookup"><span data-stu-id="51193-167">Name the file and then access the .public file to get the key, which you use in the following code, copy and paste it all into your variable `sshKey`.</span></span>

```java
package com.fabrikam.AzureApp;

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.PricingTier;
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
import java.util.List;

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


<span data-ttu-id="51193-168">Des requêtes et des réponses REST apparaissent dans la console pendant que le kit de développement logiciel (SDK) effectue les appels sous-jacents à l’API REST d’Azure pour configurer la machine virtuelle et ses ressources.</span><span class="sxs-lookup"><span data-stu-id="51193-168">You see some REST requests and responses in the console as the SDK makes the underlying calls to the Azure REST API to configure the virtual machine and its resources.</span></span> <span data-ttu-id="51193-169">Lorsque le programme se termine, vérifiez la machine virtuelle de votre abonnement avec Azure CLI 2.0 :</span><span class="sxs-lookup"><span data-stu-id="51193-169">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="51193-170">Après avoir vérifié que le code a fonctionné, utilisez l’interface CLI pour supprimer la machine virtuelle et ses ressources.</span><span class="sxs-lookup"><span data-stu-id="51193-170">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="51193-171">Déployer une application web à partir d’un référentiel GitHub</span><span class="sxs-lookup"><span data-stu-id="51193-171">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="51193-172">Remplacez la méthode principale dans `AzureApp.java` par la méthode ci-dessous pour mettre à jour la variable `appName` vers une valeur unique avant d’exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="51193-172">Replace the main method in `AzureApp.java` with the one below, updating the `appName` variable to a unique value before running the code.</span></span> <span data-ttu-id="51193-173">Ce code déploie une application web à partir de la branche `master` d’un référentiel GitHub public vers une nouvelle [application web Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) s’exécutant au niveau tarifaire gratuit.</span><span class="sxs-lookup"><span data-stu-id="51193-173">This code deploys a web application from the `master` branch in a public GitHub repo into a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free pricing tier.</span></span>

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

<span data-ttu-id="51193-174">Exécutez le code comme précédemment avec Maven :</span><span class="sxs-lookup"><span data-stu-id="51193-174">Run the code as before using Maven:</span></span>

<span data-ttu-id="51193-175">Ouvrez un navigateur menant à l’application à l’aide de l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="51193-175">Open a browser pointed to the application using the CLI:</span></span>

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
<span data-ttu-id="51193-176">Supprimez l’application web et le plan de votre abonnement après vérification du déploiement.</span><span class="sxs-lookup"><span data-stu-id="51193-176">Remove the web app and plan from your subscription once you've verified the deployment.</span></span>

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a><span data-ttu-id="51193-177">Se connecter à une instance Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="51193-177">Connect to an Azure SQL database</span></span>

<span data-ttu-id="51193-178">Remplacez la méthode principale actuelle dans `AzureApp.java` par le code ci-dessous, et définissez une valeur réelle pour la variable `dbPassword`.</span><span class="sxs-lookup"><span data-stu-id="51193-178">Replace the current main method in `AzureApp.java` with the code below, setting a real value for the `dbPassword` variable.</span></span>
<span data-ttu-id="51193-179">Ce code crée une nouvelle base de données SQL avec une règle de pare-feu autorisant l’accès à distance, puis se connecte à l’aide du pilote JBDC de SQL Database.</span><span class="sxs-lookup"><span data-stu-id="51193-179">This code creates a new SQL database with a firewall rule allowing remote access,  and then connects to it using the SQL Database JBDC driver.</span></span> 

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
<span data-ttu-id="51193-180">Exécutez l’exemple depuis la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="51193-180">Run the sample from the command line:</span></span>

```
mvn clean compile exec:java
```

<span data-ttu-id="51193-181">Effacez ensuite les ressources à l’aide de l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="51193-181">Then clean up the resources using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="51193-182">Écrire un objet blob dans un nouveau compte de stockage</span><span class="sxs-lookup"><span data-stu-id="51193-182">Write a blob into a new storage account</span></span>

<span data-ttu-id="51193-183">Remplacez la méthode principale actuelle dans `AzureApp.java` par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="51193-183">Replace the current main method in `AzureApp.java` with the code below.</span></span> <span data-ttu-id="51193-184">Ce code crée un [compte de stockage Azure](https://docs.microsoft.com/azure/storage/storage-introduction), avant d’utiliser les bibliothèques de stockage Azure pour Java pour créer un fichier texte dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="51193-184">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Java to create a new text file in the cloud.</span></span>

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

            // create a storage container to hold the files
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

<span data-ttu-id="51193-185">Exécutez l’exemple depuis la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="51193-185">Run the sample from the command line:</span></span>

<span data-ttu-id="51193-186">Vous pouvez rechercher le fichier `helloazure.txt` dans votre compte de stockage via le portail Azure ou avec l’[Explorateur de stockage Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span><span class="sxs-lookup"><span data-stu-id="51193-186">You can browse for the `helloazure.txt` file in your storage account through the Azure portal or with [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).</span></span>

<span data-ttu-id="51193-187">Effacez le compte de stockage à l’aide de l’interface CLI :</span><span class="sxs-lookup"><span data-stu-id="51193-187">Clean up the storage account using the CLI:</span></span>

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="51193-188">Explorez d’autres exemples</span><span class="sxs-lookup"><span data-stu-id="51193-188">Explore more samples</span></span>

<span data-ttu-id="51193-189">Pour savoir comment utiliser les bibliothèques de gestion Azure pour Java afin de gérer les ressources et d’automatiser des tâches, consultez notre exemple de code pour les [machines virtuelles](../java-sdk-azure-virtual-machine-samples.md), [les applications web](../java-sdk-azure-web-apps-samples.md) et [SQL Database](../java-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="51193-189">To learn more about how to use the Azure management libraries for Java to manage resources and automate tasks, see our sample code for [virtual machines](../java-sdk-azure-virtual-machine-samples.md), [web apps](../java-sdk-azure-web-apps-samples.md) and [SQL database](../java-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference-and-release-notes"></a><span data-ttu-id="51193-190">Références et notes de version</span><span class="sxs-lookup"><span data-stu-id="51193-190">Reference and release notes</span></span>

<span data-ttu-id="51193-191">Il existe une [référence](http://docs.microsoft.com/java/api) pour tous les packages.</span><span class="sxs-lookup"><span data-stu-id="51193-191">A [reference](http://docs.microsoft.com/java/api) is available for all packages.</span></span>

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="51193-192">Obtenir de l’aide et donner son avis</span><span class="sxs-lookup"><span data-stu-id="51193-192">Get help and give feedback</span></span>

<span data-ttu-id="51193-193">Posez des questions à la communauté sur [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span><span class="sxs-lookup"><span data-stu-id="51193-193">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java).</span></span> <span data-ttu-id="51193-194">Signalez des bogues et des problèmes concernant les bibliothèques Azure pour Java sur le [projet GitHub](https://github.com/Azure/azure-sdk-for-java).</span><span class="sxs-lookup"><span data-stu-id="51193-194">Report bugs and open issues against the Azure libraries for Java on the [project GitHub](https://github.com/Azure/azure-sdk-for-java).</span></span>
