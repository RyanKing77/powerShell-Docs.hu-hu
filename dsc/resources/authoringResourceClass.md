---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A PowerShell-osztályok egyéni DSC-erőforrás írása
ms.openlocfilehash: 0759685b04688f574d72b62a15833832ad19e816
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404336"
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a>A PowerShell-osztályok egyéni DSC-erőforrás írása

> Érvényes: Windows PowerShell 5.0

PowerShell-osztályok a Windows PowerShell 5.0 bevezetésével most már megadhatja a DSC-erőforrás osztály létrehozásával. Az osztály a séma- és az erőforrás végrehajtásának határozza meg, így nem kell külön MOF-fájl létrehozásához. A gyökérmappa-szerkezetében osztályalapú erőforrás egyben egyszerűbb, mivel egy **DSCResources** mappa már nem szükséges.

Osztályalapú DSC erőforrás a séma számít, ha az osztály, amely attribútumait megadhatja a tulajdonság módosítható tulajdonságai... Az erőforrás valósít meg **Get()**, **Set()**, és **Test()** metódusok (egyenértékű a **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource** függvények a parancsfájl erőforrást.

Ebben a témakörben egy egyszerű erőforrás nevű hozunk létre **FileResource** , amely kezeli a megadott elérési út egy fájlt.

DSC-erőforrások kapcsolatos további információkért lásd: [hozhat létre egyéni Windows PowerShell Desired State Configuration erőforrások](authoringResource.md)

>**Megjegyzés:** Általános gyűjtemények nem támogatottak az osztály-alapú erőforrások.

## <a name="folder-structure-for-a-class-resource"></a>A mappastruktúra osztály erőforrás

Egy olyan PowerShell osztállyal DSC egyéni erőforrás implementálásához hozzon létre a következő mappaszerkezetet. Az osztály definiálva van **MyDscResource.psm1** , és a moduljegyzékben meghatározva **MyDscResource.psd1**.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1
           MyDscResource.psd1
```

## <a name="create-the-class"></a>Az osztály létrehozása

Az osztály kulcsszó használatával hozzon létre egy PowerShell-osztályt. Adja meg, hogy egy osztály a DSC-erőforrás, használja a **DscResource()** attribútum. Az osztály nevét a DSC-erőforrás neve.

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a>Deklarálja a tulajdonságai

A DSC-erőforrás séma számít, ha az osztály tulajdonságait. A következő azt deklarálja három tulajdonságot.

```powershell
[DscProperty(Key)]
[string]$Path

[DscProperty(Mandatory)]
[Ensure] $Ensure

[DscProperty(Mandatory)]
[string] $SourcePath

[DscProperty(NotConfigurable)]
[Nullable[datetime]] $CreationTime
```

Figyelje meg, hogy a Tulajdonságok attribútumok szerint módosítják. Az attribútumok értelmében a következőképpen történik:

- **DscProperty(Key)**: A tulajdonság megadása kötelező. A tulajdonság egy kulcsot. Kulcsok belül egy konfigurációs egy erőforrás-példány egyedi azonosításához kell alakítania megjelölt összes tulajdonságának értékét.
- **DscProperty(Mandatory)**: A tulajdonság megadása kötelező.
- **DscProperty(NotConfigurable)**: A tulajdonság csak olvasható. Ez attribútummal rendelkező tulajdonságok nem állítható be a konfiguráció, de által fel van töltve a **Get()** módszer, ha a jelen.
- **DscProperty()**: A tulajdonság konfigurálható, de ez nem kötelező.

A **$Path** és **$SourcePath** tulajdonságok a következők mindkét karakterláncokat. A **$CreationTime** van egy [DateTime](/dotnet/api/system.datetime) tulajdonság. A **$Ensure** tulajdonság meghatározása a következő enumerálási típusát.

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a>A metódusok végrehajtása

A **Get()**, **Set()**, és **Test()** módszerek a következők csatlakoztatja a **Get-TargetResource**, **Set-TargetResource** , és **Test-TargetResource** függvények a parancsfájl erőforrást.

Ez a kód is magában foglalja a CopyFile() függvény segítő függvény, amely átmásolja a fájlt a **$SourcePath** való **$Path**.

```powershell

    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)

        if ($this.ensure -eq [Ensure]::Present)
        {
            if(-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ErrorAction Ignore

        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = New-Object -TypeName System.IO.FileInfo($this.Path)

        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
```

### <a name="the-complete-file"></a>A teljes fájl
A teljes fájl követi.

```powershell
enum Ensure
{
    Absent
    Present
}

<#
   This resource manages the file in a specific path.
   [DscResource()] indicates the class is a DSC resource
#>

[DscResource()]
class FileResource
{
    <#
       This property is the fully qualified path to the file that is
       expected to be present or absent.

       The [DscProperty(Key)] attribute indicates the property is a
       key and its value uniquely identifies a resource instance.
       Defining this attribute also means the property is required
       and DSC will ensure a value is set before calling the resource.

       A DSC resource must define at least one key property.
    #>
    [DscProperty(Key)]
    [string]$Path

    <#
        This property indicates if the settings should be present or absent
        on the system. For present, the resource ensures the file pointed
        to by $Path exists. For absent, it ensures the file point to by
        $Path does not exist.

        The [DscProperty(Mandatory)] attribute indicates the property is
        required and DSC will guarantee it is set.

        If Mandatory is not specified or if it is defined as
        Mandatory=$false, the value is not guaranteed to be set when DSC
        calls the resource.  This is appropriate for optional properties.
    #>
    [DscProperty(Mandatory)]
    [Ensure] $Ensure

    <#
       This property defines the fully qualified path to a file that will
       be placed on the system if $Ensure = Present and $Path does not
        exist.

       NOTE: This property is required because [DscProperty(Mandatory)] is
        set.
    #>
    [DscProperty(Mandatory)]
    [string] $SourcePath

    <#
       This property reports the file's create timestamp.

       [DscProperty(NotConfigurable)] attribute indicates the property is
       not configurable in DSC configuration.  Properties marked this way
       are populated by the Get() method to report additional details
       about the resource when it is present.

    #>
    [DscProperty(NotConfigurable)]
    [Nullable[datetime]] $CreationTime

    <#
        This method is equivalent of the Set-TargetResource script function.
        It sets the resource to the desired state.
    #>
    [void] Set()
    {
        $fileExists = $this.TestFilePath($this.Path)
        if ($this.ensure -eq [Ensure]::Present)
        {
            if (-not $fileExists)
            {
                $this.CopyFile()
            }
        }
        else
        {
            if ($fileExists)
            {
                Write-Verbose -Message "Deleting the file $($this.Path)"
                Remove-Item -LiteralPath $this.Path -Force
            }
        }
    }

    <#
        This method is equivalent of the Test-TargetResource script function.
        It should return True or False, showing whether the resource
        is in a desired state.
    #>
    [bool] Test()
    {
        $present = $this.TestFilePath($this.Path)

        if ($this.Ensure -eq [Ensure]::Present)
        {
            return $present
        }
        else
        {
            return -not $present
        }
    }

    <#
        This method is equivalent of the Get-TargetResource script function.
        The implementation should use the keys to find appropriate resources.
        This method returns an instance of this class with the updated key
         properties.
    #>
    [FileResource] Get()
    {
        $present = $this.TestFilePath($this.Path)

        if ($present)
        {
            $file = Get-ChildItem -LiteralPath $this.Path
            $this.CreationTime = $file.CreationTime
            $this.Ensure = [Ensure]::Present
        }
        else
        {
            $this.CreationTime = $null
            $this.Ensure = [Ensure]::Absent
        }

        return $this
    }

    <#
        Helper method to check if the file exists and it is file
    #>
    [bool] TestFilePath([string] $location)
    {
        $present = $true

        $item = Get-ChildItem -LiteralPath $location -ea Ignore
        if ($item -eq $null)
        {
            $present = $false
        }
        elseif ($item.PSProvider.Name -ne "FileSystem")
        {
            throw "Path $($location) is not a file path."
        }
        elseif ($item.PSIsContainer)
        {
            throw "Path $($location) is a directory path."
        }

        return $present
    }

    <#
        Helper method to copy file from source to path
    #>
    [void] CopyFile()
    {
        if (-not $this.TestFilePath($this.SourcePath))
        {
            throw "SourcePath $($this.SourcePath) is not found."
        }

        [System.IO.FileInfo] $destFileInfo = new-object System.IO.FileInfo($this.Path)
        if (-not $destFileInfo.Directory.Exists)
        {
            Write-Verbose -Message "Creating directory $($destFileInfo.Directory.FullName)"

            <#
                Use CreateDirectory instead of New-Item to avoid code
                 to handle the non-terminating error
            #>
            [System.IO.Directory]::CreateDirectory($destFileInfo.Directory.FullName)
        }

        if (Test-Path -LiteralPath $this.Path -PathType Container)
        {
            throw "Path $($this.Path) is a directory path"
        }

        Write-Verbose -Message "Copying $($this.SourcePath) to $($this.Path)"

        # DSC engine catches and reports any error that occurs
        Copy-Item -LiteralPath $this.SourcePath -Destination $this.Path -Force
    }
} # This module defines a class for a DSC "FileResource" provider.
```


## <a name="create-a-manifest"></a>Jegyzék létrehozásához

Osztályalapú erőforrás akkor válik elérhetővé a DSC motor, meg kell adni egy **DscResourcesToExport** utasítás, amely arra utasítja a modult, exportálhatja az erőforrás-jegyzékfájl. A jegyzékfájl így néz ki:

```powershell
@{

# Script module or binary module file associated with this manifest.
RootModule = 'MyDscResource.psm1'

DscResourcesToExport = 'FileResource'

# Version number of this module.
ModuleVersion = '1.0'

# ID used to uniquely identify this module
GUID = '81624038-5e71-40f8-8905-b1a87afe22d7'

# Author of this module
Author = 'Microsoft Corporation'

# Company or vendor of this module
CompanyName = 'Microsoft Corporation'

# Copyright statement for this module
Copyright = '(c) 2014 Microsoft. All rights reserved.'

# Description of the functionality provided by this module
# Description = ''

# Minimum version of the Windows PowerShell engine required by this module
PowerShellVersion = '5.0'

# Name of the Windows PowerShell host required by this module
# PowerShellHostName = ''
}
```

## <a name="test-the-resource"></a>Az erőforrás tesztelése

Az osztály és fájlok mentése a korábban leírtaknak megfelelően a gyökérmappa-szerkezetében lévő, után az új erőforrás használó konfiguráció is létrehozhat. A DSC-konfiguráció futtatásával kapcsolatos további információkért lásd: [konfigurációk életbe léptetése](../pull-server/enactingConfigurations.md). A következő konfigurációt ellenőrzi, hogy a fájlban a következő `c:\test\test.txt` létezik, és ha nem, másolja át a fájlt a `c:\test.txt` (hozzon létre `c:\test.txt` a konfiguráció futtatása előtt).

```powershell
Configuration Test
{
    Import-DSCResource -module MyDscResource
    FileResource file
    {
        Path = "C:\test\test.txt"
        SourcePath = "c:\test.txt"
        Ensure = "Present"
    }
}
Test
Start-DscConfiguration -Wait -Force Test
```

## <a name="supporting-psdscrunascredential"></a>PsDscRunAsCredential támogatása

>**Megjegyzés:** **PsDscRunAsCredential** a PowerShell 5.0-s és újabb verzióiban támogatott.

A **PsDscRunAsCredential** tulajdonság használható [DSC-konfigurációk](../configurations/configurations.md) erőforrás letiltása, hogy az erőforrás alatt kell futtatni. egy meghatározott hitelesítő adatok megadásához.
További információkért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](../configurations/runAsUser.md).

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a>Szükséges, vagy az erőforrás PsDscRunAsCredential letiltása

A **DscResource()** attribútumot vesz igénybe egy nem kötelező paraméter **RunAsCredential**.
Ez a paraméter három érték egyikét veheti fel:

- `Optional` **PsDscRunAsCredential** nem kötelező konfigurációk, amelyek meg az ehhez az erőforráshoz. Ez az alapértelmezett érték.
- `Mandatory` **PsDscRunAsCredential** kell használni minden olyan konfiguráció, amely meghívja ezt az erőforrást.
- `NotSupported` Konfigurációk, amelyek meg az ehhez az erőforráshoz nem használható **PsDscRunAsCredential**.
- `Default` Ugyanaz, mint a `Optional`.

Például adja meg, hogy az egyéni erőforrás nem támogatja a következő attribútum segítségével **PsDscRunAsCredential**:

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a>Hozzáférés a felhasználói környezet

A felhasználói környezet belül egy egyéni erőforrás elérésére, használhatja az automatikus változót `$global:PsDscContext`.

Például a következő kódot a felhasználói környezet, amelyben az erőforrás fut. a részletes kimeneti adatfolyamba volna írni:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Lásd még:
### <a name="concepts"></a>Fogalmak
[Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása](authoringResource.md)