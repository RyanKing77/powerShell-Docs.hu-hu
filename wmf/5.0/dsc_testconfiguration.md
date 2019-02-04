---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 4008a7f91af41150f26c4147135b30aa8835281c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688559"
---
# <a name="test-dscconfiguration-cmdlet-supports-reference-configurations"></a>A test-DscConfiguration parancsmag támogatja a referencia-konfigurációkat

A Test-DscConfiguration parancsmag frissítve lett, hogy egy vagy több cél csomópontok kívánt konfigurációs állapotát egy referencia-konfigurációs dokumentum porovnání megadásával tesztelése.

A következő új paraméterkészlettel DSC-konfigurációk használata csak tesztelési megadott elérési út, és soha ne alkalmazzon az egyes konfigurációkhoz a célként megadott csomópontokon. A Start-DscConfiguration és egyéb DSC-parancsmagok, minden egyes MOF neve meghatározására szolgál melyik teszteli a konfigurációt a cél-csomópont.

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

A következő új paraméterkészlettel csak teszteléshez, és soha nem a konfiguráció alkalmazása a célként megadott csomópontokon egyetlen DSC-konfigurációja használja.

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
