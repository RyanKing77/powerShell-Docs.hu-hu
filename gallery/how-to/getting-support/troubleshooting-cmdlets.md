---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Hibaelhárítási parancsmagok
ms.openlocfilehash: c0a1fbcafd8c4443dc9d628c54c4c525d9701861
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892474"
---
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="be31b-103">Hibaelhárítási parancsmagok</span><span class="sxs-lookup"><span data-stu-id="be31b-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="be31b-104">Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma</span><span class="sxs-lookup"><span data-stu-id="be31b-104">How to resolve "WARNING: Package 'your package name' failed to download" issue</span></span>

<span data-ttu-id="be31b-105">Azt jelenti, hogy `Install-Module` vagy `Update-Module` időnként meghiúsul, az egyes gépek.</span><span class="sxs-lookup"><span data-stu-id="be31b-105">It is reported that `Install-Module` or `Update-Module` sometimes fails on some machines.</span></span>
<span data-ttu-id="be31b-106">Vizsgálatunk alapul, fontos, hogy a hálózati kapcsolattal.</span><span class="sxs-lookup"><span data-stu-id="be31b-106">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="be31b-107">Nemrégiben frissítettük NuGet-szolgáltató úgy, hogy megbízhatóan letöltheti a csomagokat.</span><span class="sxs-lookup"><span data-stu-id="be31b-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="be31b-108">Követheti, hogy telepítse a NuGet-szolgáltató legújabb buildjével és telepítheti őket, vagy a modulok frissítésére, az alábbi utasításokat.</span><span class="sxs-lookup"><span data-stu-id="be31b-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="be31b-109">Az alábbi példa használjuk az "Azure" modul.</span><span class="sxs-lookup"><span data-stu-id="be31b-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```