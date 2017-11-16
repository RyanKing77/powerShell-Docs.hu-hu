---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: Install-modul
ms.openlocfilehash: 37e07cd32e7b2fd4a7a8e6cab179aecc3251baf3
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="install-module"></a><span data-ttu-id="94f69-103">Install-modul</span><span class="sxs-lookup"><span data-stu-id="94f69-103">Install-Module</span></span>

<span data-ttu-id="94f69-104">Online tárházak találhatók a helyi számítógépre a PowerShell-modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="94f69-104">Installs the PowerShell modules from online repositories to the local computer.</span></span>

## <a name="description"></a><span data-ttu-id="94f69-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="94f69-105">Description</span></span>

<span data-ttu-id="94f69-106">Install-modul a parancsmag egy vagy több modulja letölti az online katalógusból, ellenőrzi, és telepíti azokat a helyi számítógépen a megadott telepítési hatókörbe.</span><span class="sxs-lookup"><span data-stu-id="94f69-106">Install-Module cmdlet downloads one or more modules from an online gallery, validates and installs them on the local computer to the specified installation scope.</span></span>

<span data-ttu-id="94f69-107">Az Install-modul a parancsmag lekérdezi az online katalógusból megadott feltételeknek, egy vagy több modulja, ellenőrzi, hogy a keresési eredmények között érvényes modulok és a telepítési helyre másolja modul mappák.</span><span class="sxs-lookup"><span data-stu-id="94f69-107">The Install-Module cmdlet gets one or more modules that meet specified criteria from an online gallery, verifies that search results are valid modules, and copies module folders to the installation location.</span></span>

<span data-ttu-id="94f69-108">Nincs hatóköre van definiálva, vagy ha a hatókör-paraméter értéke az AllUsers tulajdonság, a modul %systemdrive%:\Program Files\WindowsPowerShell\Modules van telepítve.</span><span class="sxs-lookup"><span data-stu-id="94f69-108">When no scope is defined, or when the value of the Scope parameter is AllUsers, the module is installed to %systemdrive%:\Program Files\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="94f69-109">CurrentUser hatókör érték esetén a modul $home\Documents\WindowsPowerShell\Modules van telepítve.</span><span class="sxs-lookup"><span data-stu-id="94f69-109">When the value of Scope is CurrentUser, the module is installed to $home\Documents\WindowsPowerShell\Modules.</span></span>

<span data-ttu-id="94f69-110">A megadott modulokban minimális és a pontos verzióit eredmény végezhet.</span><span class="sxs-lookup"><span data-stu-id="94f69-110">You can filter your results based on minimum and exact versions of specified modules.</span></span>

- <span data-ttu-id="94f69-111">Egymás melletti verzióinak támogatása a Windows PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="94f69-111">Side-by-side version support on Windows PowerShell 5.0 or newer</span></span>
- <span data-ttu-id="94f69-112">A modul függőségi telepítés támogatása</span><span class="sxs-lookup"><span data-stu-id="94f69-112">Module dependency installation support</span></span>
- <span data-ttu-id="94f69-113">**Nem megbízható a parancssorból:**felhasználói elfogadás kell a modulok telepítése egy nem megbízható tárházból.</span><span class="sxs-lookup"><span data-stu-id="94f69-113">**Untrusted prompt:**User acceptance is required for installing the modules from an untrusted repository.</span></span>
- <span data-ttu-id="94f69-114">-Force újratelepíti a telepített modul</span><span class="sxs-lookup"><span data-stu-id="94f69-114">-Force reinstalls the installed module</span></span>
- <span data-ttu-id="94f69-115">RequiredVersion SxS PowerShell 5.0-s vagy újabb verziója a meglévő verzióival meghatározott verzióját telepíti.</span><span class="sxs-lookup"><span data-stu-id="94f69-115">RequiredVersion installs the specified version in SxS with existing versions on PowerShell version 5.0 or newer.</span></span>

### <a name="scope"></a><span data-ttu-id="94f69-116">Hatókör</span><span class="sxs-lookup"><span data-stu-id="94f69-116">Scope</span></span>
<span data-ttu-id="94f69-117">Adja meg a telepítést a modul hatókörében.</span><span class="sxs-lookup"><span data-stu-id="94f69-117">Specifies the installation scope of the module.</span></span> <span data-ttu-id="94f69-118">Ez a paraméter elfogadható értékek a következők: AllUsers és CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="94f69-118">The acceptable values for this parameter are: AllUsers and CurrentUser.</span></span>

<span data-ttu-id="94f69-119">Az alapértelmezett telepítési hatóköre az AllUsers tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="94f69-119">The default installation scope is AllUsers.</span></span>

<span data-ttu-id="94f69-120">Az AllUsers tulajdonság hatóköre lehetővé teszi, hogy a modulokat telepíteni, egy olyan helyre, ez azt jelenti, hogy a számítógép összes felhasználója számára elérhető "$env: SystemDrive\Program Files\WindowsPowerShell\Modules".</span><span class="sxs-lookup"><span data-stu-id="94f69-120">The AllUsers scope lets modules be installed in a location that is accessible to all users of the computer, that is, "$env:SystemDrive\Program Files\WindowsPowerShell\Modules".</span></span>

<span data-ttu-id="94f69-121">A CurrentUser hatókör lehetővé teszi, hogy csak a "$home\Documents\WindowsPowerShell\Modules", telepíthető modulok úgy, hogy a modul csak az aktuális felhasználó számára elérhető.</span><span class="sxs-lookup"><span data-stu-id="94f69-121">The CurrentUser scope lets modules be installed only to "$home\Documents\WindowsPowerShell\Modules", so that the module is available only to the current user.</span></span>

## <a name="notes"></a><span data-ttu-id="94f69-122">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="94f69-122">Notes</span></span>

<span data-ttu-id="94f69-123">Ez a parancsmag a Windows PowerShell 3.0-s vagy újabb kiadásaiban a Windows PowerShell, a Windows 7 vagy Windows 2008 R2 és újabb Windows-verziókat futtatja.</span><span class="sxs-lookup"><span data-stu-id="94f69-123">This cmdlet runs on Windows PowerShell 3.0 or later releases of Windows PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>

<span data-ttu-id="94f69-124">Ha telepített modul nem importálható, (Ez azt jelenti, hogy ha egy .psm1, .psd1 vagy egy ugyanilyen nevű .dll nincs a mappában található), telepítés sikertelen lesz, kivéve, ha a Force paramétert a parancshoz adja hozzá.</span><span class="sxs-lookup"><span data-stu-id="94f69-124">If an installed module cannot be imported (that is, if it does not have a .psm1, .psd1, or .dll of the same name within the folder), installation fails unless you add the Force parameter to your command.</span></span>

<span data-ttu-id="94f69-125">Ha a modul azon a számítógépen egy verziója megegyezik a Name paraméter megadott értéke, és nem hozzáadta a MinimumVersion vagy RequiredVersion paraméter, Install-modul csendes továbbra is fennáll, hogy a modul telepítése nélkül.</span><span class="sxs-lookup"><span data-stu-id="94f69-125">If a version of the module on the computer matches the value specified for the Name parameter, and you have not added the MinimumVersion or RequiredVersion parameter, Install-Module silently continues without installing that module.</span></span> <span data-ttu-id="94f69-126">Ha a MinimumVersion vagy RequiredVersion paraméterek vannak megadva, és a meglévő modul nem felel meg, hogy a paraméter értékének, majd hiba lép fel.</span><span class="sxs-lookup"><span data-stu-id="94f69-126">If the MinimumVersion or RequiredVersion parameters are specified, and the existing module does not match the values in that parameter, then an error occurs.</span></span> <span data-ttu-id="94f69-127">Pontosabban: a jelenleg telepített modul verziószáma alacsonyabb, mint a MinimumVersion paraméter értékét, vagy a RequiredVersion paraméter értéke nem egyenlő, ha hiba lép fel.</span><span class="sxs-lookup"><span data-stu-id="94f69-127">To be more specific: if the version of the currently-installed module is either lower than the value of the MinimumVersion parameter, or not equal to the value of the RequiredVersion parameter, an error occurs.</span></span> <span data-ttu-id="94f69-128">Ha a telepített modul verziószáma nagyobb, mint a MinimumVersion paraméter értékét, vagy a RequiredVersion paraméter értékének egyenlőnek, Install-modul csendes továbbra is fennáll, hogy a modul telepítése nélkül.</span><span class="sxs-lookup"><span data-stu-id="94f69-128">If the version of the installed module is greater than the value of the MinimumVersion parameter, or equal to the value of the RequiredVersion parameter, Install-Module silently continues without installing that module.</span></span>

<span data-ttu-id="94f69-129">Install-modul hibát ad vissza, ha nincs modul az online katalógus, amely megfelel a megadott névvel már létezik.</span><span class="sxs-lookup"><span data-stu-id="94f69-129">Install-Module returns an error if no module exists in the online gallery that matches the specified name.</span></span>

<span data-ttu-id="94f69-130">Több modul telepítéséhez adja meg a modul neve vesszőkkel elválasztva tömbjét.</span><span class="sxs-lookup"><span data-stu-id="94f69-130">To install multiple modules, specify an array of the module names, separated by commas.</span></span> <span data-ttu-id="94f69-131">Nem adhat hozzá MinimumVersion vagy RequiredVersion Ha több modul nevet ad meg.</span><span class="sxs-lookup"><span data-stu-id="94f69-131">You cannot add MinimumVersion or RequiredVersion if you specify multiple module names.</span></span>

<span data-ttu-id="94f69-132">Alapértelmezés szerint a modulok telepítve vannak a Program Files mappába, problémák elkerülése érdekében a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások telepítése. Átadhatja az Install-modul; több PSGetItemInfo objektumok Ez az egyetlen parancs telepítésének megadásával több modul egy másik módja.</span><span class="sxs-lookup"><span data-stu-id="94f69-132">By default, modules are installed to the Program Files folder, to prevent confusion when you are installing Windows PowerShell Desired State Configuration (DSC) resources.You can pipe multiple PSGetItemInfo objects to Install-Module; this is another way of specifying multiple modules to install in a single command.</span></span>

<span data-ttu-id="94f69-133">Telepített rosszindulatú kódot tartalmazó futó modulok megelőzése érdekében rendszer nem automatikusan importálja a telepítés.</span><span class="sxs-lookup"><span data-stu-id="94f69-133">To help prevent running modules that contain malicious code, installed modules are not automatically imported by installation.</span></span> <span data-ttu-id="94f69-134">Biztonsági szempontból ajánlott, kiértékelése modul kód parancsmagok és függvények futtatása egy modulban először előtt.</span><span class="sxs-lookup"><span data-stu-id="94f69-134">As a security best practice, evaluate module code before running any cmdlets or functions in a module for the first time.</span></span>


## <a name="cmdlet-syntax"></a><span data-ttu-id="94f69-135">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="94f69-135">Cmdlet syntax</span></span>
```powershell
Get-Command -Name Install-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="94f69-136">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="94f69-136">Cmdlet online help reference</span></span>

[<span data-ttu-id="94f69-137">Install-modul</span><span class="sxs-lookup"><span data-stu-id="94f69-137">Install-Module</span></span>](http://go.microsoft.com/fwlink/?LinkID=398573)

## <a name="example-commands"></a><span data-ttu-id="94f69-138">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="94f69-138">Example commands</span></span>

```powershell

# Install a module by name
Install-Module -Name MyDscModule

# Install multiple modules
Install-Module ContosoClient,ContosoServer

# Install a module using its minimum version
Install-Module -Name ContosoServer -MinimumVersion 1.0

# Install a specific version of a module
Install-Module -Name ContosoServer -RequiredVersion 1.1.3

# Install the latest version of a module to $home\Documents\WindowsPowerShell\Modules.
Install-Module -Name ContosoServer -Scope CurrentUser

# if a module is already available under $env:PSModulePath, below command fails with 'ModuleAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Module ContosoServer -RequiredVersion 1.5

# if a module is already available under $env:PSModulePath, below command fails with 'ModuleAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Module ContosoServer -MinimumVersion 2.5

# Install multiple modules from multiple registered repositories
Install-Module ContosoClient,ContosoServer -Repository PSGallery, PrivatePSGallery

# Install a module with -WhatIf
Install-Module ContosoClient -WhatIf

# Install a module with -Confirm. A prompt will be displayed to confirm the installation.
Install-Module ContosoClient -WhatIf

# -Force option reinstalls the installed module
Install-Module ContosoClient -Force

# Install a module with dependencies
Install-Module -Name 
```

## <a name="install-module-cmdlet-in-pipeline-operations"></a><span data-ttu-id="94f69-139">Install-modul a parancsmag a csővezeték-műveletek</span><span class="sxs-lookup"><span data-stu-id="94f69-139">Install-Module cmdlet in pipeline operations</span></span>

```powershell

# Find a module and install it
Find-Module -Name "MyDSC*" | Install-Module

# Find a module and install it to the CurrentUser scope
Find-Module -Name "MyDSC*" | Install-Module -Scope CurrentUser

# Find commands by name and install them
# The first command finds the specified commands in the INT repository, and then uses the pipeline operator to pass them to Install-Module to install them.
# The second command uses Get-InstalledModule to verify the modules from the prior command are installed.
Find-Command -Repository "INT" -Name Get-ContosoClient,Get-ContosoServer | Install-Module
Get-InstalledModule

# This command finds the resource named MyResource and passes it to the Install-Module cmdlet by using the pipeline operator. The Install-Module cmdlet installs the module for the resource. 
# If you pipe multiple resources to the Install-Module cmdlet from the same module, Install-Module attempts to install the module only once. 
Find-DscResource -Name "MyResource" | Install-Module
Get-InstalledModule

# Find multiple role capabilities and install them
Find-RoleCapability -Name MyJeaRole, Maintenance | Install-Module
Get-InstalledModule

```

## <a name="side-by-side-version-support-on-powershell-50-or-newer"></a><span data-ttu-id="94f69-140">Egymás melletti verzióinak támogatása PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="94f69-140">Side-by-Side Version Support on PowerShell 5.0 or newer</span></span>

<span data-ttu-id="94f69-141">PowerShellGet támogatja az egymás melletti (SxS) modul által támogatott verzió Install-modul, a frissítés-modul, és a közzététel-modul parancsmagjai a Windows PowerShell 5.0-s vagy újabb rendszerű.</span><span class="sxs-lookup"><span data-stu-id="94f69-141">PowerShellGet supports the side-by-side (SxS) module version support in Install-Module, Update-Module, and Publish-Module cmdlets that run in Windows PowerShell 5.0 or newer.</span></span>

### <a name="install-module-examples"></a><span data-ttu-id="94f69-142">Install-modul példák</span><span class="sxs-lookup"><span data-stu-id="94f69-142">Install-Module examples</span></span>

```powershell
# Install a version of the module
Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.0 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name : PSScriptAnalyzer
Version : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

# Install another version of the module in Side-by-Side with already installed version.
Install-Module -Name PSScriptAnalyzer -RequiredVersion 1.1.1 -Repository PSGallery
Get-Module -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name       : PSScriptAnalyzer 
Version    : 1.1.1
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.1
Name       : PSScriptAnalyzer
Version    : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

# Get all versions of an installed module
Get-InstalledModule -Name PSScriptAnalyzer -AllVersions
Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.1.0      PSScriptAnalyzer                    PSGallery            PSScriptAnalyzer provides script analysis... 
1.1.1      PSScriptAnalyzer                    PSGallery            PSScriptAnalyzer provides script analysis...


```

## <a name="install-module-with-its-dependencies"></a><span data-ttu-id="94f69-143">A függőségekkel rendelkező modul telepítése</span><span class="sxs-lookup"><span data-stu-id="94f69-143">Install module with its dependencies</span></span>

```powershell

# Find a module
Find-Module -Name TypePx -Repository PSGallery

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to the m...

# Find a module and its dependencies
Find-Module -Name TypePx -Repository PSGallery -IncludeDependencies

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to the m...
1.0.5.18   SnippetPx                           PSGallery            The SnippetPx module enhances the snippet experience i...

# Discover the dependencies list without adding -IncludeDependencies
$result = Find-Module -Name TypePx -Repository PSGallery
$result.Dependencies

Name                           Value
----                           -----
Name                           SnippetPx
CanonicalId                    powershellget:SnippetPx/#https://www.powershellgallery.com/api/v2/


# Now install the module along with its dependencies
Install-Module -Name TypePx -Repository PSGallery -Verbose

VERBOSE: Repository details, Name = 'PSGallery', Location = 'https://www.powershellgallery.com/api/v2/'; IsTrusted =
'False'; IsRegistered = 'True'.
VERBOSE: Using the provider 'PowerShellGet' for searching packages.
VERBOSE: Using the specified source names : 'PSGallery'.
VERBOSE: Getting the provider object for the PackageManagement Provider 'NuGet'.
VERBOSE: The specified Location is 'https://www.powershellgallery.com/api/v2/' and PackageManagementProvider is
'NuGet'.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='TypePx'' for ''.
VERBOSE: Total package yield:'1' for the specified package 'TypePx'.
VERBOSE: Performing the operation "Install-Module" on target "Version '2.0.1.20' of module 'TypePx'".

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
VERBOSE: The installation scope is specified to be 'AllUsers'.
VERBOSE: The specified module will be installed in 'C:\Program Files\WindowsPowerShell\Modules'.
VERBOSE: The specified Location is 'NuGet' and PackageManagementProvider is 'NuGet'.
VERBOSE: Downloading module 'TypePx' with version '2.0.1.20' from the repository
'https://www.powershellgallery.com/api/v2/'.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='TypePx'' for ''.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='SnippetPx'' for ''.
VERBOSE: InstallPackage' - name='SnippetPx',
version='1.0.5.18',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: DownloadPackage' - name='SnippetPx',
version='1.0.5.18',destination='C:\Users\manikb\AppData\Local\Temp\1027042896\SnippetPx\SnippetPx.nupkg',
uri='https://www.powershellgallery.com/api/v2/package/SnippetPx/1.0.5.18'
VERBOSE: Downloading 'https://www.powershellgallery.com/api/v2/package/SnippetPx/1.0.5.18'.
VERBOSE: Completed downloading 'https://www.powershellgallery.com/api/v2/package/SnippetPx/1.0.5.18'.
VERBOSE: Completed downloading 'SnippetPx'.
VERBOSE: Hash for package 'SnippetPx' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='SnippetPx',
version='1.0.5.18',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: InstallPackage' - name='TypePx',
version='2.0.1.20',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: DownloadPackage' - name='TypePx',
version='2.0.1.20',destination='C:\Users\manikb\AppData\Local\Temp\1027042896\TypePx\TypePx.nupkg',
uri='https://www.powershellgallery.com/api/v2/package/TypePx/2.0.1.20'
VERBOSE: Downloading 'https://www.powershellgallery.com/api/v2/package/TypePx/2.0.1.20'.
VERBOSE: Completed downloading 'https://www.powershellgallery.com/api/v2/package/TypePx/2.0.1.20'.
VERBOSE: Completed downloading 'TypePx'.
VERBOSE: Hash for package 'TypePx' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='TypePx',
version='2.0.1.20',destination='C:\Users\manikb\AppData\Local\Temp\1027042896'
VERBOSE: Installing the dependency module 'SnippetPx' with version '1.0.5.18' for the module 'TypePx'.
VERBOSE: Module 'SnippetPx' was installed successfully to path 'C:\Program
Files\WindowsPowerShell\Modules\SnippetPx\1.0.5.18'.
VERBOSE: Module 'TypePx' was installed successfully to path 'C:\Program
Files\WindowsPowerShell\Modules\TypePx\2.0.1.20'.


# Get the installed modules
Get-InstalledModule

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0.5.18   SnippetPx                           PSGallery            The SnippetPx module enhances the snippet experience i...
2.0.1.20   TypePx                              PSGallery            The TypePx module adds properties and methods to the m...

```

## <a name="error-scenarios"></a><span data-ttu-id="94f69-144">Hiba forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="94f69-144">Error scenarios</span></span>

```powershell

# Below command fails with 'NameShouldNotContainWildcardCharacters,Install-Module'
Install-Module ContosoServe*

# Below command fails with 'VersionRangeAndRequiredVersionCannotBeSpecifiedTogether,Install-Module'
Install-Module ContosoServer -MinimumVersion 1.0 -RequiredVersion 5.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Module'
Install-Module ContosoClient,ContosoServer -RequiredVersion 2.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Module'
Install-Module ContosoClient,ContosoServer -MinimumVersion 2.0

```

