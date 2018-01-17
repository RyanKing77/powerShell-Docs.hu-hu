---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A Linux nxService erőforrás DSC"
ms.openlocfilehash: 4273ad59f15eedd08b07888ebb6ee51d039b72b3
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-for-linux-nxservice-resource"></a>A Linux nxService erőforrás DSC

A **nxService** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) lehetővé teszi a szolgáltatások egy Linux-csomóponton kezelésére.

## <a name="syntax"></a>Szintaxis

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd }  ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság |  Leírás | 
|---|---|
| Név| A szolgáltatás/démon konfigurálása neve.| 
| Controller| A szolgáltatás konfigurálásakor használandó szolgáltatásvezérlővel típusa.| 
| Engedélyezve| Azt jelzi, hogy a szolgáltatás elindul, a rendszerindító.| 
| Állapot| Azt jelzi, hogy a szolgáltatás fut-e. "Leállítva" Győződjön meg arról, hogy a szolgáltatás nem fut a tulajdonság értékét. Állítsa az értékét annak érdekében, hogy a szolgáltatás nem fut a "fut".| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.| 


## <a name="additional-information"></a>További információ

A **nxService** erőforrás nem hoz létre egy szolgáltatásdefiníció vagy a szolgáltatás parancsfájl Ha még nem létezik. Használhatja a PowerShell célállapot-konfiguráció **nxFile** erőforrás erőforrás megléte vagy a szolgáltatásdefiníciós fájl vagy parancsfájl tartalmát kezeléséhez.

## <a name="example"></a>Példa

A következő példa bemutatja, regisztrált (az Apache HTTP Server), "httpd" szolgáltatás konfigurációját a **SystemD** szolgáltatásvezérlővel.

```
Import-DSCResource -Module nx 

Node $node {
#Apache Service
nxService ApacheService 
{
Name = "httpd"
State = "running"
Enabled = $true
Controller = "systemd"
}
}
```

