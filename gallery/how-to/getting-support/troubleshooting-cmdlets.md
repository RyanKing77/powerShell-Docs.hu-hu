---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Hibaelhárítási parancsmagok
ms.openlocfilehash: f5cd9c0cc23fef5891bf02c10b6541ab0f9d418a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62084181"
---
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="6de45-103">Hibaelhárítási parancsmagok</span><span class="sxs-lookup"><span data-stu-id="6de45-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="6de45-104">Megoldását "Figyelmeztetés: Nem sikerült letölteni a csomagot a csomag neve"probléma</span><span class="sxs-lookup"><span data-stu-id="6de45-104">How to resolve "WARNING: Package 'your package name' failed to download" issue</span></span>

<span data-ttu-id="6de45-105">Azt jelenti, hogy `Install-Module` vagy `Update-Module` időnként meghiúsul, az egyes gépek.</span><span class="sxs-lookup"><span data-stu-id="6de45-105">It is reported that `Install-Module` or `Update-Module` sometimes fails on some machines.</span></span>
<span data-ttu-id="6de45-106">Vizsgálatunk alapul, fontos, hogy a hálózati kapcsolattal.</span><span class="sxs-lookup"><span data-stu-id="6de45-106">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="6de45-107">Nemrégiben frissítettük NuGet-szolgáltató úgy, hogy megbízhatóan letöltheti a csomagokat.</span><span class="sxs-lookup"><span data-stu-id="6de45-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="6de45-108">Követheti, hogy telepítse a NuGet-szolgáltató legújabb buildjével és telepítheti őket, vagy a modulok frissítésére, az alábbi utasításokat.</span><span class="sxs-lookup"><span data-stu-id="6de45-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="6de45-109">Az alábbi példa használjuk az "Azure" modul.</span><span class="sxs-lookup"><span data-stu-id="6de45-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```
