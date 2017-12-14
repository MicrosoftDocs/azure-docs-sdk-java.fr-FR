---
title: Comment utiliser Spring Boot Starter pour Azure Active Directory
description: "Découvrez comment configurer une application d’initialisation Spring Boot avec l’application de démarrage Azure Active Directory."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 12/01/2017
ms.author: robmcm
ms.openlocfilehash: a999e33674ea01e776db10186e8af83ce157ef20
ms.sourcegitcommit: fc48e038721e6910cb8b1f8951df765d517e504d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/06/2017
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="7da86-103">Comment utiliser Spring Boot Starter pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da86-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="7da86-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7da86-104">Overview</span></span>

<span data-ttu-id="7da86-105">Cet article illustre la création d’une application avec **[Spring Initializr]** avec Spring Boot Starter pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7da86-105">This article demonstrates creating an app with the **[Spring Initializr]** which the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7da86-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7da86-106">Prerequisites</span></span>

<span data-ttu-id="7da86-107">Pour suivre les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7da86-107">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="7da86-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="7da86-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="7da86-109">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7da86-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="7da86-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7da86-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="7da86-111">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="7da86-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="7da86-112">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="7da86-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="7da86-113">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="7da86-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Spécifiez les noms de groupes et d’artefacts.][security-01]

1. <span data-ttu-id="7da86-115">Faites défiler jusqu’à la section **Core** (Principal), cochez la case en regard de **Security** (Sécurité), puis dans la section **Web** (Web) cochez la case **Web** (web).</span><span class="sxs-lookup"><span data-stu-id="7da86-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Sélectionner les applications web et de sécurité][security-02]

1. <span data-ttu-id="7da86-117">Faites défiler jusqu’à la section **Azure**, puis cochez la case en regard de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7da86-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Sélectionner l’application de démarrage Azure Active Security][security-03]

1. <span data-ttu-id="7da86-119">Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="7da86-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Générez le projet Spring Boot.][security-04]

1. <span data-ttu-id="7da86-121">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="7da86-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="7da86-122">Créer et configurer une instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da86-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="7da86-123">Créer l’instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7da86-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="7da86-124">Connectez-vous au portail <https://portal.azure.com/>.</span><span class="sxs-lookup"><span data-stu-id="7da86-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="7da86-125">Cliquez sur **+Nouveau**, puis sur **Sécurité + Identité** et enfin sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7da86-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Créer une instance Azure Active Directory][directory-01]

1. <span data-ttu-id="7da86-127">Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7da86-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Spécifier des noms Azure Active Directory][directory-02]

1. <span data-ttu-id="7da86-129">Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant de la barre d’outils située en haut du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7da86-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Choisir votre instance Azure Active Directory][directory-03]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="7da86-131">Ajouter une inscription d’application pour votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="7da86-131">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="7da86-132">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Vue d’ensemble**, puis sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="7da86-132">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Ajouter une inscription d’application][directory-04]

1. <span data-ttu-id="7da86-134">Cliquez sur **Nouvelle inscription d’application**, spécifiez le **Nom** de votre application, utilisez http://localhost:8080 en tant qu’**URL de connexion**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7da86-134">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Créer une inscription d’application][directory-05]

1. <span data-ttu-id="7da86-136">Cliquez sur l’inscription d’application une fois cette dernière créée.</span><span class="sxs-lookup"><span data-stu-id="7da86-136">Click your application registration after it has been created.</span></span>

   ![Sélectionner votre inscription d’application][directory-06]

1. <span data-ttu-id="7da86-138">Sur la page de votre inscription d’application, copiez votre **ID d’application** pour une utilisation ultérieure, puis cliquez sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="7da86-138">When the page for your app registration, copy your **Application ID** for later, then click **Keys**.</span></span>

   ![Créer des clés d’inscription d’application][directory-07]

1. <span data-ttu-id="7da86-140">Ajoutez une **Description**, spécifiez la **Durée** d’une nouvelle clé, puis cliquez sur **Enregistrer**. La valeur de la clé est automatiquement renseignée lorsque vous cliquez sur l’icône **Enregistrer** ; vous devez copier la valeur de la clé pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7da86-140">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="7da86-141">(Il ne vous sera pas possible de récupérer cette valeur plus tard.)</span><span class="sxs-lookup"><span data-stu-id="7da86-141">(You will not be able to retrieve this value later.)</span></span>

   ![Spécifier les paramètres de la clé d’inscription d’application][directory-08]

1. <span data-ttu-id="7da86-143">Sur la page principale de votre inscription d’application, cliquez sur **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="7da86-143">From the main page for your app registration, click **Required permissions**.</span></span>

   ![Autorisations requises de l’inscription d’application][directory-09]

1. <span data-ttu-id="7da86-145">Cliquez sur **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7da86-145">Click **Windows Azure Active Directory**.</span></span>

   ![Sélectionner Windows Azure Active Directory][directory-10]

1. <span data-ttu-id="7da86-147">Cochez les cases en regard de **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7da86-147">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Activer les autorisations d’accès][directory-11]

1. <span data-ttu-id="7da86-149">Sur la page **Autorisations requises**, cliquez sur **Accorder les autorisations**, puis cliquez sur **Oui** à l’invite.</span><span class="sxs-lookup"><span data-stu-id="7da86-149">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Accorder les autorisations d’accès][directory-12]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="7da86-151">Configurer et compiler votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="7da86-151">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="7da86-152">Extrayez les fichiers de l’archive du projet téléchargé dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="7da86-152">Extract the files from the downloaded project archive into a directory.</span></span>

1. <span data-ttu-id="7da86-153">Accédez au dossier parent de votre projet, puis ouvrez le fichier *pom.xml* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="7da86-153">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="7da86-154">Ajoutez la dépendance associée à la sécurité Spring OAuth2, par exemple :</span><span class="sxs-lookup"><span data-stu-id="7da86-154">Add the dependency for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security.oauth</groupId>
      <artifactId>spring-security-oauth2</artifactId>
   </dependency>
   ```

1. <span data-ttu-id="7da86-155">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="7da86-155">Save and close the  the *pom.xml* file.</span></span>

1. <span data-ttu-id="7da86-156">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="7da86-156">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="7da86-157">Ajoutez la clé de votre compte de stockage à l’aide des valeurs antérieures, par exemple :</span><span class="sxs-lookup"><span data-stu-id="7da86-157">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory Application ID:
   azure.activedirectory.clientId=11111111-1111-1111-1111-1111111111111111

   # Specifies your secret key:
   azure.activedirectory.clientSecret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.activeDirectoryGroups=Users
   ```
   <span data-ttu-id="7da86-158">Où :</span><span class="sxs-lookup"><span data-stu-id="7da86-158">Where:</span></span>
   <span data-ttu-id="7da86-159">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7da86-159">Parameter</span></span> | <span data-ttu-id="7da86-160">Description</span><span class="sxs-lookup"><span data-stu-id="7da86-160">Description</span></span>
   ---|---|---
   `azure.activedirectory.clientId` | <span data-ttu-id="7da86-161">Contient votre **ID d’application** utilisé précédemment.</span><span class="sxs-lookup"><span data-stu-id="7da86-161">Contains your **Application ID** from earlier.</span></span>
   `azure.activedirectory.clientSecret` | <span data-ttu-id="7da86-162">Contient la valeur de clé de votre inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="7da86-162">Contains the key value from your app registration which you completed earlier.</span></span>
   `azure.activedirectory.activeDirectoryGroups` | <span data-ttu-id="7da86-163">Contient une liste des groupes Active Directory à utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7da86-163">Contains a list of Active Directory groups to use for authentication.</span></span>


1. <span data-ttu-id="7da86-164">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="7da86-164">Save and close the  the *application.properties* file.</span></span>

1. <span data-ttu-id="7da86-165">Créez un dossier nommé *controller* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="7da86-165">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="7da86-166">Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="7da86-166">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="7da86-167">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="7da86-167">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.web.authentication.preauth.PreAuthenticatedAuthenticationToken;
   
   @RestController
   public class HelloController {
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String hello() {
         return "Hello World!";
      }
   }
   ```

1. <span data-ttu-id="7da86-168">Créez un dossier nommé *security* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="7da86-168">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="7da86-169">Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="7da86-169">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="7da86-170">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="7da86-170">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import com.microsoft.azure.spring.autoconfigure.aad.AADAuthenticationFilter;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.autoconfigure.security.oauth2.client.EnableOAuth2Sso;
   import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
   import org.springframework.security.config.annotation.web.builders.HttpSecurity;
   import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
   import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;
   import org.springframework.security.web.csrf.CookieCsrfTokenRepository;
   
   @EnableOAuth2Sso
   @EnableGlobalMethodSecurity(securedEnabled = true, prePostEnabled = true)
   
   public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
      @Autowired
      private AADAuthenticationFilter aadAuthFilter;
      @Override
      protected void configure(HttpSecurity http) throws Exception {
         http.authorizeRequests().anyRequest().permitAll();
         http.addFilterBefore(aadAuthFilter, UsernamePasswordAuthenticationFilter.class);
      }
   }
   ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="7da86-171">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="7da86-171">Build and test your app</span></span>

1. <span data-ttu-id="7da86-172">Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.</span><span class="sxs-lookup"><span data-stu-id="7da86-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="7da86-173">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7da86-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   ```

   ![][build-application]

1. <span data-ttu-id="7da86-174">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7da86-174">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```



1. <span data-ttu-id="7da86-175">Une fois que votre application est développée et démarrée dans Maven, ouvrez <http://localhost:8080> dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="7da86-175">After your application is built and started by Maven, open <http://localhost:8080> in a web browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7da86-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7da86-176">Next steps</span></span>

<span data-ttu-id="7da86-177">Pour plus d’informations sur Azure Active Directory, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7da86-177">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="7da86-178">[Documentation Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="7da86-178">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="7da86-179">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7da86-179">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="7da86-180">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7da86-180">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="7da86-181">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="7da86-181">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="7da86-182">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="7da86-182">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="7da86-183">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7da86-183">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="7da86-184">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="7da86-184">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="7da86-185">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="7da86-185">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="7da86-186">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="7da86-186">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<!-- URL List -->

[Documentation Azure Active Directory]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[security-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-01.png
[security-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-02.png
[security-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-03.png
[security-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/security-04.png

[directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-01.png
[directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-02.png
[directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-03.png
[directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-04.png
[directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-05.png
[directory-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-06.png
[directory-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-07.png
[directory-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-08.png
[directory-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-09.png
[directory-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-10.png
[directory-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-11.png
[directory-12]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-12.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
