---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsProcess erőforrás
ms.openlocfilehash: 3c4e6d8377c3dcbf4f1db87a603d5483b8caafb8
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093735"
---
# <a name="dsc-windowsprocess-resource"></a>DSC WindowsProcess erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A **WindowsProcess** erőforrás a Windows PowerShell Desired State Configuration (DSC) cél csomóponton folyamatok konfigurálása mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Argumentumok| Azt jelzi, hogy egy karakterlánc, a folyamat argumentumokat-van. Ha több argumentumokat át van szüksége, helyezi őket az ezt a karakterláncot.|
| Elérési út| A folyamat végrehajtható fájl elérési útja. Ha ez a végrehajtható fájl (nem teljes elérési útja), a DSC-erőforrás neve fog keresni a környezet **elérési** változó (`$env:Path`) található a végrehajtható fájl. Ha ez a tulajdonság értéke teljes elérési útja, DSC nem fogja használni a **elérési út** környezeti változót, keresse meg a fájlt, és hibát váltja, ha az elérési út nem létezik. Relatív elérési utakat nem engedélyezettek.|
| Hitelesítő adatok| Azt jelzi, hogy a hitelesítő adatokat a folyamat indításához.|
| Győződjön meg, hogy| Azt jelzi, hogy létezik-e a folyamat. Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy létezik-e a folyamat. Ellenkező esetben állítsa "Hiányzik". Az alapértelmezett érték "E".|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az **ResourceName** és a típusa **ResourceType**, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".|
| StandardErrorPath| Azt jelzi, hogy a könyvtár elérési útja a normál hiba írni. Minden olyan meglévő fájl felül lesznek írva.|
| StandardInputPath| A szabványos bemeneti helyét jelöli.|
| StandardOutputPath| Azt jelzi, hogy a hely a normál a kimenetbe írhat. Minden olyan meglévő fájl felül lesznek írva.|
| WorkingDirectory| Azt jelzi, hogy a helyre, amely a folyamat az aktuális munkakönyvtár lesz.|