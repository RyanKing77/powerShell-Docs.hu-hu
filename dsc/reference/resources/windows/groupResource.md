---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-Group erőforrás
ms.openlocfilehash: 123e09b54a923af942a15f80fa7291c555b4235f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62077347"
---
# <a name="dsc-group-resource"></a>DSC-Group erőforrás

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

A csoport erőforrás a Windows PowerShell Desired State Configuration (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.

## <a name="syntax"></a>Szintaxis

```
Group [string] #ResourceName
{
    GroupName          = [string]
    [ Credential       = [PSCredential] ]
    [ Description      = [string[]] ]
    [ Ensure           = [string] { Absent | Present }  ]
    [ Members          = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn        = [string[]] ]
}
```

## <a name="properties"></a>Tulajdonságok

|  Tulajdonság  |  Leírás   |
|---|---|
| Csoportnév| A csoport, amelyhez szeretne biztosítani egy adott állapot neve.|
| Hitelesítő adatok| A távoli erőforrások eléréséhez szükséges hitelesítő adatokat. **Megjegyzés:**: Ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz; Ellenkező esetben hiba lép fel, a konfiguráció célcsomóponton való végrehajtásakor.
| Leírás| A csoport leírása.|
| Győződjön meg, hogy| Azt jelzi, hogy létezik-e a csoportnak. Állítsa be ezt a tulajdonságot a "Hiányzó" annak érdekében, hogy a csoport nem létezik. Beállítása a "Nyújtjuk" (az alapértelmezett érték) biztosítja, hogy a csoport létezik.|
| Tagok| Ez a tulajdonság használatával az aktuális csoport tagságának cserélje le a meghatározott tagokat. Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*. Ezzel a tulajdonsággal konfigurációban, ha nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság. Ezzel létrejön egy hiba.|
| MembersToExclude| Ez a tulajdonság használatával a meglévő tagság a csoport tagjainak eltávolítását. Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*. Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság. Ezzel létrejön egy hiba.|
| MembersToInclude| Ez a tulajdonság használatával tagok hozzáadása a meglévő tagság a csoport. Ez a tulajdonság értéke az űrlap karakterláncok tömbje *tartomány*\\*felhasználónév*. Ha ezzel a tulajdonsággal konfigurációban, ne használja a **tagok** tulajdonság. Így generál hibát.|
| DependsOn | Azt jelzi, hogy a konfigurációt egy másik erőforrás futtatnia kell, mielőtt az erőforrás konfigurálva van. Például, ha az erőforrás-konfiguráció azonosítója parancsfájl-blokk futtatni kívánt első az __ResourceName__ és a típusa __ResourceType__, esetén ez a tulajdonság használatával "DependsOn"[a = Erőforrástípus] ResourceName"s".|

## <a name="example-1"></a>1. példa

Az alábbi példa bemutatja, hogyan annak érdekében, hogy hiányzik egy "TestGroup" nevű csoportot.

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```

## <a name="example-2"></a>2. példa

Az alábbi példa bemutatja, hogyan egy Active Directory-felhasználó hozzáadása a helyi Rendszergazdák csoport már használata pscredential adattá a helyi rendszergazdai fiók több gép labor build részeként.
Mivel ez után is használja a tartományi rendszergazdai fiók (előléptetését), majd egy rövid tartományi hitelesítő adatok a meglévő PSCredential konvertálni kell.
Ezután azt is hozzáadhat egy tartományi felhasználót a helyi Rendszergazdák csoport azon a tagkiszolgálón.

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
        @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'
        }
    )
}

$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup {
    GroupName='Administrators'
    Ensure= 'Present'
    MembersToInclude= "$domain\$($Node.AdminAccount)"
    Credential = $dCredential
    PsDscRunAsCredential = $DCredential
}
```

## <a name="example-3"></a>3. példa

Az alábbi példa bemutatja, hogyan kell egy helyi csoport TigerTeamAdmins biztosítása, a kiszolgálón az TigerTeamSource.Contoso.Com nem tartalmaz egy adott tartományi fiókot, Contoso\JerryG.

```powershell
Configuration SecureTigerTeamSource {
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

  Node TigerTeamSource.Contoso.Com {
    Group TigerTeamAdmins {
       GroupName        = 'TigerTeamAdmins'
       Ensure           = 'Present'
       MembersToExclude = "Contoso\JerryG"
    }
  }
}
```