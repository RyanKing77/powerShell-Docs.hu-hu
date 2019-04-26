---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Új forgatókönyvek és funkciók a WMF 5.1
ms.openlocfilehash: b00069aad7422f86d1462a62a6c4bc8a91e46705
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085454"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a>Új forgatókönyvek és funkciók a WMF 5.1

> Megjegyzés: Ezek az információk előzetesek, és változhat a tartalmuk.

## <a name="powershell-editions"></a>PowerShell-kiadások

Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.

- **Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.
- **Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.

**További tudnivalók a PowerShell-kiadások használatával**

- [Határozza meg a PowerShell használatával $PSVersionTable futó kiadása](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [Get-Module eredmények által PSEdition paraméterrel CompatiblePSEditions szűrése](/powershell/module/microsoft.powershell.core/get-module)
- [Parancsfájl végrehajtása megakadályozása, ha a PowerShell kompatibilis kiadásán futtatása](/powershell/gallery/concepts/script-psedition-support)
- [Deklarálja a verziókkal PowerShell-modul kompatibilitás](/powershell/gallery/concepts/module-psedition-support)

## <a name="catalog-cmdlets"></a>Katalógusbeli parancsmagok

Két új parancsmagot a lettek hozzáadva a [Microsoft.PowerShell.Security](/powershell/module/microsoft.powershell.security) modul; ezek létrehozása és a Windows katalógusban fájlok érvényesítése.

### <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

Új FileCatalog fájlt hoz létre Windows catalog az tartozó fájlokat és mappákat.
A katalógus-fájl tartalmazza az összes fájl megadott elérési utak a kivonatok.
Jelölő mappákat megfelelő katalógusfájlt együtt mappakészlet terjeszthetnek.
Ez az információ hasznos megállapítani, hogy e bármely módosultak a mappák katalógus létrehozása óta.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

1. és 2 katalógus verziók támogatottak.
1. verzió az SHA1 kivonatoló algoritmus segítségével hozza létre a fájlkivonat; 2. verzió SHA256 titkosítást használ.
Katalógus 2-es verzió nem támogatott az *Windows Server 2008 R2* vagy *Windows 7*.
A katalógus 2-es verziójú használjon *Windows 8*, *Windows Server 2012*, és annál újabb operációs rendszereken.

![](../images/NewFileCatalog.jpg)

Ez a katalógus fájlt hoz létre.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

A katalógus fájlt (Pester.cat a fenti példában) sértetlenségének ellenőrzése használatával írja alá [Set-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Set-AuthenticodeSignature) parancsmagot.

### <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

Test-FileCatalog érvényesíti a katalógus jelölő mappákat.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Ez a parancsmag a fájlok-kivonatok hasonlítja össze, és azok relatív elérési utakat található *katalógus* együtt megjelennek a *lemez*.
Ha azt észleli, hogy bármely fájlkivonatokkal és elérési utak nem egyezik, adja vissza, az állapot *ValidationFailed*.
Felhasználók használatával lekérhető ezt az információt a *– részletes* paraméter.
A katalógus aláíró állapotát is megjeleníti *aláírás* tulajdonság, amely egyenértékű hívása [Get-AuthenticodeSignature](/powershell/module/Microsoft.PowerShell.Security/Get-AuthenticodeSignature) katalógusfájl parancsmagot.
Felhasználók ki is hagyhatja bármely fájl ellenőrzésekor használatával a *- FilesToSkip* paraméter.

## <a name="module-analysis-cache"></a>A modul elemzési gyorsítótár

A WMF 5.1-es verziótól kezdődően PowerShell segítségével szabályozhatja, a fájl, amellyel egy modult, exportálja a parancsok például a gyorsítótár adatait.

Alapértelmezés szerint ez a gyorsítótár a fájlban tárolt `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
A gyorsítótár egy parancs keresése közben általában olvasható indításkor, és íródik a háttérbeli szálon némi várakozás után egy modul importálása kész.

Ha módosítani szeretné az alapértelmezett hely a gyorsítótár, állítsa be a `$env:PSModuleAnalysisCachePath` környezeti változót a PowerShell indítása előtt.
Ez a környezeti változó módosításai csak hatással lesz a gyermekek folyamatokat.
Az érték teljes elérési utat (például fájlnév), amely PowerShell jogosult hozhat létre és írhat fájlokat kell neve.
A fájlgyorsítótárban letiltásához állítsa be ezt az értéket érvénytelen helyre, például:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Ez az elérési út érvénytelen eszközön állítja be.
PowerShell az elérési út nem lehet írni, ha nincsenek hibát akkor adja vissza, de láthatja a hibajelentés a nyomkövető használatával:

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

Ki a gyorsítótár írásakor PowerShell modulok, amely már nem létezik egy szükségtelenül nagy méretű gyorsítótárak elkerülése érdekében ellenőrzi.
Egyes esetekben az ellenőrzések nem kívánatosak, ebben az esetben kikapcsolhatja azokat beállításával:

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

Ez a környezeti változó beállítása azonnal érvénybe a jelenlegi folyamatban.

## <a name="specifying-module-version"></a>A modul verzió megadása

A WMF 5.1 `using module` ugyanúgy, mint más a PowerShell modul kapcsolatos építmények működését.
Korábban a semmilyen módon nem lehet adjon meg egy adott modulban verziót; kellett Ha több verzió található, akkor ez hibát eredményezett.

A WMF 5.1:

- Használhat [ModuleSpecification konstruktor (szórótábla)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).
A kivonattábla rendelkezik felhasználónévként `Get-Module -FullyQualifiedName`.

**Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- Ha a modul több verziója van, használja a PowerShell a **ugyanez a logika felbontása** , `Import-Module` nem ad vissza hibát--viselkedést, és `Import-Module` és `Import-DscResource`.

## <a name="improvements-to-pester"></a>Pester fejlesztései

A WMF 5.1-es, a PowerShell-lel részét képező Pester verziója 3.4.0 véglegesítési igény szerinti hozzáadásával a 3.3.5 frissült https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, amely a Nano Serveren Pester jobb viselkedését.

Verziók 3.3.5 való 3.4.0 változásokat áttekintheti vizsgálatával szerezheti be a ChangeLog.md fájlban a következő: https://github.com/pester/Pester/blob/master/CHANGELOG.md
