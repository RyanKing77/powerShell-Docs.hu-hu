---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 042e9a30068d32dc5860255bdec960371121d866
ms.sourcegitcommit: 5990f04b8042ef2d8e571bec6d5b051e64c9921c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/12/2019
ms.locfileid: "57795096"
---
# <a name="packagemanagement-cmdlets"></a>PackageManagement-parancsmagok

Ez a központi eleme a PackageManagement a szoftverek felderítése, telepítése és leltárt (SDII). Próbálja ki ezeket a műveleteket a parancsmagokat:

- `Find-Package`
- `Find-PackageProvider`
- `Get-Package`
- `Get-PackageProvider`
- `Get-PackageSource`
- `Import-PackageProvider`
- `Install-Package`
- `Install-PackageProvider`
- `Register-PackageSource`
- `Save-Package`
- `Set-PackageSource`
- `Uninstall-Package`
- `Unregister-PackageSource`

A PackageManagement az egy PowerShell-modul, frissítéséhez PackageManagement magát a következőket teheti:

```powershell
Install-Module PackageManagement –Force
```

Ebben az esetben a PowerShell-munkamenetben írja be újra a PackageManagement az új verzióra váltás kap.

## <a name="find-package-cmdletpowershellmodulepackagemanagementfind-package"></a>[Find-Package parancsmag](/powershell/module/PackageManagement/Find-Package)

Ez a parancsmag lehetővé teszi, hogy a csomag forrásokból használatával szoftvercsomagok felderítése csomag szolgáltatók betöltése.

```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -ProviderName PowerShellGet -Source as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## <a name="find-packageprovider-cmdletpowershellmodulepackagemanagementfind-packageprovider"></a>[Keresés – PackageProvider parancsmag](/powershell/module/PackageManagement/Find-PackageProvider)

A `Find-PackageProvider` parancsmaggal megkeresi a PowerShellGet megfelelő csomag forrásainak érhető el a PackageManagement-szolgáltatók regisztrálva. Ezek a érhető el a telepítési csomag szolgáltatók a `Install-PackageProvider` parancsmagot. Alapértelmezés szerint ez a PowerShell-galériából, a "PackageManagement" és "a Felhőszolgáltatói címkék a modullistából is tartalmaz.

`Find-PackageProvider` a PackageManagement az azure blob tároló, ahol használjuk a PackageManagement boostrapper szolgáltató megtalálásához, és telepíteni kell őket a rendelkezésre álló megfelelő PackageManagement-szolgáltatókat is megtalálja.

```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"
```

## <a name="get-package-cmdletpowershellmodulepackagemanagementget-package"></a>[Get-Package parancsmag](/powershell/module/PackageManagement/Get-Package)

Ez a parancsmag az összes szoftvercsomag PackageManagement használatával telepített listáját adja vissza.

```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## <a name="get-packageprovider-cmdletpowershellmodulepackagemanagementget-packageprovider"></a>[Get-PackageProvider parancsmag](/powershell/module/PackageManagement/Get-PackageProvider)

Csomag szolgáltatók betöltött és készen áll a használatra, a helyi számítógépen is leltározandó parancsmag használatával.

```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## <a name="get-packagesource-cmdletpowershellmodulepackagemanagementget-packagesource"></a>[Get-PackageSource parancsmag](/powershell/module/PackageManagement/Get-PackageSource)

Ez a parancsmag egy csomag szolgáltató regisztrált csomagforrások listáját kéri le.

```powershell
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## <a name="import-packageprovider-cmdletpowershellmodulepackagemanagementimport-packageprovider"></a>[Importálás – PackageProvider parancsmag](/powershell/module/PackageManagement/Import-PackageProvider)

Ez a parancsmag hozzáadja a jelenlegi munkamenet csomag felügyeleti csomag szolgáltatók.

```powershell
# Import a package provider from the local machine
Import-PackageProvider –Name MyProvider

#The -Name parameter can be either the name of the provider or the full path to the provider. Currently, we support .dll, .exe and.psm1 for the full path case. If the name of the provider is used for the -Name parameter, then additional version parameters such as -RequiredVersion, -MinimumVersion and -MaximumVersion may be specified. Otherwise, the latest version of the provider will be imported.

#If a package provider is not yet loaded to your system, we can discover and install on-demand. You can use explicit discovery and install cmdlets to do so:
 Find-PackageProvider
 Install-PackageProvider –Name MyProvider

#After installed, follow the Import-PackageProvider to load it to your system.

# Import a specific version of a package provider. PackageManagement supports installations of multiple versions of a package provider using PackageProvider cmdlets (not by bootstrapper provider). You can install another version of a package provider given that you already have one up running by:
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force
Get-PackageProvider –ListAvailable
Import-PackageProvider –Name "Nuget" -RequiredVersion "2.8.5.201" -Verbose
Import-PackageProvider –Name MyProvider –RequiredVersion xxxx -force
```

## <a name="install-package-cmdletpowershellmodulepackagemanagementinstall-package"></a>[Install-Package parancsmag](/powershell/module/PackageManagement/Install-Package)

Ez a parancsmag lehetővé teszi, hogy a csomag forrásokból használatával szoftvercsomagok telepítése csomag szolgáltatók betöltése.

```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## <a name="install-packageprovider-cmdletpowershellmodulepackagemanagementinstall-packageprovider"></a>[Install-PackageProvider parancsmag](/powershell/module/PackageManagement/Install-PackageProvider)

Ez a parancsmag egy vagy több csomagot felügyeleti csomag szolgáltatót telepíti.

```powershell
# Install a package provider from the PowerShell Gallery
Install-PackageProvider –Name "Gistprovider" -Verbose

# Install a specified version of a package provider
Find-PackageProvider –Name "Nuget" -AllVersions
Install-PackageProvider -Name "Nuget" -RequiredVersion "2.8.5.201" -Force

# Find a provider and install it
Find-PackageProvider –Name "Gistprovider" | Install-PackageProvider -Verbose

# Install a provider to the current user’s module folder
Install-PackageProvider –Name Gistprovider –Verbose –Scope CurrentUser
```

## <a name="register-packagesource-cmdletpowershellmodulepackagemanagementregister-packagesource"></a>[Register-PackageSource parancsmag](/powershell/module/PackageManagement/Register-PackageSource)

Ez a parancsmag egy csomag forrása hozzáadja a megadott csomag szolgáltató.
Előfordulhat, hogy mindegyik PackageManagement-szolgáltató egy vagy több szoftverfrissítési forrásból, vagy tárházakban. A PackageManagement biztosít hozzáadása/eltávolítása/lekérdezési PowerShell-parancsmagokat a forrás. Ha például egy csomag forrása a NuGet-szolgáltató regisztrálásához:

```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## <a name="save-package-cmdletpowershellmodulepackagemanagementsave-package"></a>[A parancsmag Save-csomag](/powershell/module/PackageManagement/Save-Package)

Ez a parancsmag csomagok menti a helyi számítógépre telepítés nélkül.

```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -Source c:\test
```

## <a name="set-packagesource-cmdletpowershellmodulepackagemanagementset-packagesource"></a>[Set-PackageSource parancsmag](/powershell/module/PackageManagement/Set-PackageSource)

Ez a parancsmag módosítja egy meglévő csomag forrása kapcsolatos információkat.

```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2
```

## <a name="uninstall-package-cmdletpowershellmodulepackagemanagementuninstall-package"></a>[Csomag eltávolítása parancsmag](/powershell/module/PackageManagement/Uninstall-Package)

Ez a parancsmag eltávolítja a helyi számítógépen telepített csomagok.

```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## <a name="unregister-packagesource-cmdletpowershellmodulepackagemanagementunregister-packagesource"></a>[Regisztrációját PackageSource parancsmag](/powershell/module/PackageManagement/Unregister-PackageSource)

```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```