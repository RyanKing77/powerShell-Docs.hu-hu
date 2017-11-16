---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-beállításjegyzék erőforrás"
ms.openlocfilehash: 649cb60578c053c04a7fcc7446881fb76daee26a
ms.sourcegitcommit: 79e8f03afb8d0b0bb0a167e56464929b27f51990
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/26/2017
---
# <a name="dsc-registry-resource"></a>A DSC-beállításjegyzék erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **beállításjegyzék** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a beállításkulcsok és a cél csomópont értékek kezeléséhez.

## <a name="syntax"></a>Szintaxis

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a>Tulajdonságok
|  Tulajdonság  |  Leírás   | 
|---|---| 
| Billentyű| Azt jelzi, hogy a beállításkulcs, amelyekhez egy adott állapot biztosításához elérési útját. Ezt az elérési utat tartalmaznia kell a struktúra.| 
| ValueName| A beállításazonosító nevét jelöli. Hozzáadni vagy eltávolítani egy beállításkulcsot, adja meg ennek a tulajdonságnak egy üres karakterlánccal ValueType vagy értékadat megadása nélkül. Vagy távolítsa el az alapértelmezett érték a beállításkulcsok módosításához adja meg ezt a tulajdonságot is meg ValueType vagy értékadat egy üres karakterlánccal.| 
| Győződjön meg arról| Azt jelzi, ha a kulcs és az érték szerepel. Győződjön meg arról, hogy így tesznek, állítsa ezt a tulajdonságot "Elérhető". Győződjön meg arról, hogy azok nem léteznek, hogy a "Hiányzik" tulajdonság értéke. Az alapértelmezett érték: "Elérhető".| 
| Force| Ha a megadott beállításkulcs megtalálható, __kényszerített__ felülírja az új értékkel. Ha a beállításkulcs törlése az alkulcsok, ez kell lennie __$true__| 
| Hexadecimális| Azt jelzi, ha adatokat hexadecimális formátumban kell megadni. Ha meg van adva, a DWORD/Négyszó érték hexadecimális formátumban jelenik meg. Más esetén nem érvényes. Az alapértelmezett érték __$false__.| 
| dependsOn| Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 
| Értékadat| A beállításjegyzék-értékben adatai.| 
| ÉrtékTípusa| Azt jelzi, hogy az érték típusa. A támogatott típusok a következők: 
<ul><li>Karakterlánc (REG_SZ)</li>


<li>Bináris (REG bináris)</li>


<li>32 bites DWORD (REG_DWORD)</li>


<li>Négyszó 64 bites (REG_QWORD)</li>


<li>Karakterlánc (REG_MULTI_SZ)</li>


<li>Bővíthető karakterlánc (REG_EXPAND_SZ)</li></ul>

## <a name="example"></a>Példa
Ez a példa biztosítja, hogy "ExampleKey" nevű kulcs megtalálható-e a **HKEY\_helyi\_gép** struktúra.
```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

>**Megjegyzés:** egy beállításjegyzék-beállítást, a módosítás a **HKEY\_aktuális\_felhasználói** hive megköveteli, hogy a konfigurációs felhasználói hitelesítő adatokkal, nem pedig a rendszer fut-e.
>Használhatja a **PsDscRunAsCredential** meg felhasználói hitelesítő adatok a konfigurációs tulajdonság. Egy vonatkozó példáért lásd: [DSC futtató felhasználó hitelesítő adataival](runAsUser.md)



