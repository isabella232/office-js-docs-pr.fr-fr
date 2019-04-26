---
title: Explorer l'API JavaScript pour Office à l'aide de script Lab
description: Utilisez script Lab pour explorer l'API Office JS et pour prototyper les fonctionnalités.
ms.topic: article
ms.date: 04/23/2019
localization_priority: Normal
ms.openlocfilehash: 76888716cec8bd1754b7baa22dfcfbe5af984ea5
ms.sourcegitcommit: 9e7b4daa8d76c710b9d9dd4ae2e3c45e8fe07127
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "32640283"
---
# <a name="explore-office-javascript-api-using-script-lab"></a><span data-ttu-id="4bfcc-103">Explorer l'API JavaScript pour Office à l'aide de script Lab</span><span class="sxs-lookup"><span data-stu-id="4bfcc-103">Explore Office JavaScript API using Script Lab</span></span>

<span data-ttu-id="4bfcc-104">Le [complément script Lab](https://store.office.com/app.aspx?assetid=WA104380862), qui est disponible gratuitement à partir de l'Office Store, vous permet d'explorer l'API JavaScript Office pendant que vous travaillez dans un programme Office tel qu'Excel ou Word.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-104">The [Script Lab add-in](https://store.office.com/app.aspx?assetid=WA104380862), which is available free from the Office store, enables you to explore the Office JavaScript API while you are working in an Office program such as Excel or Word.</span></span> <span data-ttu-id="4bfcc-105">Script Lab est un outil pratique à ajouter à votre boîte à outils de développement lorsque vous prototypez et vérifiez les fonctionnalités souhaitées dans votre complément.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-105">Script Lab is a convenient tool to add to your development toolkit as you prototype and verify functionality you want in your add-in.</span></span>

## <a name="what-is-script-lab"></a><span data-ttu-id="4bfcc-106">Qu'est-ce que script Lab?</span><span class="sxs-lookup"><span data-stu-id="4bfcc-106">What is Script Lab?</span></span>

<span data-ttu-id="4bfcc-107">Script Lab est un outil destiné aux utilisateurs qui souhaitent apprendre à développer des compléments Office à l'aide de l'API JavaScript Office dans Excel, Word ou PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-107">Script Lab is a tool for anyone who wants to learn how to develop Office Add-ins using the Office JavaScript API in Excel, Word, or PowerPoint.</span></span> <span data-ttu-id="4bfcc-108">Il fournit IntelliSense afin que vous puissiez voir ce qui est disponible et repose sur l'infrastructure Monaco, la même infrastructure utilisée par Visual Studio code.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-108">It provides IntelliSense so you can see what's available and is built on the Monaco framework, the same framework used by Visual Studio Code.</span></span> <span data-ttu-id="4bfcc-109">Grâce à script Lab, vous pouvez accéder à une bibliothèque d'exemples pour essayer rapidement des fonctionnalités ou vous pouvez choisir un exemple comme base pour votre propre code.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-109">Through Script Lab, you can access a library of samples to quickly try out features or you can choose a sample as the base for your own code.</span></span> <span data-ttu-id="4bfcc-110">Vous pouvez également développer l'exemple de bibliothèque en ajoutant des extraits de code dans la [référentiel Office-js-snippets](https://github.com/OfficeDev/office-js-snippets#office-js-snippets).</span><span class="sxs-lookup"><span data-stu-id="4bfcc-110">You are also welcome to expand the sample library by adding snippets to the [office-js-snippets repo](https://github.com/OfficeDev/office-js-snippets#office-js-snippets).</span></span> <span data-ttu-id="4bfcc-111">Une autre fonctionnalité intéressante de script Lab est une fonctionnalité bêta ou d'aperçu, telle que des [fonctions personnalisées](/office/dev/add-ins/excel/custom-functions-overview) , que vous pouvez essayer.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-111">Another exciting feature of Script Lab is beta or preview functionality like [custom functions](/office/dev/add-ins/excel/custom-functions-overview) is available for you to try.</span></span>

> [!TIP]
> <span data-ttu-id="4bfcc-112">Pour participer à la version bêta ou à l'aperçu, vous devrez peut-être vous inscrire au [programme Office](https://products.office.com/office-insider)Insider.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-112">To participate in beta or preview, you may have to sign up for the [Office Insider program](https://products.office.com/office-insider).</span></span>

<span data-ttu-id="4bfcc-113">Le bruit est-il bien fait?</span><span class="sxs-lookup"><span data-stu-id="4bfcc-113">Sounds good so far?</span></span> <span data-ttu-id="4bfcc-114">Jetez un œil à cette vidéo d'une minute pour voir script Lab en action.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-114">Take a look at this one-minute video to see Script Lab in action.</span></span>

<span data-ttu-id="4bfcc-115">[![Aperçu de la vidéo avec script Lab en cours d'exécution dans Excel, Word et PowerPoint online.] (../images/screenshot-wide-youtube.png 'Vidéo de l'aperçu de script Lab')](https://aka.ms/scriptlabvideo)</span><span class="sxs-lookup"><span data-stu-id="4bfcc-115">[![Preview video showing Script Lab running in Excel, Word, and PowerPoint Online.](../images/screenshot-wide-youtube.png 'Script Lab preview video')](https://aka.ms/scriptlabvideo)</span></span>

## <a name="script-lab-supported-clients"></a><span data-ttu-id="4bfcc-116">Clients de script Lab pris en charge</span><span class="sxs-lookup"><span data-stu-id="4bfcc-116">Script Lab supported clients</span></span>

<span data-ttu-id="4bfcc-117">Le script Lab est pris en charge pour Excel, Word et PowerPoint sur les clients suivants.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-117">Script Lab is supported for Excel, Word, and PowerPoint on the following clients.</span></span>

- <span data-ttu-id="4bfcc-118">Office 365 pour Windows</span><span class="sxs-lookup"><span data-stu-id="4bfcc-118">Office 365 for Windows</span></span>
- <span data-ttu-id="4bfcc-119">Office 365 pour Mac</span><span class="sxs-lookup"><span data-stu-id="4bfcc-119">Office 365 for Mac</span></span>
- <span data-ttu-id="4bfcc-120">Office Online</span><span class="sxs-lookup"><span data-stu-id="4bfcc-120">Office Online</span></span>
- <span data-ttu-id="4bfcc-121">Office 2013 ou version ultérieure pour Windows</span><span class="sxs-lookup"><span data-stu-id="4bfcc-121">Office 2013 or later for Windows</span></span>
- <span data-ttu-id="4bfcc-122">Office 2016 ou version ultérieure pour Mac</span><span class="sxs-lookup"><span data-stu-id="4bfcc-122">Office 2016 or later for Mac</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bfcc-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4bfcc-123">Next steps</span></span>

<span data-ttu-id="4bfcc-124">Lorsque vous êtes prêt à créer votre complément Office, reportez-vous au [démarrage rapide de 5 minutes](/office/dev/add-ins/#5-minute-quick-starts) pour votre application Office par défaut.</span><span class="sxs-lookup"><span data-stu-id="4bfcc-124">When you're ready to create your Office Add-in, see the [5-minute quick start](/office/dev/add-ins/#5-minute-quick-starts) for your preferred Office application.</span></span>

## <a name="see-also"></a><span data-ttu-id="4bfcc-125">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4bfcc-125">See also</span></span>

- [<span data-ttu-id="4bfcc-126">Obtenir un laboratoire de script</span><span class="sxs-lookup"><span data-stu-id="4bfcc-126">Get Script Lab</span></span>](https://store.office.com/app.aspx?assetid=WA104380862)
- [<span data-ttu-id="4bfcc-127">En savoir plus sur script Lab</span><span class="sxs-lookup"><span data-stu-id="4bfcc-127">Learn more about Script Lab</span></span>](https://github.com/OfficeDev/script-lab#script-lab-a-microsoft-garage-project)
- [<span data-ttu-id="4bfcc-128">S'inscrire au programme de développement</span><span class="sxs-lookup"><span data-stu-id="4bfcc-128">Sign up for the dev program</span></span>](https://developer.microsoft.com/office/dev-program)