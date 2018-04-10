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
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a>Teszt-DscConfiguration parancsmag referencia-konfigurációkat támogat.

Engedélyezi az összehasonlításhoz használandó hivatkozási konfigurációs dokumentum megadásával célcsomópontokat egy vagy több kívánt konfiguráció állapotának tesztelése a Test-DscConfiguration parancsmag frissítve lett.

A következő új paraméterkészletei a DSC-konfigurációk használata csak tesztelési megadott elérési út, és soha nem érvényesek a megadott cél csomópontokon minden konfigurációs. A Start-DscConfiguration és egyéb DSC-parancsmagokkal, minden egyes MOF neve segítségével határozza meg, melyik teszteli a konfigurációt a célcsomóponton.

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

A következő új paraméterkészletei csak tesztelése, és soha ne alkalmazzon a konfigurációt a megadott cél csomópontokon egyetlen DSC-konfiguráció használatával.

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