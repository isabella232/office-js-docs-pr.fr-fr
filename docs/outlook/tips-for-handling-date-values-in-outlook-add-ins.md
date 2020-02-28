---
title: Gestion des valeurs de date dans les compléments Outlook
description: L’API JavaScript pour Office utilise l’objet JavaScript date pour la plupart du stockage et de l’extraction des dates et des heures.
ms.date: 10/31/2019
localization_priority: Normal
ms.openlocfilehash: 2d92f32f488cba1c9220296936468ca93dd320e3
ms.sourcegitcommit: 5d29801180f6939ec10efb778d2311be67d8b9f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2020
ms.locfileid: "42325332"
---
# <a name="tips-for-handling-date-values-in-outlook-add-ins"></a><span data-ttu-id="b21d8-103">Conseils pour la gestion des valeurs de date dans les compléments Outlook</span><span class="sxs-lookup"><span data-stu-id="b21d8-103">Tips for handling date values in Outlook add-ins</span></span>

<span data-ttu-id="b21d8-104">L’API JavaScript pour Office utilise l’objet JavaScript [Date](https://www.w3schools.com/jsref/jsref_obj_date.asp) pour la plupart du stockage et de l’extraction des dates et des heures.</span><span class="sxs-lookup"><span data-stu-id="b21d8-104">The Office JavaScript API uses the JavaScript [Date](https://www.w3schools.com/jsref/jsref_obj_date.asp) object for most of the storage and retrieval of dates and times.</span></span> 

<span data-ttu-id="b21d8-105">Cet `Date` objet fournit des méthodes telles que [getUTCDate](https://www.w3schools.com/jsref/jsref_getutcdate.asp), [getUTCHour](https://www.w3schools.com/jsref/jsref_getutchours.asp), [getUTCMinutes](https://www.w3schools.com/jsref/jsref_getutcminutes.asp)et [toUTCString](https://www.w3schools.com/jsref/jsref_toutcstring.asp), qui renvoient la date ou l’heure demandée en fonction de l’heure UTC (Universal Coordinated Time).</span><span class="sxs-lookup"><span data-stu-id="b21d8-105">That `Date` object provides methods such as [getUTCDate](https://www.w3schools.com/jsref/jsref_getutcdate.asp), [getUTCHour](https://www.w3schools.com/jsref/jsref_getutchours.asp), [getUTCMinutes](https://www.w3schools.com/jsref/jsref_getutcminutes.asp), and [toUTCString](https://www.w3schools.com/jsref/jsref_toutcstring.asp), which return the requested date or time value according to Universal Coordinated Time (UTC) time.</span></span>

<span data-ttu-id="b21d8-106">L' `Date` objet fournit également d’autres méthodes telles que [GETDATE](https://www.w3schools.com/jsref/jsref_getutcdate.asp), [getHour](https://www.w3schools.com/jsref/jsref_getutchours.asp), [getMinutes](https://www.w3schools.com/jsref/jsref_getminutes.asp)et [ToString](https://www.w3schools.com/jsref/jsref_tostring_date.asp), qui renvoient la date ou l’heure demandée en heure locale.</span><span class="sxs-lookup"><span data-stu-id="b21d8-106">The `Date` object also provides other methods such as [getDate](https://www.w3schools.com/jsref/jsref_getutcdate.asp), [getHour](https://www.w3schools.com/jsref/jsref_getutchours.asp), [getMinutes](https://www.w3schools.com/jsref/jsref_getminutes.asp), and [toString](https://www.w3schools.com/jsref/jsref_tostring_date.asp), which return the requested date or time according to "local time".</span></span>

<span data-ttu-id="b21d8-107">Le concept d’« heure locale » est principalement déterminé par le navigateur et le système d’exploitation de l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="b21d8-107">The concept of "local time" is largely determined by the browser and operating system on the client computer.</span></span> <span data-ttu-id="b21d8-108">Par exemple, dans la plupart des navigateurs qui s’exécutent sur un ordinateur client Windows, un `getDate`appel JavaScript à, renvoie une date basée sur le fuseau horaire défini dans Windows sur l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="b21d8-108">For instance, on most browsers running on a Windows-based client computer, a JavaScript call to `getDate`, returns a date based on the time zone set in Windows on the client computer.</span></span>

<span data-ttu-id="b21d8-109">L’exemple suivant crée un `Date` objet `myLocalDate` en heure locale, et appelle `toUTCString` pour convertir cette date en une chaîne de date au format UTC.</span><span class="sxs-lookup"><span data-stu-id="b21d8-109">The following example creates a `Date` object `myLocalDate` in local time, and calls `toUTCString` to convert that date to a date string in UTC.</span></span>

```js
// Create and get the current date represented 
// in the client computer time zone.
var myLocalDate = new Date (); 

// Convert the Date value in the client computer time zone
// to a date string in UTC, and display the string.
document.write ("The current UTC time is " + 
    myLocalDate.toUTCString());
```

<span data-ttu-id="b21d8-110">Bien que vous puissiez utiliser l' `Date` objet JavaScript pour obtenir une valeur de date ou d’heure basée sur UTC ou sur le fuseau horaire de l’ordinateur client, l’objet **Date** est limité à un égard : il ne fournit pas de méthode pour renvoyer une valeur de date ou d’heure pour un autre fuseau horaire spécifique.</span><span class="sxs-lookup"><span data-stu-id="b21d8-110">While you can use the JavaScript `Date` object to get a date or time value based on UTC or the client computer time zone, the **Date** object is limited in one respect - it does not provide methods to return a date or time value for any other specific time zone.</span></span> <span data-ttu-id="b21d8-111">Par exemple, si votre ordinateur client est défini sur l’heure de l’est (est), il n’existe `Date` pas de méthode qui vous permet d’obtenir la valeur horaire autre que est ou UTC, telle que Pacifique (PST).</span><span class="sxs-lookup"><span data-stu-id="b21d8-111">For example, if your client computer is set to be on Eastern Standard Time (EST), there is no `Date` method that allows you to get the hour value other than in EST or UTC, such as Pacific Standard Time (PST).</span></span>


## <a name="date-related-features-for-outlook-add-ins"></a><span data-ttu-id="b21d8-112">Fonctionnalités liées à la date pour les compléments Outlook</span><span class="sxs-lookup"><span data-stu-id="b21d8-112">Date-related features for Outlook add-ins</span></span>

<span data-ttu-id="b21d8-113">La limitation JavaScript susmentionnée a une implication pour vous, lorsque vous utilisez l’API JavaScript pour Office pour gérer les valeurs de date ou d’heure dans les compléments Outlook qui s’exécutent dans un client riche Outlook, et dans Outlook sur le Web ou les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="b21d8-113">The aforementioned JavaScript limitation has an implication for you, when you use the Office JavaScript API to handle date or time values in Outlook add-ins that run in an Outlook rich client, and in Outlook on the web or mobile devices.</span></span>


### <a name="time-zones-for-outlook-clients"></a><span data-ttu-id="b21d8-114">Fuseaux horaires pour les clients Outlook</span><span class="sxs-lookup"><span data-stu-id="b21d8-114">Time zones for Outlook clients</span></span>

<span data-ttu-id="b21d8-115">Pour clarifier les choses, définissons les fuseaux horaires en question.</span><span class="sxs-lookup"><span data-stu-id="b21d8-115">For clarity, let's define the time zones in question.</span></span>

|<span data-ttu-id="b21d8-116">**Fuseau horaire**</span><span class="sxs-lookup"><span data-stu-id="b21d8-116">**Time zone**</span></span>|<span data-ttu-id="b21d8-117">**Description**</span><span class="sxs-lookup"><span data-stu-id="b21d8-117">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="b21d8-118">Fuseau horaire de l’ordinateur client</span><span class="sxs-lookup"><span data-stu-id="b21d8-118">Client computer time zone</span></span>|<span data-ttu-id="b21d8-119">Cette valeur est définie sur le système d’exploitation de l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="b21d8-119">This is set on the operating system of the client computer.</span></span> <span data-ttu-id="b21d8-120">La plupart des navigateurs utilisent le fuseau horaire de l’ordinateur client pour afficher les valeurs de `Date` date ou d’heure de l’objet JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b21d8-120">Most browsers use the client computer time zone to display date or time values of the JavaScript `Date` object.</span></span><br/><br/><span data-ttu-id="b21d8-121">Le client riche Outlook utilise ce fuseau horaire pour afficher les valeurs de date ou d’heure dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b21d8-121">An Outlook rich client uses this time zone to display date or time values in the user interface.</span></span> <br/><br/><span data-ttu-id="b21d8-122">Par exemple, sur un ordinateur client exécutant Windows, Outlook utilise le fuseau horaire défini sur Windows comme fuseau horaire local.</span><span class="sxs-lookup"><span data-stu-id="b21d8-122">For example, on a client computer running Windows, Outlook uses the time zone set on Windows as the local time zone.</span></span> <span data-ttu-id="b21d8-123">Sur Mac, si l’utilisateur modifie le fuseau horaire sur l’ordinateur client, Outlook sur Mac invite également l’utilisateur à mettre à jour le fuseau horaire dans Outlook.</span><span class="sxs-lookup"><span data-stu-id="b21d8-123">On the Mac, if the user changes the time zone on the client computer, Outlook on Mac would prompt the user to update the time zone in Outlook as well.</span></span>|
|<span data-ttu-id="b21d8-124">Fuseau horaire EAC (Exchange Admin Center)</span><span class="sxs-lookup"><span data-stu-id="b21d8-124">Exchange Admin Center (EAC) time zone</span></span>|<span data-ttu-id="b21d8-125">L’utilisateur définit cette valeur de fuseau horaire (et la langue préférée) lorsqu’il se connecte à Outlook sur le Web ou les appareils mobiles la première fois.</span><span class="sxs-lookup"><span data-stu-id="b21d8-125">The user sets this time zone value (and the preferred language) when he or she logs on to Outlook on the web or mobile devices the first time.</span></span> <br/><br/><span data-ttu-id="b21d8-126">Outlook sur le Web et les appareils mobiles utilisez ce fuseau horaire pour afficher les valeurs de date ou d’heure dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b21d8-126">Outlook on the web and mobile devices use this time zone to display date or time values in the user interface.</span></span>|

<span data-ttu-id="b21d8-127">Étant donné qu’un client riche Outlook utilise le fuseau horaire de l’ordinateur client et que l’interface utilisateur d’Outlook sur le Web et les appareils mobiles utilise le fuseau horaire du centre d’administration Exchange, l’heure locale pour le même complément installé pour la même boîte aux lettres peut être différente lors de l’exécution dans une Clie riche Outlook NT et dans Outlook sur le Web ou les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="b21d8-127">Because an Outlook rich client uses the client computer time zone, and the user interface of Outlook on the web and mobile devices uses the EAC time zone, the local time for the same add-in installed for the same mailbox can be different when running in an Outlook rich client and in Outlook on the web or mobile devices.</span></span> <span data-ttu-id="b21d8-128">En tant que développeur de complément Outlook, vous devez entrer et sortir de façon appropriée les valeurs de date afin qu’elles soient toujours en accord avec le fuseau horaire attendu par l’utilisateur sur le client correspondant.</span><span class="sxs-lookup"><span data-stu-id="b21d8-128">As an Outlook add-in developer, you should appropriately input and output date values so that those values are always consistent with the time zone that the user expects on the corresponding client.</span></span>


### <a name="date-related-api"></a><span data-ttu-id="b21d8-129">API liée à la date</span><span class="sxs-lookup"><span data-stu-id="b21d8-129">Date-related API</span></span>

<span data-ttu-id="b21d8-130">Les propriétés et méthodes suivantes de l’API JavaScript pour Office prennent en charge les fonctionnalités liées à la date.</span><span class="sxs-lookup"><span data-stu-id="b21d8-130">The following are the properties and methods in the Office JavaScript API that support date-related features.</span></span>

<span data-ttu-id="b21d8-131">**Membre de l'API**</span><span class="sxs-lookup"><span data-stu-id="b21d8-131">**API member**</span></span>|<span data-ttu-id="b21d8-132">**Représentation du fuseau horaire**</span><span class="sxs-lookup"><span data-stu-id="b21d8-132">**Time zone representation**</span></span>|<span data-ttu-id="b21d8-133">**Exemple dans un client riche Outlook**</span><span class="sxs-lookup"><span data-stu-id="b21d8-133">**Example in an Outlook rich client**</span></span>|<span data-ttu-id="b21d8-134">**Exemple dans Outlook sur le Web ou les appareils mobiles**</span><span class="sxs-lookup"><span data-stu-id="b21d8-134">**Example in Outlook on the web or mobile devices**</span></span>
--------------|----------------------------|-------------------------------------|-------------------
[<span data-ttu-id="b21d8-135">Office.context.mailbox.userProfile.timeZone</span><span class="sxs-lookup"><span data-stu-id="b21d8-135">Office.context.mailbox.userProfile.timeZone</span></span>](/javascript/api/outlook/office.userprofile?view=outlook-js-preview#timezone)|<span data-ttu-id="b21d8-136">Dans un client riche Outlook, cette propriété renvoie le fuseau horaire de l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="b21d8-136">In an Outlook rich client, this property returns the client computer time zone.</span></span> <span data-ttu-id="b21d8-137">Dans Outlook sur le Web et les appareils mobiles, cette propriété renvoie le fuseau horaire du centre d’administration Exchange.</span><span class="sxs-lookup"><span data-stu-id="b21d8-137">In Outlook on the web and mobile devices, this property returns the EAC time zone.</span></span> |<span data-ttu-id="b21d8-138">EST</span><span class="sxs-lookup"><span data-stu-id="b21d8-138">EST</span></span>|<span data-ttu-id="b21d8-139">PST</span><span class="sxs-lookup"><span data-stu-id="b21d8-139">PST</span></span>
<span data-ttu-id="b21d8-140">[Office.context.mailbox.item.dateTimeCreated](../reference/objectmodel/preview-requirement-set/office.context.mailbox.item.md#properties) et [Office.context.mailbox.item.dateTimeModified](../reference/objectmodel/preview-requirement-set/office.context.mailbox.item.md#properties)</span><span class="sxs-lookup"><span data-stu-id="b21d8-140">[Office.context.mailbox.item.dateTimeCreated](../reference/objectmodel/preview-requirement-set/office.context.mailbox.item.md#properties) and [Office.context.mailbox.item.dateTimeModified](../reference/objectmodel/preview-requirement-set/office.context.mailbox.item.md#properties)</span></span>|<span data-ttu-id="b21d8-141">Chacune de ces propriétés renvoie un objet `Date` JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b21d8-141">Each of these properties returns a JavaScript `Date` object.</span></span> <span data-ttu-id="b21d8-142">Cette `Date` valeur est correcte (UTC), comme indiqué dans l’exemple suivant `myUTCDate` -a la même valeur dans un client riche Outlook, Outlook sur le Web et les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="b21d8-142">This `Date` value is UTC-correct, as shown in the following example - `myUTCDate` has the same value in an Outlook rich client, Outlook on the web and mobile devices.</span></span><br/><br/>`var myDate = Office.mailbox.item.dateTimeCreated;`<br/>`var myUTCDate = myDate.getUTCDate;`<br/><br/><span data-ttu-id="b21d8-143">Toutefois, l' `myDate.getDate` appel renvoie une valeur de date dans le fuseau horaire de l’ordinateur client, qui est cohérente avec le fuseau horaire utilisé pour afficher les valeurs de date et d’heure dans l’interface client riche Outlook, mais peut être différent du fuseau horaire du centre d’administration Exchange sur le Web et les appareils mobiles utilisés dans son interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b21d8-143">However, calling  `myDate.getDate` returns a date value in the client computer time zone, which is consistent with the time zone used to display date times values in the Outlook rich client interface, but may be different from the EAC time zone that Outlook on the web and mobile devices use in its user interface.</span></span>|<span data-ttu-id="b21d8-144">Si l’élément est créé à 9 h 00 UTC :</span><span class="sxs-lookup"><span data-stu-id="b21d8-144">If the item is created at 9am UTC:</span></span><br/><br/>`Office.mailbox.item.`<br/><span data-ttu-id="b21d8-145">`dateTimeCreated.getHours` renvoie 4 h 00 EST.</span><span class="sxs-lookup"><span data-stu-id="b21d8-145">`dateTimeCreated.getHours` returns 4am EST.</span></span><br/><br/><span data-ttu-id="b21d8-146">Si l’élément est modifié à 11 h 00 UTC :</span><span class="sxs-lookup"><span data-stu-id="b21d8-146">If the item is modified at 11am UTC:</span></span><br/><br/>`Office.mailbox.item.`<br/><span data-ttu-id="b21d8-147">`dateTimeModified.getHours` renvoie 6h00 EST.</span><span class="sxs-lookup"><span data-stu-id="b21d8-147">`dateTimeModified.getHours` returns 6am EST.</span></span>|<span data-ttu-id="b21d8-148">Si l’élément est créé à 9 h 00 UTC :</span><span class="sxs-lookup"><span data-stu-id="b21d8-148">If the item creation time is 9am UTC:</span></span><br/><br/>`Office.mailbox.item.`</br><span data-ttu-id="b21d8-149">`dateTimeCreated.getHours` renvoie 4 h 00 EST.</span><span class="sxs-lookup"><span data-stu-id="b21d8-149">`dateTimeCreated.getHours` returns 4am EST.</span></span><br/><br/><span data-ttu-id="b21d8-150">Si l’élément est modifié à 11 h 00 UTC :</span><span class="sxs-lookup"><span data-stu-id="b21d8-150">If the item is modified at 11am UTC:</span></span><br/><br/>`Office.mailbox.item.`</br><span data-ttu-id="b21d8-151">`dateTimeModified.getHours` renvoie 6 h 00 EST.</span><span class="sxs-lookup"><span data-stu-id="b21d8-151">`dateTimeModified.getHours` returns 6am EST.</span></span><br/><br/><span data-ttu-id="b21d8-152">Notez que si vous souhaitez afficher l’heure de création ou de modification dans l’interface utilisateur, vous pouvez d’abord convertir l’heure au format PST pour rester cohérent avec le reste de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b21d8-152">Notice that if you want to display the creation or modification time in the user interface, you would want to first convert the time to PST to be consistent with the rest of the user interface.</span></span>
[<span data-ttu-id="b21d8-153">Office.context.mailbox.displayNewAppointmentForm</span><span class="sxs-lookup"><span data-stu-id="b21d8-153">Office.context.mailbox.displayNewAppointmentForm</span></span>](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods)|<span data-ttu-id="b21d8-154">Chacun des paramètres de _début_ et de _fin_ requiert un `Date` objet JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b21d8-154">Each of the  _Start_ and _End_ parameters requires a JavaScript `Date` object.</span></span> <span data-ttu-id="b21d8-155">Les arguments doivent être au format UTC, quel que soit le fuseau horaire utilisé dans l’interface utilisateur d’un client riche Outlook, ou Outlook sur le Web ou les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="b21d8-155">The arguments should be UTC-correct regardless of the time zone used in the user interface of an Outlook rich client, or Outlook on the web or mobile devices.</span></span>|<span data-ttu-id="b21d8-156">Si les heures de début et de fin du formulaire de rendez-vous sont 9h00 UTC et 11h00 UTC, vous devez vous assurer que les arguments `start` et `end` sont conformes au format UTC, autrement dit :</span><span class="sxs-lookup"><span data-stu-id="b21d8-156">If the start and end times for the appointment form are 9am UTC and 11am UTC, then you should assure that the `start` and `end` arguments are UTC-correct, which means:</span></span><br/><br/><ul><li><span data-ttu-id="b21d8-157">`start.getUTCHours` renvoie 9 h 00 UTC</span><span class="sxs-lookup"><span data-stu-id="b21d8-157">`start.getUTCHours` returns 9am UTC</span></span></li><li><span data-ttu-id="b21d8-158">`end.getUTCHours` renvoie 11 h 00 UTC</span><span class="sxs-lookup"><span data-stu-id="b21d8-158">`end.getUTCHours` returns 11am UTC</span></span></li></ul>|<span data-ttu-id="b21d8-159">Si les heures de début et de fin du formulaire de rendez-vous sont 9h00 UTC et 11h00 UTC, vous devez vous assurer que les arguments `start` et `end` sont conformes au format UTC, autrement dit :</span><span class="sxs-lookup"><span data-stu-id="b21d8-159">If the start and end times for the appointment form are 9am UTC and 11am UTC, then you should assure that the `start` and `end` arguments are UTC-correct, which means:</span></span><br/><br/><ul><li><span data-ttu-id="b21d8-160">`start.getUTCHours` renvoie 9 h 00 UTC</span><span class="sxs-lookup"><span data-stu-id="b21d8-160">`start.getUTCHours` returns 9am UTC</span></span></li><li><span data-ttu-id="b21d8-161">`end.getUTCHours` renvoie 11 h 00 UTC</span><span class="sxs-lookup"><span data-stu-id="b21d8-161">`end.getUTCHours` returns 11am UTC</span></span></li></ul>

## <a name="helper-methods-for-date-related-scenarios"></a><span data-ttu-id="b21d8-162">Méthodes d’assistance pour les scénarios liés à la date</span><span class="sxs-lookup"><span data-stu-id="b21d8-162">Helper methods for date-related scenarios</span></span>


<span data-ttu-id="b21d8-163">Comme décrit dans les sections précédentes, étant donné que la « durée locale » pour un utilisateur dans Outlook sur le Web ou les appareils mobiles peut être différente sur un client riche Outlook, mais que l’objet JavaScript **Date** prend uniquement en charge la conversion vers le fuseau horaire de l’ordinateur client ou l’UTC, l’API JavaScript Office fournit deux méthodes d’assistance : [Office. Context. Mailbox. convertToLocalClientTime](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods) et [Office](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods)</span><span class="sxs-lookup"><span data-stu-id="b21d8-163">As described in the preceding sections, because the "local time" for a user in Outlook on the web or mobile devices can be different on an Outlook rich client, but the JavaScript **Date** object supports converting to only the client computer time zone or UTC, the Office JavaScript API provides two helper methods: [Office.context.mailbox.convertToLocalClientTime](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods) and [Office.context.mailbox.convertToUtcClientTime](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods).</span></span>

<span data-ttu-id="b21d8-164">Ces méthodes d’assistance ont besoin de gérer la date ou l’heure différemment pour les deux scénarios de date suivants, dans un client riche Outlook, Outlook sur le Web et les appareils mobiles, renforçant ainsi « l’écriture unique » pour les différents clients de votre complément.</span><span class="sxs-lookup"><span data-stu-id="b21d8-164">These helper methods take care of any need to handle date or time differently for the following two date-related scenarios, in an Outlook rich client, Outlook on the web and mobile devices, thus reinforcing "write-once" for different clients of your add-in.</span></span>


### <a name="scenario-a-displaying-item-creation-or-modified-time"></a><span data-ttu-id="b21d8-165">Scénario A : affichage de l’heure de création ou de modification d’un élément</span><span class="sxs-lookup"><span data-stu-id="b21d8-165">Scenario A: Displaying item creation or modified time</span></span>

<span data-ttu-id="b21d8-166">Si vous affichez l’heure de création de`Item.dateTimeCreated`l’élément () ou`Item.dateTimeModified`l’heure de modification (dans l' `convertToLocalClientTime` interface utilisateur, `Date` utilisez d’abord pour convertir l’objet fourni par ces propriétés afin d’obtenir une représentation de dictionnaire dans l’heure locale appropriée.</span><span class="sxs-lookup"><span data-stu-id="b21d8-166">If you are displaying the item creation time (`Item.dateTimeCreated`) or modification time (`Item.dateTimeModified`in the user interface, first use `convertToLocalClientTime` to convert the `Date` object provided by these properties to obtain a dictionary representation in the appropriate local time.</span></span> <span data-ttu-id="b21d8-167">Affichez ensuite les parties de la date de dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="b21d8-167">Then display the parts of the dictionary date.</span></span> <span data-ttu-id="b21d8-168">L’exemple suivant illustre ce scénario :</span><span class="sxs-lookup"><span data-stu-id="b21d8-168">The following is an example of this scenario:</span></span>


```js
// This date is UTC-correct.
var myDate = Office.context.mailbox.item.dateTimeCreated;

// Call helper method to get date in dictionary format, 
// represented in the appropriate local time.
// In an Outlook rich client, this is dictionary format 
// in client computer time zone.
// In Outlook on the web or mobile devices, this dictionary 
// format is in EAC time zone.
var myLocalDictionaryDate = Office.context.mailbox.convertToLocalClientTime(myDate);

// Display different parts of the dictionary date.
document.write ("The item was created at " + myLocalDictionaryDate["hours"] + 
    ":" + myLocalDictionaryDate["minutes"]);)
```

<span data-ttu-id="b21d8-169">Notez que `convertToLocalClientTime` prend en charge la différence entre un client riche Outlook et Outlook sur le Web ou les appareils mobiles :</span><span class="sxs-lookup"><span data-stu-id="b21d8-169">Note that `convertToLocalClientTime` takes care of the difference between an Outlook rich client, and Outlook on the web or mobile devices:</span></span>


- <span data-ttu-id="b21d8-170">Si `convertToLocalClientTime` détecte que l’hôte actuel est un client riche, la méthode convertit `Date` la représentation en une représentation de dictionnaire dans le même fuseau horaire de l’ordinateur client, conformément au reste de l’interface utilisateur du client riche.</span><span class="sxs-lookup"><span data-stu-id="b21d8-170">If `convertToLocalClientTime` detects the current host is a rich client, the method converts the `Date` representation to a dictionary representation in the same client computer time zone, consistent with the rest of the rich client user interface.</span></span>
    
- <span data-ttu-id="b21d8-171">Si `convertToLocalClientTime` détecte que l’hôte actuel est Outlook sur le Web ou sur des appareils mobiles, la méthode convertit la `Date` représentation UTC (UTC) en un format de dictionnaire dans le fuseau horaire d’un centre d’administration Exchange, cohérent avec le reste de l’interface utilisateur d’Outlook sur le Web ou sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="b21d8-171">If `convertToLocalClientTime` detects the current host is Outlook on the web or mobile devices, the method converts the UTC-correct `Date` representation to a dictionary format in the EAC time zone, consistent with the rest of the Outlook on the web or mobile devices user interface.</span></span>
    

### <a name="scenario-b-displaying-start-and-end-dates-in-a-new-appointment-form"></a><span data-ttu-id="b21d8-172">Scénario B : affichage des dates de début et de fin dans un formulaire de nouveau rendez-vous</span><span class="sxs-lookup"><span data-stu-id="b21d8-172">Scenario B: Displaying start and end dates in a new appointment form</span></span>

<span data-ttu-id="b21d8-173">Si vous obtenez en entrée des parties différentes d’une valeur de date et d’heure représentée dans l’heure locale et que vous souhaitez fournir cette valeur d’entrée de dictionnaire comme heure de début ou de fin dans un formulaire de `convertToUtcClientTime` rendez-vous, utilisez d’abord la méthode d’assistance pour `Date` convertir la valeur de dictionnaire en objet UTC correct.</span><span class="sxs-lookup"><span data-stu-id="b21d8-173">If you are obtaining as input different parts of a date-time value represented in the local time, and would like to provide this dictionary input value as a start or end time in an appointment form, first use the `convertToUtcClientTime` helper method to convert the dictionary value to a UTC-correct `Date` object.</span></span>

<span data-ttu-id="b21d8-p110">Dans l’exemple suivant, supposons que  `myLocalDictionaryStartDate` et `myLocalDictionaryEndDate` sont des valeurs de date et d’heure au format de dictionnaire que vous avez obtenues auprès de l’utilisateur. Ces valeurs sont basées sur l’heure locale, qui dépend elle-même de l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="b21d8-p110">In the following example, assume  `myLocalDictionaryStartDate` and `myLocalDictionaryEndDate` are date-time values in dictionary format that you have obtained from the user. These values are based on the local time, dependent on the host application.</span></span>

```js
var myUTCCorrectStartDate = Office.context.mailbox.convertToUtcClientTime(myLocalDictionaryStartDate);
var myUTCCorrectEndDate = Office.context.mailbox.convertToUtcClientTime(myLocalDictionaryEndDate);

```

<span data-ttu-id="b21d8-176">Les valeurs qui en résultent, `myUTCCorrectStartDate` et `myUTCCorrectEndDate`, sont au format UTC.</span><span class="sxs-lookup"><span data-stu-id="b21d8-176">The resultant values,  `myUTCCorrectStartDate` and `myUTCCorrectEndDate`, are UTC-correct.</span></span> <span data-ttu-id="b21d8-177">Transmettez ensuite `Date` ces objets comme arguments pour les paramètres de _début_ et de `Mailbox.displayNewAppointmentForm` _fin_ de la méthode pour afficher le nouveau formulaire de rendez-vous.</span><span class="sxs-lookup"><span data-stu-id="b21d8-177">Then pass these `Date` objects as arguments for the _Start_ and _End_ parameters of the `Mailbox.displayNewAppointmentForm` method to display the new appointment form.</span></span>

<span data-ttu-id="b21d8-178">Notez que `convertToUtcClientTime` prend en charge la différence entre un client riche Outlook et Outlook sur le Web ou les appareils mobiles :</span><span class="sxs-lookup"><span data-stu-id="b21d8-178">Note that `convertToUtcClientTime` takes care of the difference between an Outlook rich client, and Outlook on the web or mobile devices:</span></span>


- <span data-ttu-id="b21d8-179">Si `convertToUtcClientTime` détecte que l’hôte actuel est un client riche Outlook, la méthode convertit simplement la représentation du dictionnaire `Date` en objet.</span><span class="sxs-lookup"><span data-stu-id="b21d8-179">If `convertToUtcClientTime` detects the current host is an Outlook rich client, the method simply converts the dictionary representation to a `Date` object.</span></span> <span data-ttu-id="b21d8-180">Cet `Date` objet est conforme au format UTC, comme attendu `displayNewAppointmentForm`par.</span><span class="sxs-lookup"><span data-stu-id="b21d8-180">This `Date` object is UTC-correct, as expected by `displayNewAppointmentForm`.</span></span>
    
- <span data-ttu-id="b21d8-181">Si `convertToUtcClientTime` détecte que l’hôte actuel est Outlook sur le Web ou les appareils mobiles, la méthode convertit le format de dictionnaire des valeurs de date et d’heure exprimées dans le `Date` fuseau horaire du centre d’administration Exchange en un objet.</span><span class="sxs-lookup"><span data-stu-id="b21d8-181">If `convertToUtcClientTime` detects the current host is Outlook on the web or mobile devices, the method converts the dictionary format of the date and time values expressed in the EAC time zone to a `Date` object.</span></span> <span data-ttu-id="b21d8-182">Cet `Date` objet est conforme au format UTC, comme attendu `displayNewAppointmentForm`par.</span><span class="sxs-lookup"><span data-stu-id="b21d8-182">This `Date` object is UTC-correct, as expected by `displayNewAppointmentForm`.</span></span>
    
## <a name="see-also"></a><span data-ttu-id="b21d8-183">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b21d8-183">See also</span></span>

- [<span data-ttu-id="b21d8-184">Déployer et installer des compléments Outlook à des fins de test</span><span class="sxs-lookup"><span data-stu-id="b21d8-184">Deploy and install Outlook add-ins for testing</span></span>](testing-and-tips.md)