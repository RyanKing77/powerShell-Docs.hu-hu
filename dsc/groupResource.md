---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A DSC-csoport erőforrás"
ms.openlocfilehash: 8a2087455a72ec1f368f890b62228b31cf4ec95a
ms.sourcegitcommit: c72c76f6ed77b3e6f26fef3e8784b157bfc19355
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/06/2018
---
# <a name="dsc-group-resource"></a>A DSC-csoport erőforrás

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

A csoport erőforrás a Windows PowerShell szükséges konfiguráló (DSC) lehetővé teszi a célcsomóponton helyi csoportok kezelése.

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
| Csoportnév| A csoport, amelyekhez egy adott állapot biztosításához neve.|
| hitelesítő adatok| A távoli erőforrások eléréséhez szükséges hitelesítő adatokat. **Megjegyzés:**: ennek a fióknak rendelkeznie kell a megfelelő Active Directory-engedélyek minden nem helyi fiók hozzáadása a csoporthoz,, hiba történik a konfiguráció célcsomóponton való végrehajtásakor.
| Leírás| A csoport leírását.|
| Győződjön meg arról| Azt jelzi, hogy a csoport létezik-e. Állítsa be ezt a tulajdonságot "Hiányzik", annak érdekében, hogy a csoport nem létezik. Azt, hogy "" (az alapértelmezett érték) beállítást biztosítja, hogy a csoport létezik.|
| Tagok| Ez a tulajdonság használatával az aktuális csoporttagság cserélje le a megadott tagot. Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*. Ha ez a tulajdonság konfigurációban, nem használja a **MembersToExclude** vagy **MembersToInclude** tulajdonság. Ennek során hibát generál.|
| MembersToExclude| Ez a tulajdonság használatával az eddigi tagságot a csoport tagjainak eltávolítását. Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*. Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság. Ennek során hibát generál.|
| MembersToInclude| Ez a tulajdonság használatával tagok hozzáadása a meglévő csoport tagságát. Ez a tulajdonság értéke a következő formában karakterláncok *tartomány*\\*felhasználónév*. Ha ez a tulajdonság konfigurációban, ne használja a **tagok** tulajdonság. Ennek során hibát adnak.|
| dependsOn | Azt jelzi, hogy egy másik erőforrás konfigurációjának kell futtatni, mielőtt ehhez az erőforráshoz van konfigurálva. Például, ha az erőforrás-konfiguráció azonosítója blokk futtatni kívánt parancsfájl első az __ResourceName__ és annak típusa __ResourceType__, szintaxisa a következő e tulajdonság használatával "DependsOn ="[ A ResourceType] ResourceName"".|

## <a name="example-1"></a>1. példa

A következő példa bemutatja, hogyan annak érdekében, hogy hiányzik-e a "TestGroup" nevű csoport.

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

A következő példa bemutatja, hogyan egy Active Directory-felhasználó hozzáadása a helyi rendszergazdák csoportjának, ha már használja egy PSCredential a helyi Adminsztrátori fiók Többszámítógépes labor build részeként.
Mivel ez után is használja a tartományi rendszergazda fiók (előléptetését), majd a meglévő PSCredential átalakítása rövid tartományi hitelesítő adatokat kell.
Ezután azt adhat hozzá egy tartományi felhasználót a helyi Rendszergazdák csoport azon a tagkiszolgálón.

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

A következő példa bemutatja, hogyan egy helyi csoport, TigerTeamAdmins biztosításához, a kiszolgálón az TigerTeamSource.Contoso.Com nem tartalmaz egy adott tartományi fiókot, Contoso\JerryG.

```powershell
Configuration SecureTigerTeamSrouce {
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
