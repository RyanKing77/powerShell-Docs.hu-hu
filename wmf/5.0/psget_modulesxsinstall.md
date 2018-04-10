---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: f9a121c320ffb780503dbe0c278f698a6fa40289
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="side-by-side-version-support-on-powershell-50-or-newer"></a><span data-ttu-id="5e303-102">Egymás melletti verzióinak támogatása PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="5e303-102">Side-by-Side Version Support on PowerShell 5.0 or newer</span></span>

<span data-ttu-id="5e303-103">Most már van egymás melletti (SxS) modul által támogatott verzió a telepítés-modulban frissítés-modul, és a közzététel-modul parancsmagjai a Windows PowerShell 5.0-s vagy újabb rendszerű.</span><span class="sxs-lookup"><span data-stu-id="5e303-103">There is now side-by-side (SxS) module version support in Install-Module, Update-Module, and Publish-Module cmdlets that run in Windows PowerShell 5.0 or newer.</span></span>
<span data-ttu-id="5e303-104">Emellett jelentek meg - RequiredVersion paraméter a Publish-modul parancsmagnak közzé kell tenni a verzió megadásához.</span><span class="sxs-lookup"><span data-stu-id="5e303-104">Also, we have added a -RequiredVersion parameter to the Publish-Module cmdlet to specify the version to be published.</span></span> <span data-ttu-id="5e303-105">Az elérési út paraméter mostantól támogatja a modul alap útvonalat a mappát.</span><span class="sxs-lookup"><span data-stu-id="5e303-105">The Path parameter now supports the module base path with the version folder.</span></span>

<span data-ttu-id="5e303-106">**Install-modul példák:**</span><span class="sxs-lookup"><span data-stu-id="5e303-106">**Install-Module examples:**</span></span>
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