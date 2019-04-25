---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-környezeti erőforrás
ms.openlocfilehash: 2bc1600a9df32538d59efa712569b12fa9e3beee
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077534"
---
# <a name="dsc-environment-resource"></a>DSC-környezeti erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A __környezet__ erőforrás a Windows PowerShell Desired State Configuration (DSC) kezeléséhez rendszerszintű környezeti változókat mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Azt jelzi, hogy a neve, amelyhez szeretne biztosítani adott állapotú környezeti változó.|
| Győződjön meg, hogy| Azt jelzi, hogy létezik-e egy változóban. Ez a tulajdonság beállítása __jelen__ a környezeti változó létrehozásához, ha még nem létezik, vagy győződjön meg arról, hogy az érték megegyezik-e a keresztül biztosított a __érték__ tulajdonságot, ha a változó már létezik. Állítsa be __távol__ , ha létezik, törölje a változót.|
| Elérési út| A konfigurálni kívánt környezeti változó határozza meg. Ez a tulajdonság beállítása __$true__ Ha a változó a __elérési__ változó; ellenkező esetben beállíthatja azt a __$false__. Az alapértelmezett érték __$false__. Ha a változó konfigurált a __elérési__ változóhoz, a megadott érték keresztül a __érték__ tulajdonság hozzá lesznek fűzve a meglévő értéket.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
| Érték| Rendelhet hozzá a környezeti változó értéke.|

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy __TestEnvironmentVariable__ található és értéke __TestValue__. Ha nem található, létrehozza azt.

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```