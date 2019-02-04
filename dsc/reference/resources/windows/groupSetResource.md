---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
description: Lehetővé teszi a célcsomóponton helyi csoportok kezelése.
title: DSC GroupSet erőforrás
ms.openlocfilehash: afe4c4d33ac5620c411481e93d76a1f90c26deb9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684926"
---
# <a name="dsc-groupset-resource"></a>DSC GroupSet erőforrás

> Érvényes: Windows PowerShell 5.0

A **GroupSet** erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése. Ez az erőforrás egy [összetett erőforrás](../../../resources/authoringResourceComposite.md) , amely meghívja a [erőforrás csoport](groupResource.md) minden egyes megadott csoport számára a `GroupName` paraméter.

Akkor használja ezt az erőforrást, ha hozzáadása és/vagy távolítsa el a több csoport tagjai ugyanazt a listát, egynél több csoport eltávolítása, vagy adja hozzá ugyanazt a listát egynél több csoport tagjai.

## <a name="syntax"></a>Szintaxis

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
| Csoportnév| A csoportok, amelyhez szeretne biztosítani adott állapotú nevei.|
| MembersToExclude| Ez a tulajdonság használatával a meglévő tagság a csoportok tagjainak eltávolítását. Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*. Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság. Így generál hibát.|
| Hitelesítő adatok| A távoli erőforrások eléréséhez szükséges hitelesítő adatokat. **Megjegyzés:**: Ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; Ellenkező esetben a rendszer hibát fog jelezni.
| Győződjön meg, hogy| Azt jelzi, hogy a csoport létezik. Állítsa be ezt a tulajdonságot a "Hiányzó", győződjön meg arról, hogy a csoportok nem létezik. Azt, hogy "" (az alapértelmezett érték) beállítás biztosítja, hogy létezik-e a csoportok.|
| Tagok| Ez a tulajdonság használatával az aktuális csoport tagságának cserélje le a meghatározott tagokat. Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*. Ezzel a tulajdonsággal konfigurációban, ha nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság. Így generál hibát.|
| MembersToInclude| Ez a tulajdonság használatával tagok hozzáadása a meglévő tagság a csoport. Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*. Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság. Így generál hibát.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az __ResourceName__ és a típusa __ResourceType__, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".|

## <a name="example-1-ensuring-groups-are-present"></a>1. példa: Biztosítása csoportok találhatók.

Az alábbi példa bemutatja, hogyan győződjön meg arról, hogy telepítve-e két "myGroup" és "myOtherGroup" csoportot.

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

> [!NOTE]
> Ebben a példában az egyszerűség kedvéért egy egyszerű szöveges hitelesítő adatokat használ. A konfigurációs MOF-fájlban található hitelesítő adatainak titkosítása kapcsolatos információkért lásd: [a MOF-fájl biztonságossá tétele](../../../pull-server/secureMOF.md).
