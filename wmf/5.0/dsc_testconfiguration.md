---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 10f8dd0f5097260eb4a8516f9662df3d219bdfe5
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34187561"
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a><span data-ttu-id="1581b-102">Teszt-DscConfiguration parancsmag referencia-konfigurációkat támogat.</span><span class="sxs-lookup"><span data-stu-id="1581b-102">Test-DscConfiguration cmdlet supports Reference Configurations</span></span>

<span data-ttu-id="1581b-103">Engedélyezi az összehasonlításhoz használandó hivatkozási konfigurációs dokumentum megadásával célcsomópontokat egy vagy több kívánt konfiguráció állapotának tesztelése a Test-DscConfiguration parancsmag frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="1581b-103">The Test-DscConfiguration cmdlet has been updated to allow testing of desired configuration state of one or more target nodes by specifying a reference configuration document to compare against.</span></span>

<span data-ttu-id="1581b-104">A következő új paraméterkészletei a DSC-konfigurációk használata csak tesztelési megadott elérési út, és soha nem érvényesek a megadott cél csomópontokon minden konfigurációs.</span><span class="sxs-lookup"><span data-stu-id="1581b-104">The following new parameter sets use DSC configurations in the path specified to only test and never apply each configuration on the specified target node(s).</span></span> <span data-ttu-id="1581b-105">A Start-DscConfiguration és egyéb DSC-parancsmagokkal, minden egyes MOF neve segítségével határozza meg, melyik teszteli a konfigurációt a célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="1581b-105">As with Start-DscConfiguration and other DSC cmdlets, the name of each MOF is used to determine which target node to test the configuration on.</span></span>

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

<span data-ttu-id="1581b-106">A következő új paraméterkészletei csak tesztelése, és soha ne alkalmazzon a konfigurációt a megadott cél csomópontokon egyetlen DSC-konfiguráció használatával.</span><span class="sxs-lookup"><span data-stu-id="1581b-106">The following new parameter sets use a single DSC configuration to only test and never apply the configuration on the specified target node(s).</span></span>

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
