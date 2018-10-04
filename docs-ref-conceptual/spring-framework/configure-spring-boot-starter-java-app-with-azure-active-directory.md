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
# <a name="how-to-use-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="057bc-103">Comment utiliser Spring Boot Starter pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="057bc-103">How to use the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="057bc-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="057bc-104">Overview</span></span>

<span data-ttu-id="057bc-105">Cet article illustre la création d’une application avec **[Spring Initializr]** qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="057bc-105">This article demonstrates creating an app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="057bc-106">Prérequis</span><span class="sxs-lookup"><span data-stu-id="057bc-106">Prerequisites</span></span>

<span data-ttu-id="057bc-107">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="057bc-107">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="057bc-108">Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].</span><span class="sxs-lookup"><span data-stu-id="057bc-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="057bc-109">Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="057bc-109">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>
* <span data-ttu-id="057bc-110">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="057bc-110">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-custom-application-using-the-spring-initializr"></a><span data-ttu-id="057bc-111">Créer une application personnalisée à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="057bc-111">Create a custom application using the Spring Initializr</span></span>

1. <span data-ttu-id="057bc-112">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="057bc-112">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="057bc-113">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="057bc-113">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Spécifiez les noms de groupes et d’artefacts.][security-01]

1. <span data-ttu-id="057bc-115">Faites défiler jusqu’à la section **Core** (Principal), cochez la case en regard de **Security** (Sécurité), puis dans la section **Web** (Web) cochez la case **Web** (web).</span><span class="sxs-lookup"><span data-stu-id="057bc-115">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**.</span></span>

   ![Sélectionner les applications web et de sécurité][security-02]

1. <span data-ttu-id="057bc-117">Faites défiler jusqu’à la section **Azure**, puis cochez la case en regard de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="057bc-117">Scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Sélectionner l’application de démarrage Azure Active Security][security-03]

1. <span data-ttu-id="057bc-119">Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="057bc-119">Scroll to the bottom of the page and click the button to **Generate Project**.</span></span>

   ![Générez le projet Spring Boot.][security-04]

1. <span data-ttu-id="057bc-121">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="057bc-121">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-and-configure-a-new-azure-active-directory-instance"></a><span data-ttu-id="057bc-122">Créer et configurer une instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="057bc-122">Create and configure a new Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="057bc-123">Créer l’instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="057bc-123">Create the Active Directory instance</span></span>

1. <span data-ttu-id="057bc-124">Connectez-vous à <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="057bc-124">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="057bc-125">Cliquez sur **+Nouveau**, puis sur **Sécurité + Identité** et enfin sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="057bc-125">Click **+New**, then **Security + Identity**, and then **Azure Active Directory**.</span></span>

   ![Créer une instance Azure Active Directory][directory-01]

1. <span data-ttu-id="057bc-127">Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**.</span><span class="sxs-lookup"><span data-stu-id="057bc-127">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="057bc-128">Copier l’URL complète de votre répertoire ; vous allez l’utiliser pour ajouter des comptes d’utilisateur plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="057bc-128">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="057bc-129">(Par exemple : `wingtiptoysdirectory.onmicrosoft.com`.) Une fois que vous avez terminé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="057bc-129">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Spécifier des noms Azure Active Directory][directory-02]

1. <span data-ttu-id="057bc-131">Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant de la barre d’outils située en haut du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="057bc-131">Select your new Azure Active Directory from the drop-down menu on the top toolbar of the Azure portal.</span></span>

   ![Choisir votre instance Azure Active Directory][directory-03]

1. <span data-ttu-id="057bc-133">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Propriétés**, et copiez l’**ID d’annuaire** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="057bc-133">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Copier votre ID Azure Active Directory][directory-13]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="057bc-135">Ajouter une inscription d’application pour votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="057bc-135">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="057bc-136">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Vue d’ensemble**, puis sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="057bc-136">Select **Azure Active Directory** from the portal menu, click **Overview**, and then click **App registrations**.</span></span>

   ![Ajouter une inscription d’application][directory-04]

1. <span data-ttu-id="057bc-138">Cliquez sur **Nouvelle inscription d’application**, spécifiez le **Nom** de votre application, utilisez http://localhost:8080 en tant qu’**URL de connexion**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="057bc-138">Click **New application registration**, specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Créer une inscription d’application][directory-05]

1. <span data-ttu-id="057bc-140">Cliquez sur l’inscription d’application une fois cette dernière créée.</span><span class="sxs-lookup"><span data-stu-id="057bc-140">Click your application registration after it has been created.</span></span>

   ![Sélectionner votre inscription d’application][directory-06]

1. <span data-ttu-id="057bc-142">Lorsque la page pour l’inscription de votre application s’affiche, copiez votre **ID d’application** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="057bc-142">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="057bc-143">Cliquez sur **Paramètres**, puis sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="057bc-143">Click **Settings**, and then click **Keys**.</span></span>

   ![Créer des clés d’inscription d’application][directory-07]

1. <span data-ttu-id="057bc-145">Ajoutez une **Description**, spécifiez la **Durée** d’une nouvelle clé, puis cliquez sur **Enregistrer** ; la valeur de la clé est automatiquement renseignée lorsque vous cliquez sur l’icône **Enregistrer**, vous devez copier la valeur de la clé pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="057bc-145">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="057bc-146">(Il ne vous sera pas possible de récupérer cette valeur plus tard.)</span><span class="sxs-lookup"><span data-stu-id="057bc-146">(You will not be able to retrieve this value later.)</span></span>

   ![Spécifier les paramètres de la clé d’inscription d’application][directory-08]

1. <span data-ttu-id="057bc-148">Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="057bc-148">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Autorisations requises de l’inscription d’application][directory-09]

1. <span data-ttu-id="057bc-150">Cliquez sur **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="057bc-150">Click **Windows Azure Active Directory**.</span></span>

   ![Sélectionner Windows Azure Active Directory][directory-10]

1. <span data-ttu-id="057bc-152">Cochez les cases en regard de **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="057bc-152">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Activer les autorisations d’accès][directory-11]

1. <span data-ttu-id="057bc-154">Sur la page **Autorisations requises**, cliquez sur **Accorder les autorisations**, puis cliquez sur **Oui** à l’invite.</span><span class="sxs-lookup"><span data-stu-id="057bc-154">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Accorder les autorisations d’accès][directory-12]

1. <span data-ttu-id="057bc-156">Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="057bc-156">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

   ![Modifier les URL de réponse][directory-14]

1. <span data-ttu-id="057bc-158">Saisissez la nouvelle URL de réponse « http://localhost:8080/login/oauth2/code/azure », puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="057bc-158">Enter "http://localhost:8080/login/oauth2/code/azure" as a new reply URL, and then click **Save**.</span></span>

   ![Ajouter une nouvelle URL de réponse][directory-15]

1. <span data-ttu-id="057bc-160">Dans la page principale de l’inscription de votre application, cliquez sur **Manifeste**, définissez la valeur du paramètre `oauth2AllowImplicitFlow` sur `true`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="057bc-160">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

   ![Configurer le manifeste de l’application][directory-16]

   > [!NOTE]
   > 
   > <span data-ttu-id="057bc-162">Pour plus d’informations sur le paramètre `oauth2AllowImplicitFlow` et les autres paramètres d’applications, consultez [Manifeste de l’application Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="057bc-162">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
   >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="057bc-163">Ajouter un compte d’utilisateur à votre répertoire et ajouter ce compte à un groupe</span><span class="sxs-lookup"><span data-stu-id="057bc-163">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="057bc-164">À partir de la page **Vue d’ensemble** de votre répertoire Active Directory, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="057bc-164">From the **Overview** page of your Active Directory, click **Users**.</span></span>

   ![Ouvrir l’outil Utilisateurs][directory-17]

1. <span data-ttu-id="057bc-166">Lorsque le panneau **Utilisateurs** s’affiche, cliquez sur **Nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="057bc-166">When the **Users** panel is displayed, click **New user**.</span></span>

   ![Ajouter un compte d’utilisateur][directory-18]

1. <span data-ttu-id="057bc-168">Lorsque le panneau **Utilisateur** s’affiche, entrez le **Nom** et le **Nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="057bc-168">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Entrer les informations sur le compte d’utilisateur][directory-19]

   > [!NOTE]
   > 
   > <span data-ttu-id="057bc-170">Vous devez spécifier l’URL de votre répertoire plus tôt dans ce tutoriel lorsque vous entrez le nom d’utilisateur ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="057bc-170">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="057bc-171">Cliquez sur **Groupes**, puis sélectionnez les groupes que vous allez utiliser pour l’autorisation dans votre application, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="057bc-171">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="057bc-172">(Dans le cadre de ce tutoriel, ajoutez le compte au groupe d’_Utilisateurs_.)</span><span class="sxs-lookup"><span data-stu-id="057bc-172">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Sélectionner les groupes d’utilisateur][directory-20]

1. <span data-ttu-id="057bc-174">Cliquez sur **Afficher le mot de passe** et copiez le mot de passe ; vous l’utiliserez lorsque vous vous connecterez à votre application plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="057bc-174">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span>

   ![Afficher le mot de passe][directory-21]

1. <span data-ttu-id="057bc-176">Cliquez sur **Créer** pour ajouter le nouveau compte d’utilisateur à votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="057bc-176">Click **Create** to add the new user account to your directory.</span></span>

   ![Créer le nouveau compte d’utilisateur][directory-22]

## <a name="configure-and-compile-your-spring-boot-application"></a><span data-ttu-id="057bc-178">Configurer et compiler votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="057bc-178">Configure and compile your Spring Boot application</span></span>

1. <span data-ttu-id="057bc-179">Extrayez les fichiers des archives du projet que vous avez créées et téléchargées précédemment dans ce tutoriel dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="057bc-179">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="057bc-180">Accédez au dossier parent pour votre projet, puis ouvrez le fichier *pom.xml* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="057bc-180">Navigate to the parent folder for your project, and open the *pom.xml* file in a text editor.</span></span>

1. <span data-ttu-id="057bc-181">Ajoutez la dépendance associée à la sécurité Spring OAuth2, par exemple :</span><span class="sxs-lookup"><span data-stu-id="057bc-181">Add the dependencies for Spring OAuth2 security; for example:</span></span>

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

1. <span data-ttu-id="057bc-182">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="057bc-182">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="057bc-183">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="057bc-183">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="057bc-184">Spécifiez les paramètres pour l’inscription de votre application en utilisant les valeurs que vous avez créé précédemment ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="057bc-184">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="057bc-185">Où :</span><span class="sxs-lookup"><span data-stu-id="057bc-185">Where:</span></span>

   | <span data-ttu-id="057bc-186">Paramètre</span><span class="sxs-lookup"><span data-stu-id="057bc-186">Parameter</span></span> | <span data-ttu-id="057bc-187">Description</span><span class="sxs-lookup"><span data-stu-id="057bc-187">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="057bc-188">Contient l’**ID du répertoire** d’Active Directory vu précédemment.</span><span class="sxs-lookup"><span data-stu-id="057bc-188">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="057bc-189">Contient l’**ID de l’application** de votre inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="057bc-189">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="057bc-190">Contient la **Valeur** de votre clé d’inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="057bc-190">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="057bc-191">Contient une liste des groupes Active Directory à utiliser pour l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="057bc-191">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="057bc-192">Pour obtenir une liste complète des valeurs disponibles dans votre fichier *application.properties*, consultez [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="057bc-192">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="057bc-193">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="057bc-193">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="057bc-194">Créez un dossier nommé *controller* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="057bc-194">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="057bc-195">Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="057bc-195">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="057bc-196">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="057bc-196">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="057bc-197">Le nom de groupe spécifié pour la méthode `@PreAuthorize("hasRole('')")` doit contenir l’un des groupes spécifiés dans le champ `azure.activedirectory.active-directory-groups` de votre fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="057bc-197">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   >

   > [!NOTE]
   > 
   > <span data-ttu-id="057bc-198">Vous pouvez spécifier différents paramètres d’autorisation pour différents mappages de requêtes ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="057bc-198">You can specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="057bc-199">Créez un dossier nommé *security* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="057bc-199">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="057bc-200">Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="057bc-200">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="057bc-201">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="057bc-201">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="057bc-202">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="057bc-202">Build and test your app</span></span>

1. <span data-ttu-id="057bc-203">Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.</span><span class="sxs-lookup"><span data-stu-id="057bc-203">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="057bc-204">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="057bc-204">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Générer votre application][build-application]

1. <span data-ttu-id="057bc-206">Une fois que votre application est créée et démarrée dans Maven, ouvrez <http://localhost:8080> dans un navigateur web ; vous devez fournir un nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="057bc-206">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Se connecter à l’application][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="057bc-208">Vous pouvez être invité à modifier votre mot de passe, s’il s’agit de la première connexion à un nouveau compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="057bc-208">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Modifier votre mot de passe][update-password]
   > 

1. <span data-ttu-id="057bc-210">Une fois que vous vous êtes connecté avec succès, vous devez voir le contrôleur afficher l’exemple de texte « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="057bc-210">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Connexion réussie][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="057bc-212">Les comptes d’utilisateur qui ne sont pas autorisés recevront un message **HTTP 403 non autorisé**.</span><span class="sxs-lookup"><span data-stu-id="057bc-212">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="057bc-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="057bc-213">Next steps</span></span>

<span data-ttu-id="057bc-214">Pour plus d’informations sur Azure Active Directory, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="057bc-214">For more information about using Azure Active Directory, see the following articles:</span></span>

* <span data-ttu-id="057bc-215">[Documentation Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="057bc-215">[Azure Active Directory Documentation].</span></span>

<span data-ttu-id="057bc-216">Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="057bc-216">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="057bc-217">Déployer une application Spring Boot sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="057bc-217">Deploy a Spring Boot Application to the Azure App Service</span></span>](deploy-spring-boot-java-web-app-on-azure.md)

* [<span data-ttu-id="057bc-218">Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="057bc-218">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](deploy-spring-boot-java-app-on-kubernetes.md)

<span data-ttu-id="057bc-219">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="057bc-219">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="057bc-220">**[Spring Framework]** est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="057bc-220">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="057bc-221">L’un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="057bc-221">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="057bc-222">Pour aider les développeurs à bien démarrer avec Spring Boot, plusieurs exemples de packages Spring Boot sont disponibles à l’adresse <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="057bc-222">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="057bc-223">En plus de choisir dans la liste des projets Spring Boot de base, **[Spring Initializr]** aide les développeurs à commencer à créer des applications Spring Boot personnalisées.</span><span class="sxs-lookup"><span data-stu-id="057bc-223">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="057bc-224">Pour un exemple plus détaillé, consultez la page [Azure Active Directory Spring Boot Sample] [ AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="057bc-224">For a more-detailed sample, see the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>

<!-- URL List -->

[Documentation Azure Active Directory]: /azure/active-directory/
[Azure Active Directory Documentation]: /azure/active-directory/
[AAD app manifest]: /azure/active-directory/develop/active-directory-application-manifest
[Get started with Azure AD]: /azure/active-directory/get-started-azure-ad
[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[free Azure account]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
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
