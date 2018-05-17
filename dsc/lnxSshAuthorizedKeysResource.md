---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A Linux nxSshAuthorizedKeys erőforrás DSC
ms.openlocfilehash: d4cdb727a94a5e89e8401769f24977d49bcf4929
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-for-linux-nxsshauthorizedkeys-resource"></a>A Linux nxSshAuthorizedKeys erőforrás DSC

A **nxAuthorizedKeys** erőforrás a PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) biztosít egy olyan mechanizmus kezelésére jogosult ssh egy adott felhasználó kulcsok.

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
| KeyComment| A kulcs egyedi megjegyzés. A kulcsok egyedi azonosítására szolgál.|
| Győződjön meg arról| Meghatározza, hogy van-e adva a kulcs. Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a kulcs nem létezik a felhasználó jogosult kulcsok fájlba. Állítsa az "Elérhető" annak érdekében, hogy a felhasználó jogosult kulcsfájl definiálva van a kulcs értékét.|
| Felhasználónév| Kezeléséhez ssh felhasználónév jogosult kulcsokat. Ha nincs megadva, az alapértelmezett felhasználói a "Gyökér".|
| Billentyű| A kulcs a tartalmát. Erre azért szükség, ha **ellenőrizze, hogy** "Elérhető" értékre van állítva.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például ha a **azonosító** az erőforrás konfigurációs futtatni kívánt először parancsprogramblokkja **ResourceName** és annak típusa **ResourceType**, ez a szintaxis a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

Az alábbi példa meghatározza ssh jogosult nyilvános kulcsát, a felhasználó "monuser".

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