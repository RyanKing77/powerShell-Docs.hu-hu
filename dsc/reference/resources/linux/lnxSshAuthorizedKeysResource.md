---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxSshAuthorizedKeys erőforrás
ms.openlocfilehash: d4cdb727a94a5e89e8401769f24977d49bcf4929
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687803"
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a>DSC, a Linux nxSshAuthorizedKeys erőforrás

A **nxAuthorizedKeys** erőforrás a PowerShell Desired State Configuration (DSC) biztosít olyan mechanizmus kezelésére jogosult ssh kulcsok egy adott felhasználó.

## <a name="syntax"></a>Szintaxis

```
nxAuthorizedKeys <string> #ResourceName
{
    KeyComment = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ Username = <string> ]
    [ Key = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság |  Leírás |
|---|---|
| KeyComment| A kulcs egyedi megjegyzést. Ez kulcsok egyedi azonosítására szolgál.|
| Győződjön meg, hogy| Itt adhatja meg, hogy van-e adva a kulcs. Ez annak érdekében, hogy a kulcs nem létezik a felhasználó hitelesített kulcsfájlhoz a "Hiányzó" tulajdonság értéke. Állítsa be "E" annak érdekében, hogy a kulcsot a felhasználó hitelesített kulcsfájl definiálva van.|
| Felhasználónév| A felhasználónév kezeléséhez ssh kulcsokat a jogosult. Ha nem, az alapértelmezett felhasználó a "Gyökér".|
| Billentyű| A kulcs a tartalmát. Erre azért szükség, ha **ellenőrizze, hogy** "E" értékre van állítva.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

Az alábbi példa meghatározza az ssh jogosult nyilvános kulcs a felhasználó "monuser".

```
Import-DSCResource -Module nx

Node $node {

nxSshAuthorizedKeys myKey{
   KeyComment = "myKey"
   Ensure = "Present"
   Key = 'ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEA0b+0xSd07QXRifm3FXj7Pn/DblA6QI5VAkDm6OivFzj3U6qGD1VJ6AAxWPCyMl/qhtpRtxZJDu/TxD8AyZNgc8aN2CljN1hOMbBRvH2q5QPf/nCnnJRaGsrxIqZjyZdYo9ZEEzjZUuMDM5HI1LA9B99k/K6PK2Bc1NLivpu7nbtVG2tLOQs+GefsnHuetsRMwo/+c3LtwYm9M0XfkGjYVCLO4CoFuSQpvX6AB3TedUy6NZ0iuxC0kRGg1rIQTwSRcw+McLhslF0drs33fw6tYdzlLBnnzimShMuiDWiT37WqCRovRGYrGCaEFGTG2e0CN8Co8nryXkyWc6NSDNpMzw== rsa-key-20150401'
   UserName = "monuser"
}
}
```