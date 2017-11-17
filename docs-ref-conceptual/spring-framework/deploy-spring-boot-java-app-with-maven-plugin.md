---
title: "Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot sur Azure"
description: "Découvrez comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot dans Azure."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework, Maven
ms.assetid: 
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 32781b3ee923f4d64d4e1a11df73f077281eee40
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2017
---
# <a name="how-to-use-the-maven-plugin-for-azure-web-apps-to-deploy-a-spring-boot-app-to-azure"></a><span data-ttu-id="c2507-104">Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot sur Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-104">How to use the Maven Plugin for Azure Web Apps to deploy a Spring Boot app to Azure</span></span>

<span data-ttu-id="c2507-105">Le [plug-in Maven pour Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) pour [Apache Maven](http://maven.apache.org/) assure une intégration transparente d’Azure App Service dans les projets Maven et rationalise le processus pour permettre aux développeurs de déployer des applications web sur Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c2507-105">The [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines the process for developers to deploy web apps to Azure App Service.</span></span>

<span data-ttu-id="c2507-106">Cet article présente l’utilisation du plug-in Maven pour Azure Web Apps afin de déployer un exemple d’application Spring Boot sur Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="c2507-106">This article demonstrates using the Maven Plugin for Azure Web Apps to deploy a sample Spring Boot application to Azure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c2507-107">Le plug-in Maven pour Azure Web Apps est actuellement disponible en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="c2507-107">The Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="c2507-108">Pour l’instant, seule la publication FTP est prise en charge, mais des fonctionnalités supplémentaires sont envisagées pour le futur.</span><span class="sxs-lookup"><span data-stu-id="c2507-108">For now, only FTP publishing is supported, although additional features are planned for the future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="c2507-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c2507-109">Prerequisites</span></span>

<span data-ttu-id="c2507-110">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c2507-110">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="c2507-111">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="c2507-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c2507-112">[Azure CLI].</span><span class="sxs-lookup"><span data-stu-id="c2507-112">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c2507-113">Un [Java Development Kit (JDK)] à jour, version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c2507-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="c2507-114">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="c2507-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c2507-115">Un [client Git].</span><span class="sxs-lookup"><span data-stu-id="c2507-115">A [Git] client.</span></span>

## <a name="clone-the-sample-spring-boot-web-app"></a><span data-ttu-id="c2507-116">Cloner l’exemple d’application web Spring Boot</span><span class="sxs-lookup"><span data-stu-id="c2507-116">Clone the sample Spring Boot web app</span></span>

<span data-ttu-id="c2507-117">Dans cette section, vous clonez une application Spring Boot terminée et vous la testez localement.</span><span class="sxs-lookup"><span data-stu-id="c2507-117">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c2507-118">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-118">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c2507-119">- ou -</span><span class="sxs-lookup"><span data-stu-id="c2507-119">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c2507-120">Clonez l’exemple de projet [Spring Boot Getting Started] dans le répertoire que vous avez créé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-120">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="c2507-121">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-121">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="c2507-122">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-122">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c2507-123">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-123">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c2507-124">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="c2507-124">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="c2507-125">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="c2507-125">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c2507-126">Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="c2507-126">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="c2507-127">Créer un principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-127">Create an Azure service principal</span></span>

<span data-ttu-id="c2507-128">Dans cette section, vous créez un principal du service Azure utilisé par le plug-in Maven lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c2507-128">In this section, you create an Azure service principal that the Maven plugin uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="c2507-129">Ouvrez une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="c2507-129">Open a command prompt.</span></span>

1. <span data-ttu-id="c2507-130">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="c2507-130">Sign into your Azure account by using the Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="c2507-131">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="c2507-131">Follow the instructions to complete the sign-in process.</span></span>

1. <span data-ttu-id="c2507-132">Créez un principal du service Azure :</span><span class="sxs-lookup"><span data-stu-id="c2507-132">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="c2507-133">Où `uuuuuuuu` est le nom d’utilisateur et `pppppppp` est le mot de passe du principal du service.</span><span class="sxs-lookup"><span data-stu-id="c2507-133">Where `uuuuuuuu` is the user name and `pppppppp` is the password for the service principal.</span></span>

1. <span data-ttu-id="c2507-134">Azure répond avec un texte JSON similaire à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c2507-134">Azure responds with JSON that resembles the following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="c2507-135">Vous utiliserez les valeurs de cette réponse JSON lors de la configuration du plug-in Maven pour déployer votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c2507-135">You will use the values from this JSON response when you configure the Maven plugin to deploy your web app to Azure.</span></span> <span data-ttu-id="c2507-136">`aaaaaaaa`, `uuuuuuuu`, `pppppppp` et `tttttttt` sont des valeurs d’espace réservé qui sont utilisées dans cet exemple pour faciliter le mappage de ces valeurs avec leurs éléments respectifs lorsque vous configurerez votre fichier `settings.xml` Maven dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="c2507-136">The `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example to make it easier to map these values to their respective elements when you configure your Maven `settings.xml` file in the next section.</span></span>
   >
   >

## <a name="configure-maven-to-use-your-azure-service-principal"></a><span data-ttu-id="c2507-137">Configurer Maven pour utiliser votre principal du service Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-137">Configure Maven to use your Azure service principal</span></span>

<span data-ttu-id="c2507-138">Dans cette section, vous utilisez les valeurs de votre principal du service Azure pour configurer l’authentification utilisée par Maven lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c2507-138">In this section, you use the values from your Azure service principal to configure the authentication that Maven uses when deploying your web app to Azure.</span></span>

1. <span data-ttu-id="c2507-139">Ouvrez votre fichier `settings.xml` Maven dans un éditeur de texte ; ce fichier peut avoir un chemin d’accès similaire aux exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="c2507-139">Open your Maven `settings.xml` file in a text editor; this file might be in a path like the following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="c2507-140">Ajoutez les paramètres de votre principal du service Azure de la section précédente de ce didacticiel à la collection `<servers>` dans le fichier *settings.xml*. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-140">Add your Azure service principal settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="c2507-141">Où :</span><span class="sxs-lookup"><span data-stu-id="c2507-141">Where:</span></span>
   <span data-ttu-id="c2507-142">Élément</span><span class="sxs-lookup"><span data-stu-id="c2507-142">Element</span></span> | <span data-ttu-id="c2507-143">Description</span><span class="sxs-lookup"><span data-stu-id="c2507-143">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="c2507-144">Spécifie un nom unique que Maven utilise pour rechercher vos paramètres de sécurité lorsque vous déployez votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c2507-144">Specifies a unique name which Maven uses to look up your security settings when you deploy your web app to Azure.</span></span>
   `<client>` | <span data-ttu-id="c2507-145">Contient la valeur `appId` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="c2507-145">Contains the `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="c2507-146">Contient la valeur `tenant` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="c2507-146">Contains the `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="c2507-147">Contient la valeur `password` de votre principal du service.</span><span class="sxs-lookup"><span data-stu-id="c2507-147">Contains the `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="c2507-148">Définit l’environnement de cloud Azure cible, qui est `AZURE` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c2507-148">Defines the target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="c2507-149">(Une liste complète des environnements est disponible dans la documentation [Maven Plugin for Azure Web Apps])</span><span class="sxs-lookup"><span data-stu-id="c2507-149">(A full list of environments is available in the [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="c2507-150">Enregistrez et fermez le fichier *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="c2507-150">Save and close the *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-to-azure"></a><span data-ttu-id="c2507-151">FACULTATIF : Personnaliser votre fichier pom.xml avant de déployer votre application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-151">OPTIONAL: Customize your pom.xml before deploying your web app to Azure</span></span>

<span data-ttu-id="c2507-152">Ouvrez le fichier `pom.xml` de votre application Spring Boot dans un éditeur de texte et recherchez l’élément `<plugin>` pour `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="c2507-152">Open the `pom.xml` file for your Spring Boot application in a text editor, and then locate the `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="c2507-153">Cet élément doit ressembler à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c2507-153">This element should resemble the following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="c2507-154">Il existe plusieurs valeurs que vous pouvez modifier pour le plug-in Maven ; une description détaillée de chacun de ces éléments est disponible dans la documentation [Maven Plugin for Azure Web Apps] (Plug-in Maven pour Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="c2507-154">There are several values that you can modify for the Maven plugin, and a detailed description for each of these elements is available in the [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="c2507-155">Cela dit, il s’avère intéressant de souligner plusieurs valeurs dans cet article :</span><span class="sxs-lookup"><span data-stu-id="c2507-155">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="c2507-156">Élément</span><span class="sxs-lookup"><span data-stu-id="c2507-156">Element</span></span> | <span data-ttu-id="c2507-157">Description</span><span class="sxs-lookup"><span data-stu-id="c2507-157">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="c2507-158">Spécifie la version du [Maven Plugin for Azure Web Apps].</span><span class="sxs-lookup"><span data-stu-id="c2507-158">Specifies the version of the [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="c2507-159">Vous devez vérifier la version répertoriée dans le [référentiel Maven central](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) pour vous assurer que vous utilisez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c2507-159">You should check the version listed in the [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) to ensure that you are using the latest version.</span></span>
`<authentication>` | <span data-ttu-id="c2507-160">Spécifie les informations d’authentification pour Azure, qui dans cet exemple comportent un élément `<serverId>` contenant `azure-auth` ; Maven utilise cette valeur pour rechercher les valeurs du principal du service Azure dans votre fichier *settings.xml* Maven que vous avez défini dans une section précédente de cet article.</span><span class="sxs-lookup"><span data-stu-id="c2507-160">Specifies the authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value to look up the Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="c2507-161">Spécifie le groupe de ressources cible, qui est `maven-plugin` dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="c2507-161">Specifies the target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="c2507-162">Il est créé au cours du déploiement s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="c2507-162">The resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="c2507-163">Spécifie le nom cible de votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2507-163">Specifies the target name for your web app.</span></span> <span data-ttu-id="c2507-164">Dans cet exemple, le nom cible est `maven-web-app-${maven.build.timestamp}`, où le suffixe `${maven.build.timestamp}` est ajouté dans cet exemple pour éviter tout conflit.</span><span class="sxs-lookup"><span data-stu-id="c2507-164">In this example, the target name is `maven-web-app-${maven.build.timestamp}`, where the `${maven.build.timestamp}` suffix is appended in this example to avoid conflict.</span></span> <span data-ttu-id="c2507-165">(L’horodatage est facultatif ; vous pouvez spécifier n’importe quelle chaîne unique pour le nom de l’application.)</span><span class="sxs-lookup"><span data-stu-id="c2507-165">(The timestamp is optional; you can specify any unique string for the app name.)</span></span>
`<region>` | <span data-ttu-id="c2507-166">Spécifie la région cible, qui dans cet exemple est `westus`.</span><span class="sxs-lookup"><span data-stu-id="c2507-166">Specifies the target region, which in this example is `westus`.</span></span> <span data-ttu-id="c2507-167">(Une liste complète est disponible dans la documentation [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="c2507-167">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="c2507-168">Spécifie la version du runtime Java de votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2507-168">Specifies the Java runtime version for your web app.</span></span> <span data-ttu-id="c2507-169">(Une liste complète est disponible dans la documentation [Maven Plugin for Azure Web Apps].)</span><span class="sxs-lookup"><span data-stu-id="c2507-169">(A full list is in the [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="c2507-170">Spécifie le type de déploiement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2507-170">Specifies deployment type for your web app.</span></span> <span data-ttu-id="c2507-171">Pour l’instant, seul `ftp` est pris en charge, bien que la prise en charge d’autres types de déploiement soit en cours de développement.</span><span class="sxs-lookup"><span data-stu-id="c2507-171">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="c2507-172">Spécifie les ressources et les destinations cible utilisées par Maven lors du déploiement de votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c2507-172">Specifies resources and target destinations which Maven uses when deploying your web app to Azure.</span></span> <span data-ttu-id="c2507-173">Dans cet exemple, deux éléments `<resource>` indiquent que Maven va déployer le fichier JAR de votre application web et le fichier *web.config* du projet Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="c2507-173">In this example, two `<resource>` elements specify that Maven will deploy the JAR file for your web app and the *web.config* file from the Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-to-azure"></a><span data-ttu-id="c2507-174">Créer et déployer votre application web dans Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-174">Build and deploy your web app to Azure</span></span>

<span data-ttu-id="c2507-175">Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c2507-175">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="c2507-176">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c2507-176">To do so, use the following steps:</span></span>

1. <span data-ttu-id="c2507-177">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-177">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c2507-178">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="c2507-178">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c2507-179">Maven déploiera votre application web dans Azure. Si l’application web n’existe pas déjà, elle sera créée.</span><span class="sxs-lookup"><span data-stu-id="c2507-179">Maven will deploy your web app to Azure; if the web app does not already exist, it will be created.</span></span>

<span data-ttu-id="c2507-180">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="c2507-180">When your web has been deployed, you will be able to manage it by using the [Azure portal].</span></span>

* <span data-ttu-id="c2507-181">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="c2507-181">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="c2507-183">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="c2507-183">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="c2507-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c2507-185">Next steps</span></span>

<span data-ttu-id="c2507-186">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="c2507-186">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="c2507-187">[Maven Plugin for Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="c2507-187">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c2507-188">Se connecter à Azure à partir de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-188">Log in to Azure from the Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="c2507-189">Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot conteneurisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="c2507-189">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="c2507-190">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c2507-190">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="c2507-191">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="c2507-191">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure CLI]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven Plugin for Azure Web Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
