---
title: Bibliothèques Azure Active Directory pour Java
description: Consulter la documentation sur les bibliothèques clientes et de gestion Java pour les bases de données pour Azure Active Directory
keywords: Azure, Java, SDK, API, SQL, authentification, AAD, Active Directory, Graph, OAuth 2.0
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 07/11/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.openlocfilehash: 36758977a64600d5ac11a0c5ac59bed981e8fa33
ms.sourcegitcommit: 7c6a15f574fb85ee22f6ccdb7864627b73a6c1f7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2018
ms.locfileid: "47398161"
---
# <a name="azure-active-directory-libraries-for-java"></a>Bibliothèques Azure Active Directory pour Java

## <a name="overview"></a>Vue d’ensemble

Authentifiez des utilisateurs et contrôlez l’accès aux applications et aux API avec [Azure Active Directory](/azure/active-directory/active-directory-whatis).

Pour découvrir Azure AD, consultez l’article [Connexion aux applications web Java et déconnexion de ces dernières avec Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-java).

## <a name="client-library"></a>Bibliothèque cliente

Configurez l’authentification avec OAuth2, OpenID Connect ou Active Directory Graph et l’authentification unique [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) avec la [bibliothèque d’authentification d’Azure Active Directory (ADAL) pour Java](https://github.com/AzureAD/azure-activedirectory-library-for-java).

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser la bibliothèque cliente dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>adal4j</artifactId>
    <version>1.2.0</version>
</dependency>
```   

### <a name="example"></a>Exemples

Récupérez un JSON Web Token (JWT) pour un utilisateur dans votre client Active Directory à l’aide de l’[API Graph](https://docs.microsoft.com/azure/active-directory/develop/active-directory-graph-api) d’Azure Active Directory. Ce jeton peut ensuite servir à authentifier l’utilisateur avec une application ou une API.

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

## <a name="management-api"></a>API de gestion

Configurez le [contrôle d’accès en fonction du rôle](/azure/active-directory/role-based-access-control-what-is) et attribuez des identités (utilisateurs et [principaux de service](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects), par exemple) à ces rôles avec l’API de gestion. 

[Ajoutez une dépendance](https://maven.apache.org/guides/getting-started/index.html#How_do_I_use_external_dependencies) au fichier Maven `pom.xml` pour utiliser l’API de gestion dans votre projet.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-mgmt-graph-rbac</artifactId>
    <version>1.3.0</version>
</dependency>
```

### <a name="example"></a>Exemples 

Créez un principal de service et attribuez-lui le rôle de Contributeur.

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
> [Explorer les API de gestion](/java/api/overview/azure/activedirectory/management)


## <a name="samples"></a>Exemples

[Gérer des groupes, des utilisateurs et des rôles](https://github.com/Azure-Samples/aad-java-manage-users-groups-and-roles)    
[Ouvrir/fermer des sessions dans une application web Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)    
[Accéder à une API avec Azure AD à l’aide d’une application de ligne de commande](https://github.com/Azure-Samples/active-directory-java-native-headless)   
[Appeler l’API Graph d’Azure AD à partir de votre application web Java](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect)  

Explorez davantage d’[exemples de code Java pour Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=java) à utiliser avec vos applications.
