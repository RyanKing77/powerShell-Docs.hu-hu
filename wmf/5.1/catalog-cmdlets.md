---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Katalógusbeli parancsmagok
ms.openlocfilehash: ec5fc866fe27a894b23b93d3ea46ad9c0cba288e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45522888"
---
# <a name="catalog-cmdlets"></a>Katalógusbeli parancsmagok

A két új parancsmag új verziója [Microsoft.Powershell.Secuity](https://technet.microsoft.com/library/hh847877.aspx) modul hozza létre, és a windows katalógusban fájlok érvényesítése.

## <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

`New-FileCatalog` létrehoz egy windows katalógusfájlt az tartozó fájlok és mappák. A katalógus-kivonat a megadott elérési utak lévő összes fájlt tartalmazza. A katalógus fájl mappákat jelölő megfelelő együtt mappakészlet terjeszthetnek. Egy katalógusfájlt megállapítani, hogy e módosítások történtek a mappákat a katalógus létrehozása után használhatják a címzett tartalom.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```
1. és 2 létrehozása katalógus-verzió is támogatott. 1. verziójának SHA1 kivonatoló algoritmust használja fájlkivonatokkal és verzió 2 használja SHA256 létrehozásához. Katalógus 2-es verzió nem támogatott az *Windows Server 2008 R2* és *Windows 7*. Javasoljuk, hogy ha platformok használja a katalógus 2-es verziójú *Windows 8*, *Windows Server 2012* vagy újabb verzió.

Ezzel a paranccsal egy meglévő modulon használatához adja meg a moduljegyzékben helyének megfelelően CatalogFilePath és az elérési út változókat. Az alábbi példában a moduljegyzékben C:\Program Files\Windows PowerShell\Modules\Pester szerepel.

![](../images/NewFileCatalog.jpg)

Ez a katalógus fájlt hoz létre.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Egy katalógusfájlt (Pester.cat a fenti példában) sértetlenségének ellenőrzése, alá kell írni használatával a [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) parancsmagot.


## <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

`Test-FileCatalog` a katalógus jelölő mappákat ellenőrzi.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Ez a parancsmag összehasonlítja a kivonatok, és azok relatív elérési utakat azokról, lemezre menti a katalógus fájlban található összes fájlt. Ha azt észleli, hogy bármely fájlkivonatokkal és elérési utak nem egyezik a állapotát adja vissza `ValidationFailed`.
Felhasználók kérheti le az összes ezen információk használatával a `Detailed` váltani. Aláíró állapotát, a katalógusban elemnél a `Signature` mező, amely ugyanaz, mint a hívása a [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) katalógusfájl parancsmagot.
Felhasználók ki is hagyhatja bármely fájl ellenőrzésekor használatával a `FilesToSkip` paraméter.
