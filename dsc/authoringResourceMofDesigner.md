---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Az erőforrás-tervező eszközzel"
ms.openlocfilehash: 5a034547d0850682513e9a80367ce148bfcf0bdc
ms.sourcegitcommit: a775e4788616490980123e8e6ea78594ffeb6f7d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/29/2017
---
# <a name="using-the-resource-designer-tool"></a>Az erőforrás-tervező eszközzel

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Az erőforrás-tervező eszköz egy olyan parancsmagok jelennek meg, ha a **xDscResourceDesigner** modul, amely létrehozása Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások megkönnyítése. Az ehhez az erőforráshoz a parancsmagok segítségével, a MOF-séma, a parancsfájl modul és a könyvtárstruktúra, az új erőforrás létrehozása. A DSC-erőforrásokra vonatkozó további információkért lásd: [Build egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások](authoringResource.md).
Ebben a témakörben létre fogunk hozni egy DSC erőforrást, amely felügyeli az Active Directory-felhasználók.
Használja a [Install-modul](https://technet.microsoft.com/en-us/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xDscResourceDesigner** modul.

>**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).

## <a name="creating-resource-properties"></a>Erőforrás-tulajdonságok létrehozása
Elsőként azt kell tennie az döntse el, amelyek megmutatják a erőforrás-tulajdonságok. Például azt határozza meg az Active Directory-felhasználó a következő tulajdonságokkal.
 
A paraméternév leírása
* **Felhasználónév**: kulcs tulajdonságot, amely egyedileg azonosít egy felhasználót.
* **Győződjön meg arról**: meghatározza, hogy a felhasználói fióknak kell lennie a jelen van, vagy nincs megadva. Ez a paraméter csak két lehetséges értékekkel fognak rendelkezni.
* **DomainCredential**: a felhasználó a tartomány jelszavát.
* **Jelszó**: a felhasználó a felhasználói jelszó módosítására, ha szükséges a konfiguráció kívánt jelszavát.

A tulajdonságok létrehozásához használjuk a **New-xDscResourceProperty** parancsmag. A következő PowerShell-parancsokat a fent leírt-tulajdonságok létrehozása.

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential-Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a>Az erőforrás létrehozása

Most, hogy az erőforrás-tulajdonságok létrehozása után is hívása a **New-xDscResource** parancsmaggal hozhat létre az erőforrás. A **New-xDscResource** parancsmag fogad paraméterként tulajdonságok listája. Az elérési utat, ahol a modul létre kell hozni az új erőforrás nevét és a, amely tartalmazza azt a modul neve is szükséges. A következő PowerShell-parancs létrehozza az erőforrás.

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

A **New-xDscResource** a parancsmag létrehozza a MOF-séma, egy üres erőforrást parancsprogram, a szükséges könyvtárstruktúrát az új erőforrás, a modul, amely elérhetővé teszi az új erőforrást a jegyzék.

A MOF-fájl jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, és annak tartalmát a következők.

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
  [Key] string UserName;
  [Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
  [Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
  [Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

Az erőforrást parancsprogram jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**. Nem tartalmazza a tényleges logika valósítja meg az erőforrás, amelyek saját kezűleg kell hozzáadnia. Az üres parancsfájl tartalmát a következők:

```powershell
function Get-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Collections.Hashtable])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $returnValue = @{
  UserName = [System.String]
  Ensure = [System.String]
  DomainAdminCredential = [System.Management.Automation.PSCredential]
  Password = [System.Management.Automation.PSCredential]
  }

  $returnValue
  #>
}


function Set-TargetResource
{
  [CmdletBinding()]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  #Include this line if the resource requires a system reboot.
  #$global:DSCMachineStatus = 1


}


function Test-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Boolean])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $result = [System.Boolean]

  $result
  #>
}


Export-ModuleMember -Function *-TargetResource
```

## <a name="updating-the-resource"></a>Az erőforrás frissítése

Ha felvenni vagy módosítani a paraméterlista az erőforrás van szüksége, hívása a **frissítés-xDscResource** parancsmag. A parancsmag az erőforrás paraméter listájának frissítése. Ha már hozzáadott logika erőforrás parancsfájlban, hogy érintetlen marad.

Tegyük fel, hogy szeretne az utolsó talál meg a felhasználót az erőforrás időben. Ahelyett, hogy az erőforrás teljesen újra írásakor, az hívása a **New-xDscResourceProperty** hozzon létre az új tulajdonságot, és hívhatja **frissítés-xDscResource** , és adja hozzá az új tulajdonságot a tulajdonságok listája.

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a>Egy erőforrás séma tesztelése

Az erőforrás-tervező eszköz közzétesz egy további parancsmag segítségével ellenőrizheti a MOF-séma manuálisan írt érvényességét. Hívja a **teszt-xDscSchema** parancsmag paraméterként átadja a MOF erőforrás séma elérési útját. A parancsmag kimeneteként a séma-e hibák.

### <a name="see-also"></a>Lásd még:

#### <a name="concepts"></a>Fogalmak
[Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása](authoringResource.md)

#### <a name="other-resources"></a>Egyéb források
[xDscResourceDesigner modul](https://powershellgallery.com/packages/xDscResourceDesigner)