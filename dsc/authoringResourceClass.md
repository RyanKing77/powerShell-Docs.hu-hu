---
ms.date: 06/12/2017
keywords: DSC, powershell, a konfigurációt, a beállítása
title: A PowerShell-osztályok egyéni DSC-erőforrás írása
ms.openlocfilehash: a8f08323f2cced8a17de4224bea94a54ba5ef0cd
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50226083"
---
# <a name="writing-a-custom-dsc-resource-with-powershell-classes"></a><span data-ttu-id="3bb75-103">A PowerShell-osztályok egyéni DSC-erőforrás írása</span><span class="sxs-lookup"><span data-stu-id="3bb75-103">Writing a custom DSC resource with PowerShell classes</span></span>

> <span data-ttu-id="3bb75-104">A következőkre vonatkozik: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="3bb75-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="3bb75-105">PowerShell-osztályok a Windows PowerShell 5.0 bevezetésével most már megadhatja a DSC-erőforrás osztály létrehozásával.</span><span class="sxs-lookup"><span data-stu-id="3bb75-105">With the introduction of PowerShell classes in Windows PowerShell 5.0, you can now define a DSC resource by creating a class.</span></span> <span data-ttu-id="3bb75-106">Az osztály a séma- és az erőforrás végrehajtásának határozza meg, így nem kell külön MOF-fájl létrehozásához.</span><span class="sxs-lookup"><span data-stu-id="3bb75-106">The class defines both the schema and the implementation of the resource, so there is no need to create a separate MOF file.</span></span> <span data-ttu-id="3bb75-107">A gyökérmappa-szerkezetében osztályalapú erőforrás egyben egyszerűbb, mivel egy **DSCResources** mappa már nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="3bb75-107">The folder structure for a class-based resource is also simpler, because a **DSCResources** folder is not necessary.</span></span>

<span data-ttu-id="3bb75-108">Osztályalapú DSC erőforrás a séma számít, ha az osztály, amely attribútumait megadhatja a tulajdonság módosítható tulajdonságai...</span><span class="sxs-lookup"><span data-stu-id="3bb75-108">In a class-based DSC resource, the schema is defined as properties of the class which can be modified with attributes to specify the property type..</span></span> <span data-ttu-id="3bb75-109">Az erőforrás valósít meg **Get()**, **Set()**, és **Test()** metódusok (egyenértékű a **Get-TargetResource**, **Set-TargetResource**, és **Test-TargetResource** függvények a parancsfájl erőforrást.</span><span class="sxs-lookup"><span data-stu-id="3bb75-109">The resource is implemented by **Get()**, **Set()**, and **Test()** methods (equivalent to the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions in a script resource.</span></span>

<span data-ttu-id="3bb75-110">Ebben a témakörben egy egyszerű erőforrás nevű hozunk létre **FileResource** , amely kezeli a megadott elérési út egy fájlt.</span><span class="sxs-lookup"><span data-stu-id="3bb75-110">In this topic, we will create a simple resource named **FileResource** that manages a file in a specified path.</span></span>

<span data-ttu-id="3bb75-111">DSC-erőforrások kapcsolatos további információkért lásd: [hozhat létre egyéni Windows PowerShell Desired State Configuration erőforrások](authoringResource.md)</span><span class="sxs-lookup"><span data-stu-id="3bb75-111">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md)</span></span>

><span data-ttu-id="3bb75-112">**Megjegyzés:** általános gyűjtemények nem támogatottak az osztály-alapú erőforrások.</span><span class="sxs-lookup"><span data-stu-id="3bb75-112">**Note:** Generic collections are not supported in class-based resources.</span></span>

## <a name="folder-structure-for-a-class-resource"></a><span data-ttu-id="3bb75-113">A mappastruktúra osztály erőforrás</span><span class="sxs-lookup"><span data-stu-id="3bb75-113">Folder structure for a class resource</span></span>

<span data-ttu-id="3bb75-114">Egy olyan PowerShell osztállyal DSC egyéni erőforrás implementálásához hozzon létre a következő mappaszerkezetet.</span><span class="sxs-lookup"><span data-stu-id="3bb75-114">To implement a DSC custom resource with a PowerShell class, create the following folder structure.</span></span> <span data-ttu-id="3bb75-115">Az osztály definiálva van **MyDscResource.psm1** , és a moduljegyzékben meghatározva **MyDscResource.psd1**.</span><span class="sxs-lookup"><span data-stu-id="3bb75-115">The class is defined in **MyDscResource.psm1** and the module manifest is defined in **MyDscResource.psd1**.</span></span>

```
$env:ProgramFiles\WindowsPowerShell\Modules (folder)
    |- MyDscResource (folder)
        |- MyDscResource.psm1
           MyDscResource.psd1
```

## <a name="create-the-class"></a><span data-ttu-id="3bb75-116">Az osztály létrehozása</span><span class="sxs-lookup"><span data-stu-id="3bb75-116">Create the class</span></span>

<span data-ttu-id="3bb75-117">Az osztály kulcsszó használatával hozzon létre egy PowerShell-osztályt.</span><span class="sxs-lookup"><span data-stu-id="3bb75-117">You use the class keyword to create a PowerShell class.</span></span> <span data-ttu-id="3bb75-118">Adja meg, hogy egy osztály a DSC-erőforrás, használja a **DscResource()** attribútum.</span><span class="sxs-lookup"><span data-stu-id="3bb75-118">To specify that a class is a DSC resource, use the **DscResource()** attribute.</span></span> <span data-ttu-id="3bb75-119">Az osztály nevét a DSC-erőforrás neve.</span><span class="sxs-lookup"><span data-stu-id="3bb75-119">The name of the class is the name of the DSC resource.</span></span>

```powershell
[DscResource()]
class FileResource {
}
```

### <a name="declare-properties"></a><span data-ttu-id="3bb75-120">Deklarálja a tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="3bb75-120">Declare properties</span></span>

<span data-ttu-id="3bb75-121">A DSC-erőforrás séma számít, ha az osztály tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="3bb75-121">The DSC resource schema is defined as properties of the class.</span></span> <span data-ttu-id="3bb75-122">A következő azt deklarálja három tulajdonságot.</span><span class="sxs-lookup"><span data-stu-id="3bb75-122">We declare three properties as follows.</span></span>

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

<span data-ttu-id="3bb75-123">Figyelje meg, hogy a Tulajdonságok attribútumok szerint módosítják.</span><span class="sxs-lookup"><span data-stu-id="3bb75-123">Notice that the properties are modified by attributes.</span></span> <span data-ttu-id="3bb75-124">Az attribútumok értelmében a következőképpen történik:</span><span class="sxs-lookup"><span data-stu-id="3bb75-124">The meaning of the attributes is as follows:</span></span>

- <span data-ttu-id="3bb75-125">**DscProperty(Key)**: A tulajdonság megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="3bb75-125">**DscProperty(Key)**: The property is required.</span></span> <span data-ttu-id="3bb75-126">A tulajdonság egy kulcsot.</span><span class="sxs-lookup"><span data-stu-id="3bb75-126">The property is a key.</span></span> <span data-ttu-id="3bb75-127">Kulcsok belül egy konfigurációs egy erőforrás-példány egyedi azonosításához kell alakítania megjelölt összes tulajdonságának értékét.</span><span class="sxs-lookup"><span data-stu-id="3bb75-127">The values of all properties marked as keys must combine to uniquely identify a resource instance within a configuration.</span></span>
- <span data-ttu-id="3bb75-128">**DscProperty(Mandatory)**: A tulajdonság megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="3bb75-128">**DscProperty(Mandatory)**: The property is required.</span></span>
- <span data-ttu-id="3bb75-129">**DscProperty(NotConfigurable)**: A tulajdonság csak olvasható.</span><span class="sxs-lookup"><span data-stu-id="3bb75-129">**DscProperty(NotConfigurable)**: The property is read-only.</span></span> <span data-ttu-id="3bb75-130">Ez attribútummal rendelkező tulajdonságok nem állítható be a konfiguráció, de által fel van töltve a **Get()** módszer, ha a jelen.</span><span class="sxs-lookup"><span data-stu-id="3bb75-130">Properties marked with this attribute cannot be set by a configuration, but are populated by the **Get()** method when present.</span></span>
- <span data-ttu-id="3bb75-131">**DscProperty()**: A tulajdonság konfigurálható, de ez nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3bb75-131">**DscProperty()**: The property is configurable, but it is not required.</span></span>

<span data-ttu-id="3bb75-132">A **$Path** és **$SourcePath** tulajdonságok a következők mindkét karakterláncokat.</span><span class="sxs-lookup"><span data-stu-id="3bb75-132">The **$Path** and **$SourcePath** properties are both strings.</span></span> <span data-ttu-id="3bb75-133">A **$CreationTime** van egy [DateTime](https://technet.microsoft.com/library/system.datetime.aspx) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3bb75-133">The **$CreationTime** is a [DateTime](https://technet.microsoft.com/library/system.datetime.aspx) property.</span></span> <span data-ttu-id="3bb75-134">A **$Ensure** tulajdonság meghatározása a következő enumerálási típusát.</span><span class="sxs-lookup"><span data-stu-id="3bb75-134">The **$Ensure** property is an enumeration type, defined as follows.</span></span>

```powershell
enum Ensure
{
    Absent
    Present
}
```

### <a name="implementing-the-methods"></a><span data-ttu-id="3bb75-135">A metódusok végrehajtása</span><span class="sxs-lookup"><span data-stu-id="3bb75-135">Implementing the methods</span></span>

<span data-ttu-id="3bb75-136">A **Get()**, **Set()**, és **Test()** módszerek a következők csatlakoztatja a **Get-TargetResource**, **Set-TargetResource** , és **Test-TargetResource** függvények a parancsfájl erőforrást.</span><span class="sxs-lookup"><span data-stu-id="3bb75-136">The **Get()**, **Set()**, and **Test()** methods are analogous to the **Get-TargetResource**, **Set-TargetResource**, and **Test-TargetResource** functions in a script resource.</span></span>

<span data-ttu-id="3bb75-137">Ez a kód is magában foglalja a CopyFile() függvény segítő függvény, amely átmásolja a fájlt a **$SourcePath** való **$Path**.</span><span class="sxs-lookup"><span data-stu-id="3bb75-137">This code also includes the CopyFile() function, a helper function that copies the file from **$SourcePath** to **$Path**.</span></span>

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

### <a name="the-complete-file"></a><span data-ttu-id="3bb75-138">A teljes fájl</span><span class="sxs-lookup"><span data-stu-id="3bb75-138">The complete file</span></span>
<span data-ttu-id="3bb75-139">A teljes fájl követi.</span><span class="sxs-lookup"><span data-stu-id="3bb75-139">The complete class file follows.</span></span>

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


## <a name="create-a-manifest"></a><span data-ttu-id="3bb75-140">Jegyzék létrehozásához</span><span class="sxs-lookup"><span data-stu-id="3bb75-140">Create a manifest</span></span>

<span data-ttu-id="3bb75-141">Osztályalapú erőforrás akkor válik elérhetővé a DSC motor, meg kell adni egy **DscResourcesToExport** utasítás, amely arra utasítja a modult, exportálhatja az erőforrás-jegyzékfájl.</span><span class="sxs-lookup"><span data-stu-id="3bb75-141">To make a class-based resource available to the DSC engine, you must include a **DscResourcesToExport** statement in the manifest file that instructs the module to export the resource.</span></span> <span data-ttu-id="3bb75-142">A jegyzékfájl így néz ki:</span><span class="sxs-lookup"><span data-stu-id="3bb75-142">Our manifest looks like this:</span></span>

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

## <a name="test-the-resource"></a><span data-ttu-id="3bb75-143">Az erőforrás tesztelése</span><span class="sxs-lookup"><span data-stu-id="3bb75-143">Test the resource</span></span>

<span data-ttu-id="3bb75-144">Az osztály és fájlok mentése a korábban leírtaknak megfelelően a gyökérmappa-szerkezetében lévő, után az új erőforrás használó konfiguráció is létrehozhat.</span><span class="sxs-lookup"><span data-stu-id="3bb75-144">After saving the class and manifest files in the folder structure as described earlier, you can create a configuration that uses the new resource.</span></span> <span data-ttu-id="3bb75-145">A DSC-konfiguráció futtatásával kapcsolatos további információkért lásd: [konfigurációk életbe léptetése](enactingConfigurations.md).</span><span class="sxs-lookup"><span data-stu-id="3bb75-145">For information about how to run a DSC configuration, see [Enacting configurations](enactingConfigurations.md).</span></span> <span data-ttu-id="3bb75-146">A következő konfigurációt ellenőrzi, hogy a fájlban a következő `c:\test\test.txt` létezik, és ha nem, másolja át a fájlt a `c:\test.txt` (hozzon létre `c:\test.txt` a konfiguráció futtatása előtt).</span><span class="sxs-lookup"><span data-stu-id="3bb75-146">The following configuration will check to see whether the file at `c:\test\test.txt` exists, and, if not, copies the file from `c:\test.txt` (you should create `c:\test.txt` before you run the configuration).</span></span>

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

## <a name="supporting-psdscrunascredential"></a><span data-ttu-id="3bb75-147">PsDscRunAsCredential támogatása</span><span class="sxs-lookup"><span data-stu-id="3bb75-147">Supporting PsDscRunAsCredential</span></span>

><span data-ttu-id="3bb75-148">**Megjegyzés:** **PsDscRunAsCredential** a PowerShell 5.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="3bb75-148">**Note:** **PsDscRunAsCredential** is supported in PowerShell 5.0 and later.</span></span>

<span data-ttu-id="3bb75-149">A **PsDscRunAsCredential** tulajdonság használható [DSC-konfigurációk](configurations.md) erőforrás letiltása, hogy az erőforrás alatt kell futtatni. egy meghatározott hitelesítő adatok megadásához.</span><span class="sxs-lookup"><span data-stu-id="3bb75-149">The **PsDscRunAsCredential** property can be used in [DSC configurations](configurations.md) resource block to specify that the resource should be run under a specified set of credentials.</span></span>
<span data-ttu-id="3bb75-150">További információkért lásd: [DSC futtatása felhasználói hitelesítő adatokkal](runAsUser.md).</span><span class="sxs-lookup"><span data-stu-id="3bb75-150">For more information, see [Running DSC with user credentials](runAsUser.md).</span></span>

### <a name="require-or-disallow-psdscrunascredential-for-your-resource"></a><span data-ttu-id="3bb75-151">Szükséges, vagy az erőforrás PsDscRunAsCredential letiltása</span><span class="sxs-lookup"><span data-stu-id="3bb75-151">Require or disallow PsDscRunAsCredential for your resource</span></span>

<span data-ttu-id="3bb75-152">A **DscResource()** attribútumot vesz igénybe egy nem kötelező paraméter **RunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="3bb75-152">The **DscResource()** attribute takes an optional parameter **RunAsCredential**.</span></span>
<span data-ttu-id="3bb75-153">Ez a paraméter három érték egyikét veheti fel:</span><span class="sxs-lookup"><span data-stu-id="3bb75-153">This parameter takes one of three values:</span></span>

- <span data-ttu-id="3bb75-154">`Optional` **PsDscRunAsCredential** nem kötelező konfigurációk, amelyek meg az ehhez az erőforráshoz.</span><span class="sxs-lookup"><span data-stu-id="3bb75-154">`Optional` **PsDscRunAsCredential** is optional for configurations that call this resource.</span></span> <span data-ttu-id="3bb75-155">Ez az alapértelmezett érték.</span><span class="sxs-lookup"><span data-stu-id="3bb75-155">This is the default value.</span></span>
- <span data-ttu-id="3bb75-156">`Mandatory` **PsDscRunAsCredential** kell használni minden olyan konfiguráció, amely meghívja ezt az erőforrást.</span><span class="sxs-lookup"><span data-stu-id="3bb75-156">`Mandatory` **PsDscRunAsCredential** must be used for any configuration that calls this resource.</span></span>
- <span data-ttu-id="3bb75-157">`NotSupported` Konfigurációk, amelyek meg az ehhez az erőforráshoz nem használható **PsDscRunAsCredential**.</span><span class="sxs-lookup"><span data-stu-id="3bb75-157">`NotSupported` Configurations that call this resource cannot use **PsDscRunAsCredential**.</span></span>
- <span data-ttu-id="3bb75-158">`Default` Ugyanaz, mint a `Optional`.</span><span class="sxs-lookup"><span data-stu-id="3bb75-158">`Default` Same as `Optional`.</span></span>

<span data-ttu-id="3bb75-159">Például adja meg, hogy az egyéni erőforrás nem támogatja a következő attribútum segítségével **PsDscRunAsCredential**:</span><span class="sxs-lookup"><span data-stu-id="3bb75-159">For example, use the following attribute to specify that your custom resource does not support using **PsDscRunAsCredential**:</span></span>

```powershell
[DscResource(RunAsCredential=NotSupported)]
class FileResource {
}
```

### <a name="access-the-user-context"></a><span data-ttu-id="3bb75-160">Hozzáférés a felhasználói környezet</span><span class="sxs-lookup"><span data-stu-id="3bb75-160">Access the user context</span></span>

<span data-ttu-id="3bb75-161">A felhasználói környezet belül egy egyéni erőforrás elérésére, használhatja az automatikus változót `$global:PsDscContext`.</span><span class="sxs-lookup"><span data-stu-id="3bb75-161">To access the user context from within a custom resource, you can use the automatic variable `$global:PsDscContext`.</span></span>

<span data-ttu-id="3bb75-162">Például a következő kódot a felhasználói környezet, amelyben az erőforrás fut. a részletes kimeneti adatfolyamba volna írni:</span><span class="sxs-lookup"><span data-stu-id="3bb75-162">For example the following code would write the user context under which the resource is running to the verbose output stream:</span></span>

```powershell
if (PsDscContext.RunAsUser) {
    Write-Verbose "User: $global:PsDscContext.RunAsUser";
}
```

## <a name="see-also"></a><span data-ttu-id="3bb75-163">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3bb75-163">See Also</span></span>
### <a name="concepts"></a><span data-ttu-id="3bb75-164">Fogalmak</span><span class="sxs-lookup"><span data-stu-id="3bb75-164">Concepts</span></span>
[<span data-ttu-id="3bb75-165">Egyéni Windows PowerShell Desired State Configuration erőforrások létrehozása</span><span class="sxs-lookup"><span data-stu-id="3bb75-165">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)