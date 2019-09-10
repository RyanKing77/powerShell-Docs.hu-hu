---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.x kiadási megjegyzései
ms.openlocfilehash: 8924240a4bbedcd34bc68b7cacdd23189a3716d6
ms.sourcegitcommit: 00083f07b13c73b86936e7d7307397df27c63c04
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848156"
---
# <a name="windows-management-framework-wmf-5x-release-notes"></a>Windows Management Framework (WMF) 5. x kibocsátási megjegyzések

## <a name="wmf-50-changes"></a>WMF 5,0-változások

- A PowerShell 5,0 új strukturált **információs** streamet hoz létre
- A DSC fejlesztése, beleértve a négy új DSC-erőforrást:
  - WindowsFeatureSet
  - WindowsOptionalFeatureSet
  - ServiceSet
  - ProcessSet
- Elég felügyeletet adott hozzá a Szerepköralapú felügyelet engedélyezéséhez a PowerShell távelérés használatával
- A PowerShell 5,0 kiterjeszti a nyelvet a felhasználó által definiált osztályok és enumerálások belefoglalására.
- Továbbfejlesztett hibakeresési funkciók a PowerShell ISE-ben és távoli hibakeresés hozzáadva
- A PowerShellGet és a PackageManagement modulok hozzáadása
- Továbbfejlesztett PowerShell-parancsfájlok naplózása és átiratai
- Titkosítási üzenet Szintaxisi parancsmagjainek hozzáadása
- A WMF 5,0 tartalmazza a Windows NetworkSwitchManager modulját
- A Microsoft. PowerShell. ODataUtils modul hozzáadva
- A szoftveres leltár naplózásának (SIL) támogatása
- Új vagy frissítési parancsmagok replikálása a felhasználói kérésekre és problémákra válaszul

## <a name="wmf-51-changes"></a>WMF 5,1-változások

A WMF 5,1 magában foglalja a Windows Server 2016-ben kiadott PowerShell-, WMI-, WinRM-és szoftveres leltár-naplózási (SIL) összetevőket. A WMF 5,1 a Windows 7, a Windows 8,1, a Windows Server 2008 R2, az 2012 és az 2012 R2 rendszerre telepíthető, és számos javítást biztosít a WMF 5,0-hez, beleértve a következőket:

- Új parancsmagok
- A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése
- A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat
- DSC- és PowerShell-osztályok hibakeresési javításai
- Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén
- Válaszok néhány felhasználói kérésre és problémára

> [!IMPORTANT]
> Mielőtt telepítené a WMF 5,1-et a Windows Server 2008 vagy a Windows 7 rendszerre, győződjön meg róla, hogy a WMF 3,0 nincs telepítve. További információ: [a Windows Server 2008 R2 SP1 és a Windows 7 SP1 rendszerhez készült WMF 5,1 előfeltételei](../setup/install-configure.md#wmf-51-prerequisites-for-windows-server-2008-r2-sp1-and-windows-7-sp1).

## <a name="powershell-editions"></a>PowerShell-kiadások

A 5,1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platform-kompatibilitást jeleznek.

- **Asztali kiadás:** A .NET-keretrendszerre épülő, valamint a Windows teljes helyigényű, például a Server Core és a Windows Desktop szolgáltatásban futó PowerShell-verzióit célzó parancsfájlok és modulok kompatibilitását teszi lehetővé.
- **Core kiadás:** A .NET Core-ra épülő, valamint a Windows csökkentett lábnyomú kiadásain futó PowerShell-verziókkal való kompatibilitást biztosító parancsfájlokkal és modulokkal kompatibilis, például a nano Server és a Windows IoT.

### <a name="learn-more-about-using-powershell-editions"></a>További információ a PowerShell-kiadások használatáról

- [A PowerShell futtatási kiadásának meghatározása $PSVersionTable használatával](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [A Get-Module eredményeinek szűrése CompatiblePSEditions alapján a PSEdition paraméter használatával](/powershell/module/microsoft.powershell.core/get-module)
- [Parancsfájlok végrehajtásának megakadályozása, ha a PowerShell kompatibilis változatán fut](/powershell/gallery/concepts/script-psedition-support)
- [Modul kompatibilitásának deklarálása adott PowerShell-verziókhoz](/powershell/gallery/concepts/module-psedition-support)

## <a name="module-analysis-cache"></a>Modul elemzési gyorsítótára

A WMF 5,1-től kezdve a PowerShell szabályozza a modul adatainak gyorsítótárazásához használt fájlt, például az általa exportált parancsokat.

Alapértelmezés szerint a fájl `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`tárolja a gyorsítótárat. A gyorsítótár általában indításkor a parancs keresésekor történik, és egy modul importálása után egy háttérbeli szálon van írva.

A gyorsítótár alapértelmezett helyének módosításához állítsa a `$env:PSModuleAnalysisCachePath` környezeti változót a PowerShell elindítása előtt. A környezeti változó módosításai csak a gyermekeket érintő folyamatokat érintik. Az értéknek egy teljes elérési utat (a fájlnevet is beleértve) kell megjelennie, amelyet a PowerShell jogosult fájlok létrehozására és írására. A fájl gyorsítótárának letiltásához állítsa ezt az értéket érvénytelen helyre, például:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Ez egy érvénytelen eszköz elérési útját állítja be. Ha a PowerShell nem tud írni az elérési útra, a rendszer nem ad vissza hibát, de a következőt láthatja: nyomjelző használatával.

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

A gyorsítótár kiírásakor a PowerShell megkeresi azokat a modulokat, amelyek már nem léteznek a szükségtelenül nagy gyorsítótár elkerüléséhez. Előfordulhat, hogy ezek az ellenőrzések nem kívánatosak, ebben az esetben a következő beállítással lehet kikapcsolni:

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

A környezeti változó beállítása azonnal érvénybe lép az aktuális folyamatban.

## <a name="specifying-module-version"></a>Modul verziószámának meghatározása

A WMF 5,1- `using module` ben ugyanúgy viselkedik, mint az egyéb modulokkal kapcsolatos szerkezetek a PowerShellben.
Korábban nem volt lehetőség egy adott modul verziójának megadására; Ha több verzió is létezik, ez hibát eredményezett.

WMF 5,1 esetén:

- Használhatja a [ModuleSpecification konstruktort (szórótábla)](/dotnet/api/microsoft.powershell.commands.modulespecification.-ctor?view=powershellsdk-1.1.0#Microsoft_PowerShell_Commands_ModuleSpecification__ctor_System_Collections_Hashtable_).

  Ez a kivonatoló tábla formátuma `Get-Module -FullyQualifiedName`megegyezik a következővel:.

  **Példa:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- Ha a modul több verziója is létezik, a PowerShell ugyanazt a **feloldási logikát** használja, mint `Import-Module` a, és nem ad vissza hibát – ugyanaz `Import-DscResource`a viselkedés, mint `Import-Module` a és a.

## <a name="improvements-to-pester"></a>A Pest fejlesztése

A WMF 5,1-ben a PowerShell-lel rendelkező, a 3.3.5-ről a 3.4.0-re irányuló zaklató verziója frissült.
Ez a frissítés lehetővé teszi, hogy a nano Serveren a zaklatás jobb viselkedést biztosítson.

A kártevők változásait a GitHub-tárházban található [changelog](https://github.com/pester/Pester/blob/master/CHANGELOG.md) ellenőrizheti.
