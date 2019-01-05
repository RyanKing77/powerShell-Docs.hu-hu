---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Registry erőforrás
ms.openlocfilehash: e0ae1a4a27edc08c4e6ccd47786426917eb1ccb4
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048492"
---
# <a name="dsc-registry-resource"></a>DSC-Registry erőforrás

_A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0_

A **beállításjegyzék** erőforrás a Windows PowerShell Desired State Configuration (DSC) kezelése a beállításkulcsok és a egy célcsomóponttal mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Present | Absent }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a>Tulajdonságok

| Tulajdonság | Leírás |
| --- | --- |
| Billentyű| Azt jelzi, hogy az elérési útját, amelyhez szeretne biztosítani adott állapotú beállításkulcs. Ezt az elérési utat tartalmaznia kell a struktúra.|
| Értéknév| A beállításazonosító nevét jelzi. Hozzáadhat és eltávolíthat egy beállításkulcsot, adja meg a tulajdonság egy üres karakterlánccal ValueType vagy értékadat megadása nélkül. Módosíthatja, vagy távolítsa el az alapértelmezett érték egy beállításkulcs, adja meg, ez a tulajdonság egy üres karakterlánccal ValueType vagy értékadat megadása során.|
| Győződjön meg, hogy| Azt jelzi, ha a kulcs-érték létezik-e. Annak érdekében, hogy tesznek, a "E" tulajdonság értéke. Győződjön meg arról, hogy azok nem léteznek, hogy a "Hiányzó" tulajdonság értéke. Az alapértelmezett érték: "E".|
| Force| Ha a megadott beállításkulcs megtalálható, **kényszerített** felülírja azt az új értéket. Ha a beállításkulcs törlése az alkulcsok, ez kell lennie **$true** |
| Hexadecimális| Azt jelzi, ha adatokat hexadecimális formátumban kell megadni. Ha meg van adva, a DWORD/Négyszó típusú érték hexadecimális formátumban jelenik meg. Más fájltípusok nem érvényes. Az alapértelmezett érték **$false**.|
| DependsOn| Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van **ResourceName** és a típusa **ResourceType**, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
| Értékadat| A beállításazonosító adatait.|
| ÉrtékTípusa| Az érték típusát jelzi. A támogatott típusok a következők: Karakterlánc (REG_SZ), a bináris (REG-bináris), Dword 32-bit-es (REG_DWORD), Négyszó típusú 64 bites (REG_QWORD), karakterláncsoros (REG_MULTI_SZ), bővíthető karakterlánc (REG_EXPAND_SZ) |

## <a name="example"></a>Példa

Ebben a példában biztosítja, hogy "ExampleKey" nevű kulcs megtalálható az **HKEY\_helyi\_gép** hive.

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

> [!NOTE]
> Egy beállításjegyzékbeli beállítás módosításával a `HKEY\CURRENT\USER` hive megköveteli, hogy a konfigurációs felhasználói hitelesítő adatokkal, nem pedig a rendszer fut-e. Használhatja a **PsDscRunAsCredential** tulajdonságot adja meg a hitelesítő adatokat a konfigurációt. Egy vonatkozó példáért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../../../configurations/runAsUser.md).
