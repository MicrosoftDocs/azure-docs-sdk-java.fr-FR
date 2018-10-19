---
title: Kit de développement logiciel (SDK) Java Azure HDInsight
description: Référence pour le kit de développement logiciel (SDK) Java Azure HDInsight. Le kit de développement logiciel (SDK) Java HDInsight fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 9/20/2018
ms.openlocfilehash: 1271f70fff876f4d24c8afa81123c54735f2d522
ms.sourcegitcommit: 788b49d0b37909c575c9e5176e484cba627e7921
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49120537"
---
# <a name="hdinsight-java-management-sdk-preview"></a>Kit de développement logiciel (SDK) de gestion Java HDInsight (Préversion)

## <a name="overview"></a>Vue d’ensemble

Le kit de développement logiciel (SDK) Java HDInsight fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight. Il inclut des opérations permettant de créer, supprimer, mettre à jour, répertorier, mettre à l’échelle, exécuter des actions de script, surveiller, obtenir des propriétés des clusters HDInsight, et bien plus encore.

## <a name="prerequisites"></a>Prérequis

* Un compte Azure. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/).
* [Java JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven](https://maven.apache.org/install.html)

## <a name="sdk-installation"></a>Installation du Kit de développement logiciel (SDK)

Le Kit de développement logiciel (SDK) Java HDInsight est disponible via Maven [ici](https://mvnrepository.com/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight). Ajoutez la dépendance suivante à votre fichier pom.xml :

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

Vous devrez aussi ajouter les dépendances suivantes à votre fichier pom.xml :

* [Bibliothèque d’authentification de client Azure :](https://mvnrepository.com/artifact/com.microsoft.azure/azure-client-authentication/1.6.2)
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.2</version>
    <scope>test</scope>
</dependency>
```

* [CLR de client Java Azure pour ARM :](https://mvnrepository.com/artifact/com.microsoft.azure/azure-arm-client-runtime/1.6.2)
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.2</version>
</dependency>
```

## <a name="authentication"></a>Authentification

Le kit de développement logiciel (SDK) doit d’abord être authentifié avec votre abonnement Azure.  Suivez l’exemple ci-dessous pour créer un principal de service et l’utiliser pour s’authentifier. Une fois cette opération terminée, vous avez une instance de `HDInsightManagementClientImpl`, qui contient de nombreuses méthodes (décrites dans les sections suivantes) pouvant être utilisées pour effectuer des opérations de gestion.

> [!NOTE]
> Il existe d’autres façons de s’authentifier, en plus de l’exemple suivant, peut-être mieux adaptées à vos besoins. Toutes les méthodes sont décrites ici : [S’authentifier avec les bibliothèques de gestion Azure pour Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)

### <a name="authentication-example-using-a-service-principal"></a>Exemple d’authentification à l’aide d’un principal de service

Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash). Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé. 

```azurecli-interactive
az account show
```

Les informations relatives à votre abonnement sont affichées au format JSON.

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en exécutant : 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Si vous n’avez pas déjà enregistré le fournisseur de ressources HDInsight avec une autre méthode (par exemple, en créant un cluster HDInsight via le portail Azure), vous devez le faire une fois avant de pouvoir vous authentifier. Vous pouvez le faire à partir d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant la commande suivante :
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

Ensuite, choisissez un nom pour votre principal de service et créez-le avec la commande suivante :

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

Les informations relatives au principal de service sont affichées en tant que JSON.

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
Copiez l’extrait de code ci-dessous et remplissez `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` et `SUBSCRIPTION_ID` avec les chaînes du JSON qui a été retourné après l’exécution de la commande pour créer le principal de service.

```java
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.*;
import com.microsoft.azure.management.hdinsight.v2018_06_01_preview.implementation.HDInsightManagementClientImpl;

public class Main {
    public static void main (String[] args) {

        // Tenant ID for your Azure Subscription
        String TENANT_ID = "";
        // Your Service Principal App Client ID
        String CLIENT_ID = "";
        // Your Service Principal Client Secret
        String CLIENT_SECRET = "";
        // Azure Subscription ID
        String SUBSCRIPTION_ID = "";

        ApplicationTokenCredentials credentials = new ApplicationTokenCredentials(
                CLIENT_ID,
                TENANT_ID,
                CLIENT_SECRET,
                AzureEnvironment.AZURE);

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials);
```


## <a name="cluster-management"></a>Gestion du cluster

> [!NOTE]
> Cette section suppose que vous avez déjà authentifié et construit une instance `HDInsightManagementClientImpl` que vous avez conservée dans une variable appelée `client`. Les instructions relatives à l’authentification et à l’obtention d’un `HDInsightManagementClientImpl` se trouvent dans la section Authentification ci-dessus.

### <a name="create-a-cluster"></a>Créer un cluster

Un nouveau cluster peut être créé en appelant `client.clusters().create()`.

#### <a name="example"></a>Exemples

Cet exemple montre comment créer un cluster Spark avec 2 nœuds principaux et un nœud de travail.

> [!NOTE]
> Vous devez d’abord créer un groupe de ressources et un compte de stockage, comme expliqué ci-dessous. Si vous les avez déjà créés, vous pouvez ignorer ces étapes.

##### <a name="creating-a-resource-group"></a>Création d’un groupe de ressources

Vous pouvez créer un groupe de ressources à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Création d’un compte de stockage

Vous pouvez créer un compte de stockage à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant :
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Ensuite, exécutez la commande suivante pour obtenir la clé de votre compte de stockage (vous en aurez besoin pour créer un cluster) :
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
L’extrait de code Java ci-dessous crée un cluster Spark avec 2 nœuds principaux et 1 nœud de travail. Remplissez les variables vides comme expliqué dans les commentaires et n’hésitez pas à modifier d’autres paramètres en fonction de vos besoins.

```java
// The name for the cluster you are creating
String clusterName = "";
// The name of your existing Resource Group
String resourceGroupName = "";
// Choose a username
String username = "";
// Choose a password
String password = "";
// Replace <> with the name of your storage account
String storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
String storageAccountKey = "";
// Choose a region
String location = "";
String container = "default";

HashMap<String, HashMap<String, String>> configurations = new HashMap<String, HashMap<String, String>>();
        HashMap<String, String> gateway = new HashMap<String, String>();
        gateway.put("restAuthCredential.enabled_credential", "True");
        gateway.put("restAuthCredential.username", username);
        gateway.put("restAuthCredential.password", password);
        configurations.put("gateway", gateway);

        ClusterCreateParametersExtended parameters = new ClusterCreateParametersExtended()
            .withLocation(location)
            .withTags(Collections.EMPTY_MAP)
            .withProperties(
                new ClusterCreateProperties()
                    .withClusterVersion("3.6")
                    .withOsType(OSType.LINUX)
                    .withClusterDefinition(new ClusterDefinition()
                            .withKind("spark")
                            .withConfigurations(configurations)
                    )
                    .withTier(Tier.STANDARD)
                    .withComputeProfile(new ComputeProfile()
                        .withRoles(List.of(
                            new Role()
                                .withName("headnode")
                                .withTargetInstanceCount(2)
                                .withHardwareProfile(new HardwareProfile()
                                    .withVmSize("Large")
                                )
                                .withOsProfile(new OsProfile()
                                    .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                    )
                                ),
                            new Role()
                                    .withName("workernode")
                                    .withTargetInstanceCount(1)
                                    .withHardwareProfile(new HardwareProfile()
                                        .withVmSize("Large")
                                    )
                                    .withOsProfile(new OsProfile()
                                        .withLinuxOperatingSystemProfile(new LinuxOperatingSystemProfile()
                                            .withUsername(username)
                                            .withPassword(password)
                                        )
                                    )
                        ))
                    )
                    .withStorageProfile(new StorageProfile()
                        .withStorageaccounts(List.of(
                                new StorageAccount()
                                    .withName(storageAccount)
                                    .withKey(storageAccountKey)
                                    .withContainer(container)
                                    .withIsDefault(true)
                        ))
                    )
            );
        client.clusters().create(resourceGroupName, clusterName, parameters);
```

### <a name="get-cluster-details"></a>Obtenir les détails du cluster

Pour obtenir les propriétés d’un cluster donné :

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemples

Vous pouvez utiliser `get` pour confirmer que vous avez créé votre cluster avec succès.

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

La sortie doit ressembler à :

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a>Répertorier les clusters

#### <a name="list-clusters-under-the-subscription"></a>Répertorier les clusters dans l’abonnement

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a>Répertorier les clusters par groupe de ressources

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> `List()` et `ListByResourceGroup()` retournent un objet `PagedList<ClusterInner>`. Appeler `loadNext()` renvoie une liste de clusters sur cette page et avance l’objet `ClusterPaged` à la page suivante. Cela peut être répété jusqu'à ce que `hasNextPage()` retourne `false`, ce qui indique qu’il n’y a plus d’autres pages.

#### <a name="example"></a>Exemples

L’exemple suivant imprime les propriétés de tous les clusters pour l’abonnement actuel :

```java
PagedList<ClusterInner> clusterPages = client.clusters().list();
while (true) {
    for (ClusterInner cluster : clusterPages.currentPage().items()) {
        System.out.println(cluster.name());
    }
    if (clusterPages.hasNextPage()) {
        clusterPages.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="delete-a-cluster"></a>Supprimer un cluster

Pour supprimer un cluster :

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Mettre à jour les balises de cluster

Vous pouvez mettre à jour les balises d’un cluster donné comme suit :

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a>Redimensionner le cluster

Vous pouvez mettre à l’échelle un nombre donné de clusters de nœuds Worker en spécifiant une nouvelle taille comme suit :

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Cluster Monitoring (Surveillance des clusters)

Le kit de développement logiciel (SDK) HDInsight Management peut également être utilisé pour gérer la surveillance de vos clusters via Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Activer la surveillance OMS

> [!NOTE]
> Pour activer la surveillance OMS, vous devez disposer d’un espace de travail Log Analytics existant. Si vous n’en avez pas déjà créé un, vous pouvez apprendre à le faire ici : [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Pour activer la surveillance OMS sur votre cluster :

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Afficher l’état de surveillance OMS

Pour obtenir l’état d’OMS sur votre cluster :

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Désactiver la surveillance OMS

Pour désactiver OMS sur votre cluster :

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Actions de script

HDInsight fournit une méthode de configuration intitulée actions de script, qui appelle des scripts personnalisés pour personnaliser le cluster.
> [!NOTE]
> Vous pouvez trouver plus d’informations sur l’utilisation des actions de script ici : [Personnaliser des clusters HDInsight Linux à l’aide d’actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)

### <a name="execute-script-actions"></a>Exécuter des actions de script

Vous pouvez exécuter des actions de script sur un cluster donné comme suit :

```java
RuntimeScriptAction scriptAction1 = new RuntimeScriptAction()
    .withName("<Script Name>")
    .withUri("<URL To Script>")
    .withRoles(<List<String> of roles>);
client.clusters().executeScriptActions(
    resourceGroupName, 
    clusterName, 
    new ExecuteScriptActionParameters().withPersistOnSuccess(false).withScriptActions(new LinkedList<>(Arrays.asList(scriptAction1)))); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Supprimer une action de script

Pour supprimer une action de script persistante spécifiée sur un cluster donné :

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Répertorier les actions de script persistantes

> [!NOTE]
> `listByCluster()` retourne un objet `PagedList<RuntimeScriptActionDetailInner>`. Appeler `currentPage().items()` retourne une liste de `RuntimeScriptActionDetailInner`, et `loadNextPage()` avance à la page suivante. Cela peut être répété jusqu'à ce que `hasNextPage()` retourne `false`, ce qui indique qu’il n’y a plus d’autres pages.

Pour répertorier toutes les actions de script persistantes pour le cluster spécifié :
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemples

```java
PagedList<RuntimeScriptActionDetailInner> scriptsPaged = client.scriptActions().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptsPaged.hasNextPage()) {
        scriptsPaged.loadNextPage();
    } else {
        break;
    }
}
```

### <a name="list-all-scripts-execution-history"></a>Répertorier tout l’historique d’exécution des scripts

Pour répertorier tout l’historique d’exécution des scripts pour le cluster spécifié :

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Exemples

Cet exemple imprime tous les détails de toutes les exécutions de script passées.

```java
PagedList<RuntimeScriptActionDetailInner> scriptExecutionsPaged = client.scriptExecutionHistorys().listByCluster(resourceGroupName, clusterName);
while (true) {
    for (RuntimeScriptActionDetailInner script : scriptExecutionsPaged.currentPage().items()) {
        System.out.println(script.name()); //There are methods to get other properties of RuntimeScriptActionDetail besides name(), such as status(), operation(), startTime(), endTime(), etc. See reference documentation.
    }
    if (scriptExecutionsPaged.hasNextPage()) {
        scriptExecutionsPaged.loadNextPage();
    } else {
        break;
    }
}
```
