---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxPackage erőforrás
ms.openlocfilehash: 64bb89a95bd6cbaea4e74b8a9979de52428fef3f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077874"
---
# <a name="dsc-for-linux-nxpackage-resource"></a>DSC, a Linux nxPackage erőforrás

A **nxPackage** erőforrás a PowerShell Desired State Configuration (DSC) Linux csomóponton csomagok kezeléséhez mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| Név| A csomag, amelyhez szeretne biztosítani egy adott állapot neve.|
| Győződjön meg, hogy| Ellenőrizze, hogy létezik-e a csomag határozza meg. Ezzel a tulajdonsággal, "E" annak érdekében, hogy a csomag létezik. Állítsa a "Hiányzó" annak érdekében, hogy a csomag nem létezik. Az alapértelmezett érték: "E".|
| PackageManager| Támogatott értékei a következők: "yum", "apt" és "zypper". Adja meg a csomagok telepítéséhez használni kívánt Csomagkezelő. Ha **FilePath** van megadva, a megadott elérési út lesz a csomag telepítéséhez. Ellenkező esetben Csomagkezelő használható egy előre konfigurált adattárból a csomag telepítéséhez. Ha sem **PackageManager** sem **FilePath** érhetők el, az alapértelmezett Csomagkezelő esetében a rendszer használható.|
| FilePath| A fájl elérési útja, ahol a csomag található|
| PackageGroup| Ha **$true**, a **neve** kell lennie egy csomag csoport nevére, a segítségével egy **PackageManager**. **PacakgeGroup** esetén nem érvényes biztosít egy **FilePath**.|
| Argumentumok| Egy karakterlánc, amely a rendszer átad a csomag pontosan a megadott argumentumok.|
| ReturnCode| A várt visszatérési kód. Ha a tényleges visszatérési kód nem egyezik a várt értéknek. Itt, elérhető, a konfigurációs hibát adnak vissza.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy a "httpd" nevű csomag telepítve van-e egy Linux rendszerű számítógépre, a "Yum" package manager használatával.

```
Import-DSCResource -Module nx

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```