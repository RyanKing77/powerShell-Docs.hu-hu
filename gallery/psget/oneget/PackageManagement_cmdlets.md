---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: PackageManagement_cmdlets
ms.openlocfilehash: aca4f461ff0e51aa812f8219c74bd7d85d1e7b2d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="packagemanagement-cmdlets"></a><span data-ttu-id="a6a75-103">PackageManagement parancsmagok</span><span class="sxs-lookup"><span data-stu-id="a6a75-103">PackageManagement Cmdlets</span></span>
<span data-ttu-id="a6a75-104">Ez a szoftver felderítés, telepítés és a készlet (SDII) támogatásához PackageManagement részében.</span><span class="sxs-lookup"><span data-stu-id="a6a75-104">This is the core of PackageManagement to support software discovery, installation, and inventory (SDII).</span></span> <span data-ttu-id="a6a75-105">Próbálja ki ezeket a műveleteket a parancsmagokat:</span><span class="sxs-lookup"><span data-stu-id="a6a75-105">Try out the cmdlets for these operations:</span></span>
-   <span data-ttu-id="a6a75-106">Keresés-csomag</span><span class="sxs-lookup"><span data-stu-id="a6a75-106">Find-Package</span></span>
-   <span data-ttu-id="a6a75-107">Keresés – PackageProvider</span><span class="sxs-lookup"><span data-stu-id="a6a75-107">Find-PackageProvider</span></span>
-   <span data-ttu-id="a6a75-108">Get-csomag</span><span class="sxs-lookup"><span data-stu-id="a6a75-108">Get-Package</span></span>
-   <span data-ttu-id="a6a75-109">Get-PackageProvider</span><span class="sxs-lookup"><span data-stu-id="a6a75-109">Get-PackageProvider</span></span>
-   <span data-ttu-id="a6a75-110">Get-PackageSource</span><span class="sxs-lookup"><span data-stu-id="a6a75-110">Get-PackageSource</span></span>
-   <span data-ttu-id="a6a75-111">Importálás – PackageProvider</span><span class="sxs-lookup"><span data-stu-id="a6a75-111">Import-PackageProvider</span></span>
-   <span data-ttu-id="a6a75-112">Install-csomag</span><span class="sxs-lookup"><span data-stu-id="a6a75-112">Install-Package</span></span>
-   <span data-ttu-id="a6a75-113">Install-PackageProvider</span><span class="sxs-lookup"><span data-stu-id="a6a75-113">Install-PackageProvider</span></span>
-   <span data-ttu-id="a6a75-114">Register-PackageSource</span><span class="sxs-lookup"><span data-stu-id="a6a75-114">Register-PackageSource</span></span>
-   <span data-ttu-id="a6a75-115">Mentés-csomag</span><span class="sxs-lookup"><span data-stu-id="a6a75-115">Save-Package</span></span>
-   <span data-ttu-id="a6a75-116">Set-PackageSource</span><span class="sxs-lookup"><span data-stu-id="a6a75-116">Set-PackageSource</span></span>
-   <span data-ttu-id="a6a75-117">Csomag eltávolítása</span><span class="sxs-lookup"><span data-stu-id="a6a75-117">Uninstall-Package</span></span>
-   <span data-ttu-id="a6a75-118">PackageSource regisztrációjának törlése</span><span class="sxs-lookup"><span data-stu-id="a6a75-118">Unregister-PackageSource</span></span>

<span data-ttu-id="a6a75-119">Mivel PackageManagement egy PowerShell-modult, maga PackageManagement frissítéséhez a következőket teheti:</span><span class="sxs-lookup"><span data-stu-id="a6a75-119">As PackageManagement is a PowerShell module, you can do the following to update PackageManagement itself:</span></span>
```powershell
PS C:\> Install-Module PackageManagement –Force
```
<span data-ttu-id="a6a75-120">Ebben az esetben kell PowerShell-munkamenetben írja be újra váltson át a PackageManagement új verziója.</span><span class="sxs-lookup"><span data-stu-id="a6a75-120">In this case, you will have to re-enter PowerShell session to switch to the new version of PackageManagement.</span></span>

## <a name="find-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890709aspx"></a>[<span data-ttu-id="a6a75-121">Keresés-csomag parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-121">Find-Package Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890709.aspx)
<span data-ttu-id="a6a75-122">Ez a parancsmag lehetővé teszi a szoftvercsomagok használatával elérhető csomag adatforrások felfedezése csomag szolgáltatók betöltése.</span><span class="sxs-lookup"><span data-stu-id="a6a75-122">This cmdlet allows discovery of software packages in available package sources using loaded package providers.</span></span>
```powershell
# Find all available Windows PowerShell module packages from galleries registered
# with PowerShellGet provider
Find-Package -Provider PowerShellGet -Source PSGallery

# Find a package from a provider that is not yet installed
# This will bootstrap NuGet provider and then search for jquery package using NuGet
# with <http://www.nuget.org/api/v2/> as source
Find-Package -Name jquery –Provider NuGet -Source http://www.nuget.org/api/v2/

# Find package with name and version
# Here we are assuming that the user already registered nuget.org using
# Register-PackageSource. You can specify either the provider or the source, or
# neither. For the latter, performance may be less optimal as it searches through all
# the providers and registered sources.
Find-Package -Name jquery –Provider NuGet –RequiredVersion 2.1.4 -Source nuget.org
```

## <a name="find-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarymt676544aspx"></a>[<span data-ttu-id="a6a75-123">Keresés – PackageProvider parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-123">Find-PackageProvider Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/mt676544.aspx)
<span data-ttu-id="a6a75-124">A keresés-PackageProvider parancsmag egyező PackageManagement szolgáltatók csomag adatforrások regisztrálva PowerShellGet a rendelkezésre álló talál.</span><span class="sxs-lookup"><span data-stu-id="a6a75-124">The Find-PackageProvider cmdlet finds matching PackageManagement providers that are available in package sources registered with PowerShellGet.</span></span> <span data-ttu-id="a6a75-125">Ezek a csomag szolgáltatók telepíthetők az Install-PackageProvider parancsmaggal.</span><span class="sxs-lookup"><span data-stu-id="a6a75-125">These are package providers available for installation with the Install-PackageProvider cmdlet.</span></span> <span data-ttu-id="a6a75-126">Alapértelmezés szerint ez a "PackageManagement" és "Provider" címkék a PowerShell-galériában modullistából magában foglalja.</span><span class="sxs-lookup"><span data-stu-id="a6a75-126">By default, this includes modules available in the PowerShell Gallery with the 'PackageManagement' and 'Provider' Tags.</span></span> 

<span data-ttu-id="a6a75-127">Keresés – PackageProvider is talál megfelelő PackageManagement szolgáltatók által biztosított a PackageManagement azure blob a tárolóban, ahol használjuk a PackageManagement boostrapper szolgáltató kereséséhez és telepíteni kell őket.</span><span class="sxs-lookup"><span data-stu-id="a6a75-127">Find-PackageProvider also finds matching PackageManagement providers that are available in the PackageManagement azure blob store where we use the PackageManagement boostrapper provider for finding and installing them.</span></span>
```powershell
#Find all available package providers in PackageManagement azure blob store as well as in PowerShellGallery.com
Find-PackageProvider

#Find all versions of a provider
Find-PackageProvider -Name "Nuget" -AllVersions

#Find a provider from a specified source
Find-PackageProvider -Name "Gistprovider" -Source "PSGallery"

#For machines without internet, you can download the nuget provider first, put it to you file share and then use the following to install the nuget provider (TP5 or later).

Find-PackageProvider -Source  C:\sharedfolder\Providers\
Install-PackageProvider -Source C:\sharedfolder\Providers\ -Name nuget -force
    
```

## <a name="get-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890704aspx"></a>[<span data-ttu-id="a6a75-128">Get-csomag parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-128">Get-Package Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890704.aspx)
<span data-ttu-id="a6a75-129">Ez a parancsmag az összes szoftvercsomag PackageManagement használatával telepített listáját adja vissza.</span><span class="sxs-lookup"><span data-stu-id="a6a75-129">This cmdlet returns a list of all software packages that have been installed using PackageManagement.</span></span>
```powershell
# Get all the packages installed by Programs provider
Get-Package –Provider Programs

# Get all the packages installed by NuGet provider at c:\test using the dynamic
# parameter destination
Get-Package –Provider NuGet -Destination c:\test
```

## <a name="get-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890703aspx"></a>[<span data-ttu-id="a6a75-130">Get-PackageProvider parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-130">Get-PackageProvider Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890703.aspx)
<span data-ttu-id="a6a75-131">Betöltött, illetve a helyi gépen használatra kész csomag hitelesítésszolgáltatók is bekerülhet a leltárba parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="a6a75-131">Package providers that are loaded and ready to be used on the local machine can be inventoried by using the cmdlet.</span></span>
```powershell
# Get all currently loaded package providers
Get-PackageProvider

# The following cmdlet will show all the package providers available on the machine (including those that are not loaded):
Get-PackageProvider -ListAvailable
```

## <a name="get-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890705aspx"></a>[<span data-ttu-id="a6a75-132">Get-PackageSource parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-132">Get-PackageSource Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890705.aspx)
<span data-ttu-id="a6a75-133">Ez a parancsmag egy csomag szolgáltató regisztrált adatforrások csomag listájának lekérése.</span><span class="sxs-lookup"><span data-stu-id="a6a75-133">This cmdlet gets a list of package sources that are registered for a package provider.</span></span>
```powershelll
# Get all package sources
Get-PackageSource

# Get all package sources for a specific provider
Get-PackageSource –ProviderName PowerShellGet
```

## <a name="import-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarymt676545aspx"></a>[<span data-ttu-id="a6a75-134">Import-PackageProvider parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-134">Import-PackageProvider Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/mt676545.aspx)
<span data-ttu-id="a6a75-135">Ez a parancsmag csomag felügyeleti csomag szolgáltatók hozzáadja az aktuális munkamenet.</span><span class="sxs-lookup"><span data-stu-id="a6a75-135">This cmdlet adds Package Management package providers to the current session.</span></span>
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

As of the Windows Server Technical Preview(TP5), Install-PackageProvider does install as well as import the provider. Hence after you run find-packageprovider and install-packageprovider, the provider should be ready to use 
```

##<a name="-install-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890711aspx"></a>[<span data-ttu-id="a6a75-136">Install-Package parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-136"> Install-Package Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890711.aspx)

<span data-ttu-id="a6a75-137">Ez a parancsmag lehetővé teszi, hogy a rendelkezésre álló csomag forrásokban használatával szoftvercsomagok telepítése csomag szolgáltatók betöltése.</span><span class="sxs-lookup"><span data-stu-id="a6a75-137">This cmdlet allows installation of software packages in available package sources using loaded package providers.</span></span>
```powershell
# Install a package by name.
# NuGet provider requires us to provide the dynamic parameter destination path
# when we use this provider to install. Not all providers will require you to supply
# dynamic parameters for PackageManagement cmdlets.
Install-Package -Name jquery -Source nuget.org -Destination c:\test

# Install a package by piping.
Find-Package -Name jquery –Provider NuGet | Install-Package -Destination c:\test
```

## <a name="install-packageprovider-cmdlethttpstechnetmicrosoftcomen-uslibrarymt676543aspx"></a>[<span data-ttu-id="a6a75-138">Install-PackageProvider parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-138">Install-PackageProvider Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/mt676543.aspx)
<span data-ttu-id="a6a75-139">Ez a parancsmag egy vagy több csomagot felügyeleti csomag szolgáltatót telepíti.</span><span class="sxs-lookup"><span data-stu-id="a6a75-139">This cmdlet installs one or more Package Management package providers.</span></span>
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

## <a name="register-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890701aspx"></a>[<span data-ttu-id="a6a75-140">Register-PackageSource parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-140">Register-PackageSource Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890701.aspx)
<span data-ttu-id="a6a75-141">Ez a parancsmag egy csomagforrást meghatározott csomag-szolgáltató hozzáadása.</span><span class="sxs-lookup"><span data-stu-id="a6a75-141">This cmdlet adds a package source for a specified package provider.</span></span>
<span data-ttu-id="a6a75-142">Előfordulhat, hogy mindegyik PackageManagement-szolgáltató egy vagy több szoftverfrissítési forrásból, vagy tárházak találhatók.</span><span class="sxs-lookup"><span data-stu-id="a6a75-142">Each PackageManagement provider may have one or multiple software sources, or repositories.</span></span> <span data-ttu-id="a6a75-143">PackageManagement a forrás hozzáadása/eltávolítása/lekérdezés PowerShell-parancsmagokat kínál.</span><span class="sxs-lookup"><span data-stu-id="a6a75-143">PackageManagement provides PowerShell cmdlets to add/remove/query the source.</span></span> <span data-ttu-id="a6a75-144">Például a csomag forrásához regisztrálhatja a NuGet-szolgáltató:</span><span class="sxs-lookup"><span data-stu-id="a6a75-144">For example, you can register a package source for the NuGet provider:</span></span>
```powershell
Register-PackageSource -Name "NugetSource" -Location "http://www.nuget.org/api/v2" –ProviderName nuget
```

## <a name="save-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890708aspx"></a>[<span data-ttu-id="a6a75-145">A parancsmag mentés-csomag</span><span class="sxs-lookup"><span data-stu-id="a6a75-145">Save-Package Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890708.aspx)
<span data-ttu-id="a6a75-146">Ez a parancsmag csomagok menti a helyi számítógépre telepítés nélkül.</span><span class="sxs-lookup"><span data-stu-id="a6a75-146">This cmdlet saves packages to the local computer without installing them.</span></span>
```powershell
# Saves jquery package to c:\test using NuGetProvider
# Notes that the -Path parameter must point to an existing location
Save-Package -Name jquery –Provider NuGet -Path c:\test

# Save a package by piping.
Find-Package -Name jquery -Source http://www.nuget.org/api/v2/ | Save-Package -Path c:\test
Find-Package -source c:\test
```

## <a name="set-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890710aspx"></a>[<span data-ttu-id="a6a75-147">Set-PackageSource parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-147">Set-PackageSource Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890710.aspx)
<span data-ttu-id="a6a75-148">Ez a parancsmag módosítja egy meglévő csomag forrása kapcsolatos információkat.</span><span class="sxs-lookup"><span data-stu-id="a6a75-148">This cmdlet changes information about an existing package source.</span></span> 
```powershell
#Set-PackageSource changes the values for a source that has already been registered by running the Register-PackageSource cmdlet. By #running Set-PackageSource, you can change the source name and location.
Set-PackageSource  -Name nuget.org -Location  http://www.nuget.org/api/v2 -NewName nuget2 -NewLocation https://www.nuget.org/api/v2 
```

## <a name="uninstall-package-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890702aspx"></a>[<span data-ttu-id="a6a75-149">Távolítsa el csomag parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-149">Uninstall-Package Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890702.aspx)
<span data-ttu-id="a6a75-150">Ez a parancsmag eltávolítja a helyi számítógépen telepített csomagok.</span><span class="sxs-lookup"><span data-stu-id="a6a75-150">This cmdlet uninstalls packages installed on the local computer.</span></span>
```powershell
# Uninstall jquery using nuget
Uninstall-Package -Name jquery –Provider NuGet -Destination c:\test

# Uninstall a package with by piping with Get-Package
Get-Package -Name jquery –Provider NuGet -Destination c:\test | Uninstall-Package
```

## <a name="unregister-packagesource-cmdlethttpstechnetmicrosoftcomen-uslibrarydn890707aspx"></a>[<span data-ttu-id="a6a75-151">Unregister-PackageSource parancsmag</span><span class="sxs-lookup"><span data-stu-id="a6a75-151">Unregister-PackageSource Cmdlet</span></span>](https://technet.microsoft.com/en-us/library/dn890707.aspx)
```powershell
# Unregister a package source for the NuGet provider. You can use command Unregister-PackageSource, to disconnect with a repository, and Get-PackageSource, to discover what the repositories are associated with that provider.
Unregister-PackageSource  -Name "NugetSource"
```

