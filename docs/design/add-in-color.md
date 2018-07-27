# <a name="color"></a><span data-ttu-id="87c8c-101">Couleur</span><span class="sxs-lookup"><span data-stu-id="87c8c-101">Color</span></span>
<span data-ttu-id="87c8c-102">La couleur est souvent utilisée pour mettre en évidence l'identité graphique et renforcer la hiérarchie de l'objet visuel.</span><span class="sxs-lookup"><span data-stu-id="87c8c-102">Color is often used to emphasize brand and reinforce visual hierarchy.</span></span> <span data-ttu-id="87c8c-103">Elle aide à identifier une interface et à guider les clients à travers une expérience.</span><span class="sxs-lookup"><span data-stu-id="87c8c-103">It helps identify an interface as well as guide customers through an experience.</span></span> <span data-ttu-id="87c8c-104">Dans Office, la couleur est utilisée pour les mêmes objectifs mais elle est appliquée de manière ciblée et minimale.</span><span class="sxs-lookup"><span data-stu-id="87c8c-104">Inside Office, color is used for the same goals but it is applied purposefully and minimally.</span></span> <span data-ttu-id="87c8c-105">À aucun moment, cela ne surcharge le contenu du client.</span><span class="sxs-lookup"><span data-stu-id="87c8c-105">At no point does it overwhelm customer content.</span></span> <span data-ttu-id="87c8c-106">Même lorsque chaque application Office est marquée avec sa propre couleur dominante, elle est utilisée avec parcimonie.</span><span class="sxs-lookup"><span data-stu-id="87c8c-106">Even when each Office app is branded with its own dominant color, it is used sparingly.</span></span>

<span data-ttu-id="87c8c-p102">Office UI Fabric comprend un jeu de couleurs de thème par défaut. Lorsque Fabric est appliqué à un complément Office comme composants ou dans des dispositions, les mêmes objectifs s’appliquent. La couleur doit communiquer la hiérarchie, guidant ainsi les clients vers l’action sans interférer avec le contenu. Les couleurs de thème Fabric peuvent introduire une nouvelle couleur de l’accentuation dans l’interface globale. Cette nouvelle accentuation peut entrer en conflit avec la personnalisation de l’application Office et interférer avec la hiérarchie. En d’autres termes, Fabric peut introduire une nouvelle couleur de l’accentuation dans l’interface globale lorsqu’elle est utilisée à l’intérieur d’un complément. Cette nouvelle couleur de l’accentuation peut créer une confusion et interférer avec la hiérarchie globale. Envisagez des façons d’éviter les conflits et les interférences. Utilisez des accentuations neutres ou remplacez les couleurs de thème Fabric en fonction de la personnalisation de l’application Office ou de vos propres couleurs de la marque.</span><span class="sxs-lookup"><span data-stu-id="87c8c-p102">Office UI Fabric includes a set of default theme colors. When Fabric is applied to an Office Add-in as components or in layouts, the same goals apply. Color should communicate hierarchy, purposefully guiding customers to action without interfering with content. Fabric theme colors can introduce a new accent color to the overall interface. This new accent can conflict with Office app branding and interfere with hierarchy. In other words, Fabric can introduce a new accent color to the overall interface when used inside an add-in. This new accent color can distract and interfere with the overall hierarchy. Consider ways to avoid conflicts and interference. Use neutral accents or overwrite Fabric theme colors to match Office app branding or your own brand colors.</span></span>

<span data-ttu-id="87c8c-p103">Les applications Office permettent aux clients de personnaliser leurs interfaces en appliquant un thème de l’interface utilisateur d’Office. Les clients peuvent choisir entre quatre thèmes de l’interface utilisateur pour modifier le style des arrière-plans et des boutons dans Word, PowerPoint, Excel et les autres applications de la suite Office. Pour que vos compléments paraissent comme des composants naturels d’Office et répondent à la personnalisation, utilisez nos API de thèmes. Par exemple, les couleurs d’arrière-plan du volet des tâches deviennent gris foncé dans certains thèmes. Nos API de thèmes vous permettent de faire de même et d’ajuster le texte de premier plan pour garantir l’[accessibilité](../design/accessibility-guidelines.md).</span><span class="sxs-lookup"><span data-stu-id="87c8c-p103">Office applications allow customers to personalize their interfaces by applying an Office UI theme. Customers can choose between four UI themes to vary styling of backgrounds and buttons in Word, PowerPoint, Excel and other apps in the Office suite. To make your add-ins feel like a natural part of Office and respond to personalization, use our Themeing APIs. For example, task pane background colors switch to a dark gray in some themes. Our theming APIs allow you to follow suit and adjust foreground text to ensure [accessibility](../design/accessibility-guidelines.md).</span></span>

> [!NOTE]
> - <span data-ttu-id="87c8c-p104">Pour les compléments de volet de tâches et de messagerie, utilisez la propriété [Context.officeTheme](https://dev.office.com/reference/add-ins/shared/office.context.officetheme) pour utiliser les thèmes correspondant à ceux des applications Office. Actuellement, cette API n’est disponible que dans Office 2016.</span><span class="sxs-lookup"><span data-stu-id="87c8c-p104">For mail and task pane add-ins, use the [Context.officeTheme](https://dev.office.com/reference/add-ins/shared/office.context.officetheme) property to match the theme of the Office applications. This API is currently only available in Office 2016.</span></span>
> - <span data-ttu-id="87c8c-123">Pour plus d’informations sur les compléments de contenu pour PowerPoint, reportez-vous à l’article expliquant comment [utiliser des thèmes Office dans vos compléments PowerPoint](../powerpoint/use-document-themes-in-your-powerpoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="87c8c-123">For PowerPoint content add-ins, see [Use Office themes in your PowerPoint add-ins](../powerpoint/use-document-themes-in-your-powerpoint-add-ins.md).</span></span>

<span data-ttu-id="87c8c-124">Appliquez les recommandations générales suivantes pour la couleur :</span><span class="sxs-lookup"><span data-stu-id="87c8c-124">Apply the following general guidelines for color:</span></span>

* <span data-ttu-id="87c8c-125">Utilisez la couleur avec parcimonie pour communiquer la hiérarchie et renforcer la marque.</span><span class="sxs-lookup"><span data-stu-id="87c8c-125">Use color sparingly to communicate hierarchy and reinforce brand.</span></span>
* <span data-ttu-id="87c8c-p105">L’utilisation excessive d’une couleur d’accentuation unique appliquée aux éléments interactifs et non interactifs peut être source de confusion. Par exemple, évitez d’utiliser la même couleur pour les éléments sélectionnés et non sélectionnés dans un menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="87c8c-p105">Overuse of a single accent color applied to both interactive and non-interactive elements can lead to confusion. For example, avoid using the same color for selected and unselected items in a navigation menu.</span></span>
* <span data-ttu-id="87c8c-128">Évitez les conflits inutiles avec des couleurs non Office.</span><span class="sxs-lookup"><span data-stu-id="87c8c-128">Avoid unnecessary conflicts with Office branded app colors.</span></span>
* <span data-ttu-id="87c8c-129">Utilisez vos propres couleurs de la marque pour créer une association avec votre service ou votre société.</span><span class="sxs-lookup"><span data-stu-id="87c8c-129">Use your own brand colors to build association with your service or company.</span></span>
* <span data-ttu-id="87c8c-p106">Assurez-vous que tout le texte est accessible. N’oubliez pas qu’il existe un ratio de contraste 4.5:1 entre le texte de premier plan et l’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="87c8c-p106">Ensure that all text is accessible. Be sure that there is a 4.5:1 constrast ratio between foreground text and background.</span></span>
* <span data-ttu-id="87c8c-p107">Pensez aux personnes atteintes de daltonisme : n’utilisez pas seulement des couleurs pour indiquer l’interactivité et la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="87c8c-p107">Be aware of color blindness. Use more than just color to indicate interactivity and hierarchy.</span></span>
* <span data-ttu-id="87c8c-134">Consultez les [Instructions relatives aux icônes](../design/add-in-icons.md) pour en savoir plus sur la conception des icônes de commande de complément avec la palette de couleurs d’icônes Office.</span><span class="sxs-lookup"><span data-stu-id="87c8c-134">Refer to [icon guidelines](../design/add-in-icons.md) to learn more about designing add-in command icons with the Office icon color pallet.</span></span>