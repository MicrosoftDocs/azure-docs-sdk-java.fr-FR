---
title: Comment utiliser Spring Boot Starter pour Azure Active Directory
description: Découvrez comment configurer une application d’initialisation Spring Boot avec l’application de démarrage Azure Active Directory.
services: active-directory
documentationcenter: java
author: rmcmurray
manager: mbaldwin
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 06/20/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: adcbc78cc129daf589bf070741308e4024432e5d
ms.sourcegitcommit: 5282a51bf31771671df01af5814df1d2b8e4620c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37090832"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="a8038-103">Comment utiliser Spring Boot Starter pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8038-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="a8038-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="a8038-104">Overview</span></span>

<span data-ttu-id="a8038-105">Cet article illustre la création d’une application avec **[Spring Initializr]** qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8038-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8038-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="a8038-106">Prerequisites</span></span>

<span data-ttu-id="a8038-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a8038-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="a8038-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [Avantages pour les abonnés MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="a8038-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="a8038-109">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a8038-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="a8038-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a8038-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="a8038-111">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="a8038-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="a8038-112">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="a8038-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="a8038-113">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="a8038-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Aritifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Spécifiez les noms de groupes et d’artefacts.][security-01]

1. <span data-ttu-id="a8038-115">Faites défiler jusqu’à la section **Core** (Principal), cochez la case en regard de **Security** (Sécurité), puis dans la section **Web** (Web) cochez la case **Web** (web).</span><span class="sxs-lookup"><span data-stu-id="a8038-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Sélectionner les applications web et de sécurité][security-02]

1. <span data-ttu-id="a8038-117">Faites défiler jusqu’à la section **Azure**, puis cochez la case en regard de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8038-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Sélectionner l’application de démarrage Azure Active Security][security-03]

1. <span data-ttu-id="a8038-119">Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="a8038-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Générez le projet Spring Boot.][security-04]

1. <span data-ttu-id="a8038-121">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a8038-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="a8038-122">Créer et configurer une instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8038-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="a8038-123">Créer l’instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8038-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="a8038-124">Connectez-vous à <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="a8038-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="a8038-125">Cliquez sur **+Nouveau**, puis sur **Sécurité + Identité** et enfin sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8038-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Créer une instance Azure Active Directory][directory-01]

1. <span data-ttu-id="a8038-127">Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a8038-127">Enter your **Organization name** and your **Initial domain name**, and then click **Create**.</span></span>

   ![Spécifier des noms Azure Active Directory][directory-02]

1. <span data-ttu-id="a8038-129">Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant de la barre d’outils située en haut du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a8038-129">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Choisir votre instance Azure Active Directory][directory-03]

1. <span data-ttu-id="a8038-131">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Properties** (Propriétés), et copiez **Directory ID** (ID d’annuaire) - vous en aurez besoin plus tard dans cet article.</span><span class="sxs-lookup"><span data-stu-id="a8038-131">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID** - you will use that later in this article.</span></span>

   ![Copier votre ID Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="a8038-133">Ajouter une inscription d’application pour votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="a8038-133">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="a8038-134">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Vue d’ensemble**, puis sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="a8038-134">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Ajouter une inscription d’application][directory-04]

1. <span data-ttu-id="a8038-136">Cliquez sur **Nouvelle inscription d’application**, spécifiez le **Nom** de votre application, utilisez http://localhost:8080 en tant qu’**URL de connexion**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a8038-136">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Créer une inscription d’application][directory-05]

1. <span data-ttu-id="a8038-138">Cliquez sur l’inscription d’application une fois cette dernière créée.</span><span class="sxs-lookup"><span data-stu-id="a8038-138">Click your application registration after it has been created.</span></span>

   ![Sélectionner votre inscription d’application][directory-06]

1. <span data-ttu-id="a8038-140">Sur la page de votre inscription d’application, copiez votre **ID d’application** pour une utilisation ultérieure, puis cliquez sur **Paramètres** puis sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="a8038-140">When the page for your app registration, copy your **Application ID** for later use, then click **Settings**, and then click **Keys**.</span></span>

   ![Créer des clés d’inscription d’application][directory-07]

1. <span data-ttu-id="a8038-142">Ajoutez une **Description**, spécifiez la **Durée** d’une nouvelle clé, puis cliquez sur **Enregistrer**. La valeur de la clé est automatiquement renseignée lorsque vous cliquez sur l’icône **Enregistrer** ; vous devez copier la valeur de la clé pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a8038-142">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key for later.</span></span> <span data-ttu-id="a8038-143">(Il ne vous sera pas possible de récupérer cette valeur plus tard.)</span><span class="sxs-lookup"><span data-stu-id="a8038-143">(You will not be able to retrieve this value later.)</span></span>

   ![Spécifier les paramètres de la clé d’inscription d’application][directory-08]

1. <span data-ttu-id="a8038-145">Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="a8038-145">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Autorisations requises de l’inscription d’application][directory-09]

1. <span data-ttu-id="a8038-147">Cliquez sur **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8038-147">Click **Windows Azure Active Directory**.</span></span>

   ![Sélectionner Windows Azure Active Directory][directory-10]

1. <span data-ttu-id="a8038-149">Cochez les cases en regard de **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a8038-149">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Activer les autorisations d’accès][directory-11]

1. <span data-ttu-id="a8038-151">Sur la page **Autorisations requises**, cliquez sur **Accorder les autorisations**, puis cliquez sur **Oui** à l’invite.</span><span class="sxs-lookup"><span data-stu-id="a8038-151">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Accorder les autorisations d’accès][directory-12]

1. <span data-ttu-id="a8038-153">Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="a8038-153">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Modifier les URL de réponse][directory-14]

1. <span data-ttu-id="a8038-155">Saisissez la nouvelle URL de réponse « http://localhost:8080/login/oauth2/code/azure », puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a8038-155">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Ajouter une nouvelle URL de réponse][directory-15]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="a8038-157">Configurer et compiler votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="a8038-157">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="a8038-158">Extrayez les fichiers de l’archive du projet téléchargé dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="a8038-158">Extract the files from the downloaded project archive into a directory.</span></span>

2. <span data-ttu-id="a8038-159">Accédez au dossier parent de votre projet, puis ouvrez le fichier *pom.xml* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a8038-159">Navigate to the parent folder in your project and open the *pom.xml* file in a text editor.</span></span>

3. <span data-ttu-id="a8038-160">Ajoutez la dépendance associée à la sécurité Spring OAuth2, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a8038-160">Add the dependencies for Spring OAuth2 security; for example:</span></span>

   ```xml
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-client</artifactId>
   </dependency>
   <dependency>
      <groupId>org.springframework.security</groupId>
      <artifactId>spring-security-oauth2-jose</artifactId>
   </dependency>
   ```

4. <span data-ttu-id="a8038-161">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="a8038-161">Save and close the *pom.xml* file.</span></span>

5. <span data-ttu-id="a8038-162">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a8038-162">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

6. <span data-ttu-id="a8038-163">Ajoutez la clé de votre compte de stockage à l’aide des valeurs antérieures, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a8038-163">Add the key for your storage account using the values from earlier; for example:</span></span>

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authentication:
   azure.activedirectory.active-directory-groups=Users
   ```
   <span data-ttu-id="a8038-164">Où :</span><span class="sxs-lookup"><span data-stu-id="a8038-164">Where:</span></span>

   | <span data-ttu-id="a8038-165">Paramètre</span><span class="sxs-lookup"><span data-stu-id="a8038-165">Parameter</span></span> | <span data-ttu-id="a8038-166">Description</span><span class="sxs-lookup"><span data-stu-id="a8038-166">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="a8038-167">Contient l’**ID du répertoire** d’Active Directory vu précédemment.</span><span class="sxs-lookup"><span data-stu-id="a8038-167">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="a8038-168">Contient l’**ID de l’application** de votre inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="a8038-168">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="a8038-169">Contient la **Valeur** de votre clé d’inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="a8038-169">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="a8038-170">Contient une liste des groupes Active Directory à utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="a8038-170">Contains a list of Active Directory groups to use for authentication.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="a8038-171">Pour obtenir une liste complète des valeurs disponibles dans votre fichier *application.properties*, consultez [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8038-171">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

7. <span data-ttu-id="a8038-172">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a8038-172">Save and close the *application.properties* file.</span></span>

8. <span data-ttu-id="a8038-173">Créez un dossier nommé *controller* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="a8038-173">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

9. <span data-ttu-id="a8038-174">Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a8038-174">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

10. <span data-ttu-id="a8038-175">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="a8038-175">Enter the following code, then save and close the file:</span></span>

   ```java
   package com.wingtiptoys.security;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.security.access.prepost.PreAuthorize;
   import org.springframework.security.oauth2.client.OAuth2AuthorizedClient;
   import org.springframework.security.oauth2.client.authentication.OAuth2AuthenticationToken;
   import org.springframework.ui.Model;

   @RestController
   public class HelloController {
      @Autowired
      @PreAuthorize("hasRole('Users')")
      @RequestMapping("/")
      public String helloWorld() {
         return "Hello World!";
      }
   }
   ```
   > [!NOTE]
   > 
   > <span data-ttu-id="a8038-176">Le nom de groupe spécifié pour la méthode `@PreAuthorize("hasRole('')")` doit contenir l’un des groupes spécifiés dans le champ `azure.activedirectory.active-directory-groups` de votre fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="a8038-176">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="a8038-177">Vous pouvez spécifier différents paramètres d’autorisation pour différents mappages de requêtes ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="a8038-177">You can specify different authorization settings for different request mappings; for example:</span></span>
   >
   > ``` java
   > public class HelloController {
   >    @Autowired
   >    @PreAuthorize("hasRole('Users')")
   >    @RequestMapping("/")
   >    public String helloWorld() {
   >       return "Hello Users!";
   >    }
   >    @PreAuthorize("hasRole('Group1')")
   >    @RequestMapping("/Group1")
   >    public String groupOne() {
   >       return "Hello Group 1 Users!";
   >    }
   >    @PreAuthorize("hasRole('Group2')")
   >    @RequestMapping("/Group2")
   >    public String groupTwo() {
   >       return "Hello Group 2 Users!";
   >    }
   > }
   > ```
   >    

11. <span data-ttu-id="a8038-178">Créez un dossier nommé *security* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="a8038-178">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

12. <span data-ttu-id="a8038-179">Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="a8038-179">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

13. <span data-ttu-id="a8038-180">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="a8038-180">Enter the following code, then save and close the file:</span></span>

    ```java
    package com.wingtiptoys.security;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
    import org.springframework.security.config.annotation.web.builders.HttpSecurity;
    import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
    import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
    import org.springframework.security.oauth2.client.oidc.userinfo.OidcUserRequest;
    import org.springframework.security.oauth2.client.userinfo.OAuth2UserService;
    import org.springframework.security.oauth2.core.oidc.user.OidcUser;

    @EnableWebSecurity
    @EnableGlobalMethodSecurity(prePostEnabled = true)
    public class WebSecurityConfig extends WebSecurityConfigurerAdapter {
        @Autowired
        private OAuth2UserService<OidcUserRequest, OidcUser> oidcUserService;

        @Override
        protected void configure(HttpSecurity http) throws Exception {
            http
                .authorizeRequests()
                .anyRequest().authenticated()
                .and()
                .oauth2Login()
                .userInfoEndpoint()
                .oidcUserService(oidcUserService);
        }
    }
    ```

## <a name="build-and-test-your-app"></a><span data-ttu-id="a8038-181">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="a8038-181">Build and test your app</span></span>

1. <span data-ttu-id="a8038-182">Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.</span><span class="sxs-lookup"><span data-stu-id="a8038-182">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="a8038-183">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a8038-183">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Générer votre application][build-application]

1. <span data-ttu-id="a8038-185">Une fois que votre application est créée et démarrée dans Maven, ouvrez <http://localhost:8080> dans un navigateur web ; vous devez fournir un nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a8038-185">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Se connecter à l’application][application-login]

1. <span data-ttu-id="a8038-187">Une fois que vous vous êtes connecté avec succès, vous devez voir le contrôleur afficher l’exemple de texte « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="a8038-187">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Connexion réussie][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="a8038-189">Les comptes d’utilisateur qui ne sont pas autorisés recevront un message **HTTP 403 non autorisé**.</span><span class="sxs-lookup"><span data-stu-id="a8038-189">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="a8038-190">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8038-190">Next steps</span></span>

<span data-ttu-id="a8038-191">Pour plus d’informations sur Azure Active Directory, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a8038-191">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="a8038-192">[Documentation Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="a8038-192">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="a8038-193">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a8038-193">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="a8038-194">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a8038-194">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="a8038-195">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="a8038-195">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="a8038-196">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="a8038-196">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="a8038-197">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="a8038-197">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="a8038-198">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="a8038-198">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="a8038-199">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="a8038-199">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="a8038-200">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="a8038-200">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="a8038-201">Pour un exemple plus détaillé, consultez la page [Azure Active Directory Spring Boot Sample] [ AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="a8038-201">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Documentation Azure Active Directory]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Avantages pour les abonnés MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

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
[directory-13]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-13.png
[directory-14]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-14.png
[directory-15]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-15.png

[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
