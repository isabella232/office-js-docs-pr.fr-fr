---
title: Configuration de votre environnement de développement
description: Configuration de votre environnement de développement pour créer des compléments Office
ms.date: 04/03/2020
localization_priority: Normal
ms.openlocfilehash: 03cf525408123df9e8356555f2ab7732ed2ca263
ms.sourcegitcommit: c3bfea0818af1f01e71a1feff707fb2456a69488
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2020
ms.locfileid: "43185602"
---
# <a name="set-up-your-development-environment"></a><span data-ttu-id="5f84c-103">Configuration de votre environnement de développement</span><span class="sxs-lookup"><span data-stu-id="5f84c-103">Set up your development environment</span></span>

<span data-ttu-id="5f84c-104">Ce guide vous aide à configurer les outils de manière à pouvoir créer des compléments Office en suivant nos guides de démarrage rapide ou nos didacticiels.</span><span class="sxs-lookup"><span data-stu-id="5f84c-104">This guide helps you set up tools so you can create Office Add-ins by following our quick starts or tutorials.</span></span> <span data-ttu-id="5f84c-105">Vous devrez installer les outils à partir de la liste ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5f84c-105">You'll need to install the tools from the list below.</span></span> <span data-ttu-id="5f84c-106">Si ces éléments sont déjà installés, vous êtes prêt à commencer un démarrage rapide, tel que le [démarrage rapide de Microsoft Excel REACT](../quickstarts/excel-quickstart-react.md).</span><span class="sxs-lookup"><span data-stu-id="5f84c-106">If you already have these installed, you are ready to begin a quick start, such as this [Excel React quick start](../quickstarts/excel-quickstart-react.md).</span></span>

- <span data-ttu-id="5f84c-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="5f84c-107">Node.js</span></span>
- <span data-ttu-id="5f84c-108">npm</span><span class="sxs-lookup"><span data-stu-id="5f84c-108">npm</span></span>
- <span data-ttu-id="5f84c-109">Un compte Office 365 (la version d’abonnement d’Office)</span><span class="sxs-lookup"><span data-stu-id="5f84c-109">An Office 365 (the subscription version of Office) account</span></span>
- <span data-ttu-id="5f84c-110">Un éditeur de code de votre choix</span><span class="sxs-lookup"><span data-stu-id="5f84c-110">A code editor of your choice</span></span>

<span data-ttu-id="5f84c-111">Ce guide suppose que vous sachiez comment utiliser un outil de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="5f84c-111">This guide assumes that you know how to use a command line tool.</span></span> 

## <a name="install-nodejs"></a><span data-ttu-id="5f84c-112">Installer Node.js.</span><span class="sxs-lookup"><span data-stu-id="5f84c-112">Install Node.js</span></span>

<span data-ttu-id="5f84c-113">Node. js est un Runtime JavaScript dont vous aurez besoin pour développer des compléments Office modernes.</span><span class="sxs-lookup"><span data-stu-id="5f84c-113">Node.js is a JavaScript runtime you will need to develop modern Office Add-ins.</span></span>

<span data-ttu-id="5f84c-114">Installez node. js en [téléchargeant la version recommandée la plus récente à partir de leur site Web](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="5f84c-114">Install Node.js by [downloading the latest recommended version from their website](https://nodejs.org).</span></span> <span data-ttu-id="5f84c-115">Suivez les instructions d’installation pour votre système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="5f84c-115">Follow the installation instructions for your operating system.</span></span>

## <a name="install-npm"></a><span data-ttu-id="5f84c-116">Installer NPM</span><span class="sxs-lookup"><span data-stu-id="5f84c-116">Install npm</span></span>

<span data-ttu-id="5f84c-117">NPM est un registre de logiciels open source à partir duquel télécharger les packages utilisés dans le développement des compléments Office.</span><span class="sxs-lookup"><span data-stu-id="5f84c-117">npm is an open source software registry from which to download the packages used in developing Office Add-ins.</span></span>

<span data-ttu-id="5f84c-118">Pour installer NPM, exécutez ce qui suit dans la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="5f84c-118">To install npm, run the following in the command line:</span></span>

```command&nbsp;line
    npm install npm -g
```

<span data-ttu-id="5f84c-119">Pour vérifier si NPM est déjà installé et voir la version installée, exécutez la commande suivante dans la ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="5f84c-119">To check if you already have npm installed and see the installed version, run the following in the command line:</span></span>

```command&nbsp;line
npm -v
```

<span data-ttu-id="5f84c-120">Vous souhaiterez peut-être utiliser un gestionnaire de version de nœud pour vous permettre de basculer entre plusieurs versions de node. js et NPM, mais ce n’est pas obligatoire.</span><span class="sxs-lookup"><span data-stu-id="5f84c-120">You may wish to use a Node version manager to allow you to switch between multiple versions of Node.js and npm, but this is not strictly necessary.</span></span> <span data-ttu-id="5f84c-121">Pour plus d’informations sur la procédure à suivre, [consultez les instructions de NPM](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm).</span><span class="sxs-lookup"><span data-stu-id="5f84c-121">For details on how to do this, [see npm's instructions](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm).</span></span>

## <a name="get-office-365"></a><span data-ttu-id="5f84c-122">Obtenir Office 365</span><span class="sxs-lookup"><span data-stu-id="5f84c-122">Get Office 365</span></span>

<span data-ttu-id="5f84c-123">Si vous n’avez pas un compte Office 365, vous pouvez en obtenir un abonnement Office 365 gratuit et renouvelable de 90 jours en rejoignant le [Programme pour les développeurs Office 365](https://developer.microsoft.com/office/dev-program).</span><span class="sxs-lookup"><span data-stu-id="5f84c-123">If you don't already have an Office 365 account, you can get a free, 90-day renewable Office 365 subscription by joining the [Office 365 Developer Program](https://developer.microsoft.com/office/dev-program).</span></span>

## <a name="install-a-code-editor"></a><span data-ttu-id="5f84c-124">Installer un éditeur de code</span><span class="sxs-lookup"><span data-stu-id="5f84c-124">Install a code editor</span></span>

<span data-ttu-id="5f84c-125">Vous pouvez utiliser n’importe quel éditeur de code ou IDE qui prend en charge le développement côté client pour créer votre composant WebPart, par exemple :</span><span class="sxs-lookup"><span data-stu-id="5f84c-125">You can use any code editor or IDE that supports client-side development to build your web part, such as:</span></span>

- [<span data-ttu-id="5f84c-126">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5f84c-126">Visual Studio Code</span></span>](https://code.visualstudio.com/)
- [<span data-ttu-id="5f84c-127">Atom</span><span class="sxs-lookup"><span data-stu-id="5f84c-127">Atom</span></span>](https://atom.io)
- [<span data-ttu-id="5f84c-128">Webstorm</span><span class="sxs-lookup"><span data-stu-id="5f84c-128">Webstorm</span></span>](https://www.jetbrains.com/webstorm)

## <a name="next-steps"></a><span data-ttu-id="5f84c-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5f84c-129">Next steps</span></span>

<span data-ttu-id="5f84c-130">Essayez de créer votre propre complément ou utilisez script Lab pour essayer des exemples intégrés.</span><span class="sxs-lookup"><span data-stu-id="5f84c-130">Try creating your own add-in or use Script Lab to try built-in samples.</span></span>

### <a name="create-an-office-add-in"></a><span data-ttu-id="5f84c-131">Créer un complément Office</span><span class="sxs-lookup"><span data-stu-id="5f84c-131">Create an Office add-in</span></span>

<span data-ttu-id="5f84c-132">Vous pouvez créer rapidement un complément de base pour Excel, OneNote, Outlook, PowerPoint, Project ou Word en effectuant un [démarrage rapide de 5 minutes](../index.md).</span><span class="sxs-lookup"><span data-stu-id="5f84c-132">You can quickly create a basic add-in for Excel, OneNote, Outlook, PowerPoint, Project, or Word by completing a [5-minute quick start](../index.md).</span></span> <span data-ttu-id="5f84c-133">Si vous avez déjà effectué un démarrage rapide et que vous voulez créer un complément légèrement plus complexe, vous devez essayer le [Didacticiel](../index.md).</span><span class="sxs-lookup"><span data-stu-id="5f84c-133">If you've previously completed a quick start and want to create a slightly more complex add-in, you should try the [tutorial](../index.md).</span></span>

### <a name="explore-the-apis-with-script-lab"></a><span data-ttu-id="5f84c-134">Explorez des API avec Script Lab</span><span class="sxs-lookup"><span data-stu-id="5f84c-134">Explore the APIs with Script Lab</span></span>

<span data-ttu-id="5f84c-135">Explorez la bibliothèque d’exemples intégrés dans [Script Lab](explore-with-script-lab.md) pour avoir une idée des capacités des API JavaScript Office.</span><span class="sxs-lookup"><span data-stu-id="5f84c-135">Explore the library of built-in samples in [Script Lab](explore-with-script-lab.md) to get a sense for the capabilities of the Office JavaScript APIs.</span></span>

## <a name="see-also"></a><span data-ttu-id="5f84c-136">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5f84c-136">See also</span></span>

- [<span data-ttu-id="5f84c-137">Création de compléments Office</span><span class="sxs-lookup"><span data-stu-id="5f84c-137">Building Office Add-ins</span></span>](../overview/office-add-ins-fundamentals.md)
- [<span data-ttu-id="5f84c-138">Concepts de base pour les compléments Office</span><span class="sxs-lookup"><span data-stu-id="5f84c-138">Core concepts for Office Add-ins</span></span>](../overview/core-concepts-office-add-ins.md)
- [<span data-ttu-id="5f84c-139">Développement de compléments Office</span><span class="sxs-lookup"><span data-stu-id="5f84c-139">Develop Office Add-ins</span></span>](../develop/develop-overview.md)
- [<span data-ttu-id="5f84c-140">Concevoir des compléments Office</span><span class="sxs-lookup"><span data-stu-id="5f84c-140">Design Office Add-ins</span></span>](../design/add-in-design.md)
- [<span data-ttu-id="5f84c-141">Test et débogage de compléments Office</span><span class="sxs-lookup"><span data-stu-id="5f84c-141">Test and debug Office Add-ins</span></span>](../testing/test-debug-office-add-ins.md)
- [<span data-ttu-id="5f84c-142">Publish Office Add-ins</span><span class="sxs-lookup"><span data-stu-id="5f84c-142">Publish Office Add-ins</span></span>](../publish/publish.md)