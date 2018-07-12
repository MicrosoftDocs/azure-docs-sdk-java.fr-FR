---
title: Ajout d’un certificat racine pour Azure au magasin d’autorité de certification Java
description: Découvrez comment ajouter un certificat racine de certificat d'autorité (CA) au magasin de certificats (cacerts) de l'autorité de certification Java pour l’utilisation de Microsoft Azure.
services: ''
documentationcenter: java
author: rmcmurray
manager: mbaldwin
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 07/02/2018
ms.author: robmcm
ms.openlocfilehash: 3f2de63f7eb1422ff1dd6db45d68e02f4af188b8
ms.sourcegitcommit: 0ed7c5af0152125322ff1d265c179f35028f3c15
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37864039"
---
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a><span data-ttu-id="044c4-103">Ajout d’un certificat racine au magasin de certificats d’autorité de certification Java</span><span class="sxs-lookup"><span data-stu-id="044c4-103">Adding a root certificate to the Java CA certificates store</span></span>

<span data-ttu-id="044c4-104">Les applications qui utilisent des services Azure (tels qu'Azure Service Bus) doivent approuver le certificat racine Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="044c4-104">Applications that use Azure services (such as Azure Service Bus) need to trust the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="044c4-105">Il est possible que le certificat soit déjà installé sur votre système, mais dans le cas contraire, les étapes décrites dans ce didacticiel vous montreront comment utiliser le **keytool** d’Oracle pour ajouter le certificat racine de certificat d’autorité de certification (CA) au magasin de certificats (cacerts) de l'autorité de certification Java que vous utiliserez pour les services Azure.</span><span class="sxs-lookup"><span data-stu-id="044c4-105">This certificate may already be installed on your system, but if it is not, the steps in this tutorial will show you how to use Oracle's **keytool** to add the required certificate authority (CA) root certificate to the Java CA certificate (cacerts) store that you will use for Azure services.</span></span>

<span data-ttu-id="044c4-106">L’utilitaire keytool d’Oracle est un _Outil de gestion de clés et de certificats_ qui permet aux développeurs de gérer la liste des certificats approuvés pour une utilisation avec Java.</span><span class="sxs-lookup"><span data-stu-id="044c4-106">Oracle's keytool utility is a _Key and Certificate Management Tool_, which allows developers to manage the list of trusted certificates for use with Java.</span></span> <span data-ttu-id="044c4-107">Vous pouvez utiliser keytool pour ajouter le certificat d’autorité de certification avant de compresser le JDK et de l’ajouter au dossier **approot** de votre projet Azure. Vous pouvez également utiliser une tâche de démarrage Azure qui utilise keytool pour ajouter le certificat.</span><span class="sxs-lookup"><span data-stu-id="044c4-107">You can use keytool to add the CA certificate before zipping your JDK and adding it to your Azure project's **approot** folder, or you could run an Azure start-up task that uses keytool to add the certificate.</span></span>

<span data-ttu-id="044c4-108">Dès le 15 avril 2013, Azure a commencé à migrer du certificat racine GTE CyberTrust Global au certificat racine Baltimore CyberTrust.</span><span class="sxs-lookup"><span data-stu-id="044c4-108">Beginning April 15, 2013, Azure began migrating from the GTE CyberTrust Global root certificate to the Baltimore CyberTrust root certificate.</span></span> <span data-ttu-id="044c4-109">Les étapes suivantes vous montrent comment utiliser keytool pour ajouter le certificat racine Baltimore CyberTrust dans votre magasin de certificats (cacerts) de l’autorité de certification Java.</span><span class="sxs-lookup"><span data-stu-id="044c4-109">The following steps show you how to use keytool to add the Baltimore CyberTrust root certificate to your Java CA certificate (cacerts) store.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="044c4-110">Vous pouvez suivre les étapes décrites dans cet article pour configurer votre Kit de développement logiciel Java pour approuver les certificats racine à partir d’autres autorités de certification approuvées.</span><span class="sxs-lookup"><span data-stu-id="044c4-110">You can use the steps in this article to configure your Java SDK to trust the root certificates from other trusted certificate authorities.</span></span> <span data-ttu-id="044c4-111">Par exemple, vous souhaitez peut-être obtenir un certificat racine dans la liste de certificats répertoriée dans la page [Certificats racines GeoTrust](http://www.geotrust.com/resources/root-certificates/).</span><span class="sxs-lookup"><span data-stu-id="044c4-111">For example, you might choose a root certificate from the list of certificates at [GeoTrust Root Certificates](http://www.geotrust.com/resources/root-certificates/).</span></span>
> 

## <a name="determining-which-root-certificates-are-installed"></a><span data-ttu-id="044c4-112">Déterminer les certificats racine installés</span><span class="sxs-lookup"><span data-stu-id="044c4-112">Determining which root certificates are installed</span></span>

<span data-ttu-id="044c4-113">Il est possible que le certificat Baltimore soit déjà installé dans votre magasin cacerts ; suivez la procédure suivante pour le déterminer.</span><span class="sxs-lookup"><span data-stu-id="044c4-113">The Baltimore certificate might already be installed in your cacerts store, so you need to use the following steps to determine if it has already been installed.</span></span>

1. <span data-ttu-id="044c4-114">Sur une invite de commandes administrateur, accédez à votre dossier JDK **jdk\jre\lib\security**, puis exécutez la commande suivante pour répertorier les certificats qui sont installés sur votre système :</span><span class="sxs-lookup"><span data-stu-id="044c4-114">At an administrator command prompt, navigate to your JDK's **jdk\jre\lib\security** folder, and then run the following command to list the certificates that are installed on your system:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

1. <span data-ttu-id="044c4-115">Si le mot de passe du magasin est demandé, le mot de passe par défaut est **changeit**.</span><span class="sxs-lookup"><span data-stu-id="044c4-115">If you are prompted for the store password, the default password is **changeit**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="044c4-116">Si vous souhaitez modifier le mot de passe, consultez la documentation de keytool à l’adresse <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="044c4-116">If you want to change the store password, see the keytool documentation at <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>
   > 

1. <span data-ttu-id="044c4-117">Si vous ne voyez pas le certificat avec l’empreinte de `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, suivez les étapes décrites dans la section suivante pour télécharger et installer le certificat.</span><span class="sxs-lookup"><span data-stu-id="044c4-117">If you do not see the certificate with the thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, use the steps in the following section to download and install the certificate.</span></span>

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a><span data-ttu-id="044c4-118">Ajout d'un certificat racine au magasin cacerts</span><span class="sxs-lookup"><span data-stu-id="044c4-118">To add a root certificate to the cacerts store</span></span>

1. <span data-ttu-id="044c4-119">Téléchargez le certificat racine Baltimore CyberTrust à partir de <https://cacert.omniroot.com/bc2025.crt> et enregistrez-le dans un fichier local avec l’extension **.cer** dans votre dossier **jdk\jre\lib\security**.</span><span class="sxs-lookup"><span data-stu-id="044c4-119">Download the Baltimore CyberTrust root certificate from <https://cacert.omniroot.com/bc2025.crt>, and save to a local file with extension **.cer** in your **jdk\jre\lib\security** folder.</span></span> <span data-ttu-id="044c4-120">Dans cet exemple, supposons que vous avez téléchargé le fichier de certificat racine Baltimore CyberTrust sous le nom **bc2025.cer**.</span><span class="sxs-lookup"><span data-stu-id="044c4-120">For this example, assume that you downloaded the Baltimore CyberTrust root certificate file as **bc2025.cer**.</span></span>

   > [!NOTE]
   > 
   > <span data-ttu-id="044c4-121">Le certificat racine Baltimore CyberTrust a un numéro de série de `02:00:00:b9` et une empreinte SHA1 de `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span><span class="sxs-lookup"><span data-stu-id="044c4-121">The Baltimore CyberTrust root certificate has a serial number of `02:00:00:b9`, and a SHA1 thumbprint of `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.</span></span>
   > 

2. <span data-ttu-id="044c4-122">Importez le certificat dans le magasin cacerts via la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="044c4-122">Import the certificate to the cacerts store by using the following command:</span></span>

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   <span data-ttu-id="044c4-123">Où :</span><span class="sxs-lookup"><span data-stu-id="044c4-123">Where:</span></span>

   |  <span data-ttu-id="044c4-124">Paramètre</span><span class="sxs-lookup"><span data-stu-id="044c4-124">Parameter</span></span>   |                              <span data-ttu-id="044c4-125">Description</span><span class="sxs-lookup"><span data-stu-id="044c4-125">Description</span></span>                               |
   |--------------|------------------------------------------------------------------------|
   | `keystore`   | <span data-ttu-id="044c4-126">Spécifie le magasin de certificats.</span><span class="sxs-lookup"><span data-stu-id="044c4-126">Specifies the certificate store.</span></span>                                       |
   | `importcert` | <span data-ttu-id="044c4-127">Spécifie que vous importez un certificat.</span><span class="sxs-lookup"><span data-stu-id="044c4-127">Specifies that you are importing a certificate.</span></span>                        |
   | `alias`      | <span data-ttu-id="044c4-128">Spécifie un alias pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="044c4-128">Specifies an alias for the certificate.</span></span>                                |
   | `file`       | <span data-ttu-id="044c4-129">Spécifie le nom de fichier du certificat racine que vous importez.</span><span class="sxs-lookup"><span data-stu-id="044c4-129">Specifies the filename of the root certificate that you are importing.</span></span> |


3. <span data-ttu-id="044c4-130">Si vous êtes invité à approuver le certificat, vérifiez l’empreinte en tant que `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` et saisissez **y** si l’empreinte est correcte.</span><span class="sxs-lookup"><span data-stu-id="044c4-130">If you are prompted to trust the certificate, verify the thumbprint as `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, and type **y** if the thumbprint is correct.</span></span>

4. <span data-ttu-id="044c4-131">Exécutez la commande suivante pour vous assurer que le certificat d'autorité de certification a été correctement importé :</span><span class="sxs-lookup"><span data-stu-id="044c4-131">Run the following command to ensure the CA certificate has been successfully imported:</span></span>

   ```shell
   keytool -list -keystore cacerts
   ```

<span data-ttu-id="044c4-132">Une fois que vous avez ajouté le certificat racine pour votre JDK, vous pouvez compresser le contenu du JDK et l’ajouter au dossier **approot** de votre projet Azure.</span><span class="sxs-lookup"><span data-stu-id="044c4-132">After you have successfully added the root certificate to your JDK, you can zip the contents of JDK and add it to your Azure project's **approot** folder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="044c4-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="044c4-133">Next steps</span></span>

<span data-ttu-id="044c4-134">Pour plus d’informations sur l’utilitaire keytool, consultez <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span><span class="sxs-lookup"><span data-stu-id="044c4-134">For more information about the keytool utility, see <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.</span></span>

<span data-ttu-id="044c4-135">Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="044c4-135">For more information about Java, see [Azure for Java developers](/java/azure).</span></span>

<!-- For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx). -->
