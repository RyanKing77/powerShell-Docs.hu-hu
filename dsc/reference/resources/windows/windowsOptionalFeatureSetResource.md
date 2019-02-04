---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsOptionalFeatureSet erőforrás
ms.openlocfilehash: c27d026e01bbb443a82112e37f1d199fb3482e49
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55683946"
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a>DSC WindowsOptionalFeatureSet erőforrás

> Érvényes: Windows PowerShell 5.0

A **WindowsOptionalFeatureSet** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy választható szolgáltatások engedélyezve vannak-e a cél csomópont mechanizmust biztosít.
Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [WindowsOptionalFeature erőforrás](windowsOptionalFeatureResource.md) az egyes szolgáltatásokhoz, megadva a `Name` tulajdonság.

Akkor használja ezt az erőforrást, ha szeretne konfigurálni egy választható funkciók Windows állapot számát.

## <a name="syntax"></a>Szintaxis

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogPath = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Azt jelzi, hogy a biztosítani kívánt szolgáltatások nevére vannak engedélyezve vagy letiltva.|
| Győződjön meg, hogy| Itt adhatja meg, hogy engedélyezve vannak-e az a funkciók. Annak érdekében, hogy az funkciók engedélyezve van, állítsa be ezt a tulajdonságot az "Engedélyezés" annak érdekében, hogy a szolgáltatások le vannak tiltva, a tulajdonság értéke "Letiltás".|
| Forrás| Není implementována.|
| NoWindowsUpdateCheck| Itt adhatja meg, e DISM csatlakozik-e a Windows Update (WU),-szolgáltatások engedélyezése a forrásfájlok keresése. Ha $true, DISM nem lép kapcsolatba a WU-hoz.|
| RemoveFilesOnDisable| Beállítása **$true** eltávolítja, ha le vannak tiltva, az a funkciók az hozzárendelt összes fájl (azt jelenti, amikor **ellenőrizze, hogy** be van állítva a "Hiányzó").|
| Naplózási szint| A naplókban megjelenő legnagyobb kimeneti szintet. Az elfogadott értékek a következők: (Csak a hibák naplózása) "ErrorsOnly", "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információkat naplózza).|
| LogPath| Ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.|
| DependsOn| Itt adhatja meg, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
