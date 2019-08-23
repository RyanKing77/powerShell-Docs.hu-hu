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
# <a name="writing-a-single-instance-dsc-resource-best-practice"></a>Egypéldányos DSC-erőforrás írása (ajánlott eljárás)

>**Megjegyzés:** Ez a témakör egy olyan DSC-erőforrás definiálásának ajánlott eljárását ismerteti, amely csak egyetlen példányt engedélyez a konfigurációban. Jelenleg nincs ilyen beépített DSC-funkció. A későbbiekben változhatnak.

Vannak olyan helyzetek, amikor nem szeretné, hogy egy erőforrás többször is felhasználható legyen a konfigurációban. Például a [xTimeZone](https://github.com/PowerShell/xTimeZone) erőforrás egy korábbi implementációjában a konfiguráció többször is meghívhatja az erőforrást, és az egyes erőforrás-blokkokban egy másikra állíthatja az időzónát:

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

Ennek az az oka, hogy a DSC-erőforrás kulcsainak működése folyamatban van. Egy erőforrásnak legalább egy Key tulajdonsággal kell rendelkeznie. Az erőforrás-példány akkor minősül egyedinek, ha az összes kulcsfontosságú tulajdonság értékének kombinációja egyedi. A korábbi implementációjában a [xTimeZone](https://github.com/PowerShell/xTimeZone) -erőforrásnak csak egy tulajdonsága volt – az időzóna, amely szükséges a kulcs megadásához. Emiatt egy konfiguráció, például a fenti, figyelmeztetés nélkül lesz lefordítva és futtatva. A **xTimeZone** összes erőforrás-blokkja egyedinek számít. Ez azt eredményezi, hogy a konfigurációt ismételten alkalmazni kell a csomópontra, majd az időzónát oda-vissza kell tekerni.

Annak biztosítása érdekében, hogy egy konfiguráció csak egyszer állítsa be a célként megadott csomópont időzónáját, a rendszer frissítette az erőforrást egy második tulajdonság ( **IsSingleInstance**) hozzáadásával, amely a Key tulajdonság lett.
A **IsSingleInstance** egyetlen értékre (igen) korlátozódott egy **ValueMap**használatával. Az erőforrás régi MOF-sémája a következő volt:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the TimeZone.")] String TimeZone;
};
```

Az erőforrás frissített MOF-sémája a következő:

```powershell
[ClassVersion("1.0.0.0"), FriendlyName("xTimeZone")]
class xTimeZone : OMI_BaseResource
{
    [Key, Description("Specifies the resource is a single instance, the value must be 'Yes'"), ValueMap{"Yes"}, Values{"Yes"}] String IsSingleInstance;
    [Required, Description("Specifies the TimeZone.")] String TimeZone;
};
```

Az erőforrás-parancsfájl az új paraméter használatára is frissült. Az erőforrás-parancsfájl módosítása:

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

Figyelje meg, hogy az időzóna tulajdonság már nem kulcs. Most, ha egy konfiguráció kétszer próbálkozik az időzóna beállításával (két különböző, eltérő időzóna- értékkel rendelkező **xTimeZone** -blokk használatával), a konfiguráció fordítására tett kísérlet hibát okoz:

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
