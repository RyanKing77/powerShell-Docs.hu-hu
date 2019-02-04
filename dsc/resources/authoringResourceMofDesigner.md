---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Az erőforrás-tervező eszköz használata
ms.openlocfilehash: 3fd2f06cf46602ee30dd34f8e7bd77d3c92b808f
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686655"
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="f3b32-103">Az erőforrás-tervező eszköz használata</span><span class="sxs-lookup"><span data-stu-id="f3b32-103">Using the Resource Designer tool</span></span>

> <span data-ttu-id="f3b32-104">Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="f3b32-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="f3b32-105">Az erőforrás-tervező eszköz egy olyan parancsmagok által elérhetővé tett a **xDscResourceDesigner** modul, amely megkönnyíti a Windows PowerShell Desired State Configuration (DSC) erőforrások létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="f3b32-105">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="f3b32-106">Ennek az erőforrásnak a parancsmagok segítségével a MOF-sémát, a parancsfájl modul és a könyvtárstruktúra, az új erőforrás létrehozása.</span><span class="sxs-lookup"><span data-stu-id="f3b32-106">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="f3b32-107">DSC-erőforrások kapcsolatos további információkért lásd: [hozhat létre egyéni Windows PowerShell Desired State Configuration erőforrások](authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="f3b32-107">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span>
<span data-ttu-id="f3b32-108">Ebben a témakörben létre fogunk hozni egy DSC-erőforrás, amely felügyeli az Active Directory-felhasználók.</span><span class="sxs-lookup"><span data-stu-id="f3b32-108">In this topic, we will create a DSC resource that manages Active Directory users.</span></span>
<span data-ttu-id="f3b32-109">Használja a [Install-Module](/powershell/module/PowershellGet/Install-Module) telepítésére szolgáló parancsmagot a **xDscResourceDesigner** modul.</span><span class="sxs-lookup"><span data-stu-id="f3b32-109">Use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xDscResourceDesigner** module.</span></span>

><span data-ttu-id="f3b32-110">**Megjegyzés:**: **Install-Module** szerepel a **PowerShellGet** modult, amely része a PowerShell 5.0-s.</span><span class="sxs-lookup"><span data-stu-id="f3b32-110">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="f3b32-111">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modul előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="f3b32-111">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="f3b32-112">Erőforrás-tulajdonságok létrehozása</span><span class="sxs-lookup"><span data-stu-id="f3b32-112">Creating resource properties</span></span>
<span data-ttu-id="f3b32-113">A rendszer először azt kell tennünk döntse el, amelyek megmutatják az erőforrás-tulajdonságok.</span><span class="sxs-lookup"><span data-stu-id="f3b32-113">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="f3b32-114">Ebben a példában meghatározunk egy Active Directory-felhasználó az alábbi tulajdonságokkal.</span><span class="sxs-lookup"><span data-stu-id="f3b32-114">For this example, we will define an Active Directory user with the following properties.</span></span>

<span data-ttu-id="f3b32-115">Paraméter neve, leírása</span><span class="sxs-lookup"><span data-stu-id="f3b32-115">Parameter name  Description</span></span>
* <span data-ttu-id="f3b32-116">**Felhasználónév**: Tulajdonság, amely egyedileg azonosít egy felhasználót.</span><span class="sxs-lookup"><span data-stu-id="f3b32-116">**UserName**: Key property that uniquely identifies a user.</span></span>
* <span data-ttu-id="f3b32-117">**Győződjön meg, hogy**: Megadja a felhasználói fióknak kell lennie a jelen van-e, vagy hiányzik.</span><span class="sxs-lookup"><span data-stu-id="f3b32-117">**Ensure**: Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="f3b32-118">Ez a paraméter csak két lehetséges értékekkel fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="f3b32-118">This parameter will have only two possible values.</span></span>
* <span data-ttu-id="f3b32-119">**DomainCredential**: A tartományi jelszó a felhasználónak.</span><span class="sxs-lookup"><span data-stu-id="f3b32-119">**DomainCredential**: The domain password for the user.</span></span>
* <span data-ttu-id="f3b32-120">**Jelszó**: A kívánt jelszót a felhasználó számára lehetővé teszi a konfigurációt a szükség esetén módosítsa a felhasználó jelszavát.</span><span class="sxs-lookup"><span data-stu-id="f3b32-120">**Password**: The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="f3b32-121">Szeretne létrehozni a tulajdonságokat, használjuk a **New-xDscResourceProperty** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="f3b32-121">To create the properties, we use the **New-xDscResourceProperty** cmdlet.</span></span> <span data-ttu-id="f3b32-122">A következő PowerShell-parancsok a fentiekben leírt tulajdonságok létrehozása.</span><span class="sxs-lookup"><span data-stu-id="f3b32-122">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="f3b32-123">Az erőforrás létrehozása</span><span class="sxs-lookup"><span data-stu-id="f3b32-123">Create the resource</span></span>

<span data-ttu-id="f3b32-124">Most, hogy az erőforrás-tulajdonságok létrehozása meghívhatjuk a **New-xDscResource** parancsmagot az erőforrás létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="f3b32-124">Now that the resource properties have been created, we can call the **New-xDscResource** cmdlet to create the resource.</span></span> <span data-ttu-id="f3b32-125">A **New-xDscResource** parancsmagnál tulajdonságok paraméterekként.</span><span class="sxs-lookup"><span data-stu-id="f3b32-125">The **New-xDscResource** cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="f3b32-126">Még tart az elérési utat, ahol a modul hozható létre, az új erőforrás neve és, amelyben szerepel a modul neve.</span><span class="sxs-lookup"><span data-stu-id="f3b32-126">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="f3b32-127">A következő PowerShell-parancsot az erőforrást hoz létre.</span><span class="sxs-lookup"><span data-stu-id="f3b32-127">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

<span data-ttu-id="f3b32-128">A **New-xDscResource** parancsmag létrehozza a MOF-sémát, vázát erőforrás parancsfájl, a szükséges könyvtárstruktúrát az új erőforrás és a modul, amely elérhetővé teszi az új erőforrást a jegyzékfájl.</span><span class="sxs-lookup"><span data-stu-id="f3b32-128">The **New-xDscResource** cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="f3b32-129">A MOF-fájl jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, és annak tartalmát az alábbiak szerint.</span><span class="sxs-lookup"><span data-stu-id="f3b32-129">The MOF schema file is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, and its contents are as follows.</span></span>

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

<span data-ttu-id="f3b32-130">Az erőforrás-parancsfájl jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span><span class="sxs-lookup"><span data-stu-id="f3b32-130">The resource script is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span></span> <span data-ttu-id="f3b32-131">Nem tartalmazza a tényleges logika megvalósítása az erőforrás, amely saját magának kell hozzáadnia.</span><span class="sxs-lookup"><span data-stu-id="f3b32-131">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="f3b32-132">A vázát parancsfájl tartalmát, az alábbiak szerint.</span><span class="sxs-lookup"><span data-stu-id="f3b32-132">The contents of the skeleton script are as follows.</span></span>

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

## <a name="updating-the-resource"></a><span data-ttu-id="f3b32-133">Az erőforrás frissítése</span><span class="sxs-lookup"><span data-stu-id="f3b32-133">Updating the resource</span></span>

<span data-ttu-id="f3b32-134">Ha felvenni vagy módosítani a paraméterlistában az erőforrás van szüksége, meghívhatja a **Update-xDscResource** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="f3b32-134">If you need to add or modify the parameter list of the resource, you can call the **Update-xDscResource** cmdlet.</span></span> <span data-ttu-id="f3b32-135">A parancsmag frissíti az erőforrás egy új paraméterek listája.</span><span class="sxs-lookup"><span data-stu-id="f3b32-135">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="f3b32-136">Ha már hozzáadott logikai erőforrás parancsfájlban, azt érintetlen.</span><span class="sxs-lookup"><span data-stu-id="f3b32-136">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="f3b32-137">Tegyük fel, hogy fel szeretne venni az utolsó napló az idő a felhasználó az erőforrásban.</span><span class="sxs-lookup"><span data-stu-id="f3b32-137">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="f3b32-138">Ahelyett, hogy az erőforrás teljes egészében újra írása, meghívhatja a **New-xDscResourceProperty** hozzon létre az új tulajdonságot, és ezután hívja meg **Update-xDscResource** , és adja hozzá az új tulajdonságot a tulajdonságok listája.</span><span class="sxs-lookup"><span data-stu-id="f3b32-138">Rather than writing the resource again completely, you can call the **New-xDscResourceProperty** to create the new property, and then call **Update-xDscResource** and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="f3b32-139">Egy erőforrás-séma tesztelése</span><span class="sxs-lookup"><span data-stu-id="f3b32-139">Testing a resource schema</span></span>

<span data-ttu-id="f3b32-140">Az erőforrás-tervező eszköz tesz közzé egy további parancsmag használható a MOF-sémát, amely kézzel írt érvényességének ellenőrzéséhez.</span><span class="sxs-lookup"><span data-stu-id="f3b32-140">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="f3b32-141">Hívja a **Test-xDscSchema** elérési útját a MOF-erőforrás séma átadott paraméterként, a parancsmag.</span><span class="sxs-lookup"><span data-stu-id="f3b32-141">Call the **Test-xDscSchema** cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="f3b32-142">A parancsmag kimenete a séma az esetleges hibákat.</span><span class="sxs-lookup"><span data-stu-id="f3b32-142">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="f3b32-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f3b32-143">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="f3b32-144">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="f3b32-144">Concepts</span></span>
[<span data-ttu-id="f3b32-145">Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="f3b32-145">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="f3b32-146">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="f3b32-146">Other Resources</span></span>
[<span data-ttu-id="f3b32-147">xDscResourceDesigner Module</span><span class="sxs-lookup"><span data-stu-id="f3b32-147">xDscResourceDesigner Module</span></span>](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)
