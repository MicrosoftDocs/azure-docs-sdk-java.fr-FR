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
ms.date: 11/21/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 89e294fa739b59f87667f901e914fd5f050b5b8c
ms.sourcegitcommit: 8d0c59ae7c91adbb9be3c3e6d4a3429ffe51519d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52338773"
---
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a>Tutoriel : sécuriser une application web Java avec Spring Boot Starter pour Azure Active Directory

## <a name="overview"></a>Vue d’ensemble

Cet article illustre la création d’une application Java avec **[Spring Initializr]** qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).

Ce tutoriel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une application Java à l’aide de Spring Initializr
> * Configurer Azure Active Directory
> * Sécuriser l’application avec des classes et annotations Spring Boot
> * Générer et tester votre application Java

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un kit de développement Java (JDK) pris en charge. Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-an-app-using-spring-initializr"></a>Créer une application à l’aide de Spring Initialzr

1. Accédez à <https://start.spring.io/>.

1. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.

   ![Spécifiez les noms de groupes et d’artefacts.][create-spring-app-01]

1. Faites défiler jusqu’à la section **Core** et cochez la case **Sécurité**. Dans la section **Web**, cochez **Web**, puis faites défiler jusqu’à la section **Azure** et cochez **Azure Active Directory**.

   ![Sélectionner les starters Security, Web et Azure Active Directory][create-spring-app-02]

1. Faites défiler jusqu’en bas ou en haut de la page, puis cliquez sur le bouton pour **générer le projet**.

   ![Générez le projet Spring Boot.][create-spring-app-03]

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

## <a name="create-azure-active-directory-instance"></a>Créer une instance Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Créer l’instance Azure Active Directory

1. Connectez-vous à <https://portal.azure.com>.

1. Cliquez sur **+Créer une ressource**, puis sur **Identité** et enfin sur **Azure Active Directory**.

   ![Créer une instance Azure Active Directory][create-directory-01]

1. Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**. Copier l’URL complète de votre répertoire ; vous allez l’utiliser pour ajouter des comptes d’utilisateur plus tard dans ce tutoriel. (Par exemple : `wingtiptoysdirectory.onmicrosoft.com`.) Une fois que vous avez terminé, cliquez sur **Créer**.

   ![Spécifier des noms Azure Active Directory][create-directory-02]

1. Sélectionnez le nom de votre compte dans le coin supérieur droit de la barre d’outils du portail Azure, puis cliquez sur **Changer de répertoire**.

   ![Sélectionner le nom de votre compte Azure][create-directory-03]

1. Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant.

   ![Choisir votre instance Azure Active Directory][create-directory-04]

1. Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Propriétés**, et copiez l’**ID d’annuaire** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.

   ![Copier votre ID Azure Active Directory][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Ajouter une inscription d’application pour votre application Spring Boot

1. Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Inscriptions des applications**, puis sur **Nouvelle inscription d’application**.

   ![Ajouter une inscription d’application][create-app-registration-01]

2. Spécifiez le **Nom** de votre application, utilisez http://localhost:8080 en tant qu’**URL de connexion**, puis cliquez sur **Créer**.

   ![Créer une inscription d’application][create-app-registration-02]

4. Lorsque la page pour l’inscription de votre application s’affiche, copiez votre **ID d’application** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel. Cliquez sur **Paramètres**, puis sur **Clés**.

   ![Créer des clés d’inscription d’application][create-app-registration-03]

5. Ajoutez une **Description**, spécifiez la **Durée** d’une nouvelle clé, puis cliquez sur **Enregistrer** ; la valeur de la clé est automatiquement renseignée lorsque vous cliquez sur l’icône **Enregistrer**, vous devez copier la valeur de la clé pour configurer votre fichier *application.properties* plus tard dans ce tutoriel. (Il ne vous sera pas possible de récupérer cette valeur plus tard.)

   ![Spécifier les paramètres de la clé d’inscription d’application][create-app-registration-04]

6. Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **Autorisations requises**.

   ![Autorisations requises de l’inscription d’application][create-app-registration-05]

7. Cliquez sur **Windows Azure Active Directory**.

   ![Sélectionner Windows Azure Active Directory][create-app-registration-06]

8. Cochez les cases en regard de **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**, puis cliquez sur **Enregistrer**.

   ![Activer les autorisations d’accès][create-app-registration-07]

9. Sur la page **Autorisations requises**, cliquez sur **Accorder les autorisations**, puis cliquez sur **Oui** à l’invite.

   ![Accorder les autorisations d’accès][create-app-registration-08]

10. Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **URL de réponse**.

    ![Modifier les URL de réponse][create-app-registration-09]

11. Saisissez la nouvelle URL de réponse « <http://localhost:8080/login/oauth2/code/azure> », puis cliquez sur **Enregistrer**.

    ![Ajouter une nouvelle URL de réponse][create-app-registration-10]

12. Dans la page principale de l’inscription de votre application, cliquez sur **Manifeste**, définissez la valeur du paramètre `oauth2AllowImplicitFlow` sur `true`, puis cliquez sur **Enregistrer**.

    ![Configurer le manifeste de l’application][create-app-registration-11]

    > [!NOTE]
    > 
    > Pour plus d’informations sur le paramètre `oauth2AllowImplicitFlow` et les autres paramètres d’applications, consultez [Manifeste de l’application Azure Active Directory][AAD app manifest]. 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>Ajouter un compte d’utilisateur à votre répertoire et ajouter ce compte à un groupe

1. À partir de la page **Vue d’ensemble** de votre répertoire Active Directory, cliquez sur **Tous les utilisateurs**, puis sur **Nouvel utilisateur**.

   ![Ajouter un compte d’utilisateur][create-user-01]

1. Lorsque le panneau **Utilisateur** s’affiche, entrez le **Nom** et le **Nom d’utilisateur**.

   ![Entrer les informations sur le compte d’utilisateur][create-user-02]

   > [!NOTE]
   > 
   > Vous devez spécifier l’URL de votre répertoire plus tôt dans ce tutoriel lorsque vous entrez le nom d’utilisateur ; par exemple :
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. Cliquez sur **Groupes**, puis sélectionnez les groupes que vous allez utiliser pour l’autorisation dans votre application, puis cliquez sur **Sélectionner**. (Dans le cadre de ce tutoriel, ajoutez le compte au groupe d’_Utilisateurs_.)

   ![Sélectionner les groupes d’utilisateur][create-user-03]

1. Cliquez sur **Afficher le mot de passe** et copiez le mot de passe ; vous l’utiliserez lorsque vous vous connecterez à votre application plus tard dans ce tutoriel. Une fois le mot de passe copié, cliquez sur **Créer** pour ajouter le nouveau compte d’utilisateur à votre répertoire.

   ![Afficher le mot de passe][create-user-04]

## <a name="configure-and-compile-your-app"></a>Configurer et compiler votre application

1. Extrayez les fichiers des archives du projet que vous avez créées et téléchargées précédemment dans ce tutoriel dans un répertoire.

1. Accédez au dossier parent pour votre projet, puis ouvrez le fichier de projet Maven `pom.xml` dans un éditeur de texte.

1. Ajoutez les dépendances associées à la sécurité Spring OAuth2 au fichier `pom.xml` :

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

1. Enregistrez et fermez le fichier *pom.xml*.

1. Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.

1. Spécifiez les paramètres pour l’inscription de votre application en utilisant les valeurs que vous avez créé précédemment ; par exemple :

   ```yaml
   # Specifies your Active Directory ID:
   azure.activedirectory.tenant-id=22222222-2222-2222-2222-222222222222

   # Specifies your App Registration's Application ID:
   spring.security.oauth2.client.registration.azure.client-id=11111111-1111-1111-1111-1111111111111111

   # Specifies your App Registration's secret key:
   spring.security.oauth2.client.registration.azure.client-secret=AbCdEfGhIjKlMnOpQrStUvWxYz==

   # Specifies the list of Active Directory groups to use for authorization:
   azure.activedirectory.active-directory-groups=Users
   ```
   Où :

   | Paramètre | Description |
   |---|---|
   | `azure.activedirectory.tenant-id` | Contient l’**ID du répertoire** d’Active Directory vu précédemment. |
   | `spring.security.oauth2.client.registration.azure.client-id` | Contient l’**ID de l’application** de votre inscription d’application exécutée précédemment. |
   | `spring.security.oauth2.client.registration.azure.client-secret` | Contient la **Valeur** de votre clé d’inscription d’application exécutée précédemment. |
   | `azure.activedirectory.active-directory-groups` | Contient une liste des groupes Active Directory à utiliser pour l’autorisation. |

   > [!NOTE]
   > 
   > Pour obtenir une liste complète des valeurs disponibles dans votre fichier *application.properties*, consultez [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.
   >

1. Enregistrez et fermez le fichier *application.properties*.

1. Créez un dossier nommé *controller* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/controller*.

1. Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.

1. Entrez le code suivant, puis enregistrez et fermez le fichier :

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
   > Le nom de groupe spécifié pour la méthode `@PreAuthorize("hasRole('')")` doit contenir l’un des groupes spécifiés dans le champ `azure.activedirectory.active-directory-groups` de votre fichier *application.properties*.
   > 
   > Vous pouvez aussi spécifier différents paramètres d’autorisation pour différents mappages de requêtes ; par exemple :
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

1. Créez un dossier nommé *security* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/security*.

1. Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.

1. Entrez le code suivant, puis enregistrez et fermez le fichier :

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

## <a name="build-and-test-your-app"></a>Générer et tester votre application

1. Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.

1. Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Générer votre application][build-application]

1. Une fois que votre application est créée et démarrée dans Maven, ouvrez <http://localhost:8080> dans un navigateur web ; vous devez fournir un nom d’utilisateur et le mot de passe.

   ![Se connecter à l’application][application-login]

   > [!NOTE]
   > 
   > Vous pouvez être invité à modifier votre mot de passe, s’il s’agit de la première connexion à un nouveau compte d’utilisateur.
   > 
   > ![Modifier votre mot de passe][update-password]
   > 

1. Une fois que vous vous êtes connecté avec succès, vous devez voir le contrôleur afficher l’exemple de texte « Hello World ».

   ![Connexion réussie][hello-world]

   > [!NOTE]
   > 
   > Les comptes d’utilisateur qui ne sont pas autorisés recevront un message **HTTP 403 non autorisé**.
   >

## <a name="summary"></a>Résumé

Dans ce tutoriel, vous avez crée une application web Java avec le starter Azure Active Directory, configuré un nouveau locataire Azure AD et inscrit une nouvelle application, avant de configurer votre application pour utiliser les annotations et classes Spring pour protéger l’application web.

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

<!-- URL List -->

[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure for Java Developers]: /java/azure/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[AAD Spring Boot Sample]: https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-backend-sample

<!-- IMG List -->

[create-spring-app-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-01.png
[create-spring-app-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-02.png
[create-spring-app-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-spring-app-03.png

[create-directory-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-01.png
[create-directory-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-02.png
[create-directory-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-03.png
[create-directory-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-04.png
[create-directory-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-directory-05.png

[create-app-registration-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-01.png
[create-app-registration-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-02.png
[create-app-registration-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-03.png
[create-app-registration-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-04.png
[create-app-registration-05]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-05.png
[create-app-registration-06]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-06.png
[create-app-registration-07]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-07.png
[create-app-registration-08]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-08.png
[create-app-registration-09]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-09.png
[create-app-registration-10]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-10.png
[create-app-registration-11]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-app-registration-11.png

[create-user-01]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-01.png
[create-user-02]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-02.png
[create-user-03]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-03.png
[create-user-04]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/create-user-04.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
