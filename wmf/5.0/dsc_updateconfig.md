---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 31fde15e644455dbe77f68bca713bf026544fdc7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688531"
---
# <a name="on-demand-pull-of-dsc-configurations"></a>DSC-konfigurációk igény szerinti lekérése

Az új frissítés-DscConfiguration parancsmag elindítja a lekérési kiszolgálóról a metaadat-konfigurációjában meghatározott lekérési. A viselkedés gyakran nevezik "Most Pull".


Aktivált, miután a lekéréses pontosan ugyanúgy viselkedik, hogy mikor kell aktiválódni a szokásos gyakoriság:

1. Az ellenőrzőösszeg aktuális a rendszer összehasonlítja a konfiguráció a lekérési kiszolgálón ellenőrzőösszeget.
2. Ha a egyeznek, sikeres volt a Kapcsolódás a konfiguráció alkalmazása nélkül.
3. Ha ezek eltérnek, a konfiguráció a lekéréses kiszolgálón származhatnak és alkalmazása.

**Megjegyzés:** Ha a metaadat-konfiguráció RefreshMode = "Push" hibát ad vissza a parancsmag által, így ez a parancsmag minden esetben nem változtat semmin, ha egy célcsomóponttal "Push" módban van.

```powershell
Update-DscConfiguration     [[-ComputerName] <string[]>]
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-Credential<pscredential>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]

Update-DscConfiguration     -CimSession <CimSession[]>
                            [-Wait]
                            [-Force]
                            [-JobName <string>]
                            [-ThrottleLimit <int>]
                            [-WhatIf]
                            [-Confirm]
                            [<CommonParameters>]
```
