---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.x kibocsátási megjegyzései
ms.openlocfilehash: 8bdc423234cf0b104b72b1bee1de35e50783d8a4
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856398"
---
# <a name="windows-management-framework-wmf-5x-release-notes"></a>Windows Management Framework (WMF) 5.x kiadási megjegyzései

## <a name="wmf-50-changes"></a>A WMF 5.0 változik

- PowerShell 5.0 hozzáad egy új strukturált **információk** stream
- DSC, beleértve a négy új DSC-erőforrások fejlesztései:
  - WindowsFeatureSet
  - WindowsOptionalFeatureSet
  - ServiceSet
  - ProcessSet
- A hozzáadott Just Enough Administration – PowerShell-távelérés szerepkör alapú felügyelet engedélyezése
- PowerShell 5.0 terjeszti ki a nyelvet, a felhasználó által definiált osztályok és enumerálásokat tartalmaznak
- Továbbfejlesztett hibakeresés a PowerShell ISE-ben és az új távoli hibakeresési funkciók
- A PowerShellGet és a PackageManagement-modulok hozzáadása
- PowerShell-parancsfájl a továbbfejlesztett naplózás és szövegekben
- Titkosítási Message Syntax-parancsmagok hozzáadása
- A WMF 5.0 a NetworkSwitchManager modult tartalmaz a Windows
- A Microsoft.PowerShell.ODataUtils modul hozzáadása
- Támogatás hozzáadva a szoftverleltár-naplózási (SIL)
- Új-kiszolgálóhoz, vagy felhasználói kérésre és problémára válaszul parancsmagok frissítése

## <a name="wmf-51-changes"></a>A WMF 5.1 változik

A WMF 5.1 összetevői a PowerShell, a WMI, a Rendszerfelügyeleti webszolgáltatások és a szoftverleltár-naplózási (SIL) kiadott – Windows Server 2016-ban. A WMF 5.1 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 és 2012 R2 telepíthető, és felett, beleértve a WMF 5.0 számos fejlesztést tartalmaz:

- Új parancsmagok
- A PowerShellGet javításai, többek között az aláírt modulok használatának kényszerítése és a JEA-modulok telepítése
- A PackageManagement mostantól támogatja a Containers szolgáltatást, a CBS-beállítást, az EXE-alapú beállítást és a CAB-csomagokat
- DSC- és PowerShell-osztályok hibakeresési javításai
- Biztonsági fejlesztések: katalógus által aláírt modulok használatának kényszerítése a lekérési kiszolgálóról érkező modulok, illetve PowerShellGet-parancsmagok használata esetén
- Válaszok néhány felhasználói kérésre és problémára

## <a name="powershell-editions"></a>PowerShell-kiadások

5.1-es verziótól kezdődően PowerShell érhető el a különböző kiadásait, amelyek különböző szolgáltatáskészleteket és a platformkompatibilitásra jelöl.

- **Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.
- **Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.

### <a name="learn-more-about-using-powershell-editions"></a>További tudnivalók a PowerShell-kiadások használatával

- [Határozza meg a PowerShell használatával $PSVersionTable futó kiadása](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [Get-Module eredmények által PSEdition paraméterrel CompatiblePSEditions szűrése](/powershell/module/microsoft.powershell.core/get-module)
- [Parancsfájl végrehajtása megakadályozása, ha a PowerShell kompatibilis kiadásán futtatása](/powershell/gallery/concepts/script-psedition-support)
- [Deklarálja a verziókkal PowerShell-modul kompatibilitás](/powershell/gallery/concepts/module-psedition-support)

## <a name="module-analysis-cache"></a>A modul elemzési gyorsítótár

A WMF 5.1-es verziótól kezdődően PowerShell segítségével szabályozhatja, a fájl, amellyel egy modult, exportálja a parancsok például a gyorsítótár adatait.

Alapértelmezés szerint ez a gyorsítótár a fájlban tárolt `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`. A gyorsítótár egy parancs keresése közben általában olvasható indításkor, és íródik a háttérbeli szálon némi várakozás után egy modul importálása kész.

Ha módosítani szeretné az alapértelmezett hely a gyorsítótár, állítsa be a `$env:PSModuleAnalysisCachePath` környezeti változót a PowerShell indítása előtt. Ez a környezeti változó módosításai csak hatással lesz a gyermekek folyamatokat. Az érték teljes elérési utat (például fájlnév), amely PowerShell jogosult hozhat létre és írhat fájlokat kell neve. A fájlgyorsítótárban letiltásához állítsa be ezt az értéket érvénytelen helyre, például:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Ez az elérési út érvénytelen eszközön állítja be. PowerShell az elérési út nem lehet írni, ha nincsenek hibát akkor adja vissza, de láthatja a hibajelentés a nyomkövető használatával:

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

Ki a gyorsítótár írásakor PowerShell modulok, amely már nem létezik egy szükségtelenül nagy méretű gyorsítótárak elkerülése érdekében ellenőrzi. Egyes esetekben az ellenőrzések nem kívánatosak, ebben az esetben kikapcsolhatja azokat beállításával:

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

A WMF 5.1-es verziója a PowerShell-lel részét képező Pester frissült a 3.3.5 3.4.0.
Ez a frissítés lehetővé teszi, hogy jobb viselkedés a Pester a Nano Serveren.

Áttekintheti a módosításokat a kártevők vizsgálatával szerezheti be a [változásnaplójában](https://github.com/pester/Pester/blob/master/CHANGELOG.md) a GitHub-adattárában.
