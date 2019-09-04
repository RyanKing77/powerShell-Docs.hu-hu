---
ms.date: 09/11/2018
contributor: JKeithB
keywords: Galéria, PowerShell, psgallery
title: Csomagok manuális letöltése
ms.openlocfilehash: c0a96e866dfd27f9b2170ea540ec6dd0c67701fd
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215462"
---
# <a name="manual-package-download"></a>Csomagok manuális letöltése

A PowerShell-galéria támogatja a csomagok közvetlen letöltését a webhelyről a PowerShellGet-parancsmagok használata nélkül. A csomagokat letöltheti NuGet Package (`.nupkg`) fájlként, amelyet aztán egy belső tárházba másolhat.

> [!NOTE]
> A manuális csomagok letöltése **nem** helyettesíti a `Install-Module` parancsmagot.
> A csomag letöltése nem telepíti a modult vagy a parancsfájlt. A NuGet csomag nem tartalmazza a függőségeket. A következő utasítások csak referenciául szolgálnak.

## <a name="using-manual-download-to-acquire-a-package"></a>Manuális Letöltés használata csomag beolvasásához

Minden oldalon a manuális letöltésre mutató hivatkozás található, ahogy az itt látható:

![Manuális Letöltés](../../Images/packagedisplaypagewithpseditions.png)

A manuális letöltéshez kattintson a **RAW nupkg fájl letöltése**elemre. A rendszer átmásolja a csomag egy példányát a böngésző letöltési mappájába a névvel `<name>.<version>.nupkg`.

A NuGet-csomag egy ZIP-archívum, amely további, a csomag tartalmával kapcsolatos információkat tartalmazó fájlokat tartalmaz. Egyes böngészők, például az Internet Explorer, automatikusan lecserélik a `.zip`fájlkiterjesztést a `.nupkg` következővel:. A csomag kibontásához nevezze át `.nupkg` a `.zip`fájlt, ha szükséges, majd bontsa ki a tartalmat egy helyi mappába.

A NuGet-csomagfájl a következő **NuGet-specifikus elemeket** tartalmazza, amelyek nem részei az eredeti csomagolt kódnak:

- Egy nevű `_rels` mappa – tartalmaz egy `.rels` fájlt, amely felsorolja a függőségeket.
- Egy nevű `package` mappa – tartalmazza a NuGet-specifikus adatkészletet.
- Egy nevű `[Content_Types].xml` fájl – leírja, hogyan működik együtt a PowerShellGet a NuGet-mel
- Egy nevű `<name>.nuspec` fájl – a metaadatok nagy részét tartalmazza.

## <a name="installing-powershell-modules-from-a-nuget-package"></a>PowerShell-modulok telepítése NuGet-csomagból

> [!NOTE]
> Ezek az utasítások **nem** adják meg ugyanazt az eredményt, `Install-Module`mint a Futtatás. Ezek az utasítások megfelelnek a minimális követelményeknek. Nem helyettesíti a következőt: `Install-Module`.
> A `Install-Module` nem tartalmaz néhány lépést.

A legegyszerűbb módszer a NuGet-specifikus elemek eltávolítása a mappából. Az elemek eltávolítása elhagyja a csomag szerzője által létrehozott PowerShell-kódot.
A NuGet-specifikus elemek listáját lásd: a [manuális Letöltés használata a csomagok beolvasásához](#using-manual-download-to-acquire-a-package).

A lépések a következők:

1. Bontsa ki a NuGet-csomag tartalmát egy helyi mappába.
2. Törölje a NuGet-specifikus elemeket a mappából.
3. Nevezze át a mappát. Az alapértelmezett mappa neve általában `<name>.<version>`. A verzió tartalmazhat `-prerelease` , ha a modul előzetes verzióként van megjelölve. Nevezze át a mappát csak a modul nevére. Például `azurerm.storage.5.0.4-preview` a következő lesz `azurerm.storage`:.
4. Másolja a mappát az egyik mappájába `$env:PSModulePath value`. `$env:PSModulePath`a egy pontosvesszővel tagolt készlet, amelyben a PowerShellnek a modulokat kell keresnie.

> [!IMPORTANT]
> A manuális letöltés nem tartalmazza a modul által igényelt függőségeket. Ha a csomag függőségei vannak, a modul megfelelő működéséhez telepítve kell lennie a rendszeren. A PowerShell-galéria megjeleníti a csomag által igényelt összes függőséget.

## <a name="installing-powershell-scripts-from-a-nuget-package"></a>PowerShell-parancsfájlok telepítése NuGet-csomagból

> [!NOTE]
> Ezek az utasítások **nem** adják meg ugyanazt az eredményt, `Install-Script`mint a Futtatás. Ezek az utasítások megfelelnek a minimális követelményeknek. Nem helyettesíti a következőt: `Install-Script`.

A legegyszerűbb módszer a NuGet-csomag kibontása, majd közvetlenül a szkript használata.

A lépések a következők:

1. Bontsa ki a NuGet-csomag tartalmát.
2. A mappában található fájl közvetlenül ezen a helyen használható. `.PS1`
3. A mappában lévő NuGet-specifikus elemeket is törölheti.

A NuGet-specifikus elemek listáját lásd: a [manuális Letöltés használata a csomagok beolvasásához](#using-manual-download-to-acquire-a-package).

> [!IMPORTANT]
> A manuális letöltés nem tartalmazza a modul által igényelt függőségeket. Ha a csomag függőségei vannak, a modul megfelelő működéséhez telepítve kell lennie a rendszeren. A PowerShell-galéria megjeleníti a csomag által igényelt összes függőséget.
