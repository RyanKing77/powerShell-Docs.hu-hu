---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-WindowsOptionalFeature erőforrás
ms.openlocfilehash: 390caefd2ad190afc651b22ed1beb5cf1d604527
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685444"
---
# <a name="dsc-windowsoptionalfeature-resource"></a>DSC-WindowsOptionalFeature erőforrás

> Érvényes: Windows PowerShell 5.0

A **WindowsOptionalFeature** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy választható szolgáltatások engedélyezve vannak-e a cél csomópont mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Azt jelzi, hogy azt szeretné, a szolgáltatás neve engedélyezve van, vagy le van tiltva.|
| Győződjön meg, hogy| Itt adhatja meg, hogy engedélyezve van-e a szolgáltatás. Annak érdekében, hogy a funkció engedélyezve van, állítsa be ezt a tulajdonságot az "Engedélyezés" annak érdekében, hogy a szolgáltatás le van tiltva, a tulajdonság értéke "Letiltás".|
| Forrás| Není implementována.|
| NoWindowsUpdateCheck| Itt adhatja meg, e DISM csatlakozik-e a Windows Update (WU), a funkció engedélyezéséhez a forrásfájlok keresésekor. Ha $true, DISM nem lép kapcsolatba a WU-hoz.|
| RemoveFilesOnDisable| Állítsa **$true** eltávolítja, ha le van tiltva a szolgáltatás kapcsolódó fájlok (azt jelenti, amikor **ellenőrizze, hogy** van beállítva a "Hiányzó").|
| Naplózási szint| A naplókban megjelenő legnagyobb kimeneti szintet. Az elfogadott értékek a következők: (Csak a hibák naplózása) "ErrorsOnly", "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információkat naplózza).|
| LogPath| Ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.|
| DependsOn| Itt adhatja meg, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|