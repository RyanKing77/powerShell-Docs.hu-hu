---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-WindowsOptionalFeature erőforrás"
ms.openlocfilehash: 388fbe1bc430098d6680902e0b5643243fbf7f4c
ms.sourcegitcommit: 79e8f03afb8d0b0bb0a167e56464929b27f51990
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/26/2017
---
# <a name="dsc-windowsoptionalfeature-resource"></a>A DSC-WindowsOptionalFeature erőforrás

> Vonatkozik: A Windows PowerShell 5.0

A **WindowsOptionalFeature** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi annak érdekében, hogy az választható szolgáltatások engedélyezve vannak-e a célcsomóponton.

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
| Név| Azt jelzi, hogy biztos szeretne lenni abban a szolgáltatás neve engedélyezve vagy letiltva.| 
| Győződjön meg arról| Meghatározza, hogy engedélyezve van-e a szolgáltatás. Annak biztosításához, hogy a szolgáltatás engedélyezve van, állítsa be ezt a tulajdonságot "Engedélyezés" Győződjön meg arról, hogy a szolgáltatás le van tiltva, a tulajdonság értéke "Letiltás".|
| Forrás| Nincs megvalósítva.|
| NoWindowsUpdateCheck| Meghatározza, hogy DISM kapcsolódik-e a Windows Update (WU), a funkció engedélyezéséhez a forrásfájlok keresésekor. Ha $true, DISM nem tud kapcsolódni a WU.|
| RemoveFilesOnDisable| Beállítása **$true** eltávolítja, ha le van tiltva, a szolgáltatás társított összes fájlt (Ez azt jelenti, hogy ha **ellenőrizze, hogy** be van állítva a "Hiányzik").|
| Naplózási szint| A naplókban megjelenő legnagyobb kimeneti szintet. Az elfogadott értékei: "ErrorsOnly" (csak a hibák naplózása), "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információ bejelentkezett).|
| LogPath| A naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.| 
| dependsOn| Meghatározza, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 
 



