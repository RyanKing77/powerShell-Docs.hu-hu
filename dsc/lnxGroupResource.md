---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxGroup erőforrás
ms.openlocfilehash: c61b6ab4a8c56d085b5297dcfc7582187d54f946
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093602"
---
# <a name="dsc-for-linux-nxgroup-resource"></a>DSC, a Linux nxGroup erőforrás

A **nxGroup** erőforrás a PowerShell Desired State Configuration (DSC) Linux csomópont helyi csoportok kezeléséhez mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
nxGroup <string> #ResourceName
{
    GroupName = <string>
    [ Ensure = <string> { Absent | Present } ]
    [ Members = <string[]> ]
    [ MembersToInclude = <string[]> ]
    [ MembersToExclude = <string[]> ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| Csoportnév| Megadja a csoport, amelyhez szeretne biztosítani egy adott állapot nevét.|
| Győződjön meg, hogy| Ellenőrizze, hogy létezik-e a csoport határozza meg. Ezzel a tulajdonsággal, "E" annak érdekében, hogy a csoport létezik. Állítsa a "Hiányzó" annak érdekében, hogy a csoport nem létezik. Az alapértelmezett érték: "E".|
| Tagok| Adja meg a csoportot alkotó a tagokat.|
| MembersToInclude| Megadja, hogy a felhasználók, akik szeretne biztosítani a csoport tagjai.|
| MembersToExclude| Megadja, hogy a felhasználók, akik azt szeretné, amelyek nem a csoport tagjai.|
| PreferredGroupID| Lehetséges, ha beállítja a csoport azonosítója a megadott érték. Ha a csoportazonosító jelenleg használatban van, használja a következő rendelkezésre álló csoport azonosítója.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = '[ResourceType]ResourceName'`.|

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy a felhasználó monuser létezik, és a "DBusers" csoport tagja.

```powershell
Import-DSCResource -Module nx

Node $node {
    nxUser UserExample {
       UserName = 'monuser'
       Description = 'Monitoring user'
       Password = '$6$fZAne/Qc$MZejMrOxDK0ogv9SLiBP5J5qZFBvXLnDu8HY1Oy7ycX.Y3C7mGPUfeQy3A82ev3zIabhDQnj2ayeuGn02CqE/0'
       Ensure = 'Present'
       HomeDirectory = '/home/monuser'
    }

    nxGroup GroupExample {
       GroupName = 'DBusers'
       Ensure = 'Present'
       MembersToInclude = 'monuser'
       DependsOn = '[nxUser]UserExample'
    }
}
```