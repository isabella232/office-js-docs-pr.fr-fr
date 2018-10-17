
# <a name="item"></a>item

### [Office](office.md)[.context](office.context.md)[.mailbox](office.context.mailbox.md). item

L’espace de noms `item` est utilisé pour accéder à vos messages, à vos demandes de réunion ou à vos rendez-vous. Vous pouvez déterminer le type de `item` à l’aide de la propriété [itemType](#itemtype-officemailboxenumsitemtypejavascriptapioutlook11officemailboxenumsitemtype).

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| Restreint|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

### <a name="example"></a>Exemple

Cet exemple de code JavaScript montre comment accéder à la propriété `subject` de l’élément actif dans Outlook.

```JavaScript
// The initialize function is required for all apps.
Office.initialize = function () {
    // Checks for the DOM to load using the jQuery ready function.
    $(document).ready(function () {
    // After the DOM is loaded, app-specific code can run.
    var item = Office.context.mailbox.item;
    var subject = item.subject;
    // Continue with processing the subject of the current item,
    // which can be a message or appointment.
    });
}
```

### <a name="members"></a>Membres

#### <a name="attachments-arrayattachmentdetailsjavascriptapioutlook11officeattachmentdetails"></a>attachments :Array.<[AttachmentDetails](/javascript/api/outlook_1_1/office.attachmentdetails)>

Obtient un tableau des pièces jointes de l’élément. Mode lecture uniquement.

> [!NOTE]
> Certains types de fichiers sont bloqués par Outlook en raison de problèmes de sécurité potentiels et ne sont donc pas rendus. Pour plus d’information, voir les [pièces jointes bloquées par Outlook](https://support.office.com/article/Blocked-attachments-in-Outlook-434752E1-02D3-4E90-9124-8B81E49A8519).

##### <a name="type"></a>Type :

*   Array.<[AttachmentDetails](/javascript/api/outlook_1_1/office.attachmentdetails)>

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

Le code suivant génère une chaîne HTML avec les détails de toutes les pièces jointes de l’élément actif.

```JavaScript
var _Item = Office.context.mailbox.item;
var outputString = "";

if (_Item.attachments.length > 0) {
  for (i = 0 ; i < _Item.attachments.length ; i++) {
    var _att = _Item.attachments[i];
    outputString += "<BR>" + i + ". Name: ";
    outputString += _att.name;
    outputString += "<BR>ID: " + _att.id;
    outputString += "<BR>contentType: " + _att.contentType;
    outputString += "<BR>size: " + _att.size;
    outputString += "<BR>attachmentType: " + _att.attachmentType;
    outputString += "<BR>isInline: " + _att.isInline;
  }
}

// Do something with outputString
```

####  <a name="bcc-recipientsjavascriptapioutlook11officerecipients"></a>bcc :[Recipients](/javascript/api/outlook_1_1/office.recipients)

Obtient un objet qui fournit les méthodes permettant d’obtenir ou de mettre à jour les destinataires des Cci (copie carbone invisible) d’un message. Mode composition uniquement.

##### <a name="type"></a>Type :

*   [Recipients](/javascript/api/outlook_1_1/office.recipients)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.1|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition|

##### <a name="example"></a>Exemple

```JavaScript
Office.context.mailbox.item.bcc.setAsync( ['alice@contoso.com', 'bob@contoso.com'] );
Office.context.mailbox.item.bcc.addAsync( ['jason@contoso.com'] );
Office.context.mailbox.item.bcc.getAsync(callback);

function callback(asyncResult) {
  var arrayOfBccRecipients = asyncResult.value;
}
```

####  <a name="body-bodyjavascriptapioutlook11officebody"></a>body :[Body](/javascript/api/outlook_1_1/office.body)

Obtient un objet qui fournit des méthodes permettant de manipuler le texte d’un élément.

##### <a name="type"></a>Type :

*   [Body](/javascript/api/outlook_1_1/office.body)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.1|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

####  <a name="cc-arrayemailaddressdetailsjavascriptapioutlook11officeemailaddressdetailsrecipientsjavascriptapioutlook11officerecipients"></a>cc :Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)>|[Recipients](/javascript/api/outlook_1_1/office.recipients)

Permet d’accéder aux destinataires Cc (copie carbone) d’un message. La nature d’un objet et son niveau d’accès dépendent du mode de l’élément actuel.

##### <a name="read-mode"></a>Mode lecture

La propriété `cc` renvoie un tableau contenant un objet `EmailAddressDetails` pour chaque destinataire répertorié sur la ligne **Cc** du message. La collection est limitée à 100 membres.

##### <a name="compose-mode"></a>Mode composition

La propriété `cc` renvoie un objet `Recipients` qui fournit des méthodes permettant d’obtenir ou de mettre à jour les destinataires sur la ligne **Cc** du message.

##### <a name="type"></a>Type :

*   Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)> | [Recipients](/javascript/api/outlook_1_1/office.recipients)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

```JavaScript
Office.context.mailbox.item.cc.setAsync( ['alice@contoso.com', 'bob@contoso.com'] );
Office.context.mailbox.item.cc.addAsync( ['jason@contoso.com'] );
Office.context.mailbox.item.cc.getAsync(callback);

function callback(asyncResult) {
  var arrayOfCcRecipients = asyncResult.value;
}
```

####  <a name="nullable-conversationid-string"></a>(nullable) conversationId :String

Obtient l’identificateur de la conversation qui contient un message particulier.

Vous pouvez obtenir un nombre entier de cette propriété si votre application de messagerie est activée dans les formulaires de lecture ou les réponses des formulaires de composition. Si, par la suite, l’utilisateur modifie l’objet du message de réponse, lors de l’envoi de la réponse, l’identificateur de conversation de ce message changera et la valeur que vous aurez obtenue plus tôt ne sera plus applicable.

Cette propriété obtient une valeur null lorsqu’un élément est ajouté à un formulaire de composition. Si l’utilisateur définit la ligne Objet et enregistre l’élément, la propriété `conversationId` renverra une valeur.

##### <a name="type"></a>Type :

*   String

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

#### <a name="datetimecreated-date"></a>dateTimeCreated :Date

Obtient la date et l’heure de création d’un élément. Mode lecture uniquement.

##### <a name="type"></a>Type :

*   Date

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var created = Office.context.mailbox.item.dateTimeCreated;
```

#### <a name="datetimemodified-date"></a>dateTimeModified :Date

Obtient la date et l’heure de la dernière modification d’un élément. Mode lecture uniquement.

> [!NOTE]
> Ce membre n’est pas pris en charge par Outlook pour iOS ou Outlook pour Android.

##### <a name="type"></a>Type :

*   Date

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var modified = Office.context.mailbox.item.dateTimeModified;
```

####  <a name="end-datetimejavascriptapioutlook11officetime"></a>end :Date|[Time](/javascript/api/outlook_1_1/office.time)

Obtient ou définit la date et l’heure de fin du rendez-vous.

La propriété `end` est exprimée en date et heure U.T.C. (temps universel coordonné). Vous pouvez utiliser la méthode [`convertToLocalClientTime`](office.context.mailbox.md#converttolocalclienttimetimevalue--localclienttimejavascriptapioutlook11officelocalclienttime) pour convertir la valeur de fin de la propriété à la date et à l’heure locale du client.

##### <a name="read-mode"></a>Mode lecture

La propriété `end` renvoie un objet `Date`.

##### <a name="compose-mode"></a>Mode composition

La propriété `end` renvoie un objet `Time`.

Quand vous utilisez la méthode [`Time.setAsync`](/javascript/api/outlook_1_1/office.time#setasync-datetime--options--callback-) pour définir l’heure de fin, nous vous recommandons d’utiliser la méthode [`convertToUtcClientTime`](office.context.mailbox.md#converttoutcclienttimeinput--date) pour convertir l’heure locale du client au format UTC pour le serveur.

##### <a name="type"></a>Type :

*   Date | [Time](/javascript/api/outlook_1_1/office.time)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

L’exemple suivant définit l’heure de fin d’un rendez-vous en mode composition à l’aide de la méthode [`setAsync`](/javascript/api/outlook_1_1/office.time#setasync-datetime--options--callback-) de l’objet `Time`.

```JavaScript
var endTime = new Date("3/14/2015");
var options = {
  // Pass information that can be used
  // in the callback
     asyncContext: {verb:"Set"}
}
Office.context.mailbox.item.end.setAsync(endTime, options, function(result) {
  if (result.error) {
    console.debug(result.error);
  } else {
    // Access the asyncContext that was passed to the setAsync function
    console.debug("End Time " + result.asyncContext.verb);
  }
});
```

#### <a name="from-emailaddressdetailsjavascriptapioutlook11officeemailaddressdetails"></a>from :[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)

Obtient l’adresse de messagerie de l’expéditeur d’un message. Mode lecture uniquement.

Les propriétés `from` et [`sender`](#sender-emailaddressdetailsjavascriptapioutlook11officeemailaddressdetails) représentent la même personne, sauf si le message est envoyé par un délégué. Dans ce cas, la propriété `from` représente le délégant et la propriété expéditeur représente le délégué.

> [!NOTE]
> La propriété  `recipientType` de l'objet  `EmailAddressDetails` dans la propriété  `from` est `undefined`.

##### <a name="type"></a>Type :

*   [EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

#### <a name="internetmessageid-string"></a>internetMessageId :String

Obtient l’identificateur de message Internet d’un e-mail. Mode lecture uniquement.

##### <a name="type"></a>Type :

*   String

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var internetMessageId = Office.context.mailbox.item.internetMessageId;
```

#### <a name="itemclass-string"></a>itemClass :String

Obtient la classe de l’élément des services web Exchange de l’élément sélectionné. Mode lecture uniquement.

La propriété `itemClass` spécifie la classe de message de l’élément sélectionné. Les éléments suivants sont les classes de message par défaut du message ou de l’élément de rendez-vous.

| Type | Description | Classe d’élément |
| --- | --- | --- |
| Éléments de rendez-vous | Ce sont les éléments de calendrier de la classe de l’élément `IPM.Appointment` ou `IPM.Appointment.Occurence`. | `IPM.Appointment`<br />`IPM.Appointment.Occurence` |
| Éléments de message | Ces éléments incluent les e-mails dont la classe de message par défaut est `IPM.Note`, ainsi que les demandes de réunion, les réponses et les annulations qui utilisent `IPM.Schedule.Meeting` comme classe de message de base. | `IPM.Note`<br />`IPM.Schedule.Meeting.Request`<br />`IPM.Schedule.Meeting.Neg`<br />`IPM.Schedule.Meeting.Pos`<br />`IPM.Schedule.Meeting.Tent`<br />`IPM.Schedule.Meeting.Canceled` |

Vous pouvez créer des classes de message personnalisées qui étendent une classe de message par défaut, par exemple, une classe de message de rendez-vous personnalisée `IPM.Appointment.Contoso`.

##### <a name="type"></a>Type :

*   String

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var itemClass = Office.context.mailbox.item.itemClass;
```

#### <a name="nullable-itemid-string"></a>(nullable) itemId :String

Obtient l’identificateur de l’élément des services web Exchange pour l’élément actif. Mode lecture uniquement.

> [!NOTE]
> L’identificateur renvoyé par la propriété `itemId` est identique à celui de l’élément des services web Exchange. La propriété `itemId` n’est pas identique à l’ID d’entrée Outlook ou l’ID utilisé par l’API REST de Outlook. Avant que d’appeler l’API REST à l’aide de cette valeur, elle doit être convertie à l’aide de `Office.context.mailbox.convertToRestId`, qui est disponible à partir de l’ensemble de conditions requises 1.3. Pour plus d’informations, voir [Utilisation des API REST Outlook à partir d’un complément Outlook](https://docs.microsoft.com/outlook/add-ins/use-rest-api#get-the-item-id).

##### <a name="type"></a>Type :

*   String

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

Le code suivant vérifie la présence d’un identificateur d’élément. Si la propriété `itemId` renvoie `null` ou `undefined`, il enregistre l’élément sur le magasin et obtient l’identificateur de l’élément à partir du résultat asynchrone.

```JavaScript
var itemId = Office.context.mailbox.item.itemId;
if (itemId === null || itemId == undefined) {
  Office.context.mailbox.item.saveAsync(function(result){
    itemId = result.value;
  });
}
```

####  <a name="itemtype-officemailboxenumsitemtypejavascriptapioutlook11officemailboxenumsitemtype"></a>itemType :[Office.MailboxEnums.ItemType](/javascript/api/outlook_1_1/office.mailboxenums.itemtype)

Obtient le type d’élément représenté par une instance.

La propriété `itemType` renvoie une des valeurs d’énumération `ItemType` indiquant si l’instance d’objet `item` est un message ou un rendez-vous.

##### <a name="type"></a>Type :

*   [Office.MailboxEnums.ItemType](/javascript/api/outlook_1_1/office.mailboxenums.itemtype)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

```JavaScript
if (Office.context.mailbox.item.itemType == Office.MailboxEnums.ItemType.Message)
  // do something
else
  // do something else
```

####  <a name="location-stringlocationjavascriptapioutlook11officelocation"></a>location :String|[Location](/javascript/api/outlook_1_1/office.location)

Obtient ou définit le lieu d’un rendez-vous.

##### <a name="read-mode"></a>Mode lecture

La propriété `location` renvoie une chaîne contenant le lieu du rendez-vous.

##### <a name="compose-mode"></a>Mode composition

La propriété `location` renvoie un objet `Location` qui fournit les méthodes utilisées pour obtenir et définir le lieu du rendez-vous.

##### <a name="type"></a>Type :

*   String | [Location](/javascript/api/outlook_1_1/office.location)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

```JavaScript
var userContext = { value : 1 };
Office.context.mailbox.item.location.getAsync( { context: userContext}, callback);

function callback(asyncResult) {
  var context = asyncResult.context;
  var location = asyncResult.value;
}
```

#### <a name="normalizedsubject-string"></a>normalizedSubject :String

Obtient l’objet d’un élément, sans les préfixes (y compris `RE:` et `FWD:`). Mode lecture uniquement.

La propriété normalizedSubject obtient l’objet de l’élément, sans les préfixes standard (par exemple, `RE:` et `FW:`) qui sont ajoutés par les programmes de messagerie électronique. Pour obtenir l’objet de l’élément avec les préfixes intacts, utilisez la propriété [`subject`](#subject-stringsubjectjavascriptapioutlook11officesubject).

##### <a name="type"></a>Type :

*   String

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var normalizedSubject = Office.context.mailbox.item.normalizedSubject;
```

####  <a name="optionalattendees-arrayemailaddressdetailsjavascriptapioutlook11officeemailaddressdetailsrecipientsjavascriptapioutlook11officerecipients"></a>optionalAttendees :Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)>|[Recipients](/javascript/api/outlook_1_1/office.recipients)

Fournit l’accès aux participants facultatifs d’un événement. La nature d’un objet et son niveau d’accès dépendent du mode de l’élément actuel.

##### <a name="read-mode"></a>Mode lecture

La propriété `optionalAttendees` renvoie un tableau contenant un objet `EmailAddressDetails` pour chaque participant facultatif à la réunion.

##### <a name="compose-mode"></a>Mode composition

La propriété `optionalAttendees` renvoie un objet `Recipients` qui fournit des méthodes permettant d'obtenir ou de mettre à jour les participants facultatifs d’une réunion.

##### <a name="type"></a>Type :

*   Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)> | [Recipients](/javascript/api/outlook_1_1/office.recipients)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

```JavaScript
Office.context.mailbox.item.optionalAttendees.setAsync( ['alice@contoso.com', 'bob@contoso.com'] );
Office.context.mailbox.item.optionalAttendees.addAsync( ['jason@contoso.com'] );
Office.context.mailbox.item.optionalAttendees.getAsync(callback);

function callback(asyncResult) {
  var arrayOfOptionalAttendeesRecipients = asyncResult.value;
}
```

#### <a name="organizer-emailaddressdetailsjavascriptapioutlook11officeemailaddressdetails"></a>organizer :[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)

Obtient l’adresse de messagerie de l’organisateur de la réunion spécifiée. Mode lecture uniquement.

##### <a name="type"></a>Type :

*   [EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var organizerName = Office.context.mailbox.item.organizer.displayName;
var organizerAddress = Office.context.mailbox.item.organizer.emailAddress;
```

####  <a name="requiredattendees-arrayemailaddressdetailsjavascriptapioutlook11officeemailaddressdetailsrecipientsjavascriptapioutlook11officerecipients"></a>requiredAttendees :Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)>|[Recipients](/javascript/api/outlook_1_1/office.recipients)

Fournit l’accès aux participants obligatoires d'un événement. La nature d’un objet et son niveau d’accès dépendent du mode de l’élément actuel.

##### <a name="read-mode"></a>Mode lecture

La propriété `requiredAttendees` renvoie un tableau contenant un objet `EmailAddressDetails` pour chaque participant obligatoires de la réunion.

##### <a name="compose-mode"></a>Mode composition

La propriété `requiredAttendees` renvoie un objet `Recipients` qui fournit des méthodes permettant d’obtenir ou de mettre à jour les participants facultatifs d’une réunion.

##### <a name="type"></a>Type :

*   Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)> | [Recipients](/javascript/api/outlook_1_1/office.recipients)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

```JavaScript
Office.context.mailbox.item.requiredAttendees.setAsync( ['alice@contoso.com', 'bob@contoso.com'] );
Office.context.mailbox.item.requiredAttendees.addAsync( ['jason@contoso.com'] );
Office.context.mailbox.item.requiredAttendees.getAsync(callback);

function callback(asyncResult) {
  var arrayOfRequiredAttendeesRecipients = asyncResult.value;
}
```

#### <a name="sender-emailaddressdetailsjavascriptapioutlook11officeemailaddressdetails"></a>sender :[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)

Obtient l’adresse de messagerie de l’expéditeur d’un e-mail. Mode lecture uniquement.

Les propriétés [`from`](#from-emailaddressdetailsjavascriptapioutlook11officeemailaddressdetails) et `sender` représentent la même personne, sauf si le message est envoyé par un délégué. Dans ce cas, la propriété `from` représente le délégant et la propriété expéditeur représente le délégué.

> [!NOTE]
> La propriété  `recipientType` de l'objet  `EmailAddressDetails` dans la propriété  `from` est `undefined`.

##### <a name="type"></a>Type :

*   [EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="example"></a>Exemple

```JavaScript
var senderName = Office.context.mailbox.item.sender.displayName;
var senderAddress = Office.context.mailbox.item.sender.emailAddress;
```

####  <a name="start-datetimejavascriptapioutlook11officetime"></a>start :Date|[Time](/javascript/api/outlook_1_1/office.time)

Obtient ou définit la date et l’heure de début du rendez-vous.

La propriété `start` est exprimée en date et heure U.T.C. (temps universel coordonné). Vous pouvez utiliser la méthode [`convertToLocalClientTime`](office.context.mailbox.md#converttolocalclienttimetimevalue--localclienttimejavascriptapioutlook11officelocalclienttime) pour convertir la valeur à la date et à l’heure du client.

##### <a name="read-mode"></a>Mode lecture

La propriété `start` renvoie un objet `Date`.

##### <a name="compose-mode"></a>Mode composition

La propriété `start` renvoie un objet `Time`.

Quand vous utilisez la méthode [`Time.setAsync`](/javascript/api/outlook_1_1/office.time#setasync-datetime--options--callback-) pour définir l’heure de début, nous vous recommandons d’utiliser la méthode [`convertToUtcClientTime`](office.context.mailbox.md#converttoutcclienttimeinput--date) pour convertir l’heure locale du client au format U.T.C. pour le serveur.

##### <a name="type"></a>Type :

*   Date | [Time](/javascript/api/outlook_1_1/office.time)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

L’exemple suivant définit l’heure de début d’un rendez-vous en mode composition à l’aide de la méthode [`setAsync`](/javascript/api/outlook_1_1/office.time#setasync-datetime--options--callback-) de l’objet `Time`.

```JavaScript
var startTime = new Date("3/14/2015");
var options = {
  // Pass information that can be used
  // in the callback
     asyncContext: {verb:"Set"}
}
Office.context.mailbox.item.start.setAsync(startTime, options, function(result) {
  if (result.error) {
    console.debug(result.error);
  } else {
    // Access the asyncContext that was passed to the setAsync function
    console.debug("Start Time " + result.asyncContext.verb);
  }
});
```

####  <a name="subject-stringsubjectjavascriptapioutlook11officesubject"></a>subject :String|[Subject](/javascript/api/outlook_1_1/office.subject)

Obtient ou définit la description qui apparaît dans le champ d’objet d’un élément.

La propriété `subject` obtient ou définit l’intégralité de l’objet de l’élément, tel qu’il est envoyé par le serveur de messagerie.

##### <a name="read-mode"></a>Mode lecture

La propriété `subject` renvoie une chaîne. Utilisez la propriété [`normalizedSubject`](#normalizedsubject-string) pour obtenir l’objet sans les préfixes tels que `RE:` et `FW:`.

```
var subject = Office.context.mailbox.item.subject;
```

##### <a name="compose-mode"></a>Mode composition

La propriété `subject` renvoie un objet `Subject` qui fournit des méthodes pour obtenir et définir l’objet.

```JavaScript
Office.context.mailbox.item.subject.getAsync(callback);

function callback(asyncResult) {
  var subject = asyncResult.value;
}
```

##### <a name="type"></a>Type :

*   String | [Subject](/javascript/api/outlook_1_1/office.subject)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

####  <a name="to-arrayemailaddressdetailsjavascriptapioutlook11officeemailaddressdetailsrecipientsjavascriptapioutlook11officerecipients"></a>to :Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)>|[Recipients](/javascript/api/outlook_1_1/office.recipients)

Permet d’accéder aux destinataires de la ligne **à** du message. La nature d’un objet et son niveau d’accès dépendent du mode de l’élément actuel.

##### <a name="read-mode"></a>Mode lecture

La propriété `to` renvoie un tableau contenant un objet `EmailAddressDetails` pour chaque destinataire répertorié sur la ligne **À** du message. La collection est limitée à 100 membres.

##### <a name="compose-mode"></a>Mode composition

La propriété `to` renvoie un objet `Recipients` qui fournit des méthodes permettant d’obtenir ou de mettre à jour les destinataires sur la ligne **À** du message.

##### <a name="type"></a>Type :

*   Array.<[EmailAddressDetails](/javascript/api/outlook_1_1/office.emailaddressdetails)> | [Recipients](/javascript/api/outlook_1_1/office.recipients)

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

```JavaScript
Office.context.mailbox.item.to.setAsync( ['alice@contoso.com', 'bob@contoso.com'] );
Office.context.mailbox.item.to.addAsync( ['jason@contoso.com'] );
Office.context.mailbox.item.to.getAsync(callback);

function callback(asyncResult) {
  var arrayOfToRecipients = asyncResult.value;
}
```

### <a name="methods"></a>Méthodes

####  <a name="addfileattachmentasyncuri-attachmentname-options-callback"></a>addFileAttachmentAsync(uri, attachmentName, [options], [callback])

Ajoute un fichier à un message ou un rendez-vous en pièce jointe.

La méthode `addFileAttachmentAsync` charge le fichier depuis l’URI spécifié et le joint à l’élément dans le formulaire de composition.

L’identificateur peut être utilisé avec la méthode [`removeAttachmentAsync`](#removeattachmentasyncattachmentid-options-callback) pour supprimer la pièce jointe dans la même session.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Attributs| Description|
|---|---|---|---|
|`uri`| String||L’URI indiquant l’emplacement du fichier à joindre au message ou au rendez-vous. La longueur maximale est de 2 048 caractères.|
|`attachmentName`| String||Nom de la pièce jointe affiché lors de son chargement. La longueur maximale est de 255 caractères.|
|`options`| Objet| &lt;facultatif&gt;|Littéral d’objet contenant une ou plusieurs des propriétés suivantes.|
|`options.asyncContext`| Objet| &lt;facultatif&gt;|Les développeurs peuvent indiquer un objet auquel ils souhaitent accéder dans la méthode de rappel.|
|`callback`| function| &lt;facultatif&gt;|Quand la méthode se termine, la fonction passée dans le paramètre `callback` est appelée avec un seul paramètre, `asyncResult`, qui est un objet [`AsyncResult`](/javascript/api/office/office.asyncresult). <br/>En cas de réussite, l’identificateur de pièce jointe est fourni dans la propriété `asyncResult.value`.<br/>En cas d’échec du téléchargement de la pièce jointe, l’objet `asyncResult` contient un objet `Error` indiquant une description de l’erreur.|

##### <a name="errors"></a>Erreurs

| Code d’erreur | Description |
|------------|-------------|
| `AttachmentSizeExceeded` | La pièce jointe dépasse la taille autorisée. |
| `FileTypeNotSupported` | La pièce jointe comporte une extension qui n’est pas autorisée. |
| `NumberOfAttachmentsExceeded` | Le message ou le rendez-vous comporte un trop grand nombre de pièces jointes. |

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.1|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadWriteItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition|

##### <a name="example"></a>Exemple

```JavaScript
function callback(result) {
  if (result.error) {
    showMessage(result.error);
  } else {
    showMessage("Attachment added");
  }
}

function addAttachment() {
  // The values in asyncContext can be accessed in the callback
  var options = { 'asyncContext': { var1: 1, var2: 2 } };

  var attachmentURL = "https://contoso.com/rtm/icon.png";
  Office.context.mailbox.item.addFileAttachmentAsync(attachmentURL, attachmentURL, options, callback);
}
```

####  <a name="additemattachmentasyncitemid-attachmentname-options-callback"></a>addItemAttachmentAsync(itemId, attachmentName, [options], [callback])

Ajoute un élément Exchange, comme un message, en pièce jointe au message ou au rendez-vous.

La méthode `addItemAttachmentAsync` joint l’élément avec l’identificateur Exchange spécifié à l’élément du formulaire de composition. Si vous spécifiez une méthode de rappel, la méthode est appelée avec un paramètre, `asyncResult`, qui contient l’identificateur de pièce jointe ou un code indiquant toute erreur survenue lors de l’ajout de l’élément en tant que pièce jointe. Si nécessaire, vous pouvez utiliser le paramètre `options` pour transmettre des informations d’état à la méthode de rappel.

L’identificateur peut être utilisé avec la méthode [`removeAttachmentAsync`](#removeattachmentasyncattachmentid-options-callback) pour supprimer la pièce jointe dans la même session.

Si votre complément Office est exécuté dans la Outlook Web App , la méthode `addItemAttachmentAsync` peut joindre des éléments à des éléments autres que ceux que vous modifiez, mais cette action n’est pas prise en charge et est déconseillée.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Attributs| Description|
|---|---|---|---|
|`itemId`| String||Identificateur Exchange de l’élément à joindre. La taille maximale est de 100 caractères.|
|`attachmentName`| String||Objet de l’élément à joindre. La longueur maximale est de 255 caractères.|
|`options`| Objet| &lt;facultatif&gt;|Littéral d’objet contenant une ou plusieurs des propriétés suivantes.|
|`options.asyncContext`| Objet| &lt;facultatif&gt;|Les développeurs peuvent indiquer un objet auquel ils souhaitent accéder dans la méthode de rappel.|
|`callback`| function| &lt;facultatif&gt;|Quand la méthode se termine, la fonction passée dans le paramètre `callback` est appelée avec un seul paramètre, `asyncResult`, qui est un objet [`AsyncResult`](/javascript/api/office/office.asyncresult). <br/>En cas de réussite, l’identificateur de pièce jointe est fourni dans la propriété `asyncResult.value`.<br/>En cas d’échec de l’ajout de la pièce jointe, l’objet `asyncResult` contient un objet `Error` indiquant une description de l’erreur.|

##### <a name="errors"></a>Erreurs

| Code d’erreur | Description |
|------------|-------------|
| `NumberOfAttachmentsExceeded` | Le message ou le rendez-vous comporte un trop grand nombre de pièces jointes. |

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.1|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadWriteItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition|

##### <a name="example"></a>Exemple

L’exemple suivant ajoute un élément Outlook existant en tant que pièce jointe avec le nom `My Attachment`.

```JavaScript
function callback(result) {
  if (result.error) {
    showMessage(result.error);
  } else {
    showMessage("Attachment added");
  }
}

function addAttachment() {
  // EWS ID of item to attach
  // (Shortened for readability)
  var itemId = "AAMkADI1...AAA=";

  // The values in asyncContext can be accessed in the callback
  var options = { 'asyncContext': { var1: 1, var2: 2 } };

  Office.context.mailbox.item.addItemAttachmentAsync(itemId, "My Attachment", options, callback);
}
```

#### <a name="displayreplyallformformdata"></a>displayReplyAllForm(formData)

Affiche un formulaire de réponse qui inclut, soit l’expéditeur et tous les destinataires du message sélectionné, soit l’organisateur et tous les participants du rendez-vous sélectionné.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

Sur Outlook Web App, le formulaire de réponse s’affiche sous forme de formulaire isolé dans l’affichage à 3 colonnes et sous forme de formulaire contextuel dans l’affichage à 1 ou 2 colonnes.

Si un des paramètres de chaîne dépasse la limite, `displayReplyAllForm` lève une exception.

> [!NOTE]
> La possibilité d’inclure des pièces jointes dans l’appel à `displayReplyAllForm` n’est pas prise en charge dans l’ensemble des conditions requises 1.1. La prise en charge des pièces jointes a été ajoutée à `displayReplyAllForm` dans les versions d’ensemble de conditions requises 1.2 et supérieures.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Description|
|---|---|---|
|`formData`| String | Object| |Chaîne qui contient du texte et des éléments HTML et qui représente le texte du formulaire de réponse. La chaîne est limitée à 32 Ko.<br/>**OU**<br/>Objet qui contient les données du corps du message ou des pièces jointes et une fonction de rappel. L’objet est défini de la manière suivante : |
| `formData.htmlBody` | String | &lt;facultatif&gt; | Chaîne qui contient du texte et des éléments HTML et qui représente le corps du formulaire de réponse. La chaîne est limitée à 32 Ko.
| `callback` | function | &lt;facultatif&gt; | Une fois la méthode exécutée, la fonction transmise au paramètre `callback` est appelée avec un seul paramètre, `asyncResult`, qui est un objet [AsyncResult](/javascript/api/office/office.asyncresult). |

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="examples"></a>Exemples

Le code suivant transmet une chaîne à la fonction `displayReplyAllForm`.

```JavaScript
Office.context.mailbox.item.displayReplyAllForm('hello there');
Office.context.mailbox.item.displayReplyAllForm('<b>hello there</b>');
```

Réponse sans texte.

```JavaScript
Office.context.mailbox.item.displayReplyAllForm({});
```

Réponse avec seulement un corps de message.

```JavaScript
Office.context.mailbox.item.displayReplyAllForm(
{
  'htmlBody' : 'hi'
});
```

Réponse avec un corps et un rappel.

```JavaScript
Office.context.mailbox.item.displayReplyAllForm(
{
  'htmlBody' : 'hi',
  'callback' : function(asyncResult)
  {
    console.log(asyncResult.value);
  }
});
```

#### <a name="displayreplyformformdata"></a>displayReplyForm(formData)

Affiche un formulaire de réponse qui comprend uniquement l’expéditeur du message sélectionné ou l’organisateur du rendez-vous sélectionné.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

Sur Outlook Web App, le formulaire de réponse s’affiche sous forme de formulaire isolé dans l’affichage à 3 colonnes et sous forme de formulaire contextuel dans l’affichage à 1 ou 2 colonnes.

Si un des paramètres de chaîne dépasse la limite, `displayReplyForm` lève une exception.

> [!NOTE]
> La possibilité d’inclure des pièces jointes dans l’appel à `displayReplyForm` n’est pas prise en charge dans l’ensemble des conditions requises 1.1. La prise en charge des pièces jointes a été ajoutée à `displayReplyForm` dans les versions d’ensemble de conditions requises 1.2 et supérieures.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Description|
|---|---|---|
|`formData`| String | Object| | Chaîne qui contient du texte et des éléments HTML et qui représente le texte du formulaire de réponse. La chaîne est limitée à 32 Ko.<br/>**OU**<br/>Objet qui contient les données du corps du message ou des pièces jointes et une fonction de rappel. L’objet est défini de la manière suivante : |
| `formData.htmlBody` | String | &lt;facultatif&gt; | Chaîne qui contient du texte et des éléments HTML et qui représente le corps du formulaire de réponse. La chaîne est limitée à 32 Ko.
| `callback` | function | &lt;facultatif&gt; | Une fois la méthode exécutée, la fonction transmise au paramètre `callback` est appelée avec un seul paramètre, `asyncResult`, qui est un objet [AsyncResult](/javascript/api/office/office.asyncresult). |

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="examples"></a>Exemples

Le code suivant transmet une chaîne à la fonction `displayReplyForm`.

```JavaScript
Office.context.mailbox.item.displayReplyForm('hello there');
Office.context.mailbox.item.displayReplyForm('<b>hello there</b>');
```

Réponse sans texte.

```JavaScript
Office.context.mailbox.item.displayReplyForm({});
```

Réponse avec seulement un corps de message.

```JavaScript
Office.context.mailbox.item.displayReplyForm(
{
  'htmlBody' : 'hi'
});
```

Réponse avec un corps et un rappel.

```JavaScript
Office.context.mailbox.item.displayReplyForm(
{
  'htmlBody' : 'hi',
  'callback' : function(asyncResult)
  {
    console.log(asyncResult.value);
  }
});
```

#### <a name="getentities--entitiesjavascriptapioutlook11officeentities"></a>getEntities() → {[Entities](/javascript/api/outlook_1_1/office.entities)}

Obtient les entités figurant dans le texte de l’élément sélectionné.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="returns"></a>Renvoie :

Type : [Entités](/javascript/api/outlook_1_1/office.entities)

##### <a name="example"></a>Exemple

L’exemple suivant accède aux entités de contacts dans l’élément actif.

```JavaScript
var contacts = Office.context.mailbox.item.getEntities().contacts;
```

#### <a name="getentitiesbytypeentitytype--nullable-arraystringcontactjavascriptapioutlook11officecontactmeetingsuggestionjavascriptapioutlook11officemeetingsuggestionphonenumberjavascriptapioutlook11officephonenumbertasksuggestionjavascriptapioutlook11officetasksuggestion"></a>getEntitiesByType(entityType) → (nullable) {Array.<(String|[Contact](/javascript/api/outlook_1_1/office.contact)|[MeetingSuggestion](/javascript/api/outlook_1_1/office.meetingsuggestion)|[PhoneNumber](/javascript/api/outlook_1_1/office.phonenumber)|[TaskSuggestion](/javascript/api/outlook_1_1/office.tasksuggestion))>}

Obtient un tableau de toutes les entités du type spécifié trouvées dans le texte de l’élément sélectionné.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Description|
|---|---|---|
|`entityType`| [Office.MailboxEnums.EntityType](/javascript/api/outlook_1_1/office.MailboxEnums.entitytype)|Une des valeurs d’énumération EntityType.|

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| Restreint|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="returns"></a>Renvoie :

Si la valeur transmise à `entityType` n’est pas un membre valide de l’énumération `EntityType`, la méthode renvoie la valeur null. Si aucune entité du type spécifié n’est présente dans le texte de l’élément, la méthode renvoie un tableau vide. Sinon, le type des objets dans le tableau renvoyé dépend du type d’entité demandé dans le paramètre `entityType`.

Alors que le niveau d’autorisation minimal **Restricted** suffit pour utiliser cette méthode, certains types d’entité nécessitent le niveau **ReadItem** pour pouvoir y accéder, comme indiqué dans le tableau suivant.

| Valeur de `entityType` | Type des objets dans le tableau renvoyé | Niveau d’autorisation requis |
| --- | --- | --- |
| `Address` | String | **Restreint** |
| `Contact` | Contact | **ReadItem** |
| `EmailAddress` | String | **ReadItem** |
| `MeetingSuggestion` | MeetingSuggestion | **ReadItem** |
| `PhoneNumber` | PhoneNumber | **Restreint** |
| `TaskSuggestion` | TaskSuggestion | **ReadItem** |
| `URL` | String | **Restreint** |

Type:  Array.<(String|[Contact](/javascript/api/outlook_1_1/office.contact)|[MeetingSuggestion](/javascript/api/outlook_1_1/office.meetingsuggestion)|[PhoneNumber](/javascript/api/outlook_1_1/office.phonenumber)|[TaskSuggestion](/javascript/api/outlook_1_1/office.tasksuggestion))>


##### <a name="example"></a>Exemple

L’exemple suivant montre comment accéder à un tableau de chaînes qui représente des adresses postales dans le texte de l’élément actif.

```JavaScript
// The initialize function is required for all apps.
Office.initialize = function () {
  // Checks for the DOM to load using the jQuery ready function.
  $(document).ready(function () {
    // After the DOM is loaded, app-specific code can run.
    var item = Office.context.mailbox.item;
    // Get an array of strings that represent postal addresses in the current item's body.
    var addresses = item.getEntitiesByType(Office.MailboxEnums.EntityType.Address);
    // Continue processing the array of addresses.
  });
}
```

#### <a name="getfilteredentitiesbynamename--nullable-arraystringcontactjavascriptapioutlook11officecontactmeetingsuggestionjavascriptapioutlook11officemeetingsuggestionphonenumberjavascriptapioutlook11officephonenumbertasksuggestionjavascriptapioutlook11officetasksuggestion"></a>getFilteredEntitiesByName(name) → (nullable) {Array.<(String|[Contact](/javascript/api/outlook_1_1/office.contact)|[MeetingSuggestion](/javascript/api/outlook_1_1/office.meetingsuggestion)|[PhoneNumber](/javascript/api/outlook_1_1/office.phonenumber)|[TaskSuggestion](/javascript/api/outlook_1_1/office.tasksuggestion))>}

Renvoie des entités reconnues dans l’élément sélectionné, qui transmettent le filtre nommé défini au fichier manifeste XML.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

La méthode `getFilteredEntitiesByName` renvoie les entités qui correspondent à l’expression régulière définie dans l’élément de règle [ItemHasKnownEntity](/office/dev/add-ins/reference/manifest/rule#itemhasknownentity-rule) du fichier manifeste XML ayant la valeur de l’élément `FilterName` spécifié.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Description|
|---|---|---|
|`name`| String|Nom de l’élément de règle `ItemHasKnownEntity` qui définit le filtre à respecter.|

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="returns"></a>Renvoie :

Si aucun élément `ItemHasKnownEntity` dans le manifeste n’a une valeur d’élément `FilterName` qui correspond au paramètre `name`, la méthode renvoie `null`. Si le paramètre `name` correspond à un élément `ItemHasKnownEntity` dans le manifeste, mais qu’aucune entité dans l’élément actif ne correspond, la méthode renvoie un tableau vide.


Type : Array.<(String|[Contact](/javascript/api/outlook_1_1/office.contact)|[MeetingSuggestion](/javascript/api/outlook_1_1/office.meetingsuggestion)|[PhoneNumber](/javascript/api/outlook_1_1/office.phonenumber)|[TaskSuggestion](/javascript/api/outlook_1_1/office.tasksuggestion))>


#### <a name="getregexmatches--object"></a>getRegExMatches() → {Object}

Renvoie des valeurs de chaîne dans l’élément sélectionné, qui correspondent aux expressions régulières définies dans le fichier manifeste XML.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

La méthode `getRegExMatches` renvoie les chaînes qui correspondent à l’expression régulière définie dans chaque élément de règle `ItemHasRegularExpressionMatch` ou `ItemHasKnownEntity` du fichier XML de manifeste. Pour une règle `ItemHasRegularExpressionMatch`, une chaîne correspondante doit être présente dans la propriété de l’élément spécifié par cette règle. Le type simple `PropertyName` définit les propriétés prises en charge.

Par exemple, supposons qu’un manifeste de complément contienne l’élément `Rule` suivant :

```JavaScript
<Rule xsi:type="RuleCollection" Mode="And">
  <Rule xsi:type="ItemIs" FormType="Read" ItemType="Message" />
  <Rule xsi:type="RuleCollection" Mode="Or">
    <Rule xsi:type="ItemHasRegularExpressionMatch" RegExName="fruits" RegExValue="apple|banana|coconut" PropertyName="BodyAsPlaintext" IgnoreCase="true" />
    <Rule xsi:type="ItemHasRegularExpressionMatch" RegExName="veggies" RegExValue="tomato|onion|spinach|broccoli" PropertyName="BodyAsPlaintext" IgnoreCase="true" />
  </Rule>
</Rule>
```

L’objet renvoyé depuis `getRegExMatches` aurait deux propriétés : `fruits` et `veggies`.

```JavaScript
{
  'fruits': ['apple','banana','Banana','coconut'],
  'veggies': ['tomato','onion','spinach','broccoli']
}
```

> [!NOTE]
> Si vous spécifiez une règle `ItemHasRegularExpressionMatch` pour la propriété de corps d’un élément, l’expression régulière doit filtrer davantage le corps. Par ailleurs, elle ne doit pas tenter de renvoyer l’intégralité du corps de l’élément. L’utilisation d’une expression régulière telle que `.*` pour obtenir l’intégralité du corps d’un élément ne renvoie pas toujours les résultats attendus.

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="returns"></a>Renvoie :

Un objet qui contient les tableaux des chaînes correspondant aux expressions régulières définies dans le fichier XML de manifeste. Le nom de chaque tableau est égal à la valeur correspondante de l’attribut `RegExName` de la règle `ItemHasRegularExpressionMatch` correspondante ou de l’attribut `FilterName` de la règle `ItemHasKnownEntity` correspondante.

<dl class="param-type">

<dt>Type</dt>

<dd>Objet</dd>

</dl>

##### <a name="example"></a>Exemple

L’exemple suivant montre comment accéder au tableau de correspondances pour les <rule>éléments d’expression régulière `fruits` et `veggies`, spécifiés dans le manifeste.</rule>

```JavaScript
var allMatches = Office.context.mailbox.item.getRegExMatches();
var fruits = allMatches.fruits;
var veges = allMatches.veggies;
```

#### <a name="getregexmatchesbynamename--nullable-array-string-"></a>getRegExMatchesByName(name) → (nullable) {Array.< String >}

Renvoie des valeurs de chaîne dans l’élément sélectionné, qui correspondent aux expressions régulières nommées définies dans le fichier XML de manifeste.

> [!NOTE]
> Cette méthode n’est pas prise en charge dans Outlook pour iOS ou Outlook pour Android.

La méthode `getRegExMatchesByName` renvoie les chaînes qui correspondent à l’expression régulière définie dans l’élément de règle `ItemHasRegularExpressionMatch` du fichier XML de manifeste ayant la valeur de l’élément `RegExName` spécifié.

Si vous spécifiez une règle `ItemHasRegularExpressionMatch` pour la propriété de texte d’un élément, l’expression régulière doit filtrer davantage le texte. Par ailleurs, elle ne doit pas tenter de renvoyer l’intégralité du texte de l’élément. L’utilisation d’une expression régulière telle que `.*` pour obtenir l’intégralité du texte d’un élément ne renvoie pas toujours les résultats attendus.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Description|
|---|---|---|
|`name`| String|Nom de l’élément de règle `ItemHasRegularExpressionMatch` qui définit le filtre à respecter.|

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Lecture|

##### <a name="returns"></a>Renvoie :

Un tableau qui contient les chaînes correspondant à l’expression régulière définie dans le fichier manifeste XML.

<dl class="param-type">

<dt>Type</dt>

<dd>Array.< String ></dd>

</dl>

##### <a name="example"></a>Exemple

```JavaScript
var fruits = Office.context.mailbox.item.getRegExMatchesByName("fruits");
var veggies = Office.context.mailbox.item.getRegExMatchesByName("veggies");
```

####  <a name="loadcustompropertiesasynccallback-usercontext"></a>loadCustomPropertiesAsync(callback, [userContext])

Charge de manière asynchrone les propriétés personnalisées de ce complément vers l’élément sélectionné.

Les propriétés personnalisées sont stockées sous la forme de paires clé/valeur qui s’appliquent à une application ou un élément. Cette méthode renvoie un objet `CustomProperties` dans le rappel, qui fournit des méthodes pour accéder aux propriétés personnalisées propres à l’élément et au complément actifs. Les propriétés personnalisées ne sont pas chiffrées dans l’élément, par conséquent elles ne doivent pas servir d’espace de stockage sécurisé.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Attributs| Description|
|---|---|---|---|
|`callback`| function||Quand la méthode se termine, la fonction passée dans le paramètre `callback` est appelée avec un seul paramètre, `asyncResult`, qui est un objet [`AsyncResult`](/javascript/api/office/office.asyncresult).<br/><br/>Les propriétés personnalisées sont fournies sous la forme d’un objet [`CustomProperties`](/javascript/api/outlook_1_1/office.customproperties) dans la propriété `asyncResult.value`. Cet objet peut être utilisé pour obtenir, définir et supprimer les propriétés personnalisées de l’élément et sauvegarder les modifications du jeu de propriétés personnalisées sur le serveur.|
|`userContext`| Objet| &lt;facultatif&gt;|Les développeurs peuvent fournir n'importe quel objet auquel ils souhaitent accéder dans la méthode de rappel. Cet objet est accessible via la propriété `asyncResult.asyncContext` dans la fonction de rappel.|

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.0|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition ou lecture|

##### <a name="example"></a>Exemple

L’exemple de code suivant montre comment utiliser la méthode `loadCustomPropertiesAsync` pour charger de manière asynchrone des propriétés personnalisées spécifiques vers l’élément actif. L’exemple montre également comment utiliser la méthode `CustomProperties.saveAsync` pour réenregistrer ces propriétés sur le serveur. Une fois le chargement des propriétés personnalisées terminé, l’exemple de code utilise la méthode `CustomProperties.get` pour lire la propriété personnalisée `myProp`, utilise la méthode `CustomProperties.set` pour écrire la propriété personnalisée `otherProp`, puis appelle enfin la méthode `saveAsync` pour enregistrer les propriétés personnalisées.

```JavaScript
// The initialize function is required for all add-ins.
Office.initialize = function () {
  // Checks for the DOM to load using the jQuery ready function.
  $(document).ready(function () {
  // After the DOM is loaded, add-in-specific code can run.
  var item = Office.context.mailbox.item;
  item.loadCustomPropertiesAsync(customPropsCallback);
  });
}

function customPropsCallback(asyncResult) {
  var customProps = asyncResult.value;
  var myProp = customProps.get("myProp");

  customProps.set("otherProp", "value");
  customProps.saveAsync(saveCallback);
}

function saveCallback(asyncResult) {
}
```

####  <a name="removeattachmentasyncattachmentid-options-callback"></a>removeAttachmentAsync(attachmentId, [options], [callback])

Supprime une pièce jointe d’un message ou d’un rendez-vous.

La méthode `removeAttachmentAsync` supprime la pièce jointe avec l’identificateur spécifié de l’élément. Nous vous recommandons vivement de supprimer une pièce jointe à l’aide de son identificateur uniquement si la même application de messagerie a ajouté cette pièce jointe au cours de la même session. Dans Outlook Web App et OWA pour les appareils, l’identificateur de pièce jointe n’est valable que dans la même session. Une session est terminée lorsque l’utilisateur ferme l’application, ou si celui-ci commence à composer dans un formulaire inclus et qu’il le fait ensuite apparaître dans une nouvelle fenêtre séparée.

##### <a name="parameters"></a>Paramètres :

|Nom| Type| Attributs| Description|
|---|---|---|---|
|`attachmentId`| String||Identificateur de la pièce jointe à supprimer. La longueur maximale de la chaîne est de 100 caractères.|
|`options`| Objet| &lt;facultatif&gt;|Littéral d’objet contenant une ou plusieurs des propriétés suivantes.|
|`options.asyncContext`| Objet| &lt;facultatif&gt;|Les développeurs peuvent indiquer un objet auquel ils souhaitent accéder dans la méthode de rappel.|
|`callback`| function| &lt;facultatif&gt;|Quand la méthode se termine, la fonction passée dans le paramètre `callback` est appelée avec un seul paramètre, `asyncResult`, qui est un objet [`AsyncResult`](/javascript/api/office/office.asyncresult). <br/>En cas d’échec de la suppression de la pièce jointe, la propriété `asyncResult.error` contient un code d’erreur et la raison de l’échec.|

##### <a name="errors"></a>Erreurs

| Code d’erreur | Description |
|------------|-------------|
| `InvalidAttachmentId` | L’identificateur de la pièce jointe n’existe pas. |

##### <a name="requirements"></a>Conditions requises

|Condition requise| Valeur|
|---|---|
|[Version minimale de l’ensemble de conditions requises de boîte aux lettres](/office/dev/add-ins/reference/requirement-sets/outlook-api-requirement-sets)| 1.1|
|[Niveau minimal d’autorisation](https://docs.microsoft.com/outlook/add-ins/understanding-outlook-add-in-permissions)| ReadWriteItem|
|[Mode Outlook applicable](https://docs.microsoft.com/outlook/add-ins/#extension-points)| Composition|

##### <a name="example"></a>Exemple

Le code suivant supprime une pièce jointe dont l’identificateur est « 0 ».

```JavaScript
Office.context.mailbox.item.removeAttachmentAsync(
  '0',
  { asyncContext : null },
  function (asyncResult)
  {
    console.log(asyncResult.status);
  }
);
```