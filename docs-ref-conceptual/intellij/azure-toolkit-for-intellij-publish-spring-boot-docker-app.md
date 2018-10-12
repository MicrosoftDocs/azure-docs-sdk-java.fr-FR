---
title: Publier une application Spring Boot en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ
description: Découvrez comment publier une application web sur Microsoft Azure en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ.
services: ''
documentationcenter: java
author: rmcmurray
manager: routlaw
editor: ''
ms.assetid: ''
ms.author: robmcm
ms.date: 02/01/2018
ms.devlang: Java
ms.service: multiple
ms.tgt_pltfrm: multiple
ms.topic: article
ms.workload: na
ms.openlocfilehash: 4228352efa4354bfe4969c1a5ecd3f3b40483f85
ms.sourcegitcommit: b64017f119177f97da7a5930489874e67b09c0fc
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48893580"
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="685ac-103">Publier une application Spring Boot en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="685ac-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="685ac-104">L’[Spring Framework] est une solution open source qui aide les développeurs Java à créer des applications d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="685ac-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="685ac-105">Un des projets les plus connus basés sur cette plateforme est [Spring Boot], qui fournit une approche simplifiée pour la création d’applications Java autonomes.</span><span class="sxs-lookup"><span data-stu-id="685ac-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="685ac-106">[Docker] est une solution open source qui aide les développeurs à automatiser le déploiement, la mise à l’échelle et la gestion de leurs applications qui s’exécutent dans des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="685ac-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="685ac-107">Ce didacticiel détaille la marche à suivre pour déployer une application Spring Boot en tant que conteneur Docker vers Microsoft Azure à l’aide du kit de ressources Azure pour IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="685ac-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="685ac-108">Cloner le référentiel Docker Spring Boot par défaut</span><span class="sxs-lookup"><span data-stu-id="685ac-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="685ac-109">Les étapes suivantes détaillent la procédure de clonage du référentiel Docker Spring Boot à l’aide d’IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="685ac-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="685ac-110">Si vous voulez utiliser une ligne de commande, voir [Déployer une application Spring Boot sur Linux dans Azure Container Service][Deploy Spring Boot on Linux in AKS].</span><span class="sxs-lookup"><span data-stu-id="685ac-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in AKS].</span></span>

1. <span data-ttu-id="685ac-111">Ouvrez IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="685ac-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="685ac-112">Dans l’écran d’accueil, dans la liste **Check out from version control** (Extraire à partir de la gestion de version), sélectionnez **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="685ac-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![Option GitHub pour le contrôle de version][CL01]

1. <span data-ttu-id="685ac-114">Si vous êtes invité à vous connecter, entrez vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="685ac-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="685ac-115">Si vous utilisez un nom d’utilisateur/mot de passe pour vous connecter à GitHub :</span><span class="sxs-lookup"><span data-stu-id="685ac-115">If you are using a username/password to log in to GitHub:</span></span> 

      ![Boîte de dialogue pour la saisie du nom d’utilisateur et du mot de passe GitHub][CL02a]

   * <span data-ttu-id="685ac-117">Si vous utilisez un jeton pour vous connecter à GitHub :</span><span class="sxs-lookup"><span data-stu-id="685ac-117">If you are using a token to log in to GitHub:</span></span> 

      ![Boîte de dialogue pour la saisie d’un jeton GitHub][CL02b]

1. <span data-ttu-id="685ac-119">Entrez **https://github.com/spring-guides/gs-spring-boot-docker.git** pour l’URL du référentiel, spécifiez les informations sur le chemin local et le dossier, puis cliquez sur **Cloner**.</span><span class="sxs-lookup"><span data-stu-id="685ac-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Boîte de dialogue Cloner le référentiel][CL03]

1. <span data-ttu-id="685ac-121">Lorsque vous êtes invité à créer un projet IntelliJ, sélectionnez **Non**.</span><span class="sxs-lookup"><span data-stu-id="685ac-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Refus de créer un projet IntelliJ][CL04]

1. <span data-ttu-id="685ac-123">Dans la page d'accueil, cliquez sur **Import Project** (Importer un projet).</span><span class="sxs-lookup"><span data-stu-id="685ac-123">On the welcome page, click **Import Project**.</span></span>

   ![Choix d’importer un projet][CL05]

1. <span data-ttu-id="685ac-125">Recherchez le chemin d’accès de l’emplacement où vous avez cloné le référentiel Spring Boot, sélectionnez le dossier **complete** sous la racine, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685ac-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Sélectionner un dossier pour l’importation][CL06]

1. <span data-ttu-id="685ac-127">Lorsque vous y êtes invité, sélectionnez **Create project from existing sources** (Créer un projet à partir de sources existantes).</span><span class="sxs-lookup"><span data-stu-id="685ac-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Option pour créer un projet à partir de sources existantes][CL07]

1. <span data-ttu-id="685ac-129">Spécifiez le nom de votre projet ou acceptez le nom par défaut, vérifiez que le chemin du dossier **complete** est correct, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="685ac-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Spécifier le nom du projet][CL08]

1. <span data-ttu-id="685ac-131">Personnalisez les répertoires pour l’importation, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="685ac-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Choisir des répertoires][CL09]

1. <span data-ttu-id="685ac-133">Passez en revue les bibliothèques à importer, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="685ac-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Passer en revue les bibliothèques de projet][CL10]

1. <span data-ttu-id="685ac-135">Passez en revue la structure des modules, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="685ac-135">Review the module structure, and then click **Next**.</span></span>

   ![Passer en revue la structure des modules][CL11]

1. <span data-ttu-id="685ac-137">Spécifiez votre JDK, puis cliquez sur **Next**.</span><span class="sxs-lookup"><span data-stu-id="685ac-137">Specify your JDK, and then click **Next**.</span></span>

   ![Spécifier un JDK][CL12]

1. <span data-ttu-id="685ac-139">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="685ac-139">Click **Finish**.</span></span>

   ![Bouton Terminer][CL13]

<span data-ttu-id="685ac-141">IntelliJ importe l’application Spring Boot en tant que projet, et affiche la structure une fois l’importation terminée.</span><span class="sxs-lookup"><span data-stu-id="685ac-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Application Spring Boot dans IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="685ac-143">Générer votre application Spring Boot</span><span class="sxs-lookup"><span data-stu-id="685ac-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="685ac-144">Générer l’application à l’aide du fichier POM Maven</span><span class="sxs-lookup"><span data-stu-id="685ac-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="685ac-145">Si la fenêtre de l’outil Maven n’est pas ouverte, ouvrez-la.</span><span class="sxs-lookup"><span data-stu-id="685ac-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="685ac-146">Cliquez sur **View (Affichage)** > **Tool Windows (Fenêtre Outil)** > **Maven Projects (Projets Maven)**.</span><span class="sxs-lookup"><span data-stu-id="685ac-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Commandes Fenêtres Outil et Projets Maven][BU01]

1. <span data-ttu-id="685ac-148">Dans la fenêtre Outil de Maven, cliquez avec le bouton droit sur **package**, puis choisissez **Run Maven Build** (Exécuter la build Maven)</span><span class="sxs-lookup"><span data-stu-id="685ac-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="685ac-149">(si votre projet Maven ne s’affiche pas automatiquement, cliquez sur l’icône **Réimporter** dans la barre d’outils de Maven).</span><span class="sxs-lookup"><span data-stu-id="685ac-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Commande Run Maven Build][BU02]

1. <span data-ttu-id="685ac-151">Une fois votre application Spring Boot créée, IntelliJ doit afficher le message **BUILD SUCCESS** (GÉNÉRATION RÉUSSIE).</span><span class="sxs-lookup"><span data-stu-id="685ac-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![Message BUILD SUCCESS][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="685ac-153">Créer un artefact prêt pour le déploiement</span><span class="sxs-lookup"><span data-stu-id="685ac-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="685ac-154">Pour publier votre application Spring Boot, vous devrez créer un artefact prêt pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="685ac-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="685ac-155">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="685ac-155">Use the following steps:</span></span>

1. <span data-ttu-id="685ac-156">Ouvrez votre projet d’application web dans IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="685ac-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="685ac-157">Cliquez sur **File (Fichier)**, puis sur **Project Structure (Structure de projet)**.</span><span class="sxs-lookup"><span data-stu-id="685ac-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Commande Project Structure][ART01]

1. <span data-ttu-id="685ac-159">Cliquez sur le signe plus de couleur verte (**+**) pour ajouter un artefact, cliquez sur **JAR**, puis sur **Empty** (Vide).</span><span class="sxs-lookup"><span data-stu-id="685ac-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Ajouter un artefact][ART02]

1. <span data-ttu-id="685ac-161">Nommez votre artefact tout en prenant garde à ne pas ajouter l’extension « .jar », puis spécifiez le dossier cible pour la sortie Maven.</span><span class="sxs-lookup"><span data-stu-id="685ac-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Spécifier les propriétés de l’artefact][ART03]

1. <span data-ttu-id="685ac-163">Créez un manifeste pour votre artefact (facultatif) :</span><span class="sxs-lookup"><span data-stu-id="685ac-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="685ac-164">a.</span><span class="sxs-lookup"><span data-stu-id="685ac-164">a.</span></span> <span data-ttu-id="685ac-165">Cliquez sur **Create Manifest** (Créer un manifeste).</span><span class="sxs-lookup"><span data-stu-id="685ac-165">Click **Create Manifest**.</span></span>

      ![Cliquer sur le bouton Create Manifest][ART04a]

   <span data-ttu-id="685ac-167">b.</span><span class="sxs-lookup"><span data-stu-id="685ac-167">b.</span></span> <span data-ttu-id="685ac-168">Choisissez le chemin par défaut pour l’artefact, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685ac-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Spécifier le chemin de l’artefact][ART04b]

   <span data-ttu-id="685ac-170">c.</span><span class="sxs-lookup"><span data-stu-id="685ac-170">c.</span></span> <span data-ttu-id="685ac-171">Cliquez sur les points de suspension (**...**) pour localiser la classe principale.</span><span class="sxs-lookup"><span data-stu-id="685ac-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Localiser la classe principale][ART04c]

   <span data-ttu-id="685ac-173">d.</span><span class="sxs-lookup"><span data-stu-id="685ac-173">d.</span></span> <span data-ttu-id="685ac-174">Choisissez votre classe principale, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685ac-174">Choose your main class, and then click **OK**.</span></span>

      ![Spécifier la classe principale][ART04d]

1. <span data-ttu-id="685ac-176">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="685ac-176">Click **OK**.</span></span>

   ![Fermer la boîte de dialogue Project Structure][ART05]

> [!NOTE]
> <span data-ttu-id="685ac-178">Pour plus d’informations sur la création d’artefacts dans IntelliJ, consultez [Configuring Artifacts] (Configuration des artefacts) sur le site web JetBrains.</span><span class="sxs-lookup"><span data-stu-id="685ac-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="685ac-179">Générer l’artefact pour le déploiement</span><span class="sxs-lookup"><span data-stu-id="685ac-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="685ac-180">Cliquez sur **Build** (Générer), puis sur **Artifacts** (Artefacts).</span><span class="sxs-lookup"><span data-stu-id="685ac-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Commande Build Artifacts][BU04]

1. <span data-ttu-id="685ac-182">Quand le menu contextuel **Build Artifact** (Générer un artefact) s’affiche, cliquez sur **Build** (Générer).</span><span class="sxs-lookup"><span data-stu-id="685ac-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Menu contextuel Build Artifact][BU05]

<span data-ttu-id="685ac-184">IntelliJ doit afficher l’artefact terminé pour votre application Spring Boot dans la fenêtre Outil du projet.</span><span class="sxs-lookup"><span data-stu-id="685ac-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Artefact créé][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="685ac-186">Publier votre application web sur Azure en utilisant un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="685ac-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="685ac-187">Si vous ne vous êtes pas connecté à votre compte Azure, procédez de la manière décrite dans [Instructions de connexion pour le Kit de ressources Azure pour IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="685ac-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="685ac-188">Dans la fenêtre Outil d’exploration de projets, cliquez avec le bouton droit sur le projet, puis sélectionnez **Azure** > **Publish as Docker Container** (Publier en tant que conteneur Docker).</span><span class="sxs-lookup"><span data-stu-id="685ac-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Commande Publish as Docker Container][PU01]

1. <span data-ttu-id="685ac-190">Quand la boîte de dialogue **Deploy Docker Container on Azure** (Déployer un conteneur Docker sur Azure) apparaît, tous les hôtes Docker existants sont affichés.</span><span class="sxs-lookup"><span data-stu-id="685ac-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="685ac-191">Si vous choisissez d’effectuer le déploiement dans un hôte existant, vous pouvez passer directement à l’étape 4.</span><span class="sxs-lookup"><span data-stu-id="685ac-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="685ac-192">Autrement, procédez comme suit pour créer un hôte :</span><span class="sxs-lookup"><span data-stu-id="685ac-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="685ac-193">a.</span><span class="sxs-lookup"><span data-stu-id="685ac-193">a.</span></span> <span data-ttu-id="685ac-194">Cliquez sur le signe plus de couleur verte (**+**).</span><span class="sxs-lookup"><span data-stu-id="685ac-194">Click the green plus (**+**) symbol.</span></span>

      ![Ajouter un nouvel hôte Docker][PU02]

   <span data-ttu-id="685ac-196">b.</span><span class="sxs-lookup"><span data-stu-id="685ac-196">b.</span></span> <span data-ttu-id="685ac-197">Quand la boîte de dialogue **Create Docker Host** (Créer un hôte Docker) apparaît, vous pouvez accepter les valeurs par défaut ou spécifier divers paramètres personnalisés pour votre nouvel hôte Docker</span><span class="sxs-lookup"><span data-stu-id="685ac-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="685ac-198">(pour des descriptions détaillées des différents paramètres, voir [Publier une application web en tant que conteneur Docker à l’aide du kit de ressources Azure pour IntelliJ][Publish Container with Azure Toolkit]). Cliquez sur **Next** une fois que vous avez spécifié les paramètres à utiliser.</span><span class="sxs-lookup"><span data-stu-id="685ac-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Spécifier les options de l’hôte Docker][PU03a]

   <span data-ttu-id="685ac-200">c.</span><span class="sxs-lookup"><span data-stu-id="685ac-200">c.</span></span> <span data-ttu-id="685ac-201">Vous pouvez utiliser des identifiants de connexion existants d’un coffre de clés Azure, ou entrer de nouveaux identifiants de connexion Docker.</span><span class="sxs-lookup"><span data-stu-id="685ac-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="685ac-202">Cliquez sur **Finish** une fois que vous avez spécifié vos options.</span><span class="sxs-lookup"><span data-stu-id="685ac-202">Click **Finish** when you have specified your options.</span></span>

      ![Spécifier les identifiants de connexion à l’hôte Docker][PU03b]

1. <span data-ttu-id="685ac-204">Sélectionnez votre hôte Docker, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="685ac-204">Select your Docker host, and then click **Next**.</span></span>

   ![Sélectionner l’hôte Docker à utiliser][PU04]

1. <span data-ttu-id="685ac-206">Dans la dernière page de la boîte de dialogue **Deploy Docker Container on Azure** (Déployer un conteneur Docker sur Azure), spécifiez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="685ac-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="685ac-207">a.</span><span class="sxs-lookup"><span data-stu-id="685ac-207">a.</span></span> <span data-ttu-id="685ac-208">Vous pouvez spécifier un nom personnalisé pour le conteneur qui doit héberger votre conteneur Docker, ou accepter le nom par défaut.</span><span class="sxs-lookup"><span data-stu-id="685ac-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="685ac-209">b.</span><span class="sxs-lookup"><span data-stu-id="685ac-209">b.</span></span> <span data-ttu-id="685ac-210">Entrez les ports TCP de votre hôte Docker en utilisant la syntaxe suivante : «  *[port externe]*:*[port interne]*.</span><span class="sxs-lookup"><span data-stu-id="685ac-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="685ac-211">Par exemple, dans **80:8080**, 80 est un port externe et 8080 le port interne par défaut de Spring Boot.</span><span class="sxs-lookup"><span data-stu-id="685ac-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="685ac-212">Si vous avez personnalisé le port interne (par exemple, en modifiant le fichier application.yml), vous devez spécifier le numéro de port pour que le routage dans Azure soit correct.</span><span class="sxs-lookup"><span data-stu-id="685ac-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="685ac-213">c.</span><span class="sxs-lookup"><span data-stu-id="685ac-213">c.</span></span> <span data-ttu-id="685ac-214">Après avoir configuré ces options, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="685ac-214">After you have configured these options, click **Finish**.</span></span>

   ![Déployer un conteneur Docker dans Azure][PU05]

1. <span data-ttu-id="685ac-216">Une fois que le kit de ressources Azure a terminé la publication, le journal d’activité d’Azure affiche le statut **Publié**.</span><span class="sxs-lookup"><span data-stu-id="685ac-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Déploiement réussi de l’hôte Docker][PU06]

## <a name="next-steps"></a><span data-ttu-id="685ac-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="685ac-218">Next steps</span></span>

<span data-ttu-id="685ac-219">Pour en savoir plus sur les autres méthodes permettant de créer des applications Spring Boot à l’aide d’IntelliJ, voir [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) (Création de projets Spring Boot) sur le site web de JetBrains.</span><span class="sxs-lookup"><span data-stu-id="685ac-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-additional-resources](../includes/azure-toolkit-for-intellij-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Configuration des artefacts)
[Deploy Spring Boot on Linux in AKS]: /azure/container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
