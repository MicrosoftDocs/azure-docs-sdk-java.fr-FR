---
title: "Déployer une application Spring Boot sur Azure App Service"
description: "Ce didacticiel guide les développeurs à travers les étapes de déploiement de l’application web Spring Boot Getting Started sur Azure App Service."
services: app-service
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: 
keywords: Spring, Spring Boot, Spring Framework
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: java
ms.topic: article
ms.date: 10/11/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 5a0f13e1883c1de1adb72c450c55dcb38b1520b9
ms.sourcegitcommit: 7f8538e41c833deb69c300ad3431a431136a1f3e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a>Déployer une application Spring Boot sur Azure App Service

**[Spring Framework]** une solution open source qui permet aux développeurs Java de créer des applications d’entreprise. Un des projets les plus populaires s’appuyant sur cette plateforme est [Spring Boot], qui offre une approche simplifiée pour la création d’applications Java autonomes.

Ce didacticiel vous montre comment créer l’exemple d’application web Spring Boot Getting Started et la déployer sur [Azure App Service].

### <a name="prerequisites"></a>Composants requis

Pour pouvoir effectuer les étapes de ce didacticiel, vous avez besoin des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Un [JDK (Java Developer Kit)] à jour.
* L’outil de génération [Maven] (version 3) d’Apache.
* Un [client Git].

## <a name="create-the-spring-boot-getting-started-web-app"></a>Créer l’application web Spring Boot Getting Started

La procédure suivante vous guide à travers les étapes nécessaires pour créer une application web Spring Boot simple et pour la tester localement.

1. Ouvrez une invite de commandes et créez un répertoire local pour y stocker votre application, puis accédez à ce répertoire. Par exemple :
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   - ou -
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Clonez l’exemple de projet [Spring Boot Getting Started] dans le répertoire que vous venez de créer. Par exemple :
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Accédez au répertoire du projet terminé. Par exemple :
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Générez le fichier JAR en utilisant Maven. Par exemple :
   ```
   mvn package
   ```

1. Une fois que l’application web a été créée, accédez au répertoire du fichier JAR et démarrez l’application web. Par exemple :
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Testez l’application web en accédant à http://localhost:8080 avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :
   ```
   curl http://localhost:8080
   ```

1. Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**

   ![Parcourir l’exemple d’application][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Créer une application web Azure à utiliser avec Java

La procédure suivante vous guide à travers les étapes pour créer une application web Azure, configurer les paramètres nécessaires pour Java et configurer vos informations d’identification FTP.

1. Accédez au [portail Azure] et connectez-vous.

1. Une fois que vous êtes connecté à votre compte sur le portail Azure, cliquez sur l’icône du menu pour **App Services** :
   
   ![Portail Azure][AZ01]

1. Quand la page **App Services** est affichée, cliquez sur **+ Ajouter** pour créer un nouvel App Service.

   ![Créer un App Service][AZ02]

1. Quand la liste des modèles d’application web s’affiche, cliquez sur le lien pour l’application web Microsoft de base.

   ![Modèles d’application web][AZ03]

1. Quand la page d’informations pour le modèle d’application web s’affiche, cliquez sur **Créer**.

   ![Créer une application web][AZ04]

1. Indiquez un nom unique pour votre application web et spécifiez les éventuels paramètres supplémentaires, puis cliquez sur **Créer**.

   ![Créer les paramètres d’une application web][AZ05]

1. Une fois que votre application web a été créée, cliquez sur l’icône du menu **App Services** puis cliquez sur votre application web nouvellement créée :

   ![Répertorier les applications web][AZ06]

1. Quand votre application web s’affiche, spécifiez la version de Java en procédant comme suit :

   a. Cliquez sur l’élément de menu **Paramètres de l’application**.

   b. Choisissez **Java 8** pour la version de Java.

   c. Choisissez **La plus récente** pour la version mineure de Java.

   d. Choisissez **Tomcat 8.5 la plus récente** pour le conteneur web. (Ce conteneur ne sera en fait pas utilisé. Azure utilisera le conteneur de votre application Spring Boot.)

   e. Cliquez sur **Save**.

   ![Paramètres de l’application][AZ07]

1. Spécifiez vos informations d’identification de déploiement FTP en procédant comme suit :

   a. Cliquez sur l’élément de menu **Informations d’identification de déploiement**.

   b. Spécifiez votre nom d’utilisateur et votre mot de passe.

   c. Cliquez sur **Save**.

   ![Spécifier les informations d’identification de déploiement][AZ08]

1. Récupérez vos informations de connexion FTP à l’aide de la procédure suivante :

   a. Cliquez sur l’élément de menu **Informations d’identification de déploiement**.

   b. Copiez votre nom d’utilisateur FTP complet et l’URL, et enregistrez-les pour la section suivante de ce didacticiel.

   ![URL et informations d’identification FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a>Déployer votre application web Spring Boot sur Azure

La procédure suivante vous guide à travers les étapes pour déployer votre application web Spring Boot sur Azure.

1. Ouvrez un éditeur de texte, comme le Bloc-notes Windows, et collez le texte suivant dans un nouveau document, puis enregistrez le fichier sous *web.config* :
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Après avoir enregistré le fichier *web.config* sur votre système de fichiers, connectez-vous à votre application web via FTP en utilisant l’URL, le nom d’utilisateur et le mot de passe de la section précédente de ce didacticiel. Par exemple :
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Passez du répertoire distant au dossier racine de votre application web, (qui se trouve dans */site/wwwroot*), puis copiez le fichier JAR de votre application Spring Boot et le *web.config* créé précédemment. Par exemple :
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Après avoir déployé vos fichiers JAR et *web.config* sur votre application web, vous devez redémarrer votre application web en utilisant le portail Azure :

   ![][AZ10]

1. Testez l’application web en accédant à l’URL de votre application web avec un navigateur web, ou utilisez la syntaxe de l’exemple suivant si vous disposez de curl :
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Vous devez normalement voir le message suivant : **Greetings from Spring Boot!**

   ![Parcourir l’exemple d’application][SB02]

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Linux dans Azure Container Service](deploy-spring-boot-java-app-on-linux.md)

* [Déployer une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure] et les [outils Java pour Visual Studio Team Services].

Pour plus d’informations sur le déploiement d’applications web sur Azure avec FTP, consultez [Déployer votre application sur Azure App Service avec FTP/S].

Pour plus d’informations sur l’exemple de projet Spring Boot, consultez [Spring Boot Getting Started].

Pour de l’aide sur la mise en route de vos propres applications Spring Boot, consultez **Spring Initializr** à l’adresse https://start.spring.io/.

Pour plus d’informations sur la configuration de paramètres supplémentaires pour votre application web, consultez [Configurer des applications web dans Azure App Service].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[portail Azure]: https://portal.azure.com/
[Configurer des applications web dans Azure App Service]: /azure/app-service/web-sites-configure
[Déployer votre application sur Azure App Service avec FTP/S]: https://docs.microsoft.com/azure/app-service/app-service-deploy-ftp
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[client Git]: https://github.com/
[JDK (Java Developer Kit)]: http://www.oracle.com/technetwork/java/javase/downloads/
[outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/deploy-spring-boot-java-web-app-on-azure/SB01.png
[SB02]: ./media/deploy-spring-boot-java-web-app-on-azure/SB02.png

[AZ01]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ01.png
[AZ02]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ02.png
[AZ03]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ03.png
[AZ04]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ04.png
[AZ05]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ05.png
[AZ06]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ06.png
[AZ07]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ07.png
[AZ08]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ08.png
[AZ09]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ09.png
[AZ10]: ./media/deploy-spring-boot-java-web-app-on-azure/AZ10.png
