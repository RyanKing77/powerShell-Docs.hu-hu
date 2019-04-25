---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4008a7f91af41150f26c4147135b30aa8835281c
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62058743"
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a><span data-ttu-id="7ad68-102">A test-DscConfiguration parancsmag támogatja a referencia-konfigurációkat</span><span class="sxs-lookup"><span data-stu-id="7ad68-102">Test-DscConfiguration cmdlet supports Reference Configurations</span></span>

<span data-ttu-id="7ad68-103">A Test-DscConfiguration parancsmag frissítve lett, hogy egy vagy több cél csomópontok kívánt konfigurációs állapotát egy referencia-konfigurációs dokumentum porovnání megadásával tesztelése.</span><span class="sxs-lookup"><span data-stu-id="7ad68-103">The Test-DscConfiguration cmdlet has been updated to allow testing of desired configuration state of one or more target nodes by specifying a reference configuration document to compare against.</span></span>

<span data-ttu-id="7ad68-104">A következő új paraméterkészlettel DSC-konfigurációk használata csak tesztelési megadott elérési út, és soha ne alkalmazzon az egyes konfigurációkhoz a célként megadott csomópontokon.</span><span class="sxs-lookup"><span data-stu-id="7ad68-104">The following new parameter sets use DSC configurations in the path specified to only test and never apply each configuration on the specified target node(s).</span></span> <span data-ttu-id="7ad68-105">A Start-DscConfiguration és egyéb DSC-parancsmagok, minden egyes MOF neve meghatározására szolgál melyik teszteli a konfigurációt a cél-csomópont.</span><span class="sxs-lookup"><span data-stu-id="7ad68-105">As with Start-DscConfiguration and other DSC cmdlets, the name of each MOF is used to determine which target node to test the configuration on.</span></span>

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

<span data-ttu-id="7ad68-106">A következő új paraméterkészlettel csak teszteléshez, és soha nem a konfiguráció alkalmazása a célként megadott csomópontokon egyetlen DSC-konfigurációja használja.</span><span class="sxs-lookup"><span data-stu-id="7ad68-106">The following new parameter sets use a single DSC configuration to only test and never apply the configuration on the specified target node(s).</span></span>

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
