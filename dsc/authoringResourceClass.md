---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: A PowerShell osztályok egyéni DSC-erőforrás írása
ms.openlocfilehash: f2500bfb41302cbeaf3cb9d23b843f26f01c1d5b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a>A PowerShell osztályok egyéni DSC-erőforrás írása

> Vonatkozik: Windows Windows PowerShell 5.0

A Windows PowerShell 5.0 PowerShell osztályok bevezetésével most hozzon létre egy osztályt adhat meg DSC erőforrás. Az osztály a séma- és az erőforrás végrehajtásának határozza meg, így nincs szükség külön MOF-fájl létrehozásához. A gyökérmappa-szerkezetében osztály-alapú erőforrásokhoz is felügyelete egyszerűbb, mert egy **DSCResources** mappa nincs szükség.

Osztály-alapú DSC az erőforrás a séma van definiálva, amely attribútumokkal megadhatja a tulajdonság módosítható-osztály tulajdonságai... Az erőforrás megvalósítja **Get()**, **set() metódust**, és **Test()** módszerek (egyenértékű a **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource** funkciók a parancsprogram-erőforráshoz.

Ebben a témakörben létrehozunk egy egyszerű nevű erőforrás **FileResource** , amely kezeli a fájl a megadott elérési úton.

A DSC-erőforrásokra vonatkozó további információkért lásd: [Build egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások](authoringResource.md)

>**Megjegyzés:** általános gyűjtemények osztály fájlalapú erőforrások – használata nem támogatott.

## <a name="folder-structure-for-a-class-resource"></a>Egy osztály erőforrás mappaszerkezet

Egyéni DSC-erőforrás PowerShell osztállyal alkalmazásához hozzon létre a következő mappaszerkezetet. Az osztály definiálva van **MyDscResource.psm1** , és a moduljegyzékben meghatározva **MyDscResource.psd1**.

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1
           MyDscResource.psd1
```

## <a name="create-the-class"></a>Az osztály létrehozásához

Az osztály kulcsszó használatával hozzon létre egy PowerShell-osztályt. Adja meg, hogy egy osztály DSC erőforrás, használja a **DscResource()** attribútum. Az osztály nevét a DSC-erőforrás neve.

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a>Deklarálja tulajdonságai

A DSC-erőforrás séma a osztály tulajdonságai típusúként van definiálva. Az alábbiak szerint deklarálja azt három tulajdonságot.

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

Figyelje meg, hogy a tulajdonság módosítását mutatjuk be attribútumok szerint. Az attribútumok szerinti a következőképpen történik:

- **DscProperty(Key)**: A tulajdonságra szükség. A tulajdonság egy kulcsot. Az összes tulajdonság értékének megjelölt kulcsok kell alakítania egy erőforráspéldány konfiguráció belül egyedi azonosításához.
- **DscProperty(Mandatory)**: A tulajdonságra szükség.
- **DscProperty(NotConfigurable)**: A tulajdonság csak olvasható. Ez attribútummal rendelkező tulajdonságok nem állíthatják be a konfigurációs, de által a rendszer feltölti a **Get()** metódust, ha létezik.
- **DscProperty()**: A tulajdonság konfigurálható, de nincs rá szükség.

A **$Path** és **$SourcePath** tulajdonságainak mindkét karakterláncot. A **$CreationTime** van egy [DateTime](https://technet.microsoft.com/library/system.datetime.aspx) tulajdonság. A **$Ensure** tulajdonsága egy számbavételi típus, az alábbiak szerint definiáltuk.

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a>Az eljárások végrehajtása

A **Get()**, **set() metódust**, és **Test()** módszerrel is hasonló a **Get-TargetResource**, **Set-TargetResource** , és **teszt-TargetResource** funkciók a parancsprogram-erőforráshoz.

Ezt a kódot is magában foglalja a CopyFile() függvény, másolja át a fájlt a segítő függvény **$SourcePath** való **$Path**.

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
A teljes osztály fájl követi.

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


## <a name="create-a-manifest"></a>A jegyzékfájl létrehozása

A DSC-motor elérhetővé tegyen egy osztály-alapú erőforrás, akkor tartalmaznia kell egy **DscResourcesToExport** kivonat a jegyzékfájlban, amely arra utasítja az erőforrás exportálandó modul. A jegyzékfájl így néz ki:

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

Miután az osztály és a jegyzékfájlt a a mappastruktúra a fentebb leírt módon, az új erőforrás használó konfiguráció is létrehozhat. A DSC-konfiguráció futtatásával kapcsolatos információkért lásd: [konfigurációk hozzanak](enactingConfigurations.md). A következő konfigurációs ellenőrzi, hogy a fájlban a következő `c:\test\test.txt` létezik, és ha nem, másolja át a fájlt a `c:\test.txt` (létre kell hoznia `c:\test.txt` a konfiguráció futtatása előtt).

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

>**Megjegyzés:** **PsDscRunAsCredential** PowerShell 5.0-s vagy újabb támogatott.

A **PsDscRunAsCredential** tulajdonság használható [a DSC-konfigurációk](configurations.md) erőforrás blokk adhatja meg, hogy az erőforrás verziója alatt kell futtatni a megadott hitelesítő adatok készletét.
További információkért lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a>Szükséges, vagy az erőforrás PsDscRunAsCredential letiltása

A **DscResource()** attribútum egy választható paramétert fogad, **RunAsCredential**.
Ezt a paramétert értékek egyike szükséges:

- `Optional` **PsDscRunAsCredential** nem kötelező konfigurációk, amelyek ehhez az erőforráshoz. Ez az alapértelmezett érték.
- `Mandatory` **PsDscRunAsCredential** , amely behívja ehhez az erőforráshoz konfigurálni kell használni.
- `NotSupported` Ehhez az erőforráshoz hívó konfigurációk nem használható **PsDscRunAsCredential**.
- `Default` Ugyanaz, mint a `Optional`.

Például adja meg, hogy az egyéni erőforrás nem támogatja a következő attribútum segítségével **PsDscRunAsCredential**:

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a>Hozzáférés a felhasználói környezet

A felhasználói környezet belül egyéni erőforrás eléréséhez használhatja az automatikus változó `$global:PsDscContext`.

Például a következő kódot a felhasználói környezet, amely alatt az erőforrás fut, a részletes kimeneti adatfolyamba lesz írási:

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a>Lásd még:
### <a name="concepts"></a>Fogalmak
[Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása](authoringResource.md)