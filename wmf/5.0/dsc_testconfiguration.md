---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 18c1dab7412b8e9d31960507b612dd6cc56d31d5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a><span data-ttu-id="1bb12-102">Teszt-DscConfiguration parancsmag referencia-konfigurációkat támogat.</span><span class="sxs-lookup"><span data-stu-id="1bb12-102">Test-DscConfiguration cmdlet supports Reference Configurations</span></span>

<span data-ttu-id="1bb12-103">Engedélyezi az összehasonlításhoz használandó hivatkozási konfigurációs dokumentum megadásával célcsomópontokat egy vagy több kívánt konfiguráció állapotának tesztelése a Test-DscConfiguration parancsmag frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="1bb12-103">The Test-DscConfiguration cmdlet has been updated to allow testing of desired configuration state of one or more target nodes by specifying a reference configuration document to compare against.</span></span>

<span data-ttu-id="1bb12-104">A következő új paraméterkészletei a DSC-konfigurációk használata csak tesztelési megadott elérési út, és soha nem érvényesek a megadott cél csomópontokon minden konfigurációs.</span><span class="sxs-lookup"><span data-stu-id="1bb12-104">The following new parameter sets use DSC configurations in the path specified to only test and never apply each configuration on the specified target node(s).</span></span> <span data-ttu-id="1bb12-105">A Start-DscConfiguration és egyéb DSC-parancsmagokkal, minden egyes MOF neve segítségével határozza meg, melyik teszteli a konfigurációt a célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="1bb12-105">As with Start-DscConfiguration and other DSC cmdlets, the name of each MOF is used to determine which target node to test the configuration on.</span></span>

```powershell
Test-DscConfiguration   [-Path] <string>
                        [[-ComputerName] <string[]>]
                        [-Credential <pscredential>]
                        [-ThrottleLimit <int>]
                        [-AsJob]
                        [<CommonParameters>]

Test-DscConfiguration   [-Path] <string>
                        -CimSession <CimSession[]>
                        [-ThrottleLimit <int>]
                        [-AsJob]
                        [<CommonParameters>]
```

<span data-ttu-id="1bb12-106">A következő új paraméterkészletei csak tesztelése, és soha ne alkalmazzon a konfigurációt a megadott cél csomópontokon egyetlen DSC-konfiguráció használatával.</span><span class="sxs-lookup"><span data-stu-id="1bb12-106">The following new parameter sets use a single DSC configuration to only test and never apply the configuration on the specified target node(s).</span></span>

```powershell
Test-DscConfiguration   -ReferenceConfiguration <string>
                        [[-ComputerName] <string[]>]
                        [-Credential <pscredential>]
                        [-ThrottleLimit <int>]
                        [-AsJob]
                        [<CommonParameters>]

Test-DscConfiguration   -ReferenceConfiguration <string>
                        -CimSession <CimSession[]>
                        [-ThrottleLimit <int>]
                        [-AsJob]
                        [<CommonParameters>]
```