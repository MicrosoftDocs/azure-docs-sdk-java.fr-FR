<span data-ttu-id="0f5b1-101">Créez un [fichier d’authentification](../java-sdk-azure-authenticate.md#mgmt-file) et exportez une variable d’environnement `AZURE_AUTH_LOCATION` sur la ligne de commande avec le chemin d’accès complet au fichier.</span><span class="sxs-lookup"><span data-stu-id="0f5b1-101">Create an [authentication file](../java-sdk-azure-authenticate.md#mgmt-file) and export an environment variable `AZURE_AUTH_LOCATION` on the command line with the full path to the file.</span></span>

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azure.auth
```

<span data-ttu-id="0f5b1-102">Le fichier d’authentification est utilisé pour configurer l’objet du point d’entrée `Azure` utilisé par les bibliothèques de gestion pour définir, créer et configurer les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0f5b1-102">The authentication file is used to configure the entry point `Azure` object used by the management libraries to define, create, and configure Azure resources.</span></span>

```java
// pull in the location of the security file from the environment 
final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));

Azure azure = Azure
        .configure()
        .withLogLevel(LogLevel.NONE)
        .authenticate(credFile)
        .withDefaultSubscription();
```

<span data-ttu-id="0f5b1-103">[En savoir plus](../java-sdk-azure-authenticate.md#mgmt-auth) sur les options d’authentification lorsque vous utilisez les bibliothèques de gestion Azure pour Java.</span><span class="sxs-lookup"><span data-stu-id="0f5b1-103">[Learn more](../java-sdk-azure-authenticate.md#mgmt-auth) about authentication options when using the Azure management libraries for Java.</span></span>