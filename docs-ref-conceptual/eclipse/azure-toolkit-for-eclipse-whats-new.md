---
title: "Nouveautés du kit de ressources Azure pour Eclipse"
description: "En savoir plus sur les dernières fonctionnalités du kit de ressources Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
ms.assetid: 16b066ea-aae7-4c30-9a12-fa0c3711b93e
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 09/11/2017
ms.author: robmcm;asirveda;martinsawicki
ms.openlocfilehash: 31af7e6494f978f341e1f99a30117c57ef30a05b
ms.sourcegitcommit: 256044d7cbce16dcb8dc4e195d0f63c10cb44d4e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/13/2017
---
# <a name="whats-new-in-the-azure-toolkit-for-eclipse"></a>Nouveautés du kit de ressources Azure pour Eclipse

## <a name="azure-toolkit-for-eclipse-releases"></a>Versions du kit de ressources Azure pour Eclipse
Cet article contient des informations sur les différentes versions et les dernières mises à jour du kit de ressources Azure pour Eclipse.

> [!NOTE]
> Il existe également une boîte à outils Azure pour l’environnement de développement IntelliJ. Pour plus d’informations, consultez [Kit de ressources Azure pour IntelliJ].
> 
> 

### <a name="april-14-2017"></a>14 avril 2017
La version d’avril 2017 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Expérience de connexion Azure améliorée** : le kit de ressources Azure pour Eclipse prend désormais en charge deux méthodes de connexion à votre compte Azure : *interactive* et *automatisée*. Pour plus d’informations, voir [Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse].
* **Publication à l’aide de conteneurs Docker** : à présent, vous pouvez publier vos applications web en tant que conteneurs Docker à l’aide du kit de ressources Azure pour Eclipse. Pour plus d’informations, voir [How to publish a Web App as a Docker Container using the Azure Toolkit for Eclipse (Comment publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse)].
* **Gestion des comptes de stockage** : le kit de ressources Azure pour Eclipse prend désormais en charge la gestion de vos comptes de stockage à partir de la vue de l’Explorateur Azure. Pour plus d’informations, voir [Gestion des comptes de stockage avec l’Explorateur Azure pour Eclipse].
* **Gestion des machines virtuelles** : le kit de ressources Azure pour Eclipse prend désormais en charge la gestion de vos machines virtuelles à partir de la vue de l’Explorateur Azure. Pour plus d’informations, voir [Gestion des machines virtuelles avec l’Explorateur Azure pour Eclipse].
* **Suppression de la prise en charge du débogage distant**. Le débogage distant des applications web Java dans Azure App Service a été supprimé du kit de ressources Azure pour Eclipse ; cette action était nécessaire pour résoudre certains problèmes rencontrés par les utilisateurs lors de l’utilisation du kit de ressources.

### <a name="august-26-2016"></a>26 août 2016
La version d’août 2016 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Distributions personnalisées du JDK**. Le kit de ressources Azure pour Eclipse prend désormais en charge la spécification et le déploiement d’une version arbitraire du JDK dans votre conteneur Azure WebApp :
  * Outre les JDK fournis par Azure, vous pouvez également choisir parmi une large sélection de versions Zulu OpenJDK mises à disposition sur Azure par Azul Systems.
  * Vous pouvez également spécifier votre propre distribution JDK si vous chargez un fichier ZIP sur votre compte de stockage.
* **Améliorations apportées à l’affichage de l’Explorateur Azure**:
  * Prise en charge de la gestion des Machines Virtuelles suivant le nouveau modèle Azure Resource Manager : vous pouvez lister, créer et supprimer des machines virtuelles Resource Manager sans quitter l’IDE.
  * Prise en charge de la gestion d’objets blob des comptes de stockage à l’aide d’Azure Resource Manager, qui complète les fonctionnalités existantes de gestion des comptes de stockage « Classic ».
* **Microsoft JDBC Driver 6.0 pour SQL Server**. Cette mise à jour inclut le dernier pilote JDBC de Microsoft SQL Server (version 6.0), qui est maintenant inclus en tant que bibliothèque facile à ajouter à vos projets Java, en remplacement de l’ancienne version.

### <a name="june-29-2016"></a>29 juin 2016
La version de juin 2016 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Spécification Java 8**. Le kit de ressources Azure pour Eclipse requiert désormais Java 8. Cette exigence ne s’applique qu’au kit de ressources, vos applications peuvent continuer à utiliser toutes les versions de Java prises en charge par Azure.
* **Prise en charge des JDK Java les plus récents**. Les dernières versions des JDK Java sont désormais prises en charge par le kit de ressources Azure pour Eclipse.
* **Prise en charge du Kit de développement logiciel (SDK) Azure v2.9.1**. La dernière version du Kit de développement logiciel (SDK) Azure est désormais le minimum requis pour le Kit de ressources Azure pour Eclipse.
* **Exemples intégrés**. Le kit de ressources Azure pour Eclipse comporte désormais plusieurs exemples d’applications qui permettent aux développeurs de se lancer.
* **Intégration d’outils HDInsight**. Les outils HDInsight d’Azure sont désormais fournis avec le kit de ressources Azure pour Eclipse. Pour en savoir plus, consultez [Utilisation du plug-in Outils HDInsight pour Eclipse].
* **Débogage à distance des applications web Java**. Le kit de ressources Azure pour Eclipse prend désormais en charge le débogage à distance des applications web sur Azure App Service.
* **Prise en charge de la version Luna d’Eclipse.** Luna est la nouvelle version IDE d’Eclipse requise minimale.

### <a name="april-12-2016"></a>12 avril 2016
La version d’avril 2016 du Kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge du Kit de développement logiciel (SDK) Azure v2.9.0**. La dernière version du Kit de développement logiciel (SDK) Azure est désormais le minimum requis pour le Kit de ressources Azure pour Eclipse.
* **Diverses améliorations de la convivialité, de la réactivité et des performances liées à la prise en charge d’Azure Web App**. Plusieurs optimisations des performances dans la façon dont le Kit de ressources communique avec Azure donnent une interface utilisateur plus réactive.
* **Possibilité de supprimer un conteneur d’application web existant dans Azure à partir d’Eclipse**. Le Kit de ressources Azure pour Eclipse vous permet désormais de supprimer un conteneur Azure Web existant sans quitter Eclipse.

### <a name="march-7-2016"></a>7 mars 2016
La version de mars 2016 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge du déploiement rapide d’applications Java légères**. Le kit de ressources Azure pour Eclipse prend désormais en charge le déploiement rapide des applications Java légères dans des conteneurs d’applications web Azure ; le déploiement d’applications Java ne prend plus que quelques secondes au lieu de quelques minutes.
* **Prise en charge de la gestion d’applications web à l’aide de la vue Azure Explorer**. La vue Azure Explorer dans le kit de ressources prend désormais en charge l’affichage, le démarrage et l’arrêt des applications web Azure.
* **Distributions mises à jour de Tomcat, Jetty et Zulu OpenJDK**. Le kit de ressources Azure pour Eclipse prend en charge des versions mises à jour de Tomcat, Jetty et Zulu OpenJDK pour les déploiements de Java dans les services cloud Azure.

### <a name="january-4-2016"></a>4 janvier 2016
La version de janvier 2016 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge des mises à jour de Zulu OpenJDK**. Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Distributions Tomcat et Jetty mises à jour**. Les distributions Jetty et Tomcat qui sont disponibles sur Microsoft Azure en vue d’une utilisation avec le kit de ressources Azure pour Eclipse ont été mises à jour.
* **Parité des fonctionnalités entre les kits de ressources Eclipse et IntelliJ pour Azure**. Le kit de ressources Azure pour Eclipse et le [Kit de ressources Azure pour IntelliJ] prennent désormais en charge le même jeu de fonctionnalités.

### <a name="september-1-2015"></a>1er septembre 2015
La version de septembre 2015 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge des mises à jour de Zulu OpenJDK**. Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Distributions Tomcat et Jetty mises à jour**. Les distributions Jetty et Tomcat qui sont disponibles sur Microsoft Azure en vue d’une utilisation avec le kit de ressources Azure pour Eclipse ont été mises à jour. (Ces distributions permettent aux développeurs de créer rapidement des projets de développement et de test à l’aide du kit de ressources Azure pour Eclipse.
* **Prise en charge des références Tomcat et Jetty mises à jour automatiquement**. Outre les versions spécifiques de Tomcat et de Jetty qui sont disponibles sur Azure, les développeurs peuvent désormais référencer une distribution désignée comme la dernière (mise à jour automatiquement), qui est automatiquement mise à jour vers la dernière distribution de chaque version majeure de Jetty ou de Tomcat au prochain recyclage de vos instances de rôle. (Le recyclage se produit automatiquement, mais les développeurs peuvent en déclencher un manuellement par le biais du portail Azure). Avec cette nouvelle fonctionnalité, les développeurs n’ont pas à redéployer leur application pour pouvoir mettre à jour leurs logiciels serveur. (
* (Cette fonctionnalité est actuellement destinée uniquement à des fins de développement et de test ou pour les applications non stratégiques. Elle n’est pas recommandée pour la production.)
* **Affichage d’Azure Explorer pour les objets blob, les files d’attente et les tables d’Azure Storage**. Cela permet aux développeurs d’effectuer un ensemble de tâches courantes avec leurs artefacts de stockage directement à partir de l’environnement de développement intégré (IDE) Eclipse. Ils peuvent par exemple supprimer, charger ou télécharger des objets blob.

### <a name="august-1-2015"></a>1 août 2015
La version d’août 2015 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Gestion de clés d’instrumentation Application Insights**. Cette mise à jour vous permet d’acquérir, de créer et de gérer vos clés d’instrumentation Application Insights directement à partir de l’environnement IDE Eclipse.
* **Microsoft JDBC Driver 4.1 pour SQL Server**. Cette mise à jour prend en charge le dernier pilote JDBC de Microsoft SQL Server.
* **Version 2.7 du Kit de développement logiciel (SDK) Azure**. Cette toute dernière mise à jour disponible pour le Kit de développement logiciel (SDK) Azure est la nouvelle condition préalable à l’installation du kit de ressources sur Windows. (Notez que cette version n’est pas nécessaire sur les systèmes d’exploitation autres que Windows.)
* **Prise en charge de la mise à jour Zulu OpenJDK v7**. Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].

### <a name="may-1-2015"></a>1 mai 2015
La version de mai 2015 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Interface utilisateur de sélection de serveur améliorée**. Cette version simplifie l’utilisation du kit de ressources sur les systèmes d’exploitation autres que Windows.
* **Prise en charge des projets Maven**. Cette version prend en charge les projets Maven en tant qu’applications, que le kit de ressources peut déployer vers Azure et utiliser pour configurer Application Insights.
* **Version 2.6 du Kit de développement logiciel (SDK) Azure**. Cette toute dernière mise à jour disponible pour le Kit de développement logiciel (SDK) Azure est la nouvelle condition préalable à l’installation du kit de ressources sur Windows. (Notez que cette version n’est pas nécessaire sur les systèmes d’exploitation autres que Windows.)
* **Mise à niveau du déploiement à la place de sa republication**. Si vous republiez un projet de déploiement alors que la version précédente est déjà en ligne, le kit de ressources utilise désormais la fonctionnalité de mise à niveau de déploiement d’Azure au lieu d’arrêter le déploiement précédent et de le republier depuis le début comme c’était le cas auparavant. Votre service cloud peut alors s’exécuter sans interruption à chaque fois que possible, ce qui permet d’atteindre une haute disponibilité même pendant une mise à jour. Cette amélioration accélère le processus de republication.
* **Prise en charge de la dernière mise à jour 40 de Zulu OpenJDK v8**. Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].

### <a name="march-9-2015"></a>9 mars 2015
La version de mars 2015 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge de Mac, d’Ubuntu et d’autres versions de Linux**. Cette version du kit de ressources Azure pour Eclipse prend désormais en charge Mac OS et plusieurs plateformes Unix. Les développeurs peuvent donc installer le kit de ressources pour créer, configurer et publier des projets Java sur Azure Cloud Services (PaaS) à partir d’Eclipse s’exécutant sur les systèmes d’exploitation autres que Windows.

> [!NOTE]
> Comme il s’agit d’une version préliminaire de cette fonctionnalité, il n’est pas recommandé de l’utiliser dans les environnements de production. Il n’existe pas de contrat de niveau de service (SLA) du service clientèle, mais tous les commentaires sont appréciés et encouragés.
> 
> 

* **Nouveau plug-in Application Insights**. Les développeurs peuvent désormais configurer la télémétrie de serveur automatique à l’aide d’Application Insights sur Azure.
* **Automatisation du déploiement en ligne de commande basée sur Ant**. Cette fonctionnalité permet aux développeurs d’automatiser la publication des nouvelles versions de leurs déploiements en utilisant Ant hors d’Eclipse. Un script prégénéré est automatiquement configuré pour un projet après son premier déploiement à partir d’Eclipse, et les déploiements suivants peuvent utiliser le script pour automatiser entièrement les déploiements via la ligne de commande uniquement.
* **Disponibilité de Tomcat et de Jetty sur Azure pour un déploiement plus simple et plus rapide**. Les développeurs peuvent à présent référencer directement différentes versions de Tomcat et de Jetty disponibles sur Azure au lieu de charger un serveur Java sur leurs comptes (ou via le kit de ressources). Il est donc inutile de charger un serveur Java pour les scénarios de prise en main rapides.
* **Méthode rapide pour publier des applications web Java sur Azure Cloud Services**. Pour réduire la courbe d’apprentissage pour des scénarios simples de développement et de test, les développeurs peuvent désormais publier des applications Java plus directement sur Azure. Au lieu de devoir passer par le processus de création et de configuration d’un projet de déploiement Azure, les applications sont déployées avec une instance par défaut de Tomcat v8 et de Zulu JVM (OpenJDK).

### <a name="january-30-2015"></a>30 janvier 2015
La version de janvier 2015 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge d’IBM® WebSphere® Application Server Liberty Core**. Cette version ajoute IBM WebSphere Application Server Liberty Core à la liste des serveurs d’applications pris en charge à partir desquels le kit de ressources est en mesure d’effectuer un déploiement vers Azure. Ce dernier ajout étoffe la liste actuelle des serveurs d’applications qui sont pris en charge &quot;prêts à l’emploi&quot; par le kit de ressources. Elle comprenait déjà diverses versions de Tomcat, Jetty, JBoss et GlassFish.
* **Inclusion du kit de développement logiciel (SDK) Application Insights**. Cette bibliothèque d’API clientes récemment publiée (v0.9.0) fait désormais partie du package de bibliothèques Azure pour Java.
* **Package des bibliothèques Azure pour Java mis à jour**. Cette mise à jour comprend des bibliothèques Azure pour Java v0.7.0, l’API de client de stockage v2.0.0 et le Kit de développement logiciel (SDK) Application Insights v0.9.0 qui vient d’être publié.

### <a name="november-12-2014"></a>12 novembre 2014
La version de novembre 2014 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge du Kit de développement logiciel (SDK) Azure 2.5**. Cette toute dernière mise à jour du Kit de développement logiciel (SDK) Azure est la nouvelle condition préalable pour le kit de ressources.
* **Prise en charge de la version mise à jour des packages Zulu OpenJDK v1.8, v1.7 et v1.6**. Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Prise en charge des nouvelles tailles Standard D pour les services cloud**, qui offrent des performances accrues et des ressources mémoire supplémentaires. Pour plus d'informations, consultez la page [Tailles de machine virtuelle et de service cloud pour Azure].

### <a name="october-17-2014"></a>17 octobre 2014
La version d’octobre 2014 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Amélioration des performances dans les scénarios de publication dans le cloud**. Le chargement des informations d’abonnement se fait beaucoup plus rapidement lorsque les utilisateurs possèdent plusieurs abonnements et comptes de stockage.
* **Prise en charge de la version mise à jour du package Zulu OpenJDK v1.8**. Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Prise en charge de la dépréciation des anciennes versions des JDK tiers**. Les packages de JDK déconseillés ne s’affichent plus dans le menu déroulant pour les nouveaux projets de déploiement. Les projets existants qui référencent les packages de JDK déconseillés continuent de les afficher pour le moment, mais il est recommandé de mettre à niveau ces projets pour qu’ils utilisent les dernières versions.
* **Version mise à jour de la bibliothèque d’API clientes Package des bibliothèques Azure pour Java**. Pour plus d’informations, consultez la page [API cliente Microsoft Azure].
* **Résolution des bogues.** Cette version contient plusieurs correctifs de bogues qui ont été apportés suite aux rapports utilisateur et aux tests.

### <a name="august-5-2014"></a>5 août 2014
La version d’août 2014 du kit de ressources Azure pour Eclipse inclut les améliorations suivantes :

* **Prise en charge du Kit de développement logiciel (SDK) Azure 2.4.** Les versions antérieures du kit de ressources pour Eclipse ne fonctionnent pas avec ce Kit de développement logiciel (SDK) qui vient d’être publié.
* **Versions mises à jour des packages Zulu OpenJDK v1.6, 1.7 et v1.8.** Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Version mise à jour de la bibliothèque d’API clientes Package des bibliothèques Azure pour Java.** Pour plus d’informations, consultez la page [API cliente Microsoft Azure].
* **Prise en charge du dernier format de fichier de paramètres de publication.** La version 2.0 du format de fichier de paramètres de publication est maintenant prise en charge.
* **Modifications architecturales en appui de la fonctionnalité de publication dans le cloud.** Le kit de ressources utilise maintenant la nouvelle API cliente Microsoft Azure pour Java pour la prise en charge de la publication dans le cloud.
* **Résolution des bogues.** Cette version contient plusieurs correctifs de bogues demandés par l’utilisateur.

### <a name="june-12-2014"></a>12 juin 2014
La version de juin 2014 du kit de ressources Azure pour Eclipse est une mise à jour de maintenance mineure qui fournit les améliorations suivantes :

* **Prise en charge du package Zulu OpenJDK v1.8.** Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Versions mises à jour des packages Zulu OpenJDK v1.6 et v1.7.** Pour plus d’informations, consultez la [page web d’Azul Systems correspondant à Zulu OpenJDK].
* **Version mise à jour de la bibliothèque d’API clientes Package des bibliothèques Azure pour Java.** Pour plus d’informations, consultez la page [API cliente Microsoft Azure].
* **Résolution des bogues.** Cette version contient plusieurs correctifs de bogues demandés par l’utilisateur.

### <a name="april-4-2014"></a>4 avril 2014
Publication de la version d’avril 2014 du plug-in Azure pour Eclipse. Il s’agit d’une mise à jour accompagnant la publication du Kit de développement logiciel (SDK) Azure 2.3, qui est un composant requis téléchargé automatiquement lorsque vous installez le plug-in. Cette mise à jour comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire de février 2014 :

* **Prise en charge de la version 2.3 du Kit de développement logiciel (SDK) Azure.** La version d’avril 2014 du plug-in Azure pour Eclipse requiert le Kit de développement logiciel (SDK) Azure 2.3. Lors de l’utilisation du nouveau plug-in, si vous ne possédez pas le Kit de développement logiciel (SDK) Azure 2.3, vous devez autoriser son installation. N’utilisez pas le Kit de développement logiciel (SDK) Azure 2.3 avec les versions antérieures du plug-in.
* **Mise à niveau des applications sans déploiement de package complet.** Lors du déploiement des applications Java qui font partie de votre projet, le plug-in les charge désormais automatiquement dans votre compte de stockage sélectionné afin que vous puissiez le mettre à jour et recycler les instances de rôle pour déployer les derniers bits d’application sans devoir régénérer ni redéployer l’ensemble du package.
* **Tomcat 8 est désormais un serveur d’applications reconnu.** Si vous sélectionnez un répertoire d’installation de Tomcat 8 sur votre ordinateur dans l’onglet **Serveur** de la boîte de dialogue **Projet de déploiement Azure**, le plug-in le détecte maintenant automatiquement et peut déployer Tomcat 8 de façon automatisée, à l’instar des anciennes versions de Tomcat figurant déjà dans la liste.
* **Mises à jour de package Azul Zulu OpenJDK : mise à jour 51 de la version 1.7 et mise à jour 47 de la version 1.6.** La mise à jour 51 du package Azul System Zulu OpenJDK v7 est disponible depuis cette publication. Les packages Zulu OpenJDK v6 sont disponibles depuis la mise à jour 47. Ces mises à jour s’ajoutent aux mises à jour 45, 40 et 25 des packages Zulu OpenJDK v7 précédemment disponibles.
* **Prise en charge des tailles de machine virtuelle Microsoft Azure A8 et A9.** À présent, vous pouvez déployer un service cloud vers les machines virtuelles de taille A8 et A9 à mémoire élevée. Pour plus d’informations sur ces tailles de machine virtuelle, consultez la rubrique [Tailles de machine virtuelle et de service cloud pour Azure].
* **Redirection automatique de HTTP vers HTTPS pour les rôles compatibles SSL.** Lorsque votre service cloud contient uniquement des rôles HTTPS, si la demande utilisateur spécifie le protocole HTTP, elle est alors automatiquement redirigée vers HTTPS. Il est inutile de créer un rôle distinct pour gérer les requêtes HTTP.
* **Émulateur express utilisé pour l’émulation locale.** L’émulateur express Azure est maintenant utilisé comme émulateur lors du débogage local de vos applications.
* **Azure est renommé Microsoft Azure.** Les écrans de l’interface utilisateur indiquent désormais qu’Azure a été renommé Microsoft Azure et n’est plus appelé ainsi.

### <a name="february-6-2014"></a>6 février 2014
Publication de la version préliminaire de février 2014 du plug-in Azure pour Eclipse. Cette mise à jour comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire d’octobre 2013 :

* **Prise en charge du déchargement SSL.** Le déchargement SSL (Secure Sockets Layer) a été ajouté en tant que fonctionnalité, ce qui vous permet d’activer facilement la prise en charge du protocole sécurisé HTTPS (Hypertext Transfer Protocol Secure) dans votre déploiement Java sur Azure, sans avoir à configurer SSL dans votre serveur d’applications Java. Cela est particulièrement approprié dans les scénarios de communication authentifiée et/ou d’affinité de session, par exemple, lors de l’utilisation du filtre ACS (Access Control Service), qui est déjà pris en charge par le kit de ressources. Pour plus d’informations, consultez [Déchargement SSL] et [Comment utiliser le déchargement SSL].
* **GlassFish 4 est désormais un serveur d’applications reconnu.** Si vous sélectionnez un répertoire d’installation de GlassFish 4 sur votre ordinateur dans l’onglet **Serveur** de la boîte de dialogue **Projet de déploiement Azure**, le plug-in le détecte maintenant automatiquement et peut déployer GlassFish OSE 4 de façon automatisée, à l’instar de la version GlassFish OSE 3 figurant déjà dans la liste.
* **Mise à jour 45 du package Azul Zulu OpenJDK.** La mise à jour 45 du package Azul System Zulu OpenJDK v7 est disponible depuis cette publication. Elle s’ajoute aux mises à jour 40 et 25 déjà disponibles.
* **Prise en charge du paramètre Automatique pour les ports des points de terminaison privés.** Vous pouvez définir un port privé sur automatique pour les points de terminaison d’entrée et internes pour permettre à Azure d’affecter automatiquement un port à ce point de terminaison. Auparavant, vous ne pouviez qu’affecter un numéro de port spécifique.
* **Prise en charge de la personnalisation du nom de certificat dans l’interface utilisateur de création de certificat auto-signé.** Auparavant, un même nom codé en dur était utilisé pour tous les nouveaux certificats. Désormais, vous pouvez spécifier votre propre nom de certificat pour permettre de faire la distinction entre plusieurs certificats dans le portail Azure utilisés à des fins différentes.
* **Barre d’outils Azure :** la barre d’outils Azure a été mise à jour avec les modifications suivantes : 
  * ![][ic710876] Cette icône a été ajoutée pour le **nouveau projet de déploiement Azure**.
  * ![][ic710877] Cette icône a été ajoutée en tant que raccourci vers la boîte de dialogue de création de certificat auto-signé.
* **Prise en charge de la taille de machine virtuelle Azure A5.** À présent, vous pouvez déployer un service cloud vers les machines virtuelles de taille A5 à mémoire élevée. Pour plus d’informations sur cette taille de machine virtuelle, consultez la rubrique [Tailles de machine virtuelle et de service cloud pour Azure].
* **Prise en charge de Microsoft Windows Server 2012 R2.** Vous pouvez désormais sélectionner Windows Server 2012 R2 comme système d’exploitation cloud.

### <a name="october-22-2013"></a>22 octobre 2013
Publication de la version préliminaire d’octobre 2013 du plug-in Azure pour Eclipse. Cette mise à jour comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire de septembre 2013 :

* **Prise en charge de la version 2.2 du Kit de développement logiciel (SDK) Azure.** La version préliminaire d’octobre 2013 du plug-in Azure pour Eclipse prend en charge le Kit de développement logiciel (SDK) Azure 2.2. Le plug-in continue de fonctionner avec le Kit de développement logiciel (SDK) Azure 2.1 et installe automatiquement le Kit de développement logiciel (SDK) Azure 2.2 si vous n’avez pas encore installé au moins le Kit de développement logiciel (SDK) Azure 2.1.
* **Mise à jour 40 du package Azul Zulu OpenJDK.** Comme annoncé pour la version préliminaire de septembre 2013, le plug-in permet désormais d’utiliser directement un JDK tiers sur Azure, sans que vous deviez charger votre propre JDK. La mise à jour 40 du package Azul System Zulu OpenJDK v7 est disponible dans la publication d’octobre 2013. Elle s’ajoute à la mise à jour 25 déjà publiée.
* **Lien de déploiement cloud dans le journal d’activité.** Dans le journal des activités Azure, si votre déploiement a l’état **Publié**, vous pouvez cliquer sur **Publié** puisqu’il s’agit d’un lien vers votre déploiement, lequel s’ouvre alors dans votre navigateur. (L’état **Publié** était précédemment étiqueté **En cours d’exécution**.)
* **Sélection du système d’exploitation cible disponible au moment de la publication.** La boîte de dialogue **Publier sur Azure** contient un nouveau champ, **Système d’exploitation cible**, qui permet de définir votre système d’exploitation cible de façon plus détectable.
* **Remplacer automatiquement le déploiement précédent.** La boîte de dialogue **Publier sur Azure** contient la nouvelle case à cocher **Remplacer automatiquement le déploiement précédent**. Si cette option est activée, votre nouveau déploiement remplace automatiquement le déploiement précédent lorsqu’il est publié. Vous ne rencontrez pas de problèmes &quot;Conflit (409)&quot; lors de la publication vers le même emplacement sans annulation préalable du déploiement précédent.
* **Jetty 9 est désormais un serveur d’applications reconnu.** Si vous sélectionnez un répertoire d’installation de Jetty 9 sur votre ordinateur dans l’onglet **Serveur** de la boîte de dialogue **Projet de déploiement Azure**, le plug-in le détecte maintenant automatiquement et peut déployer Jetty 9 de façon automatisée, à l’instar des anciennes versions de Jetty figurant déjà dans la liste.
* **Ajout d’un rôle à partir du menu contextuel Projet.** Le menu contextuel du projet **Azure** contient désormais un nouvel élément de menu, **Ajouter un rôle**, qui fournit un moyen plus rapide et plus détectable d’ajouter un rôle à votre projet Azure.
* **Mise à jour de la bibliothèque Package des bibliothèques Azure pour Java.** Elle est basée sur la version 0.4.6 de l’ [API cliente Microsoft Azure].

### <a name="september-25-2013"></a>25 septembre 2013
Publication de la version préliminaire de septembre 2013 du plug-in Azure pour Eclipse. Cette mise à jour comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire d’août 2013 :

* **Capacité à déployer le package Azul Zulu OpenJDK disponible sur Azure.** Une nouvelle option a été ajoutée lors de la spécification du JDK à utiliser avec votre déploiement Azure. En utilisant cette option, vous pouvez déployer un package JDK tiers directement sur le cloud Azure sans devoir charger le vôtre. Azul Systems fournit le premier package de ce type nommé Zulu et basé sur OpenJDK, qui peut désormais être déployé à l’aide de cette option.
* **Mise à jour de la bibliothèque Package des bibliothèques Azure pour Java.** Elle est basée sur la version 0.4.5 de l’ [API cliente Microsoft Azure].

### <a name="august-1-2013"></a>1 août 2013
Publication de la version préliminaire d’août 2013 du plug-in Azure pour Eclipse. Il s’agit d’une mise à jour accompagnant la publication du Kit de développement logiciel (SDK) Azure 2.1, qui est un composant requis téléchargé automatiquement lorsque vous installez le plug-in. Cette mise à jour comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire de juillet 2013 :

* **Suppression des options permettant d’inclure le JDK et le serveur d’applications locaux dans le cadre du package de déploiement.** Le téléchargement du JDK et du serveur d’applications à partir du stockage cloud au cours du déploiement est préférable à l’incorporation de ces composants dans le package, car leur téléchargement entraîne une taille de package de déploiement plus petite, des durées de déploiement plus courtes et des tâches de maintenance simplifiées. En conséquence, les options permettant d’inclure le JDK et le serveur d’applications dans le package de déploiement ont été supprimées. Les projets existants qui étaient configurés pour inclure le JDK et le serveur d’applications locaux dans le package de déploiement sont automatiquement convertis pour charger automatiquement le JDK et le serveur d’applications vers le stockage cloud.
* **Prise en charge de la version 2.1 du Kit de développement logiciel (SDK) Azure.** La version préliminaire d’août 2013 du plug-in Azure pour Eclipse requiert le Kit de développement logiciel (SDK) Azure 2.1. N’utilisez pas la version préliminaire d’août 2013 avec les versions antérieures du Kit de développement logiciel (SDK) Azure, ni le Kit de développement logiciel (SDK) Azure 2.1 avec les versions antérieures du plug-in Azure pour Eclipse.
* **Prise en charge de la version Kepler d’Eclipse.** En conséquence, Indigo est la nouvelle version IDE d’Eclipse requise minimale. Le plug-in Azure pour Eclipse n’est plus testé officiellement sur Helios.

### <a name="july-3-2013"></a>3 juillet 2013
Publication de la version préliminaire de juillet 2013 du plug-in Azure pour Eclipse. Cette mise à jour comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire de mai 2013 :

* **Possibilité de créer un compte de stockage.** Un bouton **Nouveau** a été ajouté à la boîte de dialogue **Ajouter un compte de stockage**. Cela vous permet de créer un compte de stockage dans le plug-in Eclipse sans avoir à vous connecter au portail de gestion Azure. (Pour utiliser cette fonctionnalité, vous devez posséder un abonnement Azure.) Pour plus d’informations sur la création d’un compte de stockage, consultez la rubrique [Pour créer un compte de stockage].
* **Nouvelle option &quot;(auto)&quot; de compte de stockage utilisée pour le déploiement automatique du JDK et du serveur et pour la mise en cache.** Lorsque vous utilisez l’option **Charger automatiquement** pour le JDK et le serveur d’applications, vous pouvez désormais spécifier **(auto)** pour l’URL et le compte de stockage à utiliser lors du chargement du JDK et du serveur d’applications ou lors de l’utilisation de la mise en cache Azure. Ces fonctionnalités utilisent alors automatiquement le même compte de stockage que celui que vous sélectionnez dans la boîte de dialogue **Publier sur Azure** . Le didacticiel [Création d’une application Hello World pour Azure dans Eclipse] a été mis à jour pour utiliser la nouvelle option **(auto)** .
* **Possibilité de définir vos points de terminaison de service Azure.** Spécifiez les points de terminaison de service qui déterminent si votre application est déployée sur et gérée par la plateforme globale Azure, sur Azure exploité par 21Vianet en Chine ou sur une plateforme Azure privée. Pour plus d’informations, consultez [Points de terminaison de service Azure].
* **Les déploiements à grande échelle peuvent spécifier une ressource de stockage local.** Si votre déploiement est trop volumineux pour être contenu dans le dossier approot par défaut, vous pouvez désormais spécifier une ressource de stockage local comme destination de déploiement pour votre JDK et votre serveur d’applications. Pour plus d’informations, consultez la page [Réalisation de déploiements volumineux].
* **Prise en charge des tailles de machines virtuelles Azure A6 et A7.** À présent, vous pouvez déployer un service cloud vers les machines virtuelles de taille A6 et A7 à mémoire élevée. Pour plus d’informations sur ces tailles, consultez la rubrique [Tailles de machine virtuelle et de service cloud pour Azure].
* **Mise à jour de la bibliothèque Package des bibliothèques Azure pour Java.** Elle est basée sur la version 0.4.4 de l’ [API cliente Microsoft Azure].

### <a name="may-1-2013"></a>1er mai 2013
Publication de la version préliminaire de mai 2013 du plug-in Azure pour Eclipse. Il s’agit d’une mise à jour majeure accompagnant la publication du Kit de développement logiciel (SDK) Azure 2.0, qui est un composant requis téléchargé automatiquement lorsque vous installez le plug-in. Cette version comprend de nouvelles fonctionnalités, des correctifs de bogues et certaines améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire de février 2013 :

* **Chargement automatique du JDK et du serveur d’applications vers le stockage Azure et déploiement de ces composants à partir du stockage Azure.** Nouvelle option qui permet de charger automatiquement le JDK et le serveur d’applications sélectionnés, au besoin, vers un compte de stockage Azure spécifié, et de déployer ces composants à partir de là, au lieu de les incorporer au package de déploiement ou de demander à l’utilisateur de les charger manuellement. Cette fonctionnalité souvent demandée peut améliorer considérablement la facilité de déploiement des composants serveur et JDK, notamment pour les utilisateurs débutants. Pour connaître la procédure pas à pas utilisant ces options, consultez le didacticiel [Création d’une application Hello World pour Azure dans Eclipse].
* **Suivi de compte de stockage centralisé et possibilité de référencer plus facilement les comptes de stockage (via une liste déroulante).** Cela s’applique à plusieurs fonctionnalités qui reposent sur le stockage, comme le déploiement des composants JDK et serveur, et la mise en cache. Pour plus d’informations, consultez [Liste des comptes de stockage Azure].
* **Configuration de l’accès à distance simplifié dans l’Assistant Publication dans le cloud.** Il vous suffit de taper un nom d’utilisateur et un mot de passe pour activer l’accès à distance, ou de laisser ces champs vides pour laisser l’accès à distance désactivé.
* **Mise à jour de la bibliothèque Package des bibliothèques Azure pour Java.** Elle est basée sur la version 0.4.2 de l’ [API cliente Microsoft Azure].
* **Prise en charge des sessions rémanentes sur Windows Server 2012.** Auparavant, les sessions rémanentes ne fonctionnaient que sur Windows Server 2008 R2 ; désormais, les deux cibles de système d’exploitation cloud prennent en charge l’affinité de session.
* **Améliorations des performances de chargement de package.** Même lorsque le JDK et le serveur d’applications sont incorporés au package de déploiement, la partie chargement du processus de déploiement peut être environ deux fois plus rapide qu’avec les versions précédentes.

### <a name="february-8-2013"></a>8 février 2013
Publication de la version préliminaire de février 2013 du plug-in Azure pour Eclipse. Cette mise à jour mineure comprend des correctifs de bogues, des améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients et certaines nouvelles fonctionnalités depuis la version préliminaire de novembre 2012 :

* Prise en charge du déploiement des JDK, des serveurs d’applications et d’autres composants à partir des téléchargements de stockage des objets blob Azure public ou privé. Ces composants ne sont plus inclus dans le package de déploiement pour être déployés dans le cloud.
* Possibilité de modifier l’ordre dans lequel les composants définis par l’utilisateur d’un rôle sont traités via l’ajout des boutons **Monter** et **Descendre** dans la section **Composants** de la boîte de dialogue **Propriétés de rôle Azure**.
* Mise à jour de la bibliothèque **Package des bibliothèques Azure pour Java** basée sur la version 0.4.0 de l’ [API cliente Microsoft Azure].

### <a name="november-5-2012"></a>5 novembre 2012
Publication de la version préliminaire de novembre 2012 du plug-in Azure pour Eclipse. Il s’agit d’une mise à jour majeure qui inclut plusieurs nouvelles fonctionnalités, ainsi que des correctifs de bogues supplémentaires et des améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients depuis la version préliminaire de septembre 2012 :

* Prise en charge de Microsoft Windows Server 2012 en tant que système d’exploitation cloud.
* Prise en charge de la mise en cache colocalisée Azure pour les clients Memcached.
* Inclusion des bibliothèques clientes Apache Qpid JMS pour tirer parti de la messagerie AMQP Azure.
* Assistant **Nouveau projet** amélioré, avec une nouvelle dernière page, qui permet aux utilisateurs d’activer rapidement plusieurs fonctionnalités clés courantes dans leur projet : sessions rémanentes, mise en cache et débogage à distance.
* Réduction automatique des instances de rôle à 1 lors de l’exécution dans l’émulateur de calcul, afin d’éviter des conflits de liaison de port entre les instances de serveur.

### <a name="september-28-2012"></a>28 septembre 2012
Publication de la version préliminaire de septembre 2012 du plug-in Azure pour Eclipse. Cette mise à jour de service comprend plusieurs correctifs de bogues supplémentaires depuis la version préliminaire d’août 2012, ainsi que des améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients pour les fonctionnalités existantes :

* Prise en charge de Microsoft Windows 8 et de Microsoft Windows Server 2012 en tant que système d’exploitation de développement, ce qui résout les problèmes qui empêchaient auparavant le plug-in de fonctionner correctement sur ces systèmes d’exploitation.
* Prise en charge améliorée de la spécification des plages de ports de point de terminaison.
* Correctifs de bogues liés aux chemins d’accès de fichier contenant des espaces.
* Améliorations du menu contextuel Rôle pour un accès plus rapide aux paramètres de configuration propres aux rôles.
* Améliorations mineures de l’Assistant **Publication sur le cloud** et correctifs de bogues supplémentaires.

### <a name="august-28-2012"></a>28 août 2012
Publication de la version préliminaire d’août 2012 du plug-in Azure pour Eclipse. Cette mise à jour de service comprend des correctifs de bogues supplémentaires depuis la version préliminaire de juillet 2012, ainsi que plusieurs améliorations apportées à la convivialité qui s’appuient sur les commentaires des clients pour les fonctionnalités existantes :

* Dans la boîte de dialogue Filtre Azure Access Control Service :
  * **Option permettant d’incorporer le certificat de signature** dans le fichier WAR de votre application, afin de simplifier le déploiement cloud.
  * **Option permettant de créer un certificat auto-signé** dans l’interface utilisateur du filtre ACS. Pour plus d’informations sur le filtre Azure Access Control Service, consultez [Authentification des utilisateurs web auprès d’Azure Access Control Service à l’aide d’Eclipse].
* Dans l’Assistant Projet de déploiement Azure (s’applique également à la page des propriétés Configuration du serveur du rôle) :
  * **Détection automatique de l’emplacement du JDK** sur votre ordinateur (que vous pouvez remplacer si vous le souhaitez).
  * **Détection automatique du type de serveur** lorsque vous sélectionnez le répertoire d’installation du serveur d’applications.

### <a name="july-15-2012"></a>15 Juillet 2012
Publication de la version préliminaire de juillet 2012 du plug-in Azure pour Eclipse. Elle résout plusieurs bogues de priorité élevée trouvés et/ou signalés par des utilisateurs après la publication de juin 2012. Il s’agit d’une mise à jour de service uniquement ; aucune nouvelle fonctionnalité n’est incluse.

### <a name="june-7-2012"></a>7 juin 2012
Publication de la version préliminaire CTP (Community Technology Preview) de juin 2012 du plug-in Azure pour Eclipse. Nouvelles fonctionnalités :

* **Nouvel Assistant Projet de déploiement Azure** : vous permet de sélectionner directement votre JDK, votre serveur d’applications Java et les applications Java dans l’interface utilisateur améliorée de l’Assistant. Vous pouvez effectuer un choix parmi les configurations de serveur prêtes à l’emploi de la liste : Tomcat 6, Tomcat 7, GlassFish OSE 3, Jetty 7, Jetty 8, JBoss 6 et JBoss 7 (autonome). En outre, vous pouvez personnaliser la liste des configurations de serveur. Cette amélioration de l’interface utilisateur est une alternative au glisser-déplacer des fichiers compressés et à leur copie sur les scripts de démarrage, ce qui constituait auparavant l’approche principale. Cette méthode fonctionne toujours, mais sera probablement utilisée uniquement pour des scénarios plus avancés.
* **Page des propriétés de rôle de configuration de serveur** : vous permet de basculer facilement entre les JDK, les serveurs d’applications Java et les applications associés à votre déploiement après avoir créé le projet. Pour plus d’informations, consultez la section [Propriétés de configuration de serveur].
* **Assistant &quot;Publication sur le cloud&quot; :** permet de déployer facilement votre projet sur Azure directement à partir d’Eclipse, en automatisant la récupération des informations d’identification auparavant manuelle, la connexion au portail de gestion Azure, le chargement d’un package, etc. Pour obtenir un exemple de déploiement direct de votre projet sur Azure, consultez le didacticiel [Création d’une application Hello World pour Azure dans Eclipse].
* **Barre d’outils Azure** : une barre d’outils Azure est désormais disponible dans Eclipse. Elle contient des boutons qui appellent les fonctionnalités suivantes :
  * ![][ic710879] **Exécuter dans l’émulateur Azure**: exécute votre projet dans l’émulateur.
  * ![][ic710880] **Réinitialiser l’émulateur Azure**: réinitialise l’émulateur.
  * ![][ic710881] **Générer un package cloud pour Azure**: compile votre package pour le déploiement.
  * ![][ic710876] **Nouveau projet de déploiement Azure**: crée un projet de déploiement Azure.
  * ![][ic710882] **Publier dans le cloud Azure**: publie votre projet sur Azure.
  * ![][ic710883] **Annuler la publication**: supprime votre déploiement.
  * Nombre de ces boutons de la barre d’outils Azure sont utilisés dans le didacticiel [Création d’une application Hello World pour Azure dans Eclipse].
* **Bibliothèques Azure pour Java** : désormais disponibles dans la bibliothèque Package des bibliothèques Azure pour Java dans Eclipse, elles accompagnent l’installation du plug-in et contiennent également toutes les dépendances nécessaires. Il vous suffit d’ajouter une référence à la bibliothèque de votre projet Java. Vous n’avez pas besoin de télécharger quoi que ce soit séparément. Pour plus d’informations, consultez [Installation du kit de ressources Azure pour Eclipse].
* **Microsoft JDBC Driver 4.0 pour SQL Server disponible pendant l’installation du plug-in** : pendant l’installation du nouveau plug-in, la dernière version de Microsoft JDBC Driver pour SQL Server peut être installée.
* **Filtre Azure Access Control Service disponible pendant l’installation du plug-in** : ce nouveau composant, inclus en tant que bibliothèque Eclipse dans le kit de ressources, permet à votre application web Java de tirer pleinement parti de l’authentification Azure ACS à l’aide de différents fournisseurs d’identité tels que Google, Live.com et Yahoo!. Vous n’avez pas besoin d’écrire une logique d’authentification vous-même, il vous suffit de configurer quelques options et de laisser le filtre se charger de permettre aux utilisateurs de se connecter à l’aide d’ACS. Vous pouvez vous consacrer uniquement à l’écriture du code qui permet aux utilisateurs d’accéder à des ressources en fonction de leur identité, telle qu’elle est retournée à votre application par le filtre dans l’objet Request. Pour suivre un didacticiel sur l’utilisation du filtre ACS, consultez [Authentification des utilisateurs web auprès d’Azure Access Control Service à l’aide d’Eclipse].
* **Détection automatique de du Kit de développement logiciel (SDK) Azure 1.7** : lorsque vous créez un projet de déploiement Azure, le Kit de développement logiciel (SDK) Azure 1.7 est automatiquement téléchargé s’il n’est pas déjà installé.
* **Points de terminaison d’instance** : autorise l’accès direct des points de terminaison de port pour communiquer avec des instances de rôle à charge équilibrée. Des points de terminaison d’instance peuvent être ajoutés via l’interface utilisateur des points de terminaison, disponible dans la page [Propriétés des points de terminaison] . Cela permet d’activer le débogage à distance et les diagnostics JMX pour des instances de calcul spécifiques s’exécutant dans le cloud, dans des scénarios comprenant des déploiements de plusieurs instances. 
* **Interface utilisateur des composants** : permet aux utilisateurs avancés de configurer plus facilement les dépendances de projet entre des rôles Azure individuels dans les ressources de projet et d’autres ressources externes, par exemple les projets d’application Java. Elle facilite également la description de leur logique de déploiement. Pour plus d’informations, consultez les [propriétés des composants].
* **Mise à niveau automatique des versions précédentes des projets** : lorsque vous ouvrez un espace de travail qui comporte un projet Azure créé avec une version précédente du plug-in, les anciens projets apparaissent dans Eclipse comme étant fermés, car les versions précédentes des projets ne sont pas compatibles avec la nouvelle version. Si vous tentez d’ouvrir l’un de ces anciens projets, un Assistant de mise à niveau démarre. Si vous acceptez la mise à niveau, un nouveau projet dont le nom contient le suffixe **_Upgraded** est créé et mis à jour automatiquement pour fonctionner avec la nouvelle version. Vous pouvez renommer le nouveau projet si nécessaire. Dans le cadre de la mise à niveau, votre projet d’origine n’est pas modifié (et reste fermé).

### <a name="december-10-2011"></a>10 décembre 2011
Publication de la version préliminaire CTP de décembre 2011 du plug-in Azure pour Eclipse. Nouvelles fonctionnalités :

* **Prise en charge de l’affinité de session (&quot;sessions rémanentes&quot;)** : permet d’activer des applications Java en cluster avec état à l’aide d’une seule case à cocher. Pour plus d’informations, voir l’article [Affinité de session].
* **Exemples de script de démarrage préconçus** : pour les principaux serveurs Java (Tomcat, Jetty, JBoss et GlassFish), que vous pouvez simplement copier/coller à partir du répertoire d’exemples de votre projet dans votre script de démarrage.
* **Sortie de démarrage d’émulateur en temps réel** : vous pouvez désormais visionner l’exécution de toutes les étapes de votre script de démarrage dans une fenêtre de console dédiée, qui vous indique la progression et les échecs de votre script lorsqu’il est exécuté par Azure.
* **Surveillance de java.exe automatique et légère** : force un recyclage des rôles quand java.exe cesse de s’exécuter, en utilisant un script léger, préconçu inclus automatiquement dans votre déploiement.
* **Interface utilisateur de configuration de débogage à distance d’application Java** : vous permet d’activer facilement le débogueur distant d’Eclipse afin d’accéder à votre application Java s’exécutant dans l’émulateur ou dans le cloud Azure. Vous pouvez donc parcourir et déboguer votre code Java en temps réel. Pour plus d’informations, consultez [Débogage des applications Azure dans Eclipse].
* **Interface utilisateur de configuration des ressources de stockage locales** : vous n’avez plus à configurer de ressources locales en manipulant directement le code XML. Cette fonctionnalité vous permet également d’accéder au chemin d’accès de fichier de votre ressource locale après son déploiement via une variable d’environnement que vous pouvez référencer directement à partir de votre script de démarrage. Pour plus d’informations, consultez les [propriétés de stockage local].
* **Interface utilisateur de configuration des variables d’environnement** : vous n’avez plus à définir les variables d’environnement via une modification manuelle du code XML de configuration. Pour plus d’informations, consultez les [propriétés des variables d’environnement].
* **Pilote JDBC pour SQL Azure** : installé via le plug-in en tant que bibliothèque Eclipse intégrée en toute transparence, il facilite la programmation dans SQL Azure. 
* **Accès rapide par le menu contextuel à l’interface utilisateur de configuration des rôles** : cliquez simplement avec le bouton droit sur le dossier de rôles, puis cliquez sur **Propriétés**.
* **Icônes personnalisées du dossier de projet Azure et du dossier de rôles** : pour une meilleure visibilité et une navigation plus aisée au sein de votre projet et de votre espace de travail.

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Kit de ressources Azure pour IntelliJ]: ../intellij/azure-toolkit-for-intellij.md
[Installation du kit de ressources Azure pour Eclipse]: azure-toolkit-for-eclipse-installation.md

[Instructions de connexion à Azure pour le kit de ressources Azure pour Eclipse]: azure-toolkit-for-eclipse-sign-in-instructions.md
[Comment publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour Eclipse]: ./azure-toolkit-for-eclipse-publish-as-docker-container.md
[Gestion des comptes de stockage avec l’Explorateur Azure pour Eclipse]: ./azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer.md
[Gestion des machines virtuelles avec l’Explorateur Azure pour Eclipse]: ./azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer.md

[Azure Java Developer Center]: https://docs.microsoft.com/java/azure

[page web d’Azul Systems correspondant à Zulu OpenJDK]: http://go.microsoft.com/fwlink/?LinkId=402457
[Points de terminaison de service Azure]: http://go.microsoft.com/fwlink/?LinkID=699526
[Liste des comptes de stockage Azure]: http://go.microsoft.com/fwlink/?LinkID=699528
[Propriétés des composants]: http://go.microsoft.com/fwlink/?LinkID=699525#components_properties
[Création d’une application Hello World pour Azure dans Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Débogage des applications Azure dans Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699535
[Réalisation de déploiements volumineux]: http://go.microsoft.com/fwlink/?LinkID=699536
[Propriétés des points de terminaison]: http://go.microsoft.com/fwlink/?LinkID=699525#endpoints_properties
[propriétés des variables d’environnement]: http://go.microsoft.com/fwlink/?LinkID=699525#environment_variables_properties
[Utilisation du plug-in Outils HDInsight pour Eclipse]: /azure/hdinsight/hdinsight-apache-spark-eclipse-tool-plugin
[Authentification des utilisateurs web auprès d’Azure Access Control Service à l’aide d’Eclipse]: http://go.microsoft.com/fwlink/?LinkID=264703
[Comment utiliser le déchargement SSL]: http://go.microsoft.com/fwlink/?LinkID=699545
[propriétés de stockage local]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties
[API cliente Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=280397
[Propriétés de configuration de serveur]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[Affinité de session]: http://go.microsoft.com/fwlink/?LinkID=699548
[Déchargement SSL]: http://go.microsoft.com/fwlink/?LinkID=699549
[Pour créer un compte de stockage]: http://go.microsoft.com/fwlink/?LinkID=699528#create_new
[Tailles de machines virtuelles et services cloud pour Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=466520

<!-- IMG List -->

[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710877]: media/azure-toolkit-for-eclipse-whats-new/ic710877.png
[ic710879]: media/azure-toolkit-for-eclipse-whats-new/ic710879.png
[ic710880]: media/azure-toolkit-for-eclipse-whats-new/ic710880.png
[ic710881]: media/azure-toolkit-for-eclipse-whats-new/ic710881.png
[ic710876]: media/azure-toolkit-for-eclipse-whats-new/ic710876.png
[ic710882]: media/azure-toolkit-for-eclipse-whats-new/ic710882.png
[ic710883]: media/azure-toolkit-for-eclipse-whats-new/ic710883.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh694270.aspx -->
