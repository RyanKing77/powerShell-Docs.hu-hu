---
ms.date: 06/12/2017
contributor: manikb
keywords: gyűjtemény, a powershell, a parancsmag, a psget
title: Hibaelhárítási parancsmagok
ms.openlocfilehash: e8890cb6bbe661b8524d83cabf91483acbde8095
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219827"
---
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="e2194-103">Hibaelhárítási parancsmagok</span><span class="sxs-lookup"><span data-stu-id="e2194-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="e2194-104">Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma?</span><span class="sxs-lookup"><span data-stu-id="e2194-104">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>

<span data-ttu-id="e2194-105">Jelentette, hogy Install-modul vagy a frissítés-modul néha meghiúsul az egyes számítógépeken.</span><span class="sxs-lookup"><span data-stu-id="e2194-105">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="e2194-106">A vizsgálat alapján, valami vele a kapcsolat.</span><span class="sxs-lookup"><span data-stu-id="e2194-106">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="e2194-107">Nemrég NuGet-szolgáltató frissítése megtörtént, hogy azt megbízhatóan letölthető csomagok.</span><span class="sxs-lookup"><span data-stu-id="e2194-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="e2194-108">Telepítse a NuGet-szolgáltató a legújabb buildjével és majd telepíteni vagy frissíteni a modul az alábbi útmutató követésével.</span><span class="sxs-lookup"><span data-stu-id="e2194-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="e2194-109">Most használja az "Azure" modult az alábbi példa.</span><span class="sxs-lookup"><span data-stu-id="e2194-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```