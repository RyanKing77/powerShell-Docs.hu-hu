---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: MOF-egyéni DSC-erőforrás írása
ms.openlocfilehash: 5917e20769e750042a9855649ff5bec36ad14eb4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687565"
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a>MOF-egyéni DSC-erőforrás írása

> Érvényes: Windows PowerShell 4.0-s, a Windows PowerShell 5.0

Ebben a témakörben azt fogja adjon meg egy Windows PowerShell Desired State Configuration (DSC) egyéni erőforrást a sémát a MOF-fájlt, és az erőforrás megvalósítása az egy olyan Windows PowerShell-parancsfájlt. Az egyéni erőforrás létrehozása és üzemeltetése egy webhely van.

## <a name="creating-the-mof-schema"></a>A MOF-séma létrehozása

A séma meghatározza az erőforrást, amely a DSC konfigurációs parancsfájlt is konfigurálhatja a tulajdonságait.

### <a name="folder-structure-for-a-mof-resource"></a>A mappastruktúra a MOF-erőforrás

DSC MOF sémával egyéni erőforrás megvalósításához, hozzon létre a következő mappaszerkezetet. A MOF-séma Demo_IISWebsite.schema.mof fájlban van definiálva, és az erőforrás-parancsfájl Demo_IISWebsite.psm1 van definiálva. Igény szerint hozhat létre egy modul jegyzékfájlt (psd1 kiterjesztésű) fájlt.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

Vegye figyelembe, hogy a legfelső szintű mappa alatt DSCResources nevű mappa létrehozásához szükséges, és, hogy a mappát az egyes erőforrások rendelkeznie kell az erőforrás azonos néven.

### <a name="the-contents-of-the-mof-file"></a>A MOF-fájl tartalmát

Következő egy példa MOF-fájlt, amely egy egyéni webhely erőforrás használható. Kövesse az ebben a példában, ebben a sémában mentése fájlba, és hívja meg a fájl *Demo_IISWebsite.schema.mof*.

```
[ClassVersion("1.0.0"), FriendlyName("Website")]
class Demo_IISWebsite : OMI_BaseResource
{
  [Key] string Name;
  [Required] string PhysicalPath;
  [write,ValueMap{"Present", "Absent"},Values{"Present", "Absent"}] string Ensure;
  [write,ValueMap{"Started","Stopped"},Values{"Started", "Stopped"}] string State;
  [write] string Protocol[];
  [write] string BindingInfo[];
  [write] string ApplicationPool;
  [read] string ID;
};
```

Az előző kód kapcsolatos megjegyzések:

* `FriendlyName` Meghatározza a segítségével tekintse meg a DSC konfigurációs szkripteket az egyéni erőforrás nevét. Ebben a példában `Website` egyenértékű a valódi nevet a `Archive` a beépített archív erőforrás.
* Az osztály esetében az egyéni erőforrás származhat határoz meg `OMI_BaseResource`.
* Kvalifikátor typu se `[Key]`, a tulajdonság azt jelzi, hogy ezt a tulajdonságot egyedileg azonosítja az erőforrás-példány. Legalább egy `[Key]` tulajdonságot kötelező megadni.
* A `[Required]` minősítő azt jelzi, hogy a tulajdonság megadása kötelező (értéket kell megadni minden más konfigurációs parancsfájl, amely ezt az erőforrást használ).
* A `[write]` minősítő azt jelzi, hogy ez a tulajdonság nem kötelező az egyéni erőforrás az konfigurációs parancsfájl használata során. A `[read]` minősítő azt jelzi, hogy a tulajdonság nem állítható be a konfiguráció szerint, és csak jelentéskészítési célból van.
* `Values` korlátozza az értékeket, amelyeket a megadott értékek listájára tulajdonsághoz rendelhető `ValueMap`. További információkért lásd: [ValueMap és érték minősítők](/windows/desktop/WmiSdk/value-map).
* Például egy tulajdonság nevű `Ensure` értékekkel `Present` és `Absent` arra, hogy a beépített DSC-erőforrások egységes stílus karbantartása javasolt az erőforrás.
* A sémafájl az egyéni erőforrás a következő nevet: `classname.schema.mof`, ahol `classname` azonosítója a következő a `class` kulcsszó a sémadefiníciókban.

### <a name="writing-the-resource-script"></a>Az erőforrás-parancsprogram írása

Az erőforrás-parancsfájl valósítja meg az erőforrás a logikát. Ebben a modulban nevű három funkció tartalmaznia **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource**. Mindhárom funkció, amely megegyezik a MOF-séma, az erőforrás létrehozott tulajdonságkészlettel paraméterkészlet kell tennie. Ebben a dokumentumban a tulajdonságai készletét a neve a "erőforrás-tulajdonságokat." Ezek három funkciót egy fájlban nevű Store <ResourceName>.psm1. A functions a következő példában egy Demo_IISWebsite.psm1 nevű fájlban vannak tárolva.

> **Megjegyzés:**: Az ugyanazon konfigurációs parancsfájl futtatásakor az erőforráson egynél többször, meg kell kapnia nincsenek hibák, és az erőforrás továbbra is ugyanazt az állapotot, a szkript futtatása után. Ehhez ellenőrizze, hogy a **Get-TargetResource** és **Test-TargetResource** funkciók hagyja változatlanul az erőforrás és a meghívása a **Set-TargetResource**egynél többször ugyanezt a paramétert a sorrendben értékek 03T00 mindig egyszer ad meg, a függvény.

Az a **Get-TargetResource** függvény végrehajtása, a legfontosabb tulajdonságértékek biztosított paraméterek segítségével ellenőrizze a megadott erőforrás-példányának állapotát. Ez a függvény egy kivonattábla, amely felsorolja a kulcsok és a tényleges értékek ezeket a tulajdonságokat, mint a megfelelő értékeket erőforrás-tulajdonságok kell visszaadnia. A következő kód mutatja be.

```powershell
# DSC uses the Get-TargetResource function to fetch the status of the resource instance specified in the parameters for the target machine
function Get-TargetResource
{
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

        $getTargetResourceResult = $null;

        <# Insert logic that uses the mandatory parameter values to get the website and assign it to a variable called $Website #>
        <# Set $ensureResult to "Present" if the requested website exists and to "Absent" otherwise #>

        # Add all Website properties to the hash table
        # This simple example assumes that $Website is not null
        $getTargetResourceResult = @{
                                      Name = $Website.Name;
                                        Ensure = $ensureResult;
                                        PhysicalPath = $Website.physicalPath;
                                        State = $Website.state;
                                        ID = $Website.id;
                                        ApplicationPool = $Website.applicationPool;
                                        Protocol = $Website.bindings.Collection.protocol;
                                        Binding = $Website.bindings.Collection.bindingInformation;
                                    }

        $getTargetResourceResult;
}
```

Attól függően, az értékeket, amelyeket a konfigurációs parancsfájlt, az erőforrás-tulajdonságok vannak megadva a **Set-TargetResource** tegye a következők egyikét:

* Új webhely létrehozása
* Egy létező webhely frissítése
* Egy létező webhely törlése

A következő példa ezt mutatja be.

```powershell
# The Set-TargetResource function is used to create, delete or configure a website on the target machine.
function Set-TargetResource
{
    [CmdletBinding(SupportsShouldProcess=$true)]
    param
    (
        [ValidateSet("Present", "Absent")]
        [string]$Ensure = "Present",

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$Name,

        [Parameter(Mandatory)]
        [ValidateNotNullOrEmpty()]
        [string]$PhysicalPath,

        [ValidateSet("Started", "Stopped")]
        [string]$State = "Started",

        [string]$ApplicationPool,

        [string[]]$BindingInfo,

        [string[]]$Protocol
    )

    <# If Ensure is set to "Present" and the website specified in the mandatory input parameters does not exist, then create it using the specified parameter values #>
    <# Else, if Ensure is set to "Present" and the website does exist, then update its properties to match the values provided in the non-mandatory parameter values #>
    <# Else, if Ensure is set to "Absent" and the website does not exist, then do nothing #>
    <# Else, if Ensure is set to "Absent" and the website does exist, then delete the website #>
}
```

Végül a **Test-TargetResource** függvény végre kell hajtania állítja be ugyanezt a paramétert **Get-TargetResource** és **Set-TargetResource**. A megvalósításában **Test-TargetResource**, az erőforrás-példány a fő paraméterekkel megadott állapotának ellenőrzéséhez. A tényleges erőforrás-példány állapota nem felel meg a paraméterkészletet megadott értékeket, ha vissza **$false**. Ellenkező esetben vissza **$true**.

A következő kód valósítja meg a **Test-TargetResource** függvény.

```powershell
function Test-TargetResource
{
[CmdletBinding()]
[OutputType([System.Boolean])]
param
(
[ValidateSet("Present","Absent")]
[System.String]
$Ensure,

[parameter(Mandatory = $true)]
[System.String]
$Name,

[parameter(Mandatory = $true)]
[System.String]
$PhysicalPath,

[ValidateSet("Started","Stopped")]
[System.String]
$State,

[System.String[]]
$Protocol,

[System.String[]]
$BindingData,

[System.String]
$ApplicationPool
)

#Write-Verbose "Use this cmdlet to deliver information about command processing."

#Write-Debug "Use this cmdlet to write debug information while troubleshooting."


#Include logic to
$result = [System.Boolean]
#Add logic to test whether the website is present and its status mathes the supplied parameter values. If it does, return true. If it does not, return false.
$result
}
```

**Megjegyzés:**: Könnyebb hibakeresés, használja a **Write-Verbose** parancsmagot az előző három funkció megvalósítását.
>Ez a parancsmag szöveget ír a részletes üzenet-adatfolyam.
>Alapértelmezés szerint a részletes üzenet-adatfolyam nem jelenik meg, de értékét módosítsa úgy a megjelenítéséhez a **$VerbosePreference** változó vagy a használatával a **részletes** paraméter a DSC-parancsmagok = új.

### <a name="creating-the-module-manifest"></a>A modul jegyzékfájl létrehozása

Végül a **New-ModuleManifest** meghatározásához a parancsmag egy <ResourceName>.psd1 fájlban az egyéni erőforrás-modulhoz. Ezzel a parancsmaggal indít el, ha az előző szakaszban leírt parancsfájl modul (.psm1) hivatkozik. Például **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource** exportálása funkciók listájában. Következő egy példa jegyzékfájl.

```powershell
# Module manifest for module 'Demo.IIS.Website'
#
# Generated on: 1/10/2013
#

@{

# Script module or binary module file associated with this manifest.
# RootModule = ''

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '6AB5ED33-E923-41d8-A3A4-5ADDA2B301DE'

# Author of this module
Author = 'Contoso'

# Company or vendor of this module
CompanyName = 'Contoso'

# Copyright statement for this module
Copyright = 'Contoso. All rights reserved.'

# Description of the functionality provided by this module
Description = 'This Module is used to support the creation and configuration of IIS Websites through Get, Set and Test API on the DSC managed nodes.'

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '4.0'

# Minimum version of the common language runtime (CLR) required by this module
CLRVersion = '4.0'

# Modules that must be imported into the global environment prior to importing this module
RequiredModules = @("WebAdministration")

# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = @("Demo_IISWebsite.psm1")

# Functions to export from this module
FunctionsToExport = @("Get-TargetResource", "Set-TargetResource", "Test-TargetResource")

# Cmdlets to export from this module
#CmdletsToExport = '*'

# HelpInfo URI of this module
# HelpInfoURI = ''
}
```

## <a name="supporting-psdscrunascredential"></a>PsDscRunAsCredential támogatása

>**Megjegyzés:** **PsDscRunAsCredential** a PowerShell 5.0-s és újabb verzióiban támogatott.

A **PsDscRunAsCredential** tulajdonság használható [DSC-konfigurációk](../configurations/configurations.md) erőforrás letiltása, hogy az erőforrás alatt kell futtatni. egy meghatározott hitelesítő adatok megadásához.
További információkért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md).

A felhasználói környezet belül egy egyéni erőforrás elérésére, használhatja az automatikus változót `$PsDscContext`.

Például a következő kódot a felhasználói környezet, amelyben az erőforrás fut. a részletes kimeneti adatfolyamba volna írni:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```

## <a name="rebooting-the-node"></a>A csomópont újraindítása

Ha a végrehajtott műveletek az `Set-TargetResource` függvény újra kell indítani, globális jelző használatával ossza meg az LCM kell újraindítani a csomópontot. Az újraindítás közvetlenül után kerül sor a `Set-TargetResource` függvény lefutott.

Belül a `Set-TargetResource` működik, adja hozzá a következő kódsort.

```powershell
# Include this line if the resource requires a system reboot.
$global:DSCMachineStatus = 1
```

Ahhoz, hogy az LCM kell újraindítani a csomópontot a **RebootNodeIfNeeded** jelzőt kell beállítani `$true`. A **ActionAfterReboot** beállítás is meg kell **ContinueConfiguration**, amely az alapértelmezett érték. Az LCM konfigurálása a további információkért lásd: [a Local Configuration Manager](../managing-nodes/metaConfig.md), vagy [a Local Configuration Manager (v4)](../managing-nodes/metaConfig4.md).
