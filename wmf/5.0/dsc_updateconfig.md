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
# <a name="on-demand-pull-of-dsc-configurations"></a><span data-ttu-id="4dfd2-102">DSC-konfigurációk igény szerinti lekérése</span><span class="sxs-lookup"><span data-stu-id="4dfd2-102">On-demand PULL of DSC Configurations</span></span>

<span data-ttu-id="4dfd2-103">Az új frissítés-DscConfiguration parancsmag elindítja a lekérési kiszolgálóról a metaadat-konfigurációjában meghatározott lekérési.</span><span class="sxs-lookup"><span data-stu-id="4dfd2-103">The new Update-DscConfiguration cmdlet triggers a pull from the pull server(s) defined in the meta-configuration.</span></span> <span data-ttu-id="4dfd2-104">A viselkedés gyakran nevezik "Most Pull".</span><span class="sxs-lookup"><span data-stu-id="4dfd2-104">The behavior is often referred to as 'Pull Now'.</span></span>


<span data-ttu-id="4dfd2-105">Aktivált, miután a lekéréses pontosan ugyanúgy viselkedik, hogy mikor kell aktiválódni a szokásos gyakoriság:</span><span class="sxs-lookup"><span data-stu-id="4dfd2-105">Once triggered, the pull behaves exactly the same as it would have when triggered during the regular frequency:</span></span>

1. <span data-ttu-id="4dfd2-106">Az ellenőrzőösszeg aktuális a rendszer összehasonlítja a konfiguráció a lekérési kiszolgálón ellenőrzőösszeget.</span><span class="sxs-lookup"><span data-stu-id="4dfd2-106">The checksum for current configuration is compared to the checksum for the configuration on the pull server.</span></span>
2. <span data-ttu-id="4dfd2-107">Ha a egyeznek, sikeres volt a Kapcsolódás a konfiguráció alkalmazása nélkül.</span><span class="sxs-lookup"><span data-stu-id="4dfd2-107">If they are the same, it completes successfully without applying the configuration.</span></span>
3. <span data-ttu-id="4dfd2-108">Ha ezek eltérnek, a konfiguráció a lekéréses kiszolgálón származhatnak és alkalmazása.</span><span class="sxs-lookup"><span data-stu-id="4dfd2-108">If they are different, the configuration is pulled down from the pull server and applied.</span></span>

<span data-ttu-id="4dfd2-109">**Megjegyzés:** Ha a metaadat-konfiguráció RefreshMode = "Push" hibát ad vissza a parancsmag által, így ez a parancsmag minden esetben nem változtat semmin, ha egy célcsomóponttal "Push" módban van.</span><span class="sxs-lookup"><span data-stu-id="4dfd2-109">**Note:** If the Meta-Configuration RefreshMode = 'Push' an error is returned by this cmdlet so this cmdlet will always do nothing when a target node is in 'Push' Mode.</span></span>

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
