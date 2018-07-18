---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Package erőforrás
ms.openlocfilehash: 3046ba7d57776a996a0b917348a0e863db6cd0c8
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093803"
---
# <a name="dsc-package-resource"></a>DSC-Package erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A **csomag** erőforrás a Windows PowerShell Desired State Configuration (DSC) telepítéséhez vagy eltávolításához a csomagok, például a setup.exe és a Windows Installer csomagokat, a cél csomópont mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
Package [string] #ResourceName
{
    Name = [string]
    Path = [string]
    ProductId = [string]
    [ Arguments = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ ReturnCode = [UInt32[]] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Azt jelzi, hogy a csomag, amelyhez szeretne biztosítani egy adott állapot neve.|
| Elérési út| Azt jelzi, hogy az elérési utat, ahol a csomag található.|
| Termékazonosító| Azt jelzi, hogy a termék azonosítója, amely egyedileg azonosítja a csomagot.|
| Argumentumok| Felsorolja egy karakterlánc, amely a rendszer átad a csomag pontosan a megadott argumentumok.|
| Hitelesítő adatok| A csomag hozzáférést biztosít a távoli forrás. Ez a tulajdonság nem használatos a csomag telepítéséhez. A csomag mindig telepítve van a helyi rendszeren.|
| Győződjön meg, hogy| Azt jelzi, hogy telepítve van-e a csomag. Állítsa be ezt a tulajdonságot a "Hiányzó", győződjön meg arról, a csomag nincs telepítve (vagy távolítsa el a csomagot, ha telepítve van). Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítése.|
| LogPath| Azt jelzi, hogy a teljes elérési útja, ahol azt szeretné, hogy a szolgáltató telepítéséhez, vagy távolítsa el a csomagot a naplófájl mentéséhez.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az **ResourceName** és a típusa **ResourceType**, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".|
| Visszatérési kód:| Azt jelzi, hogy a várt visszatérési kódot. Ha a tényleges visszatérési kód nem egyezik a várt értéknek. Itt, elérhető, a konfigurációs hibát adnak vissza.|

## <a name="example"></a>Példa

Ebben a példában futtatja a .msi-telepítőt, a megadott elérési úton található, és a megadott termék azonosítója.

```powershell
Configuration PackageTest
{
    Package PackageExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Path        = "$Env:SystemDrive\TestFolder\TestProject.msi"
        Name        = "TestPackage"
        ProductId   = "ACDDCDAF-80C6-41E6-A1B9-8ABD8A05027E"
    }
}
```