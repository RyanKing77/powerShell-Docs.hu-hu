---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxFileLine erőforrás DSC
ms.openlocfilehash: 6b927839c23478aa9916a5d23836b31fccc58484
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-for-linux-nxfileline-resource"></a>A Linux nxFileLine erőforrás DSC

A **nxFileLine** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) gombra a konfigurációs fájlban lévő Linux csomópont sorait mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| fájl elérési útja| A fájl teljes elérési útja a célcsomóponton sorainak kezeléséhez.|
| ContainsLine| Győződjön meg arról, hogy egy sort a fájl létezik. Ezt a sort a fájl is bővül, ha a fájl nem létezik. **ContainsLine** kötelező, de állítható be üres karakterlánc ("ContainsLine =" ") nincs szükség esetén.|
| DoesNotContainPattern| A fájl nem létezhet sorok Reguláriskifejezés-mintának. Olyan sort, amely létezik a fájlban a reguláris kifejezésnek megfelelő a sort a fájl törlődik.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

A példa bemutatja, hogyan használja a **nxFileLine** erőforrás konfigurálása a `/etc/sudoers` fájl, ezzel biztosítható, hogy a felhasználó: nem requiretty monuser van konfigurálva.

```
Import-DSCResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```