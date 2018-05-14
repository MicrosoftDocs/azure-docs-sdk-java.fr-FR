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