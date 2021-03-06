---
title: Modèles de navigation pour les compléments Office
description: Découvrez les meilleures pratiques pour l’utilisation des barres de commandes, des barres d’onglets et des boutons de retour, pour concevoir la navigation d’un complément Office.
ms.date: 06/26/2018
localization_priority: Normal
ms.openlocfilehash: 812b56edc0653812c3519735a7300e5f3d7b38a6
ms.sourcegitcommit: be23b68eb661015508797333915b44381dd29bdb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/08/2020
ms.locfileid: "44608508"
---
# <a name="navigation-patterns"></a>Modèles de navigation

Les principales fonctionnalités d’un complément sont accessibles via les types de commande spécifique et la zone de l’écran limitée. Il est important que la navigation soit intuitive, fournisse du contexte et permette à l’utilisateur de se déplacer facilement au sein du complément.

## <a name="best-practices"></a>Meilleures pratiques

| À faire    | À ne pas faire |
| :---- | :---- |
| Vérifiez que l’utilisateur dispose d’une option de navigation clairement visible. | Ne compliquez pas le processus de navigation en utilisant des éléments d’interface utilisateur non standard.
| Servez-vous des composants suivants le cas échéant pour permettre aux utilisateurs de parcourir le complément. | N’ajoutez pas de difficultés qui empêcherait l’utilisateur de savoir où il se trouve ou de comprendre le contexte au sein du complément



## <a name="command-bar"></a>Barre de commandes

CommandBar est une surface qui héberge les commandes qui fonctionnent sur le contenu de la fenêtre, du panneau de configuration ou de la région parent située au-dessous. Exemples de fonctionnalités facultatives : point d’accès au menu « hamburger », recherche et commandes sur le côté.

![Commandes – spécifications pour le volet Office du bureau](../images/add-in-command-bar.png)



## <a name="tab-bar"></a>Barre d’onglets

Affiche la navigation à l’aide de boutons avec du texte et des icônes empilés verticalement. Utilisez la barre d’onglets pour permettre la navigation à l’aide des onglets avec des titres courts et explicites.

![Barre d’onglets – spécifications pour le volet Office du bureau](../images/add-in-tab-bar.png)


## <a name="back-button"></a>Bouton Précédent

Le bouton Précédent permet aux utilisateurs de revenir en arrière après avoir navigué dans l’interface. Ce modèle permet de vous assurer que les utilisateurs suivent une série d’étapes ordonnées.  

![Bouton Précédent – spécifications pour le volet Office du bureau](../images/add-in-back-button.png)
