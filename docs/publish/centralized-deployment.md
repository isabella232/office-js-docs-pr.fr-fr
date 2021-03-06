---
title: Publier des compléments Office à l’aide du déploiement centralisé via le centre d’administration Microsoft 365
description: Découvrez comment utiliser le déploiement centralisé pour déployer des compléments internes ainsi que des compléments fournis par les éditeurs de logiciels indépendants.
ms.date: 07/07/2020
localization_priority: Normal
ms.openlocfilehash: e3f0bca5605d48d7b6c2ead49591546561dadffe
ms.sourcegitcommit: 4a03d8b3f676ee2d91114813cb81bce5da3c8d6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48175555"
---
# <a name="publish-office-add-ins-using-centralized-deployment-via-the-microsoft-365-admin-center"></a>Publier des compléments Office à l’aide du déploiement centralisé via le centre d’administration Microsoft 365

Le centre d’administration Microsoft 365 permet à un administrateur de déployer facilement des compléments Office pour les utilisateurs et les groupes au sein de leur organisation. Les compléments déployés via le centre d’administration sont disponibles pour les utilisateurs directement dans leurs applications Office, sans qu’aucune configuration client ne soit requise. Vous pouvez utiliser le déploiement centralisé pour déployer des compléments internes, ainsi que des compléments fournis par des éditeurs de logiciels indépendants.

Le centre d’administration Microsoft 365 prend actuellement en charge les scénarios suivants.

- Déploiement centralisé de nouveaux compléments et de ceux mis à jour pour des utilisateurs, des groupes ou une organisation.
- Déploiement sur plusieurs plateformes client, y compris Windows, Mac et le Web. Pour Outlook, le déploiement sur iOS et Android est également pris en charge. (Toutefois, pendant que l’installation utilisateur des compléments Excel, Outlook, Word et PowerPoint sur iPad est prise en charge, le déploiement centralisé sur iPad n’est **pas** pris en charge.)
- Déploiement en anglais et pour les clients du monde entier.
- Déploiement de compléments hébergés sur le cloud.
- Déploiement de compléments hébergés au sein d’un pare-feu.
- Déploiement de compléments AppSource.
- Installation automatique d’un complément pour les utilisateurs au lancement de l’application Office.
- Suppression automatique d’un complément pour les utilisateurs si l’administrateur désactive ou supprime le complément, ou si les utilisateurs sont supprimés d’Azure Active Directory ou d’un groupe auprès duquel le complément a été déployé.

Le déploiement centralisé est la méthode recommandée pour un administrateur Microsoft 365 pour déployer des compléments Office au sein d’une organisation, à condition que l’organisation remplisse toutes les conditions d’utilisation du déploiement centralisé. Pour plus d’informations sur la façon de déterminer si votre organisation peut utiliser un déploiement centralisé, consultez la rubrique [déterminer si un déploiement centralisé de compléments fonctionne pour votre organisation Microsoft 365](/office365/admin/manage/centralized-deployment-of-add-ins).

> [!NOTE]
> Dans un environnement local sans connexion à Microsoft 365 ou pour déployer des compléments SharePoint ou des compléments Office qui ciblent Office 2013, utilisez un [catalogue d’applications SharePoint](publish-task-pane-and-content-add-ins-to-an-add-in-catalog.md). Pour déployer des compléments COM/VSTO, utilisez ClickOnce ou Windows Installer, comme décrit dans la rubrique [Déploiement d’une solution Office](/visualstudio/vsto/deploying-an-office-solution).

## <a name="recommended-approach-for-deploying-office-add-ins"></a>Approche recommandée pour le déploiement des compléments Office

Envisagez de déployer des compléments Office dans une approche progressive pour vous assurer que le déploiement se déroule sans problème. Nous recommandons le plan suivant :

1. Déployez le complément auprès d’un petit groupe de parties prenantes et de membres du service informatique. Si le déploiement réussit, passez à l’étape 2.

2. Déployez le complément auprès d’un groupe plus important de membres dans l’organisation qui utilisera le complément. Si le déploiement réussit, passez à l’étape 3.

3. Déployez le complément auprès du groupe entier de membres qui utilisera le complément.

Selon la taille de l’audience cible, vous pouvez ajouter des étapes à cette procédure ou en supprimer.

## <a name="publish-an-office-add-in-via-centralized-deployment"></a>Publication d’un complément Office via le déploiement centralisé

Avant de commencer, vérifiez que votre organisation remplit toutes les conditions d’utilisation du déploiement centralisé, comme décrit dans la rubrique [déterminer si un déploiement centralisé de compléments fonctionne pour votre organisation Microsoft 365](/microsoft-365/admin/manage/centralized-deployment-of-add-ins).

Si votre organisation répond à toutes les conditions requises, procédez comme suit pour publier un complément Office via un déploiement centralisé :

1. Connectez-vous à Microsoft 365 avec votre compte professionnel ou scolaire.
2. Sélectionnez l’icône du lanceur d’applications située en haut à gauche et choisissez **Administrateur**.
3. Dans le menu de navigation, appuyez sur **Afficher plus**, puis choisissez **Paramètres** > **Services et compléments**.
4. Si vous voyez un message en haut de la page annonçant le nouveau centre d’administration Microsoft 365, sélectionnez le message pour accéder à la version d’évaluation du centre d’administration (voir [à propos du centre d’administration de microsoft 365](/microsoft-365/admin/admin-overview/about-the-admin-center)).
5. Choisissez **Déployer un complément** en haut de la page.
6. Choisissez **Suivant** après avoir consulté la configuration requise.
7. Dans la page **Déploiement centralisé**, choisissez l’une des options suivantes :

    - **Je veux ajouter un complément à partir de l’Office Store**.
    - **J’ai le fichier manifeste (.xml) sur cet appareil**. Pour cette option, sélectionnez **Parcourir** afin de recherche le fichier manifeste (.xml) que vous voulez utiliser.
    - **J’ai une URL pour le fichier manifeste**. Pour cette option, entrez l’URL du manifeste dans le champ disponible.

    ![Boîte de dialogue nouveau complément dans le centre d’administration Microsoft 365](../images/new-add-in.png)

8. Si vous avez sélectionné l’option d’ajout d’un complément à partir de l’Office Store, sélectionnez le complément. Vous pouvez afficher les compléments disponibles via l’une des catégories suivantes : **Suggestions**, **Évaluation** ou **Nom**. Vous ne pouvez ajouter que des compléments gratuits de l’Office Store. L’ajout de compléments payants n’est pas actuellement pris en charge.

    > [!NOTE]
    > Avec l’option Office Store, les mises à jour et améliorations du complément sont automatiquement disponibles pour les utilisateurs sans intervention de votre part.

    ![Sélection d’une boîte de dialogue de complément dans le centre d’administration Microsoft 365](../images/select-an-add-in.png)

9. Choisissez **Continuer** après avoir vérifié les détails du complément, la politique de confidentialité et les termes de la licence.

    ![Page de complément sélectionnée dans le centre d’administration Microsoft 365](../images/selected-add-in-admin-center.png)

10. Sur la **page attribuer des utilisateurs** , choisissez **tout le monde**, **utilisateurs/groupes spécifiques**ou **moi seul**. Utilisez la zone de recherche pour trouver les utilisateurs et groupes vers lesquels vous voulez déployer le complément. Pour les compléments Outlook, vous pouvez également choisir la méthode de déploiement **fixe**, **disponible**ou **facultative**.

    ![Gérer les personnes ayant accès et méthode de déploiement dans le centre d’administration Microsoft 365](../images/manage-users-deployment-admin-center.png)

    > [!NOTE]
    > Les compléments qui utilisent l' [authentification unique (SSO)](../develop/sso-in-office-add-ins.md) invitent l’administrateur à accepter les étendues figurant dans le manifeste du complément.  Si le même service de sauvegarde est utilisé sur plusieurs compléments (le même ID d’application Azure est utilisé avec l’authentification unique dans différents compléments), les étendues de chaque complément seront invitées à donner leur consentement à chaque déploiement. Cette page affiche également la liste des autorisations requises par le complément.

11. Lorsque vous avez terminé, choisissez **déployer**. Ce processus peut prendre jusqu’à trois minutes. Ensuite, terminez la procédure en appuyant sur **Suivant**. Votre complément apparaît à présent avec d’autres applications dans Office 365.

    > [!NOTE]
    > Lorsqu’un administrateur choisit **Deploy**, le consentement est donné pour tous les utilisateurs.

    ![Liste des applications dans le centre d’administration Microsoft 365](../images/citations.png)

> [!TIP]
> lorsque vous déployez un nouveau complément vers des utilisateurs et/ou des groupes de votre organisation, pensez à leur envoyer un courrier décrivant quand et comment utiliser le complément et incluez des liens vers un contenu pertinent de l’aide ou du forum aux questions, ou d’autres ressources de support.

## <a name="considerations-when-granting-access-to-an-add-in"></a>Éléments à prendre en compte lors de l’octroi de l’accès à un complément

Les administrateurs peuvent affecter un complément à tout le monde ou à des utilisateurs et/ou groupes spécifiques au sein de l’organisation. Chaque option a des conséquences spécifiques :

- **Tout le monde** : comme son nom l’indique, cette option affecte le complément à tous les utilisateurs du client. Utilisez-la avec parcimonie et uniquement pour les compléments qui sont réellement universels pour l’ensemble de votre organisation.

- **Utilisateurs** : si vous affectez un complément à un utilisateur particulier, vous devez mettre à jour les paramètres de déploiement centralisé pour le complément chaque fois que vous souhaitez l’affecter à des utilisateurs supplémentaires. De même, vous devez mettre à jour les paramètres de déploiement centralisé pour le complément chaque fois que vous souhaitez supprimer l’accès d’un utilisateur au complément.

- **Groupes** : si vous affectez un complément à un groupe, le complément est automatiquement affecté aux utilisateurs ajoutés au groupe. De même, quand un utilisateur est supprimé d’un groupe, il perd l’accès au complément. Dans les deux cas, aucune action supplémentaire n’est requise de la part de l’administrateur 365 de Microsoft.

En général, pour faciliter la maintenance, nous vous recommandons d’affecter des compléments à l’aide de groupes. Toutefois, dans les situations où vous souhaitez restreindre l’accès au complément à un très petit nombre d’utilisateurs, il peut être plus pratique d’affecter le complément à des utilisateurs spécifiques.

## <a name="add-in-states"></a>États de complément

Le tableau suivant décrit les différents états qui s’appliquent à un complément.

|État|Comment l’état se produit|Impact|
|-----|--------------------|------|
|**Actif**|Un administrateur a chargé le complément et l’a affecté à des utilisateurs et/ou groupes.|Les utilisateurs et/ou groupes auxquels le complément est affecté voient celui-ci dans les clients Office concernés.|
|**Désactivé**|Un administrateur a désactivé le complément.|Les utilisateurs et/ou groupes auxquels le complément est affecté ne peuvent plus y accéder. Si l’état du complément est modifié, passant de **Désactivé** à **Actif**, les utilisateurs et groupes y ont de nouveau accès.|
|**Deleted**|Un administrateur a supprimé le complément.|Les utilisateurs et/ou groupes auxquels le complément est affecté ne peuvent plus y accéder.|

## <a name="updating-office-add-ins-that-are-published-via-centralized-deployment"></a>Mise à jour des compléments Office publiés via un déploiement centralisé

Une fois qu’un complément Office a été publié via un déploiement centralisé, les modifications apportées à l’application web du complément sont automatiquement disponibles pour tous les utilisateurs dès qu’elles sont implémentées dans l’application web. Les modifications apportées au [fichier manifeste XML](../develop/add-in-manifests.md) d’un complément, par exemple, pour mettre à jour l’icône du complément, le texte ou les commandes du complément se produisent comme suit :

- **Complément métier**: si un administrateur a explicitement téléchargé un fichier manifeste lors de l’implémentation du déploiement centralisé via le centre d’administration Microsoft 365, l’administrateur doit télécharger un nouveau fichier manifeste qui contient les modifications souhaitées. Une fois que le fichier manifeste a été chargé, le complément est mis à jour au démarrage suivant des applications Office concernées.

  > [!NOTE]
  > Un administrateur n’a pas besoin de supprimer un complément LOB pour effectuer une mise à jour. Dans la section compléments, l’administrateur peut simplement choisir le complément LOB et appeler cette fonctionnalité en appuyant sur le bouton **mettre à jour le complément** présent dans le coin inférieur droit.
  > 
  > ![Capture d’écran illustrant la boîte de dialogue mettre à jour le complément dans le centre d’administration Microsoft 365](../images/update-add-in-admin-center.png)

- **Complément Office Store**: si un administrateur a sélectionné un complément à partir de l’Office Store lors de l’implémentation du déploiement centralisé via le centre d’administration Microsoft 365, et que le complément est mis à jour dans l’Office Store, le complément est mis à jour par la suite via un déploiement centralisé. Le complément est mis à jour au démarrage suivant des applications Office concernées.

## <a name="end-user-experience-with-add-ins"></a>Expérience des utilisateurs finaux avec les compléments

Une fois qu’un complément a été publié via un déploiement centralisé, les utilisateurs finaux peuvent commencer à l’utiliser sur toutes les plateformes prises en charge par le complément.

Si le complément prend en charge les commandes de complément, celles-ci apparaissent dans le ruban de l’application Office pour tous les utilisateurs vers lesquels le complément est déployé. Dans l’exemple suivant, la commande **Recherche de citation** apparaît dans le ruban pour le complément **Citations**.

![Capture d’écran illustrant une section du ruban d’application Office avec la commande de citation de recherche mise en surbrillance dans le complément citations](../images/search-citation.png)

Si le complément ne prend pas en charge les commandes de complément, les utilisateurs peuvent l’ajouter à leur application Office en procédant comme suit :

1. Dans Word 2016 ou version ultérieure, Excel 2016 ou version ultérieure ou PowerPoint 2016 ou version ultérieure, choisissez **Insertion** > **Mes compléments**.
2. Sélectionnez l’onglet **Géré par l’administrateur** dans la fenêtre du complément.
3. Choisissez le complément, puis **Ajouter**.

    ![Capture d’écran illustrant l’onglet Géré par l’administrateur de la page Compléments Office d’une application Office. Le complément Citations apparaît sur l’onglet.](../images/office-add-ins-admin-managed.png)

Toutefois, pour Outlook 2016 ou version ultérieure, les utilisateurs peuvent procéder comme suit :

1. Dans Outlook, Choisissez **Accueil** > **Store**.
2. Sélectionnez l’élément **Géré par l’administrateur** dans la fenêtre du complément.
3. Choisissez le complément, puis **Ajouter**.

    ![Capture d’écran montrant la zone Géré par l’administrateur de la page Store de l’application Outlook.](../images/outlook-add-ins-admin-managed.png)

## <a name="see-also"></a>Voir aussi

- [Déterminer si le déploiement centralisé des compléments fonctionne avec votre organisation Microsoft 365](/office365/admin/manage/centralized-deployment-of-add-ins)
