---
title: Commandes de complément pour Excel, Word et PowerPoint
description: ''
ms.date: 01/23/2018
ms.openlocfilehash: 68eee18233b6b874f237ded41009561dbde774de
ms.sourcegitcommit: 4e4f7c095e8f33b06bd8a02534ee901125eb1d17
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/28/2018
ms.locfileid: "20084062"
---
# <a name="add-in-commands-for-excel-word-and-powerpoint"></a><span data-ttu-id="015e7-102">Commandes de complément pour Excel, Word et PowerPoint</span><span class="sxs-lookup"><span data-stu-id="015e7-102">Add-in commands for Excel, Word, and PowerPoint</span></span>

<span data-ttu-id="015e7-p101">Les commandes de complément sont des éléments d’interface utilisateur qui étendent l’interface utilisateur d’Office et lancent des actions dans votre complément. Vous pouvez les utiliser pour ajouter un bouton sur le ruban ou un élément dans le menu contextuel. Lorsque les utilisateurs sélectionnent une commande de complément, ils lancent des actions telles que l’exécution de code JavaScript ou l’affichage d’une page du complément dans le volet Office. Les commandes de complément aident les utilisateurs à trouver et utiliser votre complément, ce qui favorise l’adoption et la réutilisation de votre complément, et améliore la fidélisation des clients.</span><span class="sxs-lookup"><span data-stu-id="015e7-p101">Add-in commands are UI elements that extend the Office UI and start actions in your add-in. You can use add-in commands to add a button on the ribbon or an item to a context menu. When users select an add-in command, they initiate actions such as running JavaScript code, or showing a page of the add-in in a task pane. Add-in commands help users find and use your add-in, which can help increase your add-in's adoption and reuse, and improve customer retention.</span></span>

<span data-ttu-id="015e7-107">Pour en savoir plus sur les fonctionnalités, regardez la vidéo sur les [commandes de complément du ruban Office](https://channel9.msdn.com/events/Build/2016/P551).</span><span class="sxs-lookup"><span data-stu-id="015e7-107">For an overview of the feature, see the video [Add-in Commands in the Office Ribbon](https://channel9.msdn.com/events/Build/2016/P551).</span></span>

> [!NOTE]
> <span data-ttu-id="015e7-p102">Les catalogues SharePoint n’acceptent pas les commandes de complément. Vous pouvez déployer des commandes de complément via le [déploiement centralisé](../publish/centralized-deployment.md) ou [AppSource](https://docs.microsoft.com/en-us/office/dev/store/submit-to-the-office-store), ou utiliser le [chargement de version test](../testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins.md) pour déployer votre commande de complément à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="015e7-p102">SharePoint catalogs do not support add-in commands. You can deploy add-in commands via [Centralized Deployment](../publish/centralized-deployment.md) or [AppSource](https://docs.microsoft.com/en-us/office/dev/store/submit-to-the-office-store), or use [sideloading](../testing/create-a-network-shared-folder-catalog-for-task-pane-and-content-add-ins.md) to deploy your add-in command for testing.</span></span> 

<span data-ttu-id="015e7-110">*Figure 1. Complément incluant des commandes en cours d’exécution dans Excel (version de bureau)*</span><span class="sxs-lookup"><span data-stu-id="015e7-110">*Figure 1. Add-in with commands running in Excel Desktop*</span></span>

![Capture d’écran d’une commande de complément dans Excel](../images/add-in-commands-1.png)

<span data-ttu-id="015e7-112">*Figure 2. Complément incluant des commandes en cours d’exécution dans Excel Online*</span><span class="sxs-lookup"><span data-stu-id="015e7-112">*Figure 2. Add-in with commands running in Excel Online*</span></span>

![Capture d’écran d’une commande de complément dans Excel Online](../images/add-in-commands-2.png)

## <a name="command-capabilities"></a><span data-ttu-id="015e7-114">Fonctionnalités de commande</span><span class="sxs-lookup"><span data-stu-id="015e7-114">Command capabilities</span></span>
<span data-ttu-id="015e7-115">Les fonctionnalités de commande suivantes sont actuellement prises en charge.</span><span class="sxs-lookup"><span data-stu-id="015e7-115">The following command capabilities are currently supported.</span></span>

> [!NOTE]
> <span data-ttu-id="015e7-116">Les compléments de contenu ne prennent actuellement pas en charge les commandes de complément.</span><span class="sxs-lookup"><span data-stu-id="015e7-116">Content add-ins do not currently support add-in commands.</span></span>

<span data-ttu-id="015e7-117">**Points d’extension**</span><span class="sxs-lookup"><span data-stu-id="015e7-117">**Extension points**</span></span>

- <span data-ttu-id="015e7-118">Onglets de ruban - Permet d’étendre les onglets prédéfinis ou de créer un onglet personnalisé.</span><span class="sxs-lookup"><span data-stu-id="015e7-118">Ribbon tabs - Extend built-in tabs or create a new custom tab.</span></span>
- <span data-ttu-id="015e7-119">Menus contextuels - Permet d’étendre les menus contextuels sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="015e7-119">Context menus - Extend selected context menus.</span></span> 

<span data-ttu-id="015e7-120">**Types de contrôles**</span><span class="sxs-lookup"><span data-stu-id="015e7-120">**Control types**</span></span>

- <span data-ttu-id="015e7-121">Boutons simples - Permettent de déclencher des actions spécifiques.</span><span class="sxs-lookup"><span data-stu-id="015e7-121">Simple buttons - trigger specific actions.</span></span>
- <span data-ttu-id="015e7-122">Menus - Menu déroulant simple avec des boutons qui déclenchent des actions.</span><span class="sxs-lookup"><span data-stu-id="015e7-122">Menus - simple menu dropdown with buttons that trigger actions.</span></span>

<span data-ttu-id="015e7-123">**Actions**</span><span class="sxs-lookup"><span data-stu-id="015e7-123">**Actions**</span></span>

- <span data-ttu-id="015e7-124">ShowTaskpane - Affiche un ou plusieurs volets où sont chargées des pages HTML personnalisées.</span><span class="sxs-lookup"><span data-stu-id="015e7-124">ShowTaskpane - Displays one or multiple panes that load custom HTML pages inside them.</span></span>
- <span data-ttu-id="015e7-p103">ExecuteFunction - Charge une page HTML invisible, puis y exécute une fonction JavaScript. Pour afficher l’interface utilisateur au sein de votre fonction (par exemple, erreurs, avancement, entrées supplémentaires), vous pouvez utiliser l’API [displayDialog](http://dev.office.com/reference/add-ins/shared/officeui).</span><span class="sxs-lookup"><span data-stu-id="015e7-p103">ExecuteFunction - Loads an invisible HTML page and then execute a JavaScript function within it. To show UI within your function (such as errors, progress, or additional input) you can use the [displayDialog](http://dev.office.com/reference/add-ins/shared/officeui) API.</span></span>  

## <a name="supported-platforms"></a><span data-ttu-id="015e7-127">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="015e7-127">Supported platforms</span></span>
<span data-ttu-id="015e7-128">Les commandes de complément sont actuellement prises en charge sur les plateformes suivantes :</span><span class="sxs-lookup"><span data-stu-id="015e7-128">Add-in commands are currently supported on the following platforms:</span></span>

- <span data-ttu-id="015e7-129">Office pour bureau Windows 2016 (build 16.0.6769+)</span><span class="sxs-lookup"><span data-stu-id="015e7-129">Office for Windows Desktop 2016 (build 16.0.6769+)</span></span>
- <span data-ttu-id="015e7-130">Office pour Mac (build 15.33+)</span><span class="sxs-lookup"><span data-stu-id="015e7-130">Office for Mac (build 15.33+)</span></span>
- <span data-ttu-id="015e7-131">Office Online</span><span class="sxs-lookup"><span data-stu-id="015e7-131">Office Online</span></span> 

<span data-ttu-id="015e7-132">D’autres plateformes seront bientôt disponibles.</span><span class="sxs-lookup"><span data-stu-id="015e7-132">More platforms are coming soon.</span></span>

## <a name="best-practices"></a><span data-ttu-id="015e7-133">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="015e7-133">Best practices</span></span>

<span data-ttu-id="015e7-134">Appliquez les meilleures pratiques suivantes lorsque vous développez des commandes de complément :</span><span class="sxs-lookup"><span data-stu-id="015e7-134">Apply the following best practices when you develop add-in commands:</span></span>

- <span data-ttu-id="015e7-p104">Utilisez les commandes pour représenter une action spécifique avec un résultat clair et précis pour les utilisateurs. Ne combinez pas plusieurs actions dans un seul bouton.</span><span class="sxs-lookup"><span data-stu-id="015e7-p104">Use commands to represent a specific action with a clear and specific outcome for users. Do not combine multiple actions in a single button.</span></span>
- <span data-ttu-id="015e7-p105">Proposez des actions détaillées permettant de réaliser plus efficacement des tâches courantes dans votre complément. Réduisez le nombre d’étapes nécessaires à la réalisation d’une action.</span><span class="sxs-lookup"><span data-stu-id="015e7-p105">Provide granular actions that make common tasks within your add-in more efficient to perform. Minimize the number of steps an action takes to complete.</span></span>
- <span data-ttu-id="015e7-139">Pour placer vos commandes dans le ruban Office :</span><span class="sxs-lookup"><span data-stu-id="015e7-139">For the placement of your commands in the Office ribbon:</span></span>
    - <span data-ttu-id="015e7-p106">Placez les commandes sur un onglet existant (Insertion, Révision, etc.) si la fonctionnalité ajoutée lui correspond. Par exemple, si votre complément permet aux utilisateurs d’insérer un élément multimédia, ajoutez un groupe à l’onglet Insertion. Notez que l’ensemble des onglets ne sont pas nécessairement disponibles dans toutes les versions d’Office. Pour plus d’informations, voir le [manifeste XML de compléments Office](../develop/add-in-manifests.md).</span><span class="sxs-lookup"><span data-stu-id="015e7-p106">Place commands on an existing tab (Insert, Review, and so on) if the functionality provided fits there. For example, if your add-in enables users to insert media, add a group to the Insert tab. Note that not all tabs are available across all Office versions. For more information, see [Office Add-ins XML manifest](../develop/add-in-manifests.md).</span></span> 
    - <span data-ttu-id="015e7-p107">Placez les commandes sous l’onglet Accueil si la fonctionnalité ne correspond à aucun autre onglet, et si vous avez moins de six commandes de niveau supérieur. Vous pouvez également ajouter des commandes à l’onglet Accueil si votre complément doit fonctionner sur toutes les versions d’Office (par exemple, Office Desktop et Office Online) et si un onglet n’est pas disponible dans toutes les versions (par exemple, si l’onglet Création n’existe pas dans Office Online).</span><span class="sxs-lookup"><span data-stu-id="015e7-p107">Place commands on the Home tab if the functionality doesn't fit on another tab, and you have fewer than six top-level commands. You can also add commands to the Home tab if your add-in needs to work across Office versions (such as Office Desktop and Office Online) and a tab is not available in all versions (for example, the Design tab doesn't exist in Office Online).</span></span>  
    - <span data-ttu-id="015e7-145">Placez des commandes dans un onglet personnalisé si vous avez plus de six commandes de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="015e7-145">Place commands on a custom tab if you have more than six top-level commands.</span></span> 
    - <span data-ttu-id="015e7-p108">Nommez votre groupe en fonction du nom de votre complément. Si vous avez plusieurs groupes, nommez chaque groupe en fonction de la fonctionnalité offerte par les commandes de ce groupe.</span><span class="sxs-lookup"><span data-stu-id="015e7-p108">Name your group to match the name of your add-in. If you have multiple groups, name each group based on the functionality that the commands in that group provide.</span></span>
    - <span data-ttu-id="015e7-148">N’ajoutez pas de boutons superflus pour augmenter la valeur de votre complément.</span><span class="sxs-lookup"><span data-stu-id="015e7-148">Do not add superfluous buttons to increase the real estate of your add-in.</span></span>

     > [!NOTE]
     > <span data-ttu-id="015e7-149">Les compléments qui occupent trop d’espace peuvent ne pas obtenir la [validation d’AppSource](https://docs.microsoft.com/en-us/office/dev/store/validation-policies).</span><span class="sxs-lookup"><span data-stu-id="015e7-149">Add-ins that take up too much space might not pass [AppSource validation](https://docs.microsoft.com/en-us/office/dev/store/validation-policies).</span></span>

- <span data-ttu-id="015e7-150">Pour toutes les icônes, suivez les [règles de conception d’icône](add-in-icons.md).</span><span class="sxs-lookup"><span data-stu-id="015e7-150">For all icons, follow the [icon design guidelines](add-in-icons.md).</span></span>
- <span data-ttu-id="015e7-p109">Proposez une version de complément qui fonctionne aussi sur les hôtes qui ne prennent pas en charge les commandes. Un seul manifeste de complément peut fonctionner sur les hôtes tenant compte ou non des commandes (par exemple, un volet de tâches dans le second cas).</span><span class="sxs-lookup"><span data-stu-id="015e7-p109">Provide a version of your add-in that also works on hosts that do not support commands. A single add-in manifest can work in both command-aware (with commands) and non-command-aware (as a taskpane) hosts.</span></span>

   <span data-ttu-id="015e7-153">*Figure 3. Complément du volet Office dans Office 2013 et le même complément utilisant des commandes de complément dans Office 2016*</span><span class="sxs-lookup"><span data-stu-id="015e7-153">*Figure 3. Task pane add-in in Office 2013 and the same add-in using add-in commands in Office 2016*</span></span>

   ![Capture d’écran illustrant un complément du volet Office dans Office 2013 et le même complément utilisant des commandes de complément dans Office 2016](../images/office-task-pane-add-ins.png)


## <a name="next-steps"></a><span data-ttu-id="015e7-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="015e7-155">Next steps</span></span>

<span data-ttu-id="015e7-156">La meilleure façon de commencer à utiliser des commandes de complément consiste à consulter des [exemples de commandes de complément Office](https://github.com/OfficeDev/Office-Add-in-Commands-Samples/) sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="015e7-156">The best way to get started using add-in commands is to take a look at the [Office Add-in commands samples](https://github.com/OfficeDev/Office-Add-in-Commands-Samples/) on GitHub.</span></span>

<span data-ttu-id="015e7-157">Pour plus d’informations sur la spécification des commandes de complément dans votre manifeste, reportez-vous à l’article expliquant comment [créer des commandes de complément dans votre manifeste](../develop/create-addin-commands.md) et au contenu de référence sur [VersionOverrides](https://dev.office.com/reference/add-ins/manifest/versionoverrides).</span><span class="sxs-lookup"><span data-stu-id="015e7-157">For more information about specifying add-in commands in your manifest, see [Create add-in commands in your manifest](../develop/create-addin-commands.md) and the [VersionOverrides](https://dev.office.com/reference/add-ins/manifest/versionoverrides) reference content.</span></span>



