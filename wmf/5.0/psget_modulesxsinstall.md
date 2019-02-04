---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0a481fb9d4f2aab89bc448c71b01f1d541cf24bc
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687992"
---
# <a name="side-by-side-version-support-on-powershell-50-or-newer"></a><span data-ttu-id="67333-102">Párhuzamos Verziótámogatás a PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="67333-102">Side-by-Side Version Support on PowerShell 5.0 or newer</span></span>

<span data-ttu-id="67333-103">A rendszer mostantól egymás mellett (SxS) modul verziója támogatja az Install-Module Update-modult, és a Publish-Module-parancsmagok a Windows PowerShell 5.0-s vagy újabb rendszerű.</span><span class="sxs-lookup"><span data-stu-id="67333-103">There is now side-by-side (SxS) module version support in Install-Module, Update-Module, and Publish-Module cmdlets that run in Windows PowerShell 5.0 or newer.</span></span>
<span data-ttu-id="67333-104">Is azt hozzáadta a - RequiredVersion paraméterrel adja meg a verziót, hogy közzé kell tenni a Publish-Module parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="67333-104">Also, we have added a -RequiredVersion parameter to the Publish-Module cmdlet to specify the version to be published.</span></span> <span data-ttu-id="67333-105">Az elérési út paraméter mostantól támogatja a modul alapútvonal a mappát.</span><span class="sxs-lookup"><span data-stu-id="67333-105">The Path parameter now supports the module base path with the version folder.</span></span>

<span data-ttu-id="67333-106">**Install-Module példák:**</span><span class="sxs-lookup"><span data-stu-id="67333-106">**Install-Module examples:**</span></span>
```powershell
Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.0 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name : PSScriptAnalyzer
Version : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.1 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name       : PSScriptAnalyzer
Version    : 1.1.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.1
Name       : PSScriptAnalyzer
Version    : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

Get-InstalledModule -Name PSScriptAnalyzer -AllVersions

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
1.1.0      PSScriptAnalyzer                    Module     PSGallery            PSScriptAnalyzer provides script analysis...
1.1.1      PSScriptAnalyzer                    Module     PSGallery            PSScriptAnalyzer provides script analysis...
```
