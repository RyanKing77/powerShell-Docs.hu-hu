---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC-csomag erőforrás
ms.openlocfilehash: 16f7f1b8fa7b84bcfdeb09fdc46db9c93113e70c
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34188530"
---
# <a name="dsc-package-resource"></a>A DSC-csomag erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **csomag** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához csomagok, például a setup.exe és a Windows Installer-csomagokat a egy célcsomóponttal mechanizmust biztosít.

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
| Név| Azt jelzi, amelyekhez egy adott állapot biztosításához a csomag nevét.|
| Elérési út| Azt jelzi, hogy az elérési utat, amelyen a csomag található.|
| Termékazonosító| Azt jelzi, hogy a termék azonosítója, amely egyedileg azonosítja a csomagot.|
| Argumentumok| Az átadott csomag pontosan megegyezik a megadott argumentumok karakterlánc sorolja fel.|
| hitelesítő adatok| A csomag hozzáférést biztosít a távoli adatforráson. Ez a tulajdonság nem használható a csomag telepítéséhez. A csomag mindig telepítve van a helyi rendszeren.|
| Győződjön meg arról| Azt jelzi, ha a csomag telepítve van-e. Állítsa be ezt a tulajdonságot "Hiányzik", győződjön meg arról, a csomag nincs telepítve (vagy a csomag eltávolítása, ha telepítve van). Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítve van.|
| LogPath| Azt jelzi, hogy a teljes elérési útja, ha azt szeretné, hogy a szolgáltatót, amelyet telepíteni, vagy távolítsa el a csomagot naplófájlt.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **ResourceType**, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".|
| Visszatérési kód:| Azt jelzi, hogy a várt visszatérési kód. Ha a tényleges visszatérési kód nem egyezik a várt érték megadva itt, a konfigurációs hibát adnak vissza.|

## <a name="example"></a>Példa

Ez a példa futtatja a .msi telepítő, amely a megadott elérési úton található, és nem a megadott termékkulcs azonosítója.

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