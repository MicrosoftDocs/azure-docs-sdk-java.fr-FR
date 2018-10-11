---
title: Déployer une application Spring Boot sur le cloud avec Azure App Service
description: Ce didacticiel guide les développeurs à travers les étapes de déploiement de l’application web Spring Boot Getting Started sur le cloud à l’aide d’Azure App Service.
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: asirveda;robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: adf779e2ba6ca73ea3a2406613f9622cc9ecbf99
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893160"
---
# <a name="deploy-a-spring-boot-application-to-the-cloud-with-azure-app-service"></a><span data-ttu-id="f6b6b-103">Déployer une application Spring Boot sur le cloud avec Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f6b6b-103">Deploy a Spring Boot application to the cloud with Azure App Service</span></span>

<span data-ttu-id="f6b6b-104">Ce didacticiel vous montre comment créer l’exemple d’application web [Spring Boot] Getting Started et la déployer sur [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-104">This tutorial will walk you though creating a sample [Spring Boot] Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f6b6b-105">Prérequis</span><span class="sxs-lookup"><span data-stu-id="f6b6b-105">Prerequisites</span></span>

<span data-ttu-id="f6b6b-106">Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-106">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="f6b6b-107">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-107">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="f6b6b-108">Un [JDK (Java Developer Kit)] à jour.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-108">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="f6b6b-109">L’outil de génération [Maven] (version 3) d’Apache.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-109">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="f6b6b-110">Un client [Git].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-110">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="f6b6b-111">Créer l’application web Spring Boot Getting Started</span><span class="sxs-lookup"><span data-stu-id="f6b6b-111">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="f6b6b-112">La procédure suivante vous guide à travers les étapes nécessaires pour créer une application web Spring Boot simple et pour la tester localement.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-112">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="f6b6b-113">Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-113">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="f6b6b-114">- ou -</span><span class="sxs-lookup"><span data-stu-id="f6b6b-114">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="f6b6b-115">Clonez l’exemple de projet [Spring Boot Getting Started] dans le répertoire que vous venez de créer. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-115">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="f6b6b-116">Accédez au répertoire du projet terminé. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-116">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="f6b6b-117">Générez le fichier JAR en utilisant Maven. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-117">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="f6b6b-118">Une fois que l’application web a été créée, accédez au répertoire du fichier JAR et démarrez l’application web. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-118">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="f6b6b-119">Testez l’application web en accédant à http://localhost:8080 avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-119">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="f6b6b-120">Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="f6b6b-120">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Parcourir l’exemple d’application][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="f6b6b-122">Créer une application web Azure à utiliser avec Java</span><span class="sxs-lookup"><span data-stu-id="f6b6b-122">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="f6b6b-123">La procédure suivante vous guide à travers les étapes pour créer une application web Azure, configurer les paramètres nécessaires pour Java et configurer vos informations d’identification FTP.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-123">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="f6b6b-124">Accédez au [portail Azure] et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-124">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="f6b6b-125">Une fois que vous êtes connecté à votre compte sur le portail Azure, cliquez sur l’icône du menu pour **App Services** :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-125">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Portail Azure][AZ01]

1. <span data-ttu-id="f6b6b-127">Quand la page **App Services** est affichée, cliquez sur **+ Ajouter** pour créer un nouvel App Service.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-127">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Créer un App Service][AZ02]

1. <span data-ttu-id="f6b6b-129">Quand la liste des modèles d’application web s’affiche, cliquez sur le lien pour l’application web Microsoft de base.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-129">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Modèles d’application web][AZ03]

1. <span data-ttu-id="f6b6b-131">Quand la page d’informations pour le modèle d’application web s’affiche, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-131">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Créer une application web][AZ04]

1. <span data-ttu-id="f6b6b-133">Indiquez un nom unique pour votre application web et spécifiez les éventuels paramètres supplémentaires, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-133">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Créer les paramètres d’une application web][AZ05]

1. <span data-ttu-id="f6b6b-135">Une fois que votre application web a été créée, cliquez sur l’icône du menu **App Services** puis cliquez sur votre application web nouvellement créée :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-135">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Répertorier les applications web][AZ06]

1. <span data-ttu-id="f6b6b-137">Quand votre application web s’affiche, spécifiez la version de Java en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-137">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="f6b6b-138">a.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-138">a.</span></span> <span data-ttu-id="f6b6b-139">Cliquez sur l’élément de menu **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-139">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="f6b6b-140">b.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-140">b.</span></span> <span data-ttu-id="f6b6b-141">Choisissez **Java 8** pour la version de Java.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-141">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="f6b6b-142">c.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-142">c.</span></span> <span data-ttu-id="f6b6b-143">Choisissez **La plus récente** pour la version mineure de Java.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-143">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="f6b6b-144">d.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-144">d.</span></span> <span data-ttu-id="f6b6b-145">Choisissez **Tomcat 8.5 la plus récente** pour le conteneur web.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-145">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="f6b6b-146">(Ce conteneur ne sera en fait pas utilisé. Azure utilisera le conteneur de votre application Spring Boot.)</span><span class="sxs-lookup"><span data-stu-id="f6b6b-146">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="f6b6b-147">e.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-147">e.</span></span> <span data-ttu-id="f6b6b-148">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-148">Click **Save**.</span></span>

   ![Paramètres de l’application][AZ07]

1. <span data-ttu-id="f6b6b-150">Spécifiez vos informations d’identification de déploiement FTP en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-150">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="f6b6b-151">a.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-151">a.</span></span> <span data-ttu-id="f6b6b-152">Cliquez sur l’élément de menu **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-152">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="f6b6b-153">b.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-153">b.</span></span> <span data-ttu-id="f6b6b-154">Spécifiez votre nom d’utilisateur et votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-154">Specify your username and password.</span></span>

   <span data-ttu-id="f6b6b-155">c.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-155">c.</span></span> <span data-ttu-id="f6b6b-156">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-156">Click **Save**.</span></span>

   ![Spécifier les informations d’identification de déploiement][AZ08]

1. <span data-ttu-id="f6b6b-158">Récupérez vos informations de connexion FTP à l’aide de la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-158">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="f6b6b-159">a.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-159">a.</span></span> <span data-ttu-id="f6b6b-160">Cliquez sur l’élément de menu **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-160">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="f6b6b-161">b.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-161">b.</span></span> <span data-ttu-id="f6b6b-162">Copiez votre nom d’utilisateur FTP complet et l’URL, et enregistrez-les pour la section suivante de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-162">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL et informations d’identification FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="f6b6b-164">Déployer votre application web Spring Boot sur Azure</span><span class="sxs-lookup"><span data-stu-id="f6b6b-164">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="f6b6b-165">La procédure suivante vous guide à travers les étapes pour déployer votre application web Spring Boot sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-165">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="f6b6b-166">Ouvrez un éditeur de texte, comme le Bloc-notes Windows, et collez le texte suivant dans un nouveau document, puis enregistrez le fichier sous *web.config* :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-166">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="f6b6b-167">Après avoir enregistré le fichier *web.config* sur votre système de fichiers, connectez-vous à votre application web via FTP en utilisant l’URL, le nom d’utilisateur et le mot de passe de la section précédente de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-167">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="f6b6b-168">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="f6b6b-168">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="f6b6b-169">Passez du répertoire distant au dossier racine de votre application web, (qui se trouve dans */site/wwwroot*), puis copiez le fichier JAR de votre application Spring Boot et le *web.config* créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-169">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="f6b6b-170">Par exemple : </span><span class="sxs-lookup"><span data-stu-id="f6b6b-170">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="f6b6b-171">Après avoir déployé vos fichiers JAR et *web.config* sur votre application web, vous devez redémarrer votre application web en utilisant le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-171">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![Redémarrer votre application web][AZ10]

1. <span data-ttu-id="f6b6b-173">Testez l’application web en accédant à l’URL de votre application web avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="f6b6b-174">Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**</span><span class="sxs-lookup"><span data-stu-id="f6b6b-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Parcourir l’exemple d’application][SB02]

## <a name="next-steps"></a><span data-ttu-id="f6b6b-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6b6b-176">Next steps</span></span>

<span data-ttu-id="f6b6b-177">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f6b6b-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="f6b6b-178">Déployer une application Spring Boot sur Linux dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f6b6b-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-linux.md)

* [<span data-ttu-id="f6b6b-179">Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f6b6b-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="f6b6b-180">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-180">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="f6b6b-181">Pour plus d’informations sur le déploiement d’applications web sur Azure avec FTP, consultez [Déployer votre application sur Azure App Service avec FTP/S].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="f6b6b-182">Pour plus d’informations sur l’exemple de projet Spring Boot, consultez [Spring Boot Getting Started].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="f6b6b-183">Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="f6b6b-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="f6b6b-184">Pour plus d’informations sur la configuration de paramètres supplémentaires pour votre application web, consultez [Configurer des applications web dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="f6b6b-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Portail Azure]: https://portal.azure.com/
[Azure portal]: https://portal.azure.com/
[Configurer des applications web dans Azure App Service]: /azure/app-service/web-sites-configure
[Configure web apps in Azure App Service]: /azure/app-service/web-sites-configure
[Déployer votre application sur Azure App Service avec FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
