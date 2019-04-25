---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC WindowsFeatureSet erőforrás
ms.openlocfilehash: 8b7c7e72dd58459bd19cb723e5790a82841515c0
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076786"
---
# <a name="dsc-windowsfeatureset-resource"></a>DSC WindowsFeatureSet erőforrás

> A következőkre vonatkozik: Windows PowerShell 5.0

A **WindowsFeatureSet** erőforrás a Windows PowerShell Desired State Configuration (DSC), győződjön meg arról, hogy szerepkörök és funkciók hozzáadásakor vagy eltávolításakor a cél csomópont mechanizmust biztosít.
Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [WindowsFeature erőforrás](windowsfeatureResource.md) az egyes szolgáltatásokhoz, megadva a `Name` tulajdonság.

Akkor használja ezt az erőforrást, ha szeretne konfigurálni egy Windows-szolgáltatások állapot számát.

## <a name="syntax"></a>Szintaxis

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| A szerepkörök vagy szolgáltatások biztosítására kívánt nevei hozzáadásakor vagy eltávolításakor. Ez ugyanaz, mint az a **neve** tulajdonsága a [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) parancsmagot, és nem a megjelenített nevet a szerepkörök vagy funkciók.|
| Hitelesítő adatok| A hitelesítő adatok hozzáadása vagy eltávolítása a szerepkörök vagy szolgáltatások használata.|
| Győződjön meg, hogy| Azt jelzi-e a szerepkörök vagy szolgáltatások kerülnek. Annak érdekében, hogy a szerepkörök vagy szolgáltatások hozzá, állítsa be ezt a tulajdonságot a "E" annak érdekében, hogy eltávolítja a szerepkörök vagy szolgáltatások, a tulajdonság értéke "Hiányzik".|
| IncludeAllSubFeature| Ez a tulajdonság beállítása **$true** adja meg, ha a szolgáltatásokat az összes szükséges alfunkció tartalmazza a **neve** tulajdonság.|
| LogPath| Ha szeretne bejelentkezni a műveletet az erőforrás-szolgáltató naplófájl elérési útja.|
| DependsOn| Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
| Forrás| Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.|

## <a name="example"></a>Példa

A következő konfiguráció biztosítja, hogy a **webkiszolgálón** (IIS) és **SMTP-kiszolgáló** funkciók és az egyes, az összes alfunkció telepítve vannak.

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        }
    }
}
```
