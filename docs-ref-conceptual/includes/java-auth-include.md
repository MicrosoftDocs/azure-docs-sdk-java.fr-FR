---
ms.openlocfilehash: 0a9b06932baa51c3cf003a4485a3a25261ffe91d
ms.sourcegitcommit: 115f4c8ad07a11f17d79e9d945d63917836b11c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61592501"
---
Créez un [fichier d’authentification](../java-sdk-azure-authenticate.md#mgmt-file) et exportez une variable d’environnement `AZURE_AUTH_LOCATION` sur la ligne de commande avec le chemin d’accès complet au fichier.

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

Le fichier d’authentification est utilisé pour configurer l’objet du point d’entrée `Azure` utilisé par les bibliothèques de gestion pour définir, créer et configurer les ressources Azure.

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

[En savoir plus](../java-sdk-azure-authenticate.md#mgmt-auth) sur les options d’authentification lorsque vous utilisez les bibliothèques de gestion Azure pour Java.