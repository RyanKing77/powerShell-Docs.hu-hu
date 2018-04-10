---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC WindowsPackageCab erőforrás
ms.openlocfilehash: af45956c1fe8cffa1d7fd779847eded9e3f6b51e
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-windowspackagecab-resource"></a>A DSC WindowsPackageCab erőforrás

> Vonatkozik: A Windows PowerShell 5.1-es és újabb verziók

A **WindowsPackageCab** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) telepítéséhez vagy eltávolításához Windows kabinetfájl (.cab) csomagok egy célcsomóponttal mechanizmust biztosít.

A célként megadott csomópont nem rendelkezhet a DISM PowerShell-modul telepítve. További információ: [a Windows PowerShell használata a DISM](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).


## <a name="syntax"></a>Szintaxis

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| A csomag nevét jelöli, a szeretne biztosítani adott állapotú.|
| Győződjön meg arról| Azt jelzi, ha a csomag telepítve van-e. Állítsa be ezt a tulajdonságot "Hiányzik", győződjön meg arról, a csomag nincs telepítve (vagy a csomag eltávolítása, ha telepítve van). Állítsa be azt, hogy "" (az alapértelmezett érték) annak érdekében, hogy a csomag telepítve van.|
| Elérési út| Azt jelzi, hogy az elérési utat, amelyen a csomag található.|
| LogPath| Azt jelzi, hogy a teljes elérési útja, ha azt szeretné, hogy a szolgáltatót, amelyet telepíteni, vagy távolítsa el a csomagot naplófájlt.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az **ResourceName** és annak típusa **ResourceType**, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".|

## <a name="example"></a>Példa

A következő példa konfiguráció bemeneti paraméterek fogadja el, és biztosítja, hogy a kabinetfájl által megadott a `$Name` paraméter van telepítve.

```powershell
Configuration Sample_WindowsPackageCab
{
    param
    (
        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $Name,

        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $SourcePath,

        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $LogPath
    )

    Import-DscResource -ModuleName 'PSDscResources'

    WindowsPackageCab WindowsPackageCab1
    {
        Name = $Name
        Ensure = 'Present'
        SourcePath = $SourcePath
        LogPath = $LogPath
    }
}
```