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

