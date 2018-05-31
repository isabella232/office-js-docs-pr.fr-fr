---
title: Localisation des compléments Office
description: ''
ms.date: 01/23/2018
ms.openlocfilehash: d7888859ca29a62541020b45b0b7a3638c41f4f2
ms.sourcegitcommit: c72c35e8389c47a795afbac1b2bcf98c8e216d82
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2018
ms.locfileid: "19437737"
---
# <a name="localization-for-office-add-ins"></a><span data-ttu-id="c730d-102">Localisation des compléments Office</span><span class="sxs-lookup"><span data-stu-id="c730d-102">Localization for Office Add-ins</span></span>

<span data-ttu-id="c730d-p101">Vous pouvez librement implémenter n’importe quel schéma de localisation convenant à votre Complément Office. L’API JavaScript et le schéma du manifeste de la plateforme Compléments Office offrent quelques choix. Vous pouvez utiliser l’API JavaScript pour Office pour déterminer un paramètre régional et les chaînes d’affichage en fonction des paramètres régionaux de l’application hôte, ou pour interpréter ou afficher les données en fonction des paramètres régionaux des données. Vous pouvez utiliser le manifeste pour spécifier l’emplacement des fichiers et les informations descriptives propres à un paramètre régional. Sinon, vous pouvez utiliser un script Microsoft Ajax pour prendre en charge l’internationalisation et la localisation.</span><span class="sxs-lookup"><span data-stu-id="c730d-p101">You can implement any localization scheme that's appropriate for your Office Add-in. The JavaScript API and manifest schema of the Office Add-ins platform provide some choices. You can use the JavaScript API for Office to determine a locale and display strings based on the locale of the host application, or to interpret or display data based on the locale of the data. You can use the manifest to specify locale-specific add-in file location and descriptive information. Alternatively, you can use Microsoft Ajax script to support globalization and localization.</span></span>

## <a name="use-the-javascript-api-to-determine-locale-specific-strings"></a><span data-ttu-id="c730d-108">Utiliser l’API JavaScript pour déterminer les chaînes propres aux paramètres régionaux</span><span class="sxs-lookup"><span data-stu-id="c730d-108">Use the JavaScript API to determine locale-specific strings</span></span>

<span data-ttu-id="c730d-109">L’API JavaScript pour Office offre deux propriétés qui prennent en charge l’affichage ou l’interprétation de valeurs cohérentes avec les paramètres régionaux de l’application hôte et des données :</span><span class="sxs-lookup"><span data-stu-id="c730d-109">The JavaScript API for Office provides two properties that support displaying or interpreting values consistent with the locale of the host application and data:</span></span>

- <span data-ttu-id="c730d-p102">[Context.displayLanguage][displayLanguage] spécifie les paramètres régionaux (ou langue) de l’interface utilisateur de l’application hôte. L’exemple suivant vérifie si l’application hôte utilise les paramètres régionaux en-US ou fr-Fr, et affiche un message de bienvenue propre aux paramètres régionaux.</span><span class="sxs-lookup"><span data-stu-id="c730d-p102">[Context.displayLanguage][displayLanguage] specifies the locale (or language) of the user interface of the host application. The following example verifies if the host application uses the en-US or fr-Fr locale, and displays a locale-specific greeting.</span></span>
    
    ```js
    function sayHelloWithDisplayLanguage() {
        var myLanguage = Office.context.displayLanguage;
        switch (myLanguage) {
            case 'en-US':
                write('Hello!');
                break;
            case 'fr-FR':
                write('Bonjour!');
                break;
        }
    }
    
    // Function that writes to a div with id='message' on the page.
    function write(message) {
        document.getElementById('message').innerText += message; 
    }
    ```

- <span data-ttu-id="c730d-p103">[Context.contentLanguage][contentLanguage] spécifie le paramètre régional (ou langue) des données. Le fait d’étendre le dernier exemple de code, au lieu de vérifier la propriété [displayLanguage], attribue `myLanguage` à la propriété [contentLanguage] et utilise le reste du code pour afficher un message de bienvenue correspondant aux paramètres régionaux des données :</span><span class="sxs-lookup"><span data-stu-id="c730d-p103">[Context.contentLanguage][contentLanguage] specifies the locale (or language) of the data. Extending the last code sample, instead of checking the [displayLanguage] property, assign `myLanguage` to the [contentLanguage] property, and use the rest of the same code to display a greeting based on the locale of the data:</span></span>
    
    ```js
    var myLanguage = Office.context.contentLanguage;
    ```

## <a name="control-localization-from-the-manifest"></a><span data-ttu-id="c730d-114">Contrôler la localisation à partir du manifeste</span><span class="sxs-lookup"><span data-stu-id="c730d-114">Control localization from the manifest</span></span>


<span data-ttu-id="c730d-p104">Chaque complément Office indique un élément [DefaultLocale] élément et un paramètre régional dans son manifeste. Par défaut, la plateforme de complément Office et les applications hôtes Office appliquent les valeurs des éléments [Description], [DisplayName], [IconUrl], [HighResolutionIconUrl] et [SourceLocation] à tous les paramètres régionaux. Vous pouvez éventuellement prendre en charge des valeurs spécifiques pour les paramètres régionaux spécifiques, en spécifiant un élément enfant [Override] pour chaque paramètre régional supplémentaire, pour chacun des cinq éléments. La valeur de l’élément [DefaultLocale] et de l’attribut `Locale` de l’élément [Override] est spécifiée en fonction de la norme [RFC 3066] relative aux balises pour l’identification des langues (« Tags for the Identification of Languages »). Le tableau 1 décrit la prise en charge de localisation de ces éléments.</span><span class="sxs-lookup"><span data-stu-id="c730d-p104">Every Office Add-in specifies a [DefaultLocale] element and a locale in its manifest. By default, the Office Add-in platform and Office host applications apply the values of the [Description], [DisplayName], [IconUrl], [HighResolutionIconUrl], and [SourceLocation] elements to all locales. You can optionally support specific values for specific locales, by specifying an [Override] child element for each additional locale, for any of these five elements. The value for the [DefaultLocale] element and for the `Locale` attribute of the [Override] element is specified according to [RFC 3066], "Tags for the Identification of Languages." Table 1 describes the localizing support for these elements.</span></span>

<span data-ttu-id="c730d-120">**Tableau 1. Prise en charge de localisation**</span><span class="sxs-lookup"><span data-stu-id="c730d-120">**Table 1. Localization support**</span></span>


|<span data-ttu-id="c730d-121">**Élément**</span><span class="sxs-lookup"><span data-stu-id="c730d-121">**Element**</span></span>|<span data-ttu-id="c730d-122">**Prise en charge de localisation**</span><span class="sxs-lookup"><span data-stu-id="c730d-122">**Localization support**</span></span>|
|:-----|:-----|
|<span data-ttu-id="c730d-123">[Description]</span><span class="sxs-lookup"><span data-stu-id="c730d-123">[Description]</span></span>   |<span data-ttu-id="c730d-124">Les utilisateurs de chaque paramètre régional que vous spécifiez peuvent voir une description localisée du complément dans AppSource (ou dans un catalogue privé).</span><span class="sxs-lookup"><span data-stu-id="c730d-124">Users in each locale you specify can see a localized description for the add-in in AppSource (or private catalog).</span></span><br/><span data-ttu-id="c730d-125">Pour les compléments Outlook, les utilisateurs peuvent voir la description dans le Centre d’administration Exchange (EAC) après l’installation.</span><span class="sxs-lookup"><span data-stu-id="c730d-125">For Outlook add-ins, users can see the description in the Exchange Admin Center (EAC) after installation.</span></span>|
|<span data-ttu-id="c730d-126">[DisplayName]</span><span class="sxs-lookup"><span data-stu-id="c730d-126">[DisplayName]</span></span>   |<span data-ttu-id="c730d-127">Les utilisateurs de chaque paramètre régional que vous spécifiez peuvent voir une description localisée du complément dans AppSource (ou dans un catalogue privé).</span><span class="sxs-lookup"><span data-stu-id="c730d-127">Users in each locale you specify can see a localized description for the add-in in AppSource (or private catalog).</span></span><br/><span data-ttu-id="c730d-128">Pour les compléments Outlook, les utilisateurs peuvent voir le nom d’affichage sous forme d’étiquette pour le bouton de l’application Outlook ainsi que dans l’EAC après l’installation.</span><span class="sxs-lookup"><span data-stu-id="c730d-128">For Outlook add-ins, users can see the display name as a label for the Outlook add-in button and in the EAC after installation.</span></span><br/><span data-ttu-id="c730d-129">Pour les compléments de contenu et du volet Office, les utilisateurs peuvent voir l’icône dans le ruban après avoir installé l’application.</span><span class="sxs-lookup"><span data-stu-id="c730d-129">For content and task pane add-ins, users can see the display name in the ribbon after installing the add-in.</span></span>|
|<span data-ttu-id="c730d-130">[IconUrl]</span><span class="sxs-lookup"><span data-stu-id="c730d-130">[IconUrl]</span></span>        |<span data-ttu-id="c730d-p105">L’image de l’icône est facultative. Vous pouvez utiliser la même technique de remplacement pour spécifier une image donnée pour une culture particulière. Si vous utilisez et localisez une icône, les utilisateurs de chaque paramètre régional que vous spécifiez peuvent voir l’image d’icône localisée pour le complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-p105">The icon image is optional. You can use the same override technique to specify a certain image for a specific culture. If you use and localize an icon, users in each locale you specify can see a localized icon image for the add-in.</span></span><br/><span data-ttu-id="c730d-134">Pour les compléments Outlook, les utilisateurs peuvent voir l’icône dans l’EAC après l’installation du complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-134">For Outlook add-ins, users can see the icon in the EAC after installing the add-in.</span></span><br/><span data-ttu-id="c730d-135">Pour les compléments de contenu et du volet de tâches, les utilisateurs peuvent voir l’icône dans le ruban après avoir installé le complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-135">For content and task pane add-ins, users can see the icon in the ribbon after installing the add-in.</span></span>|
|<span data-ttu-id="c730d-136">[HighResolutionIconUrl] **Important :** cet élément est disponible uniquement lors de l’utilisation de la version 1.1 du manifeste de complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-136">[HighResolutionIconUrl] **Important:** This element is available only when using add-in manifest version 1.1.</span></span>|<span data-ttu-id="c730d-p106">L’image de l’icône de haute résolution est facultative. Néanmoins, si elle est indiquée, elle doit l’être après l’élément [IconUrl]. Si  [HighResolutionIconUrl] est spécifié et que le complément est installé sur un appareil qui prend en charge la haute résolution (dpi), la valeur [HighResolutionIconUrl] est utilisée à la place de la valeur [IconUrl].</span><span class="sxs-lookup"><span data-stu-id="c730d-p106">The high resolution icon image is optional but if it is specified, it must occur after the  [IconUrl] element. When [HighResolutionIconUrl] is specified, and the add-in is installed on a device that supports high dpi resolution, the [HighResolutionIconUrl] value is used instead of the value for [IconUrl].</span></span><br/><span data-ttu-id="c730d-p107">Vous pouvez utiliser la même technique de remplacement pour spécifier une image donnée pour une culture particulière. Si vous utilisez et localisez une icône, les utilisateurs de chaque paramètre régional que vous spécifiez peuvent voir l’image d’icône localisée pour le complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-p107">You can use the same override technique to specify a certain image for a specific culture. If you use and localize an icon, users in each locale you specify can see a localized icon image for the add-in.</span></span><br/><span data-ttu-id="c730d-141">Pour les compléments Outlook, les utilisateurs peuvent voir l’icône dans l’EAC après l’installation du complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-141">For Outlook add-ins, users can see the icon in the EAC after installing the add-in.</span></span><br/><span data-ttu-id="c730d-142">Pour les compléments de contenu et du volet de tâches, les utilisateurs peuvent voir l’icône dans le ruban après avoir installé le complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-142">For content and task pane add-ins, users can see the icon in the ribbon after installing the add-in.</span></span>|
|<span data-ttu-id="c730d-143">[Ressources] **Important :** cet élément est disponible uniquement lors de l’utilisation de la version 1.1 du manifeste de complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-143">[Resources] **Important:** This element is available only when using add-in manifest version 1.1.</span></span>   |<span data-ttu-id="c730d-144">Les utilisateurs de chaque paramètre régional que vous spécifiez peuvent voir les ressources de chaîne et d’icône que vous créez spécifiquement pour le complément pour ce paramètre régional.</span><span class="sxs-lookup"><span data-stu-id="c730d-144">Users in each locale you specify can see string and icon resources that you specifically create for the add-in for that locale.</span></span> |
|<span data-ttu-id="c730d-145">[SourceLocation]</span><span class="sxs-lookup"><span data-stu-id="c730d-145">[SourceLocation]</span></span>   |<span data-ttu-id="c730d-146">Les utilisateurs de chaque paramètre régional que vous spécifiez peuvent voir une page web que vous concevez spécifiquement pour le complément pour ce paramètre régional.</span><span class="sxs-lookup"><span data-stu-id="c730d-146">Users in each locale you specify can see a webpage that you specifically design for the add-in for that locale.</span></span> |


> <span data-ttu-id="c730d-p108">**REMARQUE** Vous pouvez trouver la description et le nom d’affichage uniquement pour les paramètres régionaux pris en charge par Office. Reportez-vous à la rubrique [Identificateurs de langue et valeurs d'ID de l'élément OptionState dans Office 2013](http://technet.microsoft.com/en-us/library/cc179219.aspx) pour connaître la liste des langues et des paramètres régionaux pour la version actuelle d’Office.</span><span class="sxs-lookup"><span data-stu-id="c730d-p108">**NOTE** You can localize the description and display name for only the locales that Office supports. See [Language identifiers and OptionState Id values in Office 2013](http://technet.microsoft.com/en-us/library/cc179219.aspx) for a list of languages and locales for the current release of Office.</span></span>


### <a name="examples"></a><span data-ttu-id="c730d-149">Exemples</span><span class="sxs-lookup"><span data-stu-id="c730d-149">Examples</span></span>

<span data-ttu-id="c730d-p109">Par exemple, un complément Office peut spécifier [DefaultLocale] en tant que `en-us`. Pour l’élément [DisplayName], le complément peut spécifier un élément enfant [Override] pour le paramètre régional `fr-fr`, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c730d-p109">For example, an Office Add-in can specify the [DefaultLocale] as `en-us`. For the [DisplayName] element, the add-in can specify an [Override] child element for the locale `fr-fr`, as shown below.</span></span> 


```xml
<DefaultLocale>en-us</DefaultLocale>
...
<DisplayName DefaultValue="Video player">
    <Override Locale="fr-fr" Value="Lecteur vidéo" />
</DisplayName>
```

> <span data-ttu-id="c730d-p110">**REMARQUE** Si vous devez rechercher plusieurs domaines au sein d’une famille de langues, comme `de-de` et `de-at`, nous vous recommandons d’utiliser des éléments `Override` distincts pour chaque domaine. L’utilisation uniquement du nom de la langue, soit `de` dans ce cas, n’est pas prise en charge pour toutes les combinaisons de plateformes et d’applications hôte Office.</span><span class="sxs-lookup"><span data-stu-id="c730d-p110">**NOTE** If you need to localize for more than one area within a language family, such as `de-de` and `de-at`, we recommend that you use separate `Override` elements for each area. Using just the language name alone, in this case, `de`, is not supported across all combinations of Office host applications and platforms.</span></span>

<span data-ttu-id="c730d-p111">Cela signifie que le complément adopte le paramètre régional `en-us` par défaut. Les utilisateurs voient le nom d’affichage « Video player » pour tous les paramètres régionaux, sauf si le paramètre régional de l’ordinateur client est `fr-fr`, auquel cas ils verront le nom d’affichage « Lecteur vidéo ».</span><span class="sxs-lookup"><span data-stu-id="c730d-p111">This means that the add-in assumes the  `en-us` locale by default. Users see the English display name of "Video player" for all locales unless the client computer's locale is `fr-fr`, in which case users would see the French display name "Lecteur vidéo".</span></span>

> <span data-ttu-id="c730d-p112">**REMARQUE** Vous ne pouvez spécifier qu’un seul remplacement par langue, notamment pour les paramètres régionaux par défaut. Par exemple, si votre paramètre régional par défaut est `en-us`, vous ne pouvez pas spécifier un remplacement pour `en-us`.</span><span class="sxs-lookup"><span data-stu-id="c730d-p112">**NOTE** You may only specify a single override per language, including for the default locale. For example, if your default locale is `en-us` you cannot not specify an  override for `en-us` as well.</span></span> 

<span data-ttu-id="c730d-p113">L’exemple suivant applique un remplacement de paramètre régional pour l’élément [Description]. Il commence par spécifier le paramètre régional par défaut `en-us` et une description en anglais, puis spécifie une instruction [Override] avec une description en français pour le paramètre régional `fr-fr` :</span><span class="sxs-lookup"><span data-stu-id="c730d-p113">The following example applies a locale override for the [Description] element. It first specifies a default locale of `en-us` and an English description, and then specifies an [Override] statement with a French description for the `fr-fr` locale:</span></span>

```xml
<DefaultLocale>en-us</DefaultLocale>
...
<Description DefaultValue=
   "Watch YouTube videos referenced in the emails you receive 
   without leaving your email client.">
   <Override Locale="fr-fr" Value=
   "Visualisez les vidéos YouTube référencées dans vos courriers 
   électronique directement depuis Outlook et Outlook Web App."/>
</Description>
```

<span data-ttu-id="c730d-p114">Cela signifie que le complément considère `en-us` comme le paramètre régional par défaut. Les utilisateurs verront la description en anglais figurant dans l’attribut `DefaultValue` pour tous les paramètres régionaux, sauf si le paramètre régional de l’ordinateur du client est `fr-fr`, auquel cas la description s’affichera en français.</span><span class="sxs-lookup"><span data-stu-id="c730d-p114">This means that the add-in assumes the `en-us` locale by default. Users would see the English description in the `DefaultValue` attribute for all locales unless the client computer's locale is `fr-fr`, in which case they would see the French description.</span></span>

<span data-ttu-id="c730d-p115">Dans l’exemple suivant, le complément spécifie une image séparée convenant mieux au paramètre régional et à la culture `fr-fr`. Par défaut, les utilisateurs voient l’image DefaultLogo.png, sauf lorsque le paramètre régional de l’ordinateur client est `fr-fr`. Dans ce cas, les utilisateurs voient l’image FrenchLogo.png.</span><span class="sxs-lookup"><span data-stu-id="c730d-p115">In the following example, the add-in specifies a separate image that's more appropriate for the `fr-fr` locale and culture. Users see the image DefaultLogo.png by default, except when the locale of the client computer is `fr-fr`. In this case, users would see the image FrenchLogo.png.</span></span> 


```xml
<!-- Replace "domain" with a real web server name and path. -->
<IconUrl DefaultValue="https://<domain>/DefaultLogo.png"/>
<Override Locale="fr-fr" Value="https://<domain>/FrenchLogo.png"/>
```

<span data-ttu-id="c730d-p116">L’exemple suivant montre comment localiser une ressource dans la section `Resources`. Une valeur de remplacement des paramètres régionaux est appliquée pour une image plus appropriée par rapport à la culture `ja-jp`.</span><span class="sxs-lookup"><span data-stu-id="c730d-p116">The following example shows how to localize a resource in the `Resources` section. It applies a locale override for an image that is more appropriate for the `ja-jp` culture.</span></span>

```xml
<Resources>
      <bt:Images>
        <bt:Image id="icon1_16x16" DefaultValue="https://www.contoso.com/icon_default.png">
          <bt:Override Locale="ja-jp" Value="https://www.contoso.com/ja-jp16-icon_default.png" />
        </bt:Image>
 ...
```


<span data-ttu-id="c730d-p117">Pour l’élément [SourceLocation], la prise en charge de paramètres régionaux supplémentaires implique de fournir un fichier HTML source distinct pour chacun des paramètres régionaux spécifiés. Les utilisateurs de chaque paramètre régional que vous spécifiez peuvent accéder à une page web personnalisée conçue pour eux.</span><span class="sxs-lookup"><span data-stu-id="c730d-p117">For the [SourceLocation] element, supporting additional locales means providing a separate source HTML file for each of the specified locales. Users in each locale you specify can see a customized webpage that you design for that them.</span></span>

<span data-ttu-id="c730d-p118">Pour les compléments Outlook, l’élément [SourceLocation] s’aligne également sur le facteur de forme. Cela vous permet de fournir un fichier source HTML localisé distinct pour chaque format. Vous pouvez spécifier un ou plusieurs éléments enfant [Override] dans chaque élément de paramètres applicable ([DesktopSettings], [TabletSettings] ou [PhoneSettings]). L’exemple suivant montre les éléments de paramètres pour les formats ordinateur de bureau, tablette et smartphone, avec pour chacun un fichier HTML pour le paramètre régional par défaut et pour le paramètre régional français.</span><span class="sxs-lookup"><span data-stu-id="c730d-p118">For Outlook add-ins, the [SourceLocation] element also aligns to the form factor. This allows you to provide a separate, localized source HTML file for each corresponding form factor. You can specify one or more [Override] child elements in each applicable settings element ([DesktopSettings], [TabletSettings], or [PhoneSettings]). The following example shows settings elements for the desktop, tablet, and smartphone form factors, each with one HTML file for the default locale and another for the French locale.</span></span>


```xml
<DesktopSettings>
   <SourceLocation DefaultValue="https://contoso.com/Desktop.html">
      <Override Locale="fr-fr" Value="https://contoso.com/fr/Desktop.html" />
   </SourceLocation>
   <RequestedHeight>250</RequestedHeight>
</DesktopSettings>
<TabletSettings>
   <SourceLocation DefaultValue="https://contoso.com/Tablet.html">
      <Override Locale="fr-fr" Value="https://contoso.com/fr/Tablet.html" />
   </SourceLocation>
   <RequestedHeight>200</RequestedHeight>
</TabletSettings>
<PhoneSettings>
   <SourceLocation DefaultValue="https://contoso.com/Mobile.html">
      <Override Locale="fr-fr" Value="https://contoso.com/fr/Mobile.html" />
   </SourceLocation>
</PhoneSettings>
```

## <a name="match-datetime-format-with-client-locale"></a><span data-ttu-id="c730d-173">Mettre en correspondance le format de date/heure avec le paramètre régional du client</span><span class="sxs-lookup"><span data-stu-id="c730d-173">Match date/time format with client locale</span></span>

<span data-ttu-id="c730d-p119">Vous pouvez obtenir les paramètres régionaux de l’interface utilisateur de l’application d’hébergement en utilisant la propriété [displayLanguage]. Vous pouvez ensuite afficher les valeurs de date et d’heure dans un format cohérent avec les paramètres régionaux actuels de l’application hôte. Une solution consiste à préparer un fichier de ressources qui spécifie le format d’affichage de date/heure à utiliser pour chaque paramètre régional pris en charge par le complément Office. Lors de l’exécution, votre complément peut utiliser le fichier de ressources et faire correspondre le format de date/heure approprié avec le paramètre régional obtenu à partir de la propriété [displayLanguage].</span><span class="sxs-lookup"><span data-stu-id="c730d-p119">You can get the locale of the user interface of the hosting application by using the [displayLanguage] property. You can then display date and time values in a format consistent with the current locale of the host application. One way to do that is to prepare a resource file that specifies the date/time display format to use for each locale that your Office Add-in supports. At run time, your add-in can use the resource file and match the appropriate date/time format with the locale obtained from the [displayLanguage] property.</span></span>

<span data-ttu-id="c730d-p120">Vous pouvez obtenir les paramètres régionaux des données de l’application d’hébergement en utilisant la propriété [contentLanguage]. En fonction de cette valeur, vous pouvez correctement interpréter ou afficher des chaînes de date/heure. Par exemple, dans le paramètre régional `jp-JP`, les valeurs de date/heure sont exprimées sous la forme `yyyy/MM/dd`, alors qu’avec le paramètre régional `fr-FR` elles apparaissent sous la forme `dd/MM/yyyy`.</span><span class="sxs-lookup"><span data-stu-id="c730d-p120">You can get the locale of the data of the hosting application by using the [contentLanguage] property. Based on this value, you can then appropriately interpret or display date/time strings. For example, the `jp-JP` locale expresses data/time values as `yyyy/MM/dd`, and the `fr-FR` locale, `dd/MM/yyyy`.</span></span>


## <a name="use-ajax-for-globalization-and-localization"></a><span data-ttu-id="c730d-181">Utiliser Ajax pour l’internationalisation et la localisation</span><span class="sxs-lookup"><span data-stu-id="c730d-181">Use Ajax for globalization and localization</span></span>


<span data-ttu-id="c730d-182">Si vous utilisez Visual Studio pour créer des Compléments Office, .NET Framework et Ajax offrent des moyens d’internationaliser et de localiser les fichiers de script client.</span><span class="sxs-lookup"><span data-stu-id="c730d-182">If you use Visual Studio to create Office Add-ins, the .NET Framework and Ajax provide ways to globalize and localize client script files.</span></span>

<span data-ttu-id="c730d-p121">Vous pouvez internationaliser et utiliser les extensions de type JavaScript [Date](http://msdn.microsoft.com/library/caf98d32-2de2-4704-8198-692350343681.aspx) et [Number](http://msdn.microsoft.com/library/c216d3a1-12ae-47d1-bca1-c3666d04572f.aspx) ainsi que l’objet JavaScript [Date](http://msdn.microsoft.com/library/ce2202bb-7ec9-4f5a-bf48-3a04feff283e.aspx) dans le code JavaScript pour qu’une Complément Office affiche les valeurs en fonction des paramètres régionaux du navigateur actuel. Pour plus d’informations, voir [Walkthrough: Globalizing a Date by Using Client Script](http://msdn.microsoft.com/library/69b34e6d-d590-4d03-a763-b7ae54b47d74.aspx).</span><span class="sxs-lookup"><span data-stu-id="c730d-p121">You can globalize and use the [Date](http://msdn.microsoft.com/library/caf98d32-2de2-4704-8198-692350343681.aspx) and [Number](http://msdn.microsoft.com/library/c216d3a1-12ae-47d1-bca1-c3666d04572f.aspx) JavaScript type extensions and the JavaScript [Date](http://msdn.microsoft.com/library/ce2202bb-7ec9-4f5a-bf48-3a04feff283e.aspx) object in the JavaScript code for an Office Add-in to display values based on the locale settings on the current browser. For more information, see [Walkthrough: Globalizing a Date by Using Client Script](http://msdn.microsoft.com/library/69b34e6d-d590-4d03-a763-b7ae54b47d74.aspx).</span></span>

<span data-ttu-id="c730d-p122">Vous pouvez inclure des chaînes de ressources localisées directement dans des fichiers JavaScript autonomes pour fournir des fichiers de script client pour les différents paramètres régionaux, qui sont définis dans le navigateur ou fournis par l’utilisateur. Créez un fichier de script distinct pour chaque paramètre régional pris en charge. Dans chaque fichier de script, incluez un objet au format JSON contenant les chaînes de ressources pour ce paramètre régional. Les valeurs localisées sont appliquées lorsque le script s’exécute dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="c730d-p122">You can include localized resource strings directly in standalone JavaScript files to provide client script files for different locales, which are set on the browser or provided by the user. Create a separate script file for each supported locale. In each script file, include an object in JSON format that contains the resource strings for that locale. The localized values are applied when the script runs in the browser.</span></span> 


## <a name="example-build-a-localized-office-add-in"></a><span data-ttu-id="c730d-189">Exemple : créer un complément Office localisé</span><span class="sxs-lookup"><span data-stu-id="c730d-189">Example: Build a localized Office Add-in</span></span>

<span data-ttu-id="c730d-190">Cette section inclut des exemples expliquant comment localiser la description, le nom d’affichage et l’interface utilisateur d’une Complément Office.</span><span class="sxs-lookup"><span data-stu-id="c730d-190">This section provides examples that show you how to localize an Office Add-in description, display name, and UI.</span></span>

<span data-ttu-id="c730d-191">Pour exécuter l’exemple de code fourni, configurez Microsoft Office 2013 sur votre ordinateur pour utiliser des langues supplémentaires et pouvoir tester votre complément en basculant d’une langue à l’autre pour l’affichage des menus et des commandes, l’édition et la vérification, ou les deux.</span><span class="sxs-lookup"><span data-stu-id="c730d-191">To run the sample code provided, configure Microsoft Office 2013 on your computer to use additional languages so that you can test your add-in by switching the language used for display in menus and commands, for editing and proofing, or both.</span></span>

<span data-ttu-id="c730d-192">En outre, vous devez créer un projet de complément Office Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="c730d-192">Also, you'll need to create a Visual Studio 2015 Office Add-in project.</span></span>

> <span data-ttu-id="c730d-p123">**REMARQUE** Pour télécharger Visual Studio 2015, consultez la [page dédiée aux outils de développement Office](https://www.visualstudio.com/features/office-tools-vs). Cette page contient également un lien pour télécharger les outils de développement Office.</span><span class="sxs-lookup"><span data-stu-id="c730d-p123">**NOTE** To download Visual Studio 2015, see the [Office Developer Tools page](https://www.visualstudio.com/features/office-tools-vs). This page also has a link for the Office Developer Tools.</span></span>

### <a name="configure-office-2013-to-use-additional-languages-for-display-or-editing"></a><span data-ttu-id="c730d-195">Configurer Office 2013 pour utiliser des langues supplémentaires pour l’affichage ou l’édition</span><span class="sxs-lookup"><span data-stu-id="c730d-195">Configure Office 2013 to use additional languages for display or editing</span></span>

<span data-ttu-id="c730d-p124">Vous pouvez utiliser un module linguistique Office 2013 pour installer des langues supplémentaires. Pour plus d’informations sur les modules linguistiques et comment les obtenir, voir [Options de langue Office 2013](http://office.microsoft.com/en-us/language-packs/).</span><span class="sxs-lookup"><span data-stu-id="c730d-p124">You can use an Office 2013 Language pack to install an additional language. For more information about Language Packs and where to get them, see [Office 2013 Language Options](http://office.microsoft.com/en-us/language-packs/).</span></span>

> <span data-ttu-id="c730d-p125">**REMARQUE** Si vous êtes abonné à MSDN, les modules linguistiques Office 2013 peuvent être disponibles dans le cadre de votre abonnement. Pour savoir si votre abonnement propose le téléchargement des modules linguistiques Office 2013, accédez à [Accueil Abonnements MSDN](https://msdn.microsoft.com/subscriptions/manage/), tapez « Modules linguistiques Office 2013 » dans **Téléchargements logiciels**, choisissez **Rechercher**, puis sélectionnez **Produits disponibles avec mon abonnement**. Sous **Langue**, cochez la case correspondant au module linguistique que vous voulez télécharger, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c730d-p125">**NOTE** If you are an MSDN Subscriber, you might already have the Office 2013 Language Packs available to you. To determine whether your subscription offers Office 2013 Language Packs for download, go to [MSDN Subscriptions Home](https://msdn.microsoft.com/subscriptions/manage/), enter Office 2013 Language Pack in **Software downloads**, choose **Search**, and then select **Products available with my subscription**. Under **Language**, select the check box for the Language Pack you want to download, and then choose  **Go**.</span></span> 

<span data-ttu-id="c730d-p126">Une fois le module linguistique installé, vous pouvez configurer Office 2013 pour utiliser la langue installée pour l’affichage de l’interface utilisateur, pour l’édition du contenu du document, ou les deux. Dans cet exemple, le module linguistique espagnol a été installé sur Office 2013.</span><span class="sxs-lookup"><span data-stu-id="c730d-p126">After you install the Language Pack, you can configure Office 2013 to use the installed language for display in the UI, for editing document content, or both. The example in this article uses an installation of Office 2013 that has the Spanish Language Pack applied.</span></span>

### <a name="create-an-office-add-in-project"></a><span data-ttu-id="c730d-203">Créer un projet de complément Office</span><span class="sxs-lookup"><span data-stu-id="c730d-203">Create an Office Add-in project</span></span>

1. <span data-ttu-id="c730d-204">Dans Visual Studio, choisissez **Fichier** > **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="c730d-204">In Visual Studio, choose **File** > **New Project**.</span></span>
    
2. <span data-ttu-id="c730d-205">Dans la boîte de dialogue **Nouveau projet**, sous **Modèles**, développez **Visual Basic** ou **Visual C#**, développez **Office/SharePoint**, puis sélectionnez **Compléments Office**.</span><span class="sxs-lookup"><span data-stu-id="c730d-205">In the **New Project** dialog box, under **Templates**, expand **Visual Basic** or **Visual C#**, expand **Office/SharePoint**, and then choose  **Office Add-ins**.</span></span>
    
3. <span data-ttu-id="c730d-p127">Choisissez **Complément Office** et donnez un nom à votre complément, par exemple WorldReadyApp. Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c730d-p127">Choose **Office Add-in**, and then name your add-in, for example WorldReadyAddIn. Choose  **OK**.</span></span>
    
4. <span data-ttu-id="c730d-p128">Dans la boîte de dialogue **Créer un complément Office**, sélectionnez **Volet Office** et cliquez sur **Suivant**. Sur la page suivante, désactivez les cases à cocher pour toutes les applications hôtes à l’exception de Word. Cliquez sur **Terminer** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="c730d-p128">In the **Create Office Add-in** dialog box, select **Task pane** and choose **Next**. On the next page, clear the check boxes for all host applications except Word. Choose **Finish** to create the project.</span></span>
    

### <a name="localize-the-text-used-in-your-add-in"></a><span data-ttu-id="c730d-211">Localiser le texte utilisé dans votre complément</span><span class="sxs-lookup"><span data-stu-id="c730d-211">Localize the text used in your add-in</span></span>

<span data-ttu-id="c730d-212">Le texte que vous souhaitez localiser dans une autre langue apparaît à deux emplacements :</span><span class="sxs-lookup"><span data-stu-id="c730d-212">The text that you want to localize for another language appears in two areas:</span></span>

-  <span data-ttu-id="c730d-p129">**Nom d’affichage et description du complément**. Ce contenu est contrôlé par les entrées du fichier manifeste de l’application.</span><span class="sxs-lookup"><span data-stu-id="c730d-p129">**Add-in display name and description**. This is controlled by entries in the add-in manifest file.</span></span>
    
-  <span data-ttu-id="c730d-p130">**Interface utilisateur du complément**. Vous pouvez localiser les chaînes qui s’affichent dans l’interface utilisateur de votre complément à l’aide du code JavaScript, par exemple en utilisant un fichier de ressources séparé qui contient les chaînes localisées.</span><span class="sxs-lookup"><span data-stu-id="c730d-p130">**Add-in UI**. You can localize the strings that appear in your add-in UI by using JavaScript codeâ€”for example, by using a separate resource file that contains the localized strings.</span></span>
    
<span data-ttu-id="c730d-217">Pour localiser le nom d’affichage et la description du complément</span><span class="sxs-lookup"><span data-stu-id="c730d-217">To localize the add-in display name and description:</span></span>

1. <span data-ttu-id="c730d-218">Dans l’ **Explorateur de solutions**, développez **WorldReadyApp**, **WorldReadyAppManifest**, puis choisissez **WorldReadyApp.xml**.</span><span class="sxs-lookup"><span data-stu-id="c730d-218">In **Solution Explorer**, expand **WorldReadyAddIn**, **WorldReadyAddInManifest**, and then choose  **WorldReadyAddIn.xml**.</span></span>
    
2. <span data-ttu-id="c730d-219">Dans WorldReadyAppManifest.xml, remplacez les éléments [DisplayName] et [Description] par le bloc de code suivant :</span><span class="sxs-lookup"><span data-stu-id="c730d-219">In WorldReadyAddInManifest.xml, replace the [DisplayName] and [Description] elements with the following block of code:</span></span>
    
    > <span data-ttu-id="c730d-220">**REMARQUE** Vous pouvez remplacer les chaînes localisées en espagnol utilisées dans cet exemple pour les éléments [DisplayName] et [Description] par les chaînes localisées dans une autre langue.</span><span class="sxs-lookup"><span data-stu-id="c730d-220">**NOTE** You can replace the Spanish language localized strings used in this example for the [DisplayName] and [Description] elements with the localized strings for any other language.</span></span>

    ```xml
    <DisplayName DefaultValue="World Ready add-in">
      <Override Locale="es-es" Value="Aplicación de uso internacional"/>
    </DisplayName>
    <Description DefaultValue="An add-in for testing localization">
      <Override Locale="es-es" Value="Una aplicación para la prueba de la localización"/>
    </Description>
    ```

3. <span data-ttu-id="c730d-221">Lorsque vous modifiez la langue d’affichage dans Office 2013, par exemple de l’anglais vers l’espagnol, puis que vous exécutez le complément, le nom d’affichage et la description du complément sont affichés avec le texte localisé.</span><span class="sxs-lookup"><span data-stu-id="c730d-221">When you change the display language for Office 2013 from English to Spanish, for example, and then run the add-in, the add-in display name and description are shown with localized text.</span></span> 
    
<span data-ttu-id="c730d-222">Pour mettre en page l’interface utilisateur du complément :</span><span class="sxs-lookup"><span data-stu-id="c730d-222">To lay out the add-in UI:</span></span>

1. <span data-ttu-id="c730d-223">Dans Visual Studio, dans l’**Explorateur de solutions**, choisissez  **Home.html**.</span><span class="sxs-lookup"><span data-stu-id="c730d-223">In Visual Studio, in **Solution Explorer**, choose **Home.html**.</span></span>
    
2. <span data-ttu-id="c730d-224">Remplacez le code HTML dans Home.html par le code HTML suivant.</span><span class="sxs-lookup"><span data-stu-id="c730d-224">Replace the HTML in Home.html with the following HTML.</span></span>
    
    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=Edge" />
        <title></title>
        <script src="../../Scripts/jquery-1.8.2.js" type="text/javascript"></script>
    
        <link href="../../Content/Office.css" rel="stylesheet" type="text/css" />
        <script src="https://appsforoffice.microsoft.com/lib/1/hosted/office.js" type="text/javascript"></script>
    
        <!-- To enable offline debugging using a local reference to Office.js, use:                        -->
        <!-- <script src="../../Scripts/Office/MicrosoftAjax.js" type="text/javascript"></script>          -->
        <!--    <script src="../../Scripts/Office/1.0/office.js" type="text/javascript"></script>          -->
    
        <link href="../App.css" rel="stylesheet" type="text/css" />
        <script src="../App.js" type="text/javascript"></script>
    
        <link href="Home.css" rel="stylesheet" type="text/css" />
        <script src="Home.js" type="text/javascript"></script> <body>
        <!-- Page content -->
        <div id="content-header">
            <div class="padding">
                <h1 id="greeting"></h1>
            </div>
        </div>
        <div id="content-main">
            <div class="padding">
                <div>
                    <p id="about"></p>
                </div>            
            </div>
        </div>
    </head>
    </html>
    ```

3. <span data-ttu-id="c730d-225">Dans Visual Studio, choisissez  **Fichier**,  **Enregistrer App\Home\Home.html**.</span><span class="sxs-lookup"><span data-stu-id="c730d-225">In Visual Studio, choose  **File**,  **Save AddIn\Home\Home.html**.</span></span>
    
<span data-ttu-id="c730d-226">La figure suivante montre l’élément titre (h1) et l’élément paragraphe (p) qui afficheront le texte localisé lors de l’exécution de l’exemple de complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-226">The following figure shows the heading (h1) element and the paragraph (p) element that will display localized text when your sample add-in runs.</span></span>

<span data-ttu-id="c730d-227">*Figure 1. Interface utilisateur du complément*</span><span class="sxs-lookup"><span data-stu-id="c730d-227">*Figure 1. The add-in UI*</span></span>

![Interface utilisateur de l’application avec des sections en surbrillance](../images/office15-app-how-to-localize-fig03.png)

### <a name="add-the-resource-file-that-contains-the-localized-strings"></a><span data-ttu-id="c730d-229">Ajouter le fichier de ressources qui contient les chaînes localisées</span><span class="sxs-lookup"><span data-stu-id="c730d-229">Add the resource file that contains the localized strings</span></span>

<span data-ttu-id="c730d-p131">Le fichier de ressources JavaScript contient les chaînes utilisées pour l’interface utilisateur du complément. L’interface utilisateur de l’exemple de complément comprend un élément h1 qui affiche un message de bienvenue et un élément p qui présente le complément à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c730d-p131">The JavaScript resource file contains the strings used for the add-in UI. The sample add-in UI has an h1 element that displays a greeting, and a p element that introduces the add-in to the user.</span></span> 

<span data-ttu-id="c730d-p132">Pour activer les chaînes localisées pour le titre et le paragraphe, placez les chaînes dans un fichier de ressources distinct. Le fichier de ressources crée un objet JavaScript qui contient un objet JavaScript Object Notation (JSON) individuel pour chaque ensemble de chaînes localisées. Le fichier de ressources fournit une méthode pour obtenir l’objet JSON approprié pour des paramètres régionaux donnés.</span><span class="sxs-lookup"><span data-stu-id="c730d-p132">To enable localized strings for the heading and paragraph, you place the strings in a separate resource file. The resource file creates a JavaScript object that contains a separate JavaScript Object Notation (JSON) object for each set of localized strings. The resource file also provides a method for getting back the appropriate JSON object for a given locale.</span></span> 

<span data-ttu-id="c730d-235">Pour ajouter le fichier de ressources au projet de complément :</span><span class="sxs-lookup"><span data-stu-id="c730d-235">To add the resource file to the add-in project:</span></span>

1. <span data-ttu-id="c730d-236">Dans l’**Explorateur de solutions** de Visual Studio, sélectionnez le dossier **Complément** dans le projet web pour l’exemple de complément et choisissez **Ajouter** > **Fichier JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="c730d-236">In **Solution Explorer** in Visual Studio, choose the **Add-in** folder in the web project for the sample add-in, and choose **Add** > **JavaScript file**.</span></span>
    
2. <span data-ttu-id="c730d-237">Dans la boîte de dialogue **Spécifier le nom de l’élément**, saisissez UIStrings.js.</span><span class="sxs-lookup"><span data-stu-id="c730d-237">In the **Specify Name for Item** dialog box, enterUIStrings.js.</span></span>
    
3. <span data-ttu-id="c730d-238">Ajoutez le code suivant au fichier UIStrings.js.</span><span class="sxs-lookup"><span data-stu-id="c730d-238">Add the following code to the UIStrings.js file.</span></span>

    ```js
    /* Store the locale-specific strings */
    
    var UIStrings = (function ()
    {
        "use strict";
    
        var UIStrings = {};
    
        // JSON object for English strings
        UIStrings.EN =
        {        
            "Greeting": "Welcome",
            "Introduction": "This is my localized add-in."        
        };
    
        // JSON object for Spanish strings
        UIStrings.ES =
        {        
            "Greeting": "Bienvenido",
            "Introduction": "Esta es mi aplicación localizada."
        };
    
        UIStrings.getLocaleStrings = function (locale)
        {
            var text;
            
            // Get the resource strings that match the language.
            switch (locale)
            {
                case 'en-US':
                    text = UIStrings.EN;
                    break;
                case 'es-ES':
                    text = UIStrings.ES;
                    break;
                default:
                    text = UIStrings.EN;
                    break;
            }
    
            return text;
        };
    
        return UIStrings;
    })();
    ```

<span data-ttu-id="c730d-239">Le fichier de ressources UIStrings.js crée un objet **UIStrings** qui contient les chaînes localisées pour l’interface utilisateur de votre complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-239">The UIStrings.js resource file creates an object, **UIStrings**, which contains the localized strings for your add-in UI.</span></span> 

### <a name="localize-the-text-used-for-the-add-in-ui"></a><span data-ttu-id="c730d-240">Localiser le texte utilisé pour l’interface utilisateur du complément</span><span class="sxs-lookup"><span data-stu-id="c730d-240">Localize the text used for the add-in UI</span></span>

<span data-ttu-id="c730d-p133">Pour utiliser le fichier de ressources de votre complément, vous devez ajouter une balise de script pour ce fichier dans Home.html. Quand Home.html est chargé, UIStrings.js s’exécute et l’objet  **UIStrings** que vous utilisez pour obtenir les chaînes est disponible pour votre code. Ajoutez le code HTML suivant dans la balise head pour Home.html pour que **UIStrings** soit disponible pour votre code.</span><span class="sxs-lookup"><span data-stu-id="c730d-p133">To use the resource file in your add-in, you'll need to add a script tag for it on Home.html. When Home.html is loaded, UIStrings.js executes and the **UIStrings** object that you use to get the strings is available to your code. Add the following HTML in the head tag for Home.html to make **UIStrings** available to your code.</span></span>

```html
<!-- Resource file for localized strings:                                                          -->
<script src="../UIStrings.js" type="text/javascript"></script>
```

<span data-ttu-id="c730d-244">Vous pouvez désormais utiliser l’objet **UIStrings** pour définir les chaînes pour l’interface utilisateur de votre complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-244">Now you can use the **UIStrings** object to set the strings for the UI of your add-in.</span></span>

<span data-ttu-id="c730d-p134">Si vous voulez changer la localisation pour votre complément en fonction de la langue utilisée pour afficher les menus et les commandes dans l’application hôte, utilisez la propriété **Office.context.displayLanguage** pour obtenir les paramètres régionaux pour cette langue. Par exemple, si la langue de l’application hôte utilise l’espagnol pour afficher les menus et les commandes, la propriété **Office.context.displayLanguage** retournera le code de langue es-ES.</span><span class="sxs-lookup"><span data-stu-id="c730d-p134">If you want to change the localization for your add-in based on what language is used for display in menus and commands in the host application, you use the **Office.context.displayLanguage** property to get the locale for that language. For example, if the host application language uses Spanish for display in menus and commands, the **Office.context.displayLanguage** property will return the language code es-ES.</span></span>

<span data-ttu-id="c730d-p135">Si vous voulez changer la localisation pour votre complément en fonction de la langue utilisée pour l’édition du contenu de document, utilisez la propriété  **Office.context.contentLanguage** pour obtenir les paramètres régionaux pour cette langue. Par exemple, si la langue de l’application hôte utilise l’espagnol pour l’édition de contenu de document, la propriété **Office.context.contentLanguage** retournera le code de langue es-ES.</span><span class="sxs-lookup"><span data-stu-id="c730d-p135">If you want to change the localization for your add-in based on what language is being used for editing document content, you use the  **Office.context.contentLanguage** property to get the locale for that language. For example, if the host application language uses Spanish for editing document content, the **Office.context.contentLanguage** property will return the language code es-ES.</span></span>

<span data-ttu-id="c730d-249">Une fois que vous connaissez la langue utilisée par l’application hôte, vous pouvez utiliser **UIStrings** pour obtenir les chaînes localisées qui correspondent à la langue de l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="c730d-249">After you know the language the host application is using, you can use **UIStrings** to get the set of localized strings that matches the host application language.</span></span>

<span data-ttu-id="c730d-p136">Remplacez le code du fichier Home.js par le code suivant. Le code montre comment changer les chaînes utilisées dans les éléments d’interface utilisateur de Home.html en fonction de la langue d’affichage de l’application hôte ou de la langue d’édition de l’application hôte.</span><span class="sxs-lookup"><span data-stu-id="c730d-p136">Replace the code in the Home.js file with the following code. The code shows how you can change the strings used in the UI elements on Home.html based on either the display language of the host application or the editing language of the host application.</span></span>

> <span data-ttu-id="c730d-252">**REMARQUE** Pour activer ou désactiver la localisation du complément en fonction de la langue utilisée pour la modification, supprimez le commentaire de la ligne de code `var myLanguage = Office.context.contentLanguage;` et ajoutez un commentaire à la ligne de code `var myLanguage = Office.context.displayLanguage;`</span><span class="sxs-lookup"><span data-stu-id="c730d-252">**NOTE** To switch between changing the localization of the add-in based on the language used for editing, uncomment the line of code  `var myLanguage = Office.context.contentLanguage;` and comment out the line of code `var myLanguage = Office.context.displayLanguage;`</span></span>

```js
/// <reference path="../App.js" />
/// <reference path="../UIStrings.js" />


(function () {
    "use strict";

    // The initialize function must be run each time a new page is loaded.
    Office.initialize = function (reason)
    {
       
        $(document).ready(function () {
            app.initialize();

            // Get the language setting for editing document content.
            // To test this, uncomment the following line and then comment out the
            // line that uses Office.context.displayLanguage.
            // var myLanguage = Office.context.contentLanguage;

            // Get the language setting for UI display in the host application.
            var myLanguage = Office.context.displayLanguage;            
            var UIText;

            // Get the resource strings that match the language.
            // Use the UIStrings object from the UIStrings.js file
            // to get the JSON object with the correct localized strings.
            UIText = UIStrings.getLocaleStrings(myLanguage);            

            // Set localized text for UI elements.
            $("#greeting").text(UIText.Greeting);
            $("#about").text(UIText.Instruction);
        });
    };    
})();
```

### <a name="test-your-localized-add-in"></a><span data-ttu-id="c730d-253">Tester votre complément localisé</span><span class="sxs-lookup"><span data-stu-id="c730d-253">Test your localized add-in</span></span>

<span data-ttu-id="c730d-254">Pour tester votre complément localisé, changez la langue utilisée pour l’affichage et l’édition dans l’application hôte, puis exécutez votre complément.</span><span class="sxs-lookup"><span data-stu-id="c730d-254">To test your localized add-in, change the language used for display or editing in the host application and then run your add-in.</span></span> 

<span data-ttu-id="c730d-255">Pour changer la langue utilisée pour l’affichage ou l’édition dans votre complément :</span><span class="sxs-lookup"><span data-stu-id="c730d-255">To change the language used for display or editing in your add-in:</span></span>

1. <span data-ttu-id="c730d-p137">Dans Word 2013, sélectionnez **Fichier** > **Options** > **Langue**. La figure suivante montre la boîte de dialogue **Options Word** ouverte sur l’onglet Langue.</span><span class="sxs-lookup"><span data-stu-id="c730d-p137">In Word 2013, choose **File** > **Options** > **Language**. The following figure shows the **Word Options** dialog box opened to the Language tab.</span></span>
    
    <span data-ttu-id="c730d-258">*Figure 2. Options de langue dans la boîte de dialogue Options Word 2013*</span><span class="sxs-lookup"><span data-stu-id="c730d-258">*Figure 2. Language options in the Word 2013 Options dialog box*</span></span>

    ![Boîte de dialogue Options Word 2013](../images/office15-app-how-to-localize-fig04.png)

2. <span data-ttu-id="c730d-p138">Sous **Choisir les langues de l’interface utilisateur et de l’Aide**, sélectionnez la langue souhaitée pour l’affichage, par exemple l’espagnol, puis cliquez sur la flèche vers le haut pour déplacer l’espagnol tout en haut de la liste. Pour changer la langue utilisée pour l’édition, sous **Choisir les langues d’édition**, choisissez la langue à utiliser pour l’édition, par exemple l’espagnol, puis choisissez **Définir par défaut**.</span><span class="sxs-lookup"><span data-stu-id="c730d-p138">Under **Choose Display and Help Languages**, select the language that you want for display, for example Spanish, and then choose the up arrow to move the Spanish language to the first position in the list. Alternatively, to change the language used for editing, under  **Choose editing languages**, choose the language you want to use for editing, for example, Spanish, and then choose **Set as Default**.</span></span>
    
3. <span data-ttu-id="c730d-262">Sélectionnez **OK** pour confirmer votre choix, puis fermez Word.</span><span class="sxs-lookup"><span data-stu-id="c730d-262">Choose **OK** to confirm your selection, and then close Word.</span></span>
    
<span data-ttu-id="c730d-p139">Exécutez l’exemple de complément. Le complément de volet de tâches est chargé dans Word 2013 et les chaînes de l’interface utilisateur du complément changent pour correspondre à la langue utilisée par l’application hôte, comme indiqué dans la figure suivante.</span><span class="sxs-lookup"><span data-stu-id="c730d-p139">Run the sample add-in. The taskpane add-in loads in Word 2013, and the strings in the add-in UI change to match the language used by the host application, as shown in the following figure.</span></span>


<span data-ttu-id="c730d-265">*Figure 3. Interface utilisateur du complément avec le texte localisé*</span><span class="sxs-lookup"><span data-stu-id="c730d-265">*Figure 3. Add-in UI with localized text*</span></span>

![Application avec le texte de l’interface utilisateur localisé](../images/office15-app-how-to-localize-fig05.png)

## <a name="see-also"></a><span data-ttu-id="c730d-267">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c730d-267">See also</span></span>

- [<span data-ttu-id="c730d-268">Instructions de conception pour les compléments Office</span><span class="sxs-lookup"><span data-stu-id="c730d-268">Design guidelines for Office Add-ins</span></span>](../design/add-in-design.md)    
- [<span data-ttu-id="c730d-269">Identificateurs de langue et valeurs d’ID de l’élément OptionState dans Office 2013</span><span class="sxs-lookup"><span data-stu-id="c730d-269">Language identifiers and OptionState Id values in Office 2013</span></span>](http://technet.microsoft.com/en-us/library/cc179219%28Office.15%29.aspx)

[DefaultLocale]:        https://dev.office.com/reference/add-ins/manifest/defaultlocale
[Description]:          https://dev.office.com/reference/add-ins/manifest/description
[DisplayName]:          https://dev.office.com/reference/add-ins/manifest/displayname
[IconUrl]:              https://dev.office.com/reference/add-ins/manifest/iconurl
[HighResolutionIconUrl]:https://dev.office.com/reference/add-ins/manifest/highresolutioniconurl
[Ressources]:            https://dev.office.com/reference/add-ins/manifest/resources
[Resources]:            https://dev.office.com/reference/add-ins/manifest/resources
[SourceLocation]:       https://dev.office.com/reference/add-ins/manifest/sourcelocation
[Override]:             https://dev.office.com/reference/add-ins/manifest/override
[DesktopSettings]:      https://dev.office.com/reference/add-ins/manifest/desktopsettings
[TabletSettings]:       https://dev.office.com/reference/add-ins/manifest/tabletsettings
[PhoneSettings]:        https://dev.office.com/reference/add-ins/manifest/phonesettings
[displayLanguage]:  https://dev.office.com/reference/add-ins/shared/office.context.displaylanguage 
[contentLanguage]:  https://dev.office.com/reference/add-ins/shared/office.context.contentlanguage 
[RFC 3066]: https://www.rfc-editor.org/info/rfc3066