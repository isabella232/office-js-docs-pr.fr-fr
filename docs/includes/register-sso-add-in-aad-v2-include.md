

1. <span data-ttu-id="6dd3d-101">Aller vers [https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6dd3d-101">Navigate to [https://apps.dev.microsoft.com/](https://apps.dev.microsoft.com)</span></span>

1. <span data-ttu-id="6dd3d-p101">Connectez-vous avec les informations d’identification d’administrateur à votre client Office 365. Par exemple, MyName@contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="6dd3d-p101">Sign-in with the admin credentials to your Office 365 tenancy. For example, MyName@contoso.onmicrosoft.com</span></span>

1. <span data-ttu-id="6dd3d-104">Cliquez sur **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-104">Click **Add an app**.</span></span>

1. <span data-ttu-id="6dd3d-105">Lorsque vous y êtes invité, entrez **$ADD-IN-NAME$** comme nom de l'application, puis appuyez sur **Créez l'application**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-105">When prompted, use “Office-Add-in-ASPNET-SSO” as the app name, and then press Create application.</span></span>

1. <span data-ttu-id="6dd3d-p102">Quand la page de configuration de l’application s’ouvre, copiez **l'ID de l’application** et enregistrez-le. Vous l’utiliserez dans une procédure ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-p102">When the configuration page for the app opens, copy the **Application Id** and save it. You'll use it in a later procedure.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6dd3d-p103">Cet ID est la valeur « audience » lorsque d’autres applications, telles que l’application hôte Office (par exemple, PowerPoint, Word, Excel) recherchent un accès autorisé à l’application. Il s’agit également de l’« ID client » de l’application dès que celle-ci recherche un accès autorisé à Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-p103">This ID is the “audience” value when other applications, such as the Office host application (e.g., PowerPoint, Word, Excel), seek authorized access to the application. It is also the “client ID” of the application when it, in turn, seeks authorized access to Microsoft Graph.</span></span>

1. <span data-ttu-id="6dd3d-p104">Dans la section **Secrets de l’application**, appuyez sur **Générer un nouveau mot de passe**. Une boîte de dialogue contextuelle s’ouvre avec un nouveau mot de passe (également appelé « secret de l’application »). *Copiez le mot de passe immédiatement et enregistrez-le avec l’ID de l’application.* Vous en aurez besoin dans une procédure ultérieure. Ensuite, fermez la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-p104">In the **Application Secrets** section, press **Generate New Password**. A popup dialog opens with a new password (also called an “app secret”) displayed. *Copy the password immediately and save it with the application ID.* You'll need it in a later procedure. Then close the dialog.</span></span>

1. <span data-ttu-id="6dd3d-115">Dans la section **Plateformes**, cliquez sur **Ajouter une plateforme**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-115">In the **Platforms** section, click **Add Platform**.</span></span>

1. <span data-ttu-id="6dd3d-116">Dans la boîte de dialogue qui s’ouvre, sélectionnez **API Web**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-116">In the dialog that opens, select **Web API**.</span></span>

1. <span data-ttu-id="6dd3d-117">L'URl **de l'ID de l'application** est génée à partir du for mulaire “api://$App ID GUID$”.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-117">An **Application ID URI** has been generated of the form “api://$App ID GUID$”.</span></span> <span data-ttu-id="6dd3d-118">Insérez le **$FQDN-SANS-PROTOCOLE$** (avec une barre oblique de division (/) ajoutée à la fin) entre deux barres obliques de division et le GUID.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-118">Insert the **$FQDN-WITHOUT-PROTOCOL$** (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="6dd3d-119">L'identifiant complet doit avoir la forme `api://$FQDN-WITHOUT-PROTOCOL$/$App ID GUID$` ; par exemple `api://localhost:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-119">The entire ID should have the form `api://$FQDN-WITHOUT-PROTOCOL$/$App ID GUID$`; for example `api://localhost:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6dd3d-120">Si vous obtenez une erreur indiquant que le domaine est déjà possédé, mais que vous le possédez, suivez la procédure [Quickstart: Ajouter un nom de domaine personnalisé à Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/add-custom-domain) pour l'enregistrer, puis répétez cette étape.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-120">If you get an error saying that the domain is already owned, but you own it, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/add-custom-domain) to register it, and then repeat this step.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6dd3d-121">La partie domaine du nom de **l'Étendue** situé juste en dessous de **l'URI de l'ID de l'application** changera automatiquement pour s'adapter, avec `/access_as_user` ajouté à la fin ; par exemple, `api://localhost:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-121">The domain part of the **Scope** name just below the **Application ID URI** will automatically change to match.</span></span>

1. <span data-ttu-id="6dd3d-122">Dans la section **Applications pré-autorisées,** identifiez les applications que vous souhaitez autoriser dans l’application web de votre complément.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-122">In the **Pre-authorized applications** section, you identify the applications that you want to authorize to your add-in's web application.</span></span> <span data-ttu-id="6dd3d-123">Chacun des ID suivants doit être pré-autorisé.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-123">Each of the following IDs needs to be pre-authorized.</span></span> <span data-ttu-id="6dd3d-124">Chaque fois que vous en entrez un, une nouvelle zone de texte vide s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-124">Each time you enter one, a new empty textbox appears.</span></span> <span data-ttu-id="6dd3d-125">(Entrez uniquement le GUID.)</span><span class="sxs-lookup"><span data-stu-id="6dd3d-125">(Enter only the GUID.)</span></span>
    * <span data-ttu-id="6dd3d-126">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span><span class="sxs-lookup"><span data-stu-id="6dd3d-126">`d3590ed6-52b3-4102-aeff-aad2292ab01c` (Microsoft Office)</span></span>
    * <span data-ttu-id="6dd3d-127">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office Online)</span><span class="sxs-lookup"><span data-stu-id="6dd3d-127">`57fb890c-0dab-4253-a5e0-7188c88b2bb4` (Office Online)</span></span>
    * <span data-ttu-id="6dd3d-128">`bc59ab01-8403-45c6-8796-ac3ef710b3e3` (Office Online)</span><span class="sxs-lookup"><span data-stu-id="6dd3d-128">`bc59ab01-8403-45c6-8796-ac3ef710b3e3` (Office Online)</span></span>

1. <span data-ttu-id="6dd3d-129">Ouvrez le menu déroulant **Scope** à côté de chaque **ID d’application** et activez la case à cocher pour `api://$FQDN-WITHOUT-PROTOCOL$/$App ID GUID$/access_as_user`.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-129">Open the **Scope** drop-down beside each **Application ID** and check the box for `api://$FQDN-WITHOUT-PROTOCOL$/$App ID GUID$/access_as_user`.</span></span>

1. <span data-ttu-id="6dd3d-130">En haut de la section **Plateformes**, cliquez sur **Ajouter une plateforme** à nouveau, puis sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-130">Near the top of the **Platforms** section, click **Add Platform** again and select **Web**.</span></span>

1. <span data-ttu-id="6dd3d-131">Dans la nouvelle section **Web** sous **Plateformes**, entrez les informations suivantes en guise d’**URL de redirection** : `https://$FQDN-WITHOUT-PROTOCOL$`.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-131">In the new **Web** section under **Platforms**, enter the following as a **Redirect URL**: `https://$FQDN-WITHOUT-PROTOCOL$`.</span></span>

1. <span data-ttu-id="6dd3d-p107">Faites défiler jusqu’à la section **Autorisations pour Microsoft Graph** et à la sous-section **Autorisations déléguées**. Utilisez le bouton **Ajouter** pour ouvrir une boîte de dialogue **Sélectionner des autorisations**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-p107">Scroll down to the **Microsoft Graph Permissions** section, the **Delegated Permissions** subsection. Use the **Add** button to open a **Select Permissions** dialog.</span></span>

1. <span data-ttu-id="6dd3d-134">Dans la boîte de dialogue, cochez les cases pour `profile` et toutes les autres autorisations AAD et Microsoft Graph dont votre complément a besoin.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-134">In the dialog box, check the boxes for `profile` and any other AAD and Microsoft Graph permissions that your add-in needs.</span></span> <span data-ttu-id="6dd3d-135">Les éléments suivants en sont des exemples :</span><span class="sxs-lookup"><span data-stu-id="6dd3d-135">The following are examples:</span></span>

    * <span data-ttu-id="6dd3d-136">Files.Read.All</span><span class="sxs-lookup"><span data-stu-id="6dd3d-136">Files.Read.All</span></span>
    * <span data-ttu-id="6dd3d-137">offline_access</span><span class="sxs-lookup"><span data-stu-id="6dd3d-137">offline_access</span></span>
    * <span data-ttu-id="6dd3d-138">openid</span><span class="sxs-lookup"><span data-stu-id="6dd3d-138">openid</span></span>
    * <span data-ttu-id="6dd3d-139">profil</span><span class="sxs-lookup"><span data-stu-id="6dd3d-139">profile</span></span>

    > [!NOTE]
    > <span data-ttu-id="6dd3d-140">L’autorisation `User.Read` est peut-être déjà répertoriée par défaut.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-140">The `User.Read` permission may already be listed by default.</span></span> <span data-ttu-id="6dd3d-141">Il est conseillé de ne pas demander d'autorisation qui ne sont pas nécessaires. Ainsi, nous vous recommandons de décocher la case pour cette autorisation si votre complément n'en a pas réellement besoin.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-141">It is a good practice not to ask for permissions that are not needed, so we recommend that you uncheck the box for this permission.</span></span>

1. <span data-ttu-id="6dd3d-142">Au bas de la boîte de dialogue, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-142">At the bottom of the dialog, click **OK**.</span></span>

1. <span data-ttu-id="6dd3d-143">Au bas de la page d’inscription, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6dd3d-143">At the bottom of the registration page, click **Save**.</span></span>