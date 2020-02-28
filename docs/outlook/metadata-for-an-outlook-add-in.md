---
title: Obtenir et définir des métadonnées dans un complément Outlook
description: Vous pouvez gérer les données personnalisées dans votre complément Outlook en utilisant les paramètres d’itinérance ou propriétés personnalisées.
ms.date: 10/31/2019
localization_priority: Normal
ms.openlocfilehash: 3bf19f56b11b524ea2ee722e2997465bbd36d55c
ms.sourcegitcommit: 5d29801180f6939ec10efb778d2311be67d8b9f1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2020
ms.locfileid: "42324932"
---
# <a name="get-and-set-add-in-metadata-for-an-outlook-add-in"></a><span data-ttu-id="5ab7e-103">Obtenir et définir des métadonnées de complément pour un complément Outlook</span><span class="sxs-lookup"><span data-stu-id="5ab7e-103">Get and set add-in metadata for an Outlook add-in</span></span>

<span data-ttu-id="5ab7e-104">Vous pouvez gérer les données personnalisées dans votre complément Outlook en utilisant une des solutions suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ab7e-104">You can manage custom data in your Outlook add-in by using either of the following:</span></span>

- <span data-ttu-id="5ab7e-105">Les paramètres d’itinérance, qui permettent de gérer des données personnalisées pour la boîte aux lettres d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-105">Roaming settings, which manage custom data for a user's mailbox.</span></span>
- <span data-ttu-id="5ab7e-106">Les propriétés personnalisées, qui permettent de gérer des données personnalisées pour un élément de boîte aux lettres d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-106">Custom properties, which manage custom data for an item in a user's mailbox.</span></span>

<span data-ttu-id="5ab7e-p101">Ces deux méthodes donnent accès aux données personnalisées auxquelles seul votre complément Outlook a accès, mais chaque méthode stocke les données de façon distincte. Autrement dit, les propriétés personnalisées n’ont pas accès aux données stockées par le biais des paramètres d’itinérance et inversement. Les données sont stockées sur le serveur de la boîte aux lettres et sont accessibles dans les sessions Outlook ultérieures sur tous les formats pris en charge par le complément.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-p101">Both of these give access to custom data that is only accessible by your Outlook add-in, but each method stores the data separately from the other. That is, the data stored through roaming settings is not accessible by custom properties, and vice versa. The data is stored on the server for that mailbox, and is accessible in subsequent Outlook sessions on all the form factors that the add-in supports.</span></span>

## <a name="custom-data-per-mailbox-roaming-settings"></a><span data-ttu-id="5ab7e-110">Données personnalisées par boîte aux lettres : paramètres d’itinérance</span><span class="sxs-lookup"><span data-stu-id="5ab7e-110">Custom data per mailbox: roaming settings</span></span>

<span data-ttu-id="5ab7e-p102">Vous pouvez indiquer des données propres à la boîte aux lettres Exchange d’un utilisateur, à l’aide de l’objet [RoamingSettings](/javascript/api/outlook/office.RoamingSettings), telles que les préférences et les données personnelles de l’utilisateur. Votre complément de messagerie peut accéder aux paramètres d’itinérance lorsqu’il est en itinérance sur un appareil pour lequel il a été conçu (ordinateur, tablette ou smartphone).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-p102">You can specify data specific to a user's Exchange mailbox using the [RoamingSettings](/javascript/api/outlook/office.RoamingSettings) object. Examples of such data include the user's personal data and preferences. Your mail add-in can access roaming settings when it roams on any device it's designed to run on (desktop, tablet, or smartphone).</span></span>

<span data-ttu-id="5ab7e-p103">Les modifications apportées à ces données sont stockées dans une copie en mémoire de ces paramètres pour la session Outlook en cours. Vous devez explicitement enregistrer tous les paramètres d’itinérance après les avoir mis à jour afin qu’ils soient disponibles lors de la prochaine ouverture de votre complément, sur le même appareil ou sur un autre appareil pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-p103">Changes to this data are stored on an in-memory copy of those settings for the current Outlook session. You should explicitly save all the roaming settings after updating them so that they will be available the next time the user opens your add-in, on the same or any other supported device.</span></span>


### <a name="roaming-settings-format"></a><span data-ttu-id="5ab7e-116">Format des paramètres d’itinérance</span><span class="sxs-lookup"><span data-stu-id="5ab7e-116">Roaming settings format</span></span>

<span data-ttu-id="5ab7e-117">Les données dans un objet **RoamingSettings** sont stockées sous forme d’une chaîne sérialisée JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-117">The data in a **RoamingSettings** object is stored as a serialized JavaScript Object Notation (JSON) string.</span></span> 

<span data-ttu-id="5ab7e-118">Voici un exemple de structure, en supposant qu’il y a trois paramètres d’itinérance définis nommés `add-in_setting_name_0`, `add-in_setting_name_1` et `add-in_setting_name_2`.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-118">The following is an example of the structure, assuming there are three defined roaming settings named `add-in_setting_name_0`,  `add-in_setting_name_1`, and  `add-in_setting_name_2`.</span></span>


```json
{
  "add-in_setting_name_0": "add-in_setting_value_0",
  "add-in_setting_name_1": "add-in_setting_value_1",
  "add-in_setting_name_2": "add-in_setting_value_2"
}
```


### <a name="loading-roaming-settings"></a><span data-ttu-id="5ab7e-119">Chargement des paramètres d’itinérance</span><span class="sxs-lookup"><span data-stu-id="5ab7e-119">Loading roaming settings</span></span>

<span data-ttu-id="5ab7e-120">Un complément de messagerie charge généralement les paramètres d’itinérance dans le gestionnaire d’événements [Office.initialize](/javascript/api/office#office-initialize-reason-).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-120">A mail add-in typically loads roaming settings in the [Office.initialize](/javascript/api/office#office-initialize-reason-) event handler.</span></span> <span data-ttu-id="5ab7e-121">L’exemple de code JavaScript suivant montre comment charger des paramètres d’itinérance existants et obtenir la valeur de 2 paramètres, **customerName** et **customerBalance** :</span><span class="sxs-lookup"><span data-stu-id="5ab7e-121">The following JavaScript code example shows how to load existing roaming settings and get the values of 2 settings, **customerName** and **customerBalance**:</span></span>


```js
var _mailbox;
var _settings;
var _customerName;
var _customerBalance;

// The initialize function is required for all add-ins.
Office.initialize = function () {
  // Initialize instance variables to access API objects.
  _mailbox = Office.context.mailbox;
  _settings = Office.context.roamingSettings;
  _customerName = _settings.get("customerName");
  _customerBalance = _settings.get("customerBalance");
}

```


### <a name="creating-or-assigning-a-roaming-setting"></a><span data-ttu-id="5ab7e-122">Création ou affectation d’un paramètre d’itinérance</span><span class="sxs-lookup"><span data-stu-id="5ab7e-122">Creating or assigning a roaming setting</span></span>

<span data-ttu-id="5ab7e-123">Pour faire suite à l’exemple précédent, la fonction JavaScript suivante, `setAddInSetting`, montre comment utiliser la méthode [RoamingSettings.set](/javascript/api/outlook/office.RoamingSettings) pour définir un paramètre nommé `cookie` avec la date du jour, et conserver les données en utilisant la méthode [RoamingSettings.saveAsync](/javascript/api/outlook/office.RoamingSettings#saveasync-callback-) pour réenregistrer tous les paramètres d’itinérance sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-123">Continuing with the preceding example, the following JavaScript function,  `setAddInSetting`, shows how to use the [RoamingSettings.set](/javascript/api/outlook/office.RoamingSettings) method to set a setting named `cookie` with today's date, and persist the data by using the [RoamingSettings.saveAsync](/javascript/api/outlook/office.RoamingSettings#saveasync-callback-) method to save all the roaming settings back to the server.</span></span>

<span data-ttu-id="5ab7e-124">La `set` méthode crée le paramètre si le paramètre n’existe pas déjà et affecte le paramètre à la valeur spécifiée.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-124">The `set` method creates the setting if the setting does not already exist, and assigns the setting to the specified value.</span></span> <span data-ttu-id="5ab7e-125">La `saveAsync` méthode enregistre les paramètres d’itinérance de manière asynchrone.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-125">The `saveAsync` method saves roaming settings asynchronously.</span></span> <span data-ttu-id="5ab7e-126">Cet exemple de code transmet une méthode de `saveMyAddInSettingsCallback`rappel, `saveAsync` , à la fin de l' `saveMyAddInSettingsCallback` appel asynchrone, est appelée à l’aide d’un paramètre, _asyncResult_.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-126">This code sample passes a callback method, `saveMyAddInSettingsCallback`, to `saveAsync` When the asynchronous call finishes,  `saveMyAddInSettingsCallback` is called by using one parameter, _asyncResult_.</span></span> <span data-ttu-id="5ab7e-127">Ce paramètre est un objet [AsyncResult](/javascript/api/office/office.asyncresult) qui contient le résultat des détails relatifs à l’appel asynchrone.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-127">This parameter is an [AsyncResult](/javascript/api/office/office.asyncresult) object that contains the result of and any details about the asynchronous call.</span></span> <span data-ttu-id="5ab7e-128">Vous pouvez utiliser le paramètre facultatif _userContext_ pour transmettre des informations d’état de l’appel asynchrone à la fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-128">You can use the optional _userContext_ parameter to pass any state information from the asynchronous call to the callback function.</span></span>

```js
// Set a roaming setting.
function setAddInSetting() {
  _settings.set("cookie", Date());
  // Save roaming settings for the mailbox
  // to the server so that they will be available
  // in the next session.
  _settings.saveAsync(saveMyAddInSettingsCallback);
}

// Callback method after saving custom roaming settings.
function saveMyAddInSettingsCallback(asyncResult) {
  if (asyncResult.status == Office.AsyncResultStatus.Failed) {
    // Handle the failure.
  }
}
```


### <a name="removing-a-roaming-setting"></a><span data-ttu-id="5ab7e-129">Suppression d’un paramètre d’itinérance</span><span class="sxs-lookup"><span data-stu-id="5ab7e-129">Removing a roaming setting</span></span>

<span data-ttu-id="5ab7e-130">Toujours dans le prolongement des exemples précédents, la fonction JavaScript suivante,  `removeAddInSetting`, illustre l’utilisation de la méthode [RoamingSettings.remove](/javascript/api/outlook/office.RoamingSettings#remove-name-) pour supprimer le paramètre `cookie` et réenregistrer tous les paramètres d’itinérance sur le serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-130">Also extending the preceding examples, the following JavaScript function,  `removeAddInSetting`, shows how to use the [RoamingSettings.remove](/javascript/api/outlook/office.RoamingSettings#remove-name-) method to remove the `cookie` setting and save all the roaming settings back to the Exchange Server.</span></span>


```js
// Remove an add-in setting.
function removeAddInSetting()
{
  _settings.remove("cookie");
  // Save changes to the roaming settings for the mailbox
  // to the server so that they will be available
  // in the next session.
  _settings.saveAsync(saveMyAddInSettingsCallback);
}
```


## <a name="custom-data-per-item-in-a-mailbox-custom-properties"></a><span data-ttu-id="5ab7e-131">Données personnalisées par élément dans une boîte aux lettres : propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="5ab7e-131">Custom data per item in a mailbox: custom properties</span></span>

<span data-ttu-id="5ab7e-p106">Vous pouvez spécifier les données propres à un élément dans la boîte aux lettres de l’utilisateur à l’aide de l’objet [CustomProperties](/javascript/api/outlook/office.CustomProperties). Par exemple, votre complément de messagerie peut catégoriser certains messages et noter la catégorie à l’aide d’une propriété personnalisée`messageCategory`. Si votre complément de messagerie crée des rendez-vous à partir de suggestions de réunion dans un message, vous pouvez utiliser une propriété personnalisée pour suivre chacun de ces rendez-vous. Cela garantit que si l’utilisateur ouvre à nouveau le message, votre complément de messagerie ne propose pas de créer le rendez-vous une seconde fois.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-p106">You can specify data specific to an item in the user's mailbox using the [CustomProperties](/javascript/api/outlook/office.CustomProperties) object. For example, your mail add-in could categorize certain messages and note the category using a custom property `messageCategory`. Or, if your mail add-in creates appointments from meeting suggestions in a message, you can use a custom property to track each of these appointments. This ensures that if the user opens the message again, your mail add-in doesn't offer to create the appointment a second time.</span></span>

<span data-ttu-id="5ab7e-p107">Comme pour les paramètres d’itinérance, les modifications apportées aux propriétés personnalisées sont stockées dans des copies en mémoire des propriétés de la session Outlook en cours. Pour vous assurer que les propriétés personnalisées seront disponibles dans la prochaine session, utilisez [CustomProperties.saveAsync](/javascript/api/outlook/office.CustomProperties#saveasync-callback--asynccontext-).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-p107">Similar to roaming settings, changes to custom properties are stored on in-memory copies of the properties for the current Outlook session. To make sure these custom properties will be available in the next session, use [CustomProperties.saveAsync](/javascript/api/outlook/office.CustomProperties#saveasync-callback--asynccontext-).</span></span>

<span data-ttu-id="5ab7e-138">Ces propriétés personnalisées propres aux éléments, spécifiques à un complément, sont accessibles uniquement à l’aide `CustomProperties` de l’objet.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-138">These add-in-specific, item-specific custom properties can only be accessed by using the `CustomProperties` object.</span></span> <span data-ttu-id="5ab7e-139">Ces propriétés sont différentes de la propriété [UserProperties](/office/vba/api/Outlook.UserProperties) personnalisée, basée sur MAPI dans le modèle objet Outlook, et des propriétés étendues dans les services Web Exchange (EWS).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-139">These properties are different from the custom, MAPI-based [UserProperties](/office/vba/api/Outlook.UserProperties) in the Outlook object model, and extended properties in Exchange Web Services (EWS).</span></span> <span data-ttu-id="5ab7e-140">Vous ne pouvez pas `CustomProperties` accéder directement à l’aide du modèle objet Outlook, EWS ou Rest.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-140">You cannot directly access `CustomProperties` by using the Outlook object model, EWS, or REST.</span></span> <span data-ttu-id="5ab7e-141">Pour savoir comment accéder `CustomProperties` à l’aide d’EWS ou REST, consultez la section obtenir des [propriétés personnalisées à l’aide d’EWS ou Rest](#get-custom-properties-using-ews-or-rest).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-141">To learn how to access `CustomProperties` using EWS or REST, see the section [Get custom properties using EWS or REST](#get-custom-properties-using-ews-or-rest).</span></span>

### <a name="using-custom-properties"></a><span data-ttu-id="5ab7e-142">Utilisation de propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="5ab7e-142">Using custom properties</span></span>

<span data-ttu-id="5ab7e-143">Avant de pouvoir utiliser les propriétés personnalisées, vous devez les charger en appelant la méthode [loadCustomPropertiesAsync](../reference/objectmodel/preview-requirement-set/office.context.mailbox.item.md#methods).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-143">Before you can use custom properties, you must load them by calling the [loadCustomPropertiesAsync](../reference/objectmodel/preview-requirement-set/office.context.mailbox.item.md#methods) method.</span></span> <span data-ttu-id="5ab7e-144">Après avoir créé le conteneur de propriétés, vous pouvez utiliser les méthodes [Définir](/javascript/api/outlook/office.CustomProperties#set-name--value-) et [Obtenir](/javascript/api/outlook/office.CustomProperties) pour ajouter et récupérer des propriétés personnalisées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-144">After you have created the property bag, you can use the [set](/javascript/api/outlook/office.CustomProperties#set-name--value-) and [get](/javascript/api/outlook/office.CustomProperties) methods to add and retrieve custom properties.</span></span> <span data-ttu-id="5ab7e-145">Vous devez utiliser la méthode[saveAsync](/javascript/api/outlook/office.CustomProperties#saveasync-callback--asynccontext-) pour enregistrer les modifications que vous apportez au conteneur de propriétés.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-145">You must use the [saveAsync](/javascript/api/outlook/office.CustomProperties#saveasync-callback--asynccontext-) method to save any changes that you make to the property bag.</span></span>


 > [!NOTE]
 > <span data-ttu-id="5ab7e-146">Comme Outlook sur Mac ne met pas en cache les propriétés personnalisées, si le réseau de l’utilisateur tombe en panne, les compléments de messagerie dans Outlook sur Mac ne pourront pas accéder à leurs propriétés personnalisées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-146">Because Outlook on Mac doesn't cache custom properties, if the user's network goes down, mail add-ins in Outlook on Mac would not be able to access their custom properties.</span></span>


### <a name="custom-properties-example"></a><span data-ttu-id="5ab7e-147">Exemple de propriétés personnalisées</span><span class="sxs-lookup"><span data-stu-id="5ab7e-147">Custom properties example</span></span>


<span data-ttu-id="5ab7e-p110">L’exemple suivant illustre un ensemble simplifié des méthodes pour un complément Outlook qui utilise des propriétés personnalisées. Vous pouvez utiliser cet exemple comme point de départ pour votre complément qui utilise des propriétés personnalisées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-p110">The following example shows a simplified set of methods for an Outlook add-in that uses custom properties. You can use this example as a starting point for your add-in that uses custom properties.</span></span>

<span data-ttu-id="5ab7e-150">Cet exemple inclut les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ab7e-150">This example includes the following methods:</span></span>


- <span data-ttu-id="5ab7e-151">[Office.initialize](/javascript/api/office#office-initialize-reason-) -- Initialise le complément et charge le conteneur de propriétés personnalisées depuis le serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-151">[Office.initialize](/javascript/api/office#office-initialize-reason-) -- Initializes the add-in and loads the custom property bag from the Exchange server.</span></span>

- <span data-ttu-id="5ab7e-152">**customPropsCallback** -- Obtient le conteneur de propriétés personnalisées qui est renvoyé depuis le serveur et l’enregistre pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-152">**customPropsCallback** -- Gets the custom property bag that is returned from the server and saves it for later use.</span></span>

- <span data-ttu-id="5ab7e-153">**updateProperty** -- Définit ou met à jour une propriété spécifique, puis enregistre la modification sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-153">**updateProperty** -- Sets or updates a specific property, and then saves the change to the server.</span></span>

- <span data-ttu-id="5ab7e-154">**removeProperty** -- Supprime une propriété spécifique à partir du conteneur de propriétés, puis enregistre la suppression sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-154">**removeProperty** -- Removes a specific property from the property bag, and then saves the removal to the server.</span></span>


```js
var _mailbox;
var _customProps;

// The initialize function is required for all add-ins.
Office.initialize = function () {
  _mailbox = Office.context.mailbox;
  _mailbox.item.loadCustomPropertiesAsync(customPropsCallback);
}

// Callback function from loading custom properties.
function customPropsCallback(asyncResult) {
  if (asyncResult.status == Office.AsyncResultStatus.Failed) {
    // Handle the failure.
  }
  else {
    // Successfully loaded custom properties,
    // can get them from the asyncResult argument.
    _customProps = asyncResult.value;
  }
}

// Get individual custom property.
function getProperty() {
  var myProp = _customProps.get("myProp");
}

// Set individual custom property.
function updateProperty(name, value) {
  _customProps.set(name, value);
  // Save all custom properties to server.
  _customProps.saveAsync(saveCallback);
}

// Remove a custom property.
function removeProperty(name) {
  _customProps.remove(name);
  // Save all custom properties to server.
  _customProps.saveAsync(saveCallback);
}

// Callback function from saving custom properties.
function saveCallback() {
  if (asyncResult.status == Office.AsyncResultStatus.Failed) {
    // Handle the failure.
  }
}
```

### <a name="get-custom-properties-using-ews-or-rest"></a><span data-ttu-id="5ab7e-155">Obtenir des propriétés personnalisées à l’aide de EWS ou REST</span><span class="sxs-lookup"><span data-stu-id="5ab7e-155">Get custom properties using EWS or REST</span></span>

<span data-ttu-id="5ab7e-156">Pour obtenir **CustomProperties** à l’aide de EWS ou REST, vous devez commencer par déterminer le nom de sa base propriété étendue MAPI.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-156">To get **CustomProperties** using EWS or REST, you should first determine the name of its MAPI-based extended property.</span></span> <span data-ttu-id="5ab7e-157">Vous pouvez ensuite obtenir cette propriété de la même façon que vous pouviez obtenir toute propriété étendue de base MAPI.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-157">You can then get that property in the same way you would get any MAPI-based extended property.</span></span>

#### <a name="how-custom-properties-are-stored-on-an-item"></a><span data-ttu-id="5ab7e-158">Comment les propriétés personnalisées sont stockées sur un élément</span><span class="sxs-lookup"><span data-stu-id="5ab7e-158">How custom properties are stored on an item</span></span>

<span data-ttu-id="5ab7e-159">Les propriétés personnalisées définies par un complément ne sont pas équivalentes aux propriétés de base MAPI normales.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-159">Custom properties set by an add-in are not equivalent to normal MAPI-based properties.</span></span> <span data-ttu-id="5ab7e-160">Les API `CustomProperties` de complément sérialisent tout votre complément en tant que charge utile JSON, puis les enregistrent dans une seule propriété étendue MAPI dont le nom est `cecp-<app-guid>` (`<app-guid>` est l’ID de votre complément) et le GUID de jeu de `{00020329-0000-0000-C000-000000000046}`propriétés est.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-160">Add-in APIs serialize all your add-in's `CustomProperties` as a JSON payload and then save them in a single MAPI-based extended property whose name is `cecp-<app-guid>` (`<app-guid>` is your add-in's ID) and property set GUID is `{00020329-0000-0000-C000-000000000046}`.</span></span> <span data-ttu-id="5ab7e-161">(Pour plus d’informations sur cet objet, voir[MS-OXCEXT 2.2.5 Propriétés d’Application de messagerie Personnalisées](https://msdn.microsoft.com/library/hh968549(v=exchg.80).aspx).) Vous pouvez ensuite utiliser EWS ou REST pour obtenir cette propriété basée MAPI.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-161">(For more information about this object, see [MS-OXCEXT 2.2.5 Mail App Custom Properties](https://msdn.microsoft.com/library/hh968549(v=exchg.80).aspx).) You can then use EWS or REST to get this MAPI-based property.</span></span>

#### <a name="get-custom-properties-using-ews"></a><span data-ttu-id="5ab7e-162">Obtenir des propriétés personnalisées à l’aide de EWS</span><span class="sxs-lookup"><span data-stu-id="5ab7e-162">Get custom properties using EWS</span></span>

<span data-ttu-id="5ab7e-163">Votre complément de messagerie peut obtenir la `CustomProperties` propriété étendue MAPI à l’aide de l’opération de [GETITEM](/exchange/client-developer/web-service-reference/getitem-operation) de l’EWS.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-163">Your mail add-in can get the `CustomProperties` MAPI-based extended property by using the EWS [GetItem](/exchange/client-developer/web-service-reference/getitem-operation) operation.</span></span> <span data-ttu-id="5ab7e-164">Accès `GetItem` côté serveur à l’aide d’un jeton de rappel ou côté client à l’aide de la méthode [Mailbox. makeEwsRequestAsync](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods) .</span><span class="sxs-lookup"><span data-stu-id="5ab7e-164">Access `GetItem` on the server side by using a callback token, or on the client side by using the [mailbox.makeEwsRequestAsync](../reference/objectmodel/preview-requirement-set/office.context.mailbox.md#methods) method.</span></span> <span data-ttu-id="5ab7e-165">Dans la `GetItem` demande, spécifiez `CustomProperties` la propriété MAPI dans son jeu de propriétés à l’aide des informations fournies dans la section précédente [Comment les propriétés personnalisées sont stockées sur un élément](#how-custom-properties-are-stored-on-an-item).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-165">In the `GetItem` request, specify the `CustomProperties` MAPI-based property in its property set using the details provided in the preceding section [How custom properties are stored on an item](#how-custom-properties-are-stored-on-an-item).</span></span>

<span data-ttu-id="5ab7e-166">L’exemple suivant montre comment obtenir un élément et ses propriétés personnalisées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-166">The following example shows how to get an item and its custom properties.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ab7e-167">Dans l’exemple suivant, remplacez `<app-guid>` par l’ID de votre complément.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-167">In the following example, replace `<app-guid>` with your add-in's ID.</span></span>

```typescript
let request_str =
    '<?xml version="1.0" encoding="utf-8"?>' +
    '<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"' +
                   'xmlns:m="http://schemas.microsoft.com/exchange/services/2006/messages"' +
                   'xmlns:t="http://schemas.microsoft.com/exchange/services/2006/types"' +
                   'xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">' +
        '<soap:Header xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd"' +
                     'xmlns:wsa="http://www.w3.org/2005/08/addressing">' +
            '<t:RequestServerVersion Version="Exchange2010_SP1"/>' +
        '</soap:Header>' +
        '<soap:Body>' +
            '<m:GetItem>' +
                '<m:ItemShape>' +
                    '<t:BaseShape>AllProperties</t:BaseShape>' +
                    '<t:IncludeMimeContent>true</t:IncludeMimeContent>' +
                    '<t:AdditionalProperties>' +
                        '<t:ExtendedFieldURI ' +
                          'DistinguishedPropertySetId="PublicStrings" ' +
                          'PropertyName="cecp-<app-guid>"' +
                          'PropertyType="String" ' +
                        '/>' +
                    '</t:AdditionalProperties>' +
                '</m:ItemShape>' +
                '<m:ItemIds>' +
                    '<t:ItemId Id="' +
                      Office.context.mailbox.item.itemId +
                    '"/>' +
                '</m:ItemIds>' +
            '</m:GetItem>' +
        '</soap:Body>' +
    '</soap:Envelope>';

Office.context.mailbox.makeEwsRequestAsync(
    request_str,
    function(asyncResult) {
        if (asyncResult.status === Office.AsyncResultStatus.Succeeded) {
            console.log(asyncResult.value);
        }
        else {
            console.log(JSON.stringify(asyncResult));
        }
    }
);
```

<span data-ttu-id="5ab7e-168">Vous pouvez également obtenir plus de propriétés personnalisées si vous les spécifiez dans la chaîne de demande, comme les autres éléments [ExtendedFieldURI](/exchange/client-developer/web-service-reference/extendedfielduri).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-168">You can also get more custom properties if you specify them in the request string as other [ExtendedFieldURI](/exchange/client-developer/web-service-reference/extendedfielduri) elements.</span></span>

#### <a name="get-custom-properties-using-rest"></a><span data-ttu-id="5ab7e-169">Obtenir des propriétés personnalisées à l’aide de REST</span><span class="sxs-lookup"><span data-stu-id="5ab7e-169">Get custom properties using REST</span></span>

<span data-ttu-id="5ab7e-170">Dans votre complément, vous pouvez construire votre requête REST contre les messages et événements pour obtenir ceux qui déjà ont des propriétés personnalisées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-170">In your add-in, you can construct your REST query against messages and events to get the ones that already have custom properties.</span></span> <span data-ttu-id="5ab7e-171">Dans la requête, spécifiez la propriété basée MAPI**CustomProperties**dans son ensemble de propriété à l’aide des informations fournies dans la section précédente[Comment les propriétés personnalisées sont stockées sur un élément](#how-custom-properties-are-stored-on-an-item).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-171">In your query, you should include the **CustomProperties** MAPI-based property and its property set using the details provided in the section [How custom properties are stored on an item](#how-custom-properties-are-stored-on-an-item).</span></span>

<span data-ttu-id="5ab7e-172">L’exemple suivant montre comment obtenir tous les événements ayant des propriétés personnalisées définies par votre complément et vous assurer que la réponse inclut la valeur de la propriété pour vous permettre d’appliquer une logique de filtrage.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-172">The following example shows how to get all events that have any custom properties set by your add-in and ensure that the response includes the value of the property so you can apply further filtering logic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ab7e-173">Dans l’exemple suivant, remplacez `<app-guid>` avec l’ID de votre complément.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-173">In the following example, replace `<app-guid>` with your add-in's ID.</span></span>

```rest
GET https://outlook.office.com/api/v2.0/Me/Events?$filter=SingleValueExtendedProperties/Any
  (ep: ep/PropertyId eq 'String {00020329-0000-0000-C000-000000000046}
  Name cecp-<app-guid>' and ep/Value ne null)
  &$expand=SingleValueExtendedProperties($filter=PropertyId eq 'String
  {00020329-0000-0000-C000-000000000046} Name cecp-<app-guid>')
```

<span data-ttu-id="5ab7e-174">Pour plus exemples qui utilisent REST pour obtenir les propriétés étendues à valeur unique base MAPI, voir [Obtenir singleValueExtendedProperty](/graph/api/singlevaluelegacyextendedproperty-get?view=graph-rest-1.0).</span><span class="sxs-lookup"><span data-stu-id="5ab7e-174">For other examples that use REST to get single-value MAPI-based extended properties, see [Get singleValueExtendedProperty](/graph/api/singlevaluelegacyextendedproperty-get?view=graph-rest-1.0).</span></span>

<span data-ttu-id="5ab7e-175">L’exemple suivant montre comment obtenir un élément et ses propriétés personnalisées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-175">The following example shows how to get an item and its custom properties.</span></span> <span data-ttu-id="5ab7e-176">Dans la fonction de rappel pour la méthode `done`, `item.SingleValueExtendedProperties` contient la liste des propriétés personnalisées demandées.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-176">In the callback function for the `done` method, `item.SingleValueExtendedProperties` contains a list of the requested custom properties.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ab7e-177">Dans l’exemple suivant, remplacez `<app-guid>` par l’ID de votre complément.</span><span class="sxs-lookup"><span data-stu-id="5ab7e-177">In the following example, replace `<app-guid>` with your add-in's ID.</span></span>

```typescript
Office.context.mailbox.getCallbackTokenAsync(
    {
        isRest: true
    },
    function (asyncResult) {
        if (asyncResult.status === Office.AsyncResultStatus.Succeeded
            && asyncResult.value !== "") {
            let item_rest_id = Office.context.mailbox.convertToRestId(
                Office.context.mailbox.item.itemId,
                Office.MailboxEnums.RestVersion.v2_0);
            let rest_url = Office.context.mailbox.restUrl +
                           "/v2.0/me/messages('" +
                           item_rest_id +
                           "')";
            rest_url += "?$expand=SingleValueExtendedProperties($filter=PropertyId eq 'String {00020329-0000-0000-C000-000000000046} Name cecp-<app-guid>')";

            let auth_token = asyncResult.value;
            $.ajax(
                {
                    url: rest_url,
                    dataType: 'json',
                    headers:
                        {
                            "Authorization":"Bearer " + auth_token
                        }
                }
                ).done(
                    function (item) {
                        console.log(JSON.stringify(item));
                    }
                ).fail(
                    function (error) {
                        console.log(JSON.stringify(error));
                    }
                );
        } else {
            console.log(JSON.stringify(asyncResult));
        }
    }
);
```

## <a name="see-also"></a><span data-ttu-id="5ab7e-178">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5ab7e-178">See also</span></span>

- [<span data-ttu-id="5ab7e-179">Vue d’ensemble de la propriété MAPI</span><span class="sxs-lookup"><span data-stu-id="5ab7e-179">MAPI Property Overview</span></span>](/office/client-developer/outlook/mapi/mapi-property-overview)
- [<span data-ttu-id="5ab7e-180">Présentation des propriétés Outlook</span><span class="sxs-lookup"><span data-stu-id="5ab7e-180">Outlook Properties Overview</span></span>](/office/vba/outlook/How-to/Navigation/properties-overview)  
- [<span data-ttu-id="5ab7e-181">Utilisation des API REST Outlook d’un complément Outlook</span><span class="sxs-lookup"><span data-stu-id="5ab7e-181">Call Outlook REST APIs from an Outlook add-in</span></span>](use-rest-api.md)
- [<span data-ttu-id="5ab7e-182">Appeler des services web à partir d’un complément Outlook</span><span class="sxs-lookup"><span data-stu-id="5ab7e-182">Call web services from an Outlook add-in</span></span>](web-services.md)
- [<span data-ttu-id="5ab7e-183">Les propriétés et les propriétés étendues dans EWS dans Exchange</span><span class="sxs-lookup"><span data-stu-id="5ab7e-183">Properties and extended properties in EWS in Exchange</span></span>](/exchange/client-developer/exchange-web-services/properties-and-extended-properties-in-ews-in-exchange)
- [<span data-ttu-id="5ab7e-184">Jeux de propriétés et de réponse des formes dans EWS dans Exchange</span><span class="sxs-lookup"><span data-stu-id="5ab7e-184">Property sets and response shapes in EWS in Exchange</span></span>](/exchange/client-developer/exchange-web-services/property-sets-and-response-shapes-in-ews-in-exchange)