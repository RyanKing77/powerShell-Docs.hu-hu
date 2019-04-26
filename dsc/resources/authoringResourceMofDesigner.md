---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az erőforrás-tervező eszköz használata
ms.openlocfilehash: 3fd2f06cf46602ee30dd34f8e7bd77d3c92b808f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076667"
---
# <a name="using-the-resource-designer-tool"></a>Az erőforrás-tervező eszköz használata

> A következőkre vonatkozik: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Az erőforrás-tervező eszköz egy olyan parancsmagok által elérhetővé tett a **xDscResourceDesigner** modul, amely megkönnyíti a Windows PowerShell Desired State Configuration (DSC) erőforrások létrehozásához. Ennek az erőforrásnak a parancsmagok segítségével a MOF-sémát, a parancsfájl modul és a könyvtárstruktúra, az új erőforrás létrehozása. DSC-erőforrások kapcsolatos további információkért lásd: [hozhat létre egyéni Windows PowerShell Desired State Configuration erőforrások](authoringResource.md).
Ebben a témakörben létre fogunk hozni egy DSC-erőforrás, amely felügyeli az Active Directory-felhasználók.
Használja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xDscResourceDesigner** modul.

>**Megjegyzés:**: **Install-Module** szerepel a **PowerShellGet** modult, amely része a PowerShell 5.0-s. Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).

## <a name="creating-resource-properties"></a>Erőforrás-tulajdonságok létrehozása
A rendszer először azt kell tennünk döntse el, amelyek megmutatják az erőforrás-tulajdonságok. Ebben a példában meghatározunk egy Active Directory-felhasználó az alábbi tulajdonságokkal.

Paraméter neve, leírása
* **Felhasználónév**: Tulajdonság, amely egyedileg azonosít egy felhasználót.
* **Győződjön meg, hogy**: Megadja a felhasználói fióknak kell lennie a jelen van-e, vagy hiányzik. Ez a paraméter csak két lehetséges értékekkel fog rendelkezni.
* **DomainCredential**: A tartományi jelszó a felhasználónak.
* **Jelszó**: A kívánt jelszót a felhasználó számára lehetővé teszi a konfigurációt a szükség esetén módosítsa a felhasználó jelszavát.

Szeretne létrehozni a tulajdonságokat, használjuk a **New-xDscResourceProperty** parancsmagot. A következő PowerShell-parancsok a fentiekben leírt tulajdonságok létrehozása.

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a>Az erőforrás létrehozása

Most, hogy az erőforrás-tulajdonságok létrehozása meghívhatjuk a **New-xDscResource** parancsmagot az erőforrás létrehozásához. A **New-xDscResource** parancsmagnál tulajdonságok paraméterekként. Még tart az elérési utat, ahol a modul hozható létre, az új erőforrás neve és, amelyben szerepel a modul neve. A következő PowerShell-parancsot az erőforrást hoz létre.

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

A **New-xDscResource** parancsmag létrehozza a MOF-sémát, vázát erőforrás parancsfájl, a szükséges könyvtárstruktúrát az új erőforrás és a modul, amely elérhetővé teszi az új erőforrást a jegyzékfájl.

A MOF-fájl jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, és annak tartalmát az alábbiak szerint.

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

Az erőforrás-parancsfájl jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**. Nem tartalmazza a tényleges logika megvalósítása az erőforrás, amely saját magának kell hozzáadnia. A vázát parancsfájl tartalmát, az alábbiak szerint.

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

Ha felvenni vagy módosítani a paraméterlistában az erőforrás van szüksége, meghívhatja a **Update-xDscResource** parancsmag. A parancsmag frissíti az erőforrás egy új paraméterek listája. Ha már hozzáadott logikai erőforrás parancsfájlban, azt érintetlen.

Tegyük fel, hogy fel szeretne venni az utolsó napló az idő a felhasználó az erőforrásban. Ahelyett, hogy az erőforrás teljes egészében újra írása, meghívhatja a **New-xDscResourceProperty** hozzon létre az új tulajdonságot, és ezután hívja meg **Update-xDscResource** , és adja hozzá az új tulajdonságot a tulajdonságok listája.

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a>Egy erőforrás-séma tesztelése

Az erőforrás-tervező eszköz tesz közzé egy további parancsmag használható a MOF-sémát, amely kézzel írt érvényességének ellenőrzéséhez. Hívja a **Test-xDscSchema** elérési útját a MOF-erőforrás séma átadott paraméterként, a parancsmag. A parancsmag kimenete a séma az esetleges hibákat.

### <a name="see-also"></a>Lásd még:

#### <a name="concepts"></a>Fogalmak
[Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása](authoringResource.md)

#### <a name="other-resources"></a>Egyéb források
[xDscResourceDesigner Module](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)
