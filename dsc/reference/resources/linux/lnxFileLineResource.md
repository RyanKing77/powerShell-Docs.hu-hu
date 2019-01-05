---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC, a Linux nxFileLine erőforrás
ms.openlocfilehash: 6a91db25638b09659adfabcec78f91bcb2e69dd9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048237"
---
# <a name="dsc-for-linux-nxfileline-resource"></a>DSC, a Linux nxFileLine erőforrás

A **nxFileLine** erőforrás a PowerShell Desired State Configuration (DSC) kezelése konfigurációs fájl egy Linux-csomóponton belül sorok mechanizmust biztosít.

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
| Fájl elérési útja| A fájl teljes elérési útja a célcsomóponton lévő sorok kezeléséhez.|
| ContainsLine| Győződjön meg arról, hogy egy sort a fájl létezik. Ezt a sort a fájl is bővül, ha nem létezik a fájlban. **ContainsLine** kötelező, de egy üres karakterláncra állítható (`ContainsLine = ""`) Ha már nincs szükség.|
| DoesNotContainPattern| A sorokat, amelyek a fájl nem létezhet Reguláriskifejezés-mintának. Olyan sort, amely létezik a fájlban a reguláris kifejezésnek megfelelő a sort a fájl törlődik.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például ha a **azonosító** az erőforrás, amely a futtatni kívánt konfigurációs parancsprogram-blokkot első az **ResourceName** és a típusa **ResourceType**, ezzel esetén a tulajdonság `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Példa

Ebben a példában használatát mutatja be a **nxFileLine** erőforrás konfigurálása az `/etc/sudoers` fájl, biztosítva, hogy a felhasználó: monuser nem requiretty van konfigurálva.

```powershell
Import-DscResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```