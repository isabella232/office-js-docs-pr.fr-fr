---
title: Commandes Activé et Désactivé pour les compléments
description: Découvrez la modification de l'état Activé ou Désactivé des boutons de rubans et des éléments de menu personnalisés dans votre complément web Office.
ms.date: 11/07/2020
localization_priority: Normal
ms.openlocfilehash: 7a9994ae25285c876236879e65861ee3cc59f7e5
ms.sourcegitcommit: ca66ff7462bfdf4ed7ae04f43d1388c24de63bf9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2020
ms.locfileid: "48996388"
---
# <a name="enable-and-disable-add-in-commands"></a>Commandes Activé et Désactivé pour les compléments

Lorsque seulement quelques fonctionnalités de votre complément doivent être disponibles dans certains contextes, vous pouvez activer ou désactiver vos commandes de complément personnalisées par programme. Par exemple, une fonction qui modifie l’en-tête d’un tableau doit être uniquement activée lorsque le curseur se trouve dans un tableau.

Vous pouvez également spécifier si la commande est activée ou désactivée lorsque l’application cliente Office s’ouvre.

> [!NOTE]
> Cet article suppose que vous connaissez la documentation décrite ci-après. Étudiez-la si vous n’avez pas récemment utilisé les commandes de complément (éléments de menu et boutons de ruban personnalisés).
>
> - [Concepts basiques pour les commandes de complément](add-in-commands.md)

## <a name="office-application-and-platform-support-only"></a>Prise en charge de l’application et de la plateforme Office uniquement

Les API décrites dans cet article sont disponibles uniquement dans Excel, et uniquement dans Office sous Windows, Office sur Mac et Office sur le Web.

### <a name="test-for-platform-support-with-requirement-sets"></a>Effectuez un test pour la prise en charge des plateformes avec les ensembles de conditions requises

Les ensembles de conditions requises sont des groupes nommés de membres d’API. Les compléments Office utilisent les ensembles de conditions requises spécifiés dans le manifeste ou utilisent une vérification à l’exécution pour déterminer si une combinaison d’applications Office et de plateformes prend en charge les API dont un complément a besoin. Pour plus d’informations, consultez la rubrique [versions d’Office et ensembles de conditions requises](../develop/office-versions-and-requirement-sets.md).

Les API d’activation/de désactivation appartiennent à l’ensemble de conditions requises [RibbonApi 1,1](../reference/requirement-sets/ribbon-api-requirement-sets.md) .

> [!NOTE]
> L’ensemble de conditions requises **RibbonApi 1,1** n’étant pas encore pris en charge dans le manifeste, vous ne pouvez pas le spécifier dans la section du manifeste `<Requirements>` . Pour tester la prise en charge, votre code doit appeler `Office.context.requirements.isSetSupported('RibbonApi', '1.1')` . Si, *et seulement si* , cet appel `true` est renvoyé, votre code peut appeler les API activer/désactiver. Si l’appel de la `isSetSupported` méthode retournée `false` est activé, toutes les commandes de complément personnalisées sont activées en totalité. Vous devez concevoir votre complément de production, ainsi que toutes les instructions dans l’application, pour tenir compte de la façon dont il fonctionnera lorsque l’ensemble de conditions requises **RibbonApi 1,1** n’est pas pris en charge. Pour plus d’informations et des exemples d’utilisation `isSetSupported` , reportez-vous à la rubrique [spécifier les applications Office et les conditions requises](../develop/specify-office-hosts-and-api-requirements.md)de l’API, notamment [utiliser les vérifications d’exécution dans votre code JavaScript](../develop/specify-office-hosts-and-api-requirements.md#use-runtime-checks-in-your-javascript-code). (La section [définir l’élément Requirements dans le manifeste](../develop/specify-office-hosts-and-api-requirements.md#set-the-requirements-element-in-the-manifest) de cet article ne s’applique pas au ruban 1,1.)

## <a name="shared-runtime-required"></a>Runtime partagé requis

Les API et balisages de manifeste décrits dans cet article exigent que le manifeste du complément spécifie la nécessité d’utiliser un runtime partagé. Pour ce faire, procédez comme suit.

1. Dans l'élément [Runtimes du manifeste](../reference/manifest/runtimes.md), ajoutez l’élément enfant suivant : `<Runtime resid="Contoso.SharedRuntime.Url" lifetime="long" />`. (s’il n’y a pas encore d’élément `<Runtimes>` dans le manifeste, créez-le en tant que premier enfant sous l’élément `<Host>` dans la section `VersionOverrides`.)
2. Dans la section [Resources.Urls](../reference/manifest/resources.md) du manifeste, ajoutez l’élément enfant suivant : `<bt:Url id="Contoso.SharedRuntime.Url" DefaultValue="https://{MyDomain}/{path-to-start-page}" />`, où `{MyDomain}` est le domaine du complément et `{path-to-start-page}` le chemin d’accès de la page de démarrage du complément. par exemple : `<bt:Url id="Contoso.SharedRuntime.Url" DefaultValue="https://localhost:3000/index.html" />`.
3. En fonction du contenu de votre complément, à savoir un volet des tâches, un fichier de fonctions ou une fonction Excel personnalisée, vous devez effectuer au moins une des trois étapes suivantes :

    - Si le complément contient un volet Office, définissez l'attribut `resid` de l’élément [Action](../reference/manifest/action.md).[SourceLocation](../reference/manifest/sourcelocation.md) sur la même chaîne que celle que vous avez utilisée pour le `resid` de l’élément `<Runtime>` à l’étape 1 ; par exemple, `Contoso.SharedRuntime.Url`. Le fichier doit ressembler à ceci : `<SourceLocation resid="Contoso.SharedRuntime.Url"/>`.
    - Si le complément contient une fonction personnalisée Excel, définissez l'attribut `resid` de l’élément [Page](../reference/manifest/page.md).[SourceLocation](../reference/manifest/sourcelocation.md) sur la même chaîne que celle que vous avez utilisée pour le `resid` de l’élément `<Runtime>` à l’étape 1 ; par exemple, `Contoso.SharedRuntime.Url`. Le fichier doit ressembler à ceci : `<SourceLocation resid="Contoso.SharedRuntime.Url"/>`.
    - Si le complément contient un fichier de fonctions, définissez l'attribut `resid` de l’élément [FunctionFile](../reference/manifest/functionfile.md) sur la même chaîne que celle que vous avez utilisée pour le `resid` de l’élément `<Runtime>` à l’étape 1 ; par exemple, `Contoso.SharedRuntime.Url`. Le fichier doit ressembler à ceci : `<FunctionFile resid="Contoso.SharedRuntime.Url"/>`.

## <a name="set-the-default-state-to-disabled"></a>Configurer l'état par défaut sur désactivé

Les commandes de complément sont activées par défaut au démarrage de l’application Office. Si vous souhaitez qu’un bouton ou un élément de menu personnalisé soit désactivé au démarrage de l’application Office, vous devez le spécifier dans le manifeste. Il vous suffit d’ajouter un élément [activé](../reference/manifest/enabled.md) (avec la valeur `false`) juste *au-dessous* (non à l’intérieur) de l'élément [Action](../reference/manifest/action.md) dans la déclaration du contrôle. La structure basique est la suivante :

```xml
<OfficeApp ...>
  ...
  <VersionOverrides ...>
    ...
    <Hosts>
      <Host ...>
        ...
        <DesktopFormFactor>
          <ExtensionPoint ...>
            <CustomTab ...>
              ...
              <Group ...>
                ...
                <Control ... id="MyButton">
                  ...
                  <Action ...>
                  <Enabled>false</Enabled>
...
</OfficeApp>
```

## <a name="change-the-state-programmatically"></a>Modifier l’état par programme

Les principales étapes pour modifier l’état activé d’une commande de complément sont les suivantes :

1. Créez un objet [RibbonUpdaterData](/javascript/api/office/office.ribbonupdaterdata) qui (1) spécifie la commande et son onglet parent, selon leur ID, comme spécifié dans le manifeste. et (2) indique l’état activé ou désactivé de la commande.
2. Transmettez l’objet **RibbonUpdaterData** à la méthode [Office.ribbon.requestUpdate ()](/javascript/api/office/office.ribbon?view=common-js&preserve-view=true#requestupdate-input-).

Voici un exemple simple. Veuillez noter que « MyButton » et « OfficeAddinTab1 » sont copiés à partir du manifeste.

```javascript
function enableButton() {
    Office.ribbon.requestUpdate({
        tabs: [
            {
                id: "OfficeAppTab1", 
                controls: [
                {
                    id: "MyButton", 
                    enabled: true
                }
            ]}
        ]});
}
```

Nous proposons également plusieurs interfaces (types) pour faciliter la construction de l’objet **RibbonUpdateData**. L’exemple suivant est l’équivalent de TypeScript et il utilise ces types.

```typescript
const enableButton = async () => {
    const button: Control = {id: "MyButton", enabled: true};
    const parentTab: Tab = {id: "OfficeAddinTab1", controls: [button]};
    const ribbonUpdater: RibbonUpdaterData = { tabs: [parentTab]};
    await Office.ribbon.requestUpdate(ribbonUpdater);
}
```

Office effectue un contrôle lorsqu’il met à jour l’état du ruban. La méthode **requestUpdate()** met en file d’attente une demande de mise à jour. La méthode permet de résoudre l’objet Promesse dès la mise en file d’attente de la demande, et non lors la prochaine mise à jour du ruban.

## <a name="change-the-state-in-response-to-an-event"></a>Modifier l’état en réponse à un événement

Un scénario courant est celui lors duquel l’état du ruban peut être modifié lorsqu’un événement initié par l’utilisateur modifie le contexte du complément.

Imaginez un scénario dans lequel un bouton doit être activé lorsque, et seulement lorsqu'un graphique est activé. La première étape consiste à définir l'élément [Activé](../reference/manifest/enabled.md) pour le bouton dans le manifeste `false`. Voir l'exemple ci-dessus.

Deuxièmement, assignez des gestionnaires. Cette procédure est généralement effectuée dans la méthode **Office.onReady** comme illustré dans l’exemple suivant qui assigne des gestionnaires (créés dans une étape ultérieure) aux évènements **onActivated** et **onDeactivated** de tous les graphiques de la feuille de calcul.

```javascript
Office.onReady(async () => {
    await Excel.run(context => {
        var charts = context.workbook.worksheets
            .getActiveWorksheet()
            .charts;
        charts.onActivated.add(enableChartFormat);
        charts.onDeactivated.add(disableChartFormat);
        return context.sync();
    });
});
```

Troisièmement, définissez le gestionnaire `enableChartFormat`. Voici un exemple simple, mais consultez les [Pratiques recommandées : test pour les erreurs de contrôle d’état](#best-practice-test-for-control-status-errors) ci-dessous pour modifier l’état d’un contrôle de façon plus efficace.

```javascript
function enableChartFormat() {
    var button = {id: "ChartFormatButton", enabled: true};
    var parentTab = {id: "CustomChartTab", controls: [button]};
    var ribbonUpdater = {tabs: [parentTab]};
    await Office.ribbon.requestUpdate(ribbonUpdater);
}
```

Quatrièmement, définissez le gestionnaire `disableChartFormat`. Il est identique à `enableChartFormat`, sauf que la propriété **activé** de l’objet bouton a la valeur `false`.

## <a name="best-practice-test-for-control-status-errors"></a>Pratiques recommandées : test pour les erreurs de contrôle d'état

Le ruban ne se redessine pas, dans certains cas, une fois que `requestUpdate` est appelé, de sorte que l’état du contrôle cliquable ne change pas. Il est pour cette raison recommandé de suivre l'état des contrôles du complément. Le complément doit respecter les règles suivantes :

1. Lorsque `requestUpdate` est appelé, le code doit enregistrer l’état prévu des boutons et éléments de menu personnalisés.
2. Lorsque l’utilisateur clique sur un contrôle personnalisé, le premier code dans le gestionnaire doit vérifier si le bouton aurait dû être cliquable. Dans la négative, le code doit signaler une erreur ou consigner une erreur et réessayer de définir les boutons de l'état prévu.

L’exemple suivant présente une fonction qui désactive un bouton et enregistre l’état du bouton. Veuillez noter que `chartFormatButtonEnabled` est une variable Boolean globale qui est initialisée sur la même valeur que l'élément [Activé](../reference/manifest/enabled.md) pour le bouton dans le manifeste.

```javascript
function disableChartFormat() {
    var button = {id: "ChartFormatButton", enabled: false};
    var parentTab = {id: "CustomChartTab", controls: [button]};
    var ribbonUpdater = {tabs: [parentTab]};
    await Office.ribbon.requestUpdate(ribbonUpdater);

    chartFormatButtonEnabled = false;
}
```

L’exemple suivant présente la façon dont le gestionnaire du bouton vérifie l’état d’un bouton incorrect. Veuillez noter que `reportError` est une fonction qui affiche ou consigne une erreur.

```javascript
function chartFormatButtonHandler() {
    if (chartFormatButtonEnabled) {

        // Do work here

    } else {
        // Report the error and try again to disable.
        reportError("That action is not possible at this time.");
        disableChartFormat();
    }
}
```

## <a name="error-handling"></a>Gestion des erreurs

Dans certains scénarios, Office ne peut pas mettre à jour le ruban et renvoie une erreur. Par exemple, si le complément est mis à niveau et que le complément mis à niveau dispose d'un autre groupe de commandes de complément personnalisé, l’application Office doit être fermée et ouverte de nouveau. La méthode `requestUpdate` renvoie l'erreur `HostRestartNeeded` jusqu'à ce que cela soit effectué. Voici comment vous pouvez gérer cette erreur. Dans ce cas, la méthode `reportError` affiche l’erreur à l’utilisateur.

```javascript
function disableChartFormat() {
    try {
        var button = {id: "ChartFormatButton", enabled: false};
        var parentTab = {id: "CustomChartTab", controls: [button]};
        var ribbonUpdater = {tabs: [parentTab]};
        await Office.ribbon.requestUpdate(ribbonUpdater);

        chartFormatButtonEnabled = false;
    }
    catch(error) {
        if (error.code == "HostRestartNeeded"){
            reportError("Contoso Awesome Add-in has been upgraded. Please save your work, close the Office application, and restart it.");
        }
    }
}
```
