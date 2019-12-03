---
title: Office. Context. Mailbox. Diagnostics-ensemble de conditions requises 1,8
description: ''
ms.date: 10/30/2019
localization_priority: Normal
ms.openlocfilehash: 8b2d67fbc5eb8462af67a0dc73ce65a433ad5795
ms.sourcegitcommit: e989096f3d19761bf8477c585cde20b3f8e0b90d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2019
ms.locfileid: "37902155"
---
# <a name="diagnostics"></a><span data-ttu-id="14d68-102">diagnostics</span><span class="sxs-lookup"><span data-stu-id="14d68-102">diagnostics</span></span>

### <a name="officeofficemdcontextofficecontextmdmailboxofficecontextmailboxmddiagnostics"></a><span data-ttu-id="14d68-103">[Office](Office.md)[.context](Office.context.md)[.mailbox](Office.context.mailbox.md).diagnostics</span><span class="sxs-lookup"><span data-stu-id="14d68-103">[Office](Office.md)[.context](Office.context.md)[.mailbox](Office.context.mailbox.md).diagnostics</span></span>

<span data-ttu-id="14d68-104">Fournit des informations de diagnostic à un complément Outlook.</span><span class="sxs-lookup"><span data-stu-id="14d68-104">Provides diagnostic information to an Outlook add-in.</span></span>

##### <a name="requirements"></a><span data-ttu-id="14d68-105">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="14d68-105">Requirements</span></span>

|<span data-ttu-id="14d68-106">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="14d68-106">Requirement</span></span>| <span data-ttu-id="14d68-107">Valeur</span><span class="sxs-lookup"><span data-stu-id="14d68-107">Value</span></span>|
|---|---|
|[<span data-ttu-id="14d68-108">Version de l’ensemble minimal de conditions de boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="14d68-108">Minimum mailbox requirement set version</span></span>](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| <span data-ttu-id="14d68-109">1.0</span><span class="sxs-lookup"><span data-stu-id="14d68-109">1.0</span></span>|
|[<span data-ttu-id="14d68-110">Niveau d’autorisation minimal</span><span class="sxs-lookup"><span data-stu-id="14d68-110">Minimum permission level</span></span>](/outlook/add-ins/understanding-outlook-add-in-permissions)| <span data-ttu-id="14d68-111">ReadItem</span><span class="sxs-lookup"><span data-stu-id="14d68-111">ReadItem</span></span>|
|[<span data-ttu-id="14d68-112">Mode Outlook applicable</span><span class="sxs-lookup"><span data-stu-id="14d68-112">Applicable Outlook mode</span></span>](/outlook/add-ins/#extension-points)| <span data-ttu-id="14d68-113">Rédaction ou lecture</span><span class="sxs-lookup"><span data-stu-id="14d68-113">Compose or Read</span></span>|

##### <a name="members-and-methods"></a><span data-ttu-id="14d68-114">Membres et méthodes</span><span class="sxs-lookup"><span data-stu-id="14d68-114">Members and methods</span></span>

| <span data-ttu-id="14d68-115">Membre</span><span class="sxs-lookup"><span data-stu-id="14d68-115">Member</span></span> | <span data-ttu-id="14d68-116">Type</span><span class="sxs-lookup"><span data-stu-id="14d68-116">Type</span></span> |
|--------|------|
| [<span data-ttu-id="14d68-117">Nom-d’hôte</span><span class="sxs-lookup"><span data-stu-id="14d68-117">hostName</span></span>](#hostname-string) | <span data-ttu-id="14d68-118">Membre</span><span class="sxs-lookup"><span data-stu-id="14d68-118">Member</span></span> |
| [<span data-ttu-id="14d68-119">hostVersion</span><span class="sxs-lookup"><span data-stu-id="14d68-119">hostVersion</span></span>](#hostversion-string) | <span data-ttu-id="14d68-120">Membre</span><span class="sxs-lookup"><span data-stu-id="14d68-120">Member</span></span> |
| [<span data-ttu-id="14d68-121">OWAView</span><span class="sxs-lookup"><span data-stu-id="14d68-121">OWAView</span></span>](#owaview-string) | <span data-ttu-id="14d68-122">Membre</span><span class="sxs-lookup"><span data-stu-id="14d68-122">Member</span></span> |

### <a name="members"></a><span data-ttu-id="14d68-123">Membres</span><span class="sxs-lookup"><span data-stu-id="14d68-123">Members</span></span>

#### <a name="hostname-string"></a><span data-ttu-id="14d68-124">NomHôte : chaîne</span><span class="sxs-lookup"><span data-stu-id="14d68-124">hostName: String</span></span>

<span data-ttu-id="14d68-125">Obtient une chaîne qui représente le nom de l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="14d68-125">Gets a string that represents the name of the host application.</span></span>

<span data-ttu-id="14d68-126">Chaîne qui peut avoir l’une des valeurs suivantes : `Outlook`, `OutlookWebApp`, `OutlookIOS` ou `OutlookAndroid`.</span><span class="sxs-lookup"><span data-stu-id="14d68-126">A string that can be one of the following values: `Outlook`, `OutlookWebApp`, `OutlookIOS`, or `OutlookAndroid`.</span></span>

> [!NOTE]
> <span data-ttu-id="14d68-127">La `Outlook` valeur est renvoyée pour Outlook sur les clients de bureau (par exemple, Windows et Mac).</span><span class="sxs-lookup"><span data-stu-id="14d68-127">The `Outlook` value is returned for Outlook on desktop clients (i.e., Windows and Mac).</span></span>

##### <a name="type"></a><span data-ttu-id="14d68-128">Type</span><span class="sxs-lookup"><span data-stu-id="14d68-128">Type</span></span>

*   <span data-ttu-id="14d68-129">String</span><span class="sxs-lookup"><span data-stu-id="14d68-129">String</span></span>

##### <a name="requirements"></a><span data-ttu-id="14d68-130">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="14d68-130">Requirements</span></span>

|<span data-ttu-id="14d68-131">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="14d68-131">Requirement</span></span>| <span data-ttu-id="14d68-132">Valeur</span><span class="sxs-lookup"><span data-stu-id="14d68-132">Value</span></span>|
|---|---|
|[<span data-ttu-id="14d68-133">Version de l’ensemble minimal de conditions de boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="14d68-133">Minimum mailbox requirement set version</span></span>](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| <span data-ttu-id="14d68-134">1.0</span><span class="sxs-lookup"><span data-stu-id="14d68-134">1.0</span></span>|
|[<span data-ttu-id="14d68-135">Niveau d’autorisation minimal</span><span class="sxs-lookup"><span data-stu-id="14d68-135">Minimum permission level</span></span>](/outlook/add-ins/understanding-outlook-add-in-permissions)| <span data-ttu-id="14d68-136">ReadItem</span><span class="sxs-lookup"><span data-stu-id="14d68-136">ReadItem</span></span>|
|[<span data-ttu-id="14d68-137">Mode Outlook applicable</span><span class="sxs-lookup"><span data-stu-id="14d68-137">Applicable Outlook mode</span></span>](/outlook/add-ins/#extension-points)| <span data-ttu-id="14d68-138">Rédaction ou lecture</span><span class="sxs-lookup"><span data-stu-id="14d68-138">Compose or Read</span></span>|

<br>

---
---

#### <a name="hostversion-string"></a><span data-ttu-id="14d68-139">hostVersion : chaîne</span><span class="sxs-lookup"><span data-stu-id="14d68-139">hostVersion: String</span></span>

<span data-ttu-id="14d68-140">Obtient une valeur de type String qui représente la version de l’application hôte ou du serveur Exchange (par exemple, « 15.0.468.0 »).</span><span class="sxs-lookup"><span data-stu-id="14d68-140">Gets a string that represents the version of either the host application or the Exchange Server (e.g., "15.0.468.0").</span></span>

<span data-ttu-id="14d68-141">Si le complément de messagerie est en cours d’exécution sur le client de bureau Outlook ou sur `hostVersion` iOS, la propriété renvoie la version de l’application hôte, Outlook.</span><span class="sxs-lookup"><span data-stu-id="14d68-141">If the mail add-in is running on the Outlook desktop client or on iOS, the `hostVersion` property returns the version of the host application, Outlook.</span></span> <span data-ttu-id="14d68-142">Dans Outlook sur le Web, la propriété renvoie la version du serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="14d68-142">In Outlook on the web, the property returns the version of the Exchange Server.</span></span>

##### <a name="type"></a><span data-ttu-id="14d68-143">Type</span><span class="sxs-lookup"><span data-stu-id="14d68-143">Type</span></span>

*   <span data-ttu-id="14d68-144">String</span><span class="sxs-lookup"><span data-stu-id="14d68-144">String</span></span>

##### <a name="requirements"></a><span data-ttu-id="14d68-145">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="14d68-145">Requirements</span></span>

|<span data-ttu-id="14d68-146">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="14d68-146">Requirement</span></span>| <span data-ttu-id="14d68-147">Valeur</span><span class="sxs-lookup"><span data-stu-id="14d68-147">Value</span></span>|
|---|---|
|[<span data-ttu-id="14d68-148">Version de l’ensemble minimal de conditions de boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="14d68-148">Minimum mailbox requirement set version</span></span>](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| <span data-ttu-id="14d68-149">1.0</span><span class="sxs-lookup"><span data-stu-id="14d68-149">1.0</span></span>|
|[<span data-ttu-id="14d68-150">Niveau d’autorisation minimal</span><span class="sxs-lookup"><span data-stu-id="14d68-150">Minimum permission level</span></span>](/outlook/add-ins/understanding-outlook-add-in-permissions)| <span data-ttu-id="14d68-151">ReadItem</span><span class="sxs-lookup"><span data-stu-id="14d68-151">ReadItem</span></span>|
|[<span data-ttu-id="14d68-152">Mode Outlook applicable</span><span class="sxs-lookup"><span data-stu-id="14d68-152">Applicable Outlook mode</span></span>](/outlook/add-ins/#extension-points)| <span data-ttu-id="14d68-153">Rédaction ou lecture</span><span class="sxs-lookup"><span data-stu-id="14d68-153">Compose or Read</span></span>|

<br>

---
---

#### <a name="owaview-string"></a><span data-ttu-id="14d68-154">OWAView : chaîne</span><span class="sxs-lookup"><span data-stu-id="14d68-154">OWAView: String</span></span>

<span data-ttu-id="14d68-155">Obtient une valeur de type String qui représente l’affichage actuel d’Outlook sur le Web.</span><span class="sxs-lookup"><span data-stu-id="14d68-155">Gets a string that represents the current view of Outlook on the web.</span></span>

<span data-ttu-id="14d68-156">La chaîne renvoyée peut avoir une des valeurs suivantes : `OneColumn`, `TwoColumns`, ou `ThreeColumns`.</span><span class="sxs-lookup"><span data-stu-id="14d68-156">The returned string can be one of the following values: `OneColumn`, `TwoColumns`, or `ThreeColumns`.</span></span>

<span data-ttu-id="14d68-157">Si l’application hôte n’est pas Outlook sur le Web, l’accès à cette propriété génère `undefined`.</span><span class="sxs-lookup"><span data-stu-id="14d68-157">If the host application is not Outlook on the web, then accessing this property results in `undefined`.</span></span>

<span data-ttu-id="14d68-158">Outlook sur le Web possède trois modes d’affichage qui correspondent à la largeur de l’écran et de la fenêtre, ainsi qu’au nombre de colonnes pouvant être affichées :</span><span class="sxs-lookup"><span data-stu-id="14d68-158">Outlook on the web has three views that correspond to the width of the screen and the window, and the number of columns that can be displayed:</span></span>

*   <span data-ttu-id="14d68-159">`OneColumn`, qui est affiché lorsque l’écran est étroit.</span><span class="sxs-lookup"><span data-stu-id="14d68-159">`OneColumn`, which is displayed when the screen is narrow.</span></span> <span data-ttu-id="14d68-160">Outlook sur le Web utilise cette disposition sur une seule colonne sur la totalité de l’écran d’un smartphone.</span><span class="sxs-lookup"><span data-stu-id="14d68-160">Outlook on the web uses this single-column layout on the entire screen of a smartphone.</span></span>
*   <span data-ttu-id="14d68-161">`TwoColumns`, qui est affiché lorsque l’écran est plus large.</span><span class="sxs-lookup"><span data-stu-id="14d68-161">`TwoColumns`, which is displayed when the screen is wider.</span></span> <span data-ttu-id="14d68-162">Outlook sur le Web utilise cet affichage sur la plupart des tablettes.</span><span class="sxs-lookup"><span data-stu-id="14d68-162">Outlook on the web uses this view on most tablets.</span></span>
*   <span data-ttu-id="14d68-163">`ThreeColumns`, qui est affiché lorsque l’écran est large.</span><span class="sxs-lookup"><span data-stu-id="14d68-163">`ThreeColumns`, which is displayed when the screen is wide.</span></span> <span data-ttu-id="14d68-164">Par exemple, Outlook sur le Web utilise cet affichage dans une fenêtre plein écran sur un ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="14d68-164">For example, Outlook on the web uses this view in a full screen window on a desktop computer.</span></span>

##### <a name="type"></a><span data-ttu-id="14d68-165">Type</span><span class="sxs-lookup"><span data-stu-id="14d68-165">Type</span></span>

*   <span data-ttu-id="14d68-166">String</span><span class="sxs-lookup"><span data-stu-id="14d68-166">String</span></span>

##### <a name="requirements"></a><span data-ttu-id="14d68-167">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="14d68-167">Requirements</span></span>

|<span data-ttu-id="14d68-168">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="14d68-168">Requirement</span></span>| <span data-ttu-id="14d68-169">Valeur</span><span class="sxs-lookup"><span data-stu-id="14d68-169">Value</span></span>|
|---|---|
|[<span data-ttu-id="14d68-170">Version de l’ensemble minimal de conditions de boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="14d68-170">Minimum mailbox requirement set version</span></span>](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| <span data-ttu-id="14d68-171">1.0</span><span class="sxs-lookup"><span data-stu-id="14d68-171">1.0</span></span>|
|[<span data-ttu-id="14d68-172">Niveau d’autorisation minimal</span><span class="sxs-lookup"><span data-stu-id="14d68-172">Minimum permission level</span></span>](/outlook/add-ins/understanding-outlook-add-in-permissions)| <span data-ttu-id="14d68-173">ReadItem</span><span class="sxs-lookup"><span data-stu-id="14d68-173">ReadItem</span></span>|
|[<span data-ttu-id="14d68-174">Mode Outlook applicable</span><span class="sxs-lookup"><span data-stu-id="14d68-174">Applicable Outlook mode</span></span>](/outlook/add-ins/#extension-points)| <span data-ttu-id="14d68-175">Rédaction ou lecture</span><span class="sxs-lookup"><span data-stu-id="14d68-175">Compose or Read</span></span>|