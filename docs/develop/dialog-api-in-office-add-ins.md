---
title: Utiliser l’API de dialogue dans vos compléments Office
description: ''
ms.date: 12/04/2017
ms.openlocfilehash: b026c3c5871372c52d0b44e36c01fc44a3d2bf04
ms.sourcegitcommit: c72c35e8389c47a795afbac1b2bcf98c8e216d82
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2018
ms.locfileid: "19437954"
---
# <a name="use-the-dialog-api-in-your-office-add-ins"></a><span data-ttu-id="1b555-102">Utiliser l’API de dialogue dans vos compléments Office</span><span class="sxs-lookup"><span data-stu-id="1b555-102">Use the Dialog API in your Office Add-ins</span></span>

<span data-ttu-id="1b555-p101">Vous pouvez utiliser l’[API de dialogue](https://dev.office.com/reference/add-ins/shared/officeui) pour ouvrir des boîtes de dialogue dans votre complément Office. Cet article fournit des conseils concernant l’utilisation de l’API de dialogue dans votre complément Office.</span><span class="sxs-lookup"><span data-stu-id="1b555-p101">You can use the [Dialog API](https://dev.office.com/reference/add-ins/shared/officeui) to open dialog boxes in your Office Add-in. This article provides guidance for using the Dialog API in your Office Add-in.</span></span>

> [!NOTE]
> <span data-ttu-id="1b555-p102">Pour plus d’informations sur les compléments où l’API de dialogue est actuellement prise en charge, consultez la rubrique relative aux [ensembles de conditions requises de l’API de dialogue](https://dev.office.com/reference/add-ins/requirement-sets/dialog-api-requirement-sets). L’API de dialogue est actuellement prise en charge pour Word, Excel, PowerPoint et Outlook.</span><span class="sxs-lookup"><span data-stu-id="1b555-p102">For information about where the Dialog API is currently supported, see [Dialog API requirement sets](https://dev.office.com/reference/add-ins/requirement-sets/dialog-api-requirement-sets). The Dialog API is currently supported for Word, Excel, PowerPoint, and Outlook.</span></span>

> <span data-ttu-id="1b555-107">Un scénario principal pour l’API de dialogue consiste à activer l’authentification pour une ressource telle que Google ou Facebook.</span><span class="sxs-lookup"><span data-stu-id="1b555-107">A primary scenario for the Dialog APIs is to enable authentication with a resource such as Google or Facebook.</span></span> <span data-ttu-id="1b555-108">Si votre complément nécessite les données relatives à l’utilisateur d’Office ou leurs ressources accessibles via Microsoft Graph, par exemple Office 365 ou OneDrive, nous vous recommandons d’utiliser l’API d’authentification unique chaque fois que possible.</span><span class="sxs-lookup"><span data-stu-id="1b555-108">If your add-in requires data about the Office user or their resources accessible through Microsoft Graph, such as Office 365 or OneDrive, we recommend that you use the single sign-on API whenever you can.</span></span> <span data-ttu-id="1b555-109">Si vous utilisez les API pour l’authentification unique, vous n’aurez pas besoin de l’API de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b555-109">If you use the APIs for single sign-on, then you will not need the Dialog API.</span></span> <span data-ttu-id="1b555-110">Pour plus d’informations, consultez la rubrique [Activer l’authentification unique pour des compléments Office](sso-in-office-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="1b555-110">For details, see [Enable single sign-on for Office Add-ins](sso-in-office-add-ins.md).</span></span>

<span data-ttu-id="1b555-111">Envisagez d’ouvrir une boîte de dialogue à partir d’un volet Office, d’un complément de contenu ou d’un [complément de commande](../design/add-in-commands.md) pour effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b555-111">Consider opening a dialog box from a task pane or content add-in or [add-in command](../design/add-in-commands.md) to do the following:</span></span>

- <span data-ttu-id="1b555-112">afficher les pages de connexion qui ne peuvent pas être ouvertes directement dans un volet Office ;</span><span class="sxs-lookup"><span data-stu-id="1b555-112">Display sign in pages that cannot be opened directly in a task pane.</span></span>
- <span data-ttu-id="1b555-113">fournir davantage d’espace à l’écran, ou même un plein écran, pour certaines tâches exécutées dans votre complément ;</span><span class="sxs-lookup"><span data-stu-id="1b555-113">Provide more screen space, or even a full screen, for some tasks in your add-in.</span></span>
- <span data-ttu-id="1b555-114">héberger une vidéo qui serait trop petite si elle était limitée à un volet Office.</span><span class="sxs-lookup"><span data-stu-id="1b555-114">Host a video that would be too small if confined to a task pane.</span></span>

> [!NOTE]
> <span data-ttu-id="1b555-p104">Comme des éléments d’IU qui se chevauchent peuvent gêner des utilisateurs, évitez d’ouvrir une boîte de dialogue à partir d’un volet Office à moins que votre scénario l’exige. Lorsque vous envisagez d’utiliser la surface d’exposition d’un volet Office, tenez compte du fait que les volets Office peuvent être affichés sous forme d’onglets. Pour voir un exemple, consultez la rubrique relative à l’exemple de [complément Excel JavaScript SalesTracker](https://github.com/OfficeDev/Excel-Add-in-JavaScript-SalesTracker).</span><span class="sxs-lookup"><span data-stu-id="1b555-p104">Because overlapping UI elements are discouraged, avoid opening a dialog from a task pane unless your scenario requires it. When you consider how to use the surface area of a task pane, note that task panes can be tabbed. For an example, see the [Excel Add-in JavaScript SalesTracker](https://github.com/OfficeDev/Excel-Add-in-JavaScript-SalesTracker) sample.</span></span>

<span data-ttu-id="1b555-118">L’image suivante montre un exemple de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b555-118">The following image shows an example of a dialog box.</span></span>

![Commandes de complément](../images/auth-o-dialog-open.png)

<span data-ttu-id="1b555-p105">Notez que la boîte de dialogue s’ouvre toujours au centre de l’écran. L’utilisateur peut la déplacer et la redimensionner. La fenêtre est *non modale* : un utilisateur peut continuer à interagir à la fois avec le document dans l’application Office hôte et avec la page hôte dans le volet Office, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="1b555-p105">Note that the dialog box always opens in the center of the screen. The user can move and resize it. The window is *nonmodal*--a user can continue to interact with both the document in the host Office application and with the host page in the task pane, if there is one.</span></span>

## <a name="dialog-api-scenarios"></a><span data-ttu-id="1b555-123">Scénarios de l’API de dialogue</span><span class="sxs-lookup"><span data-stu-id="1b555-123">Dialog API scenarios</span></span>

<span data-ttu-id="1b555-124">Les API JavaScript Office prennent en charge les scénarios suivants avec un objet [Dialog](https://dev.office.com/reference/add-ins/shared/officeui.dialog) et deux fonctions dans l’[espace de noms Office.context.ui](https://dev.office.com/reference/add-ins/shared/officeui).</span><span class="sxs-lookup"><span data-stu-id="1b555-124">The Office JavaScript APIs support the following scenarios with a [Dialog](https://dev.office.com/reference/add-ins/shared/officeui.dialog) object and two functions in the [Office.context.ui namespace](https://dev.office.com/reference/add-ins/shared/officeui).</span></span>

### <a name="open-a-dialog-box"></a><span data-ttu-id="1b555-125">Ouvrir une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b555-125">Open a dialog box</span></span>

<span data-ttu-id="1b555-p106">Pour ouvrir une boîte de dialogue, votre code dans le volet Office appelle la méthode [displayDialogAsync](https://dev.office.com/reference/add-ins/shared/officeui.displaydialogasync) et lui transmet l’URL de la ressource que vous voulez ouvrir. Il s’agit généralement d’une page, mais ce peut être une méthode du contrôleur dans une application MVC, un itinéraire, une méthode de service web ou toute autre ressource. Dans cet article, les termes « page » ou « site web » font référence à la ressource dans la boîte de dialogue. Le code suivant est un exemple simple.</span><span class="sxs-lookup"><span data-stu-id="1b555-p106">To open a dialog box, your code in the task pane calls the [displayDialogAsync](https://dev.office.com/reference/add-ins/shared/officeui.displaydialogasync) method and passes to it the URL of the resource that you want to open. This is usually a page, but it can be a controller method in an MVC application, a route, a web service method, or any other resource. In this article, 'page' or 'website' refers to the resource in the dialog. The following code is a simple example:</span></span>

```js
Office.context.ui.displayDialogAsync('https://myAddinDomain/myDialog.html');
```

> [!NOTE]
> - <span data-ttu-id="1b555-p107">L’URL utilise le protocole HTTP**S**. Ceci est obligatoire pour toutes les pages chargées dans une boîte de dialogue, pas seulement la première page chargée.</span><span class="sxs-lookup"><span data-stu-id="1b555-p107">The URL uses the HTTP**S** protocol. This is mandatory for all pages loaded in a dialog box, not just the first page loaded.</span></span>
> - <span data-ttu-id="1b555-p108">Le domaine est le même que celui de la page hôte, qui peut être la page d’un volet Office ou le [fichier de fonctions](https://dev.office.com/reference/add-ins/manifest/functionfile) d’une commande de complément. Obligatoire : la page, la méthode du contrôleur ou toute autre ressource qui est transmise à la méthode `displayDialogAsync` doit se trouver dans le même domaine que la page hôte.</span><span class="sxs-lookup"><span data-stu-id="1b555-p108">The domain is the same as the domain of the host page, which can be the page in a task pane or the [function file](https://dev.office.com/reference/add-ins/manifest/functionfile) of an add-in command. This is required: the page, controller method, or other resource that is passed to the `displayDialogAsync` method must be in the same domain as the host page.</span></span>

<span data-ttu-id="1b555-p109">Une fois que la première page (ou toute autre ressource) est chargée, un utilisateur peut accéder à n’importe quel site web (ou n’importe quelle autre ressource) qui utilise le protocole HTTPS. Vous pouvez également concevoir la première page de façon à ce que l’utilisateur soit immédiatement redirigé vers un autre site.</span><span class="sxs-lookup"><span data-stu-id="1b555-p109">After the first page (or other resource) is loaded, a user can go to any website (or other resource) that uses HTTPS. You can also design the first page to immediately redirect to another site.</span></span>

<span data-ttu-id="1b555-136">Par défaut, la boîte de dialogue occupera 80 % de la hauteur et de la largeur de l’écran de l’appareil, mais vous pouvez définir des pourcentages différents en transmettant un objet de configuration à la méthode, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1b555-136">By default, the dialog box will occupy 80% of the height and width of the device screen, but you can set different percentages by passing a configuration object to the method, as shown in the following example:</span></span>

```js
Office.context.ui.displayDialogAsync('https://myDomain/myDialog.html', {height: 30, width: 20});
```

<span data-ttu-id="1b555-137">Pour voir un exemple de complément qui effectue ce type d’action, consultez la rubrique relative à l’[exemple d’API de dialogue de complément Office](https://github.com/OfficeDev/Office-Add-in-Dialog-API-Simple-Example).</span><span class="sxs-lookup"><span data-stu-id="1b555-137">For a sample add-in that does this, see [Office Add-in Dialog API Example](https://github.com/OfficeDev/Office-Add-in-Dialog-API-Simple-Example).</span></span>

<span data-ttu-id="1b555-p110">Définissez les deux valeurs sur 100 % pour bénéficier d’une réelle d’expérience de plein écran. (Le maximum réel est de 99,5 %, et la fenêtre peut toujours être déplacée et redimensionnée.)</span><span class="sxs-lookup"><span data-stu-id="1b555-p110">Set both values to 100% to get what is effectively a full screen experience. (The effective maximum is 99.5%, and the window is still moveable and resizable.)</span></span>

> [!NOTE]
> <span data-ttu-id="1b555-p111">Vous ne pouvez ouvrir qu’une seule boîte de dialogue à partir d’une fenêtre hôte. Toute tentative d’ouverture d’une autre boîte de dialogue génère une erreur. Par exemple, si un utilisateur ouvre une boîte de dialogue à partir d’un volet Office, il ne peut pas ouvrir une seconde boîte de dialogue à partir d’une autre page dans le volet Office. Toutefois, quand une boîte de dialogue est ouverte à partir d’une [commande de complément](../design/add-in-commands.md), la commande ouvre un nouveau fichier HTML (mais invisible) chaque fois qu’elle est sélectionnée. Cela crée une nouvelle fenêtre hôte (invisible), afin que chaque fenêtre de ce type puisse lancer sa propre boîte de dialogue. Pour plus d’informations, reportez-vous à [Erreurs provenant de displayDialogAsync](#errors-from-displaydialogasync).</span><span class="sxs-lookup"><span data-stu-id="1b555-p111">You can open only one dialog box from a host window. An attempt to open another dialog box generates an error. For example, if a user opens a dialog box from a task pane, she cannot open a second dialog box, from a different page in the task pane. However, when a dialog box is opened from an [add-in command](../design/add-in-commands.md), the command opens a new (but unseen) HTML file each time it is selected. This creates a new (unseen) host window, so each such window can launch its own dialog box. For more information, see [Errors from displayDialogAsync](#errors-from-displaydialogasync).</span></span>

### <a name="take-advantage-of-a-performance-option-in-office-online"></a><span data-ttu-id="1b555-146">Tirer parti d’une option de performances dans Office Online</span><span class="sxs-lookup"><span data-stu-id="1b555-146">Take advantage of a performance option in Office Online</span></span>

<span data-ttu-id="1b555-p112">La propriété `displayInIframe` est une propriété supplémentaire dans l’objet de configuration que vous pouvez transmettre à `displayDialogAsync`. Lorsque cette propriété est définie sur `true` et que le complément est en cours d’exécution dans un document ouvert dans Office Online, la boîte de dialogue s’ouvre sous la forme d’un iFrame flottant et non d’une fenêtre indépendante. Elle s’ouvre ainsi plus rapidement. Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b555-p112">The `displayInIframe` property is an additional property in the configuration object that you can pass to `displayDialogAsync`. When this property is set to `true`, and the add-in is running in a document opened in Office Online, the dialog box will open as a floating iframe rather than an independent window, which makes it open faster. The following is an example:</span></span>

```js
Office.context.ui.displayDialogAsync('https://myDomain/myDialog.html', {height: 30, width: 20, displayInIframe: true});
```

<span data-ttu-id="1b555-150">La valeur par défaut est `false`, ce qui revient à omettre entièrement la propriété.</span><span class="sxs-lookup"><span data-stu-id="1b555-150">The default value is `false`, which is the same as omitting the property entirely.</span></span> <span data-ttu-id="1b555-151">Si le complément n’est pas exécuté dans Office Online, le `displayInIframe` est ignoré.</span><span class="sxs-lookup"><span data-stu-id="1b555-151">If the add-in is not running in Office Online, the `displayInIframe` is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="1b555-p114">Vous ne devez **pas** utiliser `displayInIframe: true` si la boîte de dialogue redirige à un moment donné l’utilisateur vers une page qui ne peut pas être ouverte dans un iFrame. Par exemple, les pages de connexion de nombreux services web connus, comme un compte Microsoft et Google, ne peuvent pas être ouvertes dans un iFrame.</span><span class="sxs-lookup"><span data-stu-id="1b555-p114">You should **not** use `displayInIframe: true` if the dialog will at any point redirect to a page that cannot be opened in an iframe. For example, the sign in pages of many popular web services, such as Google and Microsoft Account, cannot be opened in an iframe.</span></span>

### <a name="send-information-from-the-dialog-box-to-the-host-page"></a><span data-ttu-id="1b555-154">Envoi d’informations à la page hôte à partir de la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="1b555-154">Send information from the dialog box to the host page</span></span>

<span data-ttu-id="1b555-155">La boîte de dialogue ne peut pas communiquer avec la page hôte dans le volet Office, sauf si :</span><span class="sxs-lookup"><span data-stu-id="1b555-155">The dialog box cannot communicate with the host page in the task pane unless:</span></span>

- <span data-ttu-id="1b555-156">la page active dans la boîte de dialogue se trouve dans le même domaine que la page hôte ;</span><span class="sxs-lookup"><span data-stu-id="1b555-156">The current page in the dialog box is in the same domain as the host page.</span></span>
- <span data-ttu-id="1b555-p115">la bibliothèque JavaScript Office est chargée dans la page. (Comme n’importe quelle page qui utilise la bibliothèque JavaScript Office, le script de la page doit attribuer une méthode à la propriété `Office.initialize`, bien qu’il puisse s’agir d’une méthode vide. Pour plus d’informations, voir [Initialisation de votre complément](understanding-the-javascript-api-for-office.md#initializing-your-add-in).)</span><span class="sxs-lookup"><span data-stu-id="1b555-p115">The Office JavaScript library is loaded in the page. (Like any page that uses the Office JavaScript library, script for the page must assign a method to the `Office.initialize` property, although it can be an empty method. For details, see [Initializing your add-in](understanding-the-javascript-api-for-office.md#initializing-your-add-in).)</span></span>

<span data-ttu-id="1b555-p116">Le code de la page de boîte de dialogue utilise la fonction `messageParent` pour envoyer une valeur booléenne ou un message de type chaîne à la page hôte. La chaîne peut être un mot, une phrase, un blob XML, un JSON converti en chaîne ou un autre élément pouvant être sérialisé en chaîne. Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b555-p116">Code in the dialog page uses the `messageParent` function to send either a Boolean value or a string message to the host page. The string can be a word, sentence, XML blob, stringified JSON, or anything else that can be serialized to a string. The following is an example:</span></span>

```js
if (loginSuccess) {
    Office.context.ui.messageParent(true);
}
```

> [!NOTE]
> - <span data-ttu-id="1b555-p117">La fonction `messageParent` est l’une des deux *seules* API Office pouvant être appelées dans la boîte de dialogue. L’autre est `Office.context.requirements.isSetSupported`. Pour plus d’informations, consultez la rubrique relative à la [spécification d’hôtes Office et de conditions requises d’API](specify-office-hosts-and-api-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="1b555-p117">The `messageParent` function is one of *only* two Office APIs that can be called in the dialog box. The other is `Office.context.requirements.isSetSupported`. For information about it, see [Specify Office hosts and API requirements](specify-office-hosts-and-api-requirements.md).</span></span>
> - <span data-ttu-id="1b555-166">La fonction `messageParent` peut uniquement être appelée sur une page ayant le même domaine (y compris les mêmes protocole et port) que la page hôte.</span><span class="sxs-lookup"><span data-stu-id="1b555-166">The `messageParent` function can only be called on a page with the same domain (including protocol and port) as the host page.</span></span>

<span data-ttu-id="1b555-167">Dans l’exemple suivant, `googleProfile` est une version convertie en chaîne du profil Google de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1b555-167">In the next example, `googleProfile` is a stringified version of the user's Google profile.</span></span>

```js
if (loginSuccess) {
    Office.context.ui.messageParent(googleProfile);
}
```

<span data-ttu-id="1b555-p118">La page hôte doit être configurée de façon à recevoir le message. Pour ce faire, ajoutez un paramètre de rappel à l’appel d’origine de `displayDialogAsync`. Le rappel attribue un gestionnaire à l’événement `DialogMessageReceived`. Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b555-p118">The host page must be configured to receive the message. You do this by adding a callback parameter to the original call of `displayDialogAsync`. The callback assigns a handler to the `DialogMessageReceived` event. The following is an example:</span></span>

```js
var dialog;
Office.context.ui.displayDialogAsync('https://myDomain/myDialog.html', {height: 30, width: 20},
    function (asyncResult) {
        dialog = asyncResult.value;
        dialog.addEventHandler(Office.EventType.DialogMessageReceived, processMessage);
    }
);
```

> [!NOTE]
> - <span data-ttu-id="1b555-p119">Office transmet un objet [AsyncResult](https://dev.office.com/reference/add-ins/shared/asyncresult) au rappel. Il représente le résultat de la tentative d’ouverture de la boîte de dialogue. Il ne représente pas le résultat de tous les événements dans la boîte de dialogue. Pour plus d’informations sur cette distinction, consultez la section [Gestion des erreurs et des événements](#handle-errors-and-events).</span><span class="sxs-lookup"><span data-stu-id="1b555-p119">Office passes an [AsyncResult](https://dev.office.com/reference/add-ins/shared/asyncresult) object to the callback. It represents the result of the attempt to open the dialog box. It does not represent the outcome of any events in the dialog box. For more on this distinction, see the section [Handle errors and events](#handle-errors-and-events).</span></span>
> - <span data-ttu-id="1b555-176">La propriété `value` de `asyncResult` est définie sur un objet [Dialog](https://dev.office.com/reference/add-ins/shared/officeui.dialog), qui existe dans la page hôte, pas dans le contexte d’exécution de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b555-176">The `value` property of the `asyncResult` is set to a [Dialog](https://dev.office.com/reference/add-ins/shared/officeui.dialog) object, which exists in the host page, not in the dialog box's execution context.</span></span>
> - <span data-ttu-id="1b555-p120">est la fonction qui gère l’événement. Vous pouvez lui donner le nom que vous souhaitez.`processMessage`</span><span class="sxs-lookup"><span data-stu-id="1b555-p120">The `processMessage` is the function that handles the event. You can give it any name you want.</span></span>
> - <span data-ttu-id="1b555-179">La variable `dialog` est déclarée avec une portée plus large que le rappel, car elle est également référencée dans `processMessage`.</span><span class="sxs-lookup"><span data-stu-id="1b555-179">The `dialog` variable is declared at a wider scope than the callback because it is also referenced in `processMessage`.</span></span>

<span data-ttu-id="1b555-180">Voici un exemple simple de gestionnaire pour l’événement `DialogMessageReceived` :</span><span class="sxs-lookup"><span data-stu-id="1b555-180">The following is a simple example of a handler for the `DialogMessageReceived` event:</span></span>

```js
function processMessage(arg) {
    var messageFromDialog = JSON.parse(arg.message);
    showUserName(messageFromDialog.name);
}
```

> [!NOTE]
> - <span data-ttu-id="1b555-p121">Office transmet l’objet `arg` au gestionnaire. Sa propriété `message` est la valeur booléenne ou la chaîne envoyée par l’appel de `messageParent` dans la boîte de dialogue. Dans cet exemple, il s’agit d’une représentation convertie en chaîne du profil de l’utilisateur à partir d’un service tel qu’un compte Microsoft ou Google, qui est donc désérialisé en objet avec `JSON.parse`.</span><span class="sxs-lookup"><span data-stu-id="1b555-p121">Office passes the `arg` object to the handler. Its `message` property is the Boolean or string sent by the call of `messageParent` in the dialog. In this example, it is a stringified representation of a user's profile from a service such as Microsoft Account or Google, so it is deserialized back to an object with `JSON.parse`.</span></span>
> - <span data-ttu-id="1b555-p122">L’implémentation `showUserName` n’est pas visible. Elle peut afficher un message de bienvenue personnalisé dans le volet Office.</span><span class="sxs-lookup"><span data-stu-id="1b555-p122">The `showUserName` implementation is not shown. It might display a personalized welcome message on the task pane.</span></span>

<span data-ttu-id="1b555-186">Lorsque l’intervention de l’utilisateur sur la boîte de dialogue est terminée, votre gestionnaire de messages doit fermer la boîte de dialogue, comme indiqué dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="1b555-186">When the user interaction with the dialog box is completed, your message handler should close the dialog box, as shown in this example.</span></span>

```js
function processMessage(arg) {
    dialog.close();
    // message processing code goes here;
}
```

> [!NOTE]
> - <span data-ttu-id="1b555-187">L’objet `dialog` doit être le même que celui renvoyé par l’appel de `displayDialogAsync`.</span><span class="sxs-lookup"><span data-stu-id="1b555-187">The `dialog` object must be the same one that is returned by the call of `displayDialogAsync`.</span></span>
> - <span data-ttu-id="1b555-188">L’appel de `dialog.close` indique à Office de fermer immédiatement la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b555-188">The call of `dialog.close` tells Office to immediately close the dialog box.</span></span>

<span data-ttu-id="1b555-189">Pour voir un exemple de complément qui utilise ces techniques, consultez la rubrique relative à l’[exemple d’API de dialogue de complément Office](https://github.com/OfficeDev/Office-Add-in-Dialog-API-Simple-Example).</span><span class="sxs-lookup"><span data-stu-id="1b555-189">For a sample add-in that uses these techniques, see [Office Add-in Dialog API Example](https://github.com/OfficeDev/Office-Add-in-Dialog-API-Simple-Example).</span></span>

<span data-ttu-id="1b555-p123">Si le complément a besoin d’ouvrir une autre page du volet Office après avoir reçu le message, vous pouvez utiliser la méthode `window.location.replace` (ou `window.location.href`) en tant que dernière ligne du gestionnaire. Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b555-p123">If the add-in needs to open a different page of the task pane after receiving the message, you can use the `window.location.replace` method (or `window.location.href`) as the last line of the handler. The following is an example:</span></span>

```js
function processMessage(arg) {
    // message processing code goes here;
    window.location.replace("/newPage.html");
    // Alternatively ...
    // window.location.href = "/newPage.html";
}
```

<span data-ttu-id="1b555-192">Pour voir un exemple de complément qui effectue ce type d’action, consultez la rubrique relative à l’exemple [Insérer des graphiques Excel à l’aide de Microsoft Graph dans un complément PowerPoint](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart).</span><span class="sxs-lookup"><span data-stu-id="1b555-192">For an example of an add-in that does this, see the [Insert Excel charts using Microsoft Graph in a PowerPoint Add-in](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart) sample.</span></span>

#### <a name="conditional-messaging"></a><span data-ttu-id="1b555-193">Messagerie conditionnelle</span><span class="sxs-lookup"><span data-stu-id="1b555-193">Conditional messaging</span></span>
<span data-ttu-id="1b555-p124">Étant donné que vous pouvez envoyer plusieurs appels `messageParent` à partir de la boîte de dialogue, mais que vous n’avez qu’un seul gestionnaire dans la page hôte pour l’événement `DialogMessageReceived`, le gestionnaire doit utiliser la logique conditionnelle pour distinguer les différents messages. Par exemple, si la boîte de dialogue invite un utilisateur à se connecter à un fournisseur d’identité tel qu’un compte Microsoft ou Google, elle envoie le profil de l’utilisateur sous la forme d’un message. Si l’authentification échoue, la boîte de dialogue envoie des informations sur l’erreur à la page hôte, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1b555-p124">Because you can send multiple `messageParent` calls from the dialog box, but you have only one handler in the host page for the `DialogMessageReceived` event, the handler must use conditional logic to distinguish different messages. For example, if the dialog box prompts a user to sign in to an identity provider such as Microsoft Account or Google, it sends the user's profile as a message. If authentication fails, the dialog box sends error information to the host page, as in the following example:</span></span>

```js
if (loginSuccess) {
    var userProfile = getProfile();
    var messageObject = {messageType: "signinSuccess", profile: userProfile};            
    var jsonMessage = JSON.stringify(messageObject);
    Office.context.ui.messageParent(jsonMessage);
} else {
    var errorDetails = getError();
    var messageObject = {messageType: "signinFailure", error: errorDetails};            
    var jsonMessage = JSON.stringify(messageObject);
    Office.context.ui.messageParent(jsonMessage);
}
```

> [!NOTE]
> - <span data-ttu-id="1b555-197">La variable `loginSuccess` serait initialisée en lisant la réponse HTTP à partir du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="1b555-197">The `loginSuccess` variable would be initialized by reading the HTTP response from the identity provider.</span></span>
> - <span data-ttu-id="1b555-p125">L’implémentation des fonctions `getProfile` et `getError` n’est pas affichée. Chacune obtient des données à partir d’un paramètre de requête ou du corps de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="1b555-p125">The the implementation of the `getProfile` and `getError` functions are not not shown. They each get data from a query parameter or from the body of the HTTP response.</span></span>
> - <span data-ttu-id="1b555-p126">Des objets anonymes de différents types sont envoyés selon que la connexion a réussi ou non. Tous deux ont une propriété `messageType`, mais un a une propriété `profile` et l’autre une propriété `error`.</span><span class="sxs-lookup"><span data-stu-id="1b555-p126">Anonymous objects of different types are sent depending on whether the sign in was successful. Both have a `messageType` property, but one has a `profile` property and the other has an `error` property.</span></span>

<span data-ttu-id="1b555-202">Pour obtenir des exemples qui utilisent la messagerie conditionnelle, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b555-202">For samples that use conditional messaging, see:</span></span>
- [<span data-ttu-id="1b555-203">Complément Office qui utilise le service Auth0 pour simplifier la connexion sociale</span><span class="sxs-lookup"><span data-stu-id="1b555-203">Office Add-in that uses the Auth0 Service to Simplify Social Login</span></span>](https://github.com/OfficeDev/Office-Add-in-Auth0)
- [<span data-ttu-id="1b555-204">Complément Office qui utilise le service OAuth.io pour simplifier l’accès aux services en ligne populaires</span><span class="sxs-lookup"><span data-stu-id="1b555-204">Office Add-in that uses the OAuth.io Service to Simplify Access to Popular Online Services</span></span>](https://github.com/OfficeDev/Office-Add-in-OAuth.io)

<span data-ttu-id="1b555-p127">Le code du gestionnaire dans la page hôte utilise la valeur de la propriété `messageType` pour créer une branche comme le montre l’exemple suivant. Notez que la fonction `showUserName` est identique à celle de l’exemple précédent et que la fonction `showNotification` affiche l’erreur dans l’interface utilisateur de la page hôte.</span><span class="sxs-lookup"><span data-stu-id="1b555-p127">The handler code in the host page uses the value of the `messageType` property to branch as shown in the following example. Note that the `showUserName` function is the same as in the previous example and `showNotification` function displays the error in the host page's UI.</span></span>

```js
function processMessage(arg) {
    var messageFromDialog = JSON.parse(arg.message);
    if (messageFromDialog.messageType === "signinSuccess") {
        dialog.close();
        showUserName(messageFromDialog.profile.name);
        window.location.replace("/newPage.html");
    } else {
        dialog.close();
        showNotification("Unable to authenticate user: " + messageFromDialog.error);
    }
}
```

### <a name="closing-the-dialog-box"></a><span data-ttu-id="1b555-207">Fermeture de la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="1b555-207">Closing the dialog box</span></span>

<span data-ttu-id="1b555-p128">Vous pouvez implémenter un bouton de fermeture dans la boîte de dialogue. Pour ce faire, le gestionnaire d’événements Click du bouton doit utiliser `messageParent` pour indiquer à la page hôte que vous avez cliqué sur le bouton. Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="1b555-p128">You can implement a button in the dialog box that will close it. To do this, the click event handler for the button should use `messageParent` to tell the host page that the button has been clicked. The following is an example:</span></span>

```js
function closeButtonClick() {
    var messageObject = {messageType: "dialogClosed"};            
    var jsonMessage = JSON.stringify(messageObject);
    Office.context.ui.messageParent(jsonMessage);
}
```

<span data-ttu-id="1b555-p129">Le gestionnaire de la page hôte pour `DialogMessageReceived` appelle `dialog.close`, comme dans cet exemple. (Consultez les exemples précédents qui montrent comment l’objet Dialog est initialisé.)</span><span class="sxs-lookup"><span data-stu-id="1b555-p129">The host page handler for `DialogMessageReceived` would call `dialog.close`, as in this example. (See previous examples that show how the dialog object is initialized.)</span></span>


```js
function processMessage(arg) {
    var messageFromDialog = JSON.parse(arg.message);
    if (messageFromDialog.messageType === "dialogClosed") {
       dialog.close();
    }
}
```

<span data-ttu-id="1b555-213">Pour voir un exemple qui utilise cette technique, consultez le [modèle de conception de navigation de boîte de dialogue](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code/tree/master/templates/dialog/navigation) dans le référentiel de [modèles de conception de l’expérience utilisateur pour compléments Office](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code).</span><span class="sxs-lookup"><span data-stu-id="1b555-213">For a sample that uses this technique, see the [dialog navigation design pattern](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code/tree/master/templates/dialog/navigation) in the [UX design patterns for Office Add-ins](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code) repo.</span></span>

<span data-ttu-id="1b555-p130">Même lorsque vous ne disposez pas de votre propre IU de fermeture de boîte de dialogue, un utilisateur final peut fermer la boîte de dialogue en choisissant le **X** dans le coin supérieur droit. Cette action déclenche l’événement `DialogEventReceived`. Si votre volet hôte a besoin de savoir quand cela se produit, il doit déclarer un gestionnaire pour cet événement. Pour plus d’informations, consultez la section [Erreurs et événements dans la fenêtre de dialogue](#errors-and-events-in-the-dialog-window).</span><span class="sxs-lookup"><span data-stu-id="1b555-p130">Even when you don't have your own close dialog UI, an end user can close the dialog box by choosing the **X** in the upper-right corner. This action triggers the `DialogEventReceived` event. If your host pane needs to know when this happens, it should declare a handler for this event. See the section [Errors and events in the dialog window](#errors-and-events-in-the-dialog-window) for details.</span></span>

## <a name="handle-errors-and-events"></a><span data-ttu-id="1b555-218">Gestion des erreurs et des événements</span><span class="sxs-lookup"><span data-stu-id="1b555-218">Handle errors and events</span></span>

<span data-ttu-id="1b555-219">Votre code doit gérer deux catégories d’événements :</span><span class="sxs-lookup"><span data-stu-id="1b555-219">Your code should handle two categories of events:</span></span>

- <span data-ttu-id="1b555-220">les erreurs renvoyées par l’appel de `displayDialogAsync` car la boîte de dialogue ne peut pas être créée ;</span><span class="sxs-lookup"><span data-stu-id="1b555-220">Errors returned by the call of `displayDialogAsync` because the dialog box cannot be created.</span></span>
- <span data-ttu-id="1b555-221">les erreurs, et autres événements, dans la fenêtre de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b555-221">Errors, and other events, in the dialog window.</span></span>

### <a name="errors-from-displaydialogasync"></a><span data-ttu-id="1b555-222">Erreurs provenant de displayDialogAsync</span><span class="sxs-lookup"><span data-stu-id="1b555-222">Errors from displayDialogAsync</span></span>

<span data-ttu-id="1b555-223">En plus des erreurs système et de plateforme générales, trois erreurs sont propres à l’appel de `displayDialogAsync`.</span><span class="sxs-lookup"><span data-stu-id="1b555-223">In addition to general platform and system errors, three errors are specific to calling `displayDialogAsync`.</span></span>

|<span data-ttu-id="1b555-224">Numéro de code</span><span class="sxs-lookup"><span data-stu-id="1b555-224">Code number</span></span>|<span data-ttu-id="1b555-225">Signification</span><span class="sxs-lookup"><span data-stu-id="1b555-225">Meaning</span></span>|
|:-----|:-----|
|<span data-ttu-id="1b555-226">12004</span><span class="sxs-lookup"><span data-stu-id="1b555-226">12004</span></span>|<span data-ttu-id="1b555-p131">Le domaine de l’URL transmis à `displayDialogAsync` n’est pas approuvé. Le domaine doit être le même domaine que celui de la page hôte (y compris le protocole et le numéro de port).</span><span class="sxs-lookup"><span data-stu-id="1b555-p131">The domain of the URL passed to `displayDialogAsync` is not trusted. The domain must be the same domain as the host page (including protocol and port number).</span></span>|
|<span data-ttu-id="1b555-229">12005</span><span class="sxs-lookup"><span data-stu-id="1b555-229">12005</span></span>|<span data-ttu-id="1b555-p132">L’URL transmise à `displayDialogAsync` utilise le protocole HTTP. C’est le protocole HTTPS qui est requis. (Dans certaines versions d’Office, le message d’erreur renvoyé avec le code 12005 est identique à celui renvoyé avec le code 12004.)</span><span class="sxs-lookup"><span data-stu-id="1b555-p132">The URL passed to `displayDialogAsync` uses the HTTP protocol. HTTPS is required. (In some versions of Office, the error message returned with 12005 is the same one returned for 12004.)</span></span>|
|<span data-ttu-id="1b555-233"><span id="12007">12007</span></span><span class="sxs-lookup"><span data-stu-id="1b555-233"><span id="12007">12007</span></span></span>|<span data-ttu-id="1b555-p133">Une boîte de dialogue est déjà ouverte à partir de cette fenêtre hôte. Une fenêtre hôte, par exemple un volet Office, ne peut avoir qu’une seule boîte de dialogue ouverte à la fois.</span><span class="sxs-lookup"><span data-stu-id="1b555-p133">A dialog box is already opened from this host window. A host window, such as a task pane, can only have one dialog box open at a time.</span></span>|

<span data-ttu-id="1b555-p134">Lorsque `displayDialogAsync` est appelé, il transmet toujours un objet [AsyncResult](https://dev.office.com/reference/add-ins/shared/asyncresult) à sa fonction de rappel. Lorsque l’appel réussit (autrement dit, que la fenêtre de dialogue est ouverte), la propriété `value` de l’objet `AsyncResult` est un objet [Dialog](https://dev.office.com/reference/add-ins/shared/officeui.dialog). Vous trouverez un exemple dans la section [Envoi d’informations à la page hôte à partir de la boîte de dialogue](#send-information-from-the-dialog-box-to-the-host-page). Lorsque l’appel de `displayDialogAsync` échoue, la fenêtre n’est pas créée, la propriété `status` de l’objet `AsyncResult` est définie sur « failed » et la propriété `error` de l’objet est renseignée. Vous devez toujours disposer d’un rappel qui teste `status` et répond lorsqu’il s’agit d’une erreur. Voici un exemple de code qui signale simplement le message d’erreur, quel que soit son numéro de code :</span><span class="sxs-lookup"><span data-stu-id="1b555-p134">When `displayDialogAsync` is called, it always passes an [AsyncResult](https://dev.office.com/reference/add-ins/shared/asyncresult) object to its callback function. When the call is successful - that is, the dialog window is opened - the `value` property of the `AsyncResult` object is a [Dialog](https://dev.office.com/reference/add-ins/shared/officeui.dialog) object. An example of this is in the section [Send information from the dialog box to the host page](#send-information-from-the-dialog-box-to-the-host-page). When the call to `displayDialogAsync` fails, the window is not created, the `status` property of the `AsyncResult` object is set to "failed", and the `error` property of the object is populated. You should always have a callback that tests the `status` and responds when it's an error. For an example that simply reports the error message regardless of its code number, see the following code:</span></span>

```js
var dialog;
Office.context.ui.displayDialogAsync('https://myDomain/myDialog.html',
function (asyncResult) {
    if (asyncResult.status === "failed") {
        showNotification(asynceResult.error.code = ": " + asyncResult.error.message);
    } else {
        dialog = asyncResult.value;
        dialog.addEventHandler(Office.EventType.DialogMessageReceived, processMessage);
    }
});
```

### <a name="errors-and-events-in-the-dialog-window"></a><span data-ttu-id="1b555-242">Erreurs et événements dans la fenêtre de dialogue</span><span class="sxs-lookup"><span data-stu-id="1b555-242">Errors and events in the dialog window</span></span>

<span data-ttu-id="1b555-243">Trois erreurs et événements, désignés par leur numéro de code, dans la boîte de dialogue déclencheront un événement `DialogEventReceived` dans la page hôte.</span><span class="sxs-lookup"><span data-stu-id="1b555-243">Three errors and events, known by their code numbers, in the dialog box will trigger a `DialogEventReceived` event in the host page.</span></span>

|<span data-ttu-id="1b555-244">Numéro de code</span><span class="sxs-lookup"><span data-stu-id="1b555-244">Code number</span></span>|<span data-ttu-id="1b555-245">Signification</span><span class="sxs-lookup"><span data-stu-id="1b555-245">Meaning</span></span>|
|:-----|:-----|
|<span data-ttu-id="1b555-246">12002</span><span class="sxs-lookup"><span data-stu-id="1b555-246">12002</span></span>|<span data-ttu-id="1b555-247">Un des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1b555-247">One of the following:</span></span><br> <span data-ttu-id="1b555-248">- Aucune page n’existe à l’URL qui a été transmise à `displayDialogAsync`.</span><span class="sxs-lookup"><span data-stu-id="1b555-248">- No page exists at the URL that was passed to `displayDialogAsync`.</span></span><br> <span data-ttu-id="1b555-249">- La page qui a été transmise à `displayDialogAsync` a été chargée, mais la boîte de dialogue a été redirigée vers une page introuvable ou impossible à charger, ou a été redirigée vers une URL dont la syntaxe n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="1b555-249">- The page that was passed to `displayDialogAsync` loaded, but the dialog box was directed to a page that it cannot find or load, or it has been directed to a URL with invalid syntax.</span></span>|
|<span data-ttu-id="1b555-250">12003</span><span class="sxs-lookup"><span data-stu-id="1b555-250">12003</span></span>|<span data-ttu-id="1b555-p135">La boîte de dialogue a été redirigée vers une URL avec le protocole HTTP. C’est le protocole HTTPS qui est requis.</span><span class="sxs-lookup"><span data-stu-id="1b555-p135">The dialog box was directed to a URL with the HTTP protocol. HTTPS is required.</span></span>|
|<span data-ttu-id="1b555-253">12006</span><span class="sxs-lookup"><span data-stu-id="1b555-253">12006</span></span>|<span data-ttu-id="1b555-254">La boîte de dialogue a été fermée, généralement parce que l’utilisateur choisit le bouton **X**.</span><span class="sxs-lookup"><span data-stu-id="1b555-254">The dialog box was closed, usually because the user chooses the **X** button.</span></span>|

<span data-ttu-id="1b555-p136">Votre code peut attribuer un gestionnaire pour l’événement `DialogEventReceived` dans l’appel de `displayDialogAsync`. Voici un exemple simple :</span><span class="sxs-lookup"><span data-stu-id="1b555-p136">Your code can assign a handler for the `DialogEventReceived` event in the call to `displayDialogAsync`. The following is a simple example:</span></span>

```js
var dialog;
Office.context.ui.displayDialogAsync('https://myDomain/myDialog.html',
    function (result) {
        dialog = result.value;
        dialog.addEventHandler(Office.EventType.DialogEventReceived, processDialogEvent);
    }
);
```

<span data-ttu-id="1b555-257">Pour voir un exemple de gestionnaire pour l’événement `DialogEventReceived` qui crée des messages d’erreur personnalisés pour chaque code d’erreur, consultez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1b555-257">For an example of a handler for the `DialogEventReceived` event that creates custom error messages for each error code, see the following example:</span></span>

```js
function processDialogEvent(arg) {
    switch (arg.error) {
        case 12002:
            showNotification("The dialog box has been directed to a page that it cannot find or load, or the URL syntax is invalid.");
            break;
        case 12003:
            showNotification("The dialog box has been directed to a URL with the HTTP protocol. HTTPS is required.");            break;
        case 12006:
            showNotification("Dialog closed.");
            break;
        default:
            showNotification("Unknown error in dialog box.");
            break;
    }
}
```

<span data-ttu-id="1b555-258">Pour voir un exemple de complément qui gère les erreurs de cette façon, consultez la rubrique relative à l’[exemple d’API de dialogue de complément Office](https://github.com/OfficeDev/Office-Add-in-Dialog-API-Simple-Example).</span><span class="sxs-lookup"><span data-stu-id="1b555-258">For a sample add-in that handles errors in this way, see [Office Add-in Dialog API Example](https://github.com/OfficeDev/Office-Add-in-Dialog-API-Simple-Example).</span></span>


## <a name="pass-information-to-the-dialog-box"></a><span data-ttu-id="1b555-259">Transmission d’informations à la boîte de dialogue</span><span class="sxs-lookup"><span data-stu-id="1b555-259">Pass information to the dialog box</span></span>

<span data-ttu-id="1b555-p137">Parfois, la page hôte doit transmettre des informations à la boîte de dialogue. Pour ce faire, il existe deux moyens :</span><span class="sxs-lookup"><span data-stu-id="1b555-p137">Sometimes the host page needs to pass information to the dialog box. You can do this in two primary ways:</span></span>

- <span data-ttu-id="1b555-262">ajouter des paramètres de requête à l’URL qui est transmise à `displayDialogAsync` ;</span><span class="sxs-lookup"><span data-stu-id="1b555-262">Add query parameters to the URL that is passed to `displayDialogAsync`.</span></span>
- <span data-ttu-id="1b555-p138">stocker les informations à un emplacement auquel à la fois la fenêtre hôte et la boîte de dialogue ont accès. Les deux fenêtres ne partagent pas un stockage de session commun, mais *si elles ont le même domaine* (y compris le même numéro de port, le cas échéant), elles utilisent un [stockage local](http://www.w3schools.com/html/html5_webstorage.asp) commun.</span><span class="sxs-lookup"><span data-stu-id="1b555-p138">Store the information somewhere that is accessible to both the host window and dialog box. The two windows do not share a common session storage, but *if they have the same domain* (including port number, if any),  they share a common [local storage](http://www.w3schools.com/html/html5_webstorage.asp).</span></span>

### <a name="use-local-storage"></a><span data-ttu-id="1b555-265">Utilisation du stockage local</span><span class="sxs-lookup"><span data-stu-id="1b555-265">Use local storage</span></span>

<span data-ttu-id="1b555-266">Pour utiliser le stockage local, votre code appelle la méthode `setItem` de l’objet `window.localStorage` dans la page hôte avant l’appel de `displayDialogAsync`, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1b555-266">To use local storage, your code calls the `setItem` method of the `window.localStorage` object in the host page before the `displayDialogAsync` call, as in the following example:</span></span>

```js
localStorage.setItem("clientID", "15963ac5-314f-4d9b-b5a1-ccb2f1aea248");
```

<span data-ttu-id="1b555-267">Le code dans la fenêtre de dialogue lit l’élément lorsqu’il est nécessaire, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1b555-267">Code in the dialog window reads the item when it's needed, as in the following example:</span></span>

```js
var clientID = localStorage.getItem("clientID");
// You can also use property syntax:
// var clientID = localStorage.clientID;
```

<span data-ttu-id="1b555-268">Pour obtenir des exemples de compléments qui utilisent le stockage local de cette façon, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b555-268">For sample add-ins that uses local storage in this way, see:</span></span>

- [<span data-ttu-id="1b555-269">Complément Office qui utilise le service Auth0 pour simplifier la connexion sociale</span><span class="sxs-lookup"><span data-stu-id="1b555-269">Office Add-in that uses the Auth0 Service to Simplify Social Login</span></span>](https://github.com/OfficeDev/Office-Add-in-Auth0)
- [<span data-ttu-id="1b555-270">Complément Office qui utilise le service OAuth.io pour simplifier l’accès aux services en ligne populaires</span><span class="sxs-lookup"><span data-stu-id="1b555-270">Office Add-in that uses the OAuth.io Service to Simplify Access to Popular Online Services</span></span>](https://github.com/OfficeDev/Office-Add-in-OAuth.io)

### <a name="use-query-parameters"></a><span data-ttu-id="1b555-271">Utiliser les paramètres de requête</span><span class="sxs-lookup"><span data-stu-id="1b555-271">Use query parameters</span></span>

<span data-ttu-id="1b555-272">L’exemple suivant montre comment transmettre des données à l’aide d’un paramètre de requête :</span><span class="sxs-lookup"><span data-stu-id="1b555-272">The following example shows how to pass data with a query parameter:</span></span>

```js
Office.context.ui.displayDialogAsync('https://myAddinDomain/myDialog.html?clientID=15963ac5-314f-4d9b-b5a1-ccb2f1aea248');
```

<span data-ttu-id="1b555-273">Pour voir un exemple qui utilise cette technique, consultez la rubrique relative à l’exemple [Insérer des graphiques Excel à l’aide de Microsoft Graph dans un complément PowerPoint](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart).</span><span class="sxs-lookup"><span data-stu-id="1b555-273">For a sample that uses this technique, see [Insert Excel charts using Microsoft Graph in a PowerPoint Add-in](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart).</span></span>

<span data-ttu-id="1b555-274">Le code dans votre fenêtre de dialogue peut analyser l’URL et lire la valeur du paramètre.</span><span class="sxs-lookup"><span data-stu-id="1b555-274">Code in your dialog window can parse the URL and read the parameter value.</span></span>

> [!NOTE]
> <span data-ttu-id="1b555-p139">Office ajoute automatiquement un paramètre de requête appelé `_host_info` à l’URL qui est transmise à `displayDialogAsync`. (Il est ajouté après vos paramètres de requête personnalisés, le cas échéant. Il n’est pas ajouté à toutes les autres URL auxquelles la boîte de dialogue accède.) Microsoft peut modifier le contenu de cette valeur, ou le supprimer entièrement, à l’avenir, donc votre code ne doit pas le lire. La même valeur est ajoutée au stockage de session de la boîte de dialogue. Là encore, *votre code ne doit ni lire, ni écrire cette valeur*.</span><span class="sxs-lookup"><span data-stu-id="1b555-p139">Office automatically adds a query parameter called `_host_info` to the URL that is passed to `displayDialogAsync`. (It is appended after your custom query parameters, if any. It is not appended to any subsequent URLs that the dialog box navigates to.) Microsoft may change the content of this value, or remove it entirely, in the future, so your code should not read it. The same value is added to the dialog box's session storage. Again, *your code should neither read nor write to this value*.</span></span>

## <a name="use-the-dialog-apis-to-show-a-video"></a><span data-ttu-id="1b555-280">Utilisation des API de dialogue pour afficher une vidéo</span><span class="sxs-lookup"><span data-stu-id="1b555-280">Use the Dialog APIs to show a video</span></span>

<span data-ttu-id="1b555-281">Pour afficher une vidéo dans une boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="1b555-281">To show a video in a dialog box:</span></span>

1.  <span data-ttu-id="1b555-p140">Créez une page dont seul le contenu est un iFrame. L’attribut `src` de l’iFrame pointe vers une vidéo en ligne. Le protocole de l’URL de la vidéo doit être HTTP**S**. Dans cet article, nous appellerons cette page « video.dialogbox.html ». Voici un exemple de marques de révision :</span><span class="sxs-lookup"><span data-stu-id="1b555-p140">Create a page whose only content is an iframe. The `src` attribute of the iframe points to an online video. The protocol of the video's URL must be HTTP**S**. In this article we'll call this page "video.dialogbox.html". The following is an example of the markup:</span></span>

    ```HTML
    <iframe class="ms-firstrun-video__player"  width="640" height="360"
        src="https://www.youtube.com/embed/XVfOe5mFbAE?rel=0&autoplay=1"
        frameborder="0" allowfullscreen>
    </iframe>
    ```

2.  <span data-ttu-id="1b555-287">La page video.dialogbox.html doit se trouver dans le même domaine que la page hôte.</span><span class="sxs-lookup"><span data-stu-id="1b555-287">The video.dialogbox.html page must be in the same domain as the host page.</span></span>
3.  <span data-ttu-id="1b555-288">Utilisez un appel de `displayDialogAsync` dans la page hôte pour ouvrir video.dialogbox.html.</span><span class="sxs-lookup"><span data-stu-id="1b555-288">Use a call of `displayDialogAsync` in the host page to open video.dialogbox.html.</span></span>
4.  <span data-ttu-id="1b555-p141">Si votre complément a besoin de savoir quand l’utilisateur ferme la boîte de dialogue, inscrivez un gestionnaire pour l’événement `DialogEventReceived` et gérez l’événement 12006. Pour plus d’informations, consultez la section [Erreurs et événements dans la fenêtre de dialogue](#errors-and-events-in-the-dialog-window).</span><span class="sxs-lookup"><span data-stu-id="1b555-p141">If your add-in needs to know when the user closes the dialog box, register a handler for the `DialogEventReceived` event and handle the 12006 event. For details, see the section [Errors and events in the dialog window](#errors-and-events-in-the-dialog-window).</span></span>

<span data-ttu-id="1b555-291">Pour voir un exemple qui affiche une vidéo dans une boîte de dialogue, consultez le [modèle de conception de maquette de vidéo](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code/tree/master/templates/first-run/video-placemat) dans le référentiel de [modèles de conception de l’expérience utilisateur pour compléments Office](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code).</span><span class="sxs-lookup"><span data-stu-id="1b555-291">For a sample that shows a video in a dialog box, see the [video placemat design pattern](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code/tree/master/templates/first-run/video-placemat) in the [UX design patterns for Office Add-ins](https://github.com/OfficeDev/Office-Add-in-UX-Design-Patterns-Code) repo.</span></span>

![Capture d’écran d’une vidéo s’affichant dans une boîte de dialogue de complément](../images/video-placemats-dialog-open.png)

## <a name="use-the-dialog-apis-in-an-authentication-flow"></a><span data-ttu-id="1b555-293">Utilisation des API de dialogue dans un flux d’authentification</span><span class="sxs-lookup"><span data-stu-id="1b555-293">Use the Dialog APIs in an authentication flow</span></span>

<span data-ttu-id="1b555-294">Le scénario principal des API de dialogue consiste à activer l’authentification auprès d’un fournisseur de ressources ou d’identité qui n’autorise pas l’ouverture de sa page de connexion dans un iframe, comme un compte Microsoft, Office 365, Google et Facebook.</span><span class="sxs-lookup"><span data-stu-id="1b555-294">A primary scenario for the Dialog APIs is to enable authentication with a resource or identity provider that does not allow its sign-in page to open in an Iframe, such as Microsoft Account, Office 365, Google, and Facebook.</span></span>

> [!NOTE]
> <span data-ttu-id="1b555-p142">Lorsque vous utilisez les API de dialogue pour ce scénario, n’utilisez *pas* l’option `displayInIframe: true` dans l’appel de `displayDialogAsync`. Reportez-vous à la section [Tirer parti d’une option de performances dans Office Online](#take-advantage-of-a-performance-option-in-office-online) précédemment dans cet article pour plus d’informations sur cette option.</span><span class="sxs-lookup"><span data-stu-id="1b555-p142">When you are using the Dialog APIs for this scenario, do *not* use the `displayInIframe: true` option in the call to `displayDialogAsync`. See [Take advantage of a performance option in Office Online](#take-advantage-of-a-performance-option-in-office-online) previously in this article for details about this option.</span></span>

<span data-ttu-id="1b555-297">Voici un flux d’authentification simple et standard :</span><span class="sxs-lookup"><span data-stu-id="1b555-297">The following is a simple and typical authentication flow:</span></span>

1. <span data-ttu-id="1b555-p143">La première page qui s’ouvre dans la boîte de dialogue est une page locale (ou toute autre ressource) qui est hébergée dans le domaine du complément. Autrement dit, le domaine de la fenêtre hôte. Cette page peut avoir une IU simple indiquant « Veuillez patienter, nous allons vous rediriger vers la page sur laquelle vous pouvez vous connecter à *NOM DU FOURNISSEUR* ». Le code dans cette page construit l’URL de la page de connexion du fournisseur d’identité en utilisant les informations transmises à la boîte de dialogue, comme décrit dans [Transmission d’informations à la boîte de dialogue](#pass-information-to-the-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="1b555-p143">The first page that opens in the dialog box is a local page (or other resource) that is hosted in the add-in's domain; that is, the host window's domain. This page can have a simple UI that says "Please wait, we are redirecting you to the page where you can sign in to *NAME-OF-PROVIDER*." Code in this page constructs the URL of the identity provider's sign-in page by using information that is passed to the dialog box as described in [Pass information to the dialog box](#pass-information-to-the-dialog-box).</span></span>
2. <span data-ttu-id="1b555-p144">La fenêtre de dialogue redirige alors l’utilisateur vers la page de connexion. L’URL inclut un paramètre de requête qui indique au fournisseur d’identité de rediriger la fenêtre de dialogue une fois que l’utilisateur s’est connecté à une page spécifique. Dans cet article, nous appellerons cette page « redirectPage.html ». (*Il doit s’agir d’une page ayant le même domaine que la fenêtre hôte*, car le seul moyen pour que la fenêtre de dialogue transmette les résultats de la tentative de connexion est un appel de `messageParent`, qui ne peut être appelé que sur une page ayant le même domaine que la fenêtre hôte.)</span><span class="sxs-lookup"><span data-stu-id="1b555-p144">The dialog window then redirects to the sign-in page. The URL includes a query parameter that tells the identity provider to redirect the dialog window, after the user signs in, to a specific page. In this article, we'll call this page "redirectPage.html". (*This must be a page in the same domain as the host window*, because the only way for the dialog window to pass the results of the sign-in attempt is with a call of `messageParent`, which can only be called on a page with the same domain as the host window.)</span></span>
2. <span data-ttu-id="1b555-p145">Le service du fournisseur d’identité traite la requête GET entrante à partir de la fenêtre de dialogue. Si l’utilisateur est déjà connecté, il redirige immédiatement la fenêtre vers redirectPage.html et inclut les données utilisateur sous la forme d’un paramètre de requête. Si l’utilisateur n’est pas encore connecté, la page de connexion du fournisseur apparaît dans la fenêtre et l’utilisateur se connecte. Pour la plupart des fournisseurs, si l’utilisateur ne parvient pas à se connecter, le fournisseur affiche une page d’erreur dans la fenêtre de dialogue et ne redirige pas vers redirectPage.html. L’utilisateur doit fermer la fenêtre en sélectionnant le **X** dans le coin. Si l’utilisateur se connecte avec succès, la fenêtre de dialogue est redirigée vers redirectPage.html et les données utilisateur sont incluses sous la forme d’un paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="1b555-p145">The identity provider's service processes the incoming GET request from the dialog window. If the user is already logged on, it immediately redirects the window to redirectPage.html and includes user data as a query parameter. If the user is not already signed in, the provider's sign-in page appears in the window, and the user signs in. For most providers, if the user cannot sign in successfully, the provider shows an error page in the dialog window and does not redirect to redirectPage.html. The user must close the window by selecting the **X** in the corner. If the user successfully signs in, the dialog window is redirected to redirectPage.html and user data is included as a query parameter.</span></span>
3. <span data-ttu-id="1b555-311">Lorsque la page redirectPage.html s’ouvre, elle appelle `messageParent` pour indiquer le succès ou l’échec à la page hôte et éventuellement indiquer également des données utilisateur ou des données d’erreur.</span><span class="sxs-lookup"><span data-stu-id="1b555-311">When the redirectPage.html page opens, it calls `messageParent` to report the success or failure to the host page and optionally also report user data or error data.</span></span>
4. <span data-ttu-id="1b555-312">L’événement `DialogMessageReceived` se déclenche dans la page hôte, et son gestionnaire ferme la fenêtre de dialogue et effectue éventuellement d’autres traitements du message.</span><span class="sxs-lookup"><span data-stu-id="1b555-312">The `DialogMessageReceived` event fires in the host page and its handler closes the dialog window and optionally does other processing of the message.</span></span>

<span data-ttu-id="1b555-313">Pour voir des exemples de compléments qui utilisent ce modèle, consultez les pages suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b555-313">For sample add-ins that use this pattern, see:</span></span>

- <span data-ttu-id="1b555-p146">[Insérer des graphiques Excel à l’aide de Microsoft Graph dans un complément PowerPoint](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart) : La ressource qui s’ouvre initialement dans la fenêtre de la boîte de dialogue est une méthode du contrôleur qui ne dispose d’aucun affichage propre. Elle redirige l’utilisateur vers la page de connexion Office 365.</span><span class="sxs-lookup"><span data-stu-id="1b555-p146">[Insert Excel charts using Microsoft Graph in a PowerPoint Add-in](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart): The resource that is initially opened in the dialog window is a controller method that has no view of its own. It redirects to the Office 365 sign in page.</span></span>
- <span data-ttu-id="1b555-316">[Authentification client Office 365 du complément Office pour AngularJS](https://github.com/OfficeDev/Word-Add-in-AngularJS-Client-OAuth) : La ressource qui s’ouvre initialement dans la fenêtre de dialogue est une page.</span><span class="sxs-lookup"><span data-stu-id="1b555-316">[Office Add-in Office 365 Client Authentication for AngularJS](https://github.com/OfficeDev/Word-Add-in-AngularJS-Client-OAuth): The resource that is initially opened in the dialog window is a page.</span></span>

#### <a name="support-multiple-identity-providers"></a><span data-ttu-id="1b555-317">Prise en charge de plusieurs fournisseurs d’identité</span><span class="sxs-lookup"><span data-stu-id="1b555-317">Support multiple identity providers</span></span>

<span data-ttu-id="1b555-p147">Si votre complément offre à l’utilisateur le choix entre plusieurs fournisseurs, tels qu’un compte Microsoft, Google ou Facebook, vous avez besoin d’une première page locale (voir section précédente) qui fournit une IU permettant à l’utilisateur de sélectionner un fournisseur. La sélection déclenche la construction de l’URL de connexion et la redirection vers celle-ci.</span><span class="sxs-lookup"><span data-stu-id="1b555-p147">If your add-in gives the user a choice of providers, such as Microsoft Account, Google, or Facebook, you need a local first page (see preceding section) that provides a UI for the user to select a provider. Selection triggers the construction of the sign-in URL and redirection to it.</span></span>

<span data-ttu-id="1b555-320">Pour voir un exemple qui utilise ce modèle, consultez la rubrique relative à l’exemple [Complément Office qui utilise le service Auth0 pour simplifier la connexion aux réseaux sociaux](https://github.com/OfficeDev/Office-Add-in-Auth0).</span><span class="sxs-lookup"><span data-stu-id="1b555-320">For a sample that uses this pattern, see [Office Add-in that uses the Auth0 Service to Simplify Social Login](https://github.com/OfficeDev/Office-Add-in-Auth0).</span></span>

#### <a name="authorization-of-the-add-in-to-an-external-resource"></a><span data-ttu-id="1b555-321">Autorisation du complément pour une ressource externe</span><span class="sxs-lookup"><span data-stu-id="1b555-321">Authorization of the add-in to an external resource</span></span>

<span data-ttu-id="1b555-p148">Sur le web nouvelle génération, les applications web sont des principaux de sécurité au même titre que les utilisateurs, et l’application a sa propre identité et ses propres autorisations pour une ressource en ligne comme Office 365, Google Plus, Facebook ou LinkedIn. L’application est inscrite auprès du fournisseur de ressources avant d’être déployée. L’inscription inclut :</span><span class="sxs-lookup"><span data-stu-id="1b555-p148">In the modern web, web applications are security principals just as users are, and the application has its own identity and permissions to an online resource such as Office 365, Google Plus, Facebook, or LinkedIn. The application is registered with the resource provider before it is deployed. The registration includes:</span></span>

- <span data-ttu-id="1b555-325">la liste des autorisations dont l’application a besoin pour les ressources d’un utilisateur ;</span><span class="sxs-lookup"><span data-stu-id="1b555-325">A list of the permissions that the application needs to a user's resources.</span></span>
- <span data-ttu-id="1b555-326">l’URL à laquelle le service de ressources doit renvoyer un jeton d’accès lorsque l’application accède au service.</span><span class="sxs-lookup"><span data-stu-id="1b555-326">A URL to which the resource service should return an access token when the application accesses the service.</span></span>  

<span data-ttu-id="1b555-p149">Lorsqu’un utilisateur appelle une fonction dans l’application qui accède aux données de l’utilisateur dans le service de ressources, l’utilisateur est invité à se connecter au service, puis à accorder à l’application les autorisations dont elle a besoin pour les ressources de l’utilisateur. Ensuite, le service redirige la fenêtre de connexion vers l’URL précédemment inscrite et transmet le jeton d’accès. L’application utilise le jeton d’accès pour accéder aux ressources de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1b555-p149">When a user invokes a function in the application that accesses the user's data in the resource service, they are prompted to sign in to the service and then prompted to grant the application the permissions it needs to the user's resources. The service then redirects the sign-in window to the previously registered URL and passes the access token. The application uses the access token to access the user's resources.</span></span>

<span data-ttu-id="1b555-p150">Vous pouvez utiliser les API de dialogue pour gérer ce processus à l’aide d’un flux semblable à celui décrit pour la connexion des utilisateurs. Les seules différences sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b555-p150">You can use the Dialog APIs to manage this process by using a flow that is similar to the one described for users to sign in. The only differences are:</span></span>

- <span data-ttu-id="1b555-332">Si l’utilisateur n’a pas préalablement accordé à l’application les autorisations nécessaires, il est invité à le faire dans la boîte de dialogue après la connexion.</span><span class="sxs-lookup"><span data-stu-id="1b555-332">If the user hasn't previously granted the application the permissions it needs, she is prompted to do so in the dialog box after signing in.</span></span>
- <span data-ttu-id="1b555-p151">La fenêtre de dialogue envoie le jeton d’accès à la fenêtre hôte en utilisant `messageParent` pour envoyer le jeton d’accès converti en chaîne ou en stockant jeton d’accès à un emplacement où la fenêtre hôte peut le récupérer. Le jeton a une limite de temps, mais tant qu’elle n’est pas écoulée, la fenêtre hôte peut l’utiliser pour accéder directement aux ressources de l’utilisateur sans demander d’autre confirmation.</span><span class="sxs-lookup"><span data-stu-id="1b555-p151">The dialog window sends the access token to the host window either by using `messageParent` to send the stringified access token or by storing the access token where the host window can retrieve it. The token has a time limit, but while it lasts, the host window can use it to directly access the user's resources without any further prompting.</span></span>

<span data-ttu-id="1b555-335">Les exemples suivants utilisent les API de dialogue à cet effet :</span><span class="sxs-lookup"><span data-stu-id="1b555-335">The following samples use the Dialog APIs for this purpose:</span></span>
- <span data-ttu-id="1b555-336">[Insérer des graphiques Excel à l’aide de Microsoft Graph dans un complément PowerPoint](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart) : stocke le jeton d’accès dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="1b555-336">[Insert Excel charts using Microsoft Graph in a PowerPoint Add-in](https://github.com/OfficeDev/PowerPoint-Add-in-Microsoft-Graph-ASPNET-InsertChart) - Stores the access token in a database.</span></span>
- [<span data-ttu-id="1b555-337">Complément Office qui utilise le service OAuth.io pour simplifier l’accès aux services en ligne populaires</span><span class="sxs-lookup"><span data-stu-id="1b555-337">Office Add-in that uses the OAuth.io Service to Simplify Access to Popular Online Services</span></span>](https://github.com/OfficeDev/Office-Add-in-OAuth.io)

<span data-ttu-id="1b555-338">Pour plus d’informations sur l’authentification et l’autorisation dans des compléments, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="1b555-338">For more information about authentication and authorization in add-ins, see:</span></span>
- [<span data-ttu-id="1b555-339">Autoriser des services externes dans votre complément Office</span><span class="sxs-lookup"><span data-stu-id="1b555-339">Authorize external services in your Office Add-in</span></span>](auth-external-add-ins.md)
- [<span data-ttu-id="1b555-340">Bibliothèque d’applications d’assistance des API JavaScript Office</span><span class="sxs-lookup"><span data-stu-id="1b555-340">Office JavaScript API Helpers library</span></span>](https://github.com/OfficeDev/office-js-helpers)


## <a name="use-the-office-dialog-api-with-single-page-applications-and-client-side-routing"></a><span data-ttu-id="1b555-341">Utilisation de l’API de dialogue Office avec des applications à page unique et routage côté client</span><span class="sxs-lookup"><span data-stu-id="1b555-341">Use the Office Dialog API with single-page applications and client-side routing</span></span>

<span data-ttu-id="1b555-342">Si votre complément utilise le routage côté client, comme le font les applications à page unique en règle générale, vous avez la possibilité de transmettre l’URL d’un itinéraire à la méthode [displayDialogAsync](http://dev.office.com/reference/add-ins/shared/officeui.displaydialogasync), au lieu de l’URL de la page HTML complète et distincte.</span><span class="sxs-lookup"><span data-stu-id="1b555-342">If your add-in uses client-side routing, as single-page applications typically do, you have the option to pass the URL of a route to the [displayDialogAsync](http://dev.office.com/reference/add-ins/shared/officeui.displaydialogasync) method, instead of the URL of a complete and separate HTML page.</span></span>

> [!IMPORTANT]
><span data-ttu-id="1b555-p152">La boîte de dialogue se trouve dans une nouvelle fenêtre avec son propre contexte d’exécution. Si vous transmettez un itinéraire, votre page de base et son code d’initialisation et d’amorçage s’exécutent à nouveau dans ce nouveau contexte, et toutes les variables sont définies sur leurs valeurs initiales dans la fenêtre de dialogue. Par conséquent, cette technique lance une deuxième instance de votre application dans la fenêtre de dialogue. Le code qui modifie des variables dans la fenêtre de dialogue ne change pas la version du volet Office des mêmes variables. De même, la fenêtre de dialogue possède son propre stockage de session, qui n’est pas accessible à partir du code dans le volet Office.</span><span class="sxs-lookup"><span data-stu-id="1b555-p152">The dialog box is in a new window with its own execution context. If you pass a route, your base page and all its initialization and bootstrapping code run again in this new context, and any variables are set to their initial values in the dialog window. So this technique launches a second instance of your application in the dialog window. Code that changes variables in the dialog window does not change the task pane version of the same variables. Similarly, the dialog window has its own session storage, which is not accessible from code in the task pane.</span></span>