---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: psget_cmdlets_troubleshooting
ms.openlocfilehash: ccb39f44e8d11f1e2a912da0c4f18b700e836c91
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="5a22c-103">Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma?</span><span class="sxs-lookup"><span data-stu-id="5a22c-103">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>




<span data-ttu-id="5a22c-104">Jelentette, hogy Install-modul vagy a frissítés-modul néha meghiúsul az egyes számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="5a22c-104">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="5a22c-105">A vizsgálat alapján, valami vele a kapcsolat.</span><span class="sxs-lookup"><span data-stu-id="5a22c-105">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="5a22c-106">Nemrég NuGet-szolgáltató frissítése megtörtént, hogy azt megbízhatóan letölthető csomagok.</span><span class="sxs-lookup"><span data-stu-id="5a22c-106">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="5a22c-107">Telepítse a NuGet-szolgáltató a legújabb buildjével és majd telepíteni vagy frissíteni a modul az alábbi útmutató követésével.</span><span class="sxs-lookup"><span data-stu-id="5a22c-107">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="5a22c-108">Most használja az "Azure" modult az alábbi példa.</span><span class="sxs-lookup"><span data-stu-id="5a22c-108">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```

