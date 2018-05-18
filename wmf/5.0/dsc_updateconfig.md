---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 6d37fbc5091d69925d60349f3acbdecc92da1b95
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="on-demand-pull-of-dsc-configurations"></a><span data-ttu-id="e6358-102">DSC-konfigurációk igény szerinti lekérése</span><span class="sxs-lookup"><span data-stu-id="e6358-102">On-demand PULL of DSC Configurations</span></span>

<span data-ttu-id="e6358-103">Az új frissítés-DscConfiguration parancsmag elindítja a metaadat-konfigurációjában a lekéréses kiszolgálóról lekérési.</span><span class="sxs-lookup"><span data-stu-id="e6358-103">The new Update-DscConfiguration cmdlet triggers a pull from the pull server(s) defined in the meta-configuration.</span></span> <span data-ttu-id="e6358-104">A jelenség gyakran nevezik "Pull most".</span><span class="sxs-lookup"><span data-stu-id="e6358-104">The behavior is often referred to as 'Pull Now'.</span></span>


<span data-ttu-id="e6358-105">Miután elindul, a lekéréses pontosan ugyanúgy viselkedik, mikor kellene elindított rendszeres gyakorisága:</span><span class="sxs-lookup"><span data-stu-id="e6358-105">Once triggered, the pull behaves exactly the same as it would have when triggered during the regular frequency:</span></span>

1. <span data-ttu-id="e6358-106">Az aktuális ellenőrzőösszeg összeveti az ellenőrzőösszeg-konfigurációhoz a lekérési kiszolgálón.</span><span class="sxs-lookup"><span data-stu-id="e6358-106">The checksum for current configuration is compared to the checksum for the configuration on the pull server.</span></span>
2. <span data-ttu-id="e6358-107">Ha a egyeznek, fejeződik a konfiguráció alkalmazása nélkül.</span><span class="sxs-lookup"><span data-stu-id="e6358-107">If they are the same, it completes successfully without applying the configuration.</span></span>
3. <span data-ttu-id="e6358-108">Ha ezek eltérnek, a konfiguráció a lekérési kiszolgálójával lekért és alkalmazása.</span><span class="sxs-lookup"><span data-stu-id="e6358-108">If they are different, the configuration is pulled down from the pull server and applied.</span></span>

<span data-ttu-id="e6358-109">**Megjegyzés:** Ha a metaadat-konfiguráció RefreshMode = "Push" hibát ad vissza a parancsmag által, ezért ez a parancsmag mindig nem változtat semmin, ha egy célcsomóponttal "Push" módban van.</span><span class="sxs-lookup"><span data-stu-id="e6358-109">**Note:** If the Meta-Configuration RefreshMode = 'Push' an error is returned by this cmdlet so this cmdlet will always do nothing when a target node is in 'Push' Mode.</span></span>

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
