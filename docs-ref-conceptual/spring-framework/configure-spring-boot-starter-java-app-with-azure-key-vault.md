---
title: Comment utiliser Spring Boot Starter pour Azure Key Vault
description: Découvrez comment configurer une application d’initialisation Spring Boot avec l’application de démarrage Azure Key Vault.
services: key-vault
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: java
ms.service: key-vault
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: identity
ms.openlocfilehash: 1dda697cac80a6cad3ebbbbf8a5a4f18b515dfd8
ms.sourcegitcommit: 798f4d4199d3be9fc5c9f8bf7a754d7393de31ae
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/08/2018
ms.locfileid: "33883682"
---
# <a name="how-to-use-the-spring-boot-starter-for-azure-key-vault"></a>Comment utiliser Spring Boot Starter pour Azure Key Vault

## <a name="overview"></a>Vue d'ensemble

Cet article vous explique comment créer une application avec l’instance **[Spring Initializr]**, qui utilise la solution Spring Boot Starter pour Azure Key Vault pour récupérer une chaîne de connexion stockée comme secrète dans un coffre de clés.

## <a name="prerequisites"></a>Prérequis


Pour réaliser les étapes décrites dans cet article, vous devez disposer des éléments suivants :

* Un abonnement Azure. Si vous n’avez pas déjà un abonnement Azure, vous pouvez activer vos [avantages d’abonné MSDN] ou vous inscrire pour un [compte Azure gratuit].
* Le [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 ou ultérieure.
* [Apache Maven](http://maven.apache.org/), version 3.0 ou ultérieure.

## <a name="create-an-app-using-the-spring-initialzr"></a>Créer une application à l’aide de Spring Initialzr

1. Accédez à <https://start.spring.io/>.

1. Précisez que vous souhaitez générer un projet **Maven** avec **Java**, entrez les noms de **Groupe** et d’**Artefact** pour votre application, puis cliquez sur le lien pour **basculer vers la version complète** de Spring Initializr.

   ![Spécifiez les noms de groupes et d’artefacts.][secrets-01]

1. Faites défiler jusqu’à la section **Azure**, puis cochez la case **Azure Key Vault**.

   ![Sélectionnez l’application de démarrage Azure Key Vault.][secrets-02]

1. Faites défiler jusqu’au bas de la page, puis cliquez sur le bouton pour **générer le projet**.

   ![Générez le projet Spring Boot.][secrets-03]

1. Lorsque vous y êtes invité, téléchargez le projet dans un emplacement défini par un chemin d’accès sur votre ordinateur local.

## <a name="sign-into-azure-and-select-the-subscription-to-use"></a>Se connecter à Azure et sélectionner l’abonnement à utiliser

1. Ouvrez une invite de commandes.

1. Connectez-vous à votre compte Azure à l’aide de l’interface de ligne de commande Azure :

   ```azurecli
   az login
   ```
   Suivez les instructions pour terminer le processus de connexion.

1. Répertoriez vos abonnements :

   ```azurecli
   az account list
   ```
   Azure renvoie la liste de vos abonnements ; il vous faudra copier l’identificateur unique de l’abonnement que vous souhaitez utiliser, par exemple :

   ```json
   [
     {
       "cloudName": "AzureCloud",
       "id": "ssssssss-ssss-ssss-ssss-ssssssssssss",
       "isDefault": true,
       "name": "Converted Windows Azure MSDN - Visual Studio Ultimate",
       "state": "Enabled",
       "tenantId": "tttttttt-tttt-tttt-tttt-tttttttttttt",
       "user": {
         "name": "contoso@microsoft.com",
         "type": "user"
       }
     }
   ]
   ```

1. Spécifiez le GUID du compte que vous souhaitez utiliser avec Azure, par exemple :

   ```azurecli
   az account set -s ssssssss-ssss-ssss-ssss-ssssssssssss
   ```

## <a name="create-and-configure-a-new-azure-key-vault-using-the-azure-cli"></a>Créez et configurez une nouvelle instance Azure Key Vault à l’aide de l’interface de ligne de commande Azure.

1. Créez un groupe de ressources pour les ressources Azure que vous utiliserez avec votre coffre de clés, par exemple :
   ```azurecli
   az group create --name wingtiptoysresources --location westus
   ```
   Où :
   | Paramètre | Description |
   |---|---|
   | `name` | Spécifie un nom unique pour votre groupe de ressources. |
   | `location` | Spécifie la [Région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre groupe de ressources. |

   L’interface Azure CLI affiche les résultats de la création de votre groupe de ressources ; par exemple :  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/resourceGroups/wingtiptoysresources",
     "location": "westus",
     "managedBy": null,
     "name": "wingtiptoysresources",
     "properties": {
       "provisioningState": "Succeeded"
     },
     "tags": null
   }
   ```

1. Créez un principal de service Azure pour votre inscription d’application, par exemple :
   ```shell
   az ad sp create-for-rbac --name "wingtiptoysuser"
   ```
   Où :
   | Paramètre | Description |
   |---|---|
   | `name` | Spécifie le nom de votre principal de service Azure. |

   L’interface de ligne de commande Azure renvoie un message d’état JSON comportant les éléments *appId* et *password*, que vous utiliserez plus tard en tant que l’ID et le mot de passe client, par exemple :

   ```json
   {
     "appId": "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii",
     "displayName": "wingtiptoysuser",
     "name": "http://wingtiptoysuser",
     "password": "pppppppp-pppp-pppp-pppp-pppppppppppp",
     "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

1. Créez un nouveau coffre de clé dans le groupe de ressources, par exemple :
   ```azurecli
   az keyvault create --name wingtiptoyskeyvault --resource-group wingtiptoysresources --location westus --enabled-for-deployment true --enabled-for-disk-encryption true --enabled-for-template-deployment true --sku standard --query properties.vaultUri
   ```
   Où :
   | Paramètre | Description |
   |---|---|
   | `name` | Spécifie un nom unique à associer au coffre de clés. |
   | `location` | Spécifie la [Région Azure](https://azure.microsoft.com/regions/) dans laquelle sera hébergé votre groupe de ressources. |
   | `enabled-for-deployment` | Spécifie l’[option de déploiement du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `enabled-for-disk-encryption` | Spécifie l’[option de chiffrement du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `enabled-for-template-deployment` | Spécifie l’[option de chiffrement du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `sku` | Spécifie l’[option de référence SKU du coffre de clés](https://docs.microsoft.com/en-us/cli/azure/keyvault). |
   | `query` | Spécifie une valeur à récupérer de la réponse, qui est l’URI du coffre de clés dont vous aurez besoin pour effectuer ce didacticiel. |

   L’interface de ligne de commande Azure affiche l’URI associé au coffre de clés, que vous utiliserez ultérieurement, par exemple :  

   ```
   "https://wingtiptoyskeyvault.vault.azure.net"
   ```

1. Définissez la stratégie d’accès du principal de service Azure créé précédemment, par exemple :
   ```azurecli
   az keyvault set-policy --name wingtiptoyskeyvault --secret-permission set get list delete --spn "iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii"
   ```
   Où :
   | Paramètre | Description |
   |---|---|
   | `name` | Spécifie le nom du coffre de clés créé précédemment. |
   | `secret-permission` | Spécifie les [stratégies de sécurité](https://docs.microsoft.com/en-us/cli/azure/keyvault) de votre coffre de clés. |
   | `spn` | Spécifie l’identificateur unique de votre inscription d’application antérieure. |

   L’interface de ligne de commande Azure affiche les résultats de votre création de stratégie de sécurité, par exemple :  

   ```json
   {
     "id": "/subscriptions/ssssssss-ssss-ssss-ssss-ssssssssssss/...",
     "location": "westus",
     "name": "wingtiptoyskeyvault",
     "properties": {
       ...
       ... (A long list of values will be displayed here.)
       ...
     },
     "resourceGroup": "wingtiptoysresources",
     "tags": {},
     "type": "Microsoft.KeyVault/vaults"
   }
   ```

1. Stockez une instance secrète dans votre nouveau coffre de clés, par exemple :
   ```azurecli
   az keyvault secret set --vault-name "wingtiptoyskeyvault" --name "connectionString" --value "jdbc:sqlserver://SERVER.database.windows.net:1433;database=DATABASE;"
   ```
   Où :
   | Paramètre | Description |
   |---|---|
   | `vault-name` | Spécifie le nom du coffre de clés créé précédemment. |
   | `name` | Spécifie le nom de votre instance secrète. |
   | `value` | Spécifie la valeur de votre instance secrète. |

   L’interface de ligne de commande Azure affiche les résultats de votre création d’instance secrète, par exemple :  

   ```json
   {
     "attributes": {
       "created": "2017-12-01T09:00:16+00:00",
       "enabled": true,
       "expires": null,
       "notBefore": null,
       "recoveryLevel": "Purgeable",
       "updated": "2017-12-01T09:00:16+00:00"
     },
     "contentType": null,
     "id": "https://wingtiptoyskeyvault.vault.azure.net/secrets/connectionString/123456789abcdef123456789abcdef",
     "kid": null,
     "managed": null,
     "tags": {
       "file-encoding": "utf-8"
     },
     "value": "jdbc:sqlserver://wingtiptoys.database.windows.net:1433;database=DATABASE;"
   }
   ```

## <a name="configure-and-compile-your-spring-boot-application"></a>Configurer et compiler votre application Spring Boot

1. Extrayez les fichiers des fichiers d’archive du projet Spring Boot que vous avez téléchargés précédemment dans un répertoire.

1. Accédez au dossier *src/main/resources* de votre projet, puis ouvrez le fichier *application.properties* dans un éditeur de texte.

1. Ajoutez les valeurs associées à votre coffre de clés à l’aide des données de la procédure exécutée plus tôt dans ce didacticiel, par exemple :
   ```yaml
   azure.keyvault.uri=https://wingtiptoyskeyvault.vault.azure.net/
   azure.keyvault.client-id=iiiiiiii-iiii-iiii-iiii-iiiiiiiiiiii
   azure.keyvault.client-key=pppppppp-pppp-pppp-pppp-pppppppppppp
   ```
   Où :
   | Paramètre | Description |
   |---|---|
   | `azure.keyvault.uri` | Spécifie l’URI de l’emplacement de création de votre coffre de clés. |
   | `azure.keyvault.client-id` | Spécifie l’identificateur unique *appId* généré lors de la création de votre principal de service. |
   | `azure.keyvault.client-key` | Spécifie l’identificateur unique *password* généré lors de la création de votre principal de service. |

1. Accédez au fichier source principal de code de votre projet, par exemple : */src/main/java/com/wingtiptoys/secrets*.

1. Ouvrez le fichier Java principal de l’application dans un fichier d’un éditeur de texte, par exemple : *SecretsApplication.java*, puis ajoutez les lignes suivantes au fichier :

   ```java
   package com.wingtiptoys.secrets;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Value;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class SecretsApplication implements CommandLineRunner {

      @Value("${connectionString}")
      private String connectionString;

      public static void main(String[] args) {
         SpringApplication.run(SecretsApplication.class, args);
      }

      public void run(String... varl) throws Exception {
         System.out.println(String.format("\nConnection String stored in Azure Key Vault:\n%s\n",connectionString));
      }
   }
   ```
   Cet exemple de code récupère la chaîne de connexion du coffre de clés et l’affiche dans une ligne de commande.

1. Enregistrez et fermez le fichier Java.

## <a name="build-and-test-your-app"></a>Générer et tester votre application

1. Accédez au répertoire dans lequel est hébergé le fichier *pom.xml* de votre application Spring Boot :

1. Générez votre application Spring Boot avec Maven, par exemple :

   ```bash
   mvn clean package
   ```

   Maven affiche les résultats de la génération.

   ![État de génération de l’application Spring Boot][build-application-01]

1. Exécutez votre application Spring Boot avec Maven ; l’application affiche la chaîne de connexion de votre coffre de clés. Par exemple :

   ```bash
   mvn spring-boot:run
   ```

   ![Message d’exécution Spring Boot][build-application-02]

## <a name="next-steps"></a>Étapes suivantes

Pour en savoir plus sur l’utilisation d’Azure Key Vault, consultez les articles suivants :

* [Documentation Key Vault].

* [Bien démarrer avec Azure Key Vault]

Pour plus d’informations sur l’utilisation d’applications Spring Boot sur Azure, consultez les articles suivants :

* [Déployer une application Spring Boot sur Azure App Service](deploy-spring-boot-java-web-app-on-azure.md)

* [Exécution d’une application Spring Boot sur un cluster Kubernetes dans Azure Container Service](deploy-spring-boot-java-app-on-kubernetes.md)

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez les pages [Azure pour les développeurs Java] et [Outils Java pour Visual Studio Team Services].

<!-- URL List -->

[Documentation Key Vault]: /azure/key-vault/
[Bien démarrer avec Azure Key Vault]: /azure/key-vault/key-vault-get-started
[Azure pour les développeurs Java]: https://docs.microsoft.com/java/azure/
[compte Azure gratuit]: https://azure.microsoft.com/pricing/free-trial/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/
[avantages d’abonné MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[secrets-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-01.png
[secrets-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-02.png
[secrets-03]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/secrets-03.png

[build-application-01]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-01.png
[build-application-02]: media/configure-spring-boot-starter-java-app-with-azure-key-vault/build-application-02.png
