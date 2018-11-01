---
title: JDK Java et prise en charge à long terme pour le développement Azure
description: Téléchargements et instruction de la prise en charge d’Azure pour le développement et l’exécution d’applications Java.
author: rloutlaw
manager: angerobe
ms.devlang: java
ms.topic: article
ms.date: 10/15/2017
ms.author: routlaw
ms.openlocfilehash: 2865219f350990e8b07f7d2cd99f536168a6b8d4
ms.sourcegitcommit: 7df2d442ad7cbdb235e5dd35302a9b73379c23d5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50026995"
---
# <a name="get-java-jdk-downloads-and-support-when-developing-for-azure"></a>Obtenir des téléchargements et le support du JDK Java lors du développement pour Azure

Les développeurs Java disponibles sur Azure et Azure Stack peuvent générer et exécuter des applications de production Java grâce aux [versions OpenJDK d’Azul Systems Zulu Entreprise](https://www.azul.com/downloads/azure-only/zulu/) sans entraîner de frais supplémentaires de support. Vous pouvez utiliser le runtime Java que vous souhaitez sur Azure, mais lorsque vous utilisez Zulu, vous obtenez des mises à jour de maintenance gratuites et vous pouvez créer des questions de prise en charge avec Microsoft avec un [plan de support Azure qualifié](https://azure.microsoft.com/support/plans/).

## <a name="supported-java-versions-and-update-schedule"></a>Versions de Java prises en charge et planification de la mise à jour

Azul Systems fournira des [versions OpenJDK de Zulu Entreprise pour Microsoft Azure](https://www.azul.com/downloads/azure-only/zulu/) entièrement prises en charge, pour tous les supports à long terme (LTS) des versions de Java, en commençant par Java SE 7, 8 et 11. Le [communiqué de presse Azul](https://www.azul.com/press_release/free-java-production-support-for-microsoft-azure-azure-stack) peut vous fournir plus d’informations.


Ces versions de JDK disposeront de mises à jour de sécurité et de corrections de bogues tous les trimestres, ainsi que des mises à jour et correctifs hors bande critiques en fonction des besoins.  Cette prise en charge inclut le rétroportage des mises à jour de sécurité et des correctifs de bogues pour Java 7 et 8 signalés dans les versions plus récentes de Java, comme Java 11, et elle garantit la stabilité continue et la sécurité des versions antérieures de Java.  Les clients Azure peuvent bénéficier de ces mises à jour de sécurité et des plateformes de correction de bogues sans entraîner de frais imprévus d’abonnement Java SE. Les dates de prise en charge pour chaque version de Java SE sont mises en surbrillance dans l’image ci-dessous.

![Chronologie du support technique JDK pour Azure](media/azure-jdk-support.png)

Azul Systems conserve une [feuille de route Java SE](https://www.azul.com/products/azul_support_roadmap/) pour ces versions.

## <a name="use-for-local-development"></a>Utilisation pour le développement local 

Les développeurs peuvent télécharger des JDK Java pour Azure et Azure Stack à partir du [site Web d’Azul Systems](https://www.azul.com/downloads/azure-only/zulu/). Les téléchargements sont disponibles pour Windows, Linux et MacOS. Les développeurs qui travaillent sur Linux peuvent obtenir des packages par l’intermédiaire des gestionnaires de package [yum](https://www.azul.com/downloads/azure-only/zulu/#yum-repo) et [apt](https://www.azul.com/downloads/azure-only/zulu/#apt-repo).

La prise en charge produit du kit JDK Zulu d’Azul pris en charge par Azure est disponible si vous développez pour Azure ou Azure Stack avec un [plan de support Azure éligible](https://azure.microsoft.com/support/plans/).

## <a name="use-in-docker-containers"></a>Utilisation dans les conteneurs Docker

Vous pouvez créer des images Docker illimitées en utilisant les versions OpenJDK de Zulu Entreprise sur la distribution de votre choix. Les images Docker Zulu basées sur l’entreprise Azul Zulu pour les JDK Azure sont disponibles sur le [référentiel de Docker public de Microsoft](https://hub.docker.com/r/microsoft/java-jdk/). Les fichiers Dockerfile permettant de générer ces images sont disponibles sur le [référentiel GitHub Java de Microsoft](https://github.com/Microsoft/java/tree/master/docker).

Pour mettre en conteneur vos applications à l’aide de ces images, vous devez définir une instruction `FROM` dans votre fichier Dockerfile, puis configurer le conteneur avec des dépendances de votre application. Par exemple, pour exécuter une application Java SE empaquetée dans un fichier JAR qui se lie au port 8080 :

```Dockerfile
FROM  microsoft/java-jdk:<tag>
EXPOSE 8080
ADD target/hello.jar hello.jar
ENTRYPOINT ["java", "-jar","/hello.jar"]
```

## <a name="azure-service-runtime-support"></a>Prise en charge du runtime de service Azure

Les services de la plateforme Azure, tels que [App Service](/azure/app-service/containers/), [Functions](/azure/azure-functions/functions-create-first-java-maven), [Service Fabric](/azure/service-fabric/) et [HDInsight](/azure/hdinsight/) utilisent des versions OpenJDK de Zulu Entreprise avec une mise à jour corrective intégrée provenant de versions mineures de Java qui contiennent des correctifs de sécurité et des résolutions de bogues.