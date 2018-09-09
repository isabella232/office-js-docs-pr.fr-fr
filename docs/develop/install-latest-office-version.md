---
title: Installer la dernière version d’Office 2016
description: ''
ms.date: 12/04/2017
ms.openlocfilehash: 98dc69a7971a94b96bc3f7304fc7905f31013a87
ms.sourcegitcommit: 4de2a1b62ccaa8e51982e95537fc9f52c0c5e687
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/10/2018
ms.locfileid: "22925233"
---
# <a name="install-the-latest-version-of-office-2016"></a>Installer la dernière version d’Office 2016

De nouvelles fonctionnalités de développeur, y compris celles en version d’évaluation, sont mises à la disposition des abonnés qui souhaitent obtenir les dernières versions d’Office. 

## <a name="opt-in-to-getting-the-latest-builds"></a>Inscription pour l’obtention des versions les plus récentes

Pour s’inscrire afin d’obtenir les dernières versions d’Office 2016, procédez comme suit : 

- Si vous êtes abonné à Office 365 Famille, Personnel ou Université, consultez la page [Participez au programme Office Insider](https://products.office.com/office-insider).
- Si vous êtes un client d’Office 365 pour les entreprises, consultez l’article [Installer la version First Release pour Office 365 pour les entreprises](https://support.office.com/article/Install-the-First-Release-build-for-Office-365-for-business-customers-4dd8ba40-73c0-4468-b778-c7b744d03ead).
- Si vous exécutez Office 2016 sur un Mac :
    - Démarrez un programme Office 2016 pour Mac.
    - Sélectionnez **Vérifier les mises à jour** dans le menu Aide.
    - Dans la zone Mise à jour automatique Microsoft (AutoUpdate), cochez la case pour participer au programme Office Insider. 

## <a name="get-the-latest-build"></a>Obtention de la dernière version

Pour obtenir la dernière version d’Office 2016, procédez comme suit : 

1. Téléchargez l’[outil Déploiement d’Office 2016](https://www.microsoft.com/download/details.aspx?id=49117). 
2. Exécutez l’outil. Cette opération extrait les deux fichiers suivants : Setup.exe et configuration.xml.
3. Remplacez le fichier configuration.xml par le [fichier de configuration First Release](https://raw.githubusercontent.com/OfficeDev/Office-Add-in-Commands-Samples/master/Tools/FirstReleaseConfig/configuration.xml).
4. En tant qu’administrateur, exécutez la commande suivante : `setup.exe /configure configuration.xml` 

    > [!NOTE]
    > L’exécution de la commande peut durer plusieurs minutes sans vous en indiquer la progression.

Une fois le processus d’installation terminé, les dernières applications d’Office 2016 sont installées. Pour vérifier que la dernière version est bien installée, accédez à **Fichier**  >  **Compte** à partir de n’importe quelle application Office. Sous Mises à jour Office, vous verrez la mention (Office Insiders) au-dessus du numéro de version.

![Capture d’écran affichant les informations du produit avec la mention Office Insiders](../images/office-insiders.png)

## <a name="minimum-office-builds-for-office-javascript-api-requirement-sets"></a>Builds Office minimum pour les ensembles de conditions requises pour l’API JavaScript pour Office

Pour plus d’informations sur les versions minimum des produits pour chaque plate-forme pour les ensembles de conditions requises pour les API, voir les rubriques suivantes :

- [Ensembles de conditions requises de l’API JavaScript pour Word](https://dev.office.com/reference/add-ins/requirement-sets/word-api-requirement-sets)
- [Ensembles de conditions requises de l’API JavaScript pour Excel](https://dev.office.com/reference/add-ins/requirement-sets/excel-api-requirement-sets)
- [Ensembles de conditions requises de l’API JavaScript pour OneNote](https://dev.office.com/reference/add-ins/requirement-sets/onenote-api-requirement-sets)
- [Ensembles de conditions requises de l’API de boîte de dialogue](https://dev.office.com/reference/add-ins/requirement-sets/dialog-api-requirement-sets)
- [Ensembles de conditions requises des API communes pour Office](https://dev.office.com/reference/add-ins/requirement-sets/office-add-in-requirement-sets)