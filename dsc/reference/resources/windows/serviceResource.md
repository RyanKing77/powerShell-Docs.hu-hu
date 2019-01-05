---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC szolgáltatás-erőforrás
ms.openlocfilehash: 09571bd0eaa428e7d0bb7a533d6ad1c0c936e2cf
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048241"
---
# <a name="dsc-service-resource"></a>DSC szolgáltatás-erőforrás

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0


A **szolgáltatás** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére.

## <a name="syntax"></a>Szintaxis

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Név| Azt jelzi, hogy a szolgáltatás nevét. Vegye figyelembe, hogy egyes esetekben ez különbözik a megjelenítendő nevét. A szolgáltatások és azok aktuális állapotát a Get-Service-parancsmaggal kaphat.|
| BuiltInAccount| Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatást. A Pro tuto vlastnost engedélyezett értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.|
| Hitelesítő adatok| Azt jelzi, hogy a szolgáltatás alatt fut, a fiók hitelesítő adatait. Ez a tulajdonság és a __BuiltinAccount__ tulajdonság nem használható együtt.|
| DependsOn| Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója letiltása, a futtatni kívánt parancsfájl először van __ResourceName__ és a típusa __ResourceType__, ez a tulajdonság használata esetén `DependsOn = "[ResourceType]ResourceName"`.|
| Indítási típusa| A szolgáltatás indítási típusát jelzi. A Pro tuto vlastnost engedélyezett értékek a következők: **Automatikus**, **letiltott**, és **manuális**|
| Állapot| Szeretne biztosítani a szolgáltatás állapotát jelzi.|
| Leírás | Azt jelzi, hogy a célként megadott szolgáltatás leírását.|
| DisplayName | Azt jelzi, hogy a célként megadott szolgáltatás megjelenített nevét.|
| Győződjön meg, hogy | Azt jelzi, hogy a célként megadott szolgáltatás létezik-e a rendszer. Ez a tulajdonság beállítása **távol** annak érdekében, hogy a célként megadott szolgáltatás nem létezik. Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a célként megadott szolgáltatás.|
| Elérési út | Azt jelzi, hogy a szolgáltatást, a bináris fájl elérési útját.|

## <a name="example"></a>Példa

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```