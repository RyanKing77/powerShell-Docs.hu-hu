---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Egypéldányos DSC-erőforrás írása (ajánlott eljárás)
ms.openlocfilehash: 9494964b1b13eaa082ad5cbc279b4586bb7211cc
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076565"
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a><span data-ttu-id="0a455-103">Egypéldányos DSC-erőforrás írása (ajánlott eljárás)</span><span class="sxs-lookup"><span data-stu-id="0a455-103">Writing a single-instance DSC resource (best practice)</span></span>

><span data-ttu-id="0a455-104">**Megjegyzés:** Ez a témakör ismerteti az ajánlott eljárás, amely lehetővé teszi, hogy csak egy példányban konfigurációban DSC erőforrás meghatározása.</span><span class="sxs-lookup"><span data-stu-id="0a455-104">**Note:** This topic describes a best practice for defining a DSC resource that allows only a single instance in a configuration.</span></span> <span data-ttu-id="0a455-105">Jelenleg nincs ehhez beépített DSC szolgáltatás.</span><span class="sxs-lookup"><span data-stu-id="0a455-105">Currently, there is no built-in DSC feature to do this.</span></span> <span data-ttu-id="0a455-106">Amely a későbbiekben változhatnak.</span><span class="sxs-lookup"><span data-stu-id="0a455-106">That might change in the future.</span></span>

<span data-ttu-id="0a455-107">Vannak helyzetek, ahol nem szeretné, hogy a többször használható konfigurációban egy erőforrást.</span><span class="sxs-lookup"><span data-stu-id="0a455-107">There are situations where you don't want to allow a resource to be used multiple times in a configuration.</span></span> <span data-ttu-id="0a455-108">Például az előző megvalósítását a [xTimeZone](https://github.com/PowerShell/xTimeZone) , egy konfigurációt sikerült erőforráshívásnak felelnek meg az erőforrás többször, különböző beállítását minden egyes erőforrás blokkban az időzóna beállítása:</span><span class="sxs-lookup"><span data-stu-id="0a455-108">For example, in a previous implementation of the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource, a configuration could call the resource multiple times, setting the time zone to a different setting in each resource block:</span></span>

```powershell
Configuration SetTimeZone
{
    Param
    (
        [String[]]$NodeName = $env:COMPUTERNAME

    )

    Import-DSCResource -ModuleName xTimeZone


    Node $NodeName
    {
         xTimeZone TimeZoneExample
         {

            TimeZone = 'Eastern Standard Time'
         }

         xTimeZone TimeZoneExample2
         {

            TimeZone = 'Pacific Standard Time'

         }

    }
}
```

<span data-ttu-id="0a455-109">Ez a DSC-erőforrás kulcsainak működik módja miatt.</span><span class="sxs-lookup"><span data-stu-id="0a455-109">This is because of the way DSC resource keys work.</span></span> <span data-ttu-id="0a455-110">Egy erőforrás rendelkeznie kell legalább egy tulajdonsággal.</span><span class="sxs-lookup"><span data-stu-id="0a455-110">A resource must have at least one key property.</span></span> <span data-ttu-id="0a455-111">Egy erőforrás-példány egyedi, ha az érték az összes kulcsfontosságú tulajdonságainak egyedi számít.</span><span class="sxs-lookup"><span data-stu-id="0a455-111">A resource instance is considered unique if the combination of the values of all of its key properties is unique.</span></span> <span data-ttu-id="0a455-112">Előző végrehajtása során a [xTimeZone](https://github.com/PowerShell/xTimeZone) erőforrás korábban csak az egyik tulajdonság--**időzóna**, amely szükséges kulcsként.</span><span class="sxs-lookup"><span data-stu-id="0a455-112">In its previous implementation, the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource had only one property--**TimeZone**, which was required to be a key.</span></span> <span data-ttu-id="0a455-113">Emiatt egy konfigurációjára, például a fenti lenne fordítása és futtatása figyelmeztetés nélkül.</span><span class="sxs-lookup"><span data-stu-id="0a455-113">Because of this, a configuration such as the one above would compile and run without warning.</span></span> <span data-ttu-id="0a455-114">Minden egyes a **xTimeZone** erőforrás blokkok egyedinek számít.</span><span class="sxs-lookup"><span data-stu-id="0a455-114">Each of the **xTimeZone** resource blocks is considered unique.</span></span> <span data-ttu-id="0a455-115">Emiatt a konfigurációt a csomópont, oda-vissza az időzóna recyklování többször is alkalmazható.</span><span class="sxs-lookup"><span data-stu-id="0a455-115">This would cause the configuration to be repeatedly applied to the node, cycling the timezone back and forth.</span></span>

<span data-ttu-id="0a455-116">Annak érdekében, hogy csak egyszer, az erőforrás egy második tulajdonság hozzáadása megtörtént egy konfigurációt sikerült beállítani egy célcsomóponttal időzónáját **IsSingleInstance**, hogy a kulcstulajdonság vált.</span><span class="sxs-lookup"><span data-stu-id="0a455-116">To ensure that a configuration could set the time zone for a target node only once, the resource was updated to add a second property, **IsSingleInstance**, that became the key property.</span></span>
<span data-ttu-id="0a455-117">A **IsSingleInstance** korlátozódott, egyetlen érték "Yes" használatával egy **ValueMap**.</span><span class="sxs-lookup"><span data-stu-id="0a455-117">The **IsSingleInstance** was limited to a single value, "Yes" by using a **ValueMap**.</span></span> <span data-ttu-id="0a455-118">Az erőforrás a régi MOF-séma a következő:</span><span class="sxs-lookup"><span data-stu-id="0a455-118">The old MOF schema for the resource was:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="0a455-119">Az erőforrás a frissített MOF-séma a következő:</span><span class="sxs-lookup"><span data-stu-id="0a455-119">The updated MOF schema for the resource is:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="0a455-120">Az erőforrás-parancsfájl használata az új paramétert is frissítve lett.</span><span class="sxs-lookup"><span data-stu-id="0a455-120">The resource script was also updated to use the new parameter.</span></span> <span data-ttu-id="0a455-121">Itt látható a régi erőforrás parancsfájlt:</span><span class="sxs-lookup"><span data-stu-id="0a455-121">Here is the old resource script:</span></span>

```powershell
function Get-TargetResource
{
    [CmdletBinding()]
    [OutputType([Hashtable])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Get the current TimeZone
    $CurrentTimeZone = Get-TimeZone

    $returnValue = @{
        TimeZone = $CurrentTimeZone
        IsSingleInstance = 'Yes'
    }

    #Output the target resource
    $returnValue
}


function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output the result of Get-TargetResource function.
    $CurrentTimeZone = Get-TimeZone

    if($PSCmdlet.ShouldProcess("'$TimeZone'","Replace the System Time Zone"))
    {
        try
        {
            if($CurrentTimeZone -ne $TimeZone)
            {
                Write-Verbose -Verbose "Setting the TimeZone"
                Set-TimeZone -TimeZone $TimeZone}
            else
            {
                Write-Verbose -Verbose "TimeZone already set to $TimeZone"
            }
        }
        catch
        {
            $ErrorMsg = $_.Exception.Message
            Write-Verbose -Verbose $ErrorMsg
        }
    }
}


function Test-TargetResource
{
    [CmdletBinding()]
    [OutputType([Boolean])]
    param
    (
        [parameter(Mandatory = $true)]
        [ValidateSet('Yes')]
        [String]
        $IsSingleInstance,

        [parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $TimeZone
    )

    #Output from Get-TargetResource
    $CurrentTimeZone = Get-TimeZone

    if($TimeZone -eq $CurrentTimeZone)
    {
        return $true
    }
    else
    {
        return $false
    }
}

Function Get-TimeZone {
    [CmdletBinding()]
    param()

    & tzutil.exe /g
}

Function Set-TimeZone {
    [CmdletBinding()]
    param(
        [Parameter(Mandatory=$true)]
        [System.String]
        $TimeZone
    )

    try
    {
        & tzutil.exe /s $TimeZone
    }
    catch
    {
        $ErrorMsg = $_.Exception.Message
        Write-Verbose $ErrorMsg
    }
}

Export-ModuleMember -Function *-TargetResource
```

<span data-ttu-id="0a455-122">Figyelje meg, hogy a **időzóna** tulajdonság már nem egy kulcsot.</span><span class="sxs-lookup"><span data-stu-id="0a455-122">Notice that the **TimeZone** property is no longer a key.</span></span> <span data-ttu-id="0a455-123">Most, ha egy konfigurációs próbál meg kétszer az időzóna beállítása (a két különböző **xTimeZone** az eltérő blokkokat **időzóna** értékek), konfiguráció fordítása kísérlet hiba miatt:</span><span class="sxs-lookup"><span data-stu-id="0a455-123">Now, if a configuration attempts to set the time zone twice (by using two different **xTimeZone** blocks with different **TimeZone** values), attempting to compile the configuration will cause an error:</span></span>

```powershell
Test-ConflictingResources : A conflict was detected between resources '[xTimeZone]TimeZoneExample (::15::10::xTimeZone)' and
'[xTimeZone]TimeZoneExample2 (::22::10::xTimeZone)' in node 'CONTOSO-CLIENT'. Resources have identical key properties but there are differences in the
following non-key properties: 'TimeZone'. Values 'Eastern Standard Time' don't match values 'Pacific Standard Time'. Please update these property
values so that they are identical in both cases.
At line:271 char:9
+         Test-ConflictingResources $keywordName $canonicalizedValue $k ...
+         ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : ConflictingDuplicateResource,Test-ConflictingResources
Errors occurred while processing configuration 'SetTimeZone'.
At C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\PSDesiredStateConfiguration\PSDesiredStateConfiguration.psm1:3705 char:5
+     throw $ErrorRecord
+     ~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (SetTimeZone:String) [], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessConfiguration
```