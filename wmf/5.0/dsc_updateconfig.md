---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: f2ddde78f436e6f03f521a9a8246dbda93e7a57a
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
---
# <a name="on-demand-pull-of-dsc-configurations"></a>Igény szerinti LEKÉRÉSES DSC-konfigurációk

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

