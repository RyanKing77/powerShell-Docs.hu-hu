---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A DSC szolgáltatás erőforrás
ms.openlocfilehash: 3e2db8999ab1db2964f88e1ee14c6ad6e641c5e3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-service-resource"></a>A DSC szolgáltatás erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0


A **szolgáltatás** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton szolgáltatások kezelésére.

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
| Név| Azt jelzi, hogy a szolgáltatás nevét. Vegye figyelembe, hogy egyes esetekben ez eltér a megjelenített név. A szolgáltatások és a jelenlegi állapotában a Get-Service parancsmaggal kaphat.|
| BuiltInAccount| Azt jelzi, hogy a bejelentkezési fiókot szeretné használni a szolgáltatáshoz. Ez a tulajdonság számára engedélyezett az értékek a következők: **LocalService**, **LocalSystem**, és **NetworkService**.|
| hitelesítő adatok| Azt jelzi, hogy a szolgáltatás fog futni a fiók hitelesítő adatait. Ez a tulajdonság és a __BuiltinAccount__ tulajdonság nem használható együtt.|
| dependsOn| Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, az e tulajdonság használatával szintaxisa a következő `DependsOn = "[ResourceType]ResourceName"`.|
| StartupType| Azt jelzi, hogy a szolgáltatás indítási típusa. Ez a tulajdonság számára engedélyezett az értékek a következők: **automatikus**, **letiltott**, és **manuális**|
| Állapot| Szeretne biztosítani a szolgáltatás állapotát jelzi.|
| Leírás | Azt jelzi, hogy a célként megadott szolgáltatás leírását.|
| DisplayName | Azt jelzi, hogy a célként megadott szolgáltatás megjelenített neve.|
| Győződjön meg arról | Azt jelzi, hogy a célként megadott szolgáltatás létezik-e a rendszeren. Ez a tulajdonság beállítása **távol** annak érdekében, hogy a célként megadott szolgáltatás nem létezik. Értékre állítaná **jelen** (az alapértelmezett érték) biztosítja, hogy létezik-e a célként megadott szolgáltatás.|
| Elérési út | Azt jelzi, hogy egy új szolgáltatás a bináris fájl elérési útját.|

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