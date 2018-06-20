---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Katalógusbeli parancsmagok
ms.openlocfilehash: 7eaca09667af0eb5d719f23e987bb112e8514978
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189067"
---
# <a name="catalog-cmdlets"></a>Katalógus-parancsmagok

A két új parancsmagok jelentek meg [Microsoft.Powershell.Secuity](https://technet.microsoft.com/en-us/library/hh847877.aspx) modul hozhatnak létre és a windows katalógusban fájlok érvényesítése.

## <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

`New-FileCatalog` létrehoz egy windows catalog mappák és fájlok. A katalógusban az összes fájl megadott elérési utak a kivonatok tartalmazza. Mappák és a katalógus fájl ezeken a mappákon jelölő megfelelő készletét terjeszthetnek. Egy katalógusfájlt segítségével tartalom címzettje ellenőrzi, hogy a módosítások a mappákat a katalógus létrehozása után.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
1. és 2 létrehozása katalógus verziója támogatott. 1-es verziójú SHA1 kivonatoló algoritmust használ fájlkivonat és 2 használ SHA256 verzió létrehozásához. Katalógus 2-es verzió nem támogatott a *Windows Server 2008 R2* és *Windows 7*. Javasoljuk, hogy a katalógus 2-es verzióját használja, ha platformokat használó *Windows 8*, *Windows Server 2012* vagy újabb verzió.

Egy meglévő modul ezen parancs használatához adja meg kell egyeznie a moduljegyzékben helyét CatalogFilePath és az elérési utat változókat. Az alábbi példában a moduljegyzékben C:\Program Files\Windows PowerShell\Modules\Pester van.

![](../images/NewFileCatalog.jpg)

Ez a katalógus fájlt hoz létre.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Egy katalógusfájlt (Pester.cat a fenti exmaple) sértetlenségének ellenőrzése, alá kell írni használatával a [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) parancsmag.


## <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

`Test-FileCatalog` a katalógus képviselő mappákat ellenőrzi.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Ez a parancsmag összehasonlítja a kivonatok összes fájl és a relatív elérési utak azokat, lemezre menti a katalógus fájlban található. Ha a fájlkivonat és elérési utak bármely eltérést észlel állapotot adja vissza `ValidationFailed`.
Felhasználók tudják lekérni az összes ezek az adatokat a a `Detailed` váltani. A katalógus aláírási állapot jelenik meg a `Signature` mező, amely ugyanaz, mint a hívása a [Get-AuthenticodeSignature](https://technet.microsoft.com/en-us/library/hh849805.aspx) parancsmag a katalógus fájlra.
Felhasználók is hagyhatja a fájl ellenőrzésekor használatával a `FilesToSkip` paraméter.
