---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
description: "Lehetővé teszi a célcsomóponton helyi csoportok kezelése."
title: "A DSC GroupSet erőforrás"
ms.openlocfilehash: 0907a968bfc660adc873c28e8be6572d1d5cb993
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-groupset-resource"></a>A DSC GroupSet erőforrás

> Vonatkozik: Windows Windows PowerShell 5.0

A **GroupSet** erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése. Az erőforrás egy [összetett erőforrás](authoringResourceComposite.md) , amely meghívja a [erőforrás csoport](groupResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.

Adja hozzá és/vagy távolítsa el a egynél több csoport tagjai ugyanazt a listát, egynél több csoport eltávolítása vagy vegyen fel egy tagok ugyanazt a listát egynél több csoportot használni ehhez az erőforráshoz.

##<a name="syntax"></a>Szintaxis ##
```
Group [string] #ResourceName
{
    GroupName = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   | 
|---|---| 
| Csoportnév| A csoportokat, amelyekhez egy adott állapot biztosításához nevei.| 
| MembersToExclude| Ez a tulajdonság segítségével távolítsa el a meglévő a csoportok tagságának tagot. Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*. Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság. Ennek során hibát adnak.| 
| hitelesítő adatok| A távoli erőforrások eléréséhez szükséges hitelesítő adatokat. **Megjegyzés:**: ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; ellenkező esetben hiba történik.
| Győződjön meg arról| Azt jelzi, hogy a csoportok is léteznek. Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a csoportok nem léteznek. Azt, hogy "" (az alapértelmezett érték) beállítást biztosítja, hogy a csoportok is léteznek.| 
| Tagok| Ez a tulajdonság használatával az aktuális csoporttagság cserélje le a megadott tagot. Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*. Ha ez a tulajdonság konfigurációban, nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság. Ennek során hibát adnak.| 
| MembersToInclude| Ez a tulajdonság használatával tagok hozzáadása a meglévő csoport tagságát. Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*. Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság. Ennek során hibát adnak.| 
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".| 

## <a name="example-1"></a>1. példa

A következő példa bemutatja, hogyan annak érdekében, hogy jelen-e "myGroup" és "myOtherGroup" két csoportot. 

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}


GroupSetTest -ConfigurationData $cd
```

>**Megjegyzés:** ebben a példában egyszerű szöveges hitelesítő adatokat használja az egyszerűség érdekében. A konfigurációs MOF-fájlt a hitelesítő adatok titkosításához kapcsolatos információkért lásd: [biztonságossá tétele a MOF-fájlt](secureMOF.md).


