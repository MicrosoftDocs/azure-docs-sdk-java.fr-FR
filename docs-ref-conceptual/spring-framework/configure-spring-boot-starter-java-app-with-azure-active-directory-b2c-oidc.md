---
title: Guide pratique pour utiliser Spring Boot Starter pour Azure Active Directory B2C
description: Découvrez comment configurer une application d’initialisation Spring Boot avec l’application de démarrage Azure Active Directory B2C.
services: active-directory-b2c
documentationcenter: java
author: panli
manager: kevinzha
editor: panli
ms.assetid: ''
ms.author: panli
ms.date: 02/28/2019
ms.devlang: java
ms.service: active-directory-b2c
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 21aa6c812a519d686356851a57f00688d9a24fa4
ms.sourcegitcommit: 733115fe0a7b5109b511b4a32490f8264cf91217
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65625710"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a><span data-ttu-id="ed15e-103">Didacticiel : Sécuriser une application web Java avec Spring Boot Starter pour Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="ed15e-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory B2C.</span></span>

## <a name="overview"></a><span data-ttu-id="ed15e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ed15e-104">Overview</span></span>

<span data-ttu-id="ed15e-105">Cet article illustre la création d’une application Java avec [Spring Initializr](https://start.spring.io/), qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed15e-105">This article demonstrates creating a Java app with the [Spring Initializr](https://start.spring.io/) that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed15e-106">Ce tutoriel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ed15e-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ed15e-107">Créer une application Java à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="ed15e-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="ed15e-108">Configurer Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ed15e-108">Configure Azure Active Directory B2C</span></span>
> * <span data-ttu-id="ed15e-109">Sécuriser l’application avec des classes et annotations Spring Boot</span><span class="sxs-lookup"><span data-stu-id="ed15e-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="ed15e-110">Générer et tester votre application Java</span><span class="sxs-lookup"><span data-stu-id="ed15e-110">Build and test your Java application</span></span>

<span data-ttu-id="ed15e-111">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="ed15e-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed15e-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ed15e-112">Prerequisites</span></span>

<span data-ttu-id="ed15e-113">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ed15e-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="ed15e-114">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ed15e-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="ed15e-115">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="ed15e-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="ed15e-116">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ed15e-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="ed15e-117">Créer une application à l’aide de Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="ed15e-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="ed15e-118">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ed15e-118">Browse to <https://start.spring.io/>.</span></span>

2. <span data-ttu-id="ed15e-119">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis sélectionnez les modules **Web** et **Security** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="ed15e-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then select the **Web** and **Security** module of the Spring Initializr.</span></span>

   ![Spécifiez les noms de groupes et d’artefacts.](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. <span data-ttu-id="ed15e-121">Cliquez sur `Generate Project` et téléchargez le projet sur votre ordinateur local à l’invite.</span><span class="sxs-lookup"><span data-stu-id="ed15e-121">Click `Generate Project`, download the project to a path on your local computer when prompted.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="ed15e-122">Créer une instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed15e-122">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="ed15e-123">Créer l’instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed15e-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="ed15e-124">Connectez-vous à <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="ed15e-124">Log into <https://portal.azure.com>.</span></span>

2. <span data-ttu-id="ed15e-125">Cliquez sur **+Créer une ressource**, sur **Identité**, puis sur **Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-125">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory B2C**.</span></span>

   ![Créer une instance Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. <span data-ttu-id="ed15e-127">Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**, spécifiez `${your-tenant-name}` comme **nom de domaine**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-127">Enter your **Organization name** and your **Initial domain name**, record the **domain name** as your `${your-tenant-name}` and click **Create**.</span></span>

   ![Obtenir le nom de votre locataire B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. <span data-ttu-id="ed15e-129">Sélectionnez le nom de votre compte dans le coin supérieur droit de la barre d’outils du portail Azure, puis cliquez sur **Changer de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-129">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Choisir votre instance Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. <span data-ttu-id="ed15e-131">Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="ed15e-131">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Choisir votre instance Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. <span data-ttu-id="ed15e-133">Recherchez `b2c` et cliquez sur le service `Azure AD B2C`.</span><span class="sxs-lookup"><span data-stu-id="ed15e-133">Search `b2c` and click `Azure AD B2C` service.</span></span>

   ![Rechercher l’instance Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="ed15e-135">Ajouter une inscription d’application pour votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="ed15e-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="ed15e-136">Sélectionnez **Azure AD B2C** dans le menu du portail, cliquez sur **Applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-136">Select **Azure AD B2C** from the portal menu, click **Applications**, and then click **Add**.</span></span>

   ![Ajouter une inscription d’application](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. <span data-ttu-id="ed15e-138">Spécifiez le **Nom** de votre application, ajoutez `http://localhost:8080/home` pour l’**URL de réponse**, spécifiez votre `${your-client-id}` comme **ID d’application**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-138">Specify your application **Name**, add `http://localhost:8080/home` for the **Reply URL**, record the **Application ID** as your `${your-client-id}` and then click **Save**.</span></span>

   ![Ajouter une URL de réponse d’application](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. <span data-ttu-id="ed15e-140">Sélectionnez **Clés** à partir de votre application, cliquez sur **Générer une clé** pour générer `${your-client-secret}`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-140">Select **Keys** from your application, click **Generate key** to generate `${your-client-secret}` and then **Save**.</span></span>

4. <span data-ttu-id="ed15e-141">Sélectionnez **Flux d’utilisateurs** à gauche, puis **cliquez sur** \*\*Nouveau flux d’utilisateur \*\*.</span><span class="sxs-lookup"><span data-stu-id="ed15e-141">Select **User flows** on your left, and then **Click** \*\*New user flow \*\*.</span></span>

   ![Créer un flux d’utilisateur](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. <span data-ttu-id="ed15e-143">Choisissez **S’inscrire ou se connecter**, **Modification de profil** et **Réinitialisation du mot de passe** pour créer les flux d’utilisateurs respectifs.</span><span class="sxs-lookup"><span data-stu-id="ed15e-143">Choose **Sign up or in**, **Profile editing** and **Password reset** to create user flows respectively.</span></span> <span data-ttu-id="ed15e-144">Spécifiez le **Nom** et les **Attributs utilisateur et revendications** de votre flux d’utilisateur, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ed15e-144">Specify your user flow **Name** and **User attributes and claims**, click **Create**.</span></span>

   ![Configurer un flux d’utilisateur](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="ed15e-146">Configurer et compiler votre application</span><span class="sxs-lookup"><span data-stu-id="ed15e-146">Configure and compile your app</span></span>

1. <span data-ttu-id="ed15e-147">Extrayez les fichiers des archives du projet que vous avez créées et téléchargées précédemment dans ce tutoriel dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="ed15e-147">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

2. <span data-ttu-id="ed15e-148">Accédez au dossier parent pour votre projet, puis ouvrez le fichier de projet Maven `pom.xml` dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ed15e-148">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

3. <span data-ttu-id="ed15e-149">Ajoutez les dépendances associées à la sécurité Spring OAuth2 au fichier `pom.xml` :</span><span class="sxs-lookup"><span data-stu-id="ed15e-149">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.azure</groupId>
       <artifactId>azure-active-directory-b2c-spring-boot-starter</artifactId>
       <version>2.1.6.M2</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-thymeleaf</artifactId>
   </dependency>
   <dependency>
       <groupId>org.thymeleaf.extras</groupId>
       <artifactId>thymeleaf-extras-springsecurity5</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="ed15e-150">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="ed15e-150">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="ed15e-151">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.yml* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ed15e-151">Navigate to the *src/main/resources* folder in your project and open the *application.yml* file in a text editor.</span></span>

6. <span data-ttu-id="ed15e-152">Spécifiez les paramètres pour l’inscription de votre application en utilisant les valeurs que vous avez créé précédemment ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="ed15e-152">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

   ```yaml
   azure:
     activedirectory:
       b2c:
         tenant: ${your-tenant-name}
         client-id: ${your-client-id}
         client-secret: ${your-client-secret}
         reply-url: ${your-reply-url-from-aad} # should be absolute url.
         logout-success-url: ${you-logout-success-url}
         user-flows:
           sign-up-or-sign-in: ${your-sign-up-or-in-user-flow}
           profile-edit: ${your-profile-edit-user-flow}     # optional
           password-reset: ${your-password-reset-user-flow} # optional
   ```
   <span data-ttu-id="ed15e-153">Où :</span><span class="sxs-lookup"><span data-stu-id="ed15e-153">Where:</span></span>

   | <span data-ttu-id="ed15e-154">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ed15e-154">Parameter</span></span> | <span data-ttu-id="ed15e-155">Description</span><span class="sxs-lookup"><span data-stu-id="ed15e-155">Description</span></span> |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | <span data-ttu-id="ed15e-156">Contient la valeur `${your-tenant-name` de votre AD B2C indiquée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ed15e-156">Contains your AD B2C's `${your-tenant-name` from earlier.</span></span> |
   | `azure.activedirectory.b2c.client-id` | <span data-ttu-id="ed15e-157">Contient la valeur `${your-client-id}` de votre application indiquée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ed15e-157">Contains the `${your-client-id}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.client-secret` | <span data-ttu-id="ed15e-158">Contient la valeur `${your-client-secret}` de votre application indiquée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ed15e-158">Contains the `${your-client-secret}` from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.reply-url` | <span data-ttu-id="ed15e-159">Contient l’une des **URL de réponse** de votre application indiquées précédemment.</span><span class="sxs-lookup"><span data-stu-id="ed15e-159">Contains one of the **Reply URL** from your application that you completed earlier.</span></span> |
   | `azure.activedirectory.b2c.logout-success-url` | <span data-ttu-id="ed15e-160">Spécifiez l’URL quand votre application se déconnecte avec succès.</span><span class="sxs-lookup"><span data-stu-id="ed15e-160">Specify the URL when your application logout successfully.</span></span> |
   | `azure.activedirectory.b2c.user-flows` | <span data-ttu-id="ed15e-161">Contient les noms des flux d’utilisateurs que vous avez spécifiés plus haut.</span><span class="sxs-lookup"><span data-stu-id="ed15e-161">Contains the name of the user flows that you completed earlier.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="ed15e-162">Pour une liste complète des valeurs disponibles dans votre fichier *application.yml*, consultez l’[exemple Spring Boot Azure Active Directory B2C][exemple Spring Boot AAD B2C] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="ed15e-162">For a full list of values that are available in your *application.yml* file, see the [Azure Active Directory B2C Spring Boot Sample][AAD B2C Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="ed15e-163">Enregistrez et fermez le fichier *application.yml*.</span><span class="sxs-lookup"><span data-stu-id="ed15e-163">Save and close the *application.yml* file.</span></span>

8. <span data-ttu-id="ed15e-164">Créez un dossier nommé *controller* dans le dossier source Java pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ed15e-164">Create a folder named *controller* in the Java source folder for your application.</span></span>

9. <span data-ttu-id="ed15e-165">Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ed15e-165">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="ed15e-166">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="ed15e-166">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.controller;
    
    import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
    import org.springframework.security.oauth2.core.user.OAuth2User;
    import org.springframework.stereotype.Controller;
    import org.springframework.ui.Model;
    import org.springframework.web.bind.annotation.GetMapping;
    
    @Controller
    public class WebController {
    
        private void initializeModel(Model model, OAuth2AuthenticationToken token) {
            if (token != null) {
                final OAuth2User user = token.getPrincipal();
    
                model.addAttribute("grant_type", user.getAuthorities());
                model.addAllAttributes(user.getAttributes());
            }
        }
    
        @GetMapping(value = "/")
        public String index(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    
        @GetMapping(value = "/greeting")
        public String greeting(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "greeting";
        }
    
        @GetMapping(value = "/home")
        public String home(Model model, OAuth2AuthenticationToken token) {
            initializeModel(model, token);
    
            return "home";
        }
    }
    ```

11. <span data-ttu-id="ed15e-167">Créez un dossier nommé *security* dans le dossier source Java pour votre application.</span><span class="sxs-lookup"><span data-stu-id="ed15e-167">Create a folder named *security* in the Java source folder for your application.</span></span>

12. <span data-ttu-id="ed15e-168">Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ed15e-168">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="ed15e-169">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="ed15e-169">Enter the following code, then save and close the file:</span></span>

    ```java
    package sample.aad.security;
    
    import com.microsoft.azure.spring.autoconfigure.b2c.AADB2COidcLoginConfigurer;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    
    @EnableWebSecurity
    public class WebSecurityConfiguration extends WebSecurityConfigurerAdapter {
    
        private final AADB2COidcLoginConfigurer configurer;
    
        public WebSecurityConfiguration(AADB2COidcLoginConfigurer configurer) {
            this.configurer = configurer;
        }
    
        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                    .authorizeRequests()
                    .anyRequest()
                    .authenticated()
                    .and()
                    .apply(configurer)
            ;
        }
    }
    ```
14. <span data-ttu-id="ed15e-170">Copiez les fichiers `greeting.html` et `home.html` de l’[exemple Spring Boot Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates) et remplacez `${your-profile-edit-user-flow}` et `${your-password-reset-user-flow}` par les noms respectifs de vos flux d’utilisateurs indiqués plus haut.</span><span class="sxs-lookup"><span data-stu-id="ed15e-170">Copy the `greeting.html` and `home.html` from [Azure AD B2C Spring Boot Sample](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates), and replace the `${your-profile-edit-user-flow}` and `${your-password-reset-user-flow}` with your user flow name respectively that completed earlier.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="ed15e-171">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="ed15e-171">Build and test your app</span></span>

1. <span data-ttu-id="ed15e-172">Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.</span><span class="sxs-lookup"><span data-stu-id="ed15e-172">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

2. <span data-ttu-id="ed15e-173">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ed15e-173">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. <span data-ttu-id="ed15e-174">Une fois que votre application est créée et démarrée dans Maven, ouvrez <http://localhost:8080/> dans un navigateur web ; vous devez être redirigé vers la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="ed15e-174">After your application is built and started by Maven, open <http://localhost:8080/> in a web browser; you should be redirected to login page.</span></span>

   ![Page de connexion](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. <span data-ttu-id="ed15e-176">Cliquez sur le lien avec le nom du flux d’utilisateur `${your-sign-up-or-in}` ; vous devez être redirigé vers Azure AD B2C pour démarrer le processus d’authentification.</span><span class="sxs-lookup"><span data-stu-id="ed15e-176">Click linke with name of `${your-sign-up-or-in}` user flow, you should be rediected Azure AD B2C to start the authentication process.</span></span>

   ![Connexion à Azure AD B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. <span data-ttu-id="ed15e-178">Une fois connecté, vous devez voir l’exemple `home page` dans le navigateur,</span><span class="sxs-lookup"><span data-stu-id="ed15e-178">After you have logged in successfully, you should see the sample `home page` from the browser,</span></span>

   ![Connexion réussie](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a><span data-ttu-id="ed15e-180">Résumé</span><span class="sxs-lookup"><span data-stu-id="ed15e-180">Summary</span></span>

<span data-ttu-id="ed15e-181">Dans ce tutoriel, vous avez crée une application web Java avec l’application de démarrage Azure Active Directory B2C, configuré un nouveau locataire Azure AD B2C et inscrit une nouvelle application, avant de configurer votre application pour utiliser les annotations et classes Spring pour protéger l’application web.</span><span class="sxs-lookup"><span data-stu-id="ed15e-181">In this tutorial, you created a new Java web application using the Azure Active Directory B2C starter, configured a new Azure AD B2C tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed15e-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ed15e-182">Next steps</span></span>

<span data-ttu-id="ed15e-183">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ed15e-183">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15e-184">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="ed15e-184">Spring on Azure</span></span>](/java/azure/spring-framework)
