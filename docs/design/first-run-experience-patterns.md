---
title: Modèles de première expérience d’utilisation des complément Office
description: Découvrez les meilleures pratiques pour la conception d’expériences de première exécution dans des compléments Office.
ms.date: 06/26/2018
localization_priority: Normal
ms.openlocfilehash: c0528e869dd8ee7fe779785fb1a9b6d347deab75
ms.sourcegitcommit: 9609bd5b4982cdaa2ea7637709a78a45835ffb19
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2020
ms.locfileid: "47292952"
---
# <a name="first-run-experience-patterns"></a>Modèles de première expérience d’utilisation

Une première expérience d’utilisation (FRE) correspond à l’introduction d’un utilisateur à votre complément. Une FRE existe quand un utilisateur ouvre un complément pour la première fois et lui fournit des informations sur les fonctions, les fonctionnalités et/ou les avantages du complément. Cette expérience vous permet de modeler la première impression qu’un utilisateur va avoir d’un complément. Elle peut grandement influencer la probabilité qu’il y revienne et continue à utiliser votre complément...

## <a name="best-practices"></a>Meilleures pratiques


Suivez ces meilleures pratiques lors de la personnalisation de la première expérience d’utilisation :

|À faire|À ne pas faire|
|:------|:------|
|Proposer une simple et courte introduction aux actions principales disponibles dans le complément. | Ne pas inclure des informations et des détails qui ne sont pas pertinents pour la prise en main.
|Donner aux utilisateurs la possibilité d’effectuer une action qui aura un impact positif sur leur utilisation du complément. | Ne pas espérer que les utilisateurs découvrent tous les éléments en même temps. Concentrer les efforts sur le type ’action qui fournit le meilleur rendement.
|Créer une expérience utilisateur attrayante que les utilisateurs vont vouloir compléter. | Ne pas forcer les utilisateurs à parcourir toute l’expérience de première utilisation. Donner aux utilisateurs une option leur permettant d’ignorer l’expérience de première exécution. |



Déterminer s’il convient de montrer l’expérience de première utilisation une fois ou plusieurs fois (tout dépend de son importance pour votre scénario). Par exemple, si votre complément est uniquement utilisé de temps en temps, les utilisateurs peuvent devenir moins familiarisés avec le complément. Ils pourraient alors bénéficier d’une autre interaction avec l’expérience de première exécution.



Appliquer les modèles suivants le cas échéant pour créer ou optimisez l’expérience de première exécution de votre complément.



## <a name="carousel"></a>Carrousel


Le carrousel présente aux utilisateurs une série de fonctionnalités ou d’informations avant qu’ils ne commencent à utiliser le complément.

*Figure 1 : autoriser les utilisateurs à avancer ou à ignorer les pages de début du flux de carrousel.* 
 ![ Première exécution : étape 1 : spécifications pour le volet Office du Bureau](../images/add-in-FRE-step-1.png)



*Figure 2 : réduisez le nombre de filtres de carrousel que vous présentez à l’utilisateur uniquement en fonction de ce qui est nécessaire pour communiquer efficacement votre message.* 
 ![ Première exécution : étape 2 : spécifications pour le volet Office du Bureau](../images/add-in-FRE-step-2.png)


*Figure 3 : fournissez un appel à l’action clair pour quitter la première exécution.* 
 ![ Première exécution : étape 3-Spécifications pour le volet Office du Bureau](../images/add-in-FRE-step-3.png)



## <a name="value-placemat"></a>Mise en place de la valeur

La mise en place de la valeur communique la proposition de valeur de votre complément en faisant appel au positionnement de votre logo, à une proposition de valeur clairement déclarée, à une présentation ou un résumé des fonctionnalités et à une fonctionnalité claire d’appel à l’action.



![First Run-value-valeur de présentation-spécifications pour le volet Office du Bureau ](../images/add-in-FRE-value.png)
 *une valeur de récapitulatif, une proposition de valeur claire, un résumé des fonctionnalités et un appel à l’action.*


### <a name="video-placemat"></a>Mise en place vidéo

La mise en place vidéo montre une vidéo aux utilisateurs avant qu’ils ne commencent à utiliser votre complément.


*Figure 1 : récapitulatif de la première exécution : l’écran contient une image fixe de la vidéo avec un bouton de lecture et un bouton d’appel à l’action en clair.* 
 ![ Carte de redirection vidéo-spécifications pour le volet Office du Bureau](../images/add-in-FRE-video.png)



*Figure 2 : lecteur vidéo : les utilisateurs disposent d’une vidéo dans une fenêtre de dialogue.* 
 ![ Carte de redirection vidéo-boîte de dialogue-spécifications pour le volet Office du Bureau](../images/add-in-FRE-video-dialog.png)
