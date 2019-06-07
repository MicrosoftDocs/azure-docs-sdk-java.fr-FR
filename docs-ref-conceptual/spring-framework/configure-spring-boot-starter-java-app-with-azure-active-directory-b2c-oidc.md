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
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory-b2c"></a>Didacticiel : Sécuriser une application web Java avec Spring Boot Starter pour Azure Active Directory B2C.

## <a name="overview"></a>Vue d'ensemble

Cet article illustre la création d’une application Java avec [Spring Initializr](https://start.spring.io/), qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).

Ce tutoriel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une application Java à l’aide de Spring Initializr
> * Configurer Azure Active Directory B2C
> * Sécuriser l’application avec des classes et annotations Spring Boot
> * Générer et tester votre application Java

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-an-app-using-spring-initializr"></a>Créer une application à l’aide de Spring Initialzr

1. Accédez à <https://start.spring.io/>.

2. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis sélectionnez les modules **Web** et **Security** de Spring Initializr.

   ![Spécifiez les noms de groupes et d’artefacts.](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/SI.png)


3. Cliquez sur `Generate Project` et téléchargez le projet sur votre ordinateur local à l’invite.

## <a name="create-azure-active-directory-instance"></a>Créer une instance Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Créer l’instance Azure Active Directory

1. Connectez-vous à <https://portal.azure.com>.

2. Cliquez sur **+Créer une ressource**, sur **Identité**, puis sur **Azure Active Directory B2C**.

   ![Créer une instance Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ1.png)

3. Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**, spécifiez `${your-tenant-name}` comme **nom de domaine**, puis cliquez sur **Créer**.

   ![Obtenir le nom de votre locataire B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ5.png)

4. Sélectionnez le nom de votre compte dans le coin supérieur droit de la barre d’outils du portail Azure, puis cliquez sur **Changer de répertoire**.

   ![Choisir votre instance Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ2.png)

5. Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant.

   ![Choisir votre instance Azure Active Directory](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ3.png)

6. Recherchez `b2c` et cliquez sur le service `Azure AD B2C`.

   ![Rechercher l’instance Azure Active Directory B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/AZ4.png)

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Ajouter une inscription d’application pour votre application Spring Boot

1. Sélectionnez **Azure AD B2C** dans le menu du portail, cliquez sur **Applications**, puis sur **Ajouter**.

   ![Ajouter une inscription d’application](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C1.png)

2. Spécifiez le **Nom** de votre application, ajoutez `http://localhost:8080/home` pour l’**URL de réponse**, spécifiez votre `${your-client-id}` comme **ID d’application**, puis cliquez sur **Enregistrer**.

   ![Ajouter une URL de réponse d’application](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C2.png)

3. Sélectionnez **Clés** à partir de votre application, cliquez sur **Générer une clé** pour générer `${your-client-secret}`, puis cliquez sur **Enregistrer**.

4. Sélectionnez **Flux d’utilisateurs** à gauche, puis **cliquez sur** **Nouveau flux d’utilisateur **.

   ![Créer un flux d’utilisateur](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C3.png)

5. Choisissez **S’inscrire ou se connecter**, **Modification de profil** et **Réinitialisation du mot de passe** pour créer les flux d’utilisateurs respectifs. Spécifiez le **Nom** et les **Attributs utilisateur et revendications** de votre flux d’utilisateur, puis cliquez sur **Créer**.

   ![Configurer un flux d’utilisateur](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/B2C4.png)

## <a name="configure-and-compile-your-app"></a>Configurer et compiler votre application

1. Extrayez les fichiers des archives du projet que vous avez créées et téléchargées précédemment dans ce tutoriel dans un répertoire.

2. Accédez au dossier parent pour votre projet, puis ouvrez le fichier de projet Maven `pom.xml` dans un éditeur de texte.

3. Ajoutez les dépendances associées à la sécurité Spring OAuth2 au fichier `pom.xml` :

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

4. Enregistrez et fermez le fichier *pom.xml*.

5. Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.yml* dans un éditeur de texte.

6. Spécifiez les paramètres pour l’inscription de votre application en utilisant les valeurs que vous avez créé précédemment ; par exemple :

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
   Où :

   | Paramètre | Description |
   |---|---|
   | `azure.activedirectory.b2c.tenant` | Contient la valeur `${your-tenant-name` de votre AD B2C indiquée précédemment. |
   | `azure.activedirectory.b2c.client-id` | Contient la valeur `${your-client-id}` de votre application indiquée précédemment. |
   | `azure.activedirectory.b2c.client-secret` | Contient la valeur `${your-client-secret}` de votre application indiquée précédemment. |
   | `azure.activedirectory.b2c.reply-url` | Contient l’une des **URL de réponse** de votre application indiquées précédemment. |
   | `azure.activedirectory.b2c.logout-success-url` | Spécifiez l’URL quand votre application se déconnecte avec succès. |
   | `azure.activedirectory.b2c.user-flows` | Contient les noms des flux d’utilisateurs que vous avez spécifiés plus haut.

   > [!NOTE]
   > 
   > Pour une liste complète des valeurs disponibles dans votre fichier *application.yml*, consultez l’[exemple Spring Boot Azure Active Directory B2C][exemple Spring Boot AAD B2C] sur GitHub.
   >

7. Enregistrez et fermez le fichier *application.yml*.

8. Créez un dossier nommé *controller* dans le dossier source Java pour votre application.

9. Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.

10. Entrez le code suivant, puis enregistrez et fermez le fichier :

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

11. Créez un dossier nommé *security* dans le dossier source Java pour votre application.

12. Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.

13. Entrez le code suivant, puis enregistrez et fermez le fichier :

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
14. Copiez les fichiers `greeting.html` et `home.html` de l’[exemple Spring Boot Azure AD B2C](https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-b2c-oidc-spring-boot-sample/src/main/resources/templates) et remplacez `${your-profile-edit-user-flow}` et `${your-password-reset-user-flow}` par les noms respectifs de vos flux d’utilisateurs indiqués plus haut.

## <a name="build-and-test-your-app"></a>Générer et tester votre application

1. Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.

2. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

3. Une fois que votre application est créée et démarrée dans Maven, ouvrez <http://localhost:8080/> dans un navigateur web ; vous devez être redirigé vers la page de connexion.

   ![Page de connexion](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO1.png)

4. Cliquez sur le lien avec le nom du flux d’utilisateur `${your-sign-up-or-in}` ; vous devez être redirigé vers Azure AD B2C pour démarrer le processus d’authentification.

   ![Connexion à Azure AD B2C](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO2.png)

4. Une fois connecté, vous devez voir l’exemple `home page` dans le navigateur,

   ![Connexion réussie](media/configure-spring-boot-starter-java-app-with-azure-active-directory-b2c-oidc/LO3.png)

## <a name="summary"></a>Résumé

Dans ce tutoriel, vous avez crée une application web Java avec l’application de démarrage Azure Active Directory B2C, configuré un nouveau locataire Azure AD B2C et inscrit une nouvelle application, avant de configurer votre application pour utiliser les annotations et classes Spring pour protéger l’application web.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)
