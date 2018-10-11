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
ms.date: 02/01/2018
ms.devlang: java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 678d4b279cecb83c95b3bf0f6bcdf1581924aa62
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893500"
---
# <a name="spring-boot-starters-for-azure"></a><span data-ttu-id="0f448-103">Pour débuter avec Spring Boot pour Azure</span><span class="sxs-lookup"><span data-stu-id="0f448-103">Spring Boot Starters for Azure</span></span>

<span data-ttu-id="0f448-104">Cet article décrit les différentes instances Spring Boot Starter pour l’instance [Spring Initializr] qui octroient aux développeurs Java des fonctionnalités d’intégration permettant de travailler avec Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0f448-104">This article describes the various Spring Boot Starters for the [Spring Initializr] that provide Java developers with integration features for working with Microsoft Azure.</span></span>

![Pour débuter avec Azure Spring Boot][spring-boot-starters]

<span data-ttu-id="0f448-106">Les applications suivantes de démarrage de Spring Boot sont actuellement disponibles pour Azure :</span><span class="sxs-lookup"><span data-stu-id="0f448-106">The following Spring Boot Starters are currently available for Azure:</span></span>

* <span data-ttu-id="0f448-107">**[Support Azure](#azure-support)**</span><span class="sxs-lookup"><span data-stu-id="0f448-107">**[Azure Support](#azure-support)**</span></span>

   <span data-ttu-id="0f448-108">Fournit une prise en charge de configuration automatique pour les services Azure, par exemple Service Bus, Storage, Active Directory, etc.</span><span class="sxs-lookup"><span data-stu-id="0f448-108">Provides auto-configuration support for Azure Services; e.g. Service Bus, Storage, Active Directory, etc.</span></span>

* <span data-ttu-id="0f448-109">**[Azure Active Directory](#azure-active-directory)**</span><span class="sxs-lookup"><span data-stu-id="0f448-109">**[Azure Active Directory](#azure-active-directory)**</span></span>

   <span data-ttu-id="0f448-110">Fournit une prise en charge de l’intégration pour Spring Security avec Azure Active Directory, à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0f448-110">Provides integration support for Spring Security with Azure Active Directory for authentication.</span></span>

* <span data-ttu-id="0f448-111">**[Azure Key Vault](#azure-key-vault)**</span><span class="sxs-lookup"><span data-stu-id="0f448-111">**[Azure Key Vault](#azure-key-vault)**</span></span>

   <span data-ttu-id="0f448-112">Fournit une prise en charge des annotations de valeurs Spring pour l’intégration avec les secrets Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0f448-112">Provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

* <span data-ttu-id="0f448-113">**[Stockage Azure](#azure-storage)**</span><span class="sxs-lookup"><span data-stu-id="0f448-113">**[Azure Storage](#azure-storage)**</span></span>

   <span data-ttu-id="0f448-114">Fournit une prise en charge de Spring Boot pour les services Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f448-114">Provides Spring Boot support for Azure Storage services.</span></span>

<a name="azure-support"></a>
## <a name="azure-support"></a><span data-ttu-id="0f448-115">Support Azure</span><span class="sxs-lookup"><span data-stu-id="0f448-115">Azure Support</span></span>

<span data-ttu-id="0f448-116">Cette instance Spring Boot Starter fournit une prise en charge de configuration automatique pour les services Azure, par exemple : Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span><span class="sxs-lookup"><span data-stu-id="0f448-116">This Spring Boot Starter provides auto-configuration support for Azure Services; for example: Service Bus, Storage, Active Directory, Cosmos DB, Key Vault, etc.</span></span>

<span data-ttu-id="0f448-117">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-117">For examples of how to use the various Azure features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples>

<span data-ttu-id="0f448-118">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="0f448-118">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="0f448-119">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="0f448-119">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="0f448-120">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-120">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-spring-boot</artifactId>
   </dependency>
   ```

* <span data-ttu-id="0f448-121">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="0f448-121">The following section is added to the file:</span></span>

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
## <a name="azure-active-directory"></a><span data-ttu-id="0f448-122">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f448-122">Azure Active Directory</span></span>

<span data-ttu-id="0f448-123">Cette instance Spring Boot Starter fournit une prise en charge de configuration automatique pour Spring Security afin d’assurer l’intégration avec Azure Active Directory à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="0f448-123">This Spring Boot Starter provides auto-configuration support for Spring Security in order to provide integration with Azure Active Directory for authentication.</span></span>

<span data-ttu-id="0f448-124">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Active Directory fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-124">For examples of how to use the Azure Active Directory features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-active-directory-spring-boot-sample>

<span data-ttu-id="0f448-125">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="0f448-125">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="0f448-126">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="0f448-126">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="0f448-127">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-127">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-active-directory-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="0f448-128">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="0f448-128">The following section is added to the file:</span></span>

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
## <a name="azure-key-vault"></a><span data-ttu-id="0f448-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0f448-129">Azure Key Vault</span></span>

<span data-ttu-id="0f448-130">Cette instance Spring Boot Starter fournit une prise en charge des annotations de valeurs Spring pour l’intégration avec les secrets Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0f448-130">This Spring Boot Starter provides Spring value annotation support for integration with Azure Key Vault Secrets.</span></span>

<span data-ttu-id="0f448-131">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Key Vault fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-131">For examples of how to use the Azure Key Vault features that are provided by this starter, see the following:</span></span>

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-keyvault-secrets-spring-boot-sample>

<span data-ttu-id="0f448-132">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="0f448-132">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="0f448-133">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="0f448-133">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="0f448-134">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-134">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-keyvault-secrets-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="0f448-135">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="0f448-135">The following section is added to the file:</span></span>

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
## <a name="azure-storage"></a><span data-ttu-id="0f448-136">Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="0f448-136">Azure Storage</span></span>

<span data-ttu-id="0f448-137">Cette instance Spring Boot Starter fournit une prise en charge de l’intégration de Spring Boot pour les services Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="0f448-137">This Spring Boot Starter provides Spring Boot integration support for Azure Storage services.</span></span>

<span data-ttu-id="0f448-138">Pour des exemples sur l’utilisation des différentes fonctionnalités Azure Storage fournies par cette application de démarrage, consultez la ressource suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-138">For examples of how to use the Azure Storage features that are provided by this starter, see the following:</span></span>

* [<span data-ttu-id="0f448-139">Comment utiliser Spring Boot Starter pour Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0f448-139">How to use the Spring Boot Starter for Azure Storage</span></span>](configure-spring-boot-starter-java-app-with-azure-storage.md)

* <https://github.com/Microsoft/azure-spring-boot/tree/master/azure-spring-boot-samples/azure-storage-spring-boot-sample>

<span data-ttu-id="0f448-140">Lorsque vous ajoutez cette application de démarrage à un projet Spring Boot, les modifications suivantes sont apportées au fichier *pom.xml* :</span><span class="sxs-lookup"><span data-stu-id="0f448-140">When you add this starter to a Spring Boot project, the following changes are made to the *pom.xml* file:</span></span>

* <span data-ttu-id="0f448-141">La propriété suivante est ajoutée à l’élément `<properties>` :</span><span class="sxs-lookup"><span data-stu-id="0f448-141">The following property is added to `<properties>` element:</span></span>

   ```xml
   <properties>
      <!-- Other properties will be listed here -->
      <azure.version>0.2.0</azure.version>
   </properties>
   ```

* <span data-ttu-id="0f448-142">La dépendance `spring-boot-starter` par défaut est remplacée par la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="0f448-142">The default `spring-boot-starter` dependency is replaced with the following:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-storage-spring-boot-starter</artifactId>
   </dependency>
   ```

* <span data-ttu-id="0f448-143">La section suivante est ajoutée au fichier :</span><span class="sxs-lookup"><span data-stu-id="0f448-143">The following section is added to the file:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0f448-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0f448-144">Next steps</span></span>

<span data-ttu-id="0f448-145">Pour plus d’informations sur l’utilisation d’applications [Spring Boot] sur Azure, consultez [Spring sur Azure].</span><span class="sxs-lookup"><span data-stu-id="0f448-145">For more information about using [Spring Boot] applications on Azure, see [Spring on Azure].</span></span>

<span data-ttu-id="0f448-146">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="0f448-146">For more information about using Azure with Java, see the [Azure for Java Developers] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="0f448-147">Pour obtenir de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="0f448-147">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<!-- URL List -->

[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[Azure for Java Developers]: https://docs.microsoft.com/java/azure/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring sur Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring on Azure]: https://docs.microsoft.com/java/azure/spring-framework/
[Spring Framework]: https://spring.io/
[Spring Initializr]: https://start.spring.io/

<!-- IMG List -->

[spring-boot-starters]: media/spring-boot-starters-for-azure/spring-boot-starters-cropped.png
