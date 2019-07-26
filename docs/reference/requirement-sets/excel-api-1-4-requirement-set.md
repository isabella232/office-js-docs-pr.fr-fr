---
title: Ensemble de conditions requises de l’API JavaScript pour Excel 1,44
description: Détails sur l’ensemble de conditions requises ExcelApi 1,4
ms.date: 07/15/2019
ms.prod: excel
localization_priority: Normal
ms.openlocfilehash: c0cd380a71c98ab63aa955ec0ff2ed005065577c
ms.sourcegitcommit: bb44c9694f88cde32ffbb642689130db44456964
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/17/2019
ms.locfileid: "35771980"
---
# <a name="whats-new-in-excel-javascript-api-14"></a>Nouveautés de l’API JavaScript 1.4 pour Excel

Les ajouts apportés aux API JavaScript pour Excel dans l’ensemble de conditions requises 1.4 sont présentés ci-dessous.

## <a name="named-item-add-and-new-properties"></a>Ajout d’élément nommé et nouvelles propriétés

Nouvelles propriétés :

* `comment`
* `scope`-Éléments de feuille de calcul ou d’étendue de classeur.
* `worksheet`-Renvoie la feuille de calcul dans laquelle l’élément nommé est inclus dans l’étendue.

Nouvelles méthodes :

* `add(name: string, reference: Range or string, comment: string)`-Ajoute un nouveau nom à la collection de l’étendue donnée.
* `addFormulaLocal(name: string, formula: string, comment: string)`-Ajoute un nouveau nom à la collection de l’étendue donnée à l’aide des paramètres régionaux de l’utilisateur pour la formule.

## <a name="settings-api-in-the-excel-namespace"></a>API Settings dans l’espace de noms Excel

L’objet [Setting](/javascript/api/excel/excel.setting) représente une paire clé-valeur d’un paramètre conservé dans le document. La fonctionnalité de `Excel.Setting` équivaut à `Office.Settings`, mais utilise la syntaxe d’API par lots plutôt que le modèle de rappel de l’API commune.

Les API `getItem()` incluent pour obtenir une entrée de paramètre via `add()` la clé et pour ajouter la paire de paramètre key: value spécifiée au classeur.

## <a name="others"></a>Autres

* Définissez le nom de la colonne de tableau.
* Ajouter une colonne de table à la fin du tableau.
* Ajouter plusieurs lignes à un tableau à la fois.
* `range.getColumnsAfter(count: number)` et `range.getColumnsBefore(count: number)` pour obtenir un certain nombre de colonnes à droite/gauche de l’objet de plage actuel.
* [Fonction Get Item ou null objet](../../excel/excel-add-ins-advanced-concepts.md#ornullobject-methods): cette fonctionnalité permet d’obtenir l’objet à l’aide d’une clé. Si l’objet n’existe pas, la propriété de `isNullObject` l’objet renvoyé est true. Cela permet aux développeurs de vérifier si un objet existe ou non sans qu’il soit nécessaire de le gérer par le biais de la gestion des exceptions. La `*OrNullObject` méthode est disponible pour la plupart des objets de collection.

```javascript
worksheet.getItemOrNullObject("itemName")
```

## <a name="api-list"></a>Liste des API

| Class | Champs | Description |
|:---|:---|:---|
|[BindingCollection](/javascript/api/excel/excel.bindingcollection)|[getCount()](/javascript/api/excel/excel.bindingcollection#getcount--)|Obtient le nombre de liaisons de la collection.|
||[getItemOrNullObject(id: string)](/javascript/api/excel/excel.bindingcollection#getitemornullobject-id-)|Obtient un objet de liaison par ID. Si l’objet de liaison n’existe pas, renvoie un objet null.|
|[ChartCollection](/javascript/api/excel/excel.chartcollection)|[getCount()](/javascript/api/excel/excel.chartcollection#getcount--)|Renvoie le nombre de graphiques dans la feuille de calcul.|
||[getItemOrNullObject(name: string)](/javascript/api/excel/excel.chartcollection#getitemornullobject-name-)|Extrait un graphique à l’aide de son nom. Si plusieurs graphiques portent le même nom, c’est le premier d’entre eux qui est renvoyé.|
|[ChartPointsCollection](/javascript/api/excel/excel.chartpointscollection)|[getCount()](/javascript/api/excel/excel.chartpointscollection#getcount--)|Renvoie le nombre de points de graphique dans la série.|
|[ChartSeriesCollection](/javascript/api/excel/excel.chartseriescollection)|[getCount()](/javascript/api/excel/excel.chartseriescollection#getcount--)|Renvoie le nombre de séries de la collection.|
|[NamedItem](/javascript/api/excel/excel.nameditem)|[comment](/javascript/api/excel/excel.nameditem#comment)|Représente le commentaire associé à ce nom.|
||[delete()](/javascript/api/excel/excel.nameditem#delete--)|Supprime le nom donné.|
||[getRangeOrNullObject()](/javascript/api/excel/excel.nameditem#getrangeornullobject--)|Renvoie l’objet de plage qui est associé au nom. Renvoie un objet null si le type de l’élément nommé n’est pas une plage.|
||[étendue](/javascript/api/excel/excel.nameditem#scope)|Indique si le nom est étendu au classeur ou à une feuille de calcul spécifique. Les valeurs possibles sont les suivantes: Worksheet, Workbook. En lecture seule.|
||[worksheet](/javascript/api/excel/excel.nameditem#worksheet)|Renvoie la feuille de calcul dans laquelle est inclus l’élément nommé. Renvoie une erreur si l’élément est inclus dans l’étendue du classeur.|
||[worksheetOrNullObject](/javascript/api/excel/excel.nameditem#worksheetornullobject)|Renvoie la feuille de calcul dans laquelle est inclus l’élément nommé. Renvoie un objet null si l’élément est inclus dans le classeur à la place.|
|[NamedItemCollection](/javascript/api/excel/excel.nameditemcollection)|[Add (Name: String, Reference: Range \| String, comment?: String)](/javascript/api/excel/excel.nameditemcollection#add-name--reference--comment-)|Ajoute un nouveau nom à la collection de l’étendue donnée.|
||[addFormulaLocal (Name: String, Formula: String, comment?: String)](/javascript/api/excel/excel.nameditemcollection#addformulalocal-name--formula--comment-)|Ajoute un nouveau nom à la collection de l’étendue donnée à l’aide des paramètres régionaux de l’utilisateur pour la formule.|
||[getCount()](/javascript/api/excel/excel.nameditemcollection#getcount--)|Obtient le nombre d’éléments nommés dans la collection.|
||[getItemOrNullObject(name: string)](/javascript/api/excel/excel.nameditemcollection#getitemornullobject-name-)|Obtient un objet NamedItem à l’aide de son nom. Si l’objet nameditem n’existe pas, renvoie un objet null.|
|[NamedItemCollectionLoadOptions](/javascript/api/excel/excel.nameditemcollectionloadoptions)|[comment](/javascript/api/excel/excel.nameditemcollectionloadoptions#comment)|Pour chaque élément de la collection: représente le commentaire associé à ce nom.|
||[étendue](/javascript/api/excel/excel.nameditemcollectionloadoptions#scope)|Pour chaque élément de la collection: indique si le nom est inclus dans le classeur ou dans une feuille de calcul spécifique. Les valeurs possibles sont les suivantes: Worksheet, Workbook. En lecture seule.|
||[worksheet](/javascript/api/excel/excel.nameditemcollectionloadoptions#worksheet)|Pour chaque élément de la collection: renvoie la feuille de calcul dans laquelle l’élément nommé est inclus dans l’étendue. Renvoie une erreur si l’élément est inclus dans l’étendue du classeur.|
||[worksheetOrNullObject](/javascript/api/excel/excel.nameditemcollectionloadoptions#worksheetornullobject)|Pour chaque élément de la collection: renvoie la feuille de calcul dans laquelle l’élément nommé est inclus dans l’étendue. Renvoie un objet null si l’élément est inclus dans le classeur à la place.|
|[NamedItemData](/javascript/api/excel/excel.nameditemdata)|[comment](/javascript/api/excel/excel.nameditemdata#comment)|Représente le commentaire associé à ce nom.|
||[étendue](/javascript/api/excel/excel.nameditemdata#scope)|Indique si le nom est étendu au classeur ou à une feuille de calcul spécifique. Les valeurs possibles sont les suivantes: Worksheet, Workbook. En lecture seule.|
|[NamedItemLoadOptions](/javascript/api/excel/excel.nameditemloadoptions)|[comment](/javascript/api/excel/excel.nameditemloadoptions#comment)|Représente le commentaire associé à ce nom.|
||[étendue](/javascript/api/excel/excel.nameditemloadoptions#scope)|Indique si le nom est étendu au classeur ou à une feuille de calcul spécifique. Les valeurs possibles sont les suivantes: Worksheet, Workbook. En lecture seule.|
||[worksheet](/javascript/api/excel/excel.nameditemloadoptions#worksheet)|Renvoie la feuille de calcul dans laquelle est inclus l’élément nommé. Renvoie une erreur si l’élément est inclus dans l’étendue du classeur.|
||[worksheetOrNullObject](/javascript/api/excel/excel.nameditemloadoptions#worksheetornullobject)|Renvoie la feuille de calcul dans laquelle est inclus l’élément nommé. Renvoie un objet null si l’élément est inclus dans le classeur à la place.|
|[NamedItemUpdateData](/javascript/api/excel/excel.nameditemupdatedata)|[comment](/javascript/api/excel/excel.nameditemupdatedata#comment)|Représente le commentaire associé à ce nom.|
|[PivotTableCollection](/javascript/api/excel/excel.pivottablecollection)|[getCount()](/javascript/api/excel/excel.pivottablecollection#getcount--)|Obtient le nombre de tableaux croisés dynamiques de la collection.|
||[getItemOrNullObject(name: string)](/javascript/api/excel/excel.pivottablecollection#getitemornullobject-name-)|Extrait un tableau croisé dynamique par nom. Si le tableau croisé dynamique n’existe pas, renvoie un objet null.|
|[Range](/javascript/api/excel/excel.range)|[getIntersectionOrNullObject (anotherRange: chaîne \| de plage)](/javascript/api/excel/excel.range#getintersectionornullobject-anotherrange-)|Obtient l’objet de plage qui représente l’intersection rectangulaire des plages données. Si aucune intersection n’est trouvée, renvoie un objet Null.|
||[getUsedRangeOrNullObject (valuesOnly?: booléen)](/javascript/api/excel/excel.range#getusedrangeornullobject-valuesonly-)|Renvoie la plage utilisée d’un objet de plage donné. Si aucune cellule n’est utilisée dans la plage, cette fonction renvoie un objet null.|
|[RangeViewCollection](/javascript/api/excel/excel.rangeviewcollection)|[getCount()](/javascript/api/excel/excel.rangeviewcollection#getcount--)|Obtient le nombre d’objets RangeView dans la collection.|
|[Paramètre](/javascript/api/excel/excel.setting)|[delete()](/javascript/api/excel/excel.setting#delete--)|Supprime le paramètre.|
||[](/javascript/api/excel/excel.setting#datejsonprefix)||
||[](/javascript/api/excel/excel.setting#datejsonsuffix)||
||[](/javascript/api/excel/excel.setting#replacestringdatewithdate)||
||[key](/javascript/api/excel/excel.setting#key)|Renvoie la clé qui représente l’id du paramètre. En lecture seule.|
||[Set (propriétés: Excel. Setting)](/javascript/api/excel/excel.setting#set-properties-)|Définit plusieurs propriétés de l’objet en même temps, en fonction d’un objet chargé existant.|
||[Set (propriétés: interfaces. SettingUpdateData, Options?: objet officeextension. UpdateOptions)](/javascript/api/excel/excel.setting#set-properties--options-)|Définit plusieurs propriétés d’un objet en même temps. Vous pouvez transmettre un objet plain avec les propriétés appropriées, ou un autre objet API du même type.|
||[value](/javascript/api/excel/excel.setting#value)|Représente la valeur stockée pour ce paramètre.|
|[SettingCollection](/javascript/api/excel/excel.settingcollection)|[Add (Key: chaîne, value: numéro \| \| de chaîne \| du \| tableau<any> \| de dates booléen any)](/javascript/api/excel/excel.settingcollection#add-key--value-)|Définit ou ajoute le paramètre spécifié dans le classeur.|
||[getCount()](/javascript/api/excel/excel.settingcollection#getcount--)|Obtient le nombre de paramètres dans la collection.|
||[getItem(key: string)](/javascript/api/excel/excel.settingcollection#getitem-key-)|Obtient une Entrée de paramètre via la clé.|
||[getItemOrNullObject(key: string)](/javascript/api/excel/excel.settingcollection#getitemornullobject-key-)|Obtient une entrée de paramètre via la clé. Si le paramètre n’existe pas, renvoie un objet null.|
||[items](/javascript/api/excel/excel.settingcollection#items)|Obtient l’élément enfant chargé dans cette collection de sites.|
||[onSettingsChanged](/javascript/api/excel/excel.settingcollection#onsettingschanged)|Se produit lorsque les paramètres dans le document sont modifiés.|
|[SettingCollectionLoadOptions](/javascript/api/excel/excel.settingcollectionloadoptions)|[$all](/javascript/api/excel/excel.settingcollectionloadoptions#$all)||
||[key](/javascript/api/excel/excel.settingcollectionloadoptions#key)|Pour chaque élément de la collection: renvoie la clé qui représente l’ID du paramètre. En lecture seule.|
||[value](/javascript/api/excel/excel.settingcollectionloadoptions#value)|Pour chaque élément de la collection: représente la valeur stockée pour ce paramètre.|
|[SettingData](/javascript/api/excel/excel.settingdata)|[key](/javascript/api/excel/excel.settingdata#key)|Renvoie la clé qui représente l’id du paramètre. En lecture seule.|
||[value](/javascript/api/excel/excel.settingdata#value)|Représente la valeur stockée pour ce paramètre.|
|[SettingLoadOptions](/javascript/api/excel/excel.settingloadoptions)|[$all](/javascript/api/excel/excel.settingloadoptions#$all)||
||[key](/javascript/api/excel/excel.settingloadoptions#key)|Renvoie la clé qui représente l’id du paramètre. En lecture seule.|
||[value](/javascript/api/excel/excel.settingloadoptions#value)|Représente la valeur stockée pour ce paramètre.|
|[SettingUpdateData](/javascript/api/excel/excel.settingupdatedata)|[value](/javascript/api/excel/excel.settingupdatedata#value)|Représente la valeur stockée pour ce paramètre.|
|[SettingsChangedEventArgs](/javascript/api/excel/excel.settingschangedeventargs)|[settings](/javascript/api/excel/excel.settingschangedeventargs#settings)|Obtient l’objet Setting qui représente la liaison qui a déclenché l’événement SettingsChanged.|
|[TableCollection](/javascript/api/excel/excel.tablecollection)|[getCount()](/javascript/api/excel/excel.tablecollection#getcount--)|Obtient le nombre de tableaux de la collection.|
||[getItemOrNullObject(key: string)](/javascript/api/excel/excel.tablecollection#getitemornullobject-key-)|Obtient un tableau à l’aide de son nom ou de son ID. Si le tableau n’existe pas, renvoie un objet null.|
|[TableColumnCollection](/javascript/api/excel/excel.tablecolumncollection)|[getCount()](/javascript/api/excel/excel.tablecolumncollection#getcount--)|Obtient le nombre de colonnes dans le tableau.|
||[getItemOrNullObject (Key: valeur \| numérique)](/javascript/api/excel/excel.tablecolumncollection#getitemornullobject-key-)|Obtient un objet de colonne par nom ou par ID. Si la colonne n’existe pas, renvoie un objet null.|
|[TableRowCollection](/javascript/api/excel/excel.tablerowcollection)|[getCount()](/javascript/api/excel/excel.tablerowcollection#getcount--)|Obtient le nombre de lignes dans le tableau.|
|[Workbook](/javascript/api/excel/excel.workbook)|[settings](/javascript/api/excel/excel.workbook#settings)|Représente une collection d’objets Settings associés au classeur. En lecture seule.|
|[WorkbookData](/javascript/api/excel/excel.workbookdata)|[settings](/javascript/api/excel/excel.workbookdata#settings)|Représente une collection d’objets Settings associés au classeur. En lecture seule.|
|[Worksheet](/javascript/api/excel/excel.worksheet)|[getUsedRangeOrNullObject (valuesOnly?: booléen)](/javascript/api/excel/excel.worksheet#getusedrangeornullobject-valuesonly-)|La plage utilisée est la plus petite plage qui englobe toutes les cellules auxquelles une valeur ou un format est affecté. Si la feuille de calcul entière est vide, cette fonction renvoie un objet null.|
||[zone](/javascript/api/excel/excel.worksheet#names)|Collection de noms inclus dans l’étendue de la feuille de calcul active. En lecture seule.|
|[WorksheetCollection](/javascript/api/excel/excel.worksheetcollection)|[getCount (visibleOnly?: Boolean)](/javascript/api/excel/excel.worksheetcollection#getcount-visibleonly-)|Obtient le nombre de feuilles de calcul dans la collection.|
||[getItemOrNullObject(key: string)](/javascript/api/excel/excel.worksheetcollection#getitemornullobject-key-)|Obtient un objet de feuille de calcul à l’aide de son nom ou de son ID. Si la feuille de calcul n’existe pas, renvoie un objet null.|
|[WorksheetData](/javascript/api/excel/excel.worksheetdata)|[zone](/javascript/api/excel/excel.worksheetdata#names)|Collection de noms inclus dans l’étendue de la feuille de calcul active. En lecture seule.|

## <a name="see-also"></a>Voir aussi

- [Documentation de référence de l’API JavaScript pour Excel](/javascript/api/excel)
- [Ensembles de conditions requises de l’API JavaScript pour Excel](./excel-api-requirement-sets.md)