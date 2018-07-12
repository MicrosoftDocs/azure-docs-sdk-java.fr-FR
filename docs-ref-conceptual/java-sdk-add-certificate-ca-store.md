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
# <a name="adding-a-root-certificate-to-the-java-ca-certificates-store"></a>Ajout d’un certificat racine au magasin de certificats d’autorité de certification Java

Les applications qui utilisent des services Azure (tels qu'Azure Service Bus) doivent approuver le certificat racine Baltimore CyberTrust. Il est possible que le certificat soit déjà installé sur votre système, mais dans le cas contraire, les étapes décrites dans ce didacticiel vous montreront comment utiliser le **keytool** d’Oracle pour ajouter le certificat racine de certificat d’autorité de certification (CA) au magasin de certificats (cacerts) de l'autorité de certification Java que vous utiliserez pour les services Azure.

L’utilitaire keytool d’Oracle est un _Outil de gestion de clés et de certificats_ qui permet aux développeurs de gérer la liste des certificats approuvés pour une utilisation avec Java. Vous pouvez utiliser keytool pour ajouter le certificat d’autorité de certification avant de compresser le JDK et de l’ajouter au dossier **approot** de votre projet Azure. Vous pouvez également utiliser une tâche de démarrage Azure qui utilise keytool pour ajouter le certificat.

Dès le 15 avril 2013, Azure a commencé à migrer du certificat racine GTE CyberTrust Global au certificat racine Baltimore CyberTrust. Les étapes suivantes vous montrent comment utiliser keytool pour ajouter le certificat racine Baltimore CyberTrust dans votre magasin de certificats (cacerts) de l’autorité de certification Java.

> [!NOTE]
> 
> Vous pouvez suivre les étapes décrites dans cet article pour configurer votre Kit de développement logiciel Java pour approuver les certificats racine à partir d’autres autorités de certification approuvées. Par exemple, vous souhaitez peut-être obtenir un certificat racine dans la liste de certificats répertoriée dans la page [Certificats racines GeoTrust](http://www.geotrust.com/resources/root-certificates/).
> 

## <a name="determining-which-root-certificates-are-installed"></a>Déterminer les certificats racine installés

Il est possible que le certificat Baltimore soit déjà installé dans votre magasin cacerts ; suivez la procédure suivante pour le déterminer.

1. Sur une invite de commandes administrateur, accédez à votre dossier JDK **jdk\jre\lib\security**, puis exécutez la commande suivante pour répertorier les certificats qui sont installés sur votre système :

   ```shell
   keytool -list -keystore cacerts
   ```

1. Si le mot de passe du magasin est demandé, le mot de passe par défaut est **changeit**.

   > [!NOTE]
   > 
   > Si vous souhaitez modifier le mot de passe, consultez la documentation de keytool à l’adresse <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.
   > 

1. Si vous ne voyez pas le certificat avec l’empreinte de `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`, suivez les étapes décrites dans la section suivante pour télécharger et installer le certificat.

## <a name="to-add-a-root-certificate-to-the-cacerts-store"></a>Ajout d'un certificat racine au magasin cacerts

1. Téléchargez le certificat racine Baltimore CyberTrust à partir de <https://cacert.omniroot.com/bc2025.crt> et enregistrez-le dans un fichier local avec l’extension **.cer** dans votre dossier **jdk\jre\lib\security**. Dans cet exemple, supposons que vous avez téléchargé le fichier de certificat racine Baltimore CyberTrust sous le nom **bc2025.cer**.

   > [!NOTE]
   > 
   > Le certificat racine Baltimore CyberTrust a un numéro de série de `02:00:00:b9` et une empreinte SHA1 de `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74`.
   > 

2. Importez le certificat dans le magasin cacerts via la commande suivante :

   ```shell
   keytool -keystore cacerts -importcert -alias bc2025ca -file bc2025.cer
   ```
   Où :

   |  Paramètre   |                              Description                               |
   |--------------|------------------------------------------------------------------------|
   | `keystore`   | Spécifie le magasin de certificats.                                       |
   | `importcert` | Spécifie que vous importez un certificat.                        |
   | `alias`      | Spécifie un alias pour le certificat.                                |
   | `file`       | Spécifie le nom de fichier du certificat racine que vous importez. |


3. Si vous êtes invité à approuver le certificat, vérifiez l’empreinte en tant que `d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2c:78:db:28:52:ca:e4:74` et saisissez **y** si l’empreinte est correcte.

4. Exécutez la commande suivante pour vous assurer que le certificat d'autorité de certification a été correctement importé :

   ```shell
   keytool -list -keystore cacerts
   ```

Une fois que vous avez ajouté le certificat racine pour votre JDK, vous pouvez compresser le contenu du JDK et l’ajouter au dossier **approot** de votre projet Azure.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’utilitaire keytool, consultez <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).

<!-- For more information about the root certificates used by Azure, see [Azure Root Certificate Migration](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx). -->
