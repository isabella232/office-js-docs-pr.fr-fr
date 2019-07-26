---
title: Ensemble de conditions requises de l’API JavaScript pour Word 1,2
description: Détails sur l’ensemble de conditions requises WordApi 1,2
ms.date: 07/17/2019
ms.prod: word
localization_priority: Normal
ms.openlocfilehash: c6244b7ce9ff7b5cbde68baad26e60a6326199d8
ms.sourcegitcommit: 6d9b4820a62a914c50cef13af8b80ce626034c26
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/19/2019
ms.locfileid: "35804705"
---
# <a name="whats-new-in-word-javascript-api-12"></a>Nouveautés de l’API JavaScript 1.2 pour Word

WordApi 1,2 Ajout de la prise en charge des images insérées.

## <a name="api-list"></a>Liste des API

Le tableau suivant répertorie les API ajoutées dans le cadre de l’ensemble de conditions requises WordApi 1,2.

| Class | Champs | Description |
|:---|:---|:---|
|[Body](/javascript/api/word/word.body)|[insertInlinePictureFromBase64 (base64EncodedImage: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.body#insertinlinepicturefrombase64-base64encodedimage--insertlocation-)|Insère une image dans le corps à l’emplacement spécifié. La valeur insertLocation peut être « Start » (début) ou « End » (fin).|
|[ContentControl](/javascript/api/word/word.contentcontrol)|[insertInlinePictureFromBase64 (base64EncodedImage: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.contentcontrol#insertinlinepicturefrombase64-base64encodedimage--insertlocation-)|Insère une image incluse dans le contrôle de contenu, à l’emplacement spécifié. La valeur insertLocation peut être « Replace » (remplacer), « Start » (début) ou « End » (fin).|
|[InlinePicture](/javascript/api/word/word.inlinepicture)|[delete()](/javascript/api/word/word.inlinepicture#delete--)|Supprime l’image insérée du document.|
||[insertBreak (breakType: Word. BreakType, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#insertbreak-breaktype--insertlocation-)|Insère un saut à l’emplacement spécifié du document principal. La valeur insertLocation peut être définie sur « Before » (avant) ou « After » (après).|
||[insertFileFromBase64 (base64File: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#insertfilefrombase64-base64file--insertlocation-)|Insère un document à l’emplacement spécifié. La valeur insertLocation peut être définie sur « Before » (avant) ou « After » (après).|
||[insertHtml (HTML: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#inserthtml-html--insertlocation-)|Insère du code HTML à l’emplacement spécifié. La valeur insertLocation peut être définie sur « Before » (avant) ou « After » (après).|
||[insertInlinePictureFromBase64 (base64EncodedImage: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#insertinlinepicturefrombase64-base64encodedimage--insertlocation-)|Insère une image insérée à l’emplacement spécifié. La valeur insertLocation peut être «Replace», «Before» ou «after».|
||[insertOoxml (OOXML: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#insertooxml-ooxml--insertlocation-)|Insère du code OOXML à l’emplacement spécifié.  La valeur insertLocation peut être définie sur « Before » (avant) ou « After » (après).|
||[insertParagraph (paragraphText: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#insertparagraph-paragraphtext--insertlocation-)|Insère un paragraphe à l’emplacement spécifié. La valeur insertLocation peut être définie sur « Before » (avant) ou « After » (après).|
||[insertText (Text: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.inlinepicture#inserttext-text--insertlocation-)|Insère du texte à l’emplacement spécifié. La valeur insertLocation peut être définie sur « Before » (avant) ou « After » (après).|
||[paragraph](/javascript/api/word/word.inlinepicture#paragraph)|Obtient le paragraphe parent qui contient l’image insérée. En lecture seule.|
||[Select (selectionMode?: Word. SelectionMode)](/javascript/api/word/word.inlinepicture#select-selectionmode-)|Sélectionne l’image insérée. Word fait défiler le document jusqu’à accéder à la sélection.|
|[Range](/javascript/api/word/word.range)|[insertInlinePictureFromBase64 (base64EncodedImage: chaîne, insertLocation: Word. InsertLocation)](/javascript/api/word/word.range#insertinlinepicturefrombase64-base64encodedimage--insertlocation-)|Insère une image à l’emplacement spécifié. La valeur insertLocation peut être «Replace», «Start», «end», «Before» ou «after».|
||[inlinePictures](/javascript/api/word/word.range#inlinepictures)|Obtient la collection d’objets image insérée de la plage. En lecture seule.|

## <a name="see-also"></a>Voir aussi

- [Documentation de référence de l’API JavaScript pour Word](/javascript/api/word)
- [Ensembles de conditions requises de l’API JavaScript pour Word](word-api-requirement-sets.md)