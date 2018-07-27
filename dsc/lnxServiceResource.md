---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxService erőforrás
ms.openlocfilehash: fe8043995205649378725f2ab0a78e19313739c9
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267779"
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

| Tulajdonság | Leírás |
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