---
ms.date: 03/28/2019
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Kompatibilis PowerShell-kiadások rendelkező modulok
ms.openlocfilehash: 425588c168a4f864fdc0c52aa53cfd748b80dc98
ms.sourcegitcommit: f268dce5b5e72be669be0c6634b8db11369bbae2
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/29/2019
ms.locfileid: "58623840"
---
# <a name="modules-with-compatible-powershell-editions"></a>Kompatibilis PowerShell-kiadások rendelkező modulok

Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.

- **Desktop kiadás:** .NET-keretrendszer épül, a Windows PowerShell 4.0 és az alábbiakban vonatkozik, valamint a Windows PowerShell 5.1 Windows asztali, Windows Server, a Windows Server Core és a legtöbb más Windows-kiadások.
- **Core kiadás:** .NET Core-on fejlesztett, vonatkozik PowerShell Core 6.0-s vagy újabb verzióhoz Windows PowerShell 5.1-es és a csökkentett erőforrás-igényű Windows kiadások, mint például a Windows IoT- és Windows Nanoserver.

A PowerShell-kiadások további információkért lásd: [about_PowerShell_Editions][].

## <a name="declaring-compatible-editions"></a>Deklaráló kompatibilis verziója esetén

A modulkészítők a CompatiblePSEditions moduljegyzékkulcs segítségével deklarálhatják, hogy a moduljaik mely PowerShell-kiadással vagy -kiadásokkal kompatibilisek. Ez a kulcs csak a PowerShell 5.1-es vagy újabb verzióin támogatott.

> [!NOTE]
> Miután egy moduljegyzék CompatiblePSEditions a kulccsal van megadva, nem importálható lesz alatt és a PowerShell-verziókról 4.

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
```

```Output
Desktop
Core
```

```powershell
$ModuleInfo | Get-Member CompatiblePSEditions
```

```Output
   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}
```

Az elérhető modulok listáját szűrheti a PowerShell-kiadás alapján.

```powershell
Get-Module -ListAvailable -PSEdition Desktop
```

```Output
    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions
```

```powershell
Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
```

```Output
Desktop
Core
```

## <a name="targeting-multiple-editions"></a>Célzás több kiadás

A modul szerzők esetleg mindkét PowerShell-kiadások (asztalon és Core) célzó egy modul teheti közzé.

Egy modul dolgozhat asztali és a Core kiadás, az adott modul Szerző hozzáadásához szükséges logikát, vagy a RootModule, vagy a moduljegyzékben $PSEdition változóval rendelkezik. Modulok lefordított DLL-ek CoreCLR-és FullCLR két készletnyi is rendelkezhet. Az alábbiakban a több, a modul megfelelő DLL betöltésére szolgáló logikai csomag lehetőség közül választhat.

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a>1. lehetőség: A célcsoport-kezelési több verziói és több a PowerShell modul csomagolása

A modul mappa tartalma

- Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll
- Microsoft.Windows.PowerShell.ScriptAnalyzer.dll
- PSScriptAnalyzer.psd1
- PSScriptAnalyzer.psm1
- ScriptAnalyzer.format.ps1xml
- ScriptAnalyzer.types.ps1xml
- coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll
- coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll
- en-US\about_PSScriptAnalyzer.help.txt
- en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml
- PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll
- PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll
- Settings\CmdletDesign.psd1
- Settings\DSC.psd1
- Settings\ScriptFunctions.psd1
- Settings\ScriptingStyle.psd1
- Settings\ScriptSecurity.psd1

PSScriptAnalyzer.psd1 fájl tartalma

```powershell
@{

# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

Alább logikai betölti a szükséges szerelvényeket, attól függően, a jelenlegi kiadása vagy verziója.

PSScriptAnalyzer.psm1 fájl tartalma:

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0')
    {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
}
```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a>2. lehetőség: A psd1 kiterjesztésű fájl $PSEdition változó segítségével a megfelelő DLL-EK és a beágyazott/szükséges modulok betöltése

A PS 5.1-es vagy újabb a modul jegyzékfájl $PSEdition globális változó használata engedélyezett. Használja ezt a változót, a modul Szerző értékeket adhat meg a feltételes modul jegyzékfájl. A korlátozott nyelvmód vagy adatok szakasz $PSEdition változó lehet hivatkozni.

> [!NOTE]
> Miután egy moduljegyzék a CompatiblePSEditions kulcs meg van adva, vagy használja a `$PSEdition` változó, nem importálható lesz a kisebb PowerShell-verziókat.

Minta modul jegyzékfájl CompatiblePSEditions kulccsal

```powershell
@{
    # Script module or binary module file associated with this manifest.
    RootModule = if($PSEdition -eq 'Core')
    {
        'coreclr\MyCoreClrRM.dll'
    }
    else # Desktop
    {
        'clr\MyFullClrRM.dll'
    }

    # Supported PSEditions
    CompatiblePSEditions = 'Desktop', 'Core'

    # Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
    NestedModules = if($PSEdition -eq 'Core')
    {
        'coreclr\MyCoreClrNM1.dll',
        'coreclr\MyCoreClrNM2.dll'
    }
    else # Desktop
    {
        'clr\MyFullClrNM1.dll',
        'clr\MyFullClrNM2.dll'
    }
}
```

### <a name="module-contents"></a>A modul tartalma

```powershell
dir -Recurse
```

```Output
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
d-----    7/5/2016   1:37 PM          clr
d-----    7/5/2016   1:36 PM          coreclr
-a----    7/5/2016   1:34 PM     4906 ModuleWithEditions.psd1

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr

Mode           LastWriteTime    Length Name
----           -------------    ------ ----
-a----    7/5/2016   1:35 PM         0 MyFullClrNM1.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrNM2.dll
-a----    7/5/2016   1:35 PM         0 MyFullClrRM.dl

    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr

Mode           LastWriteTime   Length Name
----           -------------   ------ ----
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM1.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrNM2.dll
-a----    7/5/2016   1:35 PM        0 MyCoreClrRM.dl
```

PowerShell-galériából felhasználók egy adott PowerShell kiadás támogatott modulok listáját megtalálhatja, PSEdition_Desktop és PSEdition_Core címkék használatával.

Modulok PSEdition_Desktop és PSEdition_Core címkék nélküli minősülnek jól működnek az PowerShell asztali verziója esetén.

```powershell
# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEdition_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEdition_Core
```

## <a name="more-details"></a>További részletek

[PSEditions paraméterrel rendelkező parancsfájlok](script-psedition-support.md)

[Pseditions paraméterrel támogatja a PowerShell-Galériabeli](../how-to/finding-packages/searching-by-compatibility.md)

[Moduljegyzék frissítése](/powershell/module/powershellget/update-modulemanifest)

[about_PowerShell_Editions][]

[about_PowerShell_Editions]: /powershell/module/Microsoft.PowerShell.Core/About/about_PowerShell_Editions
