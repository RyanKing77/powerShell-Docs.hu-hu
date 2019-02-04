---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: Egypéldányos DSC-erőforrás írása (ajánlott eljárás)
ms.openlocfilehash: 9494964b1b13eaa082ad5cbc279b4586bb7211cc
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688657"
---
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a>Egypéldányos DSC-erőforrás írása (ajánlott eljárás)

>**Megjegyzés:** Ez a témakör ismerteti az ajánlott eljárás, amely lehetővé teszi, hogy csak egy példányban konfigurációban DSC erőforrás meghatározása. Jelenleg nincs ehhez beépített DSC szolgáltatás. Amely a későbbiekben változhatnak.

Vannak helyzetek, ahol nem szeretné, hogy a többször használható konfigurációban egy erőforrást. Például az előző megvalósítását a [xTimeZone](https://github.com/PowerShell/xTimeZone) , egy konfigurációt sikerült erőforráshívásnak felelnek meg az erőforrás többször, különböző beállítását minden egyes erőforrás blokkban az időzóna beállítása:

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

Ez a DSC-erőforrás kulcsainak működik módja miatt. Egy erőforrás rendelkeznie kell legalább egy tulajdonsággal. Egy erőforrás-példány egyedi, ha az érték az összes kulcsfontosságú tulajdonságainak egyedi számít. Előző végrehajtása során a [xTimeZone](https://github.com/PowerShell/xTimeZone) erőforrás korábban csak az egyik tulajdonság--**időzóna**, amely szükséges kulcsként. Emiatt egy konfigurációjára, például a fenti lenne fordítása és futtatása figyelmeztetés nélkül. Minden egyes a **xTimeZone** erőforrás blokkok egyedinek számít. Emiatt a konfigurációt a csomópont, oda-vissza az időzóna recyklování többször is alkalmazható.

Annak érdekében, hogy csak egyszer, az erőforrás egy második tulajdonság hozzáadása megtörtént egy konfigurációt sikerült beállítani egy célcsomóponttal időzónáját **IsSingleInstance**, hogy a kulcstulajdonság vált.
A **IsSingleInstance** korlátozódott, egyetlen érték "Yes" használatával egy **ValueMap**. Az erőforrás a régi MOF-séma a következő:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

Az erőforrás a frissített MOF-séma a következő:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

Az erőforrás-parancsfájl használata az új paramétert is frissítve lett. Itt látható a régi erőforrás parancsfájlt:

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

Figyelje meg, hogy a **időzóna** tulajdonság már nem egy kulcsot. Most, ha egy konfigurációs próbál meg kétszer az időzóna beállítása (a két különböző **xTimeZone** az eltérő blokkokat **időzóna** értékek), konfiguráció fordítása kísérlet hiba miatt:

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