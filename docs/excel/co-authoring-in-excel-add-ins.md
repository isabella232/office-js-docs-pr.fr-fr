---
title: Co-création dans des macros complémentaires Excel
description: ''
ms.date: 12/04/2017
ms.openlocfilehash: 1919f66a3c93c42ec24520f971eda33dac491355
ms.sourcegitcommit: 4de2a1b62ccaa8e51982e95537fc9f52c0c5e687
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/10/2018
ms.locfileid: "22925240"
---
# <a name="coauthoring-in-excel-add-ins"></a>Co-création dans des macros complémentaires Excel  

Avec la [co-création](https://support.office.com/article/Collaborate-on-Excel-workbooks-at-the-same-time-with-co-authoring-7152aa8b-b791-414c-a3bb-3024e46fb104), plusieurs personnes peuvent travailler ensemble et modifier simultanément le même classeur Excel. Tous les co-auteurs d’un classeur peuvent voir les modifications d’un autre co-auteur dès que ce co-auteur enregistre le classeur. Pour co-créer un classeur Excel, le classeur doit être enregistré dans OneDrive, OneDrive Entreprise ou SharePoint Online.

> [!IMPORTANT]
> Dans Excel 2016 pour Office 365, vous remarquerez l’enregistrement automatique dans le coin supérieur gauche. Lorsque l’enregistrement automatique est activé, les co-auteurs visualisent vos modifications en temps réel. Prenez en considération l’impact de ce comportement sur la conception de votre complément Excel. Les utilisateurs peuvent désactiver l’enregistrement automatique via le commutateur dans le coin supérieur gauche de la fenêtre Excel.

La co-création est disponible sur les plateformes suivantes :

- Excel Online
- Excel pour Android
- Excel pour iOS
- Excel Mobile pour Windows 10
- Excel pour bureau Windows pour les clients Office 365 (bureau Windows version 16.0.8326.2076 ou ultérieure, disponible pour les clients à compter d’août 2017)

## <a name="coauthoring-overview"></a>Vue d’ensemble de la co-création
 
Lorsque vous modifiez le contenu d’un classeur, Excel synchronise automatiquement ces modifications avec tous les co-auteurs. Les co-auteurs peuvent modifier le contenu d’un classeur, mais peuvent également exécuter du code dans un complément Excel. Par exemple, lorsque le code JavaScript suivant s’exécute dans un complément Office, la valeur de la plage est définie sur Contoso :

```js
range.values = [['Contoso']];
```
Après la synchronisation de « Contoso » avec tous les co-auteurs, tout utilisateur ou complément en cours d’exécution dans le même classeur visualisera la nouvelle valeur de la plage. 

La co-création permet uniquement la synchronisation du contenu dans le classeur partagé. Les valeurs copiées du classeur vers les variables JavaScript dans un complément Excel ne sont pas synchronisées. Par exemple, si votre complément enregistre la valeur d’une cellule (par exemple, « Contoso ») dans une variable JavaScript et qu’un co-auteur modifie ensuite la valeur de la cellule sur « Exemple », après la synchronisation, tous les co-auteurs verront « Exemple » dans la cellule. Toutefois, la valeur de la variable JavaScript sera toujours définie sur « Contoso ». En outre, lorsque plusieurs co-auteurs utilisent le même complément, chaque co-auteur possède sa propre copie de la variable, qui n’est pas synchronisée. Lorsque vous utilisez des variables qui utilisent le contenu du classeur, veillez à bien rechercher les valeurs mises à jour dans le classeur avant d’utiliser la variable. 

## <a name="use-events-to-manage-the-in-memory-state-of-your-add-in"></a>Utiliser des événements pour gérer l’état de la mémoire de votre complément
 
Les compléments Excel peuvent lire le contenu du classeur (à partir de feuilles de calcul masquées et d’un objet de paramètres), puis l’enregistrer dans des structures de données comme des variables. Une fois que les valeurs d’origine sont copiées dans l’une de ces structures de données, les co-auteurs peuvent mettre à jour le contenu du classeur d’origine. Cela signifie que les valeurs copiées dans les structures de données ne sont plus synchronisées avec le contenu du classeur. Lorsque vous générez vos compléments, pensez à prendre en compte cette séparation de contenu du classeur et les valeurs enregistrées dans les structures de données.

Par exemple, vous pouvez créer un complément de contenu qui affiche des visualisations personnalisées. L’état de vos visualisations personnalisées peut être enregistré dans une feuille de calcul masquée. Lorsque les co-auteurs utilisent le même classeur, le scénario suivant peut se produire :

- L’utilisateur A ouvre le document et les visualisations personnalisées sont affichées dans le classeur. Les visualisations personnalisées lisent les données d’une feuille de calcul masquée (par exemple, la couleur des visualisations est définie sur bleu).
- L’utilisateur B ouvre le même document et commence à modifier les visualisations personnalisées. L’utilisateur B définit la couleur des visualisations personnalisées sur orange. La valeur Orange est enregistrée dans la feuille de calcul masquée.
- La feuille de calcul masquée de l’utilisateur A est mise à jour avec la nouvelle valeur Orange.
- Les visualisations personnalisées de l’utilisateur A sont toujours bleues. 

Si vous souhaitez que les visualisations personnalisées de l’utilisateur A répondent aux modifications apportées par les co-auteurs sur la feuille de calcul masquée, utilisez l’événement [BindingDataChanged](https://dev.office.com/reference/add-ins/shared/binding.bindingdatachangedevent). Cela garantit que les modifications apportées au contenu du classeur par les co-auteurs sont répercutées à l’état de votre complément.

## <a name="caveats-to-using-events-with-coauthoring"></a>Restrictions à l’utilisation des événements dans le cadre de la co-création 

Comme indiqué précédemment, dans certains scénarios, le déclenchement d’événements pour tous les co-auteurs permet d’améliorer l’expérience utilisateur. Toutefois, sachez que, dans certains scénarios, ce comportement peut entraîner des expériences utilisateur médiocres. 

Par exemple, dans les scénarios de validation de données, il est fréquent d’afficher l’interface utilisateur en réponse aux événements. L’événement [BindingDataChanged](https://dev.office.com/reference/add-ins/shared/binding.bindingdatachangedevent) décrit dans la section précédente s’exécute lorsqu’un utilisateur local ou un co-auteur modifie (à distance) le contenu du classeur dans la liaison. Si le gestionnaire d’événements de l’événement **BindingDataChanged** affiche l’interface utilisateur, les utilisateurs verront une interface utilisateur qui n’est pas liée aux modifications sur lesquelles ils travaillaient dans le classeur, entraînant ainsi une expérience utilisateur médiocre. Évitez d’afficher l’interface utilisateur lorsque vous utilisez des événements dans votre complément.

## <a name="see-also"></a>Voir aussi 

- [À propos de la co-création dans Excel (VBA)](https://msdn.microsoft.com/vba/excel-vba/articles/about-coauthoring-in-excel) 
- [Impact de l’enregistrement automatique sur les compléments et les macros (VBA)](https://msdn.microsoft.com/vba/office-shared-vba/articles/how-autosave-impacts-addins-and-macros) 