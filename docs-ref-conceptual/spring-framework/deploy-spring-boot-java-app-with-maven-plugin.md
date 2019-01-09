---
title: Déployer le fichier JAR d’une application Spring Boot sur le cloud avec Maven et Azure
description: Découvrez comment déployer une application Spring Boot sur le cloud à l’aide du plug-in Maven pour Azure Web App pour Linux.
services: app-service
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: brborges
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: app-service
ms.topic: article
ms.openlocfilehash: 950b360eb525b0c6b97daad0798c27ded0582b8b
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991343"
---
# <a name="deploy-a-spring-boot-jar-file-web-app-to-azure-app-service-on-linux"></a><span data-ttu-id="948f3-103">Déployer le fichier JAR d’une application web Spring Boot sur Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="948f3-103">Deploy a Spring Boot JAR file web app to Azure App Service on Linux</span></span>

<span data-ttu-id="948f3-104">Cet article présente l’utilisation du [plug-in Maven pour Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) afin de déployer un package d’application Java SE JAR sur [Azure App Service sur Linux](/azure/app-service/containers/).</span><span class="sxs-lookup"><span data-stu-id="948f3-104">This article demonstrates using the [Maven Plugin for Azure App Service Web Apps](/java/api/overview/azure/maven/azure-webapp-maven-plugin/readme) to deploy a Spring Boot application packaged as a Java SE JAR to [Azure App Service on Linux](/azure/app-service/containers/).</span></span> <span data-ttu-id="948f3-105">Choisissez le déploiement Java SE sur les [fichiers Tomcat et WAR](/azure/app-service/containers/quickstart-java) lorsque vous voulez consolider les dépendances de vos applications, ainsi que leur runtime et leur configuration dans un seul artefact déployable.</span><span class="sxs-lookup"><span data-stu-id="948f3-105">Choose Java SE deployment over [Tomcat and WAR files](/azure/app-service/containers/quickstart-java) when you want to consolidate your app's dependencies, runtime, and configuration into a single deployable artifact.</span></span>


<span data-ttu-id="948f3-106">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="948f3-106">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="948f3-107">Prérequis</span><span class="sxs-lookup"><span data-stu-id="948f3-107">Prerequisites</span></span>

<span data-ttu-id="948f3-108">Pour effectuer les étapes de ce didacticiel, les éléments suivants doivent être installés et configurés :</span><span class="sxs-lookup"><span data-stu-id="948f3-108">To complete the steps in this tutorial, you'll need to have the following installed and configured:</span></span>

* <span data-ttu-id="948f3-109">[Azure CLI](/cli/azure/), en local ou via [Azure Cloud Shell](https://shell.azure.com).</span><span class="sxs-lookup"><span data-stu-id="948f3-109">The [Azure CLI](/cli/azure/), either locally or through [Azure Cloud Shell](https://shell.azure.com).</span></span>
* <span data-ttu-id="948f3-110">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="948f3-110">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="948f3-111">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="948f3-111">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="948f3-112">Apache [Maven](https://maven.apache.org/), version 3.</span><span class="sxs-lookup"><span data-stu-id="948f3-112">Apache's [Maven](https://maven.apache.org/), Version 3).</span></span>
* <span data-ttu-id="948f3-113">Un client [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="948f3-113">A [Git](https://git-scm.com/downloads) client.</span></span>

## <a name="install-and-sign-in-to-azure-cli"></a><span data-ttu-id="948f3-114">Installer Azure CLI et se connecter</span><span class="sxs-lookup"><span data-stu-id="948f3-114">Install and sign in to Azure CLI</span></span>

<span data-ttu-id="948f3-115">La façon la plus simple et la plus rapide que le Plugin Maven déploie votre application Spring Boot est d’utiliser[Azure CLI](/cli/azure/).</span><span class="sxs-lookup"><span data-stu-id="948f3-115">The simplest and easiest way to get the Maven Plugin deploying your Spring Boot application is by using [Azure CLI](/cli/azure/).</span></span>

<span data-ttu-id="948f3-116">Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="948f3-116">Sign into your Azure account by using the Azure CLI:</span></span>
   
   ```shell
   az login
   ```
   
<span data-ttu-id="948f3-117">Suivez les instructions pour terminer le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="948f3-117">Follow the instructions to complete the sign-in process.</span></span>

## <a name="clone-the-sample-app"></a><span data-ttu-id="948f3-118">Clonage de l’exemple d’application</span><span class="sxs-lookup"><span data-stu-id="948f3-118">Clone the sample app</span></span>

<span data-ttu-id="948f3-119">Dans cette section, vous allez cloner une application Spring Boot terminée et la tester localement.</span><span class="sxs-lookup"><span data-stu-id="948f3-119">In this section, you will clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="948f3-120">Ouvrez une invite de commandes ou une fenêtre de terminal et créez un répertoire local pour y stocker votre application Spring Boot, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-120">Open a command prompt or terminal window and create a local directory to hold your Spring Boot application, and change to that directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="948f3-121">- ou -</span><span class="sxs-lookup"><span data-stu-id="948f3-121">-- or --</span></span>
   ```shell
   md ~/SpringBoot
   cd ~/SpringBoot
   ```

1. <span data-ttu-id="948f3-122">Clonez l’exemple de projet [Spring Boot Getting Started] dans le répertoire que vous avez créé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-122">Clone the [Spring Boot Getting Started] sample project into the directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/spring-guides/gs-spring-boot
   ```

1. <span data-ttu-id="948f3-123">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-123">Change directory to the completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="948f3-124">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-124">Build the JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="948f3-125">Lorsque l’application web a été créée, démarrez l’application web à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-125">When the web app has been created, start the web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="948f3-126">Testez l’application web en y accédant localement via un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="948f3-126">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="948f3-127">Par exemple, vous pouvez utiliser la commande suivante si curl est disponible :</span><span class="sxs-lookup"><span data-stu-id="948f3-127">For example, you could use the following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="948f3-128">Vous devriez voir le message suivant : **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="948f3-128">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="configure-maven-plugin-for-azure-app-service"></a><span data-ttu-id="948f3-129">Configurer le plug-in Maven pour Azure App Service</span><span class="sxs-lookup"><span data-stu-id="948f3-129">Configure Maven Plugin for Azure App Service</span></span>

<span data-ttu-id="948f3-130">Dans cette section, vous allez configurer le projet Spring Boot `pom.xml` pour que Maven puisse déployer l’application sur Azure App Service sur Linux.</span><span class="sxs-lookup"><span data-stu-id="948f3-130">In this section, you will configure the Spring Boot project `pom.xml` so that Maven can deploy the app to Azure App Service on Linux.</span></span>

1. <span data-ttu-id="948f3-131">Ouvrez `pom.xml` dans un éditeur de code.</span><span class="sxs-lookup"><span data-stu-id="948f3-131">Open `pom.xml` in a code editor.</span></span>

2. <span data-ttu-id="948f3-132">Dans la section `<build>` du fichier pom.xml, ajoutez l’entrée suivante `<plugin>` dans la balise `<plugins>`.</span><span class="sxs-lookup"><span data-stu-id="948f3-132">In the `<build>` section of the pom.xml, add the following `<plugin>` entry inside the `<plugins>` tag.</span></span>

   ```xml
   <plugin>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-webapp-maven-plugin</artifactId>
    <version>1.4.0</version>
    <configuration>
      <deploymentType>jar</deploymentType>

      <!-- configure app to run on port 80, required by App Service -->
      <appSettings>
        <property> 
          <name>JAVA_OPTS</name> 
          <value>-Dserver.port=80</value> 
        </property> 
      </appSettings>

      <!-- Web App information -->
      <resourceGroup>${RESOURCEGROUP_NAME}</resourceGroup>
      <appName>${WEBAPP_NAME}</appName>
      <region>${REGION}</region>  

      <!-- Java Runtime Stack for Web App on Linux-->
      <linuxRuntime>jre8</linuxRuntime>
    </configuration>
   </plugin>
   ```

3. <span data-ttu-id="948f3-133">Mettez à jour les espaces réservés suivants dans la configuration du plug-in :</span><span class="sxs-lookup"><span data-stu-id="948f3-133">Update the following placeholders in the plugin configuration:</span></span>

| <span data-ttu-id="948f3-134">Placeholder</span><span class="sxs-lookup"><span data-stu-id="948f3-134">Placeholder</span></span> | <span data-ttu-id="948f3-135">Description</span><span class="sxs-lookup"><span data-stu-id="948f3-135">Description</span></span> |
| ----------- | ----------- |
| `RESOURCEGROUP_NAME` | <span data-ttu-id="948f3-136">Nom du nouveau groupe de ressources dans lequel créer votre application web.</span><span class="sxs-lookup"><span data-stu-id="948f3-136">Name for the new resource group in which to create your web app.</span></span> <span data-ttu-id="948f3-137">En plaçant toutes les ressources d’une application dans un groupe, vous pouvez les gérer ensemble.</span><span class="sxs-lookup"><span data-stu-id="948f3-137">By putting all the resources for an app in a group, you can manage them together.</span></span> <span data-ttu-id="948f3-138">Par exemple, si vous supprimez le groupe de ressources, vous supprimez également toutes les ressources associées à l’application.</span><span class="sxs-lookup"><span data-stu-id="948f3-138">For example, deleting the resource group would delete all resources associated with the app.</span></span> <span data-ttu-id="948f3-139">Mettez à jour cette valeur avec un nouveau nom de groupe de ressources unique, par exemple, *TestResources*.</span><span class="sxs-lookup"><span data-stu-id="948f3-139">Update this value with a unique new resource group name, for example, *TestResources*.</span></span> <span data-ttu-id="948f3-140">Vous utiliserez ce nom de groupe de ressources pour nettoyer toutes les ressources Azure dans une section ultérieure.</span><span class="sxs-lookup"><span data-stu-id="948f3-140">You will use this resource group name to clean up all Azure resources in a later section.</span></span> |
| `WEBAPP_NAME` | <span data-ttu-id="948f3-141">Le nom d’application fera partie du nom d’hôte pour l’application web lors du déploiement vers Azure (WEBAPP_NAME.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="948f3-141">The app name will be part the host name for the web app when deployed to Azure (WEBAPP_NAME.azurewebsites.net).</span></span> <span data-ttu-id="948f3-142">Mettez à jour cette valeur avec un nom unique pour la nouvelle application web Azure, qui va héberger votre application Java, par exemple *contoso*.</span><span class="sxs-lookup"><span data-stu-id="948f3-142">Update this value with a unique name for the new Azure web app, which will host your Java app, for example *contoso*.</span></span> |
| `REGION` | <span data-ttu-id="948f3-143">Une région Azure où l’application web est hébergée, par exemple `westus2`.</span><span class="sxs-lookup"><span data-stu-id="948f3-143">An Azure region where the web app is hosted, for example `westus2`.</span></span> <span data-ttu-id="948f3-144">Vous pouvez obtenir une liste de régions à partir du Cloud Shell ou de l’interface CLI à l’aide de la commande `az account list-locations`.</span><span class="sxs-lookup"><span data-stu-id="948f3-144">You can get a list of regions from the Cloud Shell or CLI using the `az account list-locations` command.</span></span> |

<span data-ttu-id="948f3-145">Une liste complète de configuration est disponible dans les [références du plug-in Maven sur GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span><span class="sxs-lookup"><span data-stu-id="948f3-145">A full list of configuration options can be found in the [Maven plugin reference on GitHub](https://github.com/Microsoft/azure-maven-plugins/tree/develop/azure-webapp-maven-plugin).</span></span>

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="948f3-146">Déploiement de l’application dans Azure</span><span class="sxs-lookup"><span data-stu-id="948f3-146">Deploy the app to Azure</span></span>

<span data-ttu-id="948f3-147">Une fois que vous avez configuré tous les paramètres dans les sections précédentes de cet article, vous êtes prêt à déployer votre application web dans Azure.</span><span class="sxs-lookup"><span data-stu-id="948f3-147">Once you have configured all of the settings in the preceding sections of this article, you are ready to deploy your web app to Azure.</span></span> <span data-ttu-id="948f3-148">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="948f3-148">To do so, use the following steps:</span></span>

1. <span data-ttu-id="948f3-149">À partir de l’invite de commandes ou de la fenêtre de terminal que vous utilisiez précédemment, régénérez le fichier JAR à l’aide de Maven si vous avez apporté des modifications au fichier *pom.xml* ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-149">From the command prompt or terminal window that you were using earlier, rebuild the JAR file using Maven if you made any changes to the *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="948f3-150">Déployez votre application web dans Azure à l’aide de Maven ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="948f3-150">Deploy your web app to Azure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="948f3-151">Maven déploie votre application web dans Azure. Si l’application web ou le plan de l’application web n’existe pas déjà, il ou elle sera créé(e).</span><span class="sxs-lookup"><span data-stu-id="948f3-151">Maven will deploy your web app to Azure; if the web app or web app plan does not already exist, it will be created for you.</span></span>

<span data-ttu-id="948f3-152">Lorsque votre application web aura été déployée, vous serez en mesure de la gérer à l’aide du [portail Azure].</span><span class="sxs-lookup"><span data-stu-id="948f3-152">When your web has been deployed, you will be able to manage it through the [Azure portal].</span></span>

* <span data-ttu-id="948f3-153">Votre application web s’affichera dans **App Services** :</span><span class="sxs-lookup"><span data-stu-id="948f3-153">Your web app will be listed in **App Services**:</span></span>

   ![Application web répertoriée dans App Services dans le portail Azure][AP01]

* <span data-ttu-id="948f3-155">Et l’URL de votre application web sera répertoriée dans la **Vue d’ensemble** de votre application web :</span><span class="sxs-lookup"><span data-stu-id="948f3-155">And the URL for your web app will be listed in the **Overview** for your web app:</span></span>

   ![Détermination de l’URL de votre application web][AP02]

<span data-ttu-id="948f3-157">Vérifiez que le déploiement a été effectué en utilisant la même commande cURL qu’auparavant, en utilisant l’URL de votre application web du portail au lieu de `localhost`.</span><span class="sxs-lookup"><span data-stu-id="948f3-157">Verify that the deployment was successful by using the same cURL command as before, using your web app URL from the Portal instead of `localhost`.</span></span> <span data-ttu-id="948f3-158">Vous devriez voir le message suivant : **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="948f3-158">You should see the following message displayed: **Greetings from Spring Boot!**</span></span> 

## <a name="next-steps"></a><span data-ttu-id="948f3-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="948f3-159">Next steps</span></span>

<span data-ttu-id="948f3-160">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="948f3-160">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="948f3-161">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="948f3-161">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="948f3-162">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="948f3-162">Additional Resources</span></span>

<span data-ttu-id="948f3-163">Pour plus d’informations sur les différentes technologies présentées dans cet article, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="948f3-163">For more information about the various technologies discussed in this article, see the following articles:</span></span>

* <span data-ttu-id="948f3-164">[Plug-in Maven pour Azure Web Apps]</span><span class="sxs-lookup"><span data-stu-id="948f3-164">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="948f3-165">Comment utiliser le plug-in Maven pour Azure Web Apps afin de déployer une application Spring Boot conteneurisée dans Azure</span><span class="sxs-lookup"><span data-stu-id="948f3-165">How to use the Maven Plugin for Azure Web Apps to deploy a containerized Spring Boot app to Azure</span></span>](deploy-containerized-spring-boot-java-app-with-maven-plugin.md)

* [<span data-ttu-id="948f3-166">Créer un principal du service avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="948f3-166">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="948f3-167">Référence des paramètres Maven</span><span class="sxs-lookup"><span data-stu-id="948f3-167">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure Command-Line Interface (CLI)]: /cli/azure/overview
[Azure for Java Developers]: /java/azure/
[Portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Working with Azure DevOps and Java]: /azure/devops/
[Maven]: http://maven.apache.org/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/
[Plug-in Maven pour Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme
[Maven Plugin for Azure Web Apps]: /java/api/overview/azure/maven/azure-webapp-maven-plugin/readme

[Java Development Kit (JDK)]: https://aka.ms/azure-jdks
<!-- http://www.oracle.com/technetwork/java/javase/downloads/ -->

<!-- IMG List -->

[AP01]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP01.png
[AP02]: ./media/deploy-spring-boot-java-app-with-maven-plugin/AP02.png
