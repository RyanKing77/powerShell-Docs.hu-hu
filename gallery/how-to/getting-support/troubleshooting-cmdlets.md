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
# <a name="troubleshooting-cmdlets"></a>Hibaelhárítási parancsmagok

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