# <a name="build-your-first-onenote-add-in"></a><span data-ttu-id="7f43c-101">Créer votre premier complément OneNote</span><span class="sxs-lookup"><span data-stu-id="7f43c-101">Build your first OneNote add-in</span></span>

<span data-ttu-id="7f43c-102">Cet article décrit le processus de création d’un complément OneNote à l’aide de jQuery et de l’API JavaScript pour Office.</span><span class="sxs-lookup"><span data-stu-id="7f43c-102">In this article, you'll walk through the process of building a OneNote add-in by using jQuery and the Office JavaScript API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f43c-103">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="7f43c-103">Prerequisites</span></span>

- [<span data-ttu-id="7f43c-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="7f43c-104">Node.js</span></span>](https://nodejs.org)

- <span data-ttu-id="7f43c-105">Installez la dernière version de [Yeoman](https://github.com/yeoman/yo) et le [générateur Yeoman pour les compléments Office](https://github.com/OfficeDev/generator-office) globalement.</span><span class="sxs-lookup"><span data-stu-id="7f43c-105">Install the latest version of [Yeoman](https://github.com/yeoman/yo) and the [Yeoman generator for Office Add-ins](https://github.com/OfficeDev/generator-office) globally.</span></span>

    ```bash
    npm install -g yo generator-office
    ```

## <a name="create-the-add-in-project"></a><span data-ttu-id="7f43c-106">Création du projet de complément</span><span class="sxs-lookup"><span data-stu-id="7f43c-106">Create the add-in project</span></span>

1. <span data-ttu-id="7f43c-107">Créez un dossier sur votre lecteur local et nommez-le `my-onenote-addin`.</span><span class="sxs-lookup"><span data-stu-id="7f43c-107">Create a folder on your local drive and name it `my-onenote-addin`.</span></span> <span data-ttu-id="7f43c-108">Il s’agit de l’emplacement dans lequel vous allez créer les fichiers de votre complément.</span><span class="sxs-lookup"><span data-stu-id="7f43c-108">This is where you'll create the files for your add-in.</span></span>

2. <span data-ttu-id="7f43c-109">Accédez à votre nouveau dossier.</span><span class="sxs-lookup"><span data-stu-id="7f43c-109">Navigate to your new folder.</span></span>

    ```bash
    cd my-onenote-addin
    ```

3. <span data-ttu-id="7f43c-110">Utilisez le générateur Yeoman afin de créer un projet de complément OneNote.</span><span class="sxs-lookup"><span data-stu-id="7f43c-110">Use the Yeoman generator to create a OneNote add-in project.</span></span> <span data-ttu-id="7f43c-111">Exécutez la commande suivante, puis répondez aux invites comme suit :</span><span class="sxs-lookup"><span data-stu-id="7f43c-111">Run the following command and then answer the prompts as follows:</span></span>

    ```bash
    yo office
    ```

    - <span data-ttu-id="7f43c-112">**Voulez-vous créer un sous-dossier de votre projet ? :** `No`</span><span class="sxs-lookup"><span data-stu-id="7f43c-112">**Would you like to create a new subfolder for your project?:** `No`</span></span>
    - <span data-ttu-id="7f43c-113">**Comment souhaitez-vous nommer votre complément ? :** `OneNote Add-in`</span><span class="sxs-lookup"><span data-stu-id="7f43c-113">**What do you want to name your add-in?:** `OneNote Add-in`</span></span>
    - <span data-ttu-id="7f43c-114">**Quelle application client Office voulez-vous prendre en charge ? :** `OneNote`</span><span class="sxs-lookup"><span data-stu-id="7f43c-114">**Which Office client application would you like to support?:** `OneNote`</span></span>
    - <span data-ttu-id="7f43c-115">**Voulez-vous créer un complément ? :** `Yes`</span><span class="sxs-lookup"><span data-stu-id="7f43c-115">**Would you like to create a new add-in?:** `Yes`</span></span>
    - <span data-ttu-id="7f43c-116">**Souhaitez-vous utiliser TypeScript ? :** `No`</span><span class="sxs-lookup"><span data-stu-id="7f43c-116">**Would you like to use TypeScript?:** `No`</span></span>
    - <span data-ttu-id="7f43c-117">**Choisissez une infrastructure :** `Jquery`</span><span class="sxs-lookup"><span data-stu-id="7f43c-117">**Choose a framework:** `Jquery`</span></span>

    <span data-ttu-id="7f43c-p103">Le générateur demande ensuite si vous voulez ouvrir **resource.html**. Il n’est pas nécessaire de l’ouvrir pour ce didacticiel, mais n’hésitez pas à l’ouvrir si vous êtes curieux. Cliquez sur Oui ou Non pour fermer l’assistant et laisser le générateur faire son travail.</span><span class="sxs-lookup"><span data-stu-id="7f43c-p103">The generator will then ask you if you want to open **resource.html**. It isn't necessary to open it for this tutorial, but feel free to open it if you're curious! Choose yes or no to complete the wizard and allow the generator to do its work.</span></span>

    ![Capture d’écran des invites et des réponses relatives au générateur Yeoman](../images/yo-office-onenote-jquery.png)


## <a name="update-the-code"></a><span data-ttu-id="7f43c-122">Mise à jour du code</span><span class="sxs-lookup"><span data-stu-id="7f43c-122">Update the code</span></span>

1. <span data-ttu-id="7f43c-123">Dans votre éditeur de code, ouvrez **index.html** à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="7f43c-123">In your code editor, open **index.html** in the root of the project.</span></span> <span data-ttu-id="7f43c-124">Ce fichier contient le code HTML qui s’affichera dans le volet Office du complément.</span><span class="sxs-lookup"><span data-stu-id="7f43c-124">This file contains the HTML that will be rendered in the add-in's task pane.</span></span>

2. <span data-ttu-id="7f43c-125">Remplacez l’élément `<main>` dans l’élément `<body>` par le balisage suivant et enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="7f43c-125">Replace the `<main>` element inside the `<body>` element with the following markup and save the file.</span></span> <span data-ttu-id="7f43c-126">Cette option ajoute une zone de texte et un bouton à l’aide des [composants de la structure de l’interface utilisateur d’Office](http://dev.office.com/fabric/components).</span><span class="sxs-lookup"><span data-stu-id="7f43c-126">This adds a text area and a button using [Office UI Fabric components](http://dev.office.com/fabric/components).</span></span>

    ```html
    <main class="ms-welcome__main">
        <br />
        <p class="ms-font-l">Enter content below</p>
        <div class="ms-TextField ms-TextField--placeholder">
            <textarea id="textBox" rows="5"></textarea>
        </div>
        <button id="addOutline" class="ms-welcome__action ms-Button ms-Button--hero ms-u-slideUpIn20">
            <span class="ms-Button-label">Add Outline</span>
            <span class="ms-Button-icon"><i class="ms-Icon"></i></span>
            <span class="ms-Button-description">Adds the content above to the current page.</span>
        </button>
    </main>
    ```

3. <span data-ttu-id="7f43c-127">Ouvrez le fichier **app.js** pour spécifier le script pour le complément.</span><span class="sxs-lookup"><span data-stu-id="7f43c-127">Open the file **app.js** to specify the script for the add-in.</span></span> <span data-ttu-id="7f43c-128">Remplacez tout le contenu par le code suivant, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="7f43c-128">Replace the entire contents with the following code and save the file.</span></span>

    ```js
    'use strict';

    (function () {

        Office.initialize = function (reason) {
            $(document).ready(function () {
                app.initialize();

                // Set up event handler for the UI.
                $('#addOutline').click(addOutlineToPage);
            });
        };

        // Add the contents of the text area to the page.
        function addOutlineToPage() {        
            OneNote.run(function (context) {
                var html = '<p>' + $('#textBox').val() + '</p>';

                // Get the current page.
                var page = context.application.getActivePage();

                // Queue a command to load the page with the title property.             
                page.load('title'); 

                // Add an outline with the specified HTML to the page.
                var outline = page.addOutline(40, 90, html);

                // Run the queued commands, and return a promise to indicate task completion.
                return context.sync()
                    .then(function() {
                        console.log('Added outline to page ' + page.title);
                    })
                    .catch(function(error) {
                        app.showNotification("Error: " + error); 
                        console.log("Error: " + error); 
                        if (error instanceof OfficeExtension.Error) { 
                            console.log("Debug info: " + JSON.stringify(error.debugInfo)); 
                        } 
                    }); 
            });
        }
    })();
    ```

## <a name="update-the-manifest"></a><span data-ttu-id="7f43c-129">Mise à jour du manifeste</span><span class="sxs-lookup"><span data-stu-id="7f43c-129">Update the manifest</span></span>

1. <span data-ttu-id="7f43c-130">Ouvrez le fichier nommé **one-note-add-in-manifest.xml** pour définir les paramètres et les fonctionnalités du complément.</span><span class="sxs-lookup"><span data-stu-id="7f43c-130">Open the file **one-note-add-in-manifest.xml** to define the add-in's settings and capabilities.</span></span>

2. <span data-ttu-id="7f43c-131">L’élément `ProviderName` possède une valeur d’espace réservé.</span><span class="sxs-lookup"><span data-stu-id="7f43c-131">The `ProviderName` element has a placeholder value.</span></span> <span data-ttu-id="7f43c-132">Remplacez-le par votre nom.</span><span class="sxs-lookup"><span data-stu-id="7f43c-132">Replace it with your name.</span></span>

3. <span data-ttu-id="7f43c-133">L’attribut `DefaultValue` de l’élément `Description` possède un espace réservé.</span><span class="sxs-lookup"><span data-stu-id="7f43c-133">The `DefaultValue` attribute of the `Description` element has a placeholder.</span></span> <span data-ttu-id="7f43c-134">Remplacez-le par **A task pane add-in for OneNote**.</span><span class="sxs-lookup"><span data-stu-id="7f43c-134">Replace it with **A task pane add-in for OneNote**.</span></span>

4. <span data-ttu-id="7f43c-135">Enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="7f43c-135">Save the file.</span></span>

    ```xml
    ...
    <ProviderName>John Doe</ProviderName>
    <DefaultLocale>en-US</DefaultLocale>
    <!-- The display name of your add-in. Used on the store and various places of the Office UI such as the add-ins dialog. -->
    <DisplayName DefaultValue="OneNote Add-in" />
    <Description DefaultValue="A task pane add-in for OneNote"/>
    ...
    ```

## <a name="start-the-dev-server"></a><span data-ttu-id="7f43c-136">Démarrage du serveur de développement</span><span class="sxs-lookup"><span data-stu-id="7f43c-136">Start the dev server</span></span>

[!include[Start server section](../includes/quickstart-yo-start-server.md)]

## <a name="try-it-out"></a><span data-ttu-id="7f43c-137">Essayez !</span><span class="sxs-lookup"><span data-stu-id="7f43c-137">Try it out</span></span>

1. <span data-ttu-id="7f43c-138">Dans [OneNote Online](https://www.onenote.com/notebooks), ouvrez un bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="7f43c-138">In [OneNote Online](https://www.onenote.com/notebooks), open a notebook.</span></span>

2. <span data-ttu-id="7f43c-139">Choisissez **Insertion > Compléments Office** pour ouvrir la boîte de dialogue Compléments Office.</span><span class="sxs-lookup"><span data-stu-id="7f43c-139">Choose **Insert > Office Add-ins** to open the Office Add-ins dialog.</span></span>

    - <span data-ttu-id="7f43c-140">Si vous êtes connecté avec votre compte de consommateur, sélectionnez l’onglet **MES COMPLÉMENTS**, puis choisissez **Télécharger mon complément**.</span><span class="sxs-lookup"><span data-stu-id="7f43c-140">If you're signed in with your consumer account, select the **MY ADD-INS** tab, and then choose **Upload My Add-in**.</span></span>

    - <span data-ttu-id="7f43c-141">Si vous êtes connecté avec votre compte professionnel ou scolaire, sélectionnez l’onglet **MON ORGANISATION**, puis choisissez **Télécharger mon complément**.</span><span class="sxs-lookup"><span data-stu-id="7f43c-141">If you're signed in with your work or school account, select the **MY ORGANIZATION** tab, and then select **Upload My Add-in**.</span></span> 

    <span data-ttu-id="7f43c-142">L’image suivante montre l’onglet **MES COMPLÉMENTS** pour les blocs-notes de consommateurs.</span><span class="sxs-lookup"><span data-stu-id="7f43c-142">The following image shows the **MY ADD-INS** tab for consumer notebooks.</span></span>

    <img alt="The Office Add-ins dialog showing the MY ADD-INS tab" src="../images/onenote-office-add-ins-dialog.png" width="500">

3. <span data-ttu-id="7f43c-143">Dans la boîte de dialogue Télécharger le complément, accédez à **one-note-add-in-manifest.xml** dans le dossier de projet, puis choisissez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="7f43c-143">In the Upload Add-in dialog, browse to **one-note-add-in-manifest.xml** in your project folder, and then choose **Upload**.</span></span> 

4. <span data-ttu-id="7f43c-144">Depuis l’onglet **Accueil**, cliquez le bouton **Afficher le volet Office** du ruban.</span><span class="sxs-lookup"><span data-stu-id="7f43c-144">In Word, choose the **Home** tab, and then choose the **Show Taskpane** button in the ribbon to open the add-in task pane.</span></span> <span data-ttu-id="7f43c-145">Le complément volet Office s’ouvre dans un iFrame à côté de la page OneNote.</span><span class="sxs-lookup"><span data-stu-id="7f43c-145">6- The add-in opens in an iFrame next to the OneNote page.</span></span>

5. <span data-ttu-id="7f43c-146">Entrez du texte dans la zone de texte, puis choisissez **Ajouter un plan**.</span><span class="sxs-lookup"><span data-stu-id="7f43c-146">Enter some text in the text area and then choose **Add outline**.</span></span> <span data-ttu-id="7f43c-147">Le texte que vous avez entré est ajouté à la page.</span><span class="sxs-lookup"><span data-stu-id="7f43c-147">The text you entered is added to the page.</span></span> 

    ![Complément OneNote généré à partir de cette procédure pas à pas](../images/onenote-first-add-in.png)

## <a name="troubleshooting-and-tips"></a><span data-ttu-id="7f43c-149">Conseils et résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="7f43c-149">Troubleshooting and tips</span></span>

- <span data-ttu-id="7f43c-p111">Vous pouvez déboguer le complément à l’aide des outils de développement de votre navigateur. Lorsque vous utilisez le serveur web Gulp et le débogage dans Internet Explorer ou Chrome, vous pouvez enregistrer les modifications localement et simplement actualiser l’iFrame du complément.</span><span class="sxs-lookup"><span data-stu-id="7f43c-p111">You can debug the add-in using your browser's developer tools. When you're using the Gulp web server and debugging in Internet Explorer or Chrome, you can save your changes locally and then just refresh the add-in's iFrame.</span></span>

- <span data-ttu-id="7f43c-p112">Lorsque vous examinez un objet OneNote, les propriétés qui sont actuellement disponibles affichent les valeurs réelles. Les propriétés qui doivent être chargées sont affichées comme *non définies*. Développez le nœud `_proto_` pour visualiser les propriétés qui sont définies sur l’objet, mais qui ne sont pas encore chargées.</span><span class="sxs-lookup"><span data-stu-id="7f43c-p112">When you inspect a OneNote object, the properties that are currently available for use display actual values. Properties that need to be loaded display *undefined*. Expand the `_proto_` node to see properties that are defined on the object but are not yet loaded.</span></span>

   ![Objet OneNote déchargé dans le débogueur](../images/onenote-debug.png)

- <span data-ttu-id="7f43c-p113">Vous devez activer le contenu mixte dans le navigateur si votre complément utilise des ressources HTTP. Les compléments de production doivent uniquement utiliser des ressources HTTPS sécurisées.</span><span class="sxs-lookup"><span data-stu-id="7f43c-p113">You need to enable mixed content in the browser if your add-in uses any HTTP resources. Production add-ins should use only secure HTTPS resources.</span></span>

- <span data-ttu-id="7f43c-158">Les compléments de volet Office peuvent être ouverts à partir de n’importe où, mais les compléments de contenu peuvent uniquement être insérés à l’intérieur de contenu de page normal (et non dans des titres, des images, des iFrames, etc.).</span><span class="sxs-lookup"><span data-stu-id="7f43c-158">Task pane add-ins can be opened from anywhere, but content add-ins can only be inserted inside regular page content (i.e. not in titles, images, iFrames, etc.).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7f43c-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f43c-159">Next steps</span></span>

<span data-ttu-id="7f43c-160">Félicitations, vous avez créé un complément OneNote !</span><span class="sxs-lookup"><span data-stu-id="7f43c-160">Congratulations, you've successfully created a OneNote add-in!</span></span> <span data-ttu-id="7f43c-161">Ensuite, vous allez étudier en détail les concepts fondamentaux de la création de compléments Excel.</span><span class="sxs-lookup"><span data-stu-id="7f43c-161">Next, learn more about the core concepts of building OneNote add-ins.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f43c-162">Vue d’ensemble de la programmation de l’API JavaScript de OneNote</span><span class="sxs-lookup"><span data-stu-id="7f43c-162">OneNote JavaScript API programming overview</span></span>](../onenote/onenote-add-ins-programming-overview.md)

## <a name="see-also"></a><span data-ttu-id="7f43c-163">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7f43c-163">See also</span></span>

- [<span data-ttu-id="7f43c-164">Vue d’ensemble de la programmation de l’API JavaScript de OneNote</span><span class="sxs-lookup"><span data-stu-id="7f43c-164">OneNote JavaScript API programming overview</span></span>](../onenote/onenote-add-ins-programming-overview.md)
- [<span data-ttu-id="7f43c-165">Référence de l’API JavaScript de OneNote</span><span class="sxs-lookup"><span data-stu-id="7f43c-165">OneNote JavaScript API reference</span></span>](https://dev.office.com/reference/add-ins/onenote/onenote-add-ins-javascript-reference)
- [<span data-ttu-id="7f43c-166">Exemple de grille d’évaluation</span><span class="sxs-lookup"><span data-stu-id="7f43c-166">Rubric Grader sample</span></span>](https://github.com/OfficeDev/OneNote-Add-in-Rubric-Grader)
- [<span data-ttu-id="7f43c-167">Vue d’ensemble de la plateforme des compléments Office</span><span class="sxs-lookup"><span data-stu-id="7f43c-167">Office Add-ins platform overview</span></span>](../overview/office-add-ins.md)