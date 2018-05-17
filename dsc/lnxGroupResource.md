---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxGroup erőforrás DSC
ms.openlocfilehash: 9651f3affc9b040a7ef8e7bf8d5ab4cebcca8128
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-for-linux-nxgroup-resource"></a>A Linux nxGroup erőforrás DSC

A **nxGroup** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi egy Linux-csomóponton helyi csoportok kezelése.

## <a name="syntax"></a>Szintaxis

```powershell
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Members = <string[]> ]
    [ MebersToInclude = <string[]>]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}

```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| Csoportnév| Adja meg a legyen egy adott állapot biztosításához a csoport nevét.|
| Győződjön meg arról| Meghatározza, hogy ellenőrizze, hogy a csoport létezik-e. Állítsa be ezt a tulajdonságot "Elérhető" annak érdekében, hogy a csoport létezik. Állítsa az értékét "Hiányzik", annak érdekében, hogy a csoport nem létezik. Az alapértelmezett érték: "Elérhető".|
| Tagok| Adja meg a csoportot alkotó tagok.|
| MembersToInclude| Adja meg a felhasználókat, akik számára biztosítani szeretné a csoport tagjai.|
| MembersToExclude| Meghatározza, hogy a felhasználók számára szeretné biztosítani nem a csoport tagjai.|
| PreferredGroupID| Ha lehetséges beállítja a csoport azonosítója a megadott értékre. Ha a csoport azonosító jelenleg használatban van, a következő rendelkezésre álló csoport azonosítót használja.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy a felhasználó "monuser" létezik, és a "DBusers" csoport tagja.

```
Import-DSCResource -Module nx

Node $node {

nxUser UserExample{
   UserName = "monuser"
   Description = "Monitoring user"
   Password  =    '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
   Ensure = "Present"
   HomeDirectory = "/home/monuser"
}

nxGroup GroupExample{
   GroupName = "DBusers"
   Ensure = "Present"
   MembersToInclude = "monuser"
   DependsOn = "[nxUser]UserExample"
}
}
```