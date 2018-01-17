---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxPackage erőforrás DSC"
ms.openlocfilehash: 41c627ebb39dad535f7acc8fe34739355f7a81b5
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxpackage-resource"></a>A Linux nxPackage erőforrás DSC

A **nxPackage** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi a csomagok egy Linux-csomóponton felügyeletéhez.

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
| Név| A csomag, amelyekhez egy adott állapot biztosításához neve.| 
| Győződjön meg arról| Meghatározza, hogy ellenőrizze, hogy a csomag létezik-e. Állítsa be ezt a tulajdonságot "Elérhető" annak érdekében, hogy a csomag létezik-e. Állítsa az értékét "Hiányzik", annak érdekében, hogy a csomag nem létezik. Az alapértelmezett érték: "Elérhető".|  
| PackageManager| Támogatott értékei a "yum", "apt" és "zypper". Adja meg a package manager csomagok telepítése során használja. Ha **FilePath** van megadva, a megadott elérési út fogja használni a csomag telepítéséhez. Ellenkező esetben a Csomagkezelő használható előre konfigurált tárházból a csomag telepítéséhez. Ha sem **PackageManager** sem **FilePath** biztosított, az alapértelmezett Csomagkezelőt a rendszer lesz használható.| 
| FilePath| A fájl elérési útját, ahol a csomag található| 
| PackageGroup| Ha **$true**, a **neve** kellene lennie a használathoz egy csomag csoport nevét a **PackageManager**. **PacakgeGroup** érvénytelen nyújtásakor a **FilePath**.| 
| Argumentumok| Az átadott csomag pontosan megegyezik a megadott argumentumok karakterlánc.| 
| Visszatérési kód:| A várt visszatérési kód. Ha a tényleges visszatérési kód nem egyezik a várt érték megadva itt, a konfigurációs hibát adnak vissza.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.| 

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy a "httpd" nevű csomaghoz: telepítve van egy Linux-számítógép, a "Yum" package manager használatával.

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

