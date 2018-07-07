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
# <a name="troubleshooting-cmdlets"></a>Hibaelhárítási parancsmagok

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Megoldását "Figyelmeztetés: nem sikerült letölteni a csomagot a csomag neve" probléma

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