---
title: Création d’un complément Office Node.js qui utilise l’authentification unique
description: 23/01/2018
ms.openlocfilehash: 4086471bec2ded671e1b3eafebc4fe69e9818344
ms.sourcegitcommit: c72c35e8389c47a795afbac1b2bcf98c8e216d82
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2018
ms.locfileid: "19437646"
---
# <a name="create-a-nodejs-office-add-in-that-uses-single-sign-on-preview"></a><span data-ttu-id="6bcaf-103">Créer un complément Office Node.js qui utilise l’authentification unique (aperçu)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-103">Create a Node.js Office Add-in that uses single sign-on (preview)</span></span>

<span data-ttu-id="6bcaf-p101">Les utilisateurs peuvent se connecter à Office et votre complément Web Office peut tirer parti de cette procédure de connexion pour autoriser les utilisateurs à accéder à votre complément et à Microsoft Graph sans obliger les utilisateurs à se connecter une deuxième fois. Pour obtenir une vue d’ensemble, consultez [Activer l’authentification unique pour des compléments Office](sso-in-office-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p101">Users can sign in to Office, and your Office Web Add-in can take advantage of this sign-in process to authorize users to your add-in and to Microsoft Graph without requiring users to sign in a second time. For an overview, see [Enable SSO in an Office Add-in](sso-in-office-add-ins.md).</span></span>

<span data-ttu-id="6bcaf-106">Cet article vous guide tout au long du processus d’activation de l’authentification unique (SSO) dans un complément intégré à Node.js et Express.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-106">This article walks you through the process of enabling single sign-on (SSO) in an add-in that is built with Node.js and Express.</span></span> 

> [!NOTE]
> <span data-ttu-id="6bcaf-107">Pour voir un article similaire sur un complément basé sur ASP.NET, reportez-vous à [Créer un complément Office ASP.NET qui utilise l’authentification unique](create-sso-office-add-ins-aspnet.md).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-107">For a similar article about an ASP.NET-based add-in, see [Create an ASP.NET Office Add-in that uses single sign-on](create-sso-office-add-ins-aspnet.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bcaf-108">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="6bcaf-108">Prerequisites</span></span>

* <span data-ttu-id="6bcaf-109">[Nœud et npm](https://nodejs.org/en/), version 6.9.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-109">[Node and npm](https://nodejs.org/en/), version 6.9.4 or later</span></span>

* <span data-ttu-id="6bcaf-110">[Git Bash](https://git-scm.com/downloads) (ou un autre client Git)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-110">[Git Bash](https://git-scm.com/downloads) (or another git client)</span></span>

* <span data-ttu-id="6bcaf-111">TypeScript version 2.2.2 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-111">TypeScript version 2.2.2 or later</span></span>

* <span data-ttu-id="6bcaf-112">Office 2016, version 1708, build 8424.nnnn ou version ultérieure (la version par abonnement Office 365, parfois appelée « Démarrer en un clic »).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-112">Office 2016, Version 1708, build 8424.nnnn or later (the Office 365 subscription version, sometimes called “Click to Run”)</span></span>

  <span data-ttu-id="6bcaf-p102">Il vous sera peut-être demandé de participer au programme Office Insider pour obtenir cette version. Pour plus d’informations, consultez la page [Participez au programme Office Insider](https://products.office.com/en-us/office-insider?tab=tab-1).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p102">You might need to be an Office Insider to get this version. For more information, see [Be an Office Insider](https://products.office.com/en-us/office-insider?tab=tab-1).</span></span>

## <a name="set-up-the-starter-project"></a><span data-ttu-id="6bcaf-115">Configurer le projet de démarrage</span><span class="sxs-lookup"><span data-stu-id="6bcaf-115">Set up the starter project</span></span>

1. <span data-ttu-id="6bcaf-116">Clonez ou téléchargez le référentiel sur [Complément Office NodeJS SSO](https://github.com/officedev/office-add-in-nodejs-sso).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-116">Clone or download the repo at [Office Add-in NodeJS SSO](https://github.com/officedev/office-add-in-nodejs-sso).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="6bcaf-117">Il existe deux versions de l’échantillon :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-117">There are two versions of the sample:</span></span>  
    > * <span data-ttu-id="6bcaf-p103">Le dossier **Before** est un projet de démarrage. L’interface utilisateur et d’autres aspects du complément qui ne sont pas directement liés à l’authentification unique ou à l’autorisation sont déjà terminés. Les sections suivantes de cet article vous guident tout au long de la procédure d’exécution de cette dernière.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p103">The **Before** folder is a starter project. The UI and other aspects of the add-in that are not directly connected to SSO or authorization are already done. Later sections of this article walk you through the process of completing it.</span></span> 
    > * <span data-ttu-id="6bcaf-p104">La version **Finale** de l’échantillon s’apparente au complément que vous auriez si vous terminiez les procédures de cet article, sauf que le projet terminé comporte des commentaires de code qui seraient redondants avec le texte de cet article. Pour utiliser la version finale, suivez simplement les instructions de cet article, mais remplacez « Avant » par « Finale » et ignorez les sections **Code côté client** et **Code côté serveur**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p104">The **Completed** version of the sample is just like the add-in that you would have if you completed the procedures of this article, except that the completed project has code comments that would be redundant with the text of this article. To use the completed version, just follow the instructions in this article, but replace "Before" with "Completed" and skip the sections **Code the client side** and **Code the server** side.</span></span>

2. <span data-ttu-id="6bcaf-123">Ouvrez une console Git Bash dans le dossier **Before**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-123">Open a Git bash console in the **Before** folder.</span></span>

3. <span data-ttu-id="6bcaf-124">Saisissez `npm install` dans la console pour installer toutes les dépendances détaillées dans le fichier package.json.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-124">Enter `npm install` in the console to install all of the dependencies itemized in the package.json file.</span></span>

4. <span data-ttu-id="6bcaf-125">Saisissez `npm run build ` dans la console pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-125">Enter `npm run build ` in the console to build the project.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="6bcaf-p105">Il se peut que vous voyiez certaines erreurs de construction indiquant que certaines variables sont déclarées mais pas utilisées. Ignorez ces erreurs. Elles représentent un effet secondaire du fait qu’il manque du code dans la version « Avant » de l’échantillon. Ce code sera ajouté ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p105">You may see some build errors saying that some variables are declared but not used. Ignore these errors. They are a side effect of the fact that the "Before" version of the sample is missing some code that will be added later.</span></span>

## <a name="register-the-add-in-with-azure-ad-v20-endpoint"></a><span data-ttu-id="6bcaf-129">Enregistrez le complément avec le point de terminaison Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="6bcaf-129">Register the add-in with Azure AD v2.0 endpoint</span></span>

<span data-ttu-id="6bcaf-130">Les instructions suivantes sont écrites de façon générique afin qu’elles puissent être utilisées à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-130">The following instruction are written generically so they can be used in multiple places.</span></span> <span data-ttu-id="6bcaf-131">Pour cet article, faites ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-131">For this ariticle do the following:</span></span>
- <span data-ttu-id="6bcaf-132">Remplacez l’espace réservé **$ADD-IN-NAME$** par `“Office-Add-in-NodeJS-SSO`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-132">Replace the placeholder **$ADD-IN-NAME$** with `“Office-Add-in-NodeJS-SSO`.</span></span>
- <span data-ttu-id="6bcaf-133">Remplacez l’espace réservé **$FQDN-WITHOUT-PROTOCOL$** par `localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-133">Replace the placeholder **$FQDN-WITHOUT-PROTOCOL$** with `localhost:3000`.</span></span>
- <span data-ttu-id="6bcaf-134">Lorsque vous spécifiez des autorisations dans la boîte de dialogue **Sélectionner autorisations**, cochez les cases pour les autorisations suivantes.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-134">When you specify permissions in the **Select Permissions** dialog, check the boxes for the following permissions.</span></span> <span data-ttu-id="6bcaf-135">Seule la première est vraiment requise par votre complément lui-même ; mais l'autorisation `profile` est requise pour que l'hôte Office obtienne un jeton pour votre application Web complémentaire.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-135">Only the first is really required by your add-in itself; but the `profile` permission is required for the Office host to get a token to your add-in web application.</span></span>
    * <span data-ttu-id="6bcaf-136">Files.Read.All</span><span class="sxs-lookup"><span data-stu-id="6bcaf-136">Files.Read.All</span></span>
    * <span data-ttu-id="6bcaf-137">profil</span><span class="sxs-lookup"><span data-stu-id="6bcaf-137">profile</span></span>

[!INCLUDE[](../includes/register-sso-add-in-aad-v2-include.md)]


## <a name="grant-administrator-consent-to-the-add-in"></a><span data-ttu-id="6bcaf-138">Accorder le consentement de l'administrateur au complément</span><span class="sxs-lookup"><span data-stu-id="6bcaf-138">Details are at: Grant administrator consent to the add-in</span></span>

[!INCLUDE[](../includes/grant-admin-consent-to-an-add-in-include.md)]

## <a name="configure-the-add-in"></a><span data-ttu-id="6bcaf-139">Configurer le complément</span><span class="sxs-lookup"><span data-stu-id="6bcaf-139">Configure the add-in</span></span>

1. <span data-ttu-id="6bcaf-p108">Dans votre éditeur de code, ouvrez le fichier src\server.ts. Près de la partie supérieure se trouve un appel à un constructeur d’une classe `AuthModule`. Il existe certains paramètres de chaîne dans le constructeur auxquels vous devez affecter des valeurs.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p108">In your code editor, open the src\server.ts file. Near the top there is a call to a constructor of an `AuthModule` class. There are some string parameters in the constructor to which you need to assign values.</span></span>

2. <span data-ttu-id="6bcaf-143">Pour la propriété `client_id`, remplacez l’espace réservé `{client GUID}` par l'ID de l’application, que vous avez enregistré lorsque vous avez enregistré le complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-143">For the `client_id` property, replace the placeholder `{client GUID}` with the application secret that you saved when you registered the add-in.</span></span> <span data-ttu-id="6bcaf-144">Lorsque vous avez terminé, il ne devrait rester q’un GUID entre deux apostrophes.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-144">When you are done, there should just be a GUID in single quotation marks.</span></span> <span data-ttu-id="6bcaf-145">Il ne devrait pas y avoir de ponctuation comme "{}".</span><span class="sxs-lookup"><span data-stu-id="6bcaf-145">There should not be any "{}" characters.</span></span>

3. <span data-ttu-id="6bcaf-146">Pour la propriété `client_secret`, remplacez l’espace réservé `{client secret}` par le secret de l’application que vous avez enregistré lorsque vous avez inscrit le complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-146">For the `client_secret` property, replace the placeholder `{client secret}` with the application secret that you saved when you registered the add-in.</span></span>

4. <span data-ttu-id="6bcaf-p110">Pour la propriété `audience`, remplacez l’espace réservé `{audience GUID}` par l’ID d’application que vous avez enregistré lorsque vous avez inscrit le complément. (La même valeur que celle affectée à la propriété `client_id`.)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p110">For the `audience` property, replace the placeholder `{audience GUID}` with the application ID that you saved when you registered the add-in. (The very same value that you assigned to the `client_id` property.)</span></span>
  
3. <span data-ttu-id="6bcaf-149">Dans la chaîne affectée à la propriété `issuer`, vous verrez l'espace réservé *{GUID locataire O365}*.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-149">In the string assigned to the `issuer` property, you will see the placeholder *{O365 tenant GUID}*.</span></span> <span data-ttu-id="6bcaf-150">Remplacez ceci par l'ID de location Office 365.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-150">Replace this with the Office 365 tenancy ID.</span></span> <span data-ttu-id="6bcaf-151">Pour l'obtenir, [utilisez l'une des méthodes décrites dans](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) Trouver votre identité Office 365.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-151">Use one of the methods in [Find your Office 365 tenant ID](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b) to obtain it.</span></span> <span data-ttu-id="6bcaf-152">Lorsque vous avez terminé, la valeur de la propriété `issuer` devrait ressembler à quelque chose comme ceci :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-152">When you are done, the `issuer` property value should look something like this:</span></span>

    `https://login.microsoftonline.com/12345678-1234-1234-1234-123456789012/v2.0`

1. <span data-ttu-id="6bcaf-153">Conservez les autres paramètres du constructeur `AuthModule` inchangés.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-153">Leave the other parameters in the `AuthModule` constructor unchanged.</span></span> <span data-ttu-id="6bcaf-154">Enregistrez et fermez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-154">Save and close the file.</span></span>

1. <span data-ttu-id="6bcaf-155">Dans la racine du projet, ouvrez le fichier manifeste du complément « Office-Add-in-NodeJS-SSO.xml ».</span><span class="sxs-lookup"><span data-stu-id="6bcaf-155">In the root of the project, open the add-in manifest file “Office-Add-in-NodeJS-SSO.xml”.</span></span>

1. <span data-ttu-id="6bcaf-156">Faites défiler vers le bas du fichier.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-156">Scroll to the bottom of the file.</span></span>

1. <span data-ttu-id="6bcaf-157">Juste au-dessus de la balise de fin `</VersionOverrides>`, vous trouverez le balisage suivant :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-157">Just above the end `</VersionOverrides>` tag, you will find the following markup:</span></span>

    ```xml
    <WebApplicationInfo>
      <Id>{application_GUID here}</Id>
      <Resource>api://localhost:3000/{application_GUID here}</Resource>
      <Scopes>
          <Scope>Files.Read.All</Scope>
          <Scope>profile</Scope>
      </Scopes>
    </WebApplicationInfo>
    ```

1. <span data-ttu-id="6bcaf-158">Remplacez l’espace réservé « {application_GUID here} » *aux deux endroits* du balisage par l’ID d’application que vous avez copié lorsque vous avez enregistré votre complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-158">Replace the placeholder “{application_GUID here}” *in both places* in the markup with the Application ID that you copied when you registered your add-in.</span></span> <span data-ttu-id="6bcaf-159">(Les "{}"ne font pas partie de l'ID, donc ne les incluez pas). Il s'agit du même ID que celui utilisé pour ClientID et Audience dans web.config.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-159">(The "{}" are not part of the ID, so don't include them.) This is the same ID you used in for the ClientID and Audience in the web.config.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="6bcaf-160">La valeur **Resource** correspond à l’**URI d’ID d’application** défini lorsque vous avez ajouté la plateforme d’API web à l’enregistrement du complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-160">The **Resource** value is the **Application ID URI** you set when you added the Web API platform to the registration of the add-in.</span></span>
    > * <span data-ttu-id="6bcaf-161">La section **Scopes** est utilisée uniquement pour générer une boîte de dialogue de consentement si le complément est vendu via AppSource.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-161">The **Scopes** section is used only to generate a consent dialog box if the add-in is sold through AppSource.</span></span>

1. <span data-ttu-id="6bcaf-162">Enregistrez et fermez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-162">Save and close the file.</span></span>

## <a name="code-the-client-side"></a><span data-ttu-id="6bcaf-163">Code côté client</span><span class="sxs-lookup"><span data-stu-id="6bcaf-163">Code the client side</span></span>

1. <span data-ttu-id="6bcaf-p114">Ouvrez le fichier program.js dans le dossier **public**. Il contient déjà du code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p114">Open the program.js file in the **public** folder. It already has some code in it:</span></span>

    * <span data-ttu-id="6bcaf-166">Une affectation à la méthode `Office.initialize` qui affecte elle-même un gestionnaire à l’événement ClickButton `getGraphAccessTokenButton`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-166">An assignment to the `Office.initialize` method that, in turn, assigns a handler to the `getGraphAccessTokenButton` button click event.</span></span>
    * <span data-ttu-id="6bcaf-167">Une méthode `showResult` permettant d’afficher les données renvoyées par Microsoft Graph (ou un message d’erreur) en bas du volet Office.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-167">A `showResult` method that will display data returned from Microsoft Graph (or an error message) at the bottom of the task pane.</span></span>
    * <span data-ttu-id="6bcaf-168">Une méthode `logErrors` qui consigne dans la console les erreurs qui ne sont pas destinées à l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-168">A `logErrors` method that will log to console errors that are not intended for the end user.</span></span>

11. <span data-ttu-id="6bcaf-p115">En dessous de l’affectation au `Office.initialize`, ajoutez le code ci-dessous. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p115">Below the assignment to `Office.initialize`, add the code below. Note the following about this code:</span></span>

    * <span data-ttu-id="6bcaf-171">La gestion des erreurs dans le complément tente parfois automatiquement d’obtenir un jeton d’accès une deuxième fois, à l’aide d’un autre jeu d’options.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-171">The error-handling in the add-in will sometimes automatically attempt a second time to get an access token, using a different set of options.</span></span> <span data-ttu-id="6bcaf-172">La variable de compteur `timesGetOneDriveFilesHasRun` et la variable d’indicateur `triedWithoutForceConsent` et `timesMSGraphErrorReceived` permettent de s’assurer que l’utilisateur ne tente pas de manière répétée d’obtenir un jeton sans y parvenir.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-172">The counter variable `timesGetOneDriveFilesHasRun`, and the flag variables `triedWithoutForceConsent` and `timesMSGraphErrorReceived` are used to ensure that the user isn't cycled repeatedly through failed attempts to get a token.</span></span> 
    * <span data-ttu-id="6bcaf-p117">Vous allez créer la méthode `getDataWithToken` à l’étape suivante, mais rappelez-vous qu’elle définit une option appelée `forceConsent` sur `false`. Vous en saurez plus à la prochaine étape.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p117">You create the `getDataWithToken` method in the next step, but note that it sets an option called `forceConsent` to `false`. More about that in the next step.</span></span>

    ```javascript
    var timesGetOneDriveFilesHasRun = 0;
    var triedWithoutForceConsent = false;
    var timesMSGraphErrorReceived = false;

    function getOneDriveFiles() {
        timesGetOneDriveFilesHasRun++;
        triedWithoutForceConsent = true;
        getDataWithToken({ forceConsent: false });
    }   
    ```

1. <span data-ttu-id="6bcaf-p118">En dessous de la méthode `getOneDriveFiles`, ajoutez le code ci-dessous. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p118">Below the `getOneDriveFiles` method, add the code below. Note the following about this code:</span></span>

    * <span data-ttu-id="6bcaf-p119">est la nouvelle API d’Office.js qui permet à un complément de demander à l’application hôte Office (Excel, PowerPoint, Word, etc.) un jeton d’accès au complément (pour l’utilisateur connecté à Office). L’application hôte Office demande alors le jeton au point de terminaison Azure AD 2.0. Dans la mesure où vous avez préalablement autorisé l’hôte Office sur votre complément lors de son inscription, Azure AD enverra le jeton.`getAccessTokenAsync`</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p119">The `getAccessTokenAsync` is the new API in Office.js that enables an add-in to ask the Office host application (Excel, PowerPoint, Word, etc.) for an access token to the add-in (for the user signed into Office). The Office host application, in turn, asks the Azure AD 2.0 endpoint for the token. Since you preauthorized the Office host to your add-in when you registered it, Azure AD will send the token.</span></span>
    * <span data-ttu-id="6bcaf-180">Si aucun utilisateur n’est connecté à Office, l’hôte Office invite l’utilisateur à se connecter.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-180">If no user is signed into Office, the Office host will prompt the user to sign in.</span></span>
    * <span data-ttu-id="6bcaf-181">Le paramètre d’options définit `forceConsent` sur `false`, donc l’utilisateur ne sera pas invité à accorder à l’hôte Office l’accès à votre complément chaque fois qu’il utilisera le complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-181">The options parameter sets `forceConsent` to `false`, so the user will not be prompted to consent to giving the Office host access to your add-in every time she or he uses the add-in.</span></span> <span data-ttu-id="6bcaf-182">La première fois que l’utilisateur exécutera le complément, l’appel à `getAccessTokenAsync` échouera, mais la logique de gestion des erreurs que vous ajouterez dans une étape ultérieure effectuera automatiquement un autre appel avec le jeu d’options `forceConsent` défini sur `true`, et l’utilisateur sera invité à donner son consentement, mais uniquement la première fois.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-182">The first time the user runs the add-in, the call of `getAccessTokenAsync` will fail, but error-handling logic that you add in a later step will automatically re-call with the `forceConsent` option set to `true` and the user will be prompted to consent, but only that first time.</span></span>
    * <span data-ttu-id="6bcaf-183">Vous créerez la méthode `handleClientSideErrors` à une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-183">You will create the `handleClientSideErrors` method in a later step.</span></span>

    ```javascript
    function getDataWithToken(options) {
    Office.context.auth.getAccessTokenAsync(options,
        function (result) {
            if (result.status === "succeeded") {
                TODO1: Use the access token to get Microsoft Graph data.
            }
            else {
                handleClientSideErrors(result);
            }
        });
    }
    ```

1. <span data-ttu-id="6bcaf-p121">Remplacez TODO1 par les lignes suivantes. Vous créez la méthode `getData` et la route « /api/values » côté serveur dans les étapes suivantes. Une URL relative est utilisée pour le point de terminaison car il doit être hébergé sur le même domaine que votre complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p121">Replace the TODO1 with the following lines. You create the `getData` method and the server-side “/api/values” route in later steps. A relative URL is used for the endpoint because it must be hosted on the same domain as your add-in.</span></span>

    ```javascript
    accessToken = result.value;
    getData("/api/values", accessToken);
    ```

1. <span data-ttu-id="6bcaf-p122">En dessous de la méthode `getOneDriveFiles`, ajoutez le code ci-dessous. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p122">Below the `getOneDriveFiles` method, add the following. About this code, note:</span></span>

    * <span data-ttu-id="6bcaf-p123">Cette méthode appelle un point de terminaison d’API Web spécifié et lui transmet le même jeton d’accès que l’application hôte Office a utilisé pour accéder à votre complément. Côté serveur, ce jeton d’accès est utilisé dans le flux « de la part de » pour obtenir un jeton d’accès à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p123">This method calls a specified Web API endpoint and passes it the same access token that the Office host application used to get access to your add-in. On the server-side, this access token will be used in the “on behalf of” flow to obtain an access token to Microsoft Graph.</span></span>
    * <span data-ttu-id="6bcaf-191">Vous créerez la méthode `handleServerSideErrors` à une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-191">You will create the `handleServerSideErrors` method in a later step.</span></span>

    ```javascript
    function getData(relativeUrl, accessToken) {
        $.ajax({
            url: relativeUrl,
            headers: { "Authorization": "Bearer " + accessToken },
            type: "GET"
        })
        .done(function (result) {
            showResult(result);
        })
        .fail(function (result) {
            handleServerSideErrors(result);
        }); 
    }
    ```

### <a name="create-the-error-handling-methods"></a><span data-ttu-id="6bcaf-192">Création des méthodes de gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="6bcaf-192">Create the error-handling methods</span></span>

1. <span data-ttu-id="6bcaf-193">En dessous de la méthode `getData`, ajoutez la méthode suivante.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-193">Below the `getData` method, add the following method.</span></span> <span data-ttu-id="6bcaf-194">Cette méthode gérera les erreurs dans le client du complément lorsque l’hôte Office ne parviendra pas à obtenir un jeton d’accès pour le service web du complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-194">This method will handle errors in the add-in's client when the Office host is unable to obtain an access token to the add-in's web service.</span></span> <span data-ttu-id="6bcaf-195">Ces erreurs sont signalées avec un code d’erreur, donc la méthode utilise une instruction `switch` pour les distinguer.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-195">These errors are reported with an error code, so the method uses a `switch` statement to distinguish them.</span></span>

    ```javascript
    function handleClientSideErrors(result) {

        switch (result.error.code) {
    
            // TODO2: Handle the case where user is not logged in, or the user cancelled, without responding, a
            //        prompt to provide a 2nd authentication factor. 
    
            // TODO3: Handle the case where the user's sign-in or consent was aborted.
    
            // TODO4: Handle the case where the user is logged in with an account that is neither work or school, 
            //        nor Micrososoft Account.
    
            // TODO5: Handle an unspecified error from the Office host.
    
            // TODO6: Handle the case where the Office host cannot get an access token to the add-ins 
            //        web service/application.
    
            // TODO7: Handle the case where the user tiggered an operation that calls `getAccessTokenAsync` 
            //        before a previous call of it completed.
    
            // TODO8: Handle the case where the add-in does not support forcing consent.
    
            // TODO9: Log all other client errors.
        }
    }
    ```

1. <span data-ttu-id="6bcaf-196">Remplacez `TODO2` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-196">Replace `TODO2` with the following code.</span></span> <span data-ttu-id="6bcaf-197">L’erreur 13001 se produit si l’utilisateur n’est pas connecté, ou s’il a annulé, sans y répondre, une invite lui demandant d’indiquer un deuxième facteur d’authentification.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-197">Error 13001 occurs when the user is not logged in, or the user cancelled, without responding, a prompt to provide a 2nd authentication factor.</span></span> <span data-ttu-id="6bcaf-198">Dans les deux cas, le code réexécute la méthode `getDataWithToken` et définit une option pour forcer une invite de connexion.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-198">In either case, the code re-runs the `getDataWithToken` method and sets an option to force a sign-in prompt.</span></span>

    ```javascript
    case 13001:
        getDataWithToken({ forceAddAccount: true });
        break;
    ```

1. <span data-ttu-id="6bcaf-199">Remplacez `TODO3` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-199">Replace `TODO3` with the following code.</span></span> <span data-ttu-id="6bcaf-200">L’erreur 13002 se produit lorsque la connexion ou l’octroi du consentement de l’utilisateur a été abandonné.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-200">Error 13002 occurs when user's sign-in or consent was aborted.</span></span> <span data-ttu-id="6bcaf-201">Demandez à l’utilisateur de réessayer, mais seulement une fois.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-201">Ask the user to try again but no more than once again.</span></span>

    ```javascript
    case 13002:
        if (timesGetOneDriveFilesHasRun < 2) {
            showResult(['Your sign-in or consent was aborted before completion. Please try that operation again.']);
        } else {
            logError(result);
        }          
        break; 
    ```

1. <span data-ttu-id="6bcaf-202">Remplacez `TODO4` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-202">Replace `TODO4` with the following code.</span></span> <span data-ttu-id="6bcaf-203">L’erreur 13003 se produit si l’utilisateur est connecté avec un compte qui n’est ni un compte professionnel ni un compte scolaire, ni un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-203">Error 13003 occurs when user is logged in with an account that is neither work or school, nor Micrososoft Account.</span></span> <span data-ttu-id="6bcaf-204">Demandez à l’utilisateur de se déconnecter, puis de se reconnecter avec un type de compte pris en charge.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-204">Ask the user to sign-out and then in again with a supported account type.</span></span>

    ```javascript
    case 13003: 
        showResult(['Please sign out of Office and sign in again with a work or school account, or Microsoft Account. Other kinds of accounts, like corporate domain accounts do not work.']);
        break;   
    ```

    > [!NOTE]
    > <span data-ttu-id="6bcaf-205">Les erreurs 13004 et 13005 ne sont pas gérées dans cette méthode, car elles ne devraient se produire qu’en développement.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-205">Errors 13004 and 13005 are not handled in this method because they should only occur in development.</span></span> <span data-ttu-id="6bcaf-206">Elles ne peuvent pas être résolues par du code d’exécution et il ne serait d’aucune utilité de les signaler à un utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-206">They cannot be fixed by runtime code and there would be no point in reporting them to an end user.</span></span>

1. <span data-ttu-id="6bcaf-p129">Remplacez `TODO5` par le code suivant. L’erreur 13006 se produit lorsqu’une erreur non spécifiée indiquant que l’hôte est dans un état instable est survenue dans l’hôte Office. Demandez à l’utilisateur de redémarrer Office.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p129">Replace `TODO5` with the following code. Error 13006 occurs when there has been an unspecified error in the Office host that may indicate that the host is in an unstable state. Ask the user to restart Office.</span></span>

    ```javascript
    case 13006:
        showResult(['Please save your work, sign out of Office, close all Office applications, and restart this Office application.']);
        break;        
    ```

1. <span data-ttu-id="6bcaf-210">Remplacez `TODO6` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-210">Replace `TODO6` with the following code.</span></span> <span data-ttu-id="6bcaf-211">L’erreur 13007 se produit lorsqu’un problème est survenu au niveau de l’interaction de l’hôte Office avec AAD de telle sorte que l’hôte ne peut pas obtenir de jeton d’accès pour accéder à l’application/au service Web des compléments.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-211">Error 13007 occurs when something has gone wrong with the Office host's interaction with AAD so the host cannot get an access token to the add-ins web service/application.</span></span> <span data-ttu-id="6bcaf-212">Il peut s’agir d’un problème temporaire de réseau.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-212">This may be a temporary network issue.</span></span> <span data-ttu-id="6bcaf-213">Demandez à l’utilisateur de réessayer plus tard.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-213">Ask the user to try again later.</span></span>

    ```javascript
    case 13007:
        showResult(['That operation cannot be done at this time. Please try again later.']);
        break;      
    ```

1. <span data-ttu-id="6bcaf-p131">Remplacez `TODO7`  par le code suivant. L’erreur 13008 se produit lorsque l’utilisateur a déclenché une opération qui appelle `getAccessTokenAsync`  avant la fin de l’appel précédent.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p131">Replace `TODO7` with the following code. Error 13008 occurs when the user tiggered an operation that calls `getAccessTokenAsync` before a previous call of it completed.</span></span>

    ```javascript
    case 13008:
        showResult(['Please try that operation again after the current operation has finished.']);
        break;
    ```      

1. <span data-ttu-id="6bcaf-216">Remplacez `TODO8` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-216">Replace `TODO8` with the following code.</span></span> <span data-ttu-id="6bcaf-217">L’erreur 13009 se produit lorsque le complément ne prend pas en charge l’obligation d’afficher une invite de consentement, mais que `getAccessTokenAsync` a été appelé avec l’option `forceConsent` définie sur `true`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-217">Error 13009 occurs when the add-in does not support forcing consent, but `getAccessTokenAsync` was called with the `forceConsent` option set to `true`.</span></span> <span data-ttu-id="6bcaf-218">Dans le cas habituel, lorsque cela se produit, le code doit automatiquement réexécuter `getAccessTokenAsync` avec l’option de consentement définie sur `false`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-218">In the usual case when this happens the code should automatically re-run `getAccessTokenAsync` with the consent option set to `false`.</span></span> <span data-ttu-id="6bcaf-219">Toutefois, dans certains cas, l’appel de la méthode avec `forceConsent` défini sur `true` était lui-même une réponse automatique à une erreur dans un appel à la méthode avec l’option définie sur `false`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-219">However, in some cases, calling the method with `forceConsent` set to `true` was itself an automatic response to an error in a call to the method with the option set to `false`.</span></span> <span data-ttu-id="6bcaf-220">Dans ce cas, le code ne doit pas réessayer, mais il doit à la place conseiller à l’utilisateur de se déconnecter et de se reconnecter.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-220">In that case, the code should not try again, but instead it should advise the user to sign out and sign in again.</span></span>

    ```javascript
    case 13009:
        if (triedWithoutForceConsent) {
            showResult(['Please sign out of Office and sign in again with a work or school account, or Microsoft Account.']);
        } else {
            getDataWithToken({ forceConsent: false });
        }
        break;
    ```      
    
1. <span data-ttu-id="6bcaf-221">Remplacez `TODO9` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-221">Replace `TODO9` with the following code.</span></span>

    ```javascript
    default:
        logError(result);
        break;
    ```  

1. <span data-ttu-id="6bcaf-p133">En dessous de la méthode `handleClientSideErrors`, ajoutez la méthode suivante. Cette méthode gérera les erreurs du service web du complément en cas de problème d’exécution du flux « de la part de » ou de problème d’obtention de données à partir de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p133">Below the `handleClientSideErrors` method, add the following method. This method will handle errors in the add-in's web service when something goes wrong in executing the on-behalf-of flow or in getting data from Microsoft Graph.</span></span>

    ```javascript
    function handleServerSideErrors(result) {
    
        // TODO10: Handle the case where AAD asks for an additional form of authentication.

        // TODO11: Handle the case where consent has not been granted, or has been revoked.

        // TODO12: Handle the case where an invalid scope (permission) was used in the on-behalf-of flow

        // TODO13: Handle the case where the token that the add-in's client-side sends to it's 
        //         server-side is not valid because it is missing `access_as_user` scope (permission).

        // TODO14: Handle the case where the token sent to Microsoft Graph in the request for 
        //         data is expired or invalid.

        // TODO15: Log all other server errors.
    }
    ```

1. <span data-ttu-id="6bcaf-p134">Remplacez `TODO10` par le code suivant. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p134">Replace `TODO10` with the following code. Note about this code:</span></span>

    * <span data-ttu-id="6bcaf-p135">Il existe des configurations d’Azure Active Directory où l’on demande à l’utilisateur de fournir un ou plusieurs facteurs d’authentification supplémentaires pour accéder à certaines cibles Microsoft Graph (par exemple, OneDrive), même si l’utilisateur peut se connecter à Office par un simple mot de passe. Dans ce cas, AAD enverra, avec l’erreur 50076, une réponse comportant la propriété `Claims`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p135">There are configurations of Azure Active Directory in which the user is required to provide additional authentication factor(s) to access some Microsoft Graph targets (e.g., OneDrive), even if the user can sign on to Office with just a password. In that case, AAD will send a response, with error 50076, that has a `Claims` property.</span></span> 
    * <span data-ttu-id="6bcaf-228">L’hôte Office dois obtenir un nouveau jeton avec la valeur **Claims** pour l’option `authChallenge`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-228">The Office host should get a new token with the **Claims** value as the `authChallenge` option.</span></span> <span data-ttu-id="6bcaf-229">Cela demande à AAD d’inviter l’utilisateur à accepter tous les formulaires d’authentification requis.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-229">This tells AAD to prompt the user for all required forms of authentication.</span></span> 

    ```javascript
    if (result.responseJSON.error.innerError
            && result.responseJSON.error.innerError.error_codes
            && result.responseJSON.error.innerError.error_codes[0] === 50076){
        getDataWithToken({ authChallenge: result.responseJSON.error.innerError.claims });
    }
    ```

1. <span data-ttu-id="6bcaf-p137">Remplacez `TODO11` par le code suivant *juste en dessous de la dernière accolade fermante du code que vous avez ajouté à l’étape précédente*. Tenez compte des remarques suivantes à propos de ce code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p137">Replace `TODO11` with the following code *just below the last closing brace of the code you added in the previous step*. Note about this code:</span></span>

    * <span data-ttu-id="6bcaf-232">L’erreur 65001 signifie que l’utilisateur a refusé de donner l’accès à Microsoft Graph (ou que l’accès a été révoqué) pour une ou plusieurs autorisations.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-232">Error 65001 means that consent to access Microsoft Graph was not granted (or was revoked) for one or more permissions.</span></span> 
    * <span data-ttu-id="6bcaf-233">Le complément doit obtenir un nouveau jeton avec l’option `forceConsent` définie sur `true`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-233">The add-in should get a new token with the `forceConsent` option set to `true`.</span></span>

    ```javascript
    else if (result.responseJSON.error.innerError
            && result.responseJSON.error.innerError.error_codes
            && result.responseJSON.error.innerError.error_codes[0] === 65001){
        showResult(['Please grant consent to this add-in to access your Microsoft Graph data.']);        
        /*
            THE FORCE CONSENT OPTION IS NOT AVAILABLE IN DURING PREVIEW. WHEN SSO FOR
            OFFICE ADD-INS IS RELEASED, REMOVE THE showResult LINE ABOVE AND UNCOMMENT
            THE FOLLOWING LINE.
        */
        // getDataWithToken({ forceConsent: true });
    }
    ```

1. <span data-ttu-id="6bcaf-p138">Remplacez `TODO12` par le code suivant *juste en dessous de la dernière accolade fermante du code que vous avez ajouté à l’étape précédente*. Tenez compte des remarques suivantes à propos de ce code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p138">Replace `TODO12` with the following code *just below the last closing brace of the code you added in the previous step*. Note about this code:</span></span>

    * <span data-ttu-id="6bcaf-236">L’erreur 70011 signifie qu’une portée (autorisation) non valide a été demandée.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-236">Error 70011 means that an invalid scope (permission) has been requested.</span></span> <span data-ttu-id="6bcaf-237">Le complément doit signaler l’erreur.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-237">The add-in should report the error.</span></span>
    * <span data-ttu-id="6bcaf-238">Le code consigne les autres erreurs avec un numéro d’erreur AAD.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-238">The code logs any other error with an AAD error number.</span></span>

    ```javascript
    else if (result.responseJSON.error.innerError
            && result.responseJSON.error.innerError.error_codes
            && result.responseJSON.error.innerError.error_codes[0] === 70011){
        showResult(['The add-in is asking for a type of permission that is not recognized.']);
    }
    ```

1. <span data-ttu-id="6bcaf-p140">Remplacez `TODO13` par le code suivant *juste en dessous de la dernière accolade fermante du code que vous avez ajouté à l’étape précédente*. Tenez compte des remarques suivantes à propos de ce code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p140">Replace `TODO13` with the following code *just below the last closing brace of the code you added in the previous step*. Note about this code:</span></span>

    * <span data-ttu-id="6bcaf-241">Le code côté serveur que vous créerez à une étape ultérieure enverra le message qui se termine par `... expected access_as_user` si l’étendue (autorisation) `access_as_user` ne se trouve pas dans le jeton d’accès que le client du complément envoie à AAD, afin qu’il soit utilisé dans le flux « de la part de ».</span><span class="sxs-lookup"><span data-stu-id="6bcaf-241">Server-side code that you create in a later step will send the message that ends with `... expected access_as_user` if the `access_as_user` scope (permission) is not in the access token that the add-in's client sends to AAD to be used in the on-behalf-of flow.</span></span>
    * <span data-ttu-id="6bcaf-242">Le complément doit signaler l’erreur.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-242">The add-in should report the error.</span></span>

    ```javascript
    else if (result.responseJSON.error.name
            && result.responseJSON.error.name.indexOf('expected access_as_user') !== -1){
        showResult(['Microsoft Office does not have permission to get Microsoft Graph data on behalf of the current user.']);
    }
    ```

1. <span data-ttu-id="6bcaf-p141">Remplacez `TODO14` par le code suivant *juste en dessous de la dernière accolade fermante du code que vous avez ajouté à l’étape précédente*. Tenez compte des remarques suivantes à propos de ce code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p141">Replace `TODO14` with the following code *just below the last closing brace of the code you added in the previous step*. Note about this code:</span></span>

    * <span data-ttu-id="6bcaf-245">Il est peu probable qu’un jeton expiré ou non valide soit envoyé à Microsoft Graph. Cependant, si cela se produit, le code côté serveur que vous créerez dans une étape ultérieure se terminera par la chaîne `Microsoft Graph error`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-245">It is unlikely that an expired or invalid token will be sent to Microsoft Graph; but if it does happen, the server-side code that you will create in a later step will end with the string `Microsoft Graph error`.</span></span>
    * <span data-ttu-id="6bcaf-246">Dans ce cas, le complément doit recommencer l’intégralité du processus d’authentification en réinitialisant les variables de compteur `timesGetOneDriveFilesHasRun` et d’indicateur `timesGetOneDriveFilesHasRun`, puis en appelant à nouveau la méthode de gestionnaire de boutons.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-246">In this case, the add-in should start the entire authentication process over by resetting the `timesGetOneDriveFilesHasRun` counter and `timesGetOneDriveFilesHasRun` flag variables, and then re-calling the button handler method.</span></span> <span data-ttu-id="6bcaf-247">Toutefois, il ne doit faire cela qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-247">But it should do this only once.</span></span> <span data-ttu-id="6bcaf-248">Si l’erreur se produit à nouveau, il doit simplement la consigner.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-248">If it happens again, it should just log the error.</span></span>
    * <span data-ttu-id="6bcaf-249">Le code consigne l’erreur si elle se produit deux fois de suite.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-249">The code logs the error if it happens twice in succession.</span></span>

    ```javascript
    else if (result.responseJSON.error.name
            && result.responseJSON.error.name.indexOf('Microsoft Graph error') !== -1) {
        if (!timesMSGraphErrorReceived) {
            timesMSGraphErrorReceived = true;
            timesGetOneDriveFilesHasRun = 0;
            triedWithoutForceConsent = false;
            getOneDriveFiles();
        } else {
            logError(result);
        }        
    }
    ```

1. <span data-ttu-id="6bcaf-250">Remplacez `TODO15` par le code suivant *juste en dessous de la dernière accolade fermante du code que vous avez ajouté à l’étape précédente*.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-250">Replace `TODO15` with the following code *just below the last closing brace of the code you added in the previous step*.</span></span>

    ```javascript
    else {
        logError(result);
    }
    ```

## <a name="code-the-server-side"></a><span data-ttu-id="6bcaf-251">Code côté serveur</span><span class="sxs-lookup"><span data-stu-id="6bcaf-251">Code the server side</span></span>

<span data-ttu-id="6bcaf-252">Il existe deux fichiers côté serveur qui doivent être modifiés.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-252">There are two server-side files that need to be modified.</span></span> 
- <span data-ttu-id="6bcaf-p143">Le fichier src\auth.js fournit des fonctions d’assistance pour l’autorisation. Il dispose déjà des membres génériques qui sont utilisés dans une variété de flux d’autorisation. Nous devons ajouter des fonctions qui implémentent le flux « de la part de ».</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p143">The src\auth.js provides authorization helper functions. It already has generic members that are used in a variety of authorization flows. We need to add functions to it that implement the "on behalf of" flow.</span></span>
- <span data-ttu-id="6bcaf-p144">Le fichier src\server.js possède les membres de base requis pour exécuter un serveur et les intergiciels express. Nous devons y ajouter des fonctions qui servent la page d’accueil et une API Web pour obtenir des données Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p144">The src\server.js file has the basic members need to run a server and express middleware. We need to add functions to it that serve the home page and a Web API for obtaining Microsoft Graph data.</span></span>

### <a name="create-a-method-to-exchange-tokens"></a><span data-ttu-id="6bcaf-258">Créer une méthode pour échanger des jetons</span><span class="sxs-lookup"><span data-stu-id="6bcaf-258">Create a method to exchange tokens</span></span>

1. <span data-ttu-id="6bcaf-p145">Ouvrez le fichier \src\auth.ts. Ajoutez la méthode ci-après à la classe `AuthModule`. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p145">Open the \src\auth.ts file. Add the method below to the `AuthModule` class. Note the following about this code:</span></span>

    * <span data-ttu-id="6bcaf-p146">Le paramètre `jwt` est le jeton d’accès à l’application. Dans le flux « de la part de », il est échangé avec AAD contre un jeton d’accès à la ressource.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p146">The `jwt` parameter is the access token to the application. In the "on behalf of" flow, it is exchanged with AAD for an access token to the resource.</span></span>
    * <span data-ttu-id="6bcaf-264">Le paramètre scopes a une valeur par défaut, mais dans cet exemple, elle sera remplacée par le code appelant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-264">The scopes parameter has a default value, but in this sample it will be overridden by the calling code.</span></span>
    * <span data-ttu-id="6bcaf-p147">Le paramètre de ressource est facultatif. Il ne doit pas être utilisé lorsque le STS est le point de terminaison AAD V 2.0. Le point de terminaison AAD V 2.0 déduit la ressource des étendues et renvoie une erreur si une ressource est envoyée dans la requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p147">The resource parameter is optional. It should not be used when the STS is the AAD V 2.0 endpoint. The V 2.0 endpoint infers the resource from the scopes and it returns an error if a resource is sent in the HTTP Request.</span></span> 
    * <span data-ttu-id="6bcaf-268">La génération d’une exception dans le bloc `catch` ne provoquera *pas* l’envoi immédiat du message « 500 Erreur interne du serveur » au client.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-268">Throwing an exception in the `catch` block will *not* cause an immediate "500 Internal Server Error" to be sent to the client.</span></span> <span data-ttu-id="6bcaf-269">L’appel de code dans le fichier server.js interceptera cette exception et la convertira en un message d’erreur qui sera envoyé au client.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-269">Calling code in the server.js file will catch this exception and turn it into an error message that is sent to the client.</span></span>

        ```javascript
        private async exchangeForToken(jwt: string, scopes: string[] = ['openid'], resource?: string) {
            try {
                // TODO3: Construct the parameters that will be sent in the body of the 
                //        HTTP Request to the STS that starts the "on behalf of" flow.
                // TODO4: Send the request to the STS.
                // TODO5: Catch errors from the STS and relay them to the client.
                // TODO6: Process the response and persist the access token to resource.
            }
            catch (exception) {
                throw new UnauthorizedError('Unable to obtain an access token to the resource' 
                                            + JSON.stringify(exception), 
                                            exception);
            }
        }
        ```

2. <span data-ttu-id="6bcaf-p149">Remplacez `TODO3` par le code suivant. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p149">Replace `TODO3` with the following code. About this code, note:</span></span>
    * <span data-ttu-id="6bcaf-p150">Un STS qui prend en charge le flux « de la part de » attend certaines paires de propriété/valeur dans le corps de la requête HTTP. Ce code construit un objet qui devient le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p150">An STS that supports the "on behalf of" flow expects certain property/value pairs in the body of the HTTP request. This code constructs an object that will become the body of the request.</span></span> 
    * <span data-ttu-id="6bcaf-274">Une propriété de ressource est ajoutée au corps si, et uniquement si, une ressource a été transmise à la méthode.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-274">A resource property is added to the body if, and only if, a resource was passed to the method.</span></span>

        ```javascript
        const v2Params = {
                client_id: this.clientId,
                client_secret: this.clientSecret,
                grant_type: 'urn:ietf:params:oauth:grant-type:jwt-bearer',
                assertion: jwt,
                requested_token_use: 'on_behalf_of',
                scope: scopes.join(' ')
            };
            let finalParams = {};
            if (resource) {
                // In JavaScript we could just add the resource property to the v2Params
                // object, but that won't compile in TypeScript.
                let v1Params  = { resource: resource };  
                for(var key in v2Params) { v1Params[key] = v2Params[key]; }
                finalParams = v1Params;
            } else {
                finalParams = v2Params;
            } 
        ```

3. <span data-ttu-id="6bcaf-275">Remplacez `TODO4` par le code suivant, qui envoie la requête HTTP au point de terminaison de jeton du STS.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-275">Replace `TODO4` with the following code which sends the HTTP request to the token endpoint of the STS.</span></span>

    ```javascript
    const res = await fetch(`${this.stsDomain}/${this.tenant}/${this.tokenURLsegment}`, {
        method: 'POST',
        body: form(finalParams),
        headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/x-www-form-urlencoded'
        }
    }); 
    ```

4. <span data-ttu-id="6bcaf-276">Remplacez `TODO5` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-276">Replace `TODO5` with the following code.</span></span> <span data-ttu-id="6bcaf-277">Vous remarquerez que la génération d’une exception ne provoquera *pas* l’envoi immédiat d’un message « 500 Erreur interne du serveur » au client.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-277">Note that throwing an exception will *not* cause an immediate "500 Internal Server Error" to be sent to the client.</span></span> <span data-ttu-id="6bcaf-278">L’appel de code dans le fichier server.js interceptera cette exception et la convertira en un message d’erreur qui sera envoyé au client.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-278">Calling code in the server.js file will catch this exception and turn it into an error message that is sent to the client.</span></span>

    ```javascript
     if (res.status !== 200) {
        const exception = await res.json();
        throw exception;                
    } 
    ```

5. <span data-ttu-id="6bcaf-p152">Remplacez `TODO6` par le code suivant. Vous remarquerez que le code prolonge le jeton d’accès à la ressource et son délai d’expiration, en plus de le renvoyer. Le code d’appel permet d’éviter les appels inutiles au STS en réutilisant un jeton d’accès non expiré à la ressource. Vous verrez comment procéder dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p152">Replace `TODO6` with the following code. Note that the code persists the access token to the resource, and it's expiration time, in addition to returning it. Calling code can avoid unnecessary calls to the STS by reusing an unexpired access token to the resource. You'll see how to do that in the next section.</span></span>

    ```javascript  
    const json = await res.json();
    const resourceToken = json['access_token'];
    ServerStorage.persist('ResourceToken', resourceToken);
    const expiresIn = json['expires_in'];  // seconds until token expires.
    const resourceTokenExpiresAt = moment().add(expiresIn, 'seconds');
    ServerStorage.persist('ResourceTokenExpiresAt', resourceTokenExpiresAt);
    return resourceToken; 
    ```

6. <span data-ttu-id="6bcaf-283">Enregistrez le fichier, mais ne le fermez pas.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-283">Save the file, but don't close it.</span></span>

### <a name="create-a-method-to-get-access-to-the-resource-using-the-on-behalf-of-flow"></a><span data-ttu-id="6bcaf-284">Créer une méthode pour accéder à la ressource à l’aide du flux « de la part de »</span><span class="sxs-lookup"><span data-stu-id="6bcaf-284">Create a method to get access to the resource using the "on behalf of" flow</span></span>

1. <span data-ttu-id="6bcaf-p153">Toujours dans src/auth.ts, ajoutez la méthode ci-après à la classe `AuthModule`. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p153">Still in src/auth.ts, add the method below to the `AuthModule` class. Note the following about this code:</span></span>

    * <span data-ttu-id="6bcaf-287">Les commentaires ci-dessus concernant les paramètres de la méthode `exchangeForToken` s’appliquent aussi aux paramètres de cette méthode.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-287">The comments above about the parameters to the the `exchangeForToken` method apply to the parameters of this method as well.</span></span>
    * <span data-ttu-id="6bcaf-p154">La méthode recherche d’abord dans le stockage permanent un jeton d’accès à la ressource qui n’a pas expiré et qui ne va pas expirer dans la minute qui suit. Il appelle la méthode `exchangeForToken` que vous avez créée dans la dernière section uniquement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p154">The method first checks the persistent storage for an access token to the resource that has not expired and is not going to expire in the next minute. It calls the `exchangeForToken` method you created in the last section only if it needs to.</span></span>

    ```javascript
    async acquireTokenOnBehalfOf(jwt: string, scopes: string[] = ['openid'], resource?: string) {
        const resourceTokenExpirationTime = ServerStorage.retrieve('ResourceTokenExpiresAt');
        if (moment().add(1, 'minute').diff(resourceTokenExpirationTime) < 1 ) {
            return ServerStorage.retrieve('ResourceToken');
        } else if (resource) {
            return this.exchangeForToken(jwt, scopes, resource);
        } else {
            return this.exchangeForToken(jwt, scopes);
        }
    } 
    ```

2. <span data-ttu-id="6bcaf-290">Enregistrez et fermez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-290">Save and close the file.</span></span>

### <a name="create-the-endpoints-that-will-serve-the-add-ins-home-page-and-data"></a><span data-ttu-id="6bcaf-291">Créer les points de terminaison que serviront la page d’accueil et les données du complément</span><span class="sxs-lookup"><span data-stu-id="6bcaf-291">Create the endpoints that will serve the add-in's home page and data</span></span>

1. <span data-ttu-id="6bcaf-292">Ouvrez le fichier src\server.ts.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-292">Open the src\server.ts file.</span></span> 

2. <span data-ttu-id="6bcaf-p155">Ajoutez la méthode suivante au bas du fichier. Cette méthode servira la page d’accueil du complément. Le manifeste du complément spécifie l’URL de la page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p155">Add the following method to the bottom of the file. This method will serve the add-in's home page. The add-in manifest specifies the home page URL.</span></span>

    ```javascript
    app.get('/index.html', handler(async (req, res) => {
        return res.sendfile('index.html');
    })); 
    ```

3. <span data-ttu-id="6bcaf-p156">Ajoutez la méthode suivante en bas du fichier. Cette méthode traite toutes les requêtes concernant l’API `onedriveitems`.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p156">Add the following method to bottom of the file. This method will handle any requests for the `onedriveitems` API.</span></span>
    ```javascript
    app.get('/api/onedriveitems', handler(async (req, res) => {
        // TODO7: Initialize the AuthModule object and validate the access token 
        //        that the client-side received from the Office host.
        // TODO8: Get a token to Microsoft Graph from either persistent storage 
        //        or the "on behalf of" flow.
        // TODO9: Use the token to get data from Microsoft Graph.
        // TODO10: Relay any errors from Microsoft Graph to the client.
        // TODO11: Send to the client only the data that it actually needs.
    })); 
    ```

4. <span data-ttu-id="6bcaf-p157">Remplacez `TODO7` par le code suivant qui valide le jeton d’accès reçu de la part de l’application hôte Office. La méthode `verifyJWT` est définie dans le fichier src\auth.ts. Elle valide toujours l’audience et l’émetteur. Nous utilisons le paramètre facultatif pour spécifier que nous souhaitons également vérifier que l’étendue du jeton d’accès est `access_as_user`. C’est la seule autorisation du complément dont l’utilisateur et l’hôte Office ont besoin pour obtenir un jeton d’accès à Microsoft Graph au moyen du flux « de la part de ».</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p157">Replace `TODO7` with the following code which validates the access token received from the Office host application. The `verifyJWT` method is defined in the src\auth.ts file. It always validates the audience and the issuer. We use the optional parameter to specify that we also want it to verify that the scope in the access token is `access_as_user`. This is the only permisison to the add-in that the user and the Office host need in order to get an access token to Microsoft Graph by means of the "on behalf" flow.</span></span> 

    ```javascript
    await auth.initialize();
    const { jwt } = auth.verifyJWT(req, { scp: 'access_as_user' }); 
    ```

    > [!NOTE]
    > <span data-ttu-id="6bcaf-p158">Vous devez uniquement utiliser l’étendue `access_as_user` pour autoriser l’API qui gère le flux « de la part de » pour les compléments Office. Les autres API de votre service peuvent avoir leurs propres exigences d’étendue. Cela limite les possibilités d’accès avec les jetons acquis par Office.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p158">You should only use the `access_as_user` scope to authorize the API that handles the on-behalf-of flow for Office add-ins. Other APIs in your service should have their own scope requirements. This limits what can be accessed with the tokens that Office acquires.</span></span>

5. <span data-ttu-id="6bcaf-p159">Remplacez `TODO8` par le code suivant. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p159">Replace `TODO8` with the following code. Note the following about this code:</span></span>

    * <span data-ttu-id="6bcaf-307">L’appel vers `acquireTokenOnBehalfOf` ne comprend pas de paramètre de ressource, étant donné que nous avons construit l’objet `AuthModule` (`auth`) avec le point de terminaison AAD V2.0 qui ne prend pas en charge une propriété de ressource.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-307">The call to `acquireTokenOnBehalfOf` does not include a resource parameter because we constructed the `AuthModule` object (`auth`) with the AAD V2.0 endpoint which does not support a resource property.</span></span>
    * <span data-ttu-id="6bcaf-308">Le deuxième paramètre de l’appel spécifie les autorisations dont le complément aura besoin pour obtenir une liste des fichiers et dossiers de l’utilisateur dans OneDrive.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-308">The second parameter of the call specifies the permissions the add-in will need to get a list of the user's files and folders on OneDrive.</span></span> <span data-ttu-id="6bcaf-309">(L’autorisation `profile` n’est pas demandée, car elle n’est nécessaire qu’au moment où l’hôte Office obtient le jeton d’accès à votre complément, pas lorsque vous travaillez dans ce jeton pour un jeton d’accès à Microsoft Graph.)</span><span class="sxs-lookup"><span data-stu-id="6bcaf-309">(The `profile` permission is not requested because it is only needed when the Office host gets the access token to your add-in, not when you are trading in that token for an access token to Microsoft Graph.)</span></span>

    ```javascript
    const graphToken = await auth.acquireTokenOnBehalfOf(jwt, ['Files.Read.All']);
    ```

6. <span data-ttu-id="6bcaf-p161">Remplacez `TODO9` par la ligne suivante. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p161">Replace `TODO9` with the following line. Note the following about this code:</span></span>

    * <span data-ttu-id="6bcaf-312">La classe MSGraphHelper est définie dans src\msgraph-helper.ts.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-312">The MSGraphHelper class is defined in src\msgraph-helper.ts.</span></span> 
    * <span data-ttu-id="6bcaf-313">Nous réduisons les données qui doivent être renvoyées en spécifiant que nous ne souhaitons que la propriété name et uniquement les 3 premiers éléments.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-313">We minimize the data that must be returned by specifying that we only want the name property and only the first 3 items.</span></span>

    `const graphData = await MSGraphHelper.getGraphData(graphToken, "/me/drive/root/children", "?$select=name&$top=3");`

7. <span data-ttu-id="6bcaf-314">Remplacez `TODO10` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-314">Replace `TODO10` with the following code.</span></span> <span data-ttu-id="6bcaf-315">Notez que ce code gère les erreurs « 401 Non autorisé » de Microsoft Graph qui signalent un jeton expiré ou non valide.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-315">Note that this code handles '401 Unauthorized" errors from Microsoft Graph which would indicate an expired or invalid token.</span></span> <span data-ttu-id="6bcaf-316">Il est très peu probable que cela se produise, car la logique persistante du jeton doit empêcher ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-316">It is very unlikely that this would ever happen since the token persisting logic should prevent it.</span></span> <span data-ttu-id="6bcaf-317">(Reportez-vous à la section **Créer une méthode pour accéder à la ressource à l’aide du flux « de la part de »** ci-dessus.) Si cela se produit, ce code communiquera l’erreur au client avec, dans le nom de l’erreur, « Microsoft Graph error ».</span><span class="sxs-lookup"><span data-stu-id="6bcaf-317">(See the section **Create a method to get access to the resource using the "on behalf of" flow** above.) If it does happen, this code will relay the error to the client with "Microsoft Graph error" in the error name.</span></span> <span data-ttu-id="6bcaf-318">(Reportez-vous à la méthode `handleClientSideErrors` que vous avez créée dans le fichier program.js dans une étape précédente.) Le code que vous ajouterez au fichier ODataHelper.js à une étape ultérieure vous permet de traiter les erreurs provenant de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-318">(See the `handleClientSideErrors` method that you created in the program.js file in an earlier step.) Code that you add to the ODataHelper.js file in a later step helps process errors from Microsoft Graph.</span></span>

    ```javascript
    if (graphData.code) {
        if (graphData.code === 401) {
            throw new UnauthorizedError('Microsoft Graph error', graphData);
        }
    }
    ```


1. <span data-ttu-id="6bcaf-p163">Remplacez `TODO11` par le code suivant. Notez que Microsoft Graph renvoie des métadonnées OData et une propriété **eTag** pour chaque élément, même si `name` est la seule propriété demandée. Le code envoie uniquement les noms d’éléments au client.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p163">Replace `TODO11` with the following code. Note that Microsoft Graph returns some OData metadata and an **eTag** property for every item, even if `name` is the only property requested. The code sends only the item names to the client.</span></span>

    ```javascript
    const itemNames: string[] = [];
    const oneDriveItems: string[] = graphData['value'];
    for (let item of oneDriveItems){
        itemNames.push(item['name']);
    }
    return res.json(itemNames);
    ```

8. <span data-ttu-id="6bcaf-322">Enregistrez et fermez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-322">Save and close the file.</span></span>

### <a name="add-response-handling-to-the-odatahelper"></a><span data-ttu-id="6bcaf-323">Ajouter une gestion des réponses à ODataHelper</span><span class="sxs-lookup"><span data-stu-id="6bcaf-323">Add response handling to the ODataHelper</span></span>

1. <span data-ttu-id="6bcaf-324">Ouvrez le fichier src\odata-helper.ts.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-324">Open the file src\odata-helper.ts.</span></span> <span data-ttu-id="6bcaf-325">Le fichier est presque complet.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-325">The file is almost complete.</span></span> <span data-ttu-id="6bcaf-326">Il manquant le corps du rappel au gestionnaire pour l’événement de « fin » de demande.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-326">What's missing is the body of the callback to the handler for the request "end" event.</span></span> <span data-ttu-id="6bcaf-327">Remplacez `TODO` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-327">Replace the `TODO` with the following code.</span></span> <span data-ttu-id="6bcaf-328">Tenez compte des informations suivantes sur ce code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-328">About this code note:</span></span>

    * <span data-ttu-id="6bcaf-329">La réponse du point de terminaison OData peut-être une erreur, supposons une erreur 401 si le point de terminaison nécessite un jeton d’accès et que celui-ci n’est pas valide ou a expiré.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-329">The response from the OData endpoint might be an error, say a 401 if the endpoint requires an access token and it was invalid or expired.</span></span> <span data-ttu-id="6bcaf-330">Cependant, un message d’erreur reste un *message*, pas une erreur dans l’appel de `https.get`, donc la ligne `on('error', reject)` à la fin de `https.get` n’est pas déclenchée.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-330">But an error message is still a *message*, not an error in the call of `https.get`, so the `on('error', reject)` line at the end of `https.get` isn't triggered.</span></span> <span data-ttu-id="6bcaf-331">Par conséquent, le code distingue les messages de réussite (200) des messages d’erreur, et envoie un objet JSON à l’appelant soit les informations d’erreur, soit avec les informations demandées.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-331">So, the code distinguishes success (200) messages from error messages and sends a JSON object to the caller with either the requested OData or error information.</span></span>

    ```javascript
    var error;
    if (response.statusCode === 200) {
        // TODO1: Return the data to the caller and resolve the Promise.
    } else {
       // TODO2: Return an error object to the caller and resolve the Promise.
    }
    ```

1.  <span data-ttu-id="6bcaf-p166">Remplacez `TODO1` par le code suivant. Notez que le code suppose que les données sont renvoyées au format JSON.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p166">Replace `TODO1` with the following code. Note that the code assumes the data is returned as JSON.</span></span>

    ```javascript
    let parsedBody = JSON.parse(body);
    resolve(parsedBody);
    ```

1.  <span data-ttu-id="6bcaf-p167">Remplacez `TODO2` par le code suivant. Tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p167">Replace `TODO2` with the following code. Note about this code:</span></span>

    * <span data-ttu-id="6bcaf-336">Une réponse d’erreur d’une source OData aura toujours un code d’état (statusCode) et généralement un message d’état (statusMessage).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-336">An error response from an OData source will always have a statusCode and usually a statusMessage.</span></span> <span data-ttu-id="6bcaf-337">Certaines sources OData ajoutent également une propriété d’erreur au corps avec des informations supplémentaires, telles qu’un message et un code internes, ou plus spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-337">Some OData sources also add an error property to the body with further information, such as an inner, or more specific, code and message.</span></span>
    * <span data-ttu-id="6bcaf-338">L’objet de promesse est résolu, pas rejeté.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-338">The Promise object is resolved, not rejected.</span></span> <span data-ttu-id="6bcaf-339">s’exécute quand un service web appelle un point de terminaison OData de serveur à serveur.`https.get`</span><span class="sxs-lookup"><span data-stu-id="6bcaf-339">The `https.get` runs when a web service calls an OData endpoint server-to-server.</span></span> <span data-ttu-id="6bcaf-340">Cependant, cet appel s’inscrit dans le contexte d’un appel d’un client à une API web dans le service web.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-340">But that call comes in the context of a call from a client to a web API in the web service.</span></span> <span data-ttu-id="6bcaf-341">La demande « externe » du client au service web n’aboutit jamais si cette demande « interne » est rejetée.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-341">The "outer" request from the client to the web service never completes if this "inner" request is rejected.</span></span> <span data-ttu-id="6bcaf-342">De plus, la résolution de la requête avec l’objet `Error` personnalisé est obligatoire si l’émetteur de l’appel `http.get` doit communiquer les erreurs du point de terminaison OData au client.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-342">Also, resolving the request with the custom `Error` object is required if the caller of `http.get` needs to relay errors from the OData endpoint to the client.</span></span>

    ```javascript
    error = new Error();
    error.code = response.statusCode;
    error.message = response.statusMessage;
    
    // The error body sometimes includes an empty space
    // before the first character, remove it or it causes an error.
    body = body.trim();
    error.bodyCode = JSON.parse(body).error.code;
    error.bodyMessage = JSON.parse(body).error.message;
    resolve(error);
    ```

1. <span data-ttu-id="6bcaf-343">Enregistrez et fermez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-343">Save and close the file.</span></span>

## <a name="deploy-the-add-in"></a><span data-ttu-id="6bcaf-344">Déploiement du complément</span><span class="sxs-lookup"><span data-stu-id="6bcaf-344">Deploy the add-in</span></span>

<span data-ttu-id="6bcaf-345">Vous devez maintenant indiquer à Office où trouver le complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-345">Now you need to let Office know where to find the add-in.</span></span>

1. <span data-ttu-id="6bcaf-346">Créez un partage réseau, ou [partagez un dossier sur le réseau](https://technet.microsoft.com/en-us/library/cc770880.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bcaf-346">Create a network share, or [share a folder to the network](https://technet.microsoft.com/en-us/library/cc770880.aspx).</span></span>

2. <span data-ttu-id="6bcaf-347">Placez une copie du fichier manifeste Office-Add-in-NodeJS-SSO.xml, depuis la racine du projet, dans le dossier partagé.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-347">Place a copy of the Office-Add-in-NodeJS-SSO.xml manifest file, from the root of the project, into the shared folder.</span></span>

3. <span data-ttu-id="6bcaf-348">Lancez PowerPoint et ouvrez un document.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-348">Launch PowerPoint and open a document.</span></span>

4. <span data-ttu-id="6bcaf-349">Choisissez l’onglet **Fichier**, puis choisissez **Options**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-349">Choose the **File** tab, and then choose **Options**.</span></span>

5. <span data-ttu-id="6bcaf-350">Choisissez l’onglet **Fichier**, puis choisissez **Options**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-350">Choose **Trust Center**, and then choose the **Trust Center Settings** button.</span></span>

6. <span data-ttu-id="6bcaf-351">Choisissez **Catalogues de compléments approuvés**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-351">Choose **Trusted Add-ins Catalogs**.</span></span>

7. <span data-ttu-id="6bcaf-352">Dans le champ **URL du catalogue**, saisissez le chemin réseau permettant d’accéder au partage de dossier qui contient le fichier Office-Add-in-NodeJS-SSO.xml, puis sélectionnez **Ajouter un catalogue**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-352">In the **Catalog Url** field, enter the network path to the folder share that contains Office-Add-in-NodeJS-SSO.xml, and then choose **Add Catalog**.</span></span>

8. <span data-ttu-id="6bcaf-353">Activez la case à cocher **Afficher dans le menu**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-353">Select the **Show in Menu** check box, and then choose **OK**.</span></span>

9. <span data-ttu-id="6bcaf-p170">Un message vous informe que vos paramètres seront appliqués lors du prochain démarrage de Microsoft Office. Fermez PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p170">A message is displayed to inform you that your settings will be applied the next time you start Microsoft Office. Close PowerPoint.</span></span>

## <a name="build-and-run-the-project"></a><span data-ttu-id="6bcaf-356">Création et exécution du projet</span><span class="sxs-lookup"><span data-stu-id="6bcaf-356">Build and run the project</span></span>

<span data-ttu-id="6bcaf-p171">Il existe deux manières de créer et d’exécuter le projet selon que vous utilisez Visual Studio Code. Pour les deux façons, le projet est généré et reconstruit automatiquement, puis ré-exécuté lorsque vous apportez des modifications au code.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p171">There are two ways to build and run the project depending on whether you are using Visual Studio Code. For both ways, the project builds and automatically rebuilds and reruns when you make changes to the code.</span></span>

1. <span data-ttu-id="6bcaf-359">Si vous n’utilisez pas Visual Studio Code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-359">If you are not using Visual Studio Code:</span></span> 
 1. <span data-ttu-id="6bcaf-360">Ouvrez un terminal de nœud et accédez au dossier racine du projet.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-360">Open a node terminal and navigate to the root folder of the project.</span></span>
 2. <span data-ttu-id="6bcaf-361">Dans le terminal, entrez **npm run build**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-361">In the terminal, enter **npm run build**.</span></span> 
 3. <span data-ttu-id="6bcaf-362">Ouvrez un second terminal de nœud et accédez au dossier racine du projet.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-362">Open a second node terminal and navigate to the root folder of the project.</span></span>
 4. <span data-ttu-id="6bcaf-363">Dans le terminal, entrez **npm run start**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-363">In the terminal, enter **npm run start**.</span></span>

2. <span data-ttu-id="6bcaf-364">Si vous utilisez VS Code :</span><span class="sxs-lookup"><span data-stu-id="6bcaf-364">If you are using VS Code:</span></span>
 1. <span data-ttu-id="6bcaf-365">Ouvrez le projet dans VS Code.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-365">Open the project in VS Code.</span></span>
 2. <span data-ttu-id="6bcaf-366">Appuyez sur CTRL-MAJ-B pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-366">Press CTRL-SHIFT-B to build the project.</span></span>
 3. <span data-ttu-id="6bcaf-367">Appuyez sur F5 pour exécuter le projet dans une session de débogage.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-367">Press F5 to run the project in a debugging session.</span></span>


## <a name="add-the-add-in-to-an-office-document"></a><span data-ttu-id="6bcaf-368">Ajouter le complément à un document Office</span><span class="sxs-lookup"><span data-stu-id="6bcaf-368">Add the add-in to an Office document</span></span>

1. <span data-ttu-id="6bcaf-369">Redémarrez PowerPoint et ouvrez ou créez une présentation.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-369">Restart PowerPoint and open or create a presentation.</span></span> 

2. <span data-ttu-id="6bcaf-370">Dans l’onglet **Développeur** de PowerPoint, choisissez **Mes compléments**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-370">On the **Developer** tab in PowerPoint, choose **My Add-ins**.</span></span>

3. <span data-ttu-id="6bcaf-371">Sélectionnez l’onglet **DOSSIER PARTAGÉ**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-371">Select the **SHARED FOLDER** tab.</span></span>

4. <span data-ttu-id="6bcaf-372">Choisissez **Échantillon SSO NodeJS**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-372">Choose **SSO NodeJS Sample**, and then select **OK**.</span></span>

5. <span data-ttu-id="6bcaf-373">Dans le ruban **Accueil**, un nouveau groupe appelé **SSO NodeJS** apparaît avec un bouton intitulé **Afficher le complément** et une icône.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-373">On the **Home** ribbon is a new group called **SSO NodeJS** with a button labeled **Show Add-in** and an icon.</span></span> 

## <a name="test-the-add-in"></a><span data-ttu-id="6bcaf-374">Test du complément</span><span class="sxs-lookup"><span data-stu-id="6bcaf-374">Test the add-in</span></span>

1. <span data-ttu-id="6bcaf-375">Assurez-vous que vous disposez de fichiers dans votre espace OneDrive afin de pouvoir vérifier les résultats.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-375">Ensure that you have some files in your OneDrive so that you can verify the results.</span></span>

2. <span data-ttu-id="6bcaf-376">Cliquez sur le bouton **Afficher le complément** pour ouvrir le complément.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-376">Click **Show Add-in** button to open the add-in.</span></span>

2. <span data-ttu-id="6bcaf-p172">Le complément s’ouvre avec une page d’accueil. Cliquez sur le bouton **Obtenir mes fichiers à partir de OneDrive**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p172">The add-in opens with a Welcome page. Click the **Get My Files from OneDrive** button.</span></span>

2. <span data-ttu-id="6bcaf-p173">Si vous êtes connecté à Office, une liste de vos fichiers et dossiers sur OneDrive apparaîtront en dessous du bouton. La première fois, l’opération peut prendre plus de 15 secondes.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p173">If you are are signed into Office, a list of your files and folders on OneDrive will appear below the button. This may take more than 15 seconds the first time.</span></span>

3. <span data-ttu-id="6bcaf-p174">Si vous n’êtes pas connecté à Office, une fenêtre contextuelle s’ouvre et vous invite à vous connecter. Une fois que vous êtes connecté, la liste de vos fichiers et dossiers s’affiche après quelques secondes. *Vous n’appuyez pas sur le bouton une deuxième fois.*</span><span class="sxs-lookup"><span data-stu-id="6bcaf-p174">If you are not signed into Office, a popup will open and prompt you to sign in. After you have completed the sign-in, the list of your files and folders will appear after a few seconds. *You do not press the button a second time.*</span></span>

> [!NOTE]
> <span data-ttu-id="6bcaf-384">Si vous étiez précédemment connecté à Office avec un ID différent, et si certaines applications Office sont toujours ouvertes, Office ne changera pas systématiquement votre identifiant même s’il semble l’avoir fait dans PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-384">If you were previously signed on to Office with a different ID, and some Office applications that were open at the time are still open, Office may not reliably change your ID even if it appears to have done so in PowerPoint.</span></span> <span data-ttu-id="6bcaf-385">Dans ce cas, l’appel vers Microsoft Graph peut échouer, ou des données de l’ID précédent peuvent être renvoyées.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-385">If this happens, the call to Microsoft Graph may fail or data from the previous ID may be returned.</span></span> <span data-ttu-id="6bcaf-386">Afin d’éviter ce problème, veillez à *fermer toutes les autres applications Office* avant de cliquer sur **Obtenir mes fichiers à partir de OneDrive**.</span><span class="sxs-lookup"><span data-stu-id="6bcaf-386">To prevent this, be sure to *close all other Office applications* before you press **Get My Files from OneDrive**.</span></span>