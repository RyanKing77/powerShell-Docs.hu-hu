---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC WindowsOptionalFeatureSet erőforrás"
ms.openlocfilehash: 3bf6a993d0ec9ce71c1e9222ddaa3bb429accb15
ms.sourcegitcommit: 79e8f03afb8d0b0bb0a167e56464929b27f51990
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/26/2017
---
# <a name="dsc-windowsoptionalfeatureset-resource"></a>A DSC WindowsOptionalFeatureSet erőforrás

> Vonatkozik: A Windows PowerShell 5.0

A **WindowsOptionalFeatureSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi annak érdekében, hogy az választható szolgáltatások engedélyezve vannak-e a célcsomóponton. Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsOptionalFeature erőforrás](windowsOptionalFeatureResource.md) az egyes szolgáltatásokhoz megadott a `Name` tulajdonság.

Ehhez az erőforráshoz akkor használja, ha a Windows választható szolgáltatások állapot számos konfigurálni szeretné.

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
| Név| Azt jelzi, a funkciókat, amelyeket szeretne biztosítani a neve engedélyezésekor vagy letiltásakor.| 
| Győződjön meg arról| Meghatározza, hogy engedélyezett-e a szolgáltatásokat. Ezzel biztosíthatja, hogy a szolgáltatások engedélyezett, állítsa be ezt a tulajdonságot "Engedélyezés" Győződjön meg arról, hogy a szolgáltatások le vannak tiltva, a tulajdonság értéke "Letiltás".|
| Forrás| Nincs megvalósítva.|
| NoWindowsUpdateCheck| Meghatározza, hogy DISM kapcsolódik-e a Windows Update (WU), a funkciók engedélyezésére forrásfájlok keresésekor. Ha $true, DISM nem tud kapcsolódni a WU.|
| RemoveFilesOnDisable| Beállítása **$true** eltávolítja, ha le vannak tiltva, a szolgáltatások társított összes fájlt (Ez azt jelenti, hogy ha **ellenőrizze, hogy** be van állítva a "Hiányzik").|
| Naplózási szint| A naplókban megjelenő legnagyobb kimeneti szintet. Az elfogadott értékei: "ErrorsOnly" (csak a hibák naplózása), "ErrorsAndWarning" (hibák és figyelmeztetések naplózása van), és a "ErrorsAndWarningAndInformation" (hibák figyelmeztetések és hibakeresési információ bejelentkezett).|
| LogPath| A naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.| 
| dependsOn| Meghatározza, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 
 



