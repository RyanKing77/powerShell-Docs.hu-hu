---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-környezet erőforrás"
ms.openlocfilehash: 9c166d719ba3f168c936278acd6fb5fb7658613e
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-environment-resource"></a>A DSC-környezet erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A __környezet__ erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a rendszerszintű környezeti változókat kezeléséhez.

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
| Név| A környezeti változó, amelyekhez egy adott állapot biztosításához nevét jelöli.| 
| Győződjön meg arról| Azt jelzi, hogy létezik-e egy változót. Ez a tulajdonság beállítása __jelen__ a környezeti változó létrehozása, ha nem létezik, vagy győződjön meg arról, hogy annak értéke megegyezik-e a keresztül elérhető a __érték__ tulajdonságot, ha a változó már létezik. Állítsa az értékét __távol__ törli a változót, ha van ilyen.| 
| Elérési út| Határozza meg a konfigurálni kívánt környezeti változó. Ez a tulajdonság beállítása __$true__ Ha a változó a __elérési__ változó; ellenkező esetben állítsa __$false__. Az alapértelmezett érték __$false__. Ha a konfigurálni kívánt változó a __elérési__ változó, a megadott érték keresztül a __érték__ tulajdonság hozzáfűzi a meglévő értéket.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 
| Érték| A környezeti változóhoz rendelhető érték.| 

## <a name="example"></a>Példa

Az alábbi példa biztosítja, hogy __TestEnvironmentVariable__ található és értéke __TestValue__. Ha nincs jelen, létrehozza azt.

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```

