---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC ProcessSet erőforrás
ms.openlocfilehash: 33000786a9e17e11168b5e08c3bcfcacf3af2611
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268017"
---
# <a name="dsc-windowsprocess-resource"></a>DSC WindowsProcess erőforrás

_A következőkre vonatkozik: Windows PowerShell 5.0_

A **ProcessSet** erőforrás a Windows PowerShell Desired State Configuration (DSC) cél csomóponton folyamatok konfigurálása mechanizmust biztosít. Ez az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsProcess erőforrás](windowsProcessResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.

## <a name="syntax"></a>Szintaxis

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Tulajdonságok

| Tulajdonság | Leírás |
| --- | --- |
| Argumentumok| A folyamat, argumentumokat tartalmazó karakterlánc-van. Ha több argumentumokat át van szüksége, helyezi őket az ezt a karakterláncot.|
| Elérési út| A folyamat végrehajtható fájlok elérési útja. Ha tartoznak a végrehajtható fájlok (teljesen minősített elérési út) nevét, a DSC-erőforrás fog keresni a környezet **elérési útja** változó (`$env:Path`) található fájlokat. Ha ez a tulajdonság értékét teljesen minősített elérési utak, DSC nem fogja használni a **elérési útja** környezeti változót, keresse meg a fájlokat, és hibát váltja, ha bármely, az elérési utak nem léteznek. Relatív elérési utakat nem engedélyezettek.|
| Hitelesítő adatok| Azt jelzi, hogy a hitelesítő adatokat a folyamat indításához.|
| Győződjön meg, hogy| Itt adhatja meg, hogy létezik-e a folyamatokat. Ezzel a tulajdonsággal, "E" Győződjön meg arról, hogy létezik-e a folyamat. Ellenkező esetben állítsa "Hiányzik". Az alapértelmezett érték "E".|
| StandardErrorPath| Az elérési út, amelyre a folyamatok írási standard hiba. Minden olyan meglévő fájl felül lesznek írva.|
| StandardInputPath| A streamet, amelyből a folyamat megkapja a standard bemenetet.|
| StandardOutputPath| A fájl, amelyre a folyamatok írási standard kimenet elérési útja. Minden olyan meglévő fájl felül lesznek írva.|
| WorkingDirectory| A folyamatok, az aktuális munkakönyvtárban használt helyet.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **_ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"` .|