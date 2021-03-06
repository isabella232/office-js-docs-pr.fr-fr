---
title: Office UI Fabric dans des compléments Office
description: Découvrez comment utiliser les composants d’Office UI Fabric dans des compléments Office.
ms.date: 10/29/2020
localization_priority: Normal
ms.openlocfilehash: c4a13c615fe63183f595e24895b9fe6054fdc05d
ms.sourcegitcommit: ca66ff7462bfdf4ed7ae04f43d1388c24de63bf9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2020
ms.locfileid: "48996374"
---
# <a name="office-ui-fabric-in-office-add-ins"></a>Office UI Fabric dans des compléments Office

Office UI Fabric est une infrastructure frontale JavaScript permettant de créer des expériences pour Office et Office 365. Fabric propose des composants axés sur des visuels que vous pouvez étendre, retravailler et utiliser dans votre complément Office. Fabric utilisant le langage de création d’Office, ses composants d’expérience utilisateur ressemblent à une extension naturelle d’Office.

Si vous créez un complément, nous vous encourageons à utiliser Office UI Fabric pour mettre au point l’expérience utilisateur. L’utilisation d’Office UI Fabric est facultative.

Les sections suivantes expliquent comment commencer à utiliser Fabric en fonction de vos besoins.

## <a name="use-fabric-core-icons-fonts-colors"></a>Utiliser Fabric Core : icônes, polices, couleurs

Fabric Core contient les principaux éléments du langage de création tels que les icônes, les couleurs, le type et la grille. Fabric Core n’est pas dépendant de l’infrastructure. Fabric Core est utilisé par et inclus avec Fabric React.

Pour commencer à utiliser Fabric Core:

1. Ajoutez la référence CDN au code HTML sur votre page.  

    ```html
    <link rel="stylesheet" href="https://static2.sharepointonline.com/files/fabric/office-ui-fabric-core/9.6.1/css/fabric.min.css">
    ```

2. Utilisez les polices et les icônes Fabric.

    Pour utiliser une icône Fabric, incluez l’élément « i » sur votre page, puis référencez les classes appropriées. Vous pouvez contrôler la taille de l’icône en modifiant la taille de police. Par exemple, le code suivant montre comment créer une icône de tableau extra large qui utilise la couleur themePrimary (#0078d7).

    ```html
    <i class="ms-Icon ms-font-xl ms-Icon--Table ms-fontColor-themePrimary"></i>
    ```

    Pour rechercher des icônes supplémentaires disponibles dans Office UI Fabric, utilisez la fonctionnalité de recherche de la page [Icônes](https://developer.microsoft.com/fabric#/styles/icons). Lorsque vous trouvez une icône à utiliser dans votre complément, veillez à précéder le nom de l’icône de `ms-Icon--`.

    Pour plus d’informations sur les tailles de police et les couleurs disponibles dans Office UI Fabric, voir [Typographie](https://developer.microsoft.com/fabric#/styles/typography) et [Couleurs](https://developer.microsoft.com/fabric#/styles/colors).

## <a name="use-fabric-components"></a>Utiliser les composants Fabric

Fabric fournit un grand nombre de composants d’expérience utilisateur que vous pouvez utiliser pour créer votre complément. Nous ne prévoyons pas que tous les composants de fabric seront utilisés par un seul complément. Déterminez les meilleurs composants pour votre scénario et l’expérience utilisateur (par exemple, il peut être difficile d’afficher correctement une barre de [navigation](https://developer.microsoft.com/fabric#/components/breadcrumb) dans le volet Office).

Voici une liste de [composants d’expérience utilisateur Fabric REACT](https://developer.microsoft.com/fluentui#/controls/web) courants que nous vous recommandons d’utiliser dans un complément :

- [Bouton](https://developer.microsoft.com/fabric#/components/button)
- [Case à cocher](https://developer.microsoft.com/fabric#/components/checkbox)
- [ChoiceGroup](https://developer.microsoft.com/fabric#/components/choicegroup)
- [Liste déroulante](https://developer.microsoft.com/fabric#/components/dropdown)
- [Étiquette](https://developer.microsoft.com/fabric#/components/label)
- [Liste](https://developer.microsoft.com/fabric#/components/list)
- [Tableau croisé dynamique](https://developer.microsoft.com/fabric#/components/pivot)
- [TextField](https://developer.microsoft.com/fabric#/components/textfield)
- [Bouton bascule](https://developer.microsoft.com/fabric#/components/toggle)

Vous pouvez utiliser différentes infrastructures JavaScript, comme Angular ou React, pour créer votre complément. Pour commencer à utiliser les composants Fabric avec votre infrastructure, consultez les ressources suivantes.

|**Infrastructure**|**Exemple**|
|:------------|:----------|
|**React**|[Utilisation d’Office UI Fabric React dans des compléments Office](using-office-ui-fabric-react.md )|
|**Angular**| [Envisagez d’emballer les composants de fabric avec des composants 2](../develop/add-ins-with-angular2.md#consider-wrapping-fabric-components-with-angular-components)|
