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
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="a415b-103">Pour débuter avec Spring Boot pour Azure</span><span class="sxs-lookup"><span data-stu-id="a415b-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="a415b-104">Cet article décrit les différentes instances Spring Boot Starter pour l’instance [Spring Initializr] qui octroient aux développeurs Java des fonctionnalités d’intégration permettant de travailler avec Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a415b-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Pour débuter avec Azure Spring Boot][spring-boot-starters]

<span data-ttu-id="a415b-106">Les applications suivantes de démarrage de Spring Boot sont actuellement disponibles pour Azure :</span><span class="sxs-lookup"><span data-stu-id="a415b-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="a415b-107">**[Support Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="a415b-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="a415b-108">Fournit une prise en charge de configuration automatique pour les services Azure, par exemple Service Bus, Storage, Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="a415b-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="a415b-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="a415b-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="a415b-110">Fournit une prise en charge de l’intégration pour Spring Security avec Azure Active Directory, à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="a415b-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="a415b-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="a415b-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="a415b-112">Fournit une prise en charge des annotations de valeurs Spring pour l’intégration avec les secrets Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a415b-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="a415b-113">**[Stockage Azure](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="a415b-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="a415b-114">Fournit une prise en charge de Spring Boot pour les services Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a415b-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="a415b-115">Support Azure</span><span class="sxs-lookup"><span data-stu-id="a415b-115">Azure Support</span></span>

<span data-ttu-id="a415b-116">Spring Boot Starter fourni un support pour la configuration automatique des services Azure, par exemple : Service Bus, Stockage, Active Directory, Cosmos DB, Key Vault, etc.</span><span class="sxs-lookup"><span data-stu-id="a415b-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="a415b-117">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="a415b-118">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="a415b-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="a415b-119">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="a415b-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="a415b-120">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="a415b-121">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="a415b-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="a415b-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a415b-122">Azure Active Directory</span></span>

<span data-ttu-id="a415b-123">Cette instance Spring Boot Starter fournit une prise en charge de configuration automatique pour Spring Security afin d’assurer l’intégration avec Azure Active Directory à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="a415b-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="a415b-124">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Active Directory fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="a415b-125">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="a415b-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="a415b-126">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="a415b-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="a415b-127">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="a415b-128">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="a415b-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="a415b-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a415b-129">Azure Key Vault</span></span>

<span data-ttu-id="a415b-130">Cette instance Spring Boot Starter fournit une prise en charge des annotations de valeurs Spring pour l’intégration avec les secrets Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a415b-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="a415b-131">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Key Vault fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="a415b-132">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="a415b-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="a415b-133">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="a415b-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="a415b-134">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="a415b-135">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="a415b-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="a415b-136">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="a415b-136">Azure Storage</span></span>

<span data-ttu-id="a415b-137">Cette instance Spring Boot Starter fournit une prise en charge de l’intégration de Spring Boot pour les services Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a415b-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="a415b-138">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Storage fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="a415b-139">Comment utiliser Spring Boot Starter pour Azure Storage</span><span class="sxs-lookup"><span data-stu-id="a415b-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="a415b-140">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="a415b-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="a415b-141">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="a415b-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="a415b-142">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="a415b-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="a415b-143">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="a415b-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a415b-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a415b-144">Next steps</span></span>

<span data-ttu-id="a415b-145">Pour en savoir plus sur Spring et Azure, poursuivez vers le centre de documentation Spring sur Azure.</span><span class="sxs-lookup"><span data-stu-id="a415b-145">To learn more about Spring and Azure, continue to the Spring on Azure documentation center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a415b-146">Spring sur Azure</span><span class="sxs-lookup"><span data-stu-id="a415b-146">Spring on Azure</span></span>](/java/azure/spring-framework)

### <a name="additional-resources"></a><span data-ttu-id="a415b-147">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a415b-147">Additional Resources</span></span>

<span data-ttu-id="a415b-148">Pour plus d’informations sur l’utilisation d’applications [Spring Boot] sur Azure, consultez [Spring sur Azure].</span><span class="sxs-lookup"><span data-stu-id="a415b-148">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="a415b-149">Pour plus d’informations sur l’utilisation d’Azure avec Java, renseignez-vous sur [Azure pour les développeurs Java] et l’[utilisation d’Azure DevOps et Java].</span><span class="sxs-lookup"><span data-stu-id="a415b-149">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Working with Azure DevOps and Java].</span></span>

<span data-ttu-id="a415b-150">Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="a415b-150">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure pour les développeurs Java]: /java/azure/
[Azure for Java Developers]: /java/azure/
[Utilisation d’Azure DevOps et Java]: /azure/devops/
[Working with Azure DevOps and Java]: /azure/devops/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring sur Azure]: /java/azure/spring-framework/
[Spring on Azure]: /java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
