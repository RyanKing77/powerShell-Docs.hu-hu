---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: scriptwithpseditionsupport
ms.openlocfilehash: 18ce2d729199e0587ef92993db7fec44ef744ec7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="script-with-compatible-powershell-editions"></a><span data-ttu-id="d0361-103">Verzióval kompatibilis PowerShell parancsfájl</span><span class="sxs-lookup"><span data-stu-id="d0361-103">Script with compatible PowerShell Editions</span></span>
<span data-ttu-id="d0361-104">Az 5.1-es verziótól kezdődően a PowerShell különböző kiadásokban érhető el, amelyek különböző szolgáltatáskészleteket és platformkompatibilitást kínálnak.</span><span class="sxs-lookup"><span data-stu-id="d0361-104">Starting with version 5.1, PowerShell is available in different editions which denote varying feature sets and platform compatibility.</span></span>

- <span data-ttu-id="d0361-105">**Desktop kiadás:** A .NET-keretrendszeren alapul, és a Windows teljes erőforrás-igényű kiadásain, például a Server Core és a Windows asztali kiadásain futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="d0361-105">**Desktop Edition:** Built on .NET Framework and provides compatibility with scripts and modules targeting versions of PowerShell running on full footprint editions of Windows such as Server Core and Windows Desktop.</span></span>
- <span data-ttu-id="d0361-106">**Core kiadás:** .NET Core-on alapul, és a Windows csökkentett erőforrás-igényű kiadásain, például a Nano Serveren és a Windows IoT kiadásokon futtatott PowerShell-verziókat célzó szkriptekhez és modulokhoz biztosít kompatibilitást.</span><span class="sxs-lookup"><span data-stu-id="d0361-106">**Core Edition:** Built on .NET Core and provides compatibility with scripts and modules targeting versions of PowerShell running on reduced footprint editions of Windows such as Nano Server and Windows IoT.</span></span>

<span data-ttu-id="d0361-107">A futtatott PowerShell-verzió a $PSVersionTable PSEdition tulajdonságában jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="d0361-107">The running edition of PowerShell is shown in the PSEdition property of $PSVersionTable.</span></span>
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

<span data-ttu-id="d0361-108">A parancsfájlkészítők egy #requires utasításban a PSEdition paraméterrel megakadályozhatják a szkriptek nem kompatibilis PowerShell-kiadáson való futtatását.</span><span class="sxs-lookup"><span data-stu-id="d0361-108">Script authors can prevent a script from executing unless it is run on a compatible edition of PowerShell using the PSEdition parameter on a #requires statement.</span></span>
```powershell
Set-Content C:\script.ps1 -Value "#requires -PSEdition Core
Get-Process -Name PowerShell"
Get-Content C:\script.ps1
#requires -PSEdition Core
Get-Process -Name PowerShell

C:\script.ps1
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a "#requires" statement for PowerShell Core edition. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.
At line:1 char:1
+ C:\script.ps1
+ ~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition
```

<span data-ttu-id="d0361-109">PowerShell-galériában felhasználói is megtalálhassák a támogatott egy adott kiadásán PowerShell parancsfájlok listáját.</span><span class="sxs-lookup"><span data-stu-id="d0361-109">PowerShell Gallery users can find the list of scripts supported on a specific PowerShell Edition.</span></span>
<span data-ttu-id="d0361-110">Parancsfájlok nélkül PSEdition_Desktop és PSEditon_Core minősülnek PowerShell asztali változatában működnek.</span><span class="sxs-lookup"><span data-stu-id="d0361-110">Scripts without PSEdition_Desktop and PSEditon_Core are considered to work fine on PowerShell Desktop editions.</span></span>

```powershell

# Find scripts supported on PowerShell Desktop edition
Find-Script -Tag PSEditon_Desktop

# Find scripts supported on PowerShell Core editions
Find-Script -Tag PSEditon_Core

```

## <a name="more-details"></a><span data-ttu-id="d0361-111">További részletekért</span><span class="sxs-lookup"><span data-stu-id="d0361-111">More details</span></span>
### <a name="modules-with-pseditionsmodulemodulewithpseditionsupportmd"></a>[<span data-ttu-id="d0361-112">PSEditions paraméterrel rendelkező modulok</span><span class="sxs-lookup"><span data-stu-id="d0361-112">Modules with PSEditions</span></span>](../module/modulewithpseditionsupport.md)
### <a name="pseditions-support-on-powershellgallerypsgallerypsgallerypseditionsmd"></a>[<span data-ttu-id="d0361-113">Támogatja a PSEditions PowerShellGallery</span><span class="sxs-lookup"><span data-stu-id="d0361-113">PSEditions support on PowerShellGallery</span></span>](../../psgallery/psgallery_pseditions.md)