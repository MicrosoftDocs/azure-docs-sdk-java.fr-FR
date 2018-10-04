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
ms.date: 07/02/2018
ms.devlang: java
ms.service: active-directory
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: d3b6bdc4aaae79864d370c581585167cf3732160
ms.sourcegitcommit: bb7286fad75a2bb43e6ce1a8f1b09e701147c9f9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48047179"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a>Comment utiliser Spring Boot Starter pour Azure Active Directory

## <a name="overview"></a>Vue d’ensemble

Cet article illustre la création d’une application avec **[Spring Initializr]** qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).

## <a name="prerequisites"></a>Prérequis

Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-a-custom-application-using-the-spring-initializr"></a>Créer une application personnalisée à l’aide de Spring Initializr

1. Accédez à <https://start.spring.io/>.

1. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.

   ![Spécifiez les noms de groupes et d’artefacts.][security-01]

1. Faites défiler jusqu’à la section **Core** (Principal), cochez la case en regard de **Security** (Sécurité), puis dans la section **Web** (Web) cochez la case **Web** (web).

   ![Sélectionner les applications web et de sécurité][security-02]

1. Faites défiler jusqu’à la section **Azure**, puis cochez la case en regard de **Azure Active Directory**.

   ![Sélectionner l’application de démarrage Azure Active Security][security-03]

1. Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.

   ![Générez le projet Spring Boot.][security-04]

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a>Créer et configurer une instance Azure Active Directory

### <a name="create-the-active-directory-instance"></a>Créer l’instance Azure Active Directory

1. Connectez-vous à <https://portal.azure.com>.

1. Cliquez sur **+Nouveau**, puis sur **Sécurité + Identité** et enfin sur **Azure Active Directory**.

   ![Créer une instance Azure Active Directory][directory-01]

1. Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**. Copier l’URL complète de votre répertoire ; vous allez l’utiliser pour ajouter des comptes d’utilisateur plus tard dans ce tutoriel. (Par exemple : `wingtiptoysdirectory.onmicrosoft.com`.) Une fois que vous avez terminé, cliquez sur **Créer**.

   ![Spécifier des noms Azure Active Directory][directory-02]

1. Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant de la barre d’outils située en haut du portail Azure.

   ![Choisir votre instance Azure Active Directory][directory-03]

1. Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Propriétés**, et copiez l’**ID d’annuaire** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.

   ![Copier votre ID Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a>Ajouter une inscription d’application pour votre application Spring Boot

1. Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Vue d’ensemble**, puis sur **Inscriptions des applications**.

   ![Ajouter une inscription d’application][directory-04]

1. Cliquez sur **Nouvelle inscription d’application**, spécifiez le **Nom** de votre application, utilisez http://localhost:8080 en tant qu’**URL de connexion**, puis cliquez sur **Créer**.

   ![Créer une inscription d’application][directory-05]

1. Cliquez sur l’inscription d’application une fois cette dernière créée.

   ![Sélectionner votre inscription d’application][directory-06]

1. Lorsque la page pour l’inscription de votre application s’affiche, copiez votre **ID d’application** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel. Cliquez sur **Paramètres**, puis sur **Clés**.

   ![Créer des clés d’inscription d’application][directory-07]

1. Ajoutez une **Description**, spécifiez la **Durée** d’une nouvelle clé, puis cliquez sur **Enregistrer** ; la valeur de la clé est automatiquement renseignée lorsque vous cliquez sur l’icône **Enregistrer**, vous devez copier la valeur de la clé pour configurer votre fichier *application.properties* plus tard dans ce tutoriel. (Il ne vous sera pas possible de récupérer cette valeur plus tard.)

   ![Spécifier les paramètres de la clé d’inscription d’application][directory-08]

1. Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **Autorisations requises**.

   ![Autorisations requises de l’inscription d’application][directory-09]

1. Cliquez sur **Windows Azure Active Directory**.

   ![Sélectionner Windows Azure Active Directory][directory-10]

1. Cochez les cases en regard de **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**, puis cliquez sur **Enregistrer**.

   ![Activer les autorisations d’accès][directory-11]

1. Sur la page **Autorisations requises**, cliquez sur **Accorder les autorisations**, puis cliquez sur **Oui** à l’invite.

   ![Accorder les autorisations d’accès][directory-12]

1. Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **URL de réponse**.

   ![Modifier les URL de réponse][directory-14]

1. Saisissez la nouvelle URL de réponse « http://localhost:8080/login/oauth2/code/azure », puis cliquez sur **Enregistrer**.

   ![Ajouter une nouvelle URL de réponse][directory-15]

1. Dans la page principale de l’inscription de votre application, cliquez sur **Manifeste**, définissez la valeur du paramètre `oauth2AllowImplicitFlow` sur `true`, puis cliquez sur **Enregistrer**.

   ![Configurer le manifeste de l’application][directory-16]

   > [!NOTE]
   > 
   > Pour plus d’informations sur le paramètre `oauth2AllowImplicitFlow` et les autres paramètres d’applications, consultez [Manifeste de l’application Azure Active Directory][AAD app manifest]. 
   >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a>Ajouter un compte d’utilisateur à votre répertoire et ajouter ce compte à un groupe

1. À partir de la page **Vue d’ensemble** de votre répertoire Active Directory, cliquez sur **Utilisateurs**.

   ![Ouvrir l’outil Utilisateurs][directory-17]

1. Lorsque le panneau **Utilisateurs** s’affiche, cliquez sur **Nouvel utilisateur**.

   ![Ajouter un compte d’utilisateur][directory-18]

1. Lorsque le panneau **Utilisateur** s’affiche, entrez le **Nom** et le **Nom d’utilisateur**.

   ![Entrer les informations sur le compte d’utilisateur][directory-19]

   > [!NOTE]
   > 
   > Vous devez spécifier l’URL de votre répertoire plus tôt dans ce tutoriel lorsque vous entrez le nom d’utilisateur ; par exemple :
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. Cliquez sur **Groupes**, puis sélectionnez les groupes que vous allez utiliser pour l’autorisation dans votre application, puis cliquez sur **Sélectionner**. (Dans le cadre de ce tutoriel, ajoutez le compte au groupe d’_Utilisateurs_.)

   ![Sélectionner les groupes d’utilisateur][directory-20]

1. Cliquez sur **Afficher le mot de passe** et copiez le mot de passe ; vous l’utiliserez lorsque vous vous connecterez à votre application plus tard dans ce tutoriel.

   ![Afficher le mot de passe][directory-21]

1. Cliquez sur **Créer** pour ajouter le nouveau compte d’utilisateur à votre répertoire.

   ![Créer le nouveau compte d’utilisateur][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurer et compiler votre application Spring Boot

1. Extrayez les fichiers des archives du projet que vous avez créées et téléchargées précédemment dans ce tutoriel dans un répertoire.

1. Accédez au dossier parent pour votre projet, puis ouvrez le fichier *pom.xml* dans un éditeur de texte.

1. Ajoutez la dépendance associée à la sécurité Spring OAuth2, par exemple :

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

   > [!NOTE]
   > 
   > Vous pouvez spécifier différents paramètres d’autorisation pour différents mappages de requêtes ; par exemple :
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

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur Azure Active Directory, consultez les articles suivants :

* [Documentation Azure Active Directory]

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].

**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise. L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes. Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>. En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.

Pour un exemple plus détaillé, consultez la page [Azure Active Directory Spring Boot Sample] [ AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.

<!-- URL List -->

[Documentation Azure Active Directory]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure pour les développeurs Java]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
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
[directory-16]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-16.png
[directory-17]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-17.png
[directory-18]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-18.png
[directory-19]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-19.png
[directory-20]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-20.png
[directory-21]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-21.png
[directory-22]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/directory-22.png

[application-login]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/application-login.png
[build-application]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/build-application.png
[hello-world]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/hello-world.png
[update-password]: media/configure-spring-boot-starter-java-app-with-azure-active-directory/update-password.png
