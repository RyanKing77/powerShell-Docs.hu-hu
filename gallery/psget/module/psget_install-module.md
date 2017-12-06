---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: Install-modul
ms.openlocfilehash: c066f4b34a03206cc0f31e9d40144fd719d9e305
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/05/2017
---
# <a name="install-module"></a>Install-modul

Online tárházak találhatók a helyi számítógépre a PowerShell-modulok telepítése

## <a name="description"></a>Leírás

Install-modul a parancsmag egy vagy több modulja letölti az online katalógusból, ellenőrzi, és telepíti azokat a helyi számítógépen a megadott telepítési hatókörbe.

Az Install-modul a parancsmag lekérdezi az online katalógusból megadott feltételeknek, egy vagy több modulja, ellenőrzi, hogy a keresési eredmények között érvényes modulok és a telepítési helyre másolja modul mappák.

Nincs hatóköre van definiálva, vagy ha a hatókör-paraméter értéke az AllUsers tulajdonság, a modul %systemdrive%:\Program Files\WindowsPowerShell\Modules van telepítve. CurrentUser hatókör érték esetén a modul $home\Documents\WindowsPowerShell\Modules van telepítve.

A megadott modulokban minimális és a pontos verzióit eredmény végezhet.

- Egymás melletti verzióinak támogatása a Windows PowerShell 5.0-s vagy újabb
- A modul függőségi telepítés támogatása
- **Nem megbízható a parancssorból:**felhasználói elfogadás kell a modulok telepítése egy nem megbízható tárházból.
- -Force újratelepíti a telepített modul
- RequiredVersion SxS PowerShell 5.0-s vagy újabb verziója a meglévő verzióival meghatározott verzióját telepíti.

### <a name="scope"></a>Hatókör
Adja meg a telepítést a modul hatókörében. Ez a paraméter elfogadható értékek a következők: AllUsers és CurrentUser.

Az alapértelmezett telepítési hatóköre az AllUsers tulajdonság.

Az AllUsers tulajdonság hatóköre lehetővé teszi, hogy a modulokat telepíteni, egy olyan helyre, ez azt jelenti, hogy a számítógép összes felhasználója számára elérhető "$env: SystemDrive\Program Files\WindowsPowerShell\Modules".

A CurrentUser hatókör lehetővé teszi, hogy csak a "$home\Documents\WindowsPowerShell\Modules", telepíthető modulok úgy, hogy a modul csak az aktuális felhasználó számára elérhető.

## <a name="notes"></a>Megjegyzések

Ez a parancsmag a Windows PowerShell 3.0-s vagy újabb kiadásaiban a Windows PowerShell, a Windows 7 vagy Windows 2008 R2 és újabb Windows-verziókat futtatja.

Ha telepített modul nem importálható, (Ez azt jelenti, hogy ha egy .psm1, .psd1 vagy egy ugyanilyen nevű .dll nincs a mappában található), telepítés sikertelen lesz, kivéve, ha a Force paramétert a parancshoz adja hozzá.

Ha a modul azon a számítógépen egy verziója megegyezik a Name paraméter megadott értéke, és nem hozzáadta a MinimumVersion vagy RequiredVersion paraméter, Install-modul csendes továbbra is fennáll, hogy a modul telepítése nélkül. Ha a MinimumVersion vagy RequiredVersion paraméterek vannak megadva, és a meglévő modul nem felel meg, hogy a paraméter értékének, majd hiba lép fel. Pontosabban: a jelenleg telepített modul verziószáma alacsonyabb, mint a MinimumVersion paraméter értékét, vagy a RequiredVersion paraméter értéke nem egyenlő, ha hiba lép fel. Ha a telepített modul verziószáma nagyobb, mint a MinimumVersion paraméter értékét, vagy a RequiredVersion paraméter értékének egyenlőnek, Install-modul csendes továbbra is fennáll, hogy a modul telepítése nélkül.

Install-modul hibát ad vissza, ha nincs modul az online katalógus, amely megfelel a megadott névvel már létezik.

Több modul telepítéséhez adja meg a modul neve vesszőkkel elválasztva tömbjét. Nem adhat hozzá MinimumVersion vagy RequiredVersion Ha több modul nevet ad meg.

Alapértelmezés szerint a modulok telepítve vannak a Program Files mappába, problémák elkerülése érdekében a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások telepítése. Átadhatja az Install-modul; több PSGetItemInfo objektumok Ez az egyetlen parancs telepítésének megadásával több modul egy másik módja.

Telepített rosszindulatú kódot tartalmazó futó modulok megelőzése érdekében rendszer nem automatikusan importálja a telepítés. Biztonsági szempontból ajánlott, kiértékelése modul kód parancsmagok és függvények futtatása egy modulban először előtt.


## <a name="cmdlet-syntax"></a>A parancsmag szintaxisa
```powershell
Get-Command -Name Install-Module -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a>A parancsmag online Súgó-hivatkozás

[Install-modul](http://go.microsoft.com/fwlink/?LinkID=398573)

## <a name="example-commands"></a>Példa parancsok

```powershell

# Install a module by name
Install-Module -Name MyDscModule

# Install multiple modules
Install-Module ContosoClient,ContosoServer

# Install a module using its minimum version
Install-Module -Name ContosoServer -MinimumVersion 1.0

# Install a specific version of a module
Install-Module -Name ContosoServer -RequiredVersion 1.1.3

# Install a specific prerelease version of a module
Install-Module -Name ContosoServer -RequiredVersion 1.1.3-alpha -AllowPrerelease

# Install the latest version of a module by name, including prelrelease versions if one exists
Install-Module -Name ContosoServer -AllowPrerelease

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

## <a name="install-module-cmdlet-in-pipeline-operations"></a>Install-modul a parancsmag a csővezeték-műveletek

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

## <a name="side-by-side-version-support-on-powershell-50-or-newer"></a>Egymás melletti verzióinak támogatása PowerShell 5.0-s vagy újabb

PowerShellGet támogatja az egymás melletti (SxS) modul által támogatott verzió Install-modul, a frissítés-modul, és a közzététel-modul parancsmagjai a Windows PowerShell 5.0-s vagy újabb rendszerű.

### <a name="install-module-examples"></a>Install-modul példák

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

## <a name="install-module-with-its-dependencies"></a>A függőségekkel rendelkező modul telepítése

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

## <a name="error-scenarios"></a>Hiba forgatókönyvek

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

