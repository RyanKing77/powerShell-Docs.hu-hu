---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC WindowsFeatureSet erőforrás
ms.openlocfilehash: 582f9b1f439056118680f6f814d2c202d0e823be
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186728"
---
# <a name="dsc-windowsfeatureset-resource"></a>A DSC WindowsFeatureSet erőforrás

> Vonatkozik: A Windows PowerShell 5.0

A **WindowsFeatureSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) Győződjön meg arról, hogy szerepkörök és szolgáltatások hozzáadása vagy eltávolítása egy célcsomóponttal mechanizmust biztosít.
Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [WindowsFeature erőforrás](windowsfeatureResource.md) az egyes szolgáltatásokhoz megadott a `Name` tulajdonság.

Ehhez az erőforráshoz akkor használja, ha a Windows-szolgáltatások számos állapot konfigurálni szeretné.

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
| Név| A szerepkörök vagy szolgáltatások biztosítása kívánt nevét hozzáadásakor vagy eltávolításakor. Ez megegyezik a **neve** tulajdonsága a [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) parancsmag, és nem a megjelenített név a szerepkörök vagy szolgáltatások.|
| hitelesítő adatok| A hitelesítő adatok hozzáadása vagy eltávolítása a szerepkörök vagy szolgáltatások használatára.|
| Győződjön meg arról| Azt jelzi, hogy a szerepkörök vagy szolgáltatások kerülnek. Ezzel biztosíthatja, hogy a szerepkörök vagy szolgáltatások hozzáadott, állítsa be ezt a tulajdonságot "Elérhető" Győződjön meg arról, hogy eltávolítja a szerepkörök vagy szolgáltatások, a tulajdonság értéke "Hiányzik".|
| IncludeAllSubFeature| Ez a tulajdonság beállítása **$true** tartalmazza a Funkciók, adja meg az összes szükséges alfunkció a **neve** tulajdonság.|
| LogPath| A naplófájl elérési útja a kívánt való bejelentkezéshez a műveletet az erőforrás-szolgáltató.|
| dependsOn| Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|
| Forrás| Azt jelzi, használható a telepítéshez, a forrás-fájl helyét, ha szükséges.|

## <a name="example"></a>Példa

A következő konfigurációs biztosítja, hogy a **webkiszolgáló** (IIS) és **SMTP-kiszolgáló** funkciók és összes részszolgáltatása, is települnek.

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