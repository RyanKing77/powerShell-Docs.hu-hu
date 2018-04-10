---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: psget_cmdlets_troubleshooting
ms.openlocfilehash: bc49dc78b8205d1194ddfe4bdca98b3e681860bd
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="a14fe-103">Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma?</span><span class="sxs-lookup"><span data-stu-id="a14fe-103">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>




<span data-ttu-id="a14fe-104">Jelentette, hogy Install-modul vagy a frissítés-modul néha meghiúsul az egyes számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="a14fe-104">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="a14fe-105">A vizsgálat alapján, valami vele a kapcsolat.</span><span class="sxs-lookup"><span data-stu-id="a14fe-105">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="a14fe-106">Nemrég NuGet-szolgáltató frissítése megtörtént, hogy azt megbízhatóan letölthető csomagok.</span><span class="sxs-lookup"><span data-stu-id="a14fe-106">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="a14fe-107">Telepítse a NuGet-szolgáltató a legújabb buildjével és majd telepíteni vagy frissíteni a modul az alábbi útmutató követésével.</span><span class="sxs-lookup"><span data-stu-id="a14fe-107">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="a14fe-108">Most használja az "Azure" modult az alábbi példa.</span><span class="sxs-lookup"><span data-stu-id="a14fe-108">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```