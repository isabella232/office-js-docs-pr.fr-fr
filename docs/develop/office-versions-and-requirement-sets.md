---
title: Versions d’Office et ensembles de conditions requises
description: ''
ms.date: 03/29/2018
ms.openlocfilehash: fe02a63e93bd7fbb8a2709b1e3977fee999e5b9a
ms.sourcegitcommit: c72c35e8389c47a795afbac1b2bcf98c8e216d82
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2018
ms.locfileid: "19437576"
---
# <a name="office-versions-and-requirement-sets"></a><span data-ttu-id="8180c-102">Versions d’Office et ensembles de conditions requises</span><span class="sxs-lookup"><span data-stu-id="8180c-102">Office versions and requirement sets</span></span>

<span data-ttu-id="8180c-103">Il existe de nombreuses versions d’Office sur plusieurs plateformes, celles-ci ne prenant pas forcément en charge toutes les API dans l’interface API JavaScript pour Office (Office.js).</span><span class="sxs-lookup"><span data-stu-id="8180c-103">There are many versions of Office on several platforms, and they don't all support every API in Office JavaScript API (Office.js).</span></span> <span data-ttu-id="8180c-104">Vous n’avez pas toujours le contrôle sur la version d’Office que vos utilisateurs ont installée.</span><span class="sxs-lookup"><span data-stu-id="8180c-104">You may not always have control over the version of Office your users have installed.</span></span>  <span data-ttu-id="8180c-105">Pour gérer cette situation, nous fournissons un système nommé ensembles de conditions requises pour vous aider à déterminer si un hôte Office prend en charge les fonctionnalités dont vous avez besoin dans votre complément Office.</span><span class="sxs-lookup"><span data-stu-id="8180c-105">To handle this situation, we provide a system called requirement sets to help you determine whether an Office host supports the capabilities you need in your Office Add-in.</span></span> 

> [!NOTE]
> - <span data-ttu-id="8180c-106">Office peut être exécuté sur plusieurs plateformes, notamment Office pour Windows, Office Online, Office pour Mac et Office pour iPad.</span><span class="sxs-lookup"><span data-stu-id="8180c-106">Office runs across multiple platforms, including Office for Windows, Office Online, Office for the Mac, and Office for the iPad.</span></span>  
> - <span data-ttu-id="8180c-107">Parmi les hôtes Office, voici quelques exemples de produits Office : Excel, Word, PowerPoint, Outlook, OneNote et autres.</span><span class="sxs-lookup"><span data-stu-id="8180c-107">Examples of Office hosts are Office Products: Excel, Word, PowerPoint, Outlook, OneNote, and so forth.</span></span>  
> - <span data-ttu-id="8180c-108">Un ensemble de conditions requises est un groupe nommé de membres d’API, par exemple : `ExcelApi 1.5`, `WordApi 1.3`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="8180c-108">A requirement set is a named group of API members e.g., `ExcelApi 1.5`, `WordApi 1.3`, and so on.</span></span>  


## <a name="how-to-check-your-office-version"></a><span data-ttu-id="8180c-109">Vérification de votre version d’Office</span><span class="sxs-lookup"><span data-stu-id="8180c-109">How to check your Office version</span></span>

<span data-ttu-id="8180c-110">Pour identifier la version d’Office que vous utilisez, à partir d’une application Office, sélectionnez le menu **Fichier**, puis sélectionnez **Compte**.</span><span class="sxs-lookup"><span data-stu-id="8180c-110">To identify the Office version that you're using, from within an Office application, select the **File** menu, and then choose **Account**.</span></span> <span data-ttu-id="8180c-111">La version d’Office s’affiche dans la section **Informations sur le produit**.</span><span class="sxs-lookup"><span data-stu-id="8180c-111">The version of Office will appear in the **Product Information** section.</span></span> <span data-ttu-id="8180c-112">Par exemple, la capture d’écran suivante indique la version 1802 d’Office (build 9026.1000) :</span><span class="sxs-lookup"><span data-stu-id="8180c-112">For example, the following screenshot indicates Office Version 1802 (Build 9026.1000):</span></span>

![Vérification de votre version d’Office](../images/office-version-number-ui.jpg)


## <a name="office-requirement-sets-availability"></a><span data-ttu-id="8180c-114">Disponibilité des ensembles de conditions requises Office</span><span class="sxs-lookup"><span data-stu-id="8180c-114">Office requirement sets availability</span></span>

<span data-ttu-id="8180c-115">Les compléments Office peuvent utiliser des ensembles de conditions requises d’API pour déterminer si l’hôte Office prend en charge les membres d’API nécessaires.</span><span class="sxs-lookup"><span data-stu-id="8180c-115">Office Add-ins can use API requirement sets to determine whether the Office host supports the API members that it need to use.</span></span> <span data-ttu-id="8180c-116">La prise en charge des ensembles de conditions requises varie selon l’hôte Office et la version de ce dernier (voir la section précédente).</span><span class="sxs-lookup"><span data-stu-id="8180c-116">Requirement set support varies by Office host and the Office host version (see previous section).</span></span>

<span data-ttu-id="8180c-117">Certains hôtes Office ont leurs propres ensembles de conditions requises d’API.</span><span class="sxs-lookup"><span data-stu-id="8180c-117">Some Office hosts have their own API requirement sets.</span></span> <span data-ttu-id="8180c-118">Par exemple, le premier ensemble de conditions requises pour l’API Excel était `ExcelApi 1.1` et le premier ensemble de conditions requises pour l’API Word était `WordApi 1.1`.</span><span class="sxs-lookup"><span data-stu-id="8180c-118">For example, the first requirement set for the Excel API was `ExcelApi 1.1` and the first requirement set for the Word API was `WordApi 1.1`.</span></span> <span data-ttu-id="8180c-119">Depuis lors, de nombreux ensembles de conditions requises d’API Excel et d’API Word ont été ajoutés pour proposer des fonctionnalités d’API supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8180c-119">Since then, multiple new ExcelApi requirement sets and WordApi requirement sets have been added to provide additional API functionality.</span></span>

<span data-ttu-id="8180c-120">Par ailleurs, d’autres fonctionnalités telles que les commandes de complément (extensibilité du ruban) et la possibilité de lancer des boîtes de dialogue (API de boîte de dialogue) ont été ajoutées à l’API commune.</span><span class="sxs-lookup"><span data-stu-id="8180c-120">In addition, other functionality such as add-in commands (ribbon extensibility) and the ability to launch dialog boxes (Dialog API) were added to the common API.</span></span> <span data-ttu-id="8180c-121">Les commandes de complément et les ensembles de conditions requises d’API de boîte de dialogue sont des exemples d’ensembles de conditions requises d’API que les différents hôtes Office ont en commun.</span><span class="sxs-lookup"><span data-stu-id="8180c-121">Add-in commands and Dialog API requirement sets are examples of API sets that the various Office hosts share in common.</span></span>

<span data-ttu-id="8180c-122">Un complément peut utiliser uniquement des API dans les ensembles de conditions requises qui sont prises en charge par la version de l’hôte Office sur lequel le complément est exécuté.</span><span class="sxs-lookup"><span data-stu-id="8180c-122">An add-in can only use APIs in requirement sets that are supported by the version of Office host where the add-in is running.</span></span> <span data-ttu-id="8180c-123">Pour savoir exactement quels ensembles de conditions requises sont disponibles pour une version spécifique de l’hôte Office, reportez-vous aux articles suivants sur les ensembles de conditions requises propres aux hôtes :</span><span class="sxs-lookup"><span data-stu-id="8180c-123">To know exactly which requirement sets are available for a specific Office host version, refer to the following host-specific requirement set articles:</span></span>

- <span data-ttu-id="8180c-124">[Ensembles de conditions requises de l’API JavaScript pour Excel](https://dev.office.com/reference/add-ins/requirement-sets/excel-api-requirement-sets?product=excel) (ExcelApi)</span><span class="sxs-lookup"><span data-stu-id="8180c-124">[Excel JavaScript API requirement sets](https://dev.office.com/reference/add-ins/requirement-sets/excel-api-requirement-sets?product=excel) (ExcelApi)</span></span>
- <span data-ttu-id="8180c-125">[Ensembles de conditions requises de l’API JavaScript pour Word](https://dev.office.com/reference/add-ins/requirement-sets/word-api-requirement-sets) (WordApi)</span><span class="sxs-lookup"><span data-stu-id="8180c-125">[Word JavaScript API requirement sets](https://dev.office.com/reference/add-ins/requirement-sets/word-api-requirement-sets) (WordApi)</span></span>
- <span data-ttu-id="8180c-126">[Ensembles de conditions requises de l’API JavaScript pour OneNote](https://dev.office.com/reference/add-ins/requirement-sets/onenote-api-requirement-sets) (OneNoteApi)</span><span class="sxs-lookup"><span data-stu-id="8180c-126">[OneNote JavaScript API requirement sets](https://dev.office.com/reference/add-ins/requirement-sets/onenote-api-requirement-sets) (OneNoteApi)</span></span>
- <span data-ttu-id="8180c-127">[Présentation de l’ensemble de conditions requises pour les API Outlook](https://dev.office.com/reference/add-ins/outlook/tutorial-api-requirement-sets) (MailBox)</span><span class="sxs-lookup"><span data-stu-id="8180c-127">[Understanding Outlook API requirement sets](https://dev.office.com/reference/add-ins/outlook/tutorial-api-requirement-sets) (MailBox)</span></span>

<span data-ttu-id="8180c-128">Certains ensembles de conditions requises contiennent des API qui peuvent être utilisées par n’importe quel hôte Office.</span><span class="sxs-lookup"><span data-stu-id="8180c-128">Some requirement sets contain APIs that can be used by any Office host.</span></span> <span data-ttu-id="8180c-129">Pour plus d’informations sur ces ensembles de conditions requises, reportez-vous aux articles suivants :</span><span class="sxs-lookup"><span data-stu-id="8180c-129">For information about these requirement sets, refer to the following articles:</span></span>

- [<span data-ttu-id="8180c-130">Ensembles de conditions requises communes pour Office</span><span class="sxs-lookup"><span data-stu-id="8180c-130">Office common requirement sets</span></span>](https://dev.office.com/reference/add-ins/requirement-sets/office-add-in-requirement-sets)
- [<span data-ttu-id="8180c-131">Ensembles de conditions requises concernant les commandes de complément</span><span class="sxs-lookup"><span data-stu-id="8180c-131">Add-in commands requirement sets</span></span>](https://dev.office.com/reference/add-ins/requirement-sets/add-in-commands-requirement-sets?product=excel)
- [<span data-ttu-id="8180c-132">Ensembles de conditions requises de l’API de boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="8180c-132">Dialog API requirement sets</span></span>](https://dev.office.com/reference/add-ins/requirement-sets/dialog-api-requirement-sets?product=excel)
- [<span data-ttu-id="8180c-133">Ensembles de conditions requises de l’API d’identité</span><span class="sxs-lookup"><span data-stu-id="8180c-133">Identity API requirement sets</span></span>](https://dev.office.com/reference/add-ins/requirement-sets/identity-api-requirement-sets?product=excel)

<span data-ttu-id="8180c-134">Le numéro de version d’un ensemble de conditions requises, par exemple « 1.1 » dans `ExcelApi 1.1`, est défini par rapport à l’hôte d’Office.</span><span class="sxs-lookup"><span data-stu-id="8180c-134">The version number of a requirement set, such as the "1.1" in `ExcelApi 1.1`, is relative to the Office host.</span></span> <span data-ttu-id="8180c-135">Le numéro de version d’un ensemble donné de conditions requises (par exemple, `ExcelApi 1.1`) ne correspond pas au numéro de version d’Office.js, ni aux ensembles de conditions requises pour d’autres hôtes Office (comme Word, Outlook, etc.).</span><span class="sxs-lookup"><span data-stu-id="8180c-135">The version number of a given requirement set (e.g., `ExcelApi 1.1`) does not correspond to the version number of Office.js or to requirement sets for other Office hosts (e.g., Word, Outlook, etc.).</span></span>  <span data-ttu-id="8180c-136">Les ensembles de conditions requises pour les différents hôtes Office sont publiés à des moments et à des rythmes différents.</span><span class="sxs-lookup"><span data-stu-id="8180c-136">Requirement sets for the different Office hosts are released at different speeds and times.</span></span> <span data-ttu-id="8180c-137">Par exemple, `ExcelApi 1.5` a été publié avant l’ensemble de conditions requises `WordApi 1.3`.</span><span class="sxs-lookup"><span data-stu-id="8180c-137">For example, `ExcelApi 1.5` was released before the `WordApi 1.3` requirement set.</span></span>

<span data-ttu-id="8180c-138">L’API JavaScript pour la bibliothèque Office (Office.js) inclut tous les ensembles de conditions requises actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="8180c-138">The JavaScript API for Office library (Office.js) includes all requirement sets that are currently available.</span></span> <span data-ttu-id="8180c-139">Alors qu’il existe des ensembles de conditions requises `ExcelApi 1.3` et `WordApi 1.3`, il n’existe pas d’ensemble de conditions requises `Office.js 1.3`.</span><span class="sxs-lookup"><span data-stu-id="8180c-139">While there is such a thing as requirement sets `ExcelApi 1.3` and `WordApi 1.3`, there is no `Office.js 1.3` requirement set.</span></span> <span data-ttu-id="8180c-140">La dernière version d’Office.js est gérée comme un point de terminaison Office unique remis via le réseau de distribution de contenu (CDN).</span><span class="sxs-lookup"><span data-stu-id="8180c-140">The latest release of Office.js is maintained as a single Office endpoint delivered via the content delivery network (CDN).</span></span> <span data-ttu-id="8180c-141">Pour plus d’informations sur le CDN Office.js, notamment sur la gestion des versions et de la compatibilité avec les anciennes versions, reportez-vous à l’article [Présentation de l’interface API JavaScript pour Office](https://docs.microsoft.com/en-us/office/dev/add-ins/develop/understanding-the-javascript-api-for-office).</span><span class="sxs-lookup"><span data-stu-id="8180c-141">For more details around the Office.js CDN, including how versioning and backward compatability is handled, see [Understanding the JavaScript API for Office](https://docs.microsoft.com/en-us/office/dev/add-ins/develop/understanding-the-javascript-api-for-office).</span></span>

## <a name="specify-office-hosts-and-requirement-sets"></a><span data-ttu-id="8180c-142">Spécification des ensembles de conditions requises et des hôtes Office</span><span class="sxs-lookup"><span data-stu-id="8180c-142">Specify Office hosts and requirement sets</span></span>

<span data-ttu-id="8180c-143">Il existe différentes méthodes pour spécifier les hôtes Office et les ensembles de conditions qui sont requis par un complément.</span><span class="sxs-lookup"><span data-stu-id="8180c-143">There are various ways to specify which Office hosts and requirement sets are required by an add-in.</span></span>  <span data-ttu-id="8180c-144">Pour plus d’informations, consultez la rubrique [Spécifier les hôtes Office et la configuration requise d’API](https://docs.microsoft.com/en-us/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements).</span><span class="sxs-lookup"><span data-stu-id="8180c-144">For detailed information, see [Specify Office hosts and API requirements](https://docs.microsoft.com/en-us/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements)</span></span>


## <a name="see-also"></a><span data-ttu-id="8180c-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8180c-145">See also</span></span>

- [<span data-ttu-id="8180c-146">Spécification des exigences en matière d’hôtes Office et d’API</span><span class="sxs-lookup"><span data-stu-id="8180c-146">Specify Office hosts and API requirements</span></span>](https://docs.microsoft.com/en-us/office/dev/add-ins/develop/specify-office-hosts-and-api-requirements)
- [<span data-ttu-id="8180c-147">Installer la dernière version d’Office</span><span class="sxs-lookup"><span data-stu-id="8180c-147">Install the latest version of Office</span></span>](https://docs.microsoft.com/en-us/office/dev/add-ins/develop/install-latest-office-version)
- [<span data-ttu-id="8180c-148">Présentation des canaux de mise à jour pour Office 365 ProPlus</span><span class="sxs-lookup"><span data-stu-id="8180c-148">Overview of update channels for Office 365 ProPlus</span></span>](https://docs.microsoft.com/en-us/deployoffice/overview-of-update-channels-for-office-365-proplus)
- [<span data-ttu-id="8180c-149">Tirez le meilleur parti d’Office avec Office 365</span><span class="sxs-lookup"><span data-stu-id="8180c-149">Get the most from Office with Office 365</span></span>](https://products.office.com/en-us/compare-all-microsoft-office-products?tab=2)