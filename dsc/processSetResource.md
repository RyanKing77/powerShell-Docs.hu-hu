---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC ProcessSet erőforrás"
ms.openlocfilehash: b713d1a9c34eab6966de4f342991ead32c19df5d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-windowsprocess-resource"></a>A DSC WindowsProcess erőforrás

> Vonatkozik: A Windows PowerShell 5.0

A **ProcessSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) folyamatok konfigurálása egy célcsomóponttal mechanizmust biztosít. Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsProcess erőforrás](windowsProcessResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.

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
|  Tulajdonság  |  Leírás   | 
|---|---| 
| Argumentumok| A folyamat, argumentumokat tartalmazó karakterlánc-értéke. Ha több argumentumot továbbítani kell, helyezze őket az összes ezt a karakterláncot.| 
| Elérési út| A folyamat végrehajtható fájlok elérési útjait. Ha a végrehajtható fájlok (teljesen minősített elérési utak) nevét, a DSC-erőforrás keressen-e a környezet **elérési** változó (`$env:Path`) található a fájl. Ha ez a tulajdonság értékének teljesen minősített elérési utak, DSC nem fogja használni a **elérési** környezeti változó található a fájl, és kivételhibát hiba történt az elérési utak közül bármelyik nem léteznek. Relatív útvonalak nem engedélyezettek.| 
| hitelesítő adatok| Azt jelzi, hogy a hitelesítő adatokat kell elindítania a telepítést.| 
| Győződjön meg arról| Meghatározza, hogy létezik-e a folyamatokat. Állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy létezik-e a folyamat. Egyéb esetben állítsa "Hiányzik". Az alapértelmezett érték az "Elérhető".| 
| StandardErrorPath| Az elérési utat, amelyhez a folyamatok írási standard hiba. Felülírja a meglévő fájlt.| 
| StandardInputPath| Az adatfolyam, ahonnan a folyamat szabványos bemeneti kapja.| 
| StandardOutputPath| A fájl elérési útját a, amelyhez a folyamat szabványos kimeneti írása. Felülírja a meglévő fájlt.| 
| WorkingDirectory| A folyamatok, az aktuális munkakönyvtárban használt helyet.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **_ResourceType**, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".| 

