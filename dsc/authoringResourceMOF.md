---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: Egyéni DSC-erőforrás MOF írása
ms.openlocfilehash: 50b5f2eddbac4571f5351b32648d45c54ded167e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189635"
---
# <a name="writing-a-custom-dsc-resource-with-mof"></a>Egyéni DSC-erőforrás MOF írása

> Vonatkozik: A Windows PowerShell 4.0-s verzióját, a Windows PowerShell 5.0

Ebben a témakörben rendszer MOF-fájlt ad meg egy Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) egyéni erőforrás sémáját, és az erőforrás valósítania egy olyan Windows PowerShell-parancsfájlt. Az egyéni erőforrás létrehozására és karbantartására egy webhely van.

## <a name="creating-the-mof-schema"></a>A MOF-séma létrehozása

A séma definiálja az erőforrás, amelyek képesek a DSC-konfigurációs parancsprogram tulajdonságait.

### <a name="folder-structure-for-a-mof-resource"></a>A MOF-erőforrások esetében mappaszerkezet

Egyéni DSC-erőforrás a MOF-séma szükséges, hozzon létre a következő mappaszerkezetet. A MOF-séma Demo_IISWebsite.schema.mof fájlban van definiálva, és az erőforrást parancsprogram Demo_IISWebsite.psm1 van definiálva. Másik lehetőségként létrehozhat egy modul jegyzékfájl (psd1 kiterjesztésű) fájlt.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResources (folder)
        |- DSCResources (folder)
            |- Demo_IISWebsite (folder)
                |- Demo_IISWebsite.psd1 (file, optional)
                |- Demo_IISWebsite.psm1 (file, required)
                |- Demo_IISWebsite.schema.mof (file, required)
```

Vegye figyelembe, hogy a legfelső szintű mappa alatt DSCResources nevű mappa létrehozásához szükséges, és, hogy a mappa minden erőforrás neve megegyezik az erőforrás kell rendelkeznie.

### <a name="the-contents-of-the-mof-file"></a>A MOF-fájl tartalma

Az alábbiakban látható egy példa MOF-fájlt egy egyéni webhely erőforrás használható. Kövesse az alábbi példát, ebben a sémában mentése fájlba, és hívja meg a fájl *Demo_IISWebsite.schema.mof*.

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

Vegye figyelembe az alábbiakat az előző kóddal:

* `FriendlyName` Tekintse meg az egyéni erőforrást DSC konfigurációs parancsfájlok segítségével nevet határoz meg. Ebben a példában `Website` felel meg a rövid név `Archive` a beépített archív erőforrás.
* Megadhatja az egyéni erőforrás kell származnia: az osztály `OMI_BaseResource`.
* A típus minősítő `[Key]`, a tulajdonság azt jelzi, hogy ezt a tulajdonságot egyedileg azonosítja a erőforráspéldány. Legalább egy `[Key]` tulajdonság megadása kötelező.
* A `[Required]` minősítő azt jelzi, hogy a tulajdonság szükséges (értéket kell megadni az összes konfigurációs parancsfájl, amely ezt az erőforrást használ).
* A `[write]` minősítő azt jelzi, hogy ez a tulajdonság opcionális konfigurációs parancsfájl az egyéni erőforrás használatakor. A `[read]` minősítő azt jelzi, hogy a tulajdonság nem állítható be olyan konfigurációja, és csak jelentéskészítési célból van.
* `Values` korlátozza az értékeket, amelyek a meghatározott értékek listájának tulajdonság hozzárendelhető `ValueMap`. További információkért lásd: [ValueMap és érték minősítők](https://msdn.microsoft.com/library/windows/desktop/aa393965.aspx).
* Például egy tulajdonság nevű `Ensure` értékekkel `Present` és `Absent` egyik módja egy beépített DSC-erőforrások egységes stílust karbantartása javasolt az erőforrás.
* A fájl az egyéni erőforrás neve az alábbiak szerint: `classname.schema.mof`, ahol `classname` az azonosító, amelyet a következő a `class` a sémadefiníciót kulcsszót.

### <a name="writing-the-resource-script"></a>Az erőforrást parancsprogram írása

Az erőforrást parancsprogram valósítja meg az erőforrás logikáját. Ebben a modulban, fel kell venni nevű három funkció **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource**. Minden három funkciók kell tennie egy paraméter halmaza, amelyet a tulajdonságkészletbe, amelyet az erőforrás hozott létre a MOF-sémájában definiált azonos. Ebben a dokumentumban a tulajdonságkészletbe műveletek a "erőforrás-tulajdonságokat." Tárban, ezek három funkciók egy fájlban <ResourceName>.psm1. A következő példában a funkciók Demo_IISWebsite.psm1 nevű fájlban vannak tárolva.

> **Megjegyzés:**: a azonos konfigurációs parancsfájl futtatása a erőforráson egynél többször, nincs hiba kell kapnia, és egyszer fut a parancsfájl abban az állapotban maradjon. az erőforrás. Ennek megvalósítása érdekében ügyeljen arra, hogy a **Get-TargetResource** és **teszt-TargetResource** funkciók hagyja változatlanul az erőforrás, és adott meghívása a **Set-TargetResource**egynél többször a ugyanezt a paramétert sorozatba értékek megegyezik mindig egyszer hívja az működik.

Az a **Get-TargetResource** függvény végrehajtása, által biztosított kulcs erőforrás tulajdonságértéket paraméter segítségével tekintse meg a megadott erőforráspéldány. Ez a függvény egy kivonattáblát a kulcsok és a tényleges értékek ezeket a tulajdonságokat, mint a megfelelő értékeket erőforrás-tulajdonságok felsoroló kell visszaadnia. A következő kód példaként szolgál.

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

Attól függően, hogy az értékek, amelyek nincsenek megadva az erőforrás-tulajdonságok konfigurációs parancsfájl a **Set-TargetResource** tegye a következők egyikét:

* Új webhely létrehozása
* Frissítés egy meglévő webhelyen
* Egy meglévő webhelyen törlése

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

Végezetül a **teszt-TargetResource** függvény állítja be ugyanazon paraméter szükséges **Get-TargetResource** és **Set-TargetResource**. A megvalósításával **teszt-TargetResource**, tekintse meg a paramétereket a megadott erőforráspéldány. Ha a tényleges állapot, az erőforrás-példány nem egyezik meg a paraméterhalmaz megadott értékeket, térjen vissza **$false**. Ellenkező esetben a visszatérési **$true**.

A következő kódot valósít meg a **teszt-TargetResource** függvény.

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

**Megjegyzés:**: hibakereséshez egyszerűbb, használja a **Write-Verbose** parancsmag az előző három funkció megvalósítását.
>Ez a parancsmag szöveg ír a részletes üzenet-adatfolyam.
>Alapértelmezés szerint a részletes üzenet-adatfolyam nem jelenik meg, de értékének módosításával megjelenítheti a **$VerbosePreference** változó vagy használatával a **részletes** a DSC-parancsmagok paraméter = új.

### <a name="creating-the-module-manifest"></a>A modul jegyzékfájl létrehozása

Végül a **New-ModuleManifest** parancsmag használatával adja meg a <ResourceName>.psd1 fájlt az egyéni erőforrás modul. Ez a parancsmag meghívásakor hivatkozzon a parancsfájl (.psm1) modul az előző szakaszban leírt. Tartalmaznak **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource** exportálása funkciók közül. Az alábbiakban látható egy példa jegyzékfájlt.

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

>**Megjegyzés:** **PsDscRunAsCredential** PowerShell 5.0-s vagy újabb támogatott.

A **PsDscRunAsCredential** tulajdonság használható [a DSC-konfigurációk](configurations.md) erőforrás blokk adhatja meg, hogy az erőforrás verziója alatt kell futtatni a megadott hitelesítő adatok készletét.
További információkért lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).

A felhasználói környezet belül egyéni erőforrás eléréséhez használhatja az automatikus változó `$PsDscContext`.

Például a következő kódot a felhasználói környezet, amely alatt az erőforrás fut, a részletes kimeneti adatfolyamba lesz írási:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $PsDscContext.RunAsUser";
}
```