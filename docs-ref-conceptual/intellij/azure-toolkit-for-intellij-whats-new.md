---
title: "Nouveautés du Kit de ressources Azure pour IntelliJ"
description: "En savoir plus sur les dernières fonctionnalités du kit de ressources Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 46ed791f-df59-416a-809e-f52345ad973c
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 861ceb148976faff1f40055094c463171bdfb4b0
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-intellij"></a>Nouveautés du Kit de ressources Azure pour IntelliJ

## <a name="azure-toolkit-for-intellij-releases"></a>Versions du kit de ressources Azure pour IntelliJ
Cet article contient des informations sur les différentes versions et les dernières mises à jour du kit de ressources Azure pour IntelliJ.

> [!NOTE]
> Il existe également une boîte à outils Azure pour l’environnement de développement Eclipse. Pour plus d’informations, consultez [Kit de ressources Azure pour Eclipse].
> 
> 

### <a name="april-14-2017"></a>14 avril 2017
La version d’avril 2017 du kit de ressources Azure pour IntelliJ inclut les améliorations suivantes :

* **Expérience de connexion Azure améliorée** : le kit de ressources Azure pour IntelliJ prend désormais en charge deux méthodes de connexion à votre compte Azure : *interactive* et *automatisée*. Pour plus d’informations, consultez [Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ].
* **Publication à l’aide de conteneurs Docker** : à présent, vous pouvez publier vos applications web en tant que conteneurs Docker à l’aide du kit de ressources Azure pour IntelliJ. Pour plus d’informations, consultez [Comment publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ].
* **Gestion des comptes de stockage** : le kit de ressources Azure pour IntelliJ prend désormais en charge la gestion de vos comptes de stockage à partir de la vue de l’Explorateur Azure. Pour plus d’informations, consultez [Gestion des comptes de stockage avec l’Explorateur Azure pour IntelliJ].
* **Gestion des machines virtuelles** : le kit de ressources Azure pour IntelliJ prend désormais en charge la gestion de vos machines virtuelles à partir de la fenêtre de l’outil Explorateur Azure. Pour plus d’informations, consultez [Gestion des machines virtuelles avec l’Explorateur Azure pour IntelliJ].
* **Suppression de la prise en charge du débogage distant**. Le débogage distant des applications web Java dans Azure App Service a été supprimé du kit de ressources Azure pour IntelliJ ; cette action était nécessaire pour résoudre certains problèmes rencontrés par les utilisateurs lors de l’utilisation du kit de ressources.

### <a name="august-26-2016"></a>26 août 2016
La version d’août 2016 du kit de ressources Azure pour IntelliJ inclut les améliorations suivantes :

* **Distributions personnalisées du JDK**. Le kit de ressources Azure pour IntelliJ prend désormais en charge la spécification et le déploiement d’une version arbitraire du JDK dans votre conteneur Azure WebApp :
  * Outre les JDK fournis par Azure, vous pouvez également choisir parmi une large sélection de versions Zulu OpenJDK mises à disposition sur Azure par Azul Systems.
  * Vous pouvez également spécifier votre propre distribution JDK si vous chargez un fichier ZIP sur votre compte de stockage.
* **Améliorations apportées à l’affichage de l’Explorateur Azure**:
  * Prise en charge de la gestion des Machines Virtuelles suivant le nouveau modèle Azure Resource Manager : vous pouvez lister, créer et supprimer des machines virtuelles Resource Manager sans quitter l’IDE.
  * Prise en charge de la gestion d’objets blob des comptes de stockage à l’aide d’Azure Resource Manager, qui complète les fonctionnalités existantes de gestion des comptes de stockage « Classic ».
* **Microsoft JDBC Driver 6.0 pour SQL Server**. Cette mise à jour inclut le dernier pilote JDBC de Microsoft SQL Server (version 6.0), qui est maintenant inclus en tant que bibliothèque facile à ajouter à vos projets Java, en remplacement de l’ancienne version.

### <a name="june-29-2016"></a>29 juin 2016
La version de juin 2016 du kit de ressources Azure pour IntelliJ inclut les améliorations suivantes :

* **Spécification Java 8**. Le kit de ressources Azure pour IntelliJ requiert désormais Java 8. Cette exigence ne s’applique qu’au kit de ressources, vos applications peuvent continuer à utiliser toutes les versions de Java prises en charge par Azure.
* **Prise en charge des JDK Java les plus récents**. Les dernières versions des JDK Java sont désormais prises en charge par le kit de ressources Azure pour IntelliJ.
* **Prise en charge du Kit de développement logiciel (SDK) Azure v2.9.1**. La dernière version du Kit de développement logiciel (SDK) Azure est désormais le minimum requis pour le Kit de ressources Azure pour IntelliJ.
* **Exemples intégrés**. Le kit de ressources Azure pour IntelliJ comporte désormais plusieurs exemples d’applications qui permettent aux développeurs de se lancer.
* **Intégration d’outils HDInsight**. Les outils HDInsight d’Azure sont désormais fournis avec le kit de ressources Azure pour IntelliJ. Pour plus d’informations, consultez [Plug-in Outils HDInsight pour IntelliJ].
* **Débogage à distance des applications web Java**. Le kit de ressources Azure pour IntelliJ prend désormais en charge le débogage à distance des applications web sur Azure App Service.

### <a name="april-12-2016"></a>12 avril 2016
La version d’avril 2016 du kit de ressources Azure pour IntelliJ inclut les améliorations suivantes :

* **Prise en charge du Kit de développement logiciel (SDK) Azure v2.9.0**. La dernière version du Kit de développement logiciel (SDK) Azure est désormais le minimum requis pour le Kit de ressources Azure pour IntelliJ.
* **Diverses améliorations de la convivialité, de la réactivité et des performances liées à la prise en charge d’Azure Web App**. Plusieurs optimisations des performances dans la façon dont le Kit de ressources communique avec Azure donnent une interface utilisateur plus réactive.
* **Possibilité de supprimer un conteneur d’application web existant dans Azure à partir d’IntelliJ**. Le Kit de ressources Azure pour IntelliJ vous permet désormais de supprimer un conteneur web Azure existant sans quitter IntelliJ.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Kit de ressources Azure pour Eclipse]: ../eclipse/azure-toolkit-for-eclipse.md

[Instructions de connexion à Azure pour le kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Comment publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Gestion des comptes de stockage avec l’Explorateur Azure pour IntelliJ]: ./azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer.md
[Gestion des machines virtuelles avec l’Explorateur Azure pour IntelliJ]: ./azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[Plug-in Outils HDInsight pour IntelliJ]: /azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin
