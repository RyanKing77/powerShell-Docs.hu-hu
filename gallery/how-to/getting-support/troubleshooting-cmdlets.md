---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: Hibaelhárítási parancsmagok
ms.openlocfilehash: f5cd9c0cc23fef5891bf02c10b6541ab0f9d418a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686550"
---
# <a name="troubleshooting-cmdlets"></a>Hibaelhárítási parancsmagok

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Megoldását "Figyelmeztetés: Nem sikerült letölteni a csomagot a csomag neve"probléma

Azt jelenti, hogy `Install-Module` vagy `Update-Module` időnként meghiúsul, az egyes gépek.
Vizsgálatunk alapul, fontos, hogy a hálózati kapcsolattal.
Nemrégiben frissítettük NuGet-szolgáltató úgy, hogy megbízhatóan letöltheti a csomagokat.
Követheti, hogy telepítse a NuGet-szolgáltató legújabb buildjével és telepítheti őket, vagy a modulok frissítésére, az alábbi utasításokat.
Az alábbi példa használjuk az "Azure" modul.

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```
