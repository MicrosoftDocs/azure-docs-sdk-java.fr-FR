---
title: Guide pratique pour configurer une application Spring Boot Initializer pour utiliser le Cache Redis
description: "Découvrez comment configurer une application Spring Boot créée avec Spring Boot Initializr pour utiliser le Cache Redis Azure."
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: cache
ms.workload: na
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: e46a90413321845cb94d72fff893e42aa2353491
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-configure-a-spring-boot-initializer-app-to-use-redis-cache"></a><span data-ttu-id="96a90-103">Guide pratique pour configurer une application Spring Boot Initializer pour utiliser le Cache Redis</span><span class="sxs-lookup"><span data-stu-id="96a90-103">How to configure a Spring Boot Initializer app to use Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="96a90-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="96a90-104">Overview</span></span>

<span data-ttu-id="96a90-105">Cet article explique comment créer un cache Redis par le biais du portail Azure, utiliser **[Spring Initializr]** pour créer une application personnalisée, puis créer une application web Java qui stocke et récupère des données à l’aide de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="96a90-105">This article walks you through creating a Redis cache using the Azure portal, then using the **[Spring Initializr]** to create a custom application, and then creating a Java web application that stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96a90-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="96a90-106">Prerequisites</span></span>

<span data-ttu-id="96a90-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="96a90-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="96a90-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="96a90-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="96a90-109">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="96a90-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="96a90-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="96a90-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="96a90-111">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="96a90-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="96a90-112">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="96a90-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="96a90-113">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="96a90-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Options de base de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="96a90-115">Spring Initializr utilisera les noms de **Groupe** et d’**Artefact** pour créer le nom du package ; par exemple : *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="96a90-115">The Spring Initializr will use the **Group** and **Aritifact** names to create the package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="96a90-116">Faites défiler jusqu’à la section**Web** et cochez la case **Web**, faites défiler jusqu’à la section **NoSQL** et cochez la case **Redis**, puis faites défiler jusqu’au bas de la page et cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="96a90-116">Scroll down to the **Web** section and check the box for **Web**, then scroll down to the **NoSQL** section and check the box for **Redis**, then scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Options complètes de Spring Initializr][SI02]

1. <span data-ttu-id="96a90-118">À l’invite, téléchargez le projet vers un emplacement sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="96a90-118">When prompted, download the project to a path on your local computer.</span></span>

   ![Télécharger un projet Spring Boot personnalisé][SI03]

1. <span data-ttu-id="96a90-120">Une fois que vous avez extrait les fichiers sur votre système local, votre application Spring Boot personnalisée est prête à être modifiée.</span><span class="sxs-lookup"><span data-stu-id="96a90-120">After you have extracted the files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Fichiers de projet Spring Boot personnalisé][SI04]

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="96a90-122">Créer un Cache Redis sur Azure</span><span class="sxs-lookup"><span data-stu-id="96a90-122">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="96a90-123">Accédez au portail Azure à l’adresse <https://portal.azure.com/> et cliquez sur l’élément **+Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="96a90-123">Browse to the Azure portal at <https://portal.azure.com/> and click the item for **+New**.</span></span>

   ![Portail Azure][AZ01]

1. <span data-ttu-id="96a90-125">Cliquez sur **Base de données**, puis sur **Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="96a90-125">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Portail Azure][AZ02]

1. <span data-ttu-id="96a90-127">Dans la page **Nouveau cache Redis**, spécifiez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="96a90-127">On the **New Redis Cache** page, specify the following information:</span></span>

   * <span data-ttu-id="96a90-128">Entrez le **nom DNS** de votre cache.</span><span class="sxs-lookup"><span data-stu-id="96a90-128">Enter the **DNS name** for your cache.</span></span>
   * <span data-ttu-id="96a90-129">Spécifiez votre **abonnement**, **groupe de ressources**, **emplacement** et **niveau tarifaire**.</span><span class="sxs-lookup"><span data-stu-id="96a90-129">Specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span>
   * <span data-ttu-id="96a90-130">Pour ce didacticiel, choisissez **Débloquer le port 6379**.</span><span class="sxs-lookup"><span data-stu-id="96a90-130">For this tutorial, choose **Unblock port 6379**.</span></span>

   > [!NOTE]
   >
   > <span data-ttu-id="96a90-131">Vous pouvez utiliser SSL avec les caches Redis, mais vous devez utiliser un autre client Redis comme Jedis.</span><span class="sxs-lookup"><span data-stu-id="96a90-131">You can use SSL with Redis caches, but you would need to use a different Redis client like Jedis.</span></span> <span data-ttu-id="96a90-132">Pour plus d’informations, consultez [Utilisation du cache Redis Azure avec Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="96a90-132">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>
   >

   <span data-ttu-id="96a90-133">Une fois que vous avez défini ces options, cliquez sur **Créer** pour créer votre cache.</span><span class="sxs-lookup"><span data-stu-id="96a90-133">When you have specified these options, click **Create** to create your cache.</span></span>

   ![Portail Azure][AZ03]

1. <span data-ttu-id="96a90-135">Une fois votre cache terminé, il est répertorié dans votre **Tableau de bord** Azure et dans les pages **Toutes les ressources** et **Caches Redis**.</span><span class="sxs-lookup"><span data-stu-id="96a90-135">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under the **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="96a90-136">Vous pouvez cliquer sur le cache à l’un de ces emplacements pour ouvrir la page des propriétés de votre cache.</span><span class="sxs-lookup"><span data-stu-id="96a90-136">You can click on your cache on any of those locations to open the properties page for your cache.</span></span>

   ![Portail Azure][AZ04]

1. <span data-ttu-id="96a90-138">Quand la page qui contient la liste des propriétés de votre cache est affichée, cliquez sur **Clés d’accès** et copiez vos clés d’accès pour votre cache.</span><span class="sxs-lookup"><span data-stu-id="96a90-138">When the page that contains the list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Portail Azure][AZ05]

## <a name="configure-your-custom-spring-boot-to-use-your-redis-cache"></a><span data-ttu-id="96a90-140">Configurer votre Spring Boot personnalisé pour utiliser votre Cache Redis</span><span class="sxs-lookup"><span data-stu-id="96a90-140">Configure your custom Spring Boot to use your Redis Cache</span></span>

1. <span data-ttu-id="96a90-141">Recherchez le fichier *application.properties* dans le répertoire *resources* de votre application, ou créez le fichier s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="96a90-141">Locate the *application.properties* file in the *resources* directory of your app, or create the file if it does not already exist.</span></span>

   ![Rechercher le fichier application.properties][RE01]

1. <span data-ttu-id="96a90-143">Ouvrez le fichier *application.properties* dans un éditeur de texte, ajoutez les lignes suivantes au fichier et remplacez les exemples de valeurs par les propriétés appropriées de votre cache :</span><span class="sxs-lookup"><span data-stu-id="96a90-143">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties from your cache:</span></span>

   ```yaml
   # Specify the DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify the port for your Redis cache.
   spring.redis.port=6379

   # Specify the access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Modification du fichier application.properties][RE02]

   > [!NOTE] 
   > 
   > <span data-ttu-id="96a90-145">Si vous utilisez un autre client Redis comme Jedis qui active SSL, spécifiez le port 6380 dans votre fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="96a90-145">If you were using a different Redis client like Jedis that enables SSL, you would specify port 6380 in your *application.properties* file.</span></span> <span data-ttu-id="96a90-146">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="96a90-146">For example:</span></span>
   > 
   > ```yaml
   > spring.redis.host=myspringbootcache.redis.cache.windows.net
   > spring.redis.password=57686f6120447564652c2049495320526f636b73=
   > spring.redis.ssl=true
   > spring.redis.port=6380
   > ```
   > 
   > <span data-ttu-id="96a90-147">Pour plus d’informations, consultez [Utilisation du cache Redis Azure avec Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="96a90-147">For more information, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span> 
   > 

1. <span data-ttu-id="96a90-148">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="96a90-148">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="96a90-149">Créez un dossier nommé *controller* sous le dossier source de votre package, par exemple :</span><span class="sxs-lookup"><span data-stu-id="96a90-149">Create a folder named *controller* under the source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="96a90-150">-ou-</span><span class="sxs-lookup"><span data-stu-id="96a90-150">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="96a90-151">Créez un fichier nommé *HelloController.java* dans le dossier *controller*.</span><span class="sxs-lookup"><span data-stu-id="96a90-151">Create a new file named *HelloController.java* in the *controller* folder.</span></span> <span data-ttu-id="96a90-152">Ouvrez le fichier dans un éditeur de texte, puis ajoutez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="96a90-152">Open the file in a text editor and add the following code to it:</span></span>

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.data.redis.core.StringRedisTemplate;
   import org.springframework.data.redis.core.ValueOperations;

   @RestController
   public class HelloController {
   
      @Autowired
      private StringRedisTemplate template;

      @RequestMapping("/")
      // Define the Hello World controller.
      public String hello() {
      
         ValueOperations<String, String> ops = this.template.opsForValue();

         // Add a Hello World string to your cache.
         String key = "greeting";
         if (!this.template.hasKey(key)) {
             ops.set(key, "Hello World!");
         }

         // Return the string from your cache.
         return ops.get(key);
      }
   }
   ```
   
   <span data-ttu-id="96a90-153">Où vous devez remplacer `com.contoso.myazuredemo` par le nom du package de votre projet.</span><span class="sxs-lookup"><span data-stu-id="96a90-153">Where you will need to replace `com.contoso.myazuredemo` with the package name for your project.</span></span>

1. <span data-ttu-id="96a90-154">Enregistrez et fermez le fichier *HelloController.java*.</span><span class="sxs-lookup"><span data-stu-id="96a90-154">Save and close the *HelloController.java* file.</span></span>

1. <span data-ttu-id="96a90-155">Générez votre application Spring Boot avec Maven et exécutez-la, par exemple :</span><span class="sxs-lookup"><span data-stu-id="96a90-155">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="96a90-156">Testez l’application web en accédant à http://localhost:8080 avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :</span><span class="sxs-lookup"><span data-stu-id="96a90-156">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="96a90-157">Le message « Hello World! » de votre exemple de contrôleur</span><span class="sxs-lookup"><span data-stu-id="96a90-157">You should see the "Hello World!"</span></span> <span data-ttu-id="96a90-158">doit s’afficher. Il est extrait de manière dynamique à partir de votre cache Redis.</span><span class="sxs-lookup"><span data-stu-id="96a90-158">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96a90-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="96a90-159">Next steps</span></span>

<span data-ttu-id="96a90-160">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="96a90-160">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="96a90-161">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="96a90-161">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="96a90-162">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="96a90-162">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="96a90-163">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="96a90-163">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="96a90-164">Pour plus d’informations sur la prise en main du Cache Redis avec Java sur Azure, consultez [Utilisation du Cache Redis Azure avec Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="96a90-164">For more information about getting started using Redis Cache with Java on Azure, see [How to use Azure Redis Cache with Java][Redis Cache with Java].</span></span>

<span data-ttu-id="96a90-165">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="96a90-165">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="96a90-166">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="96a90-166">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="96a90-167">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="96a90-167">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="96a90-168">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="96a90-168">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: /azure/redis-cache/cache-java-get-started

<!-- IMG List -->

[AZ01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ01.png
[AZ02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ02.png
[AZ03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ03.png
[AZ04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ04.png
[AZ05]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/AZ05.png

[SI01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI01.png
[SI02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI02.png
[SI03]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI03.png
[SI04]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/SI04.png

[RE01]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE01.png
[RE02]: ./media/configure-spring-boot-initializer-java-app-with-redis-cache/RE02.png
