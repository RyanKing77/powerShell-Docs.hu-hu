---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "a DSC, a powershell, a konfiguráció, a beállítása"
title: "A PowerShell osztályok egyéni DSC-erőforrás írása"
ms.openlocfilehash: 6e482f45c7d09898d46de20f43dcf16ecf3da7da
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a><span data-ttu-id="5f326-103">A PowerShell osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="5f326-103">Writing a custom DSC resource with PowerShell classes</span></span>

> <span data-ttu-id="5f326-104">Vonatkozik: Windows Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="5f326-104">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="5f326-105">A Windows PowerShell 5.0 PowerShell osztályok bevezetésével most hozzon létre egy osztályt adhat meg DSC erőforrás.</span><span class="sxs-lookup"><span data-stu-id="5f326-105">With the introduction of PowerShell classes in Windows PowerShell 5.0, you can now define a DSC resource by creating a class.</span></span> <span data-ttu-id="5f326-106">Az osztály a séma- és az erőforrás végrehajtásának határozza meg, így nincs szükség külön MOF-fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="5f326-106">The class defines both the schema and the implementation of the resource, so there is no need to create a separate MOF file.</span></span> <span data-ttu-id="5f326-107">A gyökérmappa-szerkezetében osztály-alapú erőforrásokhoz is felügyelete egyszerűbb, mert egy **DSCResources** mappa nincs szükség.</span><span class="sxs-lookup"><span data-stu-id="5f326-107">The folder structure for a class-based resource is also simpler, because a **DSCResources** folder is not necessary.</span></span>

<span data-ttu-id="5f326-108">Osztály-alapú DSC az erőforrás a séma van definiálva, amely attribútumokkal megadhatja a tulajdonság módosítható-osztály tulajdonságai...</span><span class="sxs-lookup"><span data-stu-id="5f326-108">In a class-based DSC resource, the schema is defined as properties of the class which can be modified with attributes to specify the property type..</span></span> <span data-ttu-id="5f326-109">Az erőforrás megvalósítja **Get()**, **set() metódust**, és **Test()** módszerek (egyenértékű a **Get-TargetResource**, **Set-TargetResource**, és **teszt-TargetResource** funkciók a parancsprogram-erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="5f326-109">The resource is implemented by **Get()**, **Set()**, and **Test()** methods (equivalent to the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions in a script resource.</span></span>

<span data-ttu-id="5f326-110">Ebben a témakörben létrehozunk egy egyszerű nevű erőforrás **FileResource** , amely kezeli a fájl a megadott elérési úton.</span><span class="sxs-lookup"><span data-stu-id="5f326-110">In this topic, we will create a simple resource named **FileResource** that manages a file in a specified path.</span></span>

<span data-ttu-id="5f326-111">A DSC-erőforrásokra vonatkozó további információkért lásd: [Build egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások](authoringResource.md)</span><span class="sxs-lookup"><span data-stu-id="5f326-111">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md)</span></span>

><span data-ttu-id="5f326-112">**Megjegyzés:** általános gyűjtemények osztály fájlalapú erőforrások – használata nem támogatott.</span><span class="sxs-lookup"><span data-stu-id="5f326-112">**Note:** Generic collections are not supported in class-based resources.</span></span>

## <a name="folder-structure-for-a-class-resource"></a><span data-ttu-id="5f326-113">Egy osztály erőforrás mappaszerkezet</span><span class="sxs-lookup"><span data-stu-id="5f326-113">Folder structure for a class resource</span></span>

<span data-ttu-id="5f326-114">Egyéni DSC-erőforrás PowerShell osztállyal alkalmazásához hozzon létre a következő mappaszerkezetet.</span><span class="sxs-lookup"><span data-stu-id="5f326-114">To implement a DSC custom resource with a PowerShell class, create the following folder structure.</span></span> <span data-ttu-id="5f326-115">Az osztály definiálva van **MyDscResource.psm1** , és a moduljegyzékben meghatározva **MyDscResource.psd1**.</span><span class="sxs-lookup"><span data-stu-id="5f326-115">The class is defined in **MyDscResource.psm1** and the module manifest is defined in **MyDscResource.psd1**.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1 
           MyDscResource.psd1 
```

## <a name="create-the-class"></a><span data-ttu-id="5f326-116">Az osztály létrehozásához</span><span class="sxs-lookup"><span data-stu-id="5f326-116">Create the class</span></span>

<span data-ttu-id="5f326-117">Az osztály kulcsszó használatával hozzon létre egy PowerShell-osztályt.</span><span class="sxs-lookup"><span data-stu-id="5f326-117">You use the class keyword to create a PowerShell class.</span></span> <span data-ttu-id="5f326-118">Adja meg, hogy egy osztály DSC erőforrás, használja a **DscResource()** attribútum.</span><span class="sxs-lookup"><span data-stu-id="5f326-118">To specify that a class is a DSC resource, use the **DscResource()** attribute.</span></span> <span data-ttu-id="5f326-119">Az osztály nevét a DSC-erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="5f326-119">The name of the class is the name of the DSC resource.</span></span>

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a><span data-ttu-id="5f326-120">Deklarálja tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="5f326-120">Declare properties</span></span>

<span data-ttu-id="5f326-121">A DSC-erőforrás séma a osztály tulajdonságai típusúként van definiálva.</span><span class="sxs-lookup"><span data-stu-id="5f326-121">The DSC resource schema is defined as properties of the class.</span></span> <span data-ttu-id="5f326-122">Az alábbiak szerint deklarálja azt három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="5f326-122">We declare three properties as follows.</span></span>

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

<span data-ttu-id="5f326-123">Figyelje meg, hogy a tulajdonság módosítását mutatjuk be attribútumok szerint.</span><span class="sxs-lookup"><span data-stu-id="5f326-123">Notice that the properties are modified by attributes.</span></span> <span data-ttu-id="5f326-124">Az attribútumok szerinti a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="5f326-124">The meaning of the attributes is as follows:</span></span>

- <span data-ttu-id="5f326-125">**DscProperty(Key)**: A tulajdonságra szükség.</span><span class="sxs-lookup"><span data-stu-id="5f326-125">**DscProperty(Key)**: The property is required.</span></span> <span data-ttu-id="5f326-126">A tulajdonság egy kulcsot.</span><span class="sxs-lookup"><span data-stu-id="5f326-126">The property is a key.</span></span> <span data-ttu-id="5f326-127">Az összes tulajdonság értékének megjelölt kulcsok kell alakítania egy erőforráspéldány konfiguráció belül egyedi azonosításához.</span><span class="sxs-lookup"><span data-stu-id="5f326-127">The values of all properties marked as keys must combine to uniquely identify a resource instance within a configuration.</span></span>
- <span data-ttu-id="5f326-128">**DscProperty(Mandatory)**: A tulajdonságra szükség.</span><span class="sxs-lookup"><span data-stu-id="5f326-128">**DscProperty(Mandatory)**: The property is required.</span></span>
- <span data-ttu-id="5f326-129">**DscProperty(NotConfigurable)**: A tulajdonság csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="5f326-129">**DscProperty(NotConfigurable)**: The property is read-only.</span></span> <span data-ttu-id="5f326-130">Ez attribútummal rendelkező tulajdonságok nem állíthatják be a konfigurációs, de által a rendszer feltölti a **Get()** metódust, ha létezik.</span><span class="sxs-lookup"><span data-stu-id="5f326-130">Properties marked with this attribute cannot be set by a configuration, but are populated by the **Get()** method when present.</span></span>
- <span data-ttu-id="5f326-131">**DscProperty()**: A tulajdonság konfigurálható, de nincs rá szükség.</span><span class="sxs-lookup"><span data-stu-id="5f326-131">**DscProperty()**: The property is configurable, but it is not required.</span></span>

<span data-ttu-id="5f326-132">A **$Path** és **$SourcePath** tulajdonságainak mindkét karakterláncot.</span><span class="sxs-lookup"><span data-stu-id="5f326-132">The **$Path** and **$SourcePath** properties are both strings.</span></span> <span data-ttu-id="5f326-133">A **$CreationTime** van egy [DateTime](https://technet.microsoft.com/en-us/library/system.datetime.aspx) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="5f326-133">The **$CreationTime** is a [DateTime](https://technet.microsoft.com/en-us/library/system.datetime.aspx) property.</span></span> <span data-ttu-id="5f326-134">A **$Ensure** tulajdonsága egy számbavételi típus, az alábbiak szerint definiáltuk.</span><span class="sxs-lookup"><span data-stu-id="5f326-134">The **$Ensure** property is an enumeration type, defined as follows.</span></span>

```powershell
enum Ensure 
{ 
    Absent 
    Present 
}
```

### <a name="implementing-the-methods"></a><span data-ttu-id="5f326-135">Az eljárások végrehajtása</span><span class="sxs-lookup"><span data-stu-id="5f326-135">Implementing the methods</span></span>

<span data-ttu-id="5f326-136">A **Get()**, **set() metódust**, és **Test()** módszerrel is hasonló a **Get-TargetResource**, **Set-TargetResource** , és **teszt-TargetResource** funkciók a parancsprogram-erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="5f326-136">The **Get()**, **Set()**, and **Test()** methods are analogous to the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions in a script resource.</span></span>

<span data-ttu-id="5f326-137">Ezt a kódot is magában foglalja a CopyFile() függvény, másolja át a fájlt a segítő függvény **$SourcePath** való **$Path**.</span><span class="sxs-lookup"><span data-stu-id="5f326-137">This code also includes the CopyFile() function, a helper function that copies the file from **$SourcePath** to **$Path**.</span></span> 

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

### <a name="the-complete-file"></a><span data-ttu-id="5f326-138">A teljes fájl</span><span class="sxs-lookup"><span data-stu-id="5f326-138">The complete file</span></span>
<span data-ttu-id="5f326-139">A teljes osztály fájl követi.</span><span class="sxs-lookup"><span data-stu-id="5f326-139">The complete class file follows.</span></span>

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


## <a name="create-a-manifest"></a><span data-ttu-id="5f326-140">A jegyzékfájl létrehozása</span><span class="sxs-lookup"><span data-stu-id="5f326-140">Create a manifest</span></span>

<span data-ttu-id="5f326-141">A DSC-motor elérhetővé tegyen egy osztály-alapú erőforrás, akkor tartalmaznia kell egy **DscResourcesToExport** kivonat a jegyzékfájlban, amely arra utasítja az erőforrás exportálandó modul.</span><span class="sxs-lookup"><span data-stu-id="5f326-141">To make a class-based resource available to the DSC engine, you must include a **DscResourcesToExport** statement in the manifest file that instructs the module to export the resource.</span></span> <span data-ttu-id="5f326-142">A jegyzékfájl így néz ki:</span><span class="sxs-lookup"><span data-stu-id="5f326-142">Our manifest looks like this:</span></span>

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

## <a name="test-the-resource"></a><span data-ttu-id="5f326-143">Az erőforrás tesztelése</span><span class="sxs-lookup"><span data-stu-id="5f326-143">Test the resource</span></span>

<span data-ttu-id="5f326-144">Miután az osztály és a jegyzékfájlt a a mappastruktúra a fentebb leírt módon, az új erőforrás használó konfiguráció is létrehozhat.</span><span class="sxs-lookup"><span data-stu-id="5f326-144">After saving the class and manifest files in the folder structure as described earlier, you can create a configuration that uses the new resource.</span></span> <span data-ttu-id="5f326-145">A DSC-konfiguráció futtatásával kapcsolatos információkért lásd: [konfigurációk hozzanak](enactingConfigurations.md).</span><span class="sxs-lookup"><span data-stu-id="5f326-145">For information about how to run a DSC configuration, see [Enacting configurations](enactingConfigurations.md).</span></span> <span data-ttu-id="5f326-146">A következő konfigurációs ellenőrzi, hogy a fájlban a következő `c:\test\test.txt` létezik, és ha nem, másolja át a fájlt a `c:\test.txt` (létre kell hoznia `c:\test.txt` a konfiguráció futtatása előtt).</span><span class="sxs-lookup"><span data-stu-id="5f326-146">The following configuration will check to see whether the file at `c:\test\test.txt` exists, and, if not, copies the file from `c:\test.txt` (you should create `c:\test.txt` before you run the configuration).</span></span>

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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="5f326-147">PsDscRunAsCredential támogatása</span><span class="sxs-lookup"><span data-stu-id="5f326-147">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="5f326-148">**Megjegyzés:** **PsDscRunAsCredential** PowerShell 5.0-s vagy újabb támogatott.</span><span class="sxs-lookup"><span data-stu-id="5f326-148">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="5f326-149">A **PsDscRunAsCredential** tulajdonság használható [a DSC-konfigurációk](configurations.md) erőforrás blokk adhatja meg, hogy az erőforrás verziója alatt kell futtatni a megadott hitelesítő adatok készletét.</span><span class="sxs-lookup"><span data-stu-id="5f326-149">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="5f326-150">További információkért lásd: [felhasználói hitelesítő adatokkal rendelkező futtató DSC](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="5f326-150">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a><span data-ttu-id="5f326-151">Szükséges, vagy az erőforrás PsDscRunAsCredential letiltása</span><span class="sxs-lookup"><span data-stu-id="5f326-151">Require or disallow PsDscRunAsCredential for your resource</span></span>

<span data-ttu-id="5f326-152">A **DscResource()** attribútum egy választható paramétert fogad, **RunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="5f326-152">The **DscResource()** attribute takes an optional parameter **RunAsCredential**.</span></span>
<span data-ttu-id="5f326-153">Ezt a paramétert értékek egyike szükséges:</span><span class="sxs-lookup"><span data-stu-id="5f326-153">This parameter takes one of three values:</span></span>

- <span data-ttu-id="5f326-154">`Optional`**PsDscRunAsCredential** nem kötelező konfigurációk, amelyek ehhez az erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="5f326-154">`Optional` **PsDscRunAsCredential** is optional for configurations that call this resource.</span></span> <span data-ttu-id="5f326-155">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="5f326-155">This is the default value.</span></span>
- <span data-ttu-id="5f326-156">`Mandatory`**PsDscRunAsCredential** , amely behívja ehhez az erőforráshoz konfigurálni kell használni.</span><span class="sxs-lookup"><span data-stu-id="5f326-156">`Mandatory` **PsDscRunAsCredential** must be used for any configuration that calls this resource.</span></span>
- <span data-ttu-id="5f326-157">`NotSupported`Ehhez az erőforráshoz hívó konfigurációk nem használható **PsDscRunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="5f326-157">`NotSupported` Configurations that call this resource cannot use **PsDscRunAsCredential**.</span></span>
- <span data-ttu-id="5f326-158">`Default`Ugyanaz, mint a `Optional`.</span><span class="sxs-lookup"><span data-stu-id="5f326-158">`Default` Same as `Optional`.</span></span>

<span data-ttu-id="5f326-159">Például adja meg, hogy az egyéni erőforrás nem támogatja a következő attribútum segítségével **PsDscRunAsCredential**:</span><span class="sxs-lookup"><span data-stu-id="5f326-159">For example, use the following attribute to specify that your custom resource does not support using **PsDscRunAsCredential**:</span></span>

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a><span data-ttu-id="5f326-160">Hozzáférés a felhasználói környezet</span><span class="sxs-lookup"><span data-stu-id="5f326-160">Access the user context</span></span>

<span data-ttu-id="5f326-161">A felhasználói környezet belül egyéni erőforrás eléréséhez használhatja az automatikus változó `$global:PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="5f326-161">To access the user context from within a custom resource, you can use the automatic variable `$global:PsDscContext`.</span></span>

<span data-ttu-id="5f326-162">Például a következő kódot a felhasználói környezet, amely alatt az erőforrás fut, a részletes kimeneti adatfolyamba lesz írási:</span><span class="sxs-lookup"><span data-stu-id="5f326-162">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="5f326-163">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5f326-163">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="5f326-164">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="5f326-164">Concepts</span></span>
[<span data-ttu-id="5f326-165">Egyéni Windows PowerShell kívánt állapot konfigurációs erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="5f326-165">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

