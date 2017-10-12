---
title: "Bibliothèques Azure Active Directory pour Java"
description: "Consulter la documentation sur les bibliothèques clientes et de gestion Java pour les bases de données pour Azure Active Directory"
keywords: Azure, Java, SDK, API, SQL, authentification, AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: active-directory
ms.openlocfilehash: 6226cf0f94b6403ac81ff344eba022420f5e20ea
ms.sourcegitcommit: 634ab7578c73a219f8f3a2a6d43999d9d372cb43
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2017
---
# <a name="azure-active-directory-libraries-for-java"></a><span data-ttu-id="ba78d-104">Bibliothèques Azure Active Directory pour Java</span><span class="sxs-lookup"><span data-stu-id="ba78d-104">Azure Active Directory libraries for Java</span></span>

## <a name="overview"></a><span data-ttu-id="ba78d-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ba78d-105">Overview</span></span>

<span data-ttu-id="ba78d-106">Authentifiez des utilisateurs et contrôlez l’accès aux applications et aux API avec [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span><span class="sxs-lookup"><span data-stu-id="ba78d-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

<span data-ttu-id="ba78d-107">Pour découvrir Azure AD, consultez l’article [Connexion aux applications web Java et déconnexion de ces dernières avec Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span><span class="sxs-lookup"><span data-stu-id="ba78d-107">To get started with Azure AD, see [Java web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).</span></span>

## <a name="client-library"></a><span data-ttu-id="ba78d-108">Bibliothèque cliente</span><span class="sxs-lookup"><span data-stu-id="ba78d-108">Client library</span></span>

<span data-ttu-id="ba78d-109">Configurez l’authentification avec OAuth2, OpenID Connect ou Active Directory Graph et l’authentification unique [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) avec la [bibliothèque d’authentification d’Azure Active Directory (ADAL) pour Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span><span class="sxs-lookup"><span data-stu-id="ba78d-109">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).</span></span>

<span data-ttu-id="ba78d-110">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ba78d-110">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the client library in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a><span data-ttu-id="ba78d-111">Exemple</span><span class="sxs-lookup"><span data-stu-id="ba78d-111">Example</span></span>

<span data-ttu-id="ba78d-112">Récupérez un JSON Web Token (JWT) pour un utilisateur dans votre client Active Directory à l’aide de l’[API Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba78d-112">Retrieve a JSON Web Token (JWT) for a user in your an Active Directory tenant using Azure Active Directory's [Graph API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api).</span></span> <span data-ttu-id="ba78d-113">Ce jeton peut ensuite servir à authentifier l’utilisateur avec une application ou une API.</span><span class="sxs-lookup"><span data-stu-id="ba78d-113">This token can then be used to authenticate the user with an application or API.</span></span>

```java
ExecutorService service = Executors.newFixedThreadPool(1);
AuthenticationContext context = new AuthenticationContext(AUTHORITY, false, service);
Future<AuthenticationResult> future = context.acquireToken(
    "https://graph.windows.net", YOUR_TENANT_ID, username, password,
    null);
AuthenticationResult result = future.get();
System.out.println("Access Token - " + result.getAccessToken());
System.out.println("Refresh Token - " + result.getRefreshToken());
System.out.println("ID Token - " + result.getIdToken());
```

## <a name="management-api"></a><span data-ttu-id="ba78d-114">API de gestion</span><span class="sxs-lookup"><span data-stu-id="ba78d-114">Management API</span></span>

<span data-ttu-id="ba78d-115">Configurez le [contrôle d’accès en fonction du rôle](/azure/active-directory/role-based-access-control-what-is) et attribuez des identités (utilisateurs et [principaux de service](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects), par exemple) à ces rôles avec l’API de gestion.</span><span class="sxs-lookup"><span data-stu-id="ba78d-115">Configure [role based access control](/azure/active-directory/role-based-access-control-what-is) and assign identities (such as users and [service principals](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-application-objects)) to those roles with the management API.</span></span> 

<span data-ttu-id="ba78d-116">[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="ba78d-116">[Add a dependency](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) to your Maven `pom.xml` file to use the management API in your project.</span></span>

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a><span data-ttu-id="ba78d-117">Exemple</span><span class="sxs-lookup"><span data-stu-id="ba78d-117">Example</span></span> 

<span data-ttu-id="ba78d-118">Créez un principal de service et attribuez-lui le rôle de Contributeur.</span><span class="sxs-lookup"><span data-stu-id="ba78d-118">Create a new service principal and assign it the Contributor role.</span></span>

```java
ServicePrincipal sp = Azure.servicePrincipals().define(spName)
    .withNewApplication("http://" + spName)
    .create();
RoleAssignment roleAssignment2 = authenticated.roleAssignments()
    .define("contribRoleAssignment")
    .forServicePrincipal(sp)
    .withBuiltInRole(BuiltInRole.CONTRIBUTOR)
    .withSubscriptionScope("862f67bc-d3ae-4243-bec7-3da6dca77717")
    .create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba78d-119">Explorer les API de gestion</span><span class="sxs-lookup"><span data-stu-id="ba78d-119">Explore the Management APIs</span></span>](/java/api/overview/azure/activedirectory/managementapi)


## <a name="samples"></a><span data-ttu-id="ba78d-120">Exemples</span><span class="sxs-lookup"><span data-stu-id="ba78d-120">Samples</span></span>

<span data-ttu-id="ba78d-121">[Gérer des groupes, des utilisateurs et des rôles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span><span class="sxs-lookup"><span data-stu-id="ba78d-121">[Manage groups, users, and roles](https://github.com/Azure-Samples/aad-java-browse-graph-and-manage-roles)  </span></span>  
<span data-ttu-id="ba78d-122">[Ouvrir/fermer des sessions dans une application web Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span><span class="sxs-lookup"><span data-stu-id="ba78d-122">[Sign-in and sign-out users in a Java web app](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  </span></span>  
<span data-ttu-id="ba78d-123">[Accéder à une API avec Azure AD à l’aide d’une application de ligne de commande](https://github.com/Azure-Samples/active-directory-java-native-headless) </span><span class="sxs-lookup"><span data-stu-id="ba78d-123">[Access an API with Azure AD using a command line app](https://github.com/Azure-Samples/active-directory-java-native-headless) </span></span>  
[<span data-ttu-id="ba78d-124">Appeler l’API Graph d’Azure AD à partir de votre application web Java</span><span class="sxs-lookup"><span data-stu-id="ba78d-124">Call the Active AD Graph API from your Java web app</span></span>](https://github.com/Azure-Samples/active-directory-java-graphapi-web/)  

<span data-ttu-id="ba78d-125">Explorez davantage d’[exemples de code Java pour Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) à utiliser avec vos applications.</span><span class="sxs-lookup"><span data-stu-id="ba78d-125">Explore more [sample Java code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) you can use in your apps.</span></span>