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
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma?




Jelentette, hogy Install-modul vagy a frissítés-modul néha meghiúsul az egyes számítógépeken.
A vizsgálat alapján, valami vele a kapcsolat.
Nemrég NuGet-szolgáltató frissítése megtörtént, hogy azt megbízhatóan letölthető csomagok.
Telepítse a NuGet-szolgáltató a legújabb buildjével és majd telepíteni vagy frissíteni a modul az alábbi útmutató követésével.
Most használja az "Azure" modult az alábbi példa.

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```

