---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Parancsfájl-kompatibilis PowerShell-kiadások
ms.openlocfilehash: e364879f611429a8583e550fb7704431e456fbb1
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686634"
---
# <a name="script-with-compatible-powershell-editions"></a><span data-ttu-id="1c719-103">Parancsfájl-kompatibilis PowerShell-kiadások</span><span class="sxs-lookup"><span data-stu-id="1c719-103">Script with compatible PowerShell editions</span></span>

<span data-ttu-id="1c719-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="1c719-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="1c719-105">**Desktop kiadás:** .NET-keretrendszer épül, és kompatibilis a Windows például a Server Core és a Windows asztal teljes erőforrás-igényű kiadásain fut PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="1c719-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>

- <span data-ttu-id="1c719-106">**Core kiadás:** .NET Core épül, és kompatibilis csökkentett erőforrás-igényű kiadása esetén például a Nano Server Windows és Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít.</span><span class="sxs-lookup"><span data-stu-id="1c719-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="1c719-107">A futtatott PowerShell-verzió a $PSVersionTable PSEdition tulajdonságában jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="1c719-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>

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

<span data-ttu-id="1c719-108">Szkriptkészítők megakadályozhatja a parancsfájl végrehajtása, ha a PowerShell használatával a PSEdition paraméterrel a kompatibilis kiadásán fut egy `#requires` utasítást.</span><span class="sxs-lookup"><span data-stu-id="1c719-108">Script authors can prevent a script from executing unless it is run on a compatible edition of PowerShell using the PSEdition parameter on a `#requires` statement.</span></span>

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

<span data-ttu-id="1c719-109">PowerShell-galériából felhasználók megtalálhassák a parancsfájlokat egy adott PowerShell kiadás támogatott listáját.</span><span class="sxs-lookup"><span data-stu-id="1c719-109">PowerShell Gallery users can find the list of scripts supported on a specific PowerShell Edition.</span></span>
<span data-ttu-id="1c719-110">Parancsfájlok PSEdition_Desktop és PSEdition_Core címkék nélküli jól működnek az PowerShell Desktop kiadás minősülnek.</span><span class="sxs-lookup"><span data-stu-id="1c719-110">Scripts without PSEdition_Desktop and PSEdition_Core tags are considered to work fine on PowerShell Desktop edition.</span></span>

```powershell
# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEdition_Desktop

# Find scripts supported on PowerShell Core edition
Find-Script -Tag PSEdition_Core
```

## <a name="more-details"></a><span data-ttu-id="1c719-111">További részletek</span><span class="sxs-lookup"><span data-stu-id="1c719-111">More details</span></span>

- [<span data-ttu-id="1c719-112">PSEditions paraméterrel rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="1c719-112">Modules with PSEditions</span></span>](module-psedition-support.md)
- [<span data-ttu-id="1c719-113">Pseditions paraméterrel támogatja a PowerShell-Galériabeli</span><span class="sxs-lookup"><span data-stu-id="1c719-113">PSEditions support on PowerShellGallery</span></span>](../how-to/finding-packages/searching-by-compatibility.md)
