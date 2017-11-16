---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "gyűjtemény, a powershell, a parancsmag, a psget"
title: "Install-parancsfájl"
ms.openlocfilehash: 4c3fd9393ccb7ee5c3b010f1114b6596a74fdee2
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="install-script"></a><span data-ttu-id="4b6b9-103">Install-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="4b6b9-103">Install-Script</span></span>

<span data-ttu-id="4b6b9-104">Telepíti a PowerShell parancsfájlok online tárházak találhatók a helyi számítógépre.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-104">Installs the PowerShell script files from online repositories to the local computer.</span></span>


## <a name="description"></a><span data-ttu-id="4b6b9-105">Leírás</span><span class="sxs-lookup"><span data-stu-id="4b6b9-105">Description</span></span>

<span data-ttu-id="4b6b9-106">A telepítési parancsfájl-parancsmag szerez be a parancsfájl hasznos adatok között egy adattárból, ellenőrzi, hogy a tartalom egy érvényes PowerShell-parancsfájl, és a parancsfájl a megadott telepítési helyre másolja.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-106">The Install-Script cmdlet acquires a script payload from a repository, verifies that the payload is a valid PowerShell script, and copies the script file to a specified installation location.</span></span>

<span data-ttu-id="4b6b9-107">Az Install-parancsfájl működik elleni alapértelmezett adattárak esetében a Register-PSRepository, a Set-PSRepository, a Unregister-PSRepository és a Get-PSRepository parancsmagok segítségével konfigurálhatók.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-107">The default repositories Install-Script operates against are configurable through the Register-PSRepository, Set-PSRepository, Unregister-PSRepository, and Get-PSRepository cmdlets.</span></span> <span data-ttu-id="4b6b9-108">Ha több adattárak ellen, telepítési parancsfájl-telepíti az első parancsfájl, amely a megadott keresési feltételeknek megfelelő (név, MinimumVersion vagy MaximumVersion) bármely hiba nélkül első tárházból.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-108">When operating against multiple repositories, Install-Script installs the first script that matches the specified search criteria (Name, MinimumVersion, or MaximumVersion) from the first repository without any error.</span></span>


<span data-ttu-id="4b6b9-109">Install-parancsfájl parancsmag tölt le egy vagy több modulja egy online gyűjtemény, ellenőrzi, és telepíti azokat a helyi számítógépen a megadott telepítési hatókörbe.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-109">Install-Script cmdlet downloads one or more modules from an online gallery, validates and installs them on the local computer to the specified installation scope.</span></span>

<span data-ttu-id="4b6b9-110">A telepítési parancsfájl-parancsmag lekéri az online katalógusból megadott feltételeknek, egy vagy több modulja, ellenőrzi, hogy a keresési eredmények között érvényes modulok és a telepítési helyre másolja modul mappák.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-110">The Install-Script cmdlet gets one or more modules that meet specified criteria from an online gallery, verifies that search results are valid modules, and copies module folders to the installation location.</span></span>

<span data-ttu-id="4b6b9-111">Nincs hatóköre van definiálva, vagy ha a hatókör-paraméter értéke az AllUsers tulajdonság, a modul %systemdrive%:\Program Files\WindowsPowerShell\Modules van telepítve.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-111">When no scope is defined, or when the value of the Scope parameter is AllUsers, the module is installed to %systemdrive%:\Program Files\WindowsPowerShell\Modules.</span></span> <span data-ttu-id="4b6b9-112">CurrentUser hatókör érték esetén a modul $home\Documents\WindowsPowerShell\Modules van telepítve.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-112">When the value of Scope is CurrentUser, the module is installed to $home\Documents\WindowsPowerShell\Modules.</span></span>

<span data-ttu-id="4b6b9-113">A megadott modulokban minimális és a pontos verzióit eredmény végezhet.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-113">You can filter your results based on minimum and exact versions of specified modules.</span></span>

- <span data-ttu-id="4b6b9-114">Nincs PowerShell parancsfájlok párhuzamos verzió támogatása</span><span class="sxs-lookup"><span data-stu-id="4b6b9-114">No Side-by-side version support for PowerShell Script files</span></span>
- <span data-ttu-id="4b6b9-115">Parancsfájl függőségi telepítés támogatása</span><span class="sxs-lookup"><span data-stu-id="4b6b9-115">Script dependency installation support</span></span>
- <span data-ttu-id="4b6b9-116">**Nem megbízható a parancssorból:** felhasználói elfogadás kell a modulok telepítése egy nem megbízható tárházból.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-116">**Untrusted prompt:** User acceptance is required for installing the modules from an untrusted repository.</span></span>
- <span data-ttu-id="4b6b9-117">-Force újratelepíti a telepített modul</span><span class="sxs-lookup"><span data-stu-id="4b6b9-117">-Force reinstalls the installed module</span></span>
- <span data-ttu-id="4b6b9-118">RequiredVersion SxS PowerShell 5.0-s vagy újabb verziója a meglévő verzióival meghatározott verzióját telepíti.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-118">RequiredVersion installs the specified version in SxS with existing versions on PowerShell version 5.0 or newer.</span></span>

<span data-ttu-id="4b6b9-119">Helyettesítő karakterek nem támogatottak a - Name Install-modul, mentés-modul, eltávolítás-modulon, Install-parancsfájl, mentés-parancsfájl és eltávolítás parancsfájl-parancsmagokat.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-119">Wildcards are not supported in -Name on Install-Module, Save-Module, Uninstall-Module, Install-Script, Save-Script, and Uninstall-Script cmdlets.</span></span>

### <a name="scope"></a><span data-ttu-id="4b6b9-120">Hatókör</span><span class="sxs-lookup"><span data-stu-id="4b6b9-120">Scope</span></span>
<span data-ttu-id="4b6b9-121">Adja meg a telepítést a modul hatókörében.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-121">Specifies the installation scope of the module.</span></span> <span data-ttu-id="4b6b9-122">Ez a paraméter elfogadható értékek a következők: AllUsers és CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-122">The acceptable values for this parameter are: AllUsers and CurrentUser.</span></span>

<span data-ttu-id="4b6b9-123">Az alapértelmezett telepítési hatóköre az AllUsers tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-123">The default installation scope is AllUsers.</span></span>

<span data-ttu-id="4b6b9-124">Az AllUsers tulajdonság hatóköre lehetővé teszi, hogy a modulokat telepíteni, egy olyan helyre, ez azt jelenti, hogy a számítógép összes felhasználója számára elérhető "$env: SystemDrive\Program Files\WindowsPowerShell\Modules".</span><span class="sxs-lookup"><span data-stu-id="4b6b9-124">The AllUsers scope lets modules be installed in a location that is accessible to all users of the computer, that is, "$env:SystemDrive\Program Files\WindowsPowerShell\Modules".</span></span>

<span data-ttu-id="4b6b9-125">A CurrentUser hatókör lehetővé teszi, hogy csak a "$home\Documents\WindowsPowerShell\Modules", telepíthető modulok úgy, hogy a modul csak az aktuális felhasználó számára elérhető.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-125">The CurrentUser scope lets modules be installed only to "$home\Documents\WindowsPowerShell\Modules", so that the module is available only to the current user.</span></span>


<span data-ttu-id="4b6b9-126">A parancsfájl a telepítés hatóköre határozza meg.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-126">Specifies the installation scope of the script.</span></span> <span data-ttu-id="4b6b9-127">Érvényes értékek a következők: AllUsers és CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-127">Valid values are: AllUsers and CurrentUser.</span></span> <span data-ttu-id="4b6b9-128">Az alapértelmezett érték a CurrentUser.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-128">The default is CurrentUser.</span></span>

<span data-ttu-id="4b6b9-129">Az AllUsers hatókör meghatározza, hogy a parancsfájl %systemdrive%:\ProgramFiles\WindowsPowerShell\Scripts telepítése, úgy, hogy a parancsfájl minden felhasználó számára elérhető.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-129">The AllUsers scope specifies to install a script to %systemdrive%:\ProgramFiles\WindowsPowerShell\Scripts so that the script is available to all users.</span></span> <span data-ttu-id="4b6b9-130">A CurrentUser hatókör határozza meg, hogy a parancsfájl áll rendelkezésre, csak az aktuális felhasználóhoz való telepítéséhez a parancsfájl $home\Documents\WindowsPowerShell\Scripts.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-130">The CurrentUser scope specifies to install the script in $home\Documents\WindowsPowerShell\Scripts so that the script is available only to the current user.</span></span>


## <a name="nopathupdate"></a><span data-ttu-id="4b6b9-131">NoPathUpdate</span><span class="sxs-lookup"><span data-stu-id="4b6b9-131">NoPathUpdate</span></span>

- <span data-ttu-id="4b6b9-132">NoPathUpdate kapcsolóparaméter az Install-parancsfájl parancsmag megkerüli a parancsfájl telepítési helyére hozzáadása a PATH környezeti változóba a kérése.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-132">NoPathUpdate switch parameter on Install-Script cmdlet bypasses the prompt for adding the script install location to the PATH environment variable.</span></span>
- <span data-ttu-id="4b6b9-133">A parancs használata a megadott – NoPathUpdate hatására az kérdés nélkül és az elérési út nem frissítése (kényszerített figyelmen kívül hagyható itt).</span><span class="sxs-lookup"><span data-stu-id="4b6b9-133">Any use of the command WITH –NoPathUpdate specified will result in no prompt and the PATH NOT being updated (force is ignorable here).</span></span>
- <span data-ttu-id="4b6b9-134">-Force nélkül – NoPathUpdate kérdés nélkül eredményez, és az elérési út frissülni fog.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-134">-Force without –NoPathUpdate will result in no prompt and the PATH will be updated.</span></span>
- <span data-ttu-id="4b6b9-135">Ha sem – Force, vagy – NoPathUpdate meg van adva, a felhasználó a kérdés jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-135">If neither –Force or –NoPathUpdate are specified, the user will see the prompt.</span></span>
- <span data-ttu-id="4b6b9-136">Mindez csak az első alkalommal való használatakor telepítési-parancsfájl egy adott hatókörben érvényes.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-136">All of this only applies the first time Install-Script is used in a given scope.</span></span>


## <a name="notes"></a><span data-ttu-id="4b6b9-137">Megjegyzések</span><span class="sxs-lookup"><span data-stu-id="4b6b9-137">Notes</span></span>

<span data-ttu-id="4b6b9-138">Ez a parancsmag a Windows PowerShell 3.0-s vagy újabb kiadásaiban a Windows PowerShell, a Windows 7 vagy Windows 2008 R2 és újabb Windows-verziókat futtatja.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-138">This cmdlet runs on Windows PowerShell 3.0 or later releases of Windows PowerShell, on Windows 7 or Windows 2008 R2 and later releases of Windows.</span></span>

<span data-ttu-id="4b6b9-139">Ha telepített modul nem importálható, (Ez azt jelenti, hogy ha egy .psm1, .psd1 vagy egy ugyanilyen nevű .dll nincs a mappában található), telepítés sikertelen lesz, kivéve, ha a Force paramétert a parancshoz adja hozzá.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-139">If an installed module cannot be imported (that is, if it does not have a .psm1, .psd1, or .dll of the same name within the folder), installation fails unless you add the Force parameter to your command.</span></span>

<span data-ttu-id="4b6b9-140">A modul azon a számítógépen egy verziója megegyezik a Name paraméter megadott értéke, és nem hozzá vannak adva a MinimumVersion vagy RequiredVersion paramétert, ha telepítési-parancsfájl csendes továbbra is fennáll, hogy a modul telepítése nélkül.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-140">If a version of the module on the computer matches the value specified for the Name parameter, and you have not added the MinimumVersion or RequiredVersion parameter, Install-Script silently continues without installing that module.</span></span> <span data-ttu-id="4b6b9-141">Ha a MinimumVersion vagy RequiredVersion paraméterek vannak megadva, és a meglévő modul nem felel meg, hogy a paraméter értékének, majd hiba lép fel.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-141">If the MinimumVersion or RequiredVersion parameters are specified, and the existing module does not match the values in that parameter, then an error occurs.</span></span> <span data-ttu-id="4b6b9-142">Pontosabban: a jelenleg telepített modul verziószáma alacsonyabb, mint a MinimumVersion paraméter értékét, vagy a RequiredVersion paraméter értéke nem egyenlő, ha hiba lép fel.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-142">To be more specific: if the version of the currently-installed module is either lower than the value of the MinimumVersion parameter, or not equal to the value of the RequiredVersion parameter, an error occurs.</span></span> <span data-ttu-id="4b6b9-143">A telepített modul verziószáma nagyobb, mint a MinimumVersion paraméter értékét, vagy a RequiredVersion paraméter értékének egyenlőnek, ha telepítés-parancsfájl csendes továbbra is fennáll, hogy a modul telepítése nélkül.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-143">If the version of the installed module is greater than the value of the MinimumVersion parameter, or equal to the value of the RequiredVersion parameter, Install-Script silently continues without installing that module.</span></span>

<span data-ttu-id="4b6b9-144">Telepítési parancsfájl-hibát ad vissza, ha nincs modul az online katalógus, amely megfelel a megadott névvel már létezik.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-144">Install-Script returns an error if no module exists in the online gallery that matches the specified name.</span></span>

<span data-ttu-id="4b6b9-145">Több modul telepítéséhez adja meg a modul neve vesszőkkel elválasztva tömbjét.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-145">To install multiple modules, specify an array of the module names, separated by commas.</span></span> <span data-ttu-id="4b6b9-146">Nem adhat hozzá MinimumVersion vagy RequiredVersion Ha több modul nevet ad meg.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-146">You cannot add MinimumVersion or RequiredVersion if you specify multiple module names.</span></span>

<span data-ttu-id="4b6b9-147">Alapértelmezés szerint a modulok telepítve vannak a Program Files mappába, problémák elkerülése érdekében a Windows PowerShell kívánt állapot konfigurációs szolgáltatása (DSC) erőforrások telepítése. Átadhatja az Install-parancsprogram, több PSGetItemInfo objektumok Ez az egyetlen parancs telepítésének megadásával több modul egy másik módja.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-147">By default, modules are installed to the Program Files folder, to prevent confusion when you are installing Windows PowerShell Desired State Configuration (DSC) resources.You can pipe multiple PSGetItemInfo objects to Install-Script; this is another way of specifying multiple modules to install in a single command.</span></span>

<span data-ttu-id="4b6b9-148">Telepített rosszindulatú kódot tartalmazó futó modulok megelőzése érdekében rendszer nem automatikusan importálja a telepítés.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-148">To help prevent running modules that contain malicious code, installed modules are not automatically imported by installation.</span></span> <span data-ttu-id="4b6b9-149">Biztonsági szempontból ajánlott, kiértékelése modul kód parancsmagok és függvények futtatása egy modulban először előtt.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-149">As a security best practice, evaluate module code before running any cmdlets or functions in a module for the first time.</span></span>


## <a name="cmdlet-syntax"></a><span data-ttu-id="4b6b9-150">A parancsmag szintaxisa</span><span class="sxs-lookup"><span data-stu-id="4b6b9-150">Cmdlet syntax</span></span>

```powershell
Get-Command -Name Install-Script -Module PowerShellGet -Syntax
```

## <a name="cmdlet-online-help-reference"></a><span data-ttu-id="4b6b9-151">A parancsmag online Súgó-hivatkozás</span><span class="sxs-lookup"><span data-stu-id="4b6b9-151">Cmdlet online help reference</span></span>

[<span data-ttu-id="4b6b9-152">Install-parancsfájl</span><span class="sxs-lookup"><span data-stu-id="4b6b9-152">Install-Script</span></span>](http://go.microsoft.com/fwlink/?LinkId=619784)

## <a name="example-commands"></a><span data-ttu-id="4b6b9-153">Példa parancsok</span><span class="sxs-lookup"><span data-stu-id="4b6b9-153">Example commands</span></span>

```powershell


# Piping Find-Script output to Install-Script cmdlet

Find-Script -Repository Local1 -Name Required-Script2

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script2                    local1               Description for the Required-Script2 script


Find-Script -Repository Local1 -Name Required-Script2 | Install-Script

Get-Command Required-Script2

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
ExternalScript  Required-Script2.ps1                                2.0       C:\Users\manikb\Documents\WindowsPowerShell\Scripts\Required-Script2.ps1


Get-InstalledScript Required-Script2

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script2                    local1               Description for the Required-Script2 script


Get-InstalledScript Required-Script2 | fl * -Force


Name                       : Required-Script2
Version                    : 2.5
Type                       : Script
Description                : Description for the Required-Script2 script
Author                     : manikb
CompanyName                :
Copyright                  : (c) 2015 Microsoft Corporation. All rights reserved.
PublishedDate              : 8/15/2015 12:42:39 AM
LicenseUri                 : http://required-script2.com/license
ProjectUri                 : http://required-script2.com/
IconUri                    : http://required-script2.com/icon
Tags                       : {Tag1, Tag2, Tag-Required-Script2-2.5, PSScript...}
Includes                   : {Function, DscResource, Cmdlet, Command}
PowerShellGetFormatVersion :
ReleaseNotes               : Required-Script2 release notes
Dependencies               : {}
RepositorySourceLocation   : http://manikb-dev:8765/api/v2/
Repository                 : local1
PackageManagementProvider  : NuGet
InstalledLocation          : C:\Users\manikb\Documents\WindowsPowerShell\Scripts


# Installing a script to AllUsers scope

Install-Script -Repository Local1 -Name Required-Script3 -Scope AllUsers
Get-InstalledScript -Name Required-Script3

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script3                    local1               Description for the Required-Script3 script


Get-InstalledScript -Name Required-Script3  | fl * -Force


Name                       : Required-Script3
Version                    : 2.5
Type                       : Script
Description                : Description for the Required-Script3 script
Author                     : manikb
CompanyName                :
Copyright                  : (c) 2015 Microsoft Corporation. All rights reserved.
PublishedDate              : 8/15/2015 12:42:45 AM
LicenseUri                 : http://required-script3.com/license
ProjectUri                 : http://required-script3.com/
IconUri                    : http://required-script3.com/icon
Tags                       : {Tag1, Tag2, Tag-Required-Script3-2.5, PSScript...}
Includes                   : {Function, DscResource, Cmdlet, Command}
PowerShellGetFormatVersion :
ReleaseNotes               : Required-Script3 release notes
Dependencies               : {}
RepositorySourceLocation   : http://manikb-dev:8765/api/v2/
Repository                 : local1
PackageManagementProvider  : NuGet
InstalledLocation          : C:\Program Files\WindowsPowerShell\Scripts


# Installing a script with dependent scripts and modules

Find-Script -Repository Local1 -Name Script-WithDependencies2 -IncludeDependencies

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.0        Script-WithDependencies2            local1               Description for the Script-WithDependencies2 script
2.5        RequiredModule1                     local1               RequiredModule1 module
2.5        RequiredModule2                     local1               RequiredModule2 module
2.5        RequiredModule3                     local1               RequiredModule3 module
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script


Install-Script -Repository Local1 -Name Script-WithDependencies2
Get-InstalledScript

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script
2.0        Script-WithDependencies2            local1               Description for the Script-WithDependencies2 script


Get-InstalledModule

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        RequiredModule1                     local1               RequiredModule1 module
2.5        RequiredModule2                     local1               RequiredModule2 module
2.5        RequiredModule3                     local1               RequiredModule3 module


Find-Script -Repository Local1 -Name Required-Script*

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script


Install-Script -Repository Local1 -Name Required-Script*

Get-InstalledScript

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
2.5        Required-Script1                    local1               Description for the Required-Script1 script
2.5        Required-Script2                    local1               Description for the Required-Script2 script
2.5        Required-Script3                    local1               Description for the Required-Script3 script


# Find a script and install it

# The first command finds the script named Required-Script2 from the Local1 repository and displays the results.
# The second command finds the Required-Script2 script, and then uses the pipeline operator to pass it to the Install-Script cmdlet to install it.
# The third command uses the Get-Command cmdlet to get Required-Script2, and then displays the results.
# The fourth command uses the Get-InstalledScript cmdlet to get Required-Script2 and display the results.
# The fifth command gets RequiredScript2 and uses the pipeline operator to pass it to the Format-List cmdlet to format the output.

Find-Script -Repository "Local1" -Name "Required-Script2"

Find-Script -Repository "Local1" -Name "Required-Script2" | Install-Script
Get-Command -Name "Required-Script2"

Get-InstalledScript -Name "Required-Script2"

Get-InstalledScript -Name "Required-Script2" | Format-List * 


# Install a script with AllUsers scope

# The first command installs the script named Required-Script3 and assigns it AllUsers scope.
# The second command gets the installed script Required-Script3 and displays information about it.
# The third command gets Required-Script3 and uses the pipeline operator to pass it to the Format-List cmdlet to format the output.

Install-Script -Repository "Local1" -Name "Required-Script3" -Scope "AllUsers"
Get-InstalledScript -Name "Required-Script3"
Get-InstalledScript -Name "Required-Script3" | Format-List * 


# Install a script with its dependent scripts and modules

# The first command finds the script named Script-WithDependencies2 and its dependencies in the Local1 repository and displays the results.
# The second command installs Script-WithDependencies2.
# The third command uses the Get-InstalledScript script cmdlet to get installed scripts and display the results.
# The fourth command uses the Get-InstalledModule cmdlet to get installed modules and display the results.
# The fifth command uses the Find-Script cmdlet to find scripts where the name begins with Required-Script and display the results.
# The sixth command installs the scripts where the name begins with Required-Script in the Local1 repository. 
# The final command gets installed scripts and displays the results.

Find-Script -Repository "Local1" -Name "Script-WithDependencies2" -IncludeDependencies
Install-Script -Repository "Local1" -Name "Script-WithDependencies2"
Get-InstalledScript
Get-InstalledModule
Find-Script -Repository "Local1" -Name "Required-Script*"
Install-Script -Repository "Local1" -Name "Required-Script*"
Get-InstalledScript

```

<span data-ttu-id="4b6b9-154">Get-parancs is használható – Name <InstalledScriptFileName> Letöltés helye.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-154">You can also use Get-Command –Name <InstalledScriptFileName> to get it.</span></span> <span data-ttu-id="4b6b9-155">A PATH környezeti változóba első használatát egy adott hatókör két telepítési helyek kerülnek.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-155">Two install locations are added to the PATH environment variable on first use of a specified scope.</span></span>
```powershell
$env:Path -split ';'| Where-Object {$\_} | Select-Object -Last 2
C:\\Program Files\\WindowsPowerShell\\Scripts
C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts

Get-Command Required-Script2
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Required-Script2.ps1 C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts\\Required-Script2.ps1
```

```powershell

# Install a module by name
Install-Script -Name MyDscModule

# Install multiple modules
Install-Script ContosoClient,ContosoServer

# Install a module using its minimum version
Install-Script -Name ContosoServer -MinimumVersion 1.0

# Install a specific version of a module
Install-Script -Name ContosoServer -RequiredVersion 1.1.3

# Install the latest version of a module to $home\Documents\WindowsPowerShell\Modules.
Install-Script -Name ContosoServer -Scope CurrentUser

# if a module is already available under $env:PSModulePath, below command fails with 'ModuleAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Script ContosoServer -RequiredVersion 1.5

# if a module is already available under $env:PSModulePath, below command fails with 'ModuleAlreadyInstalled,Install-Package,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage'
Install-Script ContosoServer -MinimumVersion 2.5

# Install multiple modules from multiple registered repositories
Install-Script ContosoClient,ContosoServer -Repository PSGallery, PrivatePSGallery

# Install a module with -WhatIf
Install-Script ContosoClient -WhatIf

# Install a module with -Confirm. A prompt will be displayed to confirm the installation.
Install-Script ContosoClient -WhatIf

# -Force option reinstalls the installed module
Install-Script ContosoClient -Force

# Install a module with dependencies
Install-Script -Name 


# Install a script from the registered repository with ScriptSourceLocation
Install-Script Connect-AzureVM

Version    Name                                Repository           Description
-------    ----                                ----------           -----------
1.0        Connect-AzureVM                     PSGallery            This runbook sets up a connection to an Azure vi...

# Find multiple scripts
Install-Script -Name Connect-AzureVM, Show-Tree, Connect-O365

# Find scripts with wildcards in -Name
Install-Script -Name *Azure*

# Find all versions of a script
Install-Script -Name Connect-O365 -AllVersions

# Find a script with -MinimumVersion. 
# With MinimumVersion we can find a script whose version is greate than or equal to the specified MinimumVersion value.
Install-Script Connect-O365 -MinimumVersion 1.4

# Find a script with MaximumVersion
Install-Script -Name Connect-O365 -MaximumVersion 1.6.2

# Find a script with both MinimumVersion and MaximumVersion range.
Install-Script -Name Connect-O365 -MinimumVersion 1.1 -MaximumVersion 1.6.2

# Installing a script to default AllUsers scope and with RequiredVersion
Install-Script -Name Connect-O365 -RequiredVersion 1.5.7

# Find a script from the specified repository
Install-Script -Name Fabrikam-ServerScript -Repository MyLocalRepo

# Find available scripts from all registered repositories
Install-Script

# Find available scripts from few registered repositories
Install-Script -Repository PSGallery, PrivatePSGallery

```

```powershell
 Added the logic for checking and failing the install script operation when there is a command with same name is already available on the system.
Also updated the prompt message.

 Examples:
PS C:\WINDOWS\system32> install-script get-childitem -Repository localrepo
install-script : A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.
At line:1 char:1
+ install-script get-childitem -Repository localrepo
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     + CategoryInfo          : InvalidOperation: (:) [Write-Error], WriteErrorException
     + FullyQualifiedErrorId : CommandAlreadyAvailableWitScriptName,Install-Script

 
 
 PS C:\WINDOWS\system32> install-script get-childitem,contosos -Repository localrepo
install-script : A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.
At line:1 char:1
+ install-script get-childitem,contosos -Repository localrepo
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     + CategoryInfo          : InvalidOperation: (:) [Write-Error], WriteErrorException
     + FullyQualifiedErrorId : CommandAlreadyAvailableWitScriptName,Install-Script

 PackageManagement\Install-Package : No match was found for the specified search criteria and script name 'contosos'. Try Get-ScriptRepository to see all available registered script repositories.
At C:\Program Files\WindowsPowerShell\Modules\powershellget\1.0.0.1\PSModule.psm1:2891 char:21
+ ...          $null = PackageManagement\Install-Package @PSBoundParameters
+                      ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
     + CategoryInfo          : ObjectNotFound: (Microsoft.Power....InstallPackage:InstallPackage) [Install-Package], Exception
     + FullyQualifiedErrorId : NoMatchFoundForCriteria,Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage

 PS C:\WINDOWS\system32>

 
 
 PS C:\WINDOWS\system32> find-script get-childitem -Repository localrepo | install-script
install-script : A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.
At line:1 char:51
+ find-script get-childitem -Repository localrepo | install-script
+                                                   ~~~~~~~~~~~~~~
     + CategoryInfo          : InvalidOperation: (:) [Write-Error], WriteErrorException
     + FullyQualifiedErrorId : CommandAlreadyAvailableWitScriptName,Install-Script

 
 PS C:\WINDOWS\system32>

 PS C:\WINDOWS\system32> Install-Package -Name Get-ChildItem -source LocalRepo  -ProviderName powershellget -Type Script
WARNING: A command with name 'get-childitem' is already available on this system. This script 'get-childitem' may override the existing command. If you still want to install this script 'get-childitem', use -Force parameter.

```

```powershell

Prompt ONCE per USER and per SCOPE for adding the script installation location to PATH environment variable.

- Prompt message for CurrentUser scope: (Complete message will be scrubbed later)

Acceptance required for adding the script installation locations to the PATH environment variable
The scripts install location 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts' is required to be added to the PATH environment variable in order to execute an installed script with only file name along with its script dependencies. If you accept this prompt, 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts' will be added to system specific PATH environment variable and process specific $env:PATH variable, if not already added. Otherwise you will have to use the full file path to  execute an installed script. Alternatively, you can use Save-Script cmdlet to download the script files to your favorite location. This prompt can be avoided and automatically considered as opted-out by adding 'C:\Users\manikb\Documents\WindowsPowerShell\Scripts' install location to the PATH environment variable or to the $env:PATH variable of current process. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):


- Prompt message for –AllUsers scope is same as above with $env:ProgramFiles\WindowsPowerShell\Scripts .

Acceptance required for adding the script installation locations to the PATH environment variable
The scripts install location 'C:\Program Files\WindowsPowerShell\Scripts' is required to be added to the PATH environment variable in order to execute an installed script with only file name along with its script dependencies. If you accept this prompt, 'C:\Program Files\WindowsPowerShell\Scripts' will be added to system specific PATH environment variable and process specific $env:PATH variable, if not already added. Otherwise you will have to use the full file path to  execute an installed script. Alternatively, you can use Save-Script cmdlet to download the script files to your favorite location. This prompt can be avoided and automatically considered as opted-out by adding 'C:\Program Files\WindowsPowerShell\Scripts' install location to the PATH environment variable or to the $env:PATH variable of current process. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):


- To prompt only once per scope, user acceptance for PATH variable change will be added to the user specific settings file under %localappdata%\Microsoft\windows\PowerShell\PowerShellGet
%localappdata%\Microsoft\windows\PowerShell\PowerShellGet\PowerShellGetSettings.XML. 
This settings file will be used to not prompt again.

After prompting for CurrentUser scope: 
    true or false for CurrentUserScope_AllowPATHChangeForScripts key based on user input.

After prompting for AllUsers scope: 
    true or false for AllUsersScope_AllowPATHChangeForScripts key based on user input.

- If user accepts the prompt
                Check and add $home\Documents\WindowsPowerShell\Scripts to user specific PATH environment variable.
                Check and add $env:ProgramFiles\WindowsPowerShell\Scripts to system specific PATH environment variable only when Install-Script cmdlet is used in an administrator process.
                Check and add above two paths to $env:PATH variable of the current process.

- If user denies the prompt, script installation will be proceeded without making any changes to the PATH environment variable.



Example:             
PS C:\windows\system32> Install-Script -Name $scriptName -Repository $repositoryName -Scope $Scope -Verbose

Acceptance required for adding the script installation locations to the PATH environment variable
The scripts install location 'C:\Program Files\WindowsPowerShell\Scripts' is required to be added to the PATH environment variable in order to execute an installed script with only file name along with its script dependencies. If you accept this prompt, 'C:\Program Files\WindowsPowerShell\Scripts' will be added to system specific PATH environment variable and process specific $env:PATH variable, if not already added. Otherwise you will have to use the full file path to  execute an installed script. Alternatively, you can use Save-Script cmdlet to download the script files to your favorite location. This prompt can be avoided and automatically considered as opted-out by adding 'C:\Program Files\WindowsPowerShell\Scripts' install location to the PATH environment variable or to the $env:PATH variable of current process. Do you want to continue?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n


```

## <a name="install-script-cmdlet-in-pipeline-operations"></a><span data-ttu-id="4b6b9-156">A feldolgozási sor műveletek telepítési parancsfájl-parancsmag</span><span class="sxs-lookup"><span data-stu-id="4b6b9-156">Install-Script cmdlet in pipeline operations</span></span>

```powershell

# Find a module and install it
Find-Script -Name "MyDSC*" | Install-Script

# Find a module and install it to the CurrentUser scope
Find-Script -Name "MyDSC*" | Install-Script -Scope CurrentUser

# Find commands by name and install them
# The first command finds the specified commands in the INT repository, and then uses the pipeline operator to pass them to Install-Script to install them.
# The second command uses Get-InstalledModule to verify the modules from the prior command are installed.
Find-Command -Repository "INT" -Name Get-ContosoClient,Get-ContosoServer | Install-Script
Get-InstalledModule

# This command finds the resource named MyResource and passes it to the Install-Script cmdlet by using the pipeline operator. The Install-Script cmdlet installs the module for the resource. 
# If you pipe multiple resources to the Install-Script cmdlet from the same module, Install-Script attempts to install the module only once. 
Find-DscResource -Name "MyResource" | Install-Script
Get-InstalledModule

# Find multiple role capabilities and install them
Find-RoleCapability -Name MyJeaRole, Maintenance | Install-Script
Get-InstalledModule

```

## <a name="side-by-side-version-support-on-powershell-50-or-newer"></a><span data-ttu-id="4b6b9-157">Egymás melletti verzióinak támogatása PowerShell 5.0-s vagy újabb</span><span class="sxs-lookup"><span data-stu-id="4b6b9-157">Side-by-Side Version Support on PowerShell 5.0 or newer</span></span>

<span data-ttu-id="4b6b9-158">PowerShellGet támogatja az egymás melletti (SxS) modul által támogatott verzió telepítési-parancsfájl, a frissítés-parancsfájl, és a közzététel-parancsfájl parancsmagok a Windows PowerShell 5.0-s vagy újabb rendszerű.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-158">PowerShellGet supports the side-by-side (SxS) module version support in Install-Script, Update-Script, and Publish-Script cmdlets that run in Windows PowerShell 5.0 or newer.</span></span>

### <a name="install-script-examples"></a><span data-ttu-id="4b6b9-159">Telepítési parancsfájl-példák</span><span class="sxs-lookup"><span data-stu-id="4b6b9-159">Install-Script examples</span></span>

```powershell
# Install a version of the module
Install-Script -Name PSScriptAnalyzer -RequiredVersion 1.1.0 -Repository PSGallery
Get-Script -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

Name : PSScriptAnalyzer
Version : 1.1.0
ModuleBase : C:\Program Files\WindowsPowerShell\Modules\PSScriptAnalyzer\1.1.0

# Install another version of the module in Side-by-Side with already installed version.
Install-Script -Name PSScriptAnalyzer -RequiredVersion 1.1.1 -Repository PSGallery
Get-Script -ListAvailable -Name PSScriptAnalyzer | Format-List Name,Version,ModuleBase

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

## <a name="install-module-with-its-dependencies"></a><span data-ttu-id="4b6b9-160">A függőségekkel rendelkező modul telepítése</span><span class="sxs-lookup"><span data-stu-id="4b6b9-160">Install module with its dependencies</span></span>

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
Install-Script -Name TypePx -Repository PSGallery -Verbose

VERBOSE: Repository details, Name = 'PSGallery', Location = 'https://www.powershellgallery.com/api/v2/'; IsTrusted =
'False'; IsRegistered = 'True'.
VERBOSE: Using the provider 'PowerShellGet' for searching packages.
VERBOSE: Using the specified source names : 'PSGallery'.
VERBOSE: Getting the provider object for the PackageManagement Provider 'NuGet'.
VERBOSE: The specified Location is 'https://www.powershellgallery.com/api/v2/' and PackageManagementProvider is
'NuGet'.
VERBOSE: Searching repository 'https://www.powershellgallery.com/api/v2/FindPackagesById()?id='TypePx'' for ''.
VERBOSE: Total package yield:'1' for the specified package 'TypePx'.
VERBOSE: Performing the operation "Install-Script" on target "Version '2.0.1.20' of module 'TypePx'".

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

## <a name="error-scenarios"></a><span data-ttu-id="4b6b9-161">Hiba forgatókönyvek</span><span class="sxs-lookup"><span data-stu-id="4b6b9-161">Error scenarios</span></span>

```powershell

# Below command fails with 'NameShouldNotContainWildcardCharacters,Install-Script'
Install-Script ContosoServe*

# Below command fails with 'VersionRangeAndRequiredVersionCannotBeSpecifiedTogether,Install-Script'
Install-Script ContosoServer -MinimumVersion 1.0 -RequiredVersion 5.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Script'
Install-Script ContosoClient,ContosoServer -RequiredVersion 2.0

# Below command fails with 'VersionParametersAreAllowedOnlyWithSingleName,Install-Script'
Install-Script ContosoClient,ContosoServer -MinimumVersion 2.0

```

## <a name="installing-a-script-with-dependent-scripts-and-modules"></a><span data-ttu-id="4b6b9-162">Parancsfájl a függő parancsfájlok és a modulok telepítése</span><span class="sxs-lookup"><span data-stu-id="4b6b9-162">Installing a script with dependent scripts and modules</span></span>

```powershell
# Installing a script with dependent scripts and modules
Find-Script -Repository GalleryINT -Name Script-WithDependencies2 -IncludeDependencies
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
2.5 RequiredModule1 Module GalleryINT RequiredModule1 module
2.5 RequiredModule2 Module GalleryINT RequiredModule2 module
2.5 RequiredModule3 Module GalleryINT RequiredModule3 module
2.0 RequiredModule4 Module GalleryINT RequiredModule4 module
1.5 RequiredModule5 Module GalleryINT RequiredModule5 module
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.5 Required-Script3 Script GalleryINT Description for the Required-Script3 script

Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
Get-InstalledModule
Install-Script -Repository GalleryINT -Name Script-WithDependencies2 -Scope CurrentUser
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
Get-InstalledModule
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 RequiredModule1 Module GalleryINT RequiredModule1 module
2.5 RequiredModule2 Module GalleryINT RequiredModule2 module
2.5 RequiredModule3 Module GalleryINT RequiredModule3 module
2.0 RequiredModule4 Module GalleryINT RequiredModule4 module
1.5 RequiredModule5 Module GalleryINT RequiredModule5 module

# Contents of Script-WithDependencies2 file.
<#PSScriptInfo
.VERSION 2.0
.GUID 90082fa1-0b84-49fb-a00e-0a624fbb6584
.AUTHOR manikb
.COMPANYNAME Microsoft Corporation
.COPYRIGHT (c) 2015 Microsoft Corporation. All rights reserved.
.TAGS Tag1 Tag2 Tag-Script-WithDependencies2-2.0
.LICENSEURI http://script-withdependencies2.com/license
.PROJECTURI http://script-withdependencies2.com/
.ICONURI http://script-withdependencies2.com/icon
.EXTERNALMODULEDEPENDENCIES
.REQUIREDSCRIPTS Required-Script1,Required-Script2,Required-Script3
.EXTERNALSCRIPTDEPENDENCIES
.RELEASENOTES
Script-WithDependencies2 release notes
#>
#Requires -Module RequiredModule1
#Requires -Module @{ModuleName = 'RequiredModule2'; ModuleVersion = '2.0'}
#Requires -Module @{RequiredVersion = '2.5'; ModuleName = 'RequiredModule3'}
#Requires -Module @{ModuleVersion = '1.1'; ModuleName = 'RequiredModule4'; MaximumVersion = '2.0'}
#Requires -Module @{MaximumVersion = '1.5'; ModuleName = 'RequiredModule5'}
<#
.DESCRIPTION
Description for the Script-WithDependencies2 script
#>
Param()
Function Test-FunctionFromScript\_Script-WithDependencies2 { Get-Date }
Workflow Test-WorkflowFromScript\_Script-WithDependencies2 { Get-Date }
```

## <a name="install-script-and-get-installedscript-cmdlets"></a><span data-ttu-id="4b6b9-163">Telepítési-parancsfájlt és a Get-InstalledScript parancsmagok</span><span class="sxs-lookup"><span data-stu-id="4b6b9-163">Install-Script and Get-InstalledScript cmdlets</span></span>
<span data-ttu-id="4b6b9-164">Install-parancsfájl parancsmag lehetővé teszi egy adott parancsfájl és függőségeinek telepítése a megadott hatókörben.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-164">Install-Script cmdlet lets you to install a specific script file along with its dependencies to the specified scope.</span></span> <span data-ttu-id="4b6b9-165">Alapértelmezés szerint a parancsfájlok telepítve vannak az AllUsers hatókörre.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-165">By default, scripts are installed to the AllUsers scope.</span></span> <span data-ttu-id="4b6b9-166">Get-InstalledScript parancsmag lehetővé teszi a parancsprogramok, amely a telepítési parancsfájl-parancsmag használatával telepített listájának lekérdezése.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-166">Get-InstalledScript cmdlet lets you to get the list of script files which were installed using Install-Script cmdlet.</span></span>

<span data-ttu-id="4b6b9-167">Használjon Megjegyzés: ahhoz, hogy a felügyeleti és parancsfájlok megkeresése, ha telepítve vannak, Install parancsprogramot fog hozzon létre egy $home\Documents\WindowsPowerShell\Scripts scripts tárolására szolgáló alapértelmezett mappát, és mappában hozzáadni az elérési út környezethez.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-167">Use note: To allow management and locating of scripts once they are installed, Install-script will create a default folder for storing scripts at $home\Documents\WindowsPowerShell\Scripts, and add that folder to your PATH environment.</span></span> <span data-ttu-id="4b6b9-168">Az elérési út fontos, ha az Install-parancsfájl helyett Mentés-parancsfájl használatával.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-168">If modifying the path is a concern, use Save-Script instead of Install-Script.</span></span> <span data-ttu-id="4b6b9-169">Get-InstalledScripts és eltávolítás parancsfájl-csak együttműködhet parancsfájl helyezve a rendszer telepítse-parancsfájl használatával.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-169">Get-InstalledScripts and Uninstall-Script can only work with scripts placed on the system using Install-Script.</span></span>
```powershell
# Install locations for scripts:
# Default scope is AllUsers.
# AllUsers scope --> "$env:ProgramFiles\\WindowsPowerShell\\Scripts"
# CurrentUser scope -->; "$env:USERPROFILE\\Documents\\WindowsPowerShell\\Scripts"

# Piping Find-Script output to Install-Script cmdlet
Find-Script -Repository GalleryINT -Name Required-Script2 | Install-Script -Scope CurrentUser -Verbose
VERBOSE: Repository details, Name = 'GalleryINT', Location = 'https://customgallery.cloudapp.net/api/v2/'; IsTrusted = 'True'; IsRegistered = 'True'.
VERBOSE: Performing the operation "Install-Script" on target "Version '2.5' of script 'Required-Script2'".
VERBOSE: Using the provider 'PowerShellGet' for searching packages.
VERBOSE: Using the specified source names : 'GalleryINT'.
VERBOSE: Getting the provider object for the PackageManagement Provider 'NuGet'.
VERBOSE: The specified Location is 'https://customgallery.cloudapp.net/api/v2/items/psscript/' and PackageManagementProvider is 'NuGet'.
VERBOSE: Searching repository 'https://customgallery.cloudapp.net/api/v2/items/psscript/FindPackagesById()?id='Required-Script2'' for ''.
VERBOSE: Total package yield:'1' for the specified package 'Required-Script2'.
VERBOSE: Performing the operation "Install-Script" on target "Version '2.5' of script 'Required-Script2'".
VERBOSE: The installation scope is specified to be 'CurrentUser'.
VERBOSE: The specified script will be installed in 'C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts' and its dependent modules will be installed in
'C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Modules'.
VERBOSE: The specified Location is 'NuGet' and PackageManagementProvider is 'NuGet'.
VERBOSE: Downloading script 'Required-Script2' with version '2.5' from the repository 'https://customgallery.cloudapp.net/api/v2/items/psscript/'.
VERBOSE: Script 'Required-Script2' was installed successfully.

Get-InstalledScript Required-Scri\*
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script

Get-InstalledScript Required-Script2 | Format-List \* -Force
Name : Required-Script2
Version : 2.5
Type : Script
Description : Description for the Required-Script2 script
Author : manikb
CompanyName :
Copyright : (c) 2015 Microsoft Corporation. All rights reserved.
PublishedDate : 10/30/2015 1:25:15 AM
LicenseUri : http://required-script2.com/license
ProjectUri : http://required-script2.com/
IconUri : http://required-script2.com/icon
Tags : {Tag1, Tag2, Tag-Required-Script2-2.5, PSScript}
Includes : {Function, DscResource, Cmdlet, Workflow...}
PowerShellGetFormatVersion :
ReleaseNotes : Required-Script2 release notes
Dependencies : {}
RepositorySourceLocation : https://customgallery.cloudapp.net/api/v2/
Repository : GalleryINT
PackageManagementProvider : NuGet
AdditionalMetadata : {Type, releaseNotes, copyright, PackageManagementProvider...}
InstalledLocation : C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts

Installed script file is immediately available for usage.
```

<span data-ttu-id="4b6b9-170">Get-parancs is használható – Name <InstalledScriptFileName> Letöltés helye.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-170">You can also use Get-Command –Name <InstalledScriptFileName> to get it.</span></span> <span data-ttu-id="4b6b9-171">A PATH környezeti változóba első használatát egy adott hatókör két telepítési helyek kerülnek.</span><span class="sxs-lookup"><span data-stu-id="4b6b9-171">Two install locations are added to the PATH environment variable on first use of a specified scope.</span></span>
```powershell
$env:Path -split ';'| Where-Object {$\_} | Select-Object -Last 2
C:\\Program Files\\WindowsPowerShell\\Scripts
C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts

Get-Command Required-Script2
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Required-Script2.ps1 C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts\\Required-Script2.ps1

Find-Script -Repository LocalRepo1 -Name Demo-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.0 Demo-Script Script LocalRepo1 Script file description goes here

Find-Script -Repository LocalRepo1 -Name Demo-Script | Install-Script -Scope CurrentUser
Untrusted repository
You are installing the scripts from an untrusted repository. If you trust this repository, change its InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the scripts from 'C:\\MyLocalRepo'?
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "N"): Y

Get-InstalledScript Demo-Script
Version Name Type Repository Description
------- ---- ---- ---------- -----------
1.0 Demo-Script Script LocalRepo1 Script file description goes here

Get-Command Demo-Script
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Demo-Script.ps1 C:\\Users\\manikb\\Documents\\WindowsPowerShell\\Scripts\\Demo-Script.ps1

# Using the installed script
Demo-Script
Demo-ScriptFunction
Demo-ScriptWorkflow

# Installing a script to default AllUsers scope and with RequiredVersion
Install-Script -Repository GalleryINT -Name Required-Script3 -RequiredVersion 2.0
Get-InstalledScript -Name Required-Script3

Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
Get-InstalledScript -Name Required-Script3 | Format-List Name,InstalledLocation -Force
Name : Required-Script3
InstalledLocation : C:\\Program Files\\WindowsPowerShell\\Scripts

Get-Command Required-Script3
CommandType Name Version Source
----------- ---- ------- ------
ExternalScript Required-Script3.ps1 C:\\Program Files\\WindowsPowerShell\\Scripts\\Required-Script3.ps1

# Installing a script with dependent scripts and modules
Find-Script -Repository GalleryINT -Name Script-WithDependencies2 -IncludeDependencies
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
2.5 RequiredModule1 Module GalleryINT RequiredModule1 module
2.5 RequiredModule2 Module GalleryINT RequiredModule2 module
2.5 RequiredModule3 Module GalleryINT RequiredModule3 module
2.0 RequiredModule4 Module GalleryINT RequiredModule4 module
1.5 RequiredModule5 Module GalleryINT RequiredModule5 module
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.5 Required-Script3 Script GalleryINT Description for the Required-Script3 script

Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
Get-InstalledModule
Install-Script -Repository GalleryINT -Name Script-WithDependencies2 -Scope CurrentUser
Get-InstalledScript
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.0 Required-Script3 Script GalleryINT Description for the Required-Script3 script
1.0 Demo-Script Script LocalRepo1 Script file description goes here
2.5 Required-Script1 Script GalleryINT Description for the Required-Script1 script
2.5 Required-Script2 Script GalleryINT Description for the Required-Script2 script
2.0 Script-WithDependencies2 Script GalleryINT Description for the Script-WithDependencies2 script
Get-InstalledModule
Version Name Type Repository Description
------- ---- ---- ---------- -----------
2.5 RequiredModule1 Module GalleryINT RequiredModule1 module
2.5 RequiredModule2 Module GalleryINT RequiredModule2 module
2.5 RequiredModule3 Module GalleryINT RequiredModule3 module
2.0 RequiredModule4 Module GalleryINT RequiredModule4 module
1.5 RequiredModule5 Module GalleryINT RequiredModule5 module

# Contents of Script-WithDependencies2 file.
<#PSScriptInfo
.VERSION 2.0
.GUID 90082fa1-0b84-49fb-a00e-0a624fbb6584
.AUTHOR manikb
.COMPANYNAME Microsoft Corporation
.COPYRIGHT (c) 2015 Microsoft Corporation. All rights reserved.
.TAGS Tag1 Tag2 Tag-Script-WithDependencies2-2.0
.LICENSEURI http://script-withdependencies2.com/license
.PROJECTURI http://script-withdependencies2.com/
.ICONURI http://script-withdependencies2.com/icon
.EXTERNALMODULEDEPENDENCIES
.REQUIREDSCRIPTS Required-Script1,Required-Script2,Required-Script3
.EXTERNALSCRIPTDEPENDENCIES
.RELEASENOTES
Script-WithDependencies2 release notes
#>
#Requires -Module RequiredModule1
#Requires -Module @{ModuleName = 'RequiredModule2'; ModuleVersion = '2.0'}
#Requires -Module @{RequiredVersion = '2.5'; ModuleName = 'RequiredModule3'}
#Requires -Module @{ModuleVersion = '1.1'; ModuleName = 'RequiredModule4'; MaximumVersion = '2.0'}
#Requires -Module @{MaximumVersion = '1.5'; ModuleName = 'RequiredModule5'}
<#
.DESCRIPTION
Description for the Script-WithDependencies2 script
#>
Param()
Function Test-FunctionFromScript\_Script-WithDependencies2 { Get-Date }
Workflow Test-WorkflowFromScript\_Script-WithDependencies2 { Get-Date }
```

