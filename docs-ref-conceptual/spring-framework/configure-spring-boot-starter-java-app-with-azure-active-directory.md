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
# <a name="tutorial-secure-a-java-web-app-using-the-spring-boot-starter-for-azure-active-directory"></a><span data-ttu-id="ea6e9-103">Tutoriel : sécuriser une application web Java avec Spring Boot Starter pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea6e9-103">Tutorial: Secure a Java web app using the Spring Boot Starter for Azure Active Directory</span></span>

## <a name="overview"></a><span data-ttu-id="ea6e9-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="ea6e9-104">Overview</span></span>

<span data-ttu-id="ea6e9-105">Cet article illustre la création d’une application Java avec **[Spring Initializr]** qui utilise Spring Boot Starter pour Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ea6e9-105">This article demonstrates creating a Java app with the **[Spring Initializr]** that uses the Spring Boot Starter for Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ea6e9-106">Ce tutoriel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ea6e9-107">Créer une application Java à l’aide de Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="ea6e9-107">Create a Java application using the Spring Initializr</span></span>
> * <span data-ttu-id="ea6e9-108">Configurer Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea6e9-108">Configure Azure Active Directory</span></span>
> * <span data-ttu-id="ea6e9-109">Sécuriser l’application avec des classes et annotations Spring Boot</span><span class="sxs-lookup"><span data-stu-id="ea6e9-109">Secure the application with Spring Boot classes and annotations</span></span>
> * <span data-ttu-id="ea6e9-110">Générer et tester votre application Java</span><span class="sxs-lookup"><span data-stu-id="ea6e9-110">Build and test your Java application</span></span>

<span data-ttu-id="ea6e9-111">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea6e9-112">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ea6e9-112">Prerequisites</span></span>

<span data-ttu-id="ea6e9-113">Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-113">The following prerequisites are required in order to complete the steps in this article:</span></span>

* <span data-ttu-id="ea6e9-114">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-114">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="ea6e9-115">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-115">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* <span data-ttu-id="ea6e9-116">[Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-116">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-app-using-spring-initializr"></a><span data-ttu-id="ea6e9-117">Créer une application à l’aide de Spring Initialzr</span><span class="sxs-lookup"><span data-stu-id="ea6e9-117">Create an app using Spring Initializr</span></span>

1. <span data-ttu-id="ea6e9-118">Accédez à <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-118">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ea6e9-119">Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-119">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the link to **Switch to the full version** of the Spring Initializr.</span></span>

   ![Spécifiez les noms de groupes et d’artefacts.][create-spring-app-01]

1. <span data-ttu-id="ea6e9-121">Faites défiler jusqu’à la section **Core** et cochez la case **Sécurité**. Dans la section **Web**, cochez **Web**, puis faites défiler jusqu’à la section **Azure** et cochez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-121">Scroll down to the **Core** section and check the box for **Security**, and in the **Web** section check the box for **Web**, then scroll down to the **Azure** section and check the box for **Azure Active Directory**.</span></span>

   ![Sélectionner les starters Security, Web et Azure Active Directory][create-spring-app-02]

1. <span data-ttu-id="ea6e9-123">Faites défiler jusqu’en bas ou en haut de la page, puis cliquez sur le bouton pour **générer le projet**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-123">Scroll to the top or bottom of the page and click the button to **Generate Project**.</span></span>

   ![Générez le projet Spring Boot.][create-spring-app-03]

1. <span data-ttu-id="ea6e9-125">Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-125">When prompted, download the project to a path on your local computer.</span></span>

## <a name="create-azure-active-directory-instance"></a><span data-ttu-id="ea6e9-126">Créer une instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea6e9-126">Create Azure Active Directory instance</span></span>

### <a name="create-the-active-directory-instance"></a><span data-ttu-id="ea6e9-127">Créer l’instance Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ea6e9-127">Create the Active Directory instance</span></span>

1. <span data-ttu-id="ea6e9-128">Connectez-vous à <https://portal.azure.com>.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-128">Log into <https://portal.azure.com>.</span></span>

1. <span data-ttu-id="ea6e9-129">Cliquez sur **+Créer une ressource**, puis sur **Identité** et enfin sur **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-129">Click **+Create a resource**, then **Identity**, and then **Azure Active Directory**.</span></span>

   ![Créer une instance Azure Active Directory][create-directory-01]

1. <span data-ttu-id="ea6e9-131">Entrez le **Nom de l’organisation** et votre **Nom de domaine initial**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-131">Enter your **Organization name** and your **Initial domain name**.</span></span> <span data-ttu-id="ea6e9-132">Copier l’URL complète de votre répertoire ; vous allez l’utiliser pour ajouter des comptes d’utilisateur plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-132">Copy the full URL of your directory; you will use that to add user accounts later in this tutorial.</span></span> <span data-ttu-id="ea6e9-133">(Par exemple : `wingtiptoysdirectory.onmicrosoft.com`.) Une fois que vous avez terminé, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-133">(For example: `wingtiptoysdirectory.onmicrosoft.com`.) When you have finished, click **Create**.</span></span>

   ![Spécifier des noms Azure Active Directory][create-directory-02]

1. <span data-ttu-id="ea6e9-135">Sélectionnez le nom de votre compte dans le coin supérieur droit de la barre d’outils du portail Azure, puis cliquez sur **Changer de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-135">Select your account name on the top-right of the Azure portal toolbar, then click **Switch directory**.</span></span>

   ![Sélectionner le nom de votre compte Azure][create-directory-03]

1. <span data-ttu-id="ea6e9-137">Sélectionnez votre nouvelle instance Azure Active Directory dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-137">Select your new Azure Active Directory from the drop-down menu.</span></span>

   ![Choisir votre instance Azure Active Directory][create-directory-04]

1. <span data-ttu-id="ea6e9-139">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Propriétés**, et copiez l’**ID d’annuaire** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-139">Select **Azure Active Directory** from the portal menu, click **Properties**, and copy the **Directory ID**; you will use that value to configure your *application.properties* file later in this tutorial.</span></span>

   ![Copier votre ID Azure Active Directory][create-directory-05]

### <a name="add-an-application-registration-for-your-spring-boot-app"></a><span data-ttu-id="ea6e9-141">Ajouter une inscription d’application pour votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="ea6e9-141">Add an application registration for your Spring Boot app</span></span>

1. <span data-ttu-id="ea6e9-142">Sélectionnez **Azure Active Directory** dans le menu du portail, cliquez sur **Inscriptions des applications**, puis sur **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-142">Select **Azure Active Directory** from the portal menu, click **App registrations**, and then click **New application registration**, .</span></span>

   ![Ajouter une inscription d’application][create-app-registration-01]

2. <span data-ttu-id="ea6e9-144">Spécifiez le **Nom** de votre application, utilisez http://localhost:8080 en tant qu’**URL de connexion**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-144">Specify your application **Name**, use http://localhost:8080 for the **Sign-on URL**, and then click **Create**.</span></span>

   ![Créer une inscription d’application][create-app-registration-02]

4. <span data-ttu-id="ea6e9-146">Lorsque la page pour l’inscription de votre application s’affiche, copiez votre **ID d’application** ; vous utiliserez cette valeur pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-146">When the page for your app registration appears, copy your **Application ID**; you will use this value to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="ea6e9-147">Cliquez sur **Paramètres**, puis sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-147">Click **Settings**, and then click **Keys**.</span></span>

   ![Créer des clés d’inscription d’application][create-app-registration-03]

5. <span data-ttu-id="ea6e9-149">Ajoutez une **Description**, spécifiez la **Durée** d’une nouvelle clé, puis cliquez sur **Enregistrer** ; la valeur de la clé est automatiquement renseignée lorsque vous cliquez sur l’icône **Enregistrer**, vous devez copier la valeur de la clé pour configurer votre fichier *application.properties* plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-149">Add a **Description** and specify the **Duration** for a new key and click **Save**; the value for the key will be automatically filled in when you click the **Save** icon, and you need to copy down the value of the key to configure your *application.properties* file later in this tutorial.</span></span> <span data-ttu-id="ea6e9-150">(Il ne vous sera pas possible de récupérer cette valeur plus tard.)</span><span class="sxs-lookup"><span data-stu-id="ea6e9-150">(You will not be able to retrieve this value later.)</span></span>

   ![Spécifier les paramètres de la clé d’inscription d’application][create-app-registration-04]

6. <span data-ttu-id="ea6e9-152">Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-152">From the main page for your app registration, click **Settings**, and then click **Required permissions**.</span></span>

   ![Autorisations requises de l’inscription d’application][create-app-registration-05]

7. <span data-ttu-id="ea6e9-154">Cliquez sur **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-154">Click **Windows Azure Active Directory**.</span></span>

   ![Sélectionner Windows Azure Active Directory][create-app-registration-06]

8. <span data-ttu-id="ea6e9-156">Cochez les cases en regard de **Accéder au répertoire en tant qu’utilisateur actuellement connecté** et **Activer la connexion et lire le profil utilisateur**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-156">Check the boxes for **Access the directory as the signed-in user** and **Sign in and read user profile**, and then click **Save**.</span></span>

   ![Activer les autorisations d’accès][create-app-registration-07]

9. <span data-ttu-id="ea6e9-158">Sur la page **Autorisations requises**, cliquez sur **Accorder les autorisations**, puis cliquez sur **Oui** à l’invite.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-158">On the **Required permissions** page, click **Grant Permissions**, and click **Yes** when prompted.</span></span>

   ![Accorder les autorisations d’accès][create-app-registration-08]

10. <span data-ttu-id="ea6e9-160">Sur la page principale de votre inscription d’application, cliquez sur **Paramètres** puis sur **URL de réponse**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-160">From the main page for your app registration, click **Settings**, and then click **Reply URLs**.</span></span>

    ![Modifier les URL de réponse][create-app-registration-09]

11. <span data-ttu-id="ea6e9-162">Saisissez la nouvelle URL de réponse « <http://localhost:8080/login/oauth2/code/azure> », puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-162">Enter "<http://localhost:8080/login/oauth2/code/azure>" as a new reply URL, and then click **Save**.</span></span>

    ![Ajouter une nouvelle URL de réponse][create-app-registration-10]

12. <span data-ttu-id="ea6e9-164">Dans la page principale de l’inscription de votre application, cliquez sur **Manifeste**, définissez la valeur du paramètre `oauth2AllowImplicitFlow` sur `true`, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-164">From the main page for your app registration, click **Manifest**, then set the value of the `oauth2AllowImplicitFlow` parameter to `true`, and then click **Save**.</span></span>

    ![Configurer le manifeste de l’application][create-app-registration-11]

    > [!NOTE]
    > 
    > <span data-ttu-id="ea6e9-166">Pour plus d’informations sur le paramètre `oauth2AllowImplicitFlow` et les autres paramètres d’applications, consultez [Manifeste de l’application Azure Active Directory][AAD app manifest].</span><span class="sxs-lookup"><span data-stu-id="ea6e9-166">For more information about the `oauth2AllowImplicitFlow` parameter and other application settings, see [Azure Active Directory application manifest][AAD app manifest].</span></span> 
    >

### <a name="add-a-user-account-to-your-directory-and-add-that-account-to-a-group"></a><span data-ttu-id="ea6e9-167">Ajouter un compte d’utilisateur à votre répertoire et ajouter ce compte à un groupe</span><span class="sxs-lookup"><span data-stu-id="ea6e9-167">Add a user account to your directory, and add that account to a group</span></span>

1. <span data-ttu-id="ea6e9-168">À partir de la page **Vue d’ensemble** de votre répertoire Active Directory, cliquez sur **Tous les utilisateurs**, puis sur **Nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-168">From the **Overview** page of your Active Directory, click **All Users**, and then click **New user**.</span></span>

   ![Ajouter un compte d’utilisateur][create-user-01]

1. <span data-ttu-id="ea6e9-170">Lorsque le panneau **Utilisateur** s’affiche, entrez le **Nom** et le **Nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-170">When the **User** panel is displayed, enter the **Name** and **User name**.</span></span>

   ![Entrer les informations sur le compte d’utilisateur][create-user-02]

   > [!NOTE]
   > 
   > <span data-ttu-id="ea6e9-172">Vous devez spécifier l’URL de votre répertoire plus tôt dans ce tutoriel lorsque vous entrez le nom d’utilisateur ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-172">You need to specify your directory URL from earlier in this tutorial when you enter the user name; for example:</span></span>
   >
   > `wingtipuser@wingtiptoysdirectory.onmicrosoft.com`
   > 

1. <span data-ttu-id="ea6e9-173">Cliquez sur **Groupes**, puis sélectionnez les groupes que vous allez utiliser pour l’autorisation dans votre application, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-173">Click **Groups**, then select the groups that you will use for authorization in your application, and then click **Select**.</span></span> <span data-ttu-id="ea6e9-174">(Dans le cadre de ce tutoriel, ajoutez le compte au groupe d’_Utilisateurs_.)</span><span class="sxs-lookup"><span data-stu-id="ea6e9-174">(For the purposes of this tutorial, add the account to the _Users_ group.)</span></span>

   ![Sélectionner les groupes d’utilisateur][create-user-03]

1. <span data-ttu-id="ea6e9-176">Cliquez sur **Afficher le mot de passe** et copiez le mot de passe ; vous l’utiliserez lorsque vous vous connecterez à votre application plus tard dans ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-176">Click **Show password**, and copy the password; you will use this when you log into your application later in this tutorial.</span></span> <span data-ttu-id="ea6e9-177">Une fois le mot de passe copié, cliquez sur **Créer** pour ajouter le nouveau compte d’utilisateur à votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-177">When you have copied the password, click **Create** to add the new user account to your directory.</span></span>

   ![Afficher le mot de passe][create-user-04]

## <a name="configure-and-compile-your-app"></a><span data-ttu-id="ea6e9-179">Configurer et compiler votre application</span><span class="sxs-lookup"><span data-stu-id="ea6e9-179">Configure and compile your app</span></span>

1. <span data-ttu-id="ea6e9-180">Extrayez les fichiers des archives du projet que vous avez créées et téléchargées précédemment dans ce tutoriel dans un répertoire.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-180">Extract the files from the project archive you created and downloaded earlier in this tutorial into a directory.</span></span>

1. <span data-ttu-id="ea6e9-181">Accédez au dossier parent pour votre projet, puis ouvrez le fichier de projet Maven `pom.xml` dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-181">Navigate to the parent folder for your project, and open the `pom.xml` Maven project file in a text editor.</span></span>

1. <span data-ttu-id="ea6e9-182">Ajoutez les dépendances associées à la sécurité Spring OAuth2 au fichier `pom.xml` :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-182">Add the dependencies for Spring OAuth2 security to the `pom.xml`:</span></span>

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

1. <span data-ttu-id="ea6e9-183">Enregistrez et fermez le fichier *pom.xml*.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-183">Save and close the *pom.xml* file.</span></span>

1. <span data-ttu-id="ea6e9-184">Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-184">Navigate to the *src/main/resources* folder in your project and open the *application.properties* file in a text editor.</span></span>

1. <span data-ttu-id="ea6e9-185">Spécifiez les paramètres pour l’inscription de votre application en utilisant les valeurs que vous avez créé précédemment ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-185">Specify the settings for your app registration using the values you created earlier; for example:</span></span>

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
   <span data-ttu-id="ea6e9-186">Où :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-186">Where:</span></span>

   | <span data-ttu-id="ea6e9-187">Paramètre</span><span class="sxs-lookup"><span data-stu-id="ea6e9-187">Parameter</span></span> | <span data-ttu-id="ea6e9-188">Description</span><span class="sxs-lookup"><span data-stu-id="ea6e9-188">Description</span></span> |
   |---|---|
   | `azure.activedirectory.tenant-id` | <span data-ttu-id="ea6e9-189">Contient l’**ID du répertoire** d’Active Directory vu précédemment.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-189">Contains your Active Directory's **Directory ID** from earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-id` | <span data-ttu-id="ea6e9-190">Contient l’**ID de l’application** de votre inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-190">Contains the **Application ID** from your app registration that you completed earlier.</span></span> |
   | `spring.security.oauth2.client.registration.azure.client-secret` | <span data-ttu-id="ea6e9-191">Contient la **Valeur** de votre clé d’inscription d’application exécutée précédemment.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-191">Contains the **Value** from your app registration key that you completed earlier.</span></span> |
   | `azure.activedirectory.active-directory-groups` | <span data-ttu-id="ea6e9-192">Contient une liste des groupes Active Directory à utiliser pour l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-192">Contains a list of Active Directory groups to use for authorization.</span></span> |

   > [!NOTE]
   > 
   > <span data-ttu-id="ea6e9-193">Pour obtenir une liste complète des valeurs disponibles dans votre fichier *application.properties*, consultez [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] (exemple de Spring Boot Azure Active Directory) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-193">For a full list of values that are available in your *application.properties* file, see  the [Azure Active Directory Spring Boot Sample][AAD Spring Boot Sample] on GitHub.</span></span>
   >

1. <span data-ttu-id="ea6e9-194">Enregistrez et fermez le fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-194">Save and close the *application.properties* file.</span></span>

1. <span data-ttu-id="ea6e9-195">Créez un dossier nommé *controller* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/controller*.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-195">Create a folder named *controller* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/controller*.</span></span>

1. <span data-ttu-id="ea6e9-196">Créez un fichier Java nommé *HelloController.java* dans le dossier *controller*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-196">Create a new Java file named *HelloController.java* in the *controller* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="ea6e9-197">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-197">Enter the following code, then save and close the file:</span></span>

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
   > <span data-ttu-id="ea6e9-198">Le nom de groupe spécifié pour la méthode `@PreAuthorize("hasRole('')")` doit contenir l’un des groupes spécifiés dans le champ `azure.activedirectory.active-directory-groups` de votre fichier *application.properties*.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-198">The group name that you specify for the `@PreAuthorize("hasRole('')")` method must contain one of the groups that you specified in the `azure.activedirectory.active-directory-groups` field of your *application.properties* file.</span></span>
   > 
   > <span data-ttu-id="ea6e9-199">Vous pouvez aussi spécifier différents paramètres d’autorisation pour différents mappages de requêtes ; par exemple :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-199">You can also specify different authorization settings for different request mappings; for example:</span></span>
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

1. <span data-ttu-id="ea6e9-200">Créez un dossier nommé *security* dans le dossier source Java de votre application, par exemple : *src/main/java/com/wingtiptoys/security/security*.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-200">Create a folder named *security* in the Java source folder for your application; for example: *src/main/java/com/wingtiptoys/security/security*.</span></span>

1. <span data-ttu-id="ea6e9-201">Créez un fichier Java nommé *WebSecurityConfig.java* dans le dossier *security*, puis ouvrez-le dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-201">Create a new Java file named *WebSecurityConfig.java* in the *security* folder and open it in a text editor.</span></span>

1. <span data-ttu-id="ea6e9-202">Entrez le code suivant, puis enregistrez et fermez le fichier :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-202">Enter the following code, then save and close the file:</span></span>

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

## <a name="build-and-test-your-app"></a><span data-ttu-id="ea6e9-203">Générer et tester votre application</span><span class="sxs-lookup"><span data-stu-id="ea6e9-203">Build and test your app</span></span>

1. <span data-ttu-id="ea6e9-204">Ouvrez une invite de commandes, puis définissez le répertoire sur le dossier hébergeant le fichier *pom.xml* de votre application.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-204">Open a command prompt and change directory to the folder where your app's *pom.xml* file is located.</span></span>

1. <span data-ttu-id="ea6e9-205">Générez votre application Spring Boot avec Maven, puis exécutez-la. Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ea6e9-205">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

   ![Générer votre application][build-application]

1. <span data-ttu-id="ea6e9-207">Une fois que votre application est créée et démarrée dans Maven, ouvrez <http://localhost:8080> dans un navigateur web ; vous devez fournir un nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-207">After your application is built and started by Maven, open <http://localhost:8080> in a web browser; you should be prompted for a user name and password.</span></span>

   ![Se connecter à l’application][application-login]

   > [!NOTE]
   > 
   > <span data-ttu-id="ea6e9-209">Vous pouvez être invité à modifier votre mot de passe, s’il s’agit de la première connexion à un nouveau compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-209">You may be prompted to change your password if this is the first login for a new user account.</span></span>
   > 
   > ![Modifier votre mot de passe][update-password]
   > 

1. <span data-ttu-id="ea6e9-211">Une fois que vous vous êtes connecté avec succès, vous devez voir le contrôleur afficher l’exemple de texte « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="ea6e9-211">After you have logged in successfully, you should see the sample "Hello World" text from the controller.</span></span>

   ![Connexion réussie][hello-world]

   > [!NOTE]
   > 
   > <span data-ttu-id="ea6e9-213">Les comptes d’utilisateur qui ne sont pas autorisés recevront un message **HTTP 403 non autorisé**.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-213">User accounts which are not authorized will receive an **HTTP 403 Unauthorized** message.</span></span>
   >

## <a name="summary"></a><span data-ttu-id="ea6e9-214">Résumé</span><span class="sxs-lookup"><span data-stu-id="ea6e9-214">Summary</span></span>

<span data-ttu-id="ea6e9-215">Dans ce tutoriel, vous avez crée une application web Java avec le starter Azure Active Directory, configuré un nouveau locataire Azure AD et inscrit une nouvelle application, avant de configurer votre application pour utiliser les annotations et classes Spring pour protéger l’application web.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-215">In this tutorial, you created a new Java web application using the Azure Active Directory starter, configured a new Azure AD tenant and registered a new application in it, and then configured your application to use the Spring annotations and classes to protect the web app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea6e9-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ea6e9-216">Next steps</span></span>

<span data-ttu-id="ea6e9-217">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="ea6e9-217">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea6e9-218">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="ea6e9-218">Spring on Azure</span></span>](/java/azure/spring-framework)

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
