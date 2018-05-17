---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Új forgatókönyvek és funkciók a WMF 5.1
ms.openlocfilehash: 77b439e61c5802f8ddbc4a0f39923cc8c0c36fe9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="new-scenarios-and-features-in-wmf-51"></a>Új forgatókönyvek és funkciók a WMF 5.1

> Megjegyzés: A rendszer előzetes és bármikor megváltozhat.

## <a name="powershell-editions"></a>PowerShell-kiadások

Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.

- **Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.
- **Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.

**További tudnivalók a PowerShell verziójával**

- [Határozza meg a PowerShell használatával $PSVersionTable futó kiadása](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [Get-Module eredmény által PSEdition paraméter használatával CompatiblePSEditions szűrése](/powershell/module/microsoft.powershell.core/get-module)
- [Megakadályozza a parancsfájl végrehajtása, kivéve, ha egy kompatibilis PowerShell kiadásán futtatása](/powershell/gallery/psget/script/scriptwithpseditionsupport)
- [A modul kompatibilitási adott PowerShell verziókra deklarálható](/powershell/gallery/psget/module/modulewithpseditionsupport)

## <a name="catalog-cmdlets"></a>Katalógus-parancsmagok

Két új parancsmagokkal bővült a a [Microsoft.PowerShell.Security](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security) modul; ezek létrehozása és a Windows katalógusban fájlok érvényesítése.

### <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

Új FileCatalog fájlt hoz létre a Windows katalógusban mappák és fájlok.
Ez a katalógus fájl tartalmazza az összes fájl megadott elérési utak a kivonatok.
Az ezeken a mappákon jelölő megfelelő katalógusfájlt együtt mappák készletét terjeszthetnek.
Ez az információ akkor hasznos, ellenőrzése, hogy bármely módosult a mappák katalógus létrehozása óta.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

1. és 2-katalógus verziókat támogatja.
1-es verziójú az SHA1 kivonatoló algoritmus segítségével hozza létre a fájlkivonat; 2-es verzióját használja az SHA-256.
Katalógus 2-es verzió nem támogatott a *Windows Server 2008 R2* vagy *Windows 7*.
A katalógus 2-es verzióját kell használnia *Windows 8*, *Windows Server 2012*, és annál újabb operációs rendszereken.

![](../images/NewFileCatalog.jpg)

Ez a katalógus fájlt hoz létre.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Katalógusfájlt (Pester.cat a fenti példában) sértetlenségének ellenőrzéséhez használatával írja alá [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) parancsmag.

### <a name="test-filecatalog"></a>Test-FileCatalog
--------------------------------

Teszt-FileCatalog érvényesíti a katalógus képviselő mappákat.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Ez a parancsmag összehasonlítja a fájlok kivonatok és azok relatív elérési utak található *katalógus* az azokat a *lemez*.
Ha a fájlkivonat és elérési utak bármely eltérést észlel a állapotának adja vissza *ValidationFailed*.
Felhasználók használatával kérheti le ezt az információt a *-részletes* paraméter.
Azt is állapotát jeleníti meg az aláíró katalógust a *aláírás* tulajdonság, amely egyenértékű hívása [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) parancsmag a katalógus fájlra.
Felhasználók is hagyhatja a fájl ellenőrzésekor használatával a *- FilesToSkip* paraméter.

## <a name="module-analysis-cache"></a>A modul elemzés gyorsítótár

WMF 5.1 verziótól kezdődően PowerShell segítségével szabályozhatja, a fájl, amellyel egy modul, mint például a parancsok kivitt gyorsítótár adatait.

Alapértelmezés szerint ez a gyorsítótár a fájlban tárolt `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
A gyorsítótár indításkor parancs keresése során általában olvasható nevével, és a háttérszálon az némi várakozás után egy modul importálása.

A gyorsítótár alapértelmezett helyének módosításához állítsa a `$env:PSModuleAnalysisCachePath` környezeti változó PowerShell indítása előtt.
A környezeti változó módosítása csak hatással gyermekei folyamat.
Az érték egy teljes elérési útja (többek között a következőket fájlnév), amely PowerShell jogosult létrehozásához és írásához fájlok nevet.
Tiltsa le a gyorsítótárban, állítsa be az érték érvénytelen helyre, például:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Ez beállítja az elérési út érvénytelen eszközök számára.
PowerShell az elérési út nem lehet írni, ha nincs hibát ad vissza, de egy követő használatával hibajelentési láthatja:

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

A gyorsítótár írása, PowerShell ellenőrzi a modulok, amely egy feleslegesen gyorsítótár elkerülése érdekében a továbbiakban nem létezik.
Az ellenőrzések sokszor nem kívánatos, ebben az esetben kikapcsolható őket úgy, hogy:

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

A környezeti változó beállítása azonnali hatállyal érvénybe a jelenlegi folyamatban.

## <a name="specifying-module-version"></a>Modul verzió megadása

A WMF 5.1 `using module` ugyanúgy, mint más a PowerShell modul kapcsolatos építmények viselkedik.
Adjon meg egy adott modulban verziót; semmilyen módon nem volt korábban Ha több verziója található, akkor ez hibát eredményezett.

A WMF 5.1:

- Használhat [ModuleSpecification konstruktor (hibás)](https://msdn.microsoft.com/library/jj136290).
A kivonattábla formátuma, `Get-Module -FullyQualifiedName`.

**Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- Ha a modul több verziója is van, a PowerShell használja a **logikák feloldási** , `Import-Module` nem ad visszatérési hiba – a kívánt viselkedést eredményező beállítást, és `Import-Module` és `Import-DscResource`.

## <a name="improvements-to-pester"></a>Pester fejlesztései

WMF 5.1, a PowerShell-lel részét képező Pester verziója 3.4.0 véglegesítés azonban kiegészül a 3.3.5 megújult https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, amely lehetővé teszi, hogy jobb viselkedését a Nano Server Pester a.

Ellenőrizze a ChangeLog.md fájlban a következő verziók 3.3.5 való 3.4.0 változásai tekinthetők át: https://github.com/pester/Pester/blob/master/CHANGELOG.md
