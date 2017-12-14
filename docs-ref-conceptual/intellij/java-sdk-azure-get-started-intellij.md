---
title: "Prise en main d’Azure pour Java à l’aide d’Intellij"
description: "Prise en main des fonctions de base des bibliothèques Azure pour Java avec votre propre abonnement Azure."
keywords: "Azure, Java, SDK, API, s’authentifier, prise en main"
author: roygara
ms.author: v-rogara
manager: timlt
ms.date: 10/30/2017
ms.topic: get-started-article
ms.prod: azure
ms.technology: azure
ms.devlang: java
ms.service: multiple
ms.openlocfilehash: 1e10a7c5a46ed0e36143fd4a99decc037c04e1fe
ms.sourcegitcommit: fcf1189ede712ae30f8c7626bde50c9b8bb561bc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/01/2017
---
# <a name="get-started-with-the-azure-libraries-using-intellij"></a>Prise en main des blibliothèques Azure à l’aide d’Intellij

Ce guide vous présente la configuration d’un environnement de développement et l’utilisation des bibliothèques Azure pour Java. Vous créez un principal de service afin de vous authentifier auprès d’Azure et exécutez un exemple de code qui génère et utilise les ressources Azure dans votre abonnement. L’utilisation d’Intellij pour le développement Java avec Azure est facultative. Tout environnement de développement intégré affichant une intégration Maven est adapté. Sinon, vous pouvez exécuter votre code à partir de la ligne de commande à l’aide de Maven, si vous préférez n’utiliser aucun environnement de développement intégré.

## <a name="prerequisites"></a>Composants requis

- Un compte Azure. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/)
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) ou [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).
- La dernière version stable d’[Intellij](https://www.jetbrains.com/idea/)

## <a name="set-up-authentication"></a>Configurer l’authentification

Votre application Java doit lire et créer des autorisations dans votre abonnement Azure pour exécuter l’exemple de code de ce didacticiel. Créez un principal de service et configurez votre application pour qu’elle s’exécute avec ses informations d’identification. Les principaux de service permettent de créer un compte non interactif associé à votre identité, auquel vous accordez seulement les privilèges que votre application doit exécuter.

[Créez un principal de service](/cli/azure/create-an-azure-service-principal-azure-cli) afin d’octroyer votre autorisation de code pour créer et mettre à jour les ressources de votre abonnement sans utiliser directement les informations d’identification de votre compte. Assurez-vous de capturer la sortie. Fournissez un [mot de passe sécurisé](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-policy) dans l’argument de mot de passe, en lieu et place de `MY_SECURE_PASSWORD`. Votre mot de passe doit comporter entre 8 et 16 caractères et répondre à au moins 3 des 4 critères suivants :

* Il comprend des caractères minuscules
* Il comprend des caractères majuscules
* Il comprend des nombres
* Il comprend l’un des symboles suivants : @ # $ % ^ & * - _ ! + = [ ] { } | \ : ‘ , . ? / ` ~ “ ( ) ;


```azurecli-interactive
az ad sp create-for-rbac --name AzureJavaTest --password "MY_SECURE_PASSWORD"
```

Qui vous fournit une réponse au format suivant :

```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "AzureJavaTest",
  "name": "http://AzureJavaTest",
  "password": password,
  "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
}
```

Ensuite, copiez les éléments suivants dans un fichier texte sur votre système :

```text
# sample management library properties file
subscription=ssssssss-ssss-ssss-ssss-ssssssssssss
client=cccccccc-cccc-cccc-cccc-cccccccccccc
key=kkkkkkkkkkkkkkkk
tenant=tttttttt-tttt-tttt-tttt-tttttttttttt
managementURI=https\://management.core.windows.net/
baseURL=https\://management.azure.com/
authURL=https\://login.windows.net/
graphURL=https\://graph.windows.net/
```

Remplacez les quatre valeurs du haut par les éléments suivants :

- abonnement : utilisez la valeur *id* de `az account show` dans Azure CLI 2.0.
- client : utilisez la valeur *appId* de la sortie d’un principal de service.
- clé : utilisez la valeur *password* de la sortie du principal de service.
- abonné : utilisez la valeur *tenant* de la sortie du principal de service.

Enregistrez ce fichier dans un emplacement sécurisé sur votre système que votre code peut lire. Dans la mesure où vous pouvez utiliser ce fichier pour un code ultérieur, il est recommandé de le stocker à l’extérieur de l’application dans cet article. 

Définissez une variable d’environnement `AZURE_AUTH_LOCATION` avec le chemin complet du fichier d’authentification dans l’interpréteur de commande.  

```bash
export AZURE_AUTH_LOCATION=/Users/raisa/azureauth.properties
```

Si vous travaillez dans un environnement Windows, ajoutez la variable à vos propriétés système. Ouvrez PowerShell, et après avoir remplacé la seconde variable par le chemin d’accès à votre fichier, entrez la commande suivante :

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\<fullpath>\azureauth.properties", "Machine")
```

## <a name="create-a-new-maven-project"></a>Création d’un projet Maven

> [!NOTE]
> Ce guide utilise un outil de build Maven pour générer et exécuter l’exemple de code, mais d’autres outils de build tels que Gradle fonctionnent aussi avec les bibliothèques Azure pour Java. 

Ouvrez Intellij, sélectionnez File > New > Project... (Fichier > Nouveau > Projet...). Passez ensuite à l’écran suivant.

Saisissez « com.fabrikam » pour groupID et saisissez un artefact de votre choix.

Accédez à l’écran final, et terminez la création du projet.

Ouvrez maintenant le fichier pom.xml. Ajoutez le code suivant :

```XML
<dependencies>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure</artifactId>
    <version>1.3.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-storage</artifactId>
    <version>5.0.0</version>
</dependency>
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>6.2.1.jre8</version>
</dependency>
</dependencies>
```

Enregistrez le fichier pom.xml.
   
## <a name="install-the-azure-toolkit-for-intellij"></a>Installez le Kit de ressources Azure pour Intellij

Le [kit de ressources Azure](azure-toolkit-for-intellij-installation.md) est nécessaire si vous avez l’intention de déployer des applications web ou des API par programmation, cependant il n’est actuellement utilisé pour aucune autre opération de développement. Les instructions suivantes sont un résumé du processus d’installation. Pour une procédure détaillée, consultez la section [Installation du kit de ressources Azure pour Intellij](azure-toolkit-for-intellij-installation.md).

Sélectionnez le menu **File** (Fichier), puis sélectionnez **Settings...** (Paramètres...). 

Sélectionnez **Browse repositories...** (Accédez aux référentiels...), cherchez « Azure », puis installez le **Azure toolkit for Intellij** (Kit de ressources Azure pour Intellij).

Redémarrez Intellij.

## <a name="create-a-linux-virtual-machine"></a>Créer une machine virtuelle Linux

Créez un fichier nommé `AzureApp.java` dans le répertoire `src/main/java` du projet et collez-y le bloc de code suivant. Mettez à jour les variables `userName` et `sshKey` avec des valeurs réelles pour votre machine. Le code crée une nouvelle machine virtuelle Linux avec le nom `testLinuxVM` dans un groupe de ressources `sampleResourceGroup` qui s’exécute dans la région Azure Est des États-Unis.

Pour créer un élément `sshkey`, ouvrez l’interpréteur de commande Azure, puis entrez `ssh-keygen -t rsa -b 2048`. Nommez le fichier, puis accédez au fichier .public pour obtenir la clé, que vous utilisez dans le code suivant ; copiez et collez le tout dans votre variable `sshKey`.

```java

import com.microsoft.azure.management.Azure;
import com.microsoft.azure.management.compute.VirtualMachine;
import com.microsoft.azure.management.compute.KnownLinuxVirtualMachineImage;
import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
import com.microsoft.azure.management.appservice.PricingTier;
import com.microsoft.azure.management.appservice.WebApp;
import com.microsoft.azure.management.storage.StorageAccount;
import com.microsoft.azure.management.storage.SkuName;
import com.microsoft.azure.management.storage.StorageAccountKey;
import com.microsoft.azure.management.sql.SqlDatabase;
import com.microsoft.azure.management.sql.SqlServer;
import com.microsoft.azure.management.resources.fluentcore.arm.Region;
import com.microsoft.azure.management.resources.fluentcore.utils.SdkContext;

import com.microsoft.rest.LogLevel;

import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

import java.io.File;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.List;

public class AzureApp {

    public static void main(String[] args) {

        final String userName = "YOUR_VM_USERNAME";
        final String sshKey = "YOUR_PUBLIC_SSH_KEY";

        try {

            // use the properties file with the service principal information to authenticate
            // change the name of the environment variable if you used a different name in the previous step
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));    
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();
           
            // create a Ubuntu virtual machine in a new resource group 
            VirtualMachine linuxVM = azure.virtualMachines().define("testLinuxVM")
                    .withRegion(Region.US_EAST)
                    .withNewResourceGroup("sampleVmResourceGroup")
                    .withNewPrimaryNetwork("10.0.0.0/24")
                    .withPrimaryPrivateIPAddressDynamic()
                    .withoutPrimaryPublicIPAddress()
                    .withPopularLinuxImage(KnownLinuxVirtualMachineImage.UBUNTU_SERVER_16_04_LTS)
                    .withRootUsername(userName)
                    .withSsh(sshKey)
                    .withUnmanagedDisks()
                    .withSize(VirtualMachineSizeTypes.STANDARD_D3_V2)
                    .create();   

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
}
```


Des requêtes et des réponses REST apparaissent dans la console pendant que le kit de développement logiciel (SDK) effectue les appels sous-jacents à l’API REST d’Azure pour configurer la machine virtuelle et ses ressources. Lorsque le programme se termine, vérifiez la machine virtuelle de votre abonnement avec Azure CLI 2.0 :

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

Après avoir vérifié que le code a fonctionné, utilisez l’interface CLI pour supprimer la machine virtuelle et ses ressources.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Déployer une application web à partir d’un référentiel GitHub

Remplacez la méthode principale dans `AzureApp.java` par la méthode ci-dessous pour mettre à jour la variable `appName` vers une valeur unique avant d’exécuter le code. Ce code déploie une application web à partir de la branche `master` d’un référentiel GitHub public vers une nouvelle [application web Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) s’exécutant au niveau tarifaire gratuit.

```java
    public static void main(String[] args) {
        try {

            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            final String appName = "YOUR_APP_NAME";

            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            WebApp app = azure.webApps().define(appName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleWebResourceGroup")
                    .withNewWindowsPlan(PricingTier.FREE_F1)
                    .defineSourceControl()
                    .withPublicGitRepository(
                            "https://github.com/Azure-Samples/app-service-web-java-get-started")
                    .withBranch("master")
                    .attach()
                    .create();

        } catch (Exception e) {
            System.out.println(e.getMessage());
            e.printStackTrace();
        }
    }
```

Exécutez le code comme précédemment avec Maven :

Ouvrez un navigateur menant à l’application à l’aide de l’interface CLI :

```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```
Supprimez l’application web et le plan de votre abonnement après vérification du déploiement.

```azurecli-interactive
az group delete --name sampleWebResourceGroup
```

## <a name="connect-to-an-azure-sql-database"></a>Se connecter à une instance Azure SQL Database

Remplacez la méthode principale actuelle dans `AzureApp.java` par le code ci-dessous, et définissez une valeur réelle pour la variable `dbPassword`.
Ce code crée une nouvelle base de données SQL avec une règle de pare-feu autorisant l’accès à distance, puis se connecte à l’aide du pilote JBDC de SQL Database. 

```java

    public static void main(String args[])
    {
        // create the db using the management libraries
        try {
            final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
            Azure azure = Azure.configure()
                    .withLogLevel(LogLevel.BASIC)
                    .authenticate(credFile)
                    .withDefaultSubscription();

            final String adminUser = SdkContext.randomResourceName("db",8);
            final String sqlServerName = SdkContext.randomResourceName("sql",10);
            final String sqlDbName = SdkContext.randomResourceName("dbname",8);
            final String dbPassword = "YOUR_PASSWORD_HERE";


            SqlServer sampleSQLServer = azure.sqlServers().define(sqlServerName)
                            .withRegion(Region.US_EAST)
                            .withNewResourceGroup("sampleSqlResourceGroup")
                            .withAdministratorLogin(adminUser)
                            .withAdministratorPassword(dbPassword)
                            .withNewFirewallRule("0.0.0.0","255.255.255.255")
                            .create();

            SqlDatabase sampleSQLDb = sampleSQLServer.databases().define(sqlDbName).create();

            // assemble the connection string to the database
            final String domain = sampleSQLServer.fullyQualifiedDomainName();
            String url = "jdbc:sqlserver://"+ domain + ":1433;" +
                    "database=" + sqlDbName +";" +
                    "user=" + adminUser+ "@" + sqlServerName + ";" +
                    "password=" + dbPassword + ";" +
                    "encrypt=true;trustServerCertificate=false;hostNameInCertificate=*.database.windows.net;loginTimeout=30;";

            // connect to the database, create a table and insert a entry into it
            Connection conn = DriverManager.getConnection(url);

            String createTable = "CREATE TABLE CLOUD ( name varchar(255), code int);";
            String insertValues = "INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);";
            String selectValues = "SELECT * FROM CLOUD";
            Statement createStatement = conn.createStatement();
            createStatement.execute(createTable);
            Statement insertStatement = conn.createStatement();
            insertStatement.execute(insertValues);
            Statement selectStatement = conn.createStatement();
            ResultSet rst = selectStatement.executeQuery(selectValues);

            while (rst.next()) {
                System.out.println(rst.getString(1) + " "
                        + rst.getString(2));
            }


        } catch (Exception e) {
            System.out.println(e.getMessage());
            System.out.println(e.getStackTrace().toString());
        }
    }
```
Exécutez l’exemple depuis la ligne de commande :

```
mvn clean compile exec:java
```

Effacez ensuite les ressources à l’aide de l’interface CLI :

```azurecli-interactive
az group delete --name sampleSqlResourceGroup
```

## <a name="write-a-blob-into-a-new-storage-account"></a>Écrire un objet blob dans un nouveau compte de stockage

Remplacez la méthode principale actuelle dans `AzureApp.java` par le code ci-dessous. Ce code crée un [compte de stockage Azure](https://docs.microsoft.com/azure/storage/storage-introduction), avant d’utiliser les bibliothèques de stockage Azure pour Java pour créer un fichier texte dans le cloud.

```java
public static void main(String[] args) {

    try {

        // use the properties file with the service principal information to authenticate
        // change the name of the environment variable if you used a different name in the previous step
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
                .withLogLevel(LogLevel.BASIC)
                .authenticate(credFile)
                .withDefaultSubscription();

        // create a new storage account
        String storageAccountName = SdkContext.randomResourceName("st",8);
        StorageAccount storage = azure.storageAccounts().define(storageAccountName)
                    .withRegion(Region.US_WEST2)
                    .withNewResourceGroup("sampleStorageResourceGroup")
                    .create();

        // create a storage container to hold the file
        List<StorageAccountKey> keys = storage.getKeys();
        final String storageConnection = "DefaultEndpointsProtocol=https;"
                + "AccountName=" + storage.name()
                + ";AccountKey=" + keys.get(0).value()
                + ";EndpointSuffix=core.windows.net";

        CloudStorageAccount account = CloudStorageAccount.parse(storageConnection);
        CloudBlobClient serviceClient = account.createCloudBlobClient();

        // Container name must be lower case.
        CloudBlobContainer container = serviceClient.getContainerReference("helloazure");
        container.createIfNotExists();

        // Make the container public
        BlobContainerPermissions containerPermissions = new BlobContainerPermissions();
        containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
        container.uploadPermissions(containerPermissions);

        // write a blob to the container
        CloudBlockBlob blob = container.getBlockBlobReference("helloazure.txt");
        blob.uploadText("hello Azure");

    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }
    }
}
```

Exécutez l’exemple depuis la ligne de commande :

Vous pouvez rechercher le fichier `helloazure.txt` dans votre compte de stockage via le portail Azure ou avec l’[Explorateur de stockage Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-explorer-blobs).

Effacez le compte de stockage à l’aide de l’interface CLI :

```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>Explorez d’autres exemples

Pour savoir comment utiliser les bibliothèques de gestion Azure pour Java afin de gérer les ressources et d’automatiser des tâches, consultez notre exemple de code pour les [machines virtuelles](../java-sdk-azure-virtual-machine-samples.md), [les applications web](../java-sdk-azure-web-apps-samples.md) et [SQL Database](../java-sdk-azure-sql-database-samples.md).

## <a name="reference-and-release-notes"></a>Références et notes de version

Il existe une [référence](http://docs.microsoft.com/java/api) pour tous les packages.

## <a name="get-help-and-give-feedback"></a>Obtenir de l’aide et donner son avis

Posez des questions à la communauté sur [Stack Overflow](http://stackoverflow.com/questions/tagged/azure+java). Signalez des bogues et des problèmes concernant les bibliothèques Azure pour Java sur le [projet GitHub](https://github.com/Azure/azure-sdk-for-java).
