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