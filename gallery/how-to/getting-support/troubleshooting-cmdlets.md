---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Hibaelhárítási parancsmagok
ms.openlocfilehash: 6295a5b99aa19db933569638d84e490ad81eedc7
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: hu-HU
ms.lasthandoff: 05/10/2018
---
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="1567c-103">Hibaelhárítási parancsmagok</span><span class="sxs-lookup"><span data-stu-id="1567c-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="1567c-104">Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma?</span><span class="sxs-lookup"><span data-stu-id="1567c-104">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>

<span data-ttu-id="1567c-105">Jelentette, hogy Install-modul vagy a frissítés-modul néha meghiúsul az egyes számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="1567c-105">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="1567c-106">A vizsgálat alapján, valami vele a kapcsolat.</span><span class="sxs-lookup"><span data-stu-id="1567c-106">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="1567c-107">Nemrég NuGet-szolgáltató frissítése megtörtént, hogy azt megbízhatóan letölthető csomagok.</span><span class="sxs-lookup"><span data-stu-id="1567c-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="1567c-108">Telepítse a NuGet-szolgáltató a legújabb buildjével és majd telepíteni vagy frissíteni a modul az alábbi útmutató követésével.</span><span class="sxs-lookup"><span data-stu-id="1567c-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="1567c-109">Most használja az "Azure" modult az alábbi példa.</span><span class="sxs-lookup"><span data-stu-id="1567c-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```