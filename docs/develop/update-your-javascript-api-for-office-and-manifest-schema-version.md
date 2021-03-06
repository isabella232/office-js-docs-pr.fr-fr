---
title: Mise à jour vers la dernière bibliothèque d’API JavaScript Office et schéma de manifeste de complément version 1,1
description: Mettez à jour vos fichiers JavaScript (Office.js et fichiers .js propres aux applications) et le fichier de validation du manifeste du complément dans votre projet Complément Office vers la version 1.1.
ms.date: 10/11/2019
localization_priority: Normal
ms.openlocfilehash: b0536b4b55accd99e002e26c467572330ba72ae2
ms.sourcegitcommit: 9609bd5b4982cdaa2ea7637709a78a45835ffb19
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2020
ms.locfileid: "47293127"
---
# <a name="update-to-the-latest-office-javascript-api-library-and-version-11-add-in-manifest-schema"></a>Mise à jour vers la dernière bibliothèque d’API JavaScript Office et schéma de manifeste de complément version 1,1

Cet article décrit comment mettre à jour vers la version 1.1 les fichiers JavaScript pour Office (Office.js et fichiers .js propres aux applications) et le fichier de validation du manifeste du complément utilisés dans votre projet de complément Office.

> [!NOTE]
> Les projets créés dans Visual Studio 2019 utiliseront déjà la version 1,1. Il existe toutefois des mises à jour mineures occasionnelles vers la version 1.1 que vous pouvez appliquer à l’aide des techniques décrites dans cet article.

## <a name="use-the-most-up-to-date-project-files"></a>Utilisation des fichiers de projet les plus récents

Si vous utilisez Visual Studio pour développer votre complément, pour utiliser les membres les plus récents de l’API JavaScript pour Office et les [fonctionnalités v 1.1 du manifeste de complément](../develop/add-in-manifests.md) (qui est validé par rapport à offappmanifest-1.1. xsd), vous devez télécharger Visual Studio 2019. Pour télécharger Visual Studio 2019, voir la [page Visual Studio IDE](https://visualstudio.microsoft.com/vs/). Lors de l’installation, vous devez sélectionner la charge de travail de développement Office/SharePoint.

Si vous utilisez un éditeur de texte ou une interface IDE autre que Visual Studio pour développer votre complément, vous devez mettre à jour les références vers le CDN pour Office.js et la version de schéma référencée dans le manifeste de votre complément.

Pour exécuter un complément développé à l’aide des fonctionnalités de manifeste de complément et de l’API Office.js nouvelles et mises à jour, vos clients doivent exécuter Office 2013 SP1 ou version ultérieure sur des produits locaux et, le cas échéant, SharePoint Server 2013 SP1 et les produits serveur associés, Exchange Server 2013 Service Pack 1 (SP1) ou les produits hébergés en ligne équivalents : Microsoft 365, SharePoint Online et

Pour télécharger des produits Office, SharePoint et Exchange SP1, voir :

- [Liste de toutes les mises à jour Service Pack 1 (SP1) pour Microsoft Office 2013 et les produits bureautiques connexes](https://support.microsoft.com/kb/2850036)

- [Liste de toutes les mises à jour Service Pack 1 (SP1) pour Microsoft SharePoint Server 2013 et les produits serveur connexes](https://support.microsoft.com/kb/2850035)

- [Description du Service Pack 1 d’Exchange Server 2013](https://support.microsoft.com/kb/2926248)


## <a name="updating-an-office-add-in-project-created-with-visual-studio"></a>Mise à jour d’un projet de complément Office créé avec Visual Studio

Pour les projets créés avant la publication de la version 1.1 de l’API JavaScript Office et du schéma de manifeste de complément, vous pouvez mettre à jour les fichiers d’un projet à l’aide du **Gestionnaire de package NuGet**, puis mettre à jour les pages HTML de votre complément pour les référencer. 

Notez que le processus de mise à jour est appliqué  _par projet_  ; vous devrez répéter le processus de mise à jour pour chaque projet de complément dans lequel vous souhaitez utiliser la version 1.1 d’Office.js et du schéma de manifeste de complément.

### <a name="update-the-office-javascript-api-library-files-in-your-project-to-the-newest-release"></a>Mettre à jour les fichiers de bibliothèque de l’API JavaScript pour Office dans votre projet vers la version la plus récente
Les étapes suivantes permettent de mettre à jour vos fichiers de bibliothèque Office.js vers la dernière version. Les étapes utilisent Visual Studio 2019, mais elles sont similaires pour les versions précédentes de Visual Studio.

1. Dans Visual Studio 2019, ouvrez ou créez un projet **de complément Office** .
2. Sélectionnez **Outils**le  >  **Gestionnaire de package NuGet**  >  **gérer les packages NuGet pour la solution**.
3. Sélectionnez l’onglet **Mises à jour**.
4. Sélectionnez Microsoft.Office.js. Vérifiez que la source du package provient de **NuGet.org**.
5. Dans le volet de gauche, choisissez **installer** et exécutez le processus de mise à jour du package.

Vous devez effectuer quelques étapes supplémentaires pour terminer la mise à jour. Dans la balise **Head** des pages HTML de votre complément, mettez en commentaire ou supprimez les références de script office.js existantes, puis référencez la bibliothèque d’API JavaScript Office mise à jour comme suit :

  ```html
  <script src="https://appsforoffice.microsoft.com/lib/1/hosted/office.js" type="text/javascript"></script>
  ```

   > [!NOTE] 
   > La valeur `/1/` de `office.js` dans l’URL du CDN préconise l’utilisation de la dernière version incrémentielle comprise dans la version 1 d’Office.js.


### <a name="update-the-manifest-file-in-your-project-to-use-schema-version-11"></a>Mise à jour du fichier manifeste dans votre projet afin d’utiliser la version 1.1 du schéma

Dans le fichier manifeste de votre complément, mettez à jour l’attribut **xmlns** de l’élément **OfficeApp** en appliquant la valeur `1.1` à la version (sans modifier les attributs autres que **xmlns**).

```xml
<?xml version="1.0" encoding="utf-8"?>
<OfficeApp xsi:type="ContentApp"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns="http://schemas.microsoft.com/office/appforoffice/1.1">
  
  <!-- manifest contents -->

</OfficeApp>
```

> [!NOTE]
> Après avoir mis à jour la version du schéma de manifeste de complément en 1,1, vous devrez supprimer les éléments **Capabilities** et **Capability** , et les remplacer par les éléments [hosts](../reference/manifest/hosts.md) et [Host](../reference/manifest/host.md) ou les [éléments Requirements et](specify-office-hosts-and-api-requirements.md)requirement.

## <a name="updating-an-office-add-in-project-created-with-a-text-editor-or-other-ide"></a>Mise à jour d’un projet de complément Office créé avec un éditeur de texte ou une autre IDE

Pour les projets créés avant la publication de la version 1.1 de l’API JavaScript Office et du schéma de manifeste de complément, vous devez mettre à jour les pages HTML de votre complément pour référencer le CDN de la bibliothèque v 1.1 et mettre à jour le fichier manifeste de votre complément pour utiliser la version 1.1 du schéma. 

Le processus de mise à jour est appliqué  _par projet_  ; vous devrez répéter le processus de mise à jour pour chaque projet de complément dans lequel vous souhaitez utiliser la version 1.1 d’Office.js et du schéma de manifeste de complément.

Vous n’avez pas besoin de copies locales des fichiers de l’API JavaScript Office (Office.js et des fichiers. js propres à l’application) pour développer le complément Abonnementoffice (référençant le CDN pour Office.js télécharge les fichiers nécessaires au moment de l’exécution), mais si vous souhaitez une copie locale des fichiers de bibliothèque, vous pouvez utiliser l' [utilitaire de ligne de commande NuGet](https://docs.nuget.org/consume/installing-nuget) et la `Install-Package Microsoft.Office.js` commande pour les télécharger.

> [!NOTE]
> pour obtenir une copie du fichier XSD (définition du schéma XML) pour le manifeste de complément version 1.1, consultez les [informations de référence sur le schéma des manifestes des compléments Office (version 1.1)](../develop/add-in-manifests.md).


### <a name="update-the-office-javascript-api-library-files-in-your-project-to-use-the-newest-release"></a>Mettre à jour les fichiers de bibliothèque de l’API JavaScript pour Office dans votre projet pour utiliser la dernière version

1. Ouvrez les pages HTML de votre complément dans un éditeur de texte ou une interface IDE.

2. Dans la balise **Head** des pages HTML de votre complément, mettez en commentaire ou supprimez les références de script office.js existantes, puis référencez la bibliothèque d’API JavaScript Office mise à jour comme suit :

    ```html
    <script src="https://appsforoffice.microsoft.com/lib/1/hosted/office.js" type="text/javascript"></script>
    ```

   > [!NOTE]
   > la valeur `/1/` devant `office.js` dans l’URL du CDN préconise l’utilisation de la dernière version incrémentielle comprise dans la version 1 d’Office.js.

### <a name="update-the-manifest-file-in-your-project-to-use-schema-version-11"></a>Mise à jour du fichier manifeste dans votre projet afin d’utiliser la version 1.1 du schéma

Dans le fichier manifeste de votre complément, mettez à jour l’attribut **xmlns** de l’élément **OfficeApp** en appliquant la valeur `1.1` à la version (sans modifier les attributs autres que **xmlns**).

```xml
<?xml version="1.0" encoding="utf-8"?>
<OfficeApp xsi:type="ContentApp"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns="http://schemas.microsoft.com/office/appforoffice/1.1">
  
  <!-- manifest contents -->

</OfficeApp>
```

> [!NOTE]
> Après avoir mis à jour la version du schéma de manifeste de complément en 1,1, vous devrez supprimer les éléments **Capabilities** et **Capability** , et les remplacer par les éléments [hosts](../reference/manifest/hosts.md) et [Host](../reference/manifest/host.md) ou les [éléments Requirements et](specify-office-hosts-and-api-requirements.md)requirement.

## <a name="see-also"></a>Voir aussi

- [Spécifier les applications Office et les conditions requises de l’API](specify-office-hosts-and-api-requirements.md) ]
- [Compréhension de l’API JavaScript pour Office](understanding-the-javascript-api-for-office.md)
- [API JavaScript pour Office](../reference/javascript-api-for-office.md)
- [Informations de référence sur le schéma des manifestes des applications pour Office (version 1.1)](../develop/add-in-manifests.md)
