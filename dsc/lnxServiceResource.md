---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxService erőforrás
ms.openlocfilehash: ab6544762862c9b2477e92f0d782b13afb96f2c9
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093568"
---
# <a name="dsc-for-linux-nxservice-resource"></a>DSC, a Linux nxService erőforrás

A **nxService** erőforrás a PowerShell Desired State Configuration (DSC) biztosít egy mechanizmust, amely egy Linux-csomóponton a szolgáltatások kezeléséhez.

## <a name="syntax"></a>Szintaxis

```
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd } ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság |  Leírás |
|---|---|
| Név| A szolgáltatás/démon konfigurálása neve.|
| Tartományvezérlő| A szolgáltatás konfigurálásakor használandó szolgáltatásvezérlő típusa.|
| Engedélyezve| Azt jelzi, hogy a szolgáltatás elindul, a rendszerindító.|
| Állapot| Azt jelzi, hogy a szolgáltatás fut-e. Ez annak biztosítása érdekében, hogy a szolgáltatás nem fut a "Stopped" tulajdonság értéke. Állítsa be, győződjön meg arról, hogy a szolgáltatás nem fut a "fut".|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>További információ

A **nxService** erőforrás nem hozza létre a szolgáltatás definíciós vagy parancsfájl a szolgáltatás, ha még nem létezik. Használhatja a PowerShell Desired State Configuration **nxFile** erőforrásra megléte vagy a szolgáltatásdefiníciós fájl vagy parancsfájl tartalmát kezeléséhez.

## <a name="example"></a>Példa

Az alábbi példa bemutatja a regisztrált (az Apache HTTP Server), "httpd" szolgáltatás konfigurációját a **SystemD** szolgáltatásvezérlőhöz.

```powershell
Import-DSCResource -Module nx

Node $node {
    #Apache Service
    nxService ApacheService {
        Name = 'httpd'
        State = 'running'
        Enabled = $true
        Controller = 'systemd'
    }
}
```