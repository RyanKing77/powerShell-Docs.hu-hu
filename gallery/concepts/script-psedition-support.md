---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Parancsfájl-kompatibilis PowerShell-kiadások
ms.openlocfilehash: e364879f611429a8583e550fb7704431e456fbb1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084691"
---
# <a name="script-with-compatible-powershell-editions"></a>Parancsfájl-kompatibilis PowerShell-kiadások

Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.

- **Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.

- **Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.

A futtatott PowerShell-verzió a $PSVersionTable PSEdition tulajdonságában jelenik meg.

```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

Szkriptkészítők megakadályozhatja a parancsfájl végrehajtása, ha a PowerShell használatával a PSEdition paraméterrel a kompatibilis kiadásán fut egy `#requires` utasítást.

```powershell
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core
Get-Process -Name PowerShell"
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

PowerShell-galériából felhasználók megtalálhassák a parancsfájlokat egy adott PowerShell kiadás támogatott listáját.
Parancsfájlok PSEdition_Desktop és PSEdition_Core címkék nélküli jól működnek az PowerShell Desktop kiadás minősülnek.

```powershell
# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEdition_Desktop

# Find scripts supported on PowerShell Core edition
Find-Script -Tag PSEdition_Core
```

## <a name="more-details"></a>További részletek

- [PSEditions paraméterrel rendelkező modulok](module-psedition-support.md)
- [Pseditions paraméterrel támogatja a PowerShell-Galériabeli](../how-to/finding-packages/searching-by-compatibility.md)
