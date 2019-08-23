---
ms.date: 06/12/2017
keywords: DSC, PowerShell, konfigurálás, beállítás
title: Egypéldányos DSC-erőforrás írása (ajánlott eljárás)
ms.openlocfilehash: 4d9e07c6aaa064f808a03d4252e8d352b82183ec
ms.sourcegitcommit: 5a004064f33acc0145ccd414535763e95f998c89
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/23/2019
ms.locfileid: "69986520"
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a><span data-ttu-id="5e3f8-103">Egypéldányos DSC-erőforrás írása (ajánlott eljárás)</span><span class="sxs-lookup"><span data-stu-id="5e3f8-103">Writing a single-instance DSC resource (best practice)</span></span>

><span data-ttu-id="5e3f8-104">**Megjegyzés:** Ez a témakör egy olyan DSC-erőforrás definiálásának ajánlott eljárását ismerteti, amely csak egyetlen példányt engedélyez a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-104">**Note:** This topic describes a best practice for defining a DSC resource that allows only a single instance in a configuration.</span></span> <span data-ttu-id="5e3f8-105">Jelenleg nincs ilyen beépített DSC-funkció.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-105">Currently, there is no built-in DSC feature to do this.</span></span> <span data-ttu-id="5e3f8-106">A későbbiekben változhatnak.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-106">That might change in the future.</span></span>

<span data-ttu-id="5e3f8-107">Vannak olyan helyzetek, amikor nem szeretné, hogy egy erőforrás többször is felhasználható legyen a konfigurációban.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-107">There are situations where you don't want to allow a resource to be used multiple times in a configuration.</span></span> <span data-ttu-id="5e3f8-108">Például a [xTimeZone](https://github.com/PowerShell/xTimeZone) erőforrás egy korábbi implementációjában a konfiguráció többször is meghívhatja az erőforrást, és az egyes erőforrás-blokkokban egy másikra állíthatja az időzónát:</span><span class="sxs-lookup"><span data-stu-id="5e3f8-108">For example, in a previous implementation of the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource, a configuration could call the resource multiple times, setting the time zone to a different setting in each resource block:</span></span>

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

<span data-ttu-id="5e3f8-109">Ennek az az oka, hogy a DSC-erőforrás kulcsainak működése folyamatban van.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-109">This is because of the way DSC resource keys work.</span></span> <span data-ttu-id="5e3f8-110">Egy erőforrásnak legalább egy Key tulajdonsággal kell rendelkeznie.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-110">A resource must have at least one key property.</span></span> <span data-ttu-id="5e3f8-111">Az erőforrás-példány akkor minősül egyedinek, ha az összes kulcsfontosságú tulajdonság értékének kombinációja egyedi.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-111">A resource instance is considered unique if the combination of the values of all of its key properties is unique.</span></span> <span data-ttu-id="5e3f8-112">A korábbi implementációjában a [xTimeZone](https://github.com/PowerShell/xTimeZone) -erőforrásnak csak egy tulajdonsága volt – az időzóna, amely szükséges a kulcs megadásához.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-112">In its previous implementation, the [xTimeZone](https://github.com/PowerShell/xTimeZone) resource had only one property--**TimeZone**, which was required to be a key.</span></span> <span data-ttu-id="5e3f8-113">Emiatt egy konfiguráció, például a fenti, figyelmeztetés nélkül lesz lefordítva és futtatva.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-113">Because of this, a configuration such as the one above would compile and run without warning.</span></span> <span data-ttu-id="5e3f8-114">A **xTimeZone** összes erőforrás-blokkja egyedinek számít.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-114">Each of the **xTimeZone** resource blocks is considered unique.</span></span> <span data-ttu-id="5e3f8-115">Ez azt eredményezi, hogy a konfigurációt ismételten alkalmazni kell a csomópontra, majd az időzónát oda-vissza kell tekerni.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-115">This would cause the configuration to be repeatedly applied to the node, cycling the timezone back and forth.</span></span>

<span data-ttu-id="5e3f8-116">Annak biztosítása érdekében, hogy egy konfiguráció csak egyszer állítsa be a célként megadott csomópont időzónáját, a rendszer frissítette az erőforrást egy második tulajdonság ( **IsSingleInstance**) hozzáadásával, amely a Key tulajdonság lett.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-116">To ensure that a configuration could set the time zone for a target node only once, the resource was updated to add a second property, **IsSingleInstance**, that became the key property.</span></span>
<span data-ttu-id="5e3f8-117">A **IsSingleInstance** egyetlen értékre (igen) korlátozódott egy **ValueMap**használatával.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-117">The **IsSingleInstance** was limited to a single value, "Yes" by using a **ValueMap**.</span></span> <span data-ttu-id="5e3f8-118">Az erőforrás régi MOF-sémája a következő volt:</span><span class="sxs-lookup"><span data-stu-id="5e3f8-118">The old MOF schema for the resource was:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="5e3f8-119">Az erőforrás frissített MOF-sémája a következő:</span><span class="sxs-lookup"><span data-stu-id="5e3f8-119">The updated MOF schema for the resource is:</span></span>

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

<span data-ttu-id="5e3f8-120">Az erőforrás-parancsfájl az új paraméter használatára is frissült.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-120">The resource script was also updated to use the new parameter.</span></span> <span data-ttu-id="5e3f8-121">Az erőforrás-parancsfájl módosítása:</span><span class="sxs-lookup"><span data-stu-id="5e3f8-121">Here how the resource script was changed:</span></span>

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
    [CmdletBinding()]
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

    Write-Verbose -Message "Replace the System Time Zone to $TimeZone"
    
    try
    {
        if($CurrentTimeZone -ne $TimeZone)
        {
            Write-Verbose -Verbose "Setting the TimeZone"
            Set-TimeZone -TimeZone $TimeZone
        }
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

<span data-ttu-id="5e3f8-122">Figyelje meg, hogy az időzóna tulajdonság már nem kulcs.</span><span class="sxs-lookup"><span data-stu-id="5e3f8-122">Notice that the **TimeZone** property is no longer a key.</span></span> <span data-ttu-id="5e3f8-123">Most, ha egy konfiguráció kétszer próbálkozik az időzóna beállításával (két különböző, eltérő időzóna- értékkel rendelkező **xTimeZone** -blokk használatával), a konfiguráció fordítására tett kísérlet hibát okoz:</span><span class="sxs-lookup"><span data-stu-id="5e3f8-123">Now, if a configuration attempts to set the time zone twice (by using two different **xTimeZone** blocks with different **TimeZone** values), attempting to compile the configuration will cause an error:</span></span>

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
