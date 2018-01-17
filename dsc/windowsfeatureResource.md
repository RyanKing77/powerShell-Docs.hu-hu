---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-WindowsFeature erőforrás"
ms.openlocfilehash: 3dd4a9c6f11b0c76054ca3e95796cab8e709a7c6
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsfeature-resource"></a>A DSC-WindowsFeature erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A **WindowsFeature** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) Győződjön meg arról, hogy szerepkörök és szolgáltatások hozzáadása vagy eltávolítása egy célcsomóponttal mechanizmust biztosít.

## <a name="syntax"></a>Szintaxis

```
WindowsFeature [string] #ResourceName
{
    Name = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ IncludeAllSubFeature = [bool] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    [ Source = [string] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   | 
|---|---| 
| Név| Azt jelzi, biztosítani kívánt szerepkör vagy szolgáltatás neve hozzáadni vagy eltávolítani. Megegyezik a a __neve__ tulajdonságot a [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) parancsmagot, és nem a szerepkör vagy szolgáltatás megjelenített nevét.| 
| hitelesítő adatok| Azt jelzi, hogy a hitelesítő adatok hozzáadása vagy eltávolítása a szerepkör vagy szolgáltatás használata.| 
| Győződjön meg arról| Azt jelzi, ha a szerepkör vagy szolgáltatás kerül. Annak biztosításához, hogy a szerepkör vagy szolgáltatás hozzá, állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy a szerepkör vagy szolgáltatás eltávolítása a tulajdonság értéke "Hiányzik".| 
| IncludeAllSubFeature| Ez a tulajdonság beállítása __$true__ adja meg, ha az összes szükséges alfunkció és a szolgáltatás állapotának állapotának biztosításához a __neve__ tulajdonság.| 
| LogPath| Azt jelzi, hogy a naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.| 
| dependsOn| Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.| 
| Forrás| Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.| 

## <a name="example"></a>Példa
```powershell
WindowsFeature RoleExample
{
    Ensure = "Present" 
    # Alternatively, to ensure the role is uninstalled, set Ensure to "Absent"
    Name = "Web-Server" # Use the Name property from Get-WindowsFeature  
}
```

