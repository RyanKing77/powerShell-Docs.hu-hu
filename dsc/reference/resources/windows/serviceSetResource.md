---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC ServiceSet erőforrás
ms.openlocfilehash: 5694c2abc5c0caf0098670b629af464b35125583
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076834"
---
# <a name="dsc-serviceset-resource"></a>DSC ServiceSet erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A **ServiceSet** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére. Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [erőforrás szolgáltatás](serviceResource.md) minden egyes megadott szolgáltatás a `Name` tulajdonság.

Használja ezt az erőforrást, ha a szolgáltatásokat állapot konfigurálni szeretné.

## <a name="syntax"></a>Szintaxis

```
Service [string] #ResourceName
{
    Name = [string[]]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Azt jelzi, hogy a szolgáltatás nevét. Vegye figyelembe, hogy egyes esetekben ez különbözik a megjelenítendő nevét. A szolgáltatások és a jelenlegi állapotuk listát kap a [Get-Service](https://technet.microsoft.com/library/hh849804.aspx) parancsmagot.|
| StartupType| A szolgáltatás indítási típusát jelzi. A Pro tuto vlastnost engedélyezett értékek a következők: **Automatikus**, **letiltott**, és **manuális**|
| BuiltInAccount| Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatásokat. A Pro tuto vlastnost engedélyezett értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.|
| Állapot| Szeretne biztosítani a szolgáltatások állapotát jelzi: **Leállítva** vagy **futó**.|
| Győződjön meg, hogy| Azt jelzi, hogy a szolgáltatások létezik-e a rendszer. Ez a tulajdonság beállítása **távol** , győződjön meg arról, hogy a szolgáltatások nem létezik. Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a cél-szolgáltatások.|
| Hitelesítő adatok| Azt jelzi, hogy a szolgáltatás-erőforrás fog futni a fiók hitelesítő adatait. Ez a tulajdonság és a **BuiltinAccount** tulajdonság nem használható együtt.|
| DependsOn| Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van *ResourceName* és a típusa *ResourceType*, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|



## <a name="example"></a>Példa

A következő konfigurációt elindítja a "Windows hang" és "Távoli asztali szolgáltatások" szolgáltatásokat.

```powershell
configuration ServiceSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        ServiceSet ServiceSetExample
        {
            Name        = @("TermService", "Audiosrv")
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```
