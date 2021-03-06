---
title: Pour débuter avec Spring Boot pour Azure
description: Cet article décrit les différentes instances Spring Boot Starters disponibles pour Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 12/19/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 69c0381313994796af31d5301ceadb9f6f40dcb5
ms.sourcegitcommit: f0f140b0862ca5338b1b7e5c33cec3e58a70b8fd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/03/2019
ms.locfileid: "53991553"
---
# <a name="spring-boot-starters-for-azure"></a>Pour débuter avec Spring Boot pour Azure

Cet article décrit les différentes instances Spring Boot Starter pour l’instance [Spring Initializr] qui octroient aux développeurs Java des fonctionnalités d’intégration permettant de travailler avec Microsoft Azure.

![Pour débuter avec Azure Spring Boot][spring-boot-starters]

Les applications suivantes de démarrage de Spring Boot sont actuellement disponibles pour Azure :

* **[Support Azure](#azure-support)**

   Fournit une prise en charge de configuration automatique pour les services Azure, par exemple Service Bus, Storage, Active Directory, etc.

* **[Azure Active Directory](#azure-active-directory)**

   Fournit une prise en charge de l’intégration pour Spring Security avec Azure Active Directory, à des fins d’authentification.

* **[Azure Key Vault](#azure-key-vault)**

   Fournit une prise en charge des annotations de valeurs Spring pour l’intégration avec les secrets Azure Key Vault.

* **[Stockage Azure](#azure-storage)**

   Fournit une prise en charge de Spring Boot pour les services Azure Storage.

<a name="azure-support"></a>
## <a name="azure-support"></a>Support Azure

Spring Boot Starter fourni un support pour la configuration automatique des services Azure, par exemple : Service Bus, Stockage, Active Directory, Cosmos DB, Key Vault, etc.

Pour des exemples sur l’utilisation des différentes fonctionnalités Azure fournies par cette application de démarrage, consultez la ressource suivante :

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :

* La propriété suivante est ajoutée à l’élément `<properties>` :

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* La section suivante est ajoutée au fichier :

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-active-directory"></a>
## <a name="azure-active-directory"></a>Azure Active Directory

Cette instance Spring Boot Starter fournit une prise en charge de configuration automatique pour Spring Security afin d’assurer l’intégration avec Azure Active Directory à des fins d’authentification.

Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Active Directory fournies par cette application de démarrage, consultez la ressource suivante :

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :

* La propriété suivante est ajoutée à l’élément `<properties>` :

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* La section suivante est ajoutée au fichier :

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-key-vault"></a>
## <a name="azure-key-vault"></a>Azure Key Vault

Cette instance Spring Boot Starter fournit une prise en charge des annotations de valeurs Spring pour l’intégration avec les secrets Azure Key Vault.

Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Key Vault fournies par cette application de démarrage, consultez la ressource suivante :

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :

* La propriété suivante est ajoutée à l’élément `<properties>` :

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* La section suivante est ajoutée au fichier :

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

<a name="azure-storage"></a>
## <a name="azure-storage"></a>Stockage Azure

Cette instance Spring Boot Starter fournit une prise en charge de l’intégration de Spring Boot pour les services Azure Storage.

Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Storage fournies par cette application de démarrage, consultez la ressource suivante :

* [Comment utiliser Spring Boot Starter pour Azure Storage](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :

* La propriété suivante est ajoutée à l’élément `<properties>` :

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* La section suivante est ajoutée au fichier :

   ```xml
   <dependencyManagement>
      <dependencies>
         <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-spring-boot-bom</artifactId>
            <version>${azure.version}</version>
            <type>pom</type>
            <scope>import</scope>
         </dependency>
      </dependencies>
   </dependencyManagement>
   ```

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.

> [!div class="nextstepaction"]
> [Spring sur Azure](/java/azure/spring-framework)

### <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur l’utilisation d’applications [Spring Boot] sur Azure, consultez [Spring sur Azure].

Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].

Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring sur Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
