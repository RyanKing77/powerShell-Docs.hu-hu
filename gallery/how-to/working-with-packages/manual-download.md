---
ms.date: 09/11/2018
contributor: JKeithB
keywords: katalógus, a powershell, a psgallery
title: Csomagok manuális letöltése
ms.openlocfilehash: 57baa14089b803f58c42ccb54553ecace841e34b
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742822"
---
# <a name="manual-package-download"></a>Csomagok manuális letöltése

A Powershell-galériából támogatja a webhely a csomag közvetlenül, letölti a PowerShellGet-parancsmagok használata nélkül. Minden olyan csomag, a NuGet csomag (.nupkg) fájlt, amely majd másolhat egy belső tárházat töltheti le.

> [!NOTE]
> Manuális csomag a Letöltés **nem** szánt az Install-Module parancsmaggal helyettesítője.
> A csomag letöltése nem telepíti a modult vagy parancsfájl. Függőségek nem szerepelnek a NuGet-csomag letöltése. Az alábbi utasítások csak tájékoztatási céllal van megadva.

## <a name="using-manual-download-to-acquire-a-package"></a>Manuális letöltés segítségével csomag beszerzése

Minden oldalnak van a manuális letöltéséhez, egy hivatkozás, itt látható módon:

![Manuális letöltés](../../Images/packagedisplaypagewithpseditions.png)

Manuális letöltéséhez kattintson a **töltse le a nyers nupkg**. A csomag másolatát másolta a letöltési mappa nevét a böngésző `<name>.<version>.nupkg`.

A NuGet-csomagot a csomag tartalma kapcsolatos információkat tartalmazó további fájlokat a ZIP-archívumot. Egyes böngészők, például az Internet Explorer, automatikusan cserélje le a `.nupkg` kiterjesztése a `.zip`. Bontsa ki a csomagot, nevezze át a `.nupkg` fájlt `.zip`, ha szükséges, bontsa ki a tartalmát egy helyi mappába.

A NuGet csomag fájlt a következő NuGet-specifikus elemeket, amelyek nem részei az eredeti csomagolt kódot tartalmazza:

- Nevű mappa `_rels` -tartalmaz egy `.rels` fájlt, amely felsorolja a függőségeket
- Nevű mappa `package` -NuGet-specifikus adatait tartalmazza
- Nevű fájl `[Content_Types].xml` -ismerteti, hogyan működnek a PowerShellGet-kiterjesztése a NuGet
- Nevű fájl `<name>.nuspec` -metaadatok tömeges tartalmaz

## <a name="installing-powershell-modules-from-a-nuget-package"></a>A NuGet-csomagot a PowerShell-modulok telepítése

> [!NOTE]
> Ezek az utasítások **nem** futtatásával ugyanazt az eredményt adja `Install-Module`. Ezek az utasítások megfelelnek a minimális követelményeknek. Ezek nem tartozhat helyettesítheti a `Install-Module`. Néhány által végrehajtott lépések `Install-Module` nem szerepelnek.

A legegyszerűbb megközelítés, hogy távolítsa el a NuGet-specifikus elemek. A PowerShell-kóddal, a csomagot a szerző által létrehozott kihasználatlan marad. A lépések a következők:

1. Bontsa ki a tartalmát egy helyi mappába a NuGet-csomagot.
2. A NuGet-specifikus elemeket törölje a mappát.
3. Nevezze át a mappát. Az alapértelmezett mappa neve: általában `<name>.<version>`. A verzió lehetnek "– előzetes" Ha a modul előzetes verziójának van megjelölve. Nevezze át a mappát csak a modul nevét. Például a "azurerm.storage.5.0.4-preview" "azurerm.storage" lesz.
4. Másolja a mappát a található mappák közül a `$env:PSModulePath value`. `$env:PSModulePath` az elérési utak, amelyben PowerShell modulok kell keresnie egy pontosvesszővel elválasztott csoportja.

> [!IMPORTANT]
> A Manuális letöltés nem tartalmazza a modul által igényelt függőségek. Ha a csomag függőségekkel rendelkezik, a rendszer, hogy megfelelően működjön a modul csak telepíthető. A PowerShell-galériából jeleníti meg a csomag által igényelt összes függőségét.

## <a name="installing-powershell-scripts-from-a-nuget-package"></a>A NuGet-csomagot a PowerShell-parancsprogramok telepítése

> [!NOTE]
> Ezek az utasítások **nem** futtatásával ugyanazt az eredményt adja `Install-Script`. Ezek az utasítások megfelelnek a minimális követelményeknek. Ezek nem tartozhat helyettesítheti a `Install-Script`.

A legegyszerűbb megközelítés közvetlenül, hogy a kivonatot a NuGet-csomagot, majd használja a szkriptet. A lépések a következők:

1. Bontsa ki a NuGet-csomag tartalmát.
2. A `.PS1` mappában található fájl közvetlenül a következő helyről is használható.
3. Előfordulhat, hogy törli a NuGet-specifikus elemek a mappában.

> [!IMPORTANT]
> A Manuális letöltés nem tartalmazza a modul által igényelt függőségek. Ha a csomag függőségekkel rendelkezik, a rendszer, hogy megfelelően működjön a modul csak telepíthető. A PowerShell-galériából jeleníti meg a csomag által igényelt összes függőségét.
