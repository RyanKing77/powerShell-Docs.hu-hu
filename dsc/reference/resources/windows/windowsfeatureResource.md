---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-WindowsFeature erőforrás
ms.openlocfilehash: 7a57f4b2797ab3bb202aea8b2543d1e3f14074e9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685969"
---
# <a name="dsc-windowsfeature-resource"></a>DSC-WindowsFeature erőforrás

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A **WindowsFeature** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy szerepkörök és funkciók hozzáadásakor vagy eltávolításakor a cél csomópont mechanizmust biztosít.

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
| Név| Azt jelzi, hogy biztosítani kívánt szerepkör vagy szolgáltatás neve hozzáadva vagy eltávolítva. Ez ugyanaz, mint az a __neve__ tulajdonságot a [Get-WindowsFeature](/powershell/module/servermanager/Get-WindowsFeature) parancsmagot, és nem a szerepkör vagy szolgáltatás megjelenített nevét.|
| Hitelesítő adatok| Azt jelzi, hogy a hitelesítő adatok hozzáadása vagy eltávolítása a szerepkör vagy szolgáltatás használatára.|
| Győződjön meg, hogy| Azt jelzi, ha a szerepkör vagy szolgáltatás kerül. Annak érdekében, hogy a szerepkör vagy szolgáltatás hozzá, állítsa be ezt a tulajdonságot a "E" annak érdekében, hogy a szerepkör vagy szolgáltatás eltávolítása a tulajdonság értéke "Hiányzik".|
| IncludeAllSubFeature| Ez a tulajdonság beállítása __$true__ adja meg a szolgáltatás állapotával minden szükséges alfunkció állapotának biztosítása érdekében a __neve__ tulajdonság.|
| LogPath| Azt jelzi, ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.|
| DependsOn| Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
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