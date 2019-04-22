---
title: Kit SDK Azure HDInsight pour Java
description: Informations de référence sur le kit SDK Azure HDInsight pour Java. Le kit SDK HDInsight pour Java fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight.
author: tylerfox
ms.author: tyfox
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: reference
ms.devlang: java
ms.date: 04/15/2019
ms.openlocfilehash: fe87c9214e2a620230cf2f1f52261fd66a2b8857
ms.sourcegitcommit: f33befab25a66a252b4c91c7aeb1b77cb32821bb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59705117"
---
# <a name="hdinsight-sdk-for-java"></a><span data-ttu-id="22b6a-104">Kit SDK HDInsight pour Java</span><span class="sxs-lookup"><span data-stu-id="22b6a-104">HDInsight SDK for Java</span></span>

## <a name="overview"></a><span data-ttu-id="22b6a-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="22b6a-105">Overview</span></span>

<span data-ttu-id="22b6a-106">Le kit SDK HDInsight pour Java fournit des classes et des méthodes qui vous permettent de gérer vos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="22b6a-106">The HDInsight SDK for Java provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="22b6a-107">Il inclut des opérations permettant de créer, supprimer, mettre à jour, répertorier, mettre à l’échelle, exécuter des actions de script, surveiller, obtenir des propriétés des clusters HDInsight, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="22b6a-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22b6a-108">Prérequis</span><span class="sxs-lookup"><span data-stu-id="22b6a-108">Prerequisites</span></span>

* <span data-ttu-id="22b6a-109">Un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="22b6a-109">An Azure account.</span></span> <span data-ttu-id="22b6a-110">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="22b6a-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="22b6a-111">Un kit de développement Java (JDK) pris en charge.</span><span class="sxs-lookup"><span data-stu-id="22b6a-111">A supported Java Development Kit (JDK).</span></span> <span data-ttu-id="22b6a-112">Pour en savoir plus sur les kits de développement disponibles pour le développement sur Azure, consultez <https://aka.ms/azure-jdks>.</span><span class="sxs-lookup"><span data-stu-id="22b6a-112">For more information about the JDKs available for use when developing on Azure, see <https://aka.ms/azure-jdks>.</span></span>
* [<span data-ttu-id="22b6a-113">Maven</span><span class="sxs-lookup"><span data-stu-id="22b6a-113">Maven</span></span>](https://maven.apache.org/download.cgi)

## <a name="sdk-installation"></a><span data-ttu-id="22b6a-114">Installation du Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="22b6a-114">SDK Installation</span></span>

<span data-ttu-id="22b6a-115">Le kit SDK HDInsight pour Java est disponible via Maven [ici](https://search.maven.org/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span><span class="sxs-lookup"><span data-stu-id="22b6a-115">The HDInsight SDK for Java is available through Maven [here](https://search.maven.org/artifact/com.microsoft.azure.hdinsight.v2018_06_01_preview/azure-mgmt-hdinsight).</span></span> <span data-ttu-id="22b6a-116">Ajoutez la dépendance suivante à votre fichier pom.xml :</span><span class="sxs-lookup"><span data-stu-id="22b6a-116">Add the following dependency to your pom.xml:</span></span>

```
<dependency>
    <groupId>com.microsoft.azure.hdinsight.v2018_06_01_preview</groupId>
    <artifactId>azure-mgmt-hdinsight</artifactId>
    <version>1.0.0-beta-1</version>
</dependency>
```

<span data-ttu-id="22b6a-117">Vous devrez aussi ajouter les dépendances suivantes à votre fichier pom.xml :</span><span class="sxs-lookup"><span data-stu-id="22b6a-117">You will also need to add the following dependencies to your pom.xml:</span></span>

* [<span data-ttu-id="22b6a-118">Bibliothèque d’authentification de client Azure :</span><span class="sxs-lookup"><span data-stu-id="22b6a-118">Azure Client Authentication Library:</span></span>](https://search.maven.org/artifact/com.microsoft.azure/azure-client-authentication)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-client-authentication</artifactId>
    <version>1.6.5</version>
  </dependency>
  ```

* [<span data-ttu-id="22b6a-119">CLR de client Java Azure pour ARM :</span><span class="sxs-lookup"><span data-stu-id="22b6a-119">Azure Java Client Runtime For ARM:</span></span>](https://search.maven.org/artifact/com.microsoft.azure/azure-arm-client-runtime)
  ```
  <dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-arm-client-runtime</artifactId>
    <version>1.6.5</version>
  </dependency>
  ```

## <a name="authentication"></a><span data-ttu-id="22b6a-120">Authentication</span><span class="sxs-lookup"><span data-stu-id="22b6a-120">Authentication</span></span>

<span data-ttu-id="22b6a-121">Le kit de développement logiciel (SDK) doit d’abord être authentifié avec votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="22b6a-121">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="22b6a-122">Suivez l’exemple ci-dessous pour créer un principal de service et l’utiliser pour s’authentifier.</span><span class="sxs-lookup"><span data-stu-id="22b6a-122">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="22b6a-123">Une fois cette opération terminée, vous avez une instance de `HDInsightManagementClientImpl`, qui contient de nombreuses méthodes (décrites dans les sections suivantes) pouvant être utilisées pour effectuer des opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="22b6a-123">After this is done, you will have an instance of an `HDInsightManagementClientImpl`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="22b6a-124">Il existe d’autres façons de s’authentifier, en plus de l’exemple suivant, peut-être mieux adaptées à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="22b6a-124">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="22b6a-125">Toutes les méthodes sont décrites ici : [S’authentifier avec les bibliothèques de gestion Azure pour Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span><span class="sxs-lookup"><span data-stu-id="22b6a-125">All methods are outlined here: [Authenticate with the Azure management libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-authenticate?view=azure-java-stable)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="22b6a-126">Exemple d’authentification à l’aide d’un principal de service</span><span class="sxs-lookup"><span data-stu-id="22b6a-126">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="22b6a-127">Tout d’abord, connectez-vous à [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="22b6a-127">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="22b6a-128">Vérifiez que vous utilisez actuellement l’abonnement dans lequel vous souhaitez que le principal de service soit créé.</span><span class="sxs-lookup"><span data-stu-id="22b6a-128">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="22b6a-129">Les informations relatives à votre abonnement sont affichées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="22b6a-129">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="22b6a-130">Si vous n’êtes pas connecté au bon abonnement, sélectionnez le bon en exécutant :</span><span class="sxs-lookup"><span data-stu-id="22b6a-130">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="22b6a-131">Si vous n’avez pas déjà enregistré le fournisseur de ressources HDInsight avec une autre méthode (par exemple, en créant un cluster HDInsight via le portail Azure), vous devez le faire une fois avant de pouvoir vous authentifier.</span><span class="sxs-lookup"><span data-stu-id="22b6a-131">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="22b6a-132">Vous pouvez le faire à partir d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="22b6a-132">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="22b6a-133">Ensuite, choisissez un nom pour votre principal de service et créez-le avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="22b6a-133">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="22b6a-134">Les informations relatives au principal de service sont affichées en tant que JSON.</span><span class="sxs-lookup"><span data-stu-id="22b6a-134">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="22b6a-135">Copiez l’extrait de code ci-dessous et remplissez `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` et `SUBSCRIPTION_ID` avec les chaînes du JSON qui a été retourné après l’exécution de la commande pour créer le principal de service.</span><span class="sxs-lookup"><span data-stu-id="22b6a-135">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

        HDInsightManagementClientImpl client = new HDInsightManagementClientImpl(credentials)
                .withSubscriptionId(SUBSCRIPTION_ID);
```

## <a name="cluster-management"></a><span data-ttu-id="22b6a-136">Gestion du cluster</span><span class="sxs-lookup"><span data-stu-id="22b6a-136">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="22b6a-137">Cette section suppose que vous avez déjà authentifié et construit une instance `HDInsightManagementClientImpl` que vous avez conservée dans une variable appelée `client`.</span><span class="sxs-lookup"><span data-stu-id="22b6a-137">This section assumes you have already authenticated and constructed an `HDInsightManagementClientImpl` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="22b6a-138">Les instructions relatives à l’authentification et à l’obtention d’un `HDInsightManagementClientImpl` se trouvent dans la section Authentification ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="22b6a-138">Instructions for authenticating and obtaining an `HDInsightManagementClientImpl` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="22b6a-139">Créer un cluster</span><span class="sxs-lookup"><span data-stu-id="22b6a-139">Create a Cluster</span></span>

<span data-ttu-id="22b6a-140">Un nouveau cluster peut être créé en appelant `client.clusters().create()`.</span><span class="sxs-lookup"><span data-stu-id="22b6a-140">A new cluster can be created by calling `client.clusters().create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="22b6a-141">Exemples</span><span class="sxs-lookup"><span data-stu-id="22b6a-141">Samples</span></span>

<span data-ttu-id="22b6a-142">Des exemples de code pour créer plusieurs types courants de clusters HDInsight sont disponibles : [HDInsight Java Samples](https://github.com/Azure-Samples/hdinsight-java-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="22b6a-142">Code samples for creating several common types of HDInsight clusters are available: [HDInsight Java Samples](https://github.com/Azure-Samples/hdinsight-java-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="22b6a-143">Exemples</span><span class="sxs-lookup"><span data-stu-id="22b6a-143">Example</span></span>

<span data-ttu-id="22b6a-144">Cet exemple montre comment créer un cluster Spark avec 2 nœuds principaux et un nœud de travail.</span><span class="sxs-lookup"><span data-stu-id="22b6a-144">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="22b6a-145">Vous devez d’abord créer un groupe de ressources et un compte de stockage, comme expliqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="22b6a-145">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="22b6a-146">Si vous les avez déjà créés, vous pouvez ignorer ces étapes.</span><span class="sxs-lookup"><span data-stu-id="22b6a-146">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="22b6a-147">Création d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="22b6a-147">Creating a Resource Group</span></span>

<span data-ttu-id="22b6a-148">Vous pouvez créer un groupe de ressources à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant</span><span class="sxs-lookup"><span data-stu-id="22b6a-148">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="22b6a-149">Création d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="22b6a-149">Creating a Storage Account</span></span>

<span data-ttu-id="22b6a-150">Vous pouvez créer un compte de stockage à l’aide d’[Azure Cloud Shell](https://shell.azure.com/bash) en exécutant :</span><span class="sxs-lookup"><span data-stu-id="22b6a-150">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="22b6a-151">Ensuite, exécutez la commande suivante pour obtenir la clé de votre compte de stockage (vous en aurez besoin pour créer un cluster) :</span><span class="sxs-lookup"><span data-stu-id="22b6a-151">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="22b6a-152">L’extrait de code Java ci-dessous crée un cluster Spark avec 2 nœuds principaux et 1 nœud de travail.</span><span class="sxs-lookup"><span data-stu-id="22b6a-152">The below Java snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="22b6a-153">Remplissez les variables vides comme expliqué dans les commentaires et n’hésitez pas à modifier d’autres paramètres en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="22b6a-153">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="22b6a-154">Obtenir les détails du cluster</span><span class="sxs-lookup"><span data-stu-id="22b6a-154">Get Cluster Details</span></span>

<span data-ttu-id="22b6a-155">Pour obtenir les propriétés d’un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="22b6a-155">To get properties for a given cluster:</span></span>

```java
client.clusters.getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="22b6a-156">Exemples</span><span class="sxs-lookup"><span data-stu-id="22b6a-156">Example</span></span>

<span data-ttu-id="22b6a-157">Vous pouvez utiliser `get` pour confirmer que vous avez créé votre cluster avec succès.</span><span class="sxs-lookup"><span data-stu-id="22b6a-157">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```java
ClusterInner cluster = client.clusters().getByResourceGroup("<Resource Group Name>", "<Cluster Name>");
System.out.println(cluster.name()); //Prints the name of the cluster
System.out.println(cluster.id()); //Prints the resource Id of the cluster
```

<span data-ttu-id="22b6a-158">La sortie doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="22b6a-158">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```

### <a name="list-clusters"></a><span data-ttu-id="22b6a-159">Répertorier les clusters</span><span class="sxs-lookup"><span data-stu-id="22b6a-159">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="22b6a-160">Répertorier les clusters dans l’abonnement</span><span class="sxs-lookup"><span data-stu-id="22b6a-160">List Clusters Under The Subscription</span></span>

```java
client.clusters.list();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="22b6a-161">Répertorier les clusters par groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="22b6a-161">List Clusters By Resource Group</span></span>

```java
client.clusters.listByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="22b6a-162">`List()` et `ListByResourceGroup()` retournent un objet `PagedList<ClusterInner>`.</span><span class="sxs-lookup"><span data-stu-id="22b6a-162">Both `List()` and `ListByResourceGroup()` return a `PagedList<ClusterInner>` object.</span></span> <span data-ttu-id="22b6a-163">Appeler `loadNext()` renvoie une liste de clusters sur cette page et avance l’objet `ClusterPaged` à la page suivante.</span><span class="sxs-lookup"><span data-stu-id="22b6a-163">Calling `loadNext()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="22b6a-164">Cela peut être répété jusqu'à ce que `hasNextPage()` retourne `false`, ce qui indique qu’il n’y a plus d’autres pages.</span><span class="sxs-lookup"><span data-stu-id="22b6a-164">This can be repeated until `hasNextPage()` return `false`, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="22b6a-165">Exemples</span><span class="sxs-lookup"><span data-stu-id="22b6a-165">Example</span></span>

<span data-ttu-id="22b6a-166">L’exemple suivant imprime les propriétés de tous les clusters pour l’abonnement actuel :</span><span class="sxs-lookup"><span data-stu-id="22b6a-166">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="22b6a-167">Supprimer un cluster</span><span class="sxs-lookup"><span data-stu-id="22b6a-167">Delete a Cluster</span></span>

<span data-ttu-id="22b6a-168">Pour supprimer un cluster :</span><span class="sxs-lookup"><span data-stu-id="22b6a-168">To delete a cluster:</span></span>

```java
client.clusters.delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="22b6a-169">Mettre à jour les balises de cluster</span><span class="sxs-lookup"><span data-stu-id="22b6a-169">Update Cluster Tags</span></span>

<span data-ttu-id="22b6a-170">Vous pouvez mettre à jour les balises d’un cluster donné comme suit :</span><span class="sxs-lookup"><span data-stu-id="22b6a-170">You can update the tags of a given cluster like so:</span></span>

```java
client.clusters.update("<Resource Group Name>", "<Cluster Name>", <Map<String,String> of Tags>);
```

### <a name="resize-cluster"></a><span data-ttu-id="22b6a-171">Redimensionner le cluster</span><span class="sxs-lookup"><span data-stu-id="22b6a-171">Resize Cluster</span></span>

<span data-ttu-id="22b6a-172">Vous pouvez mettre à l’échelle un nombre donné de clusters de nœuds Worker en spécifiant une nouvelle taille comme suit :</span><span class="sxs-lookup"><span data-stu-id="22b6a-172">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```java
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="22b6a-173">Cluster Monitoring (Surveillance des clusters)</span><span class="sxs-lookup"><span data-stu-id="22b6a-173">Cluster Monitoring</span></span>

<span data-ttu-id="22b6a-174">Le kit de développement logiciel (SDK) HDInsight Management peut également être utilisé pour gérer la surveillance de vos clusters via Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="22b6a-174">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="22b6a-175">Activer la surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="22b6a-175">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="22b6a-176">Pour activer la supervision OMS, vous devez disposer d’un espace de travail Log Analytics existant.</span><span class="sxs-lookup"><span data-stu-id="22b6a-176">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="22b6a-177">Si vous n’en n’avez pas déjà créé un, vous pouvez apprendre comment le faire ici : [Créer un espace de travail Log Analytics dans le portail Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="22b6a-177">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="22b6a-178">Pour activer la surveillance OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="22b6a-178">To enable OMS Monitoring on your cluster:</span></span>

```java
client.extensions().enableMonitoring("<Resource Group Name", "<Cluster Name>", new ClusterMonitoringRequest().withWorkspaceId("<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="22b6a-179">Afficher l’état de surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="22b6a-179">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="22b6a-180">Pour obtenir l’état d’OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="22b6a-180">To get the status of OMS on your cluster:</span></span>

```java
client.extensions().getMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="22b6a-181">Désactiver la surveillance OMS</span><span class="sxs-lookup"><span data-stu-id="22b6a-181">Disable OMS Monitoring</span></span>

<span data-ttu-id="22b6a-182">Pour désactiver OMS sur votre cluster :</span><span class="sxs-lookup"><span data-stu-id="22b6a-182">To disable OMS on your cluster:</span></span>

```java
client.extensions().disableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="22b6a-183">Actions de script</span><span class="sxs-lookup"><span data-stu-id="22b6a-183">Script Actions</span></span>

<span data-ttu-id="22b6a-184">HDInsight fournit une méthode de configuration intitulée actions de script, qui appelle des scripts personnalisés pour personnaliser le cluster.</span><span class="sxs-lookup"><span data-stu-id="22b6a-184">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="22b6a-185">Vous trouverez plus d’informations sur l’utilisation des actions de script ici : [Personnaliser des clusters HDInsight Linux avec des actions de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="22b6a-185">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="22b6a-186">Exécuter des actions de script</span><span class="sxs-lookup"><span data-stu-id="22b6a-186">Execute Script Actions</span></span>

<span data-ttu-id="22b6a-187">Vous pouvez exécuter des actions de script sur un cluster donné comme suit :</span><span class="sxs-lookup"><span data-stu-id="22b6a-187">You can execute script actions on a given cluster like so:</span></span>

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

### <a name="delete-script-action"></a><span data-ttu-id="22b6a-188">Supprimer une action de script</span><span class="sxs-lookup"><span data-stu-id="22b6a-188">Delete Script Action</span></span>

<span data-ttu-id="22b6a-189">Pour supprimer une action de script persistante spécifiée sur un cluster donné :</span><span class="sxs-lookup"><span data-stu-id="22b6a-189">To delete a specified persisted script action on a given cluster:</span></span>

```java
client.scriptActions().delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="22b6a-190">Répertorier les actions de script persistantes</span><span class="sxs-lookup"><span data-stu-id="22b6a-190">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="22b6a-191">`listByCluster()` retourne un objet `PagedList<RuntimeScriptActionDetailInner>`.</span><span class="sxs-lookup"><span data-stu-id="22b6a-191">Both `listByCluster()` returns a `PagedList<RuntimeScriptActionDetailInner>` object.</span></span> <span data-ttu-id="22b6a-192">Appeler `currentPage().items()` retourne une liste de `RuntimeScriptActionDetailInner`, et `loadNextPage()` avance à la page suivante.</span><span class="sxs-lookup"><span data-stu-id="22b6a-192">Calling `currentPage().items()` returns a list of `RuntimeScriptActionDetailInner`, and `loadNextPage()` advances to the next page.</span></span> <span data-ttu-id="22b6a-193">Cela peut être répété jusqu'à ce que `hasNextPage()` retourne `false`, ce qui indique qu’il n’y a plus d’autres pages.</span><span class="sxs-lookup"><span data-stu-id="22b6a-193">This can be repeated until `hasNextPage()` returns `false`, indicating that there are no more pages.</span></span>

<span data-ttu-id="22b6a-194">Pour répertorier toutes les actions de script persistantes pour le cluster spécifié :</span><span class="sxs-lookup"><span data-stu-id="22b6a-194">To list all persisted script actions for the specified cluster:</span></span>
```java
client.scriptActions().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="22b6a-195">Exemples</span><span class="sxs-lookup"><span data-stu-id="22b6a-195">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="22b6a-196">Répertorier tout l’historique d’exécution des scripts</span><span class="sxs-lookup"><span data-stu-id="22b6a-196">List All Scripts' Execution History</span></span>

<span data-ttu-id="22b6a-197">Pour répertorier tout l’historique d’exécution des scripts pour le cluster spécifié :</span><span class="sxs-lookup"><span data-stu-id="22b6a-197">To list all scripts' execution history for the specified cluster:</span></span>

```java
client.scriptExecutionHistorys().listByCluster("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="22b6a-198">Exemples</span><span class="sxs-lookup"><span data-stu-id="22b6a-198">Example</span></span>

<span data-ttu-id="22b6a-199">Cet exemple imprime tous les détails de toutes les exécutions de script passées.</span><span class="sxs-lookup"><span data-stu-id="22b6a-199">This example prints all the details for all past script executions.</span></span>

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
