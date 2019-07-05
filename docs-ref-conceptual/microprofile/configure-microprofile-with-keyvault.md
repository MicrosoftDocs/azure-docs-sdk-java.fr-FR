---
title: Configurer MicroProfile avec Azure Key Vault
description: Découvrez comment injecter des secrets dans un service web MicroProfile avec Azure Key Vault.
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
ms.openlocfilehash: c405711813176823f2ddee6b4002f75c2b25fdb5
ms.sourcegitcommit: f8faa4a14c714e148c513fd46f119524f3897abf
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533616"
---
# <a name="configure-microprofile-by-using-azure-key-vault"></a>Configurer MicroProfile avec Azure Key Vault

Cet article montre comment configurer une application [MicroProfile](http://microprofile.io) pour récupérer des secrets à partir d’[Azure Key Vault](https://azure.microsoft.com/services/key-vault/). Dans ce processus, vous allez utiliser les [API MicroProfile Config](https://microprofile.io/project/eclipse/microprofile-config) pour créer une connexion directe à Azure Key Vault. En tant que développeur, l’utilisation des API MicroProfile Config vous permet de bénéficier d’une API standard pour récupérer et injecter des données de configuration dans leurs microservices.

Avant de rentrer dans le vif du sujet, jetons un rapide coup d’œil à ce que la combinaison d’Azure Key Vault et de l’API MicroProfile Config nous permet d’écrire dans notre code. L’extrait de code suivant correspond à un champ au sein d’une classe annotée avec `@Inject` et `@ConfigProperty`. Le nom (*name*) spécifié dans l’annotation correspond au nom de la propriété à rechercher dans Azure Key Vault, et *defaultValue* correspond à ce qui sera configuré si la clé n’est pas découverte. De cette façon, la valeur qui est stockée dans le coffre de clés (c’est-à-dire, la valeur par défaut) est automatiquement injectée dans le champ lors de l’exécution. Cette action peut vous simplifier la vie, car vous n’avez plus besoin de passer des valeurs dans les constructeurs et les méthodes setter. C’est MicroProfile qui s’en charge.

```java
@Inject
@ConfigProperty(name = "key-name", defaultValue = "Unknown")
String keyValue;
```

Pour demander des secrets, vous pouvez accéder directement à MicroProfile Config. Par exemple :

```java
public class DemoClass {
    @Inject
    Config config;

    public void method() {
        System.out.println("Hello: " + config.getValue("key-name", String.class));
    }
}
```

Cet exemple de code utilise [Payara Micro](https://www.payara.fish/payara_micro) et [MicroProfile](https://microprofile.io/) pour créer un petit fichier Java au format WAR pouvant être exécuté localement sur votre machine. Il ne montre pas la procédure de dockerisation ni la poussé (push) de code vers Azure. Toutefois, la section située à la fin de cet article fournit des liens vers des tutoriels qui expliquent ces procédures.

Cet exemple utilise une bibliothèque gratuite en open source qui crée une source de configuration (via l’API MicroProfile Config) dans votre coffre de clés. Pour obtenir plus d’informations sur cette bibliothèque et passer en revue le code, consultez la [page GitHub du projet](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault). Si vous utilisez la bibliothèque, le code de ce tutoriel peut se concentrer sur la configuration de la bibliothèque, puis injecter des clés dans votre code. Vous n’avez pas besoin d’écrire du code spécialement pour Azure.

Pour exécuter ce code sur votre ordinateur local, commencez par créer une ressource de coffre de clés, puis suivez les instructions des sections suivantes.

## <a name="create-a-key-vault-resource"></a>Créer une ressource de coffre de clés

Dans cette section, vous allez utiliser Azure CLI pour créer une ressource de coffre de clés et ajouter un secret à celle-ci.

1. Créez un principal de service Azure. Cette étape vous donne l’ID client et la clé dont vous avez besoin pour accéder à votre coffre de clés :

    ```bash
    az login
    az account set --subscription <subscription_id>

    az ad sp create-for-rbac --name <service_principal_name>
    ```

    Nous allons utiliser *microprofile-keyvault-service-principal* pour remplacer *\<nom_principal_service>* dans l’étape précédente. La réponse d’Azure ressemblera à celle-ci :

    ```json
    {
      "appId": "5292398e-XXXX-40ce-XXXX-d49fXXXX9e79",
      "displayName": "microprofile-keyvault-service-principal",
      "name": "http://microprofile-keyvault-service-principal",
      "password": "9b217777-XXXX-4954-XXXX-deafXXXX790a",
      "tenant": "72f988bf-XXXX-41af-XXXX-2d7cd011db47"
    }
    ```

    Notez les valeurs *appId* et *password*. Vous en aurez besoin plus loin dans cet article pour l’*ID client* et la *clé*.

1. (Facultatif) Maintenant que vous avez créé un principal de service, vous pouvez créer un groupe de ressources. Vous pouvez ignorer cette étape si vous disposez déjà d’un groupe de ressources. Pour obtenir la liste des emplacements des groupes de ressources, vous pouvez appeler `az account list-locations` et utiliser la valeur *name* de cette liste pour spécifier l’emplacement de création du groupe de ressources.

    ```bash
    # In this tutorial, "westus" is the resource group location
    # and "jg-test" is the resource group name.
    az group create -l <resource_group_location> -n <resource_group_name>
    ```

1. Créez une ressource de coffre de clés. Vous allez utiliser son nom pour faire référence au coffre de clés, veillez donc à choisir un nom facile à mémoriser.

    ```bash
    az keyvault create --name <your_keyvault_name>            \
                      --resource-group <your_resource_group> \
                      --location <location>                  \
                      --enabled-for-deployment true          \
                      --enabled-for-disk-encryption true     \
                      --enabled-for-template-deployment true \
                      --sku standard
    ```

1. Accordez les autorisations nécessaires au principal de service que vous avez précédemment créé, de sorte qu’il puisse accéder aux secrets du coffre de clés. Dans le code suivant, la valeur appId correspond à la valeur *appId* de l’étape 1, lors de laquelle vous avez créé le principal du service. Autrement dit, même si l’*appId* de l’étape 1 était *5292398e-XXXX-40ce-XXXX-d49fXXXX9e79*, vous devez utiliser la valeur à partir de votre propre sortie de terminal.

    ```bash
    az keyvault set-policy --name <your_keyvault_name>   \
                          --secret-permission get list  \
                          --spn <your_sp_appId_created_in_step1>
    ```

1. Maintenant, vous pouvez pousser (push) un secret vers votre coffre de clés. Utilisez le nom de clé *demo-key*, puis définissez la valeur de la clé sur *demo-value* :

    ```bash
    az keyvault secret set --name demo-key      \
                           --value demo-value   \
                           --vault-name <your_keyvault_name>  
    ```

Et voilà ! Vous disposez à présent d’un coffre de clés fonctionnant dans Azure avec un secret. Vous pouvez cloner ce dépôt et le configurer pour utiliser cette ressource dans votre application.

## <a name="get-up-and-running-locally"></a>Mise en route et exécution locales

Cet exemple se fonde sur un exemple d’application disponible sur GitHub. Vous allez donc cloner cette application puis parcourir le code pas à pas. 

1. Clonez le code sur votre ordinateur en entrant les commandes suivantes :

    `git clone https://github.com/Azure-Samples/microprofile-configsource-keyvault.git`

    `cd microprofile-configsource-keyvault`

1. Accédez à *src/main/resources/META-INF/microprofile-config.properties*, puis changez les propriétés du fichier *microprofile-config.Properties* en utilisant les valeurs des étapes précédentes.

1. Essayez d’exécuter le serveur en utilisant `mvn clean package payara-micro:start`.

1. Essayez d’accéder à [http://localhost:8080/keyvault-configsource/api/config](http://localhost:8080/keyvault-configsource/api/config) dans votre navigateur web. Vous devriez voir une réponse simple montrant les valeurs qui sont lues dans votre coffre de clés.

## <a name="summary"></a>Résumé

Cet exemple d’application combine l’API de MicroProfile Config, Azure Key Vault et la bibliothèque gratuite et open source [microprofile-config-keyvault](https://github.com/Azure/azure-microprofile/tree/master/microprofile-config-keyvault), afin de faciliter l’injection des données de configuration et des secrets dans vos services web MicroProfile.
