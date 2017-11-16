---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: ce60b240045acf538edae1a08007971e538588ca
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a><span data-ttu-id="b29d5-102">Teszt-DscConfiguration parancsmag referencia-konfigurációkat támogat.</span><span class="sxs-lookup"><span data-stu-id="b29d5-102">Test-DscConfiguration cmdlet supports Reference Configurations</span></span>

<span data-ttu-id="b29d5-103">Engedélyezi az összehasonlításhoz használandó hivatkozási konfigurációs dokumentum megadásával célcsomópontokat egy vagy több kívánt konfiguráció állapotának tesztelése a Test-DscConfiguration parancsmag frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="b29d5-103">The Test-DscConfiguration cmdlet has been updated to allow testing of desired configuration state of one or more target nodes by specifying a reference configuration document to compare against.</span></span>

<span data-ttu-id="b29d5-104">A következő új paraméterkészletei a DSC-konfigurációk használata csak tesztelési megadott elérési út, és soha nem érvényesek a megadott cél csomópontokon minden konfigurációs.</span><span class="sxs-lookup"><span data-stu-id="b29d5-104">The following new parameter sets use DSC configurations in the path specified to only test and never apply each configuration on the specified target node(s).</span></span> <span data-ttu-id="b29d5-105">A Start-DscConfiguration és egyéb DSC-parancsmagokkal, minden egyes MOF neve segítségével határozza meg, melyik teszteli a konfigurációt a célcsomóponton.</span><span class="sxs-lookup"><span data-stu-id="b29d5-105">As with Start-DscConfiguration and other DSC cmdlets, the name of each MOF is used to determine which target node to test the configuration on.</span></span> 

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

<span data-ttu-id="b29d5-106">A következő új paraméterkészletei csak tesztelése, és soha ne alkalmazzon a konfigurációt a megadott cél csomópontokon egyetlen DSC-konfiguráció használatával.</span><span class="sxs-lookup"><span data-stu-id="b29d5-106">The following new parameter sets use a single DSC configuration to only test and never apply the configuration on the specified target node(s).</span></span> 

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

