---
title: "Outils pour développeurs Azure Java | Microsoft Docs"
description: "Intégrations d’IDE, émulateurs, explorateurs de ressources et interfaces de ligne de commande pour développeurs Azure Java."
author: rloutlaw
manager: douge
ms.assetid: b55923b7-d60a-460d-b77c-af5fac67f1cc
ms.devlang: java
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 4/10/2017
ms.author: routlaw;asirveda
ms.openlocfilehash: 01fe31f2c59810f972875331d49ce5130755c8f2
ms.sourcegitcommit: 1500f341a96d9da461c288abf4baf79f494ae662
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2017
---
# <a name="azure-tools-for-java-developers"></a>Outils Azure pour développeurs Java

## <a name="client-and-management-libraries"></a>Bibliothèques clientes et de gestion

Connectez-vous aux services et gérez les ressources Azure depuis vos applications avec les bibliothèques Azure pour Java. Importez les bibliothèques de gestion dans vos projets Maven en ajoutant cette dépendance à votre projet *pom.xml*.

```XML
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.1.2</version>
</dependency>
```

Affichez la [liste complète des bibliothèques](java-sdk-azure-install.md) et [découvrez](java-sdk-azure-get-started.md) les bibliothèques Azure pour Java.

## <a name="eclipse-and-intellij-plugins"></a>Plug-ins Eclipse et IntelliJ

Gérez les ressources Azure et déployez des applications à partir de votre environnement IDE avec le kit de ressources Azure pour [Eclipse](https://docs.microsoft.com/azure/azure-toolkit-for-eclipse) et [IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij).   

![Kit de ressources IntelliJ affichant l’Explorateur Azure](media/intelliJ-azure-explorer.png)

[Prise en main du kit de ressources Azure pour Eclipse](https://docs.microsoft.com/azure/app-service-web/app-service-web-eclipse-create-hello-world-web-app) | [Prise en main du kit de ressources Azure pour IntelliJ](https://docs.microsoft.com/azure/app-service-web/app-service-web-intellij-create-hello-world-web-app) 

## <a name="azure-cli-20"></a>Azure CLI 2.0

Azure CLI 2.0 offre une expérience en ligne de commande pour gérer les ressources Azure. Vous pouvez l’utiliser dans votre navigateur avec [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview) ou [l’installer](https://docs.microsoft.com/cli/azure/install-azure-cli) sur macOS, Linux et Windows et l’exécuter à partir de la ligne de commande.

[Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).

## <a name="azure-storage-explorer"></a>Explorateur de stockage Azure 

Gérez les comptes de stockage, conteneurs et fichiers blob Azure à partir de votre bureau. L’Explorateur de stockage Azure est actuellement en version préliminaire et fonctionne sur Windows, macOS et Linux.

[Prise en main de l’explorateur de stockage Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)