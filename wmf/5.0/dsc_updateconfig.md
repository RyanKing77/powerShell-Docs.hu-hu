---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 6d37fbc5091d69925d60349f3acbdecc92da1b95
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="on-demand-pull-of-dsc-configurations"></a>DSC-konfigurációk igény szerinti lekérése

Az új frissítés-DscConfiguration parancsmag elindítja a metaadat-konfigurációjában a lekéréses kiszolgálóról lekérési. A jelenség gyakran nevezik "Pull most".


Miután elindul, a lekéréses pontosan ugyanúgy viselkedik, mikor kellene elindított rendszeres gyakorisága:

1. Az aktuális ellenőrzőösszeg összeveti az ellenőrzőösszeg-konfigurációhoz a lekérési kiszolgálón.
2. Ha a egyeznek, fejeződik a konfiguráció alkalmazása nélkül.
3. Ha ezek eltérnek, a konfiguráció a lekérési kiszolgálójával lekért és alkalmazása.

**Megjegyzés:** Ha a metaadat-konfiguráció RefreshMode = "Push" hibát ad vissza a parancsmag által, ezért ez a parancsmag mindig nem változtat semmin, ha egy célcsomóponttal "Push" módban van.

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
