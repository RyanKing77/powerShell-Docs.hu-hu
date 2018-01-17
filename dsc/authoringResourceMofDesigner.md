---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "Az erőforrás-tervező eszközzel"
ms.openlocfilehash: c21602e219b5830877cc211e092e93bb7fc8ad9c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 01/17/2018
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="707b6-103">Az erőforrás-tervező eszközzel</span><span class="sxs-lookup"><span data-stu-id="707b6-103">Using the Resource Designer tool</span></span>

> <span data-ttu-id="707b6-104">Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="707b6-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="707b6-105">Az erőforrás-tervező eszköz egy olyan parancsmagok jelennek meg, ha a **xDscResourceDesigner** modul, amely létrehozása Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások megkönnyítése.</span><span class="sxs-lookup"><span data-stu-id="707b6-105">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="707b6-106">Az ehhez az erőforráshoz a parancsmagok segítségével, a MOF-séma, a parancsfájl modul és a könyvtárstruktúra, az új erőforrás létrehozása.</span><span class="sxs-lookup"><span data-stu-id="707b6-106">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="707b6-107">A DSC-erőforrásokra vonatkozó további információkért lásd: [Build egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások](authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="707b6-107">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span>
<span data-ttu-id="707b6-108">Ebben a témakörben létre fogunk hozni egy DSC erőforrást, amely felügyeli az Active Directory-felhasználók.</span><span class="sxs-lookup"><span data-stu-id="707b6-108">In this topic, we will create a DSC resource that manages Active Directory users.</span></span>
<span data-ttu-id="707b6-109">Használja a [Install-modul](https://technet.microsoft.com/en-us/library/dn807162.aspx) telepítésére szolgáló parancsmagot a **xDscResourceDesigner** modul.</span><span class="sxs-lookup"><span data-stu-id="707b6-109">Use the [Install-Module](https://technet.microsoft.com/en-us/library/dn807162.aspx) cmdlet to install the **xDscResourceDesigner** module.</span></span>

><span data-ttu-id="707b6-110">**Megjegyzés:**: **Install-modul** megtalálható a **PowerShellGet** modul, amely PowerShell 5.0 szerepel.</span><span class="sxs-lookup"><span data-stu-id="707b6-110">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="707b6-111">Letöltheti a **PowerShellGet** modul a PowerShell 3.0 és 4.0-s verzióját, [PackageManagement PowerShell modulok előzetes](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span><span class="sxs-lookup"><span data-stu-id="707b6-111">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="707b6-112">Erőforrás-tulajdonságok létrehozása</span><span class="sxs-lookup"><span data-stu-id="707b6-112">Creating resource properties</span></span>
<span data-ttu-id="707b6-113">Elsőként azt kell tennie az döntse el, amelyek megmutatják a erőforrás-tulajdonságok.</span><span class="sxs-lookup"><span data-stu-id="707b6-113">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="707b6-114">Például azt határozza meg az Active Directory-felhasználó a következő tulajdonságokkal.</span><span class="sxs-lookup"><span data-stu-id="707b6-114">For this example, we will define an Active Directory user with the following properties.</span></span>
 
<span data-ttu-id="707b6-115">A paraméternév leírása</span><span class="sxs-lookup"><span data-stu-id="707b6-115">Parameter name  Description</span></span>
* <span data-ttu-id="707b6-116">**Felhasználónév**: kulcs tulajdonságot, amely egyedileg azonosít egy felhasználót.</span><span class="sxs-lookup"><span data-stu-id="707b6-116">**UserName**: Key property that uniquely identifies a user.</span></span>
* <span data-ttu-id="707b6-117">**Győződjön meg arról**: meghatározza, hogy a felhasználói fióknak kell lennie a jelen van, vagy nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="707b6-117">**Ensure**: Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="707b6-118">Ez a paraméter csak két lehetséges értékekkel fognak rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="707b6-118">This parameter will have only two possible values.</span></span>
* <span data-ttu-id="707b6-119">**DomainCredential**: a felhasználó a tartomány jelszavát.</span><span class="sxs-lookup"><span data-stu-id="707b6-119">**DomainCredential**: The domain password for the user.</span></span>
* <span data-ttu-id="707b6-120">**Jelszó**: a felhasználó a felhasználói jelszó módosítására, ha szükséges a konfiguráció kívánt jelszavát.</span><span class="sxs-lookup"><span data-stu-id="707b6-120">**Password**: The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="707b6-121">A tulajdonságok létrehozásához használjuk a **New-xDscResourceProperty** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="707b6-121">To create the properties, we use the **New-xDscResourceProperty** cmdlet.</span></span> <span data-ttu-id="707b6-122">A következő PowerShell-parancsokat a fent leírt-tulajdonságok létrehozása.</span><span class="sxs-lookup"><span data-stu-id="707b6-122">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential-Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="707b6-123">Az erőforrás létrehozása</span><span class="sxs-lookup"><span data-stu-id="707b6-123">Create the resource</span></span>

<span data-ttu-id="707b6-124">Most, hogy az erőforrás-tulajdonságok létrehozása után is hívása a **New-xDscResource** parancsmaggal hozhat létre az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="707b6-124">Now that the resource properties have been created, we can call the **New-xDscResource** cmdlet to create the resource.</span></span> <span data-ttu-id="707b6-125">A **New-xDscResource** parancsmag fogad paraméterként tulajdonságok listája.</span><span class="sxs-lookup"><span data-stu-id="707b6-125">The **New-xDscResource** cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="707b6-126">Az elérési utat, ahol a modul létre kell hozni az új erőforrás nevét és a, amely tartalmazza azt a modul neve is szükséges.</span><span class="sxs-lookup"><span data-stu-id="707b6-126">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="707b6-127">A következő PowerShell-parancs létrehozza az erőforrás.</span><span class="sxs-lookup"><span data-stu-id="707b6-127">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

<span data-ttu-id="707b6-128">A **New-xDscResource** a parancsmag létrehozza a MOF-séma, egy üres erőforrást parancsprogram, a szükséges könyvtárstruktúrát az új erőforrás, a modul, amely elérhetővé teszi az új erőforrást a jegyzék.</span><span class="sxs-lookup"><span data-stu-id="707b6-128">The **New-xDscResource** cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="707b6-129">A MOF-fájl jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, és annak tartalmát a következők.</span><span class="sxs-lookup"><span data-stu-id="707b6-129">The MOF schema file is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, and its contents are as follows.</span></span>

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

<span data-ttu-id="707b6-130">Az erőforrást parancsprogram jelenleg **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span><span class="sxs-lookup"><span data-stu-id="707b6-130">The resource script is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span></span> <span data-ttu-id="707b6-131">Nem tartalmazza a tényleges logika valósítja meg az erőforrás, amelyek saját kezűleg kell hozzáadnia.</span><span class="sxs-lookup"><span data-stu-id="707b6-131">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="707b6-132">Az üres parancsfájl tartalmát a következők:</span><span class="sxs-lookup"><span data-stu-id="707b6-132">The contents of the skeleton script are as follows.</span></span>

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

## <a name="updating-the-resource"></a><span data-ttu-id="707b6-133">Az erőforrás frissítése</span><span class="sxs-lookup"><span data-stu-id="707b6-133">Updating the resource</span></span>

<span data-ttu-id="707b6-134">Ha felvenni vagy módosítani a paraméterlista az erőforrás van szüksége, hívása a **frissítés-xDscResource** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="707b6-134">If you need to add or modify the parameter list of the resource, you can call the **Update-xDscResource** cmdlet.</span></span> <span data-ttu-id="707b6-135">A parancsmag az erőforrás paraméter listájának frissítése.</span><span class="sxs-lookup"><span data-stu-id="707b6-135">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="707b6-136">Ha már hozzáadott logika erőforrás parancsfájlban, hogy érintetlen marad.</span><span class="sxs-lookup"><span data-stu-id="707b6-136">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="707b6-137">Tegyük fel, hogy szeretne az utolsó talál meg a felhasználót az erőforrás időben.</span><span class="sxs-lookup"><span data-stu-id="707b6-137">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="707b6-138">Ahelyett, hogy az erőforrás teljesen újra írásakor, az hívása a **New-xDscResourceProperty** hozzon létre az új tulajdonságot, és hívhatja **frissítés-xDscResource** , és adja hozzá az új tulajdonságot a tulajdonságok listája.</span><span class="sxs-lookup"><span data-stu-id="707b6-138">Rather than writing the resource again completely, you can call the **New-xDscResourceProperty** to create the new property, and then call **Update-xDscResource** and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="707b6-139">Egy erőforrás séma tesztelése</span><span class="sxs-lookup"><span data-stu-id="707b6-139">Testing a resource schema</span></span>

<span data-ttu-id="707b6-140">Az erőforrás-tervező eszköz közzétesz egy további parancsmag segítségével ellenőrizheti a MOF-séma manuálisan írt érvényességét.</span><span class="sxs-lookup"><span data-stu-id="707b6-140">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="707b6-141">Hívja a **teszt-xDscSchema** parancsmag paraméterként átadja a MOF erőforrás séma elérési útját.</span><span class="sxs-lookup"><span data-stu-id="707b6-141">Call the **Test-xDscSchema** cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="707b6-142">A parancsmag kimeneteként a séma-e hibák.</span><span class="sxs-lookup"><span data-stu-id="707b6-142">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="707b6-143">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="707b6-143">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="707b6-144">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="707b6-144">Concepts</span></span>
[<span data-ttu-id="707b6-145">Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="707b6-145">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="707b6-146">Egyéb források</span><span class="sxs-lookup"><span data-stu-id="707b6-146">Other Resources</span></span>
[<span data-ttu-id="707b6-147">xDscResourceDesigner Module</span><span class="sxs-lookup"><span data-stu-id="707b6-147">xDscResourceDesigner Module</span></span>](https://powershellgallery.com/packages/xDscResourceDesigner)