---
title: Configurer MicroProfile avec Azure Key Vault
description: Découvrez comment injecter des clés secrètes dans un service web de MicroProfile avec Azure Key Vault
services: key-vault
documentationcenter: java
author: jonathangiles
manager: routlaw
editor: jonathangiles
ms.assetid: ''
ms.author: jogiles
ms.date: 09/07/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: web
ms.openlocfilehash: fa93788f9b600d963f35ea599a58d309d3a3ee52
ms.sourcegitcommit: 77dc6c03a2e6264df688d91a04fc6b40950779ef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43240822"
---
# <a name="configure-microprofile-with-azure-key-vault"></a>Configurer MicroProfile avec Azure Key Vault

Ce tutoriel vous présentera comment configurer une application [MicroProfile](http://microprofile.io) pour extraire des clés secrètes à partir d’[Azure Key Vault](https://azure.microsoft.com/services/key-vault/) à l’aide des [API MicroProfile Config](https://microprofile.io/project/eclipse/microprofile-config) pour créer une connexion directe vers Azure Key Vault. Avec les API MicroProfile Config, les développeurs bénéficient d’une API standard pour extraire et injecter des données de configuration dans leurs microservices.

Avant de rentrer dans le vif du sujet, jetons un rapide coup d’œil à ce que la combinaison d’Azure Key Vault et de l’API MicroProfile Config nous permet d’écrire dans notre code. Voici un extrait de code d’un champ au sein d’une classe annotée avec `@Inject` et `@ConfigProperty`. Le `name` spécifié dans l’annotation correspond au nom de la propriété à rechercher dans Azure Key Vault, et le `defaultValue` correspond à ce qui sera configuré si la clé n’est pas découverte. À la fin de l’opération, la valeur stockée dans Azure Key Vault, ou la valeur par défaut, est automatiquement injectée dans le champ lors de l’exécution, ce qui simplifie la tâche des développeurs, leur évitant ainsi le transfert de valeurs pour les méthodes constructors et setter, désormais prise en charge par MicroProfile.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Il est également possible d’accéder directement à MicroProfile Config, afin d’effectuer des requêtes de clés secrètes si nécessaire, par exemple :

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

Cet exemple utilise [Payara Micro](https://www.payara.fish/payara_micro) et [MicroProfile](https://microprofile.io/) pour créer un petit fichier Java au format war pouvant être exécuté localement sur votre machine. Il n’illustre pas la procédure d’ancrage ni l’envoi de code vers Azure. Vous trouverez en fin de tutoriel une section de liens renvoyant vers d’autres tutoriels vous expliquant ces opérations.

Cet exemple utilise une bibliothèque gratuite en open source créant une source de configuration (via l’API MicroProfile Config) pour Azure Key Vault. Pour en apprendre davantage sur cette bibliothèque et passer en revue le code, consultez la [page du projet GitHub](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Grâce à cette bibliothèque, vous pouvez utiliser le code de ce tutoriel pour configurer la bibliothèque et injecter des clés à votre code, sans qu’il n’y ait besoin de rédiger un code spécifique à Azure.

Voici les étapes nécessaires à l’exécution de ce code sur votre ordinateur local, la première consistant à créer une ressource pour Azure Key Vault.

## <a name="creating-an-azure-key-vault-resource"></a>Création d’une ressource Azure Key Vault

Nous utiliserons l’interface Azure CLI pour créer la ressource Azure Key Vault et remplir cette dernière avec une clé secrète.

1. Tout d’abord, il nous faut créer un principal de service Azure. Celui-ci nous fournira l’ID client ainsi que sa clé qui permettront d’accéder à Key Vault :

```bash
az login
az account set --subscription <subscription_id>

az ad sp create-for-rbac --name <service_principal_name>
```

Commençons par utiliser `microprofile-keyvault-service-principal` comme nom du principal de service de l’étape précédente. La réponse d’Azure à cette action s’affichera sous la forme suivante (affichage partiel) :

```json
{
  "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
  "displayName": "microprofile-keyvault-service-principal",
  "name": "http://microprofile-keyvault-service-principal",
  "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
  "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
}
```

Remarquez particulièrement les valeurs `appID` et `password`. Nous les utiliserons plus tard, respectivement comme `client ID` et `key`.

À présent que nous avons créé un principal de service, nous pouvons éventuellement créer un groupe de ressources (si vous disposez déjà d’un groupe que vous souhaitez utiliser, vous pouvez passer cette étape). Notez que vous pouvez obtenir une liste des emplacements des groupes de ressources à l’aide de la requête `az account list-locations` et utiliser la valeur `name` de cette liste pour spécifier l’emplacement de création du groupe de ressources.

```bash
# For this tutorial, the author chose to use `westus`
# and `jg-test` for the resource group name.
az group create -l <resource_group_location> -n <resource_group_name>
```

Nous allons désormais créer une ressource Azure Key Vault. Notez que le nom du Key Vault nous servira plus tard pour nous référer au coffre de clés, nous vous conseillons donc de choisir un nom facile à retenir.

```bash
az keyvault create --name <your_keyvault_name>            \
                   --resource-group <your_resource_group> \
                   --location <location>                  \
                   --enabled-for-deployment true          \
                   --enabled-for-disk-encryption true     \
                   --enabled-for-template-deployment true \
                   --sku standard
```

Nous avons également besoin d’accorder les autorisations appropriées au principal de service que nous avons précédemment créé, de sorte qu’il puisse accéder aux clés secrètes Key Vault. Notez que la valeur de l’ID de l’application correspond à la valeur `appId` attribuée en amont de la création du principal de service (à savoir `5292398e-XXXX-40ce-XXXX-d49fXXXX9e79`, mais utilisez la valeur indiquée en sortie sur votre terminal).

```bash
az keyvault set-policy --name <your_keyvault_name>   \
                       --secret-permission get list  \
                       --spn <your_sp_appId_created_in_step1>
```

C’est le moment pour nous d’envoyer une clé secrète dans Key Vault. Utilisons le nom de clé `demo-key`, puis définissons la valeur de la clé sur `demo-value` :

```bash
az keyvault secret set --name demo-key      \
                       --value demo-value   \
                       --vault-name <your_keyvault_name>  
```

Et voilà ! Nous disposons à présent d’un Key Vault fonctionnant sur Azure avec une clé secrète. Nous pouvons à présent cloner ce référentiel et le configurer pour utiliser cette ressource dans notre application.

## <a name="getting-up-and-running-locally"></a>Mise en route et exécution en local

Cet exemple se fonde sur un exemple d’application disponible sur GitHub, nous pouvons donc le cloner et parcourir le code pas à pas. Suivez les étapes ci-dessous pour cloner le code sur votre ordinateur :

1. `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

1. `cd microprofile-configsource-keyvault`

1. Accédez à `src/main/resources/META-INF/microprofile-config.properties` et modifiez les propriétés dans le fichier microprofile-config.properties avec les détails renseignés plus haut.

1. Essayez de faire fonctionner le serveur en utilisant `mvn clean package payara-micro:start`

1. Essayez d’accéder à [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) dans votre navigateur web. Vous devriez voir une réponse simple illustrant les valeurs lues depuis Azure Key Vault.

## <a name="summary"></a>Résumé

Cet exemple d’application mêle l’API de MicroProfile Config, d’Azure Key Vault et de la bibliothèque gratuite et open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault), afin de faciliter l’injection de données de configuration et de clés secrètes dans nos services web MicroProfile.
