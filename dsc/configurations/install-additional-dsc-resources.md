---
ms.date: 12/12/2018
keywords: DSC, powershell, erőforrás, katalógus, beállítása
title: További DSC-erőforrások telepítése
ms.openlocfilehash: ecaf176230ccd934b57b1c27d72ff83e6ba906e9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686382"
---
# <a name="install-additional-dsc-resources"></a><span data-ttu-id="200e7-103">További DSC-erőforrások telepítése</span><span class="sxs-lookup"><span data-stu-id="200e7-103">Install Additional DSC Resources</span></span>

<span data-ttu-id="200e7-104">PowerShell Desired State Configuration (DSC) tartalmaz a több-az-beépített erőforrás.</span><span class="sxs-lookup"><span data-stu-id="200e7-104">PowerShell includes several Out-of-the-box resources for Desired State Configuration (DSC).</span></span> <span data-ttu-id="200e7-105">A **PSDesiredStateConfiguration** modul tartalmazza az összes elérhető a PowerShell, a meghatározott példányának OOB DSC-erőforrások.</span><span class="sxs-lookup"><span data-stu-id="200e7-105">The **PSDesiredStateConfiguration** module contains all of the OOB DSC resources available on your specific instance of PowerShell.</span></span>

<span data-ttu-id="200e7-106">Ez az a PowerShell 4.0-s verzióját és leírását, az erőforrás-funkciókat az OOB-erőforrások listáját.</span><span class="sxs-lookup"><span data-stu-id="200e7-106">This is a list of the OOB resources included in PowerShell 4.0 and a description of the resource's capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="200e7-107">Ez a lehetőség egy nem teljes listája az OOB-erőforrások számát az egyes PowerShell-verzió nőtt.</span><span class="sxs-lookup"><span data-stu-id="200e7-107">This is an incomplete list, as the number of OOB resources has grown with each version of PowerShell.</span></span>

|<span data-ttu-id="200e7-108">Forrásanyag</span><span class="sxs-lookup"><span data-stu-id="200e7-108">Resource</span></span>  |<span data-ttu-id="200e7-109">Leírás</span><span class="sxs-lookup"><span data-stu-id="200e7-109">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="200e7-110">**Fájl**</span><span class="sxs-lookup"><span data-stu-id="200e7-110">**File**</span></span>|<span data-ttu-id="200e7-111">Fájlok és könyvtárak állapotát vezérli.</span><span class="sxs-lookup"><span data-stu-id="200e7-111">Controls the state of files and directories.</span></span> <span data-ttu-id="200e7-112">Átmásolja a fájlokat egy **forrás** , egy **cél** frissíti őket, és amikor a **forrás** módosítások összehasonlítja a dátumok, az ellenőrzőösszegek és kivonatokat.</span><span class="sxs-lookup"><span data-stu-id="200e7-112">Copies files from a **Source** to a **Destination** and updates them when the **Source** changes by comparing dates, checksums, and hashes.</span></span>|
|<span data-ttu-id="200e7-113">**Archívum**</span><span class="sxs-lookup"><span data-stu-id="200e7-113">**Archive**</span></span>|<span data-ttu-id="200e7-114">Kibontja a archívumok és a egy adott helyre.</span><span class="sxs-lookup"><span data-stu-id="200e7-114">Unpacks archives and a specified location.</span></span> <span data-ttu-id="200e7-115">Ellenőrzi a megadott archívum **ellenőrzőösszeg**.</span><span class="sxs-lookup"><span data-stu-id="200e7-115">Validates the archives with a specified **Checksum**.</span></span>|
|<span data-ttu-id="200e7-116">**Környezet**</span><span class="sxs-lookup"><span data-stu-id="200e7-116">**Environment**</span></span>|<span data-ttu-id="200e7-117">Kezeli a környezeti változókat.</span><span class="sxs-lookup"><span data-stu-id="200e7-117">Manages environment variables.</span></span>|
|<span data-ttu-id="200e7-118">**Csoport**</span><span class="sxs-lookup"><span data-stu-id="200e7-118">**Group**</span></span>|<span data-ttu-id="200e7-119">Helyi csoportok kezeli, és ellenőrzi a csoport tagságát.</span><span class="sxs-lookup"><span data-stu-id="200e7-119">Manages local groups and controls group membership.</span></span>|
|<span data-ttu-id="200e7-120">**Log**</span><span class="sxs-lookup"><span data-stu-id="200e7-120">**Log**</span></span>|<span data-ttu-id="200e7-121">Írja az üzeneteket a `Microsoft-Windows-Desired State Configuration/Analytic` Eseménynapló.</span><span class="sxs-lookup"><span data-stu-id="200e7-121">Writes messages to the `Microsoft-Windows-Desired State Configuration/Analytic` event log.</span></span>|
|<span data-ttu-id="200e7-122">**Csomag**</span><span class="sxs-lookup"><span data-stu-id="200e7-122">**Package**</span></span>|<span data-ttu-id="200e7-123">Telepíti vagy eltávolítja a csomagokat **argumentumok**, **LogPath**, **ReturnCode**, egyéb beállításokat.</span><span class="sxs-lookup"><span data-stu-id="200e7-123">Installs or uninstalls packages using **Arguments**, **LogPath**, **ReturnCode**, other settings.</span></span>|
|<span data-ttu-id="200e7-124">**Registry**</span><span class="sxs-lookup"><span data-stu-id="200e7-124">**Registry**</span></span>|<span data-ttu-id="200e7-125">Kezeli a beállításjegyzék-kulcsokat és értékeket.</span><span class="sxs-lookup"><span data-stu-id="200e7-125">Manages registry keys and values.</span></span>|
|<span data-ttu-id="200e7-126">**Parancsfájl**</span><span class="sxs-lookup"><span data-stu-id="200e7-126">**Script**</span></span>|<span data-ttu-id="200e7-127">Lehetővé teszi, hogy tervezheti meg a saját [get-teszt – set](../resources/get-test-set.md) parancsfájl-blokk.</span><span class="sxs-lookup"><span data-stu-id="200e7-127">Allows you to design your own [get-test-set](../resources/get-test-set.md) script blocks.</span></span>|
|<span data-ttu-id="200e7-128">**Service**</span><span class="sxs-lookup"><span data-stu-id="200e7-128">**Service**</span></span>|<span data-ttu-id="200e7-129">Konfigurálja a Windows-szolgáltatások.</span><span class="sxs-lookup"><span data-stu-id="200e7-129">Configures Windows services.</span></span>|
|<span data-ttu-id="200e7-130">**Felhasználó**</span><span class="sxs-lookup"><span data-stu-id="200e7-130">**User**</span></span> |<span data-ttu-id="200e7-131">A helyi felhasználók és attribútumok kezeli.</span><span class="sxs-lookup"><span data-stu-id="200e7-131">Manages local users and attributes.</span></span>|
|<span data-ttu-id="200e7-132">**WindowsFeature**</span><span class="sxs-lookup"><span data-stu-id="200e7-132">**WindowsFeature**</span></span>|<span data-ttu-id="200e7-133">Szerepkörök és szolgáltatások kezelése.</span><span class="sxs-lookup"><span data-stu-id="200e7-133">Manages roles and features.</span></span>|
|<span data-ttu-id="200e7-134">**WindowsProcess**</span><span class="sxs-lookup"><span data-stu-id="200e7-134">**WindowsProcess**</span></span>|<span data-ttu-id="200e7-135">Konfigurálja a Windows folyamatokat.</span><span class="sxs-lookup"><span data-stu-id="200e7-135">Configures Windows processes.</span></span>|

<span data-ttu-id="200e7-136">Az OOB-erőforrások lehetővé teszik a gyakori műveletekhez egy jó kiindulási pont.</span><span class="sxs-lookup"><span data-stu-id="200e7-136">The OOB resources allow a good starting point for common operations.</span></span> <span data-ttu-id="200e7-137">Ha az OOB-erőforrások nem felelnek meg igényeinek, írhat saját [egyéni erőforrás](../resources/authoringResource.md).</span><span class="sxs-lookup"><span data-stu-id="200e7-137">If the OOB resources do not meet your needs, you can write your own [Custom Resource](../resources/authoringResource.md).</span></span> <span data-ttu-id="200e7-138">Ír egy egyéni erőforrás megoldani a problémát, mielőtt a DSC-erőforrások, Microsoft és a PowerShell-Közösség által létrehozott hatalmas számát keresztül kell keresnie.</span><span class="sxs-lookup"><span data-stu-id="200e7-138">Before you write a custom resource to solve your problem, you should look through the vast number of DSC resources that have already been created by both Microsoft and the PowerShell community.</span></span>

<span data-ttu-id="200e7-139">DSC-erőforrások is talál a [PowerShell-galériából](https://www.powershellgallery.com/) és [GitHub](https://github.com/).</span><span class="sxs-lookup"><span data-stu-id="200e7-139">You can find DSC resources in both the [PowerShell Gallery](https://www.powershellgallery.com/) and [GitHub](https://github.com/).</span></span> <span data-ttu-id="200e7-140">DSC-erőforrások is telepítheti közvetlenül a PowerShell konzol használata a [PowerShellGet](/powershell/module/powershellget/).</span><span class="sxs-lookup"><span data-stu-id="200e7-140">You can also install DSC resources directly from the PowerShell console using [PowerShellGet](/powershell/module/powershellget/).</span></span>

## <a name="installing-powershellget"></a><span data-ttu-id="200e7-141">A PowerShellGet telepítése</span><span class="sxs-lookup"><span data-stu-id="200e7-141">Installing PowerShellGet</span></span>

<span data-ttu-id="200e7-142">Annak megállapításához, ha már rendelkezik **PowerShell** beszerzése, illetve telepíti azt segítséget szeretne kérni, tekintse meg a következő útmutatót: [A PowerShellGet telepítése](/powershell/gallery/installing-psget).</span><span class="sxs-lookup"><span data-stu-id="200e7-142">To determine if you already have **PowerShell** get, or to get help installing it, see the following guide: [Installing PowerShellGet](/powershell/gallery/installing-psget).</span></span>

## <a name="finding-dsc-resources-using-powershellget"></a><span data-ttu-id="200e7-143">A PowerShellGet-modul DSC-erőforrások keresése</span><span class="sxs-lookup"><span data-stu-id="200e7-143">Finding DSC resources using PowerShellGet</span></span>

<span data-ttu-id="200e7-144">Egyszer **PowerShellGet** van telepítve a rendszerén, keresése és telepítése lévő üzemeltetett DSC-erőforrások a [PowerShell-galériából](https://www.powershellgallery.com/).</span><span class="sxs-lookup"><span data-stu-id="200e7-144">Once **PowerShellGet** is installed on your system, you can find and install DSC resources hosted in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>

<span data-ttu-id="200e7-145">Először a [Find-DSCResource](/powershell/module/powershellget/find-dscresource) parancsmag DSC-erőforrások megkereséséhez.</span><span class="sxs-lookup"><span data-stu-id="200e7-145">First, use the [Find-DSCResource](/powershell/module/powershellget/find-dscresource) cmdlet to find DSC resources.</span></span> <span data-ttu-id="200e7-146">Futtatásakor `Find-DSCResource` , először, a következő üzenet jelenik meg a "NuGet-szolgáltató" telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="200e7-146">When you run `Find-DSCResource` for the first time, you see the following prompt to install the "NuGet provider".</span></span>

```
PS> Find-DSCResource

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The
NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\xAdministrator\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider
 by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to
install and import the NuGet provider now?
[Y] Yes  [N] No  [?] Help (default is "Y"):
```

<span data-ttu-id="200e7-147">Után lenyomja "y" a "NuGet" szolgáltató van telepítve, telepítheti a PowerShell-galériából DSC-erőforrások listájának megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="200e7-147">After pressing 'y', the "NuGet" provider is installed, you see a list of DSC resources that you can install from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="200e7-148">Listán nem jelenik meg, mert nagyon nagy méretű.</span><span class="sxs-lookup"><span data-stu-id="200e7-148">List is not shown because it is very large.</span></span>

<span data-ttu-id="200e7-149">Azt is megadhatja a `-Name` helyettesítő karaktereket használ, paraméter vagy `-Filter` paraméter a keresés szűkítéséhez helyettesítő karakterek nélkül.</span><span class="sxs-lookup"><span data-stu-id="200e7-149">You can also specify the `-Name` parameter using wildcards, or `-Filter` parameter without wildcards to narrow down your search.</span></span> <span data-ttu-id="200e7-150">Ebben a példában megkísérli megtalálni a helyettesítő karakterek használatával "Időzóna" DSC erőforrás.</span><span class="sxs-lookup"><span data-stu-id="200e7-150">This example attempts to find a "TimeZone" DSC resource using the wildcards.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="200e7-151">Jelenleg nincs tárkötetek a `Find-DSCResource` parancsmagot, amely megakadályozza, hogy a helyettesítő karakterek használatával is a `-Name` és `-Filter` paramétereket.</span><span class="sxs-lookup"><span data-stu-id="200e7-151">Currently there is a bug in the `Find-DSCResource` cmdlet that prevents using wildcards in both the `-Name` and `-Filter` parameters.</span></span> <span data-ttu-id="200e7-152">A lenti második példában látható, hogy egy megkerülő megoldás az `Where-Object`.</span><span class="sxs-lookup"><span data-stu-id="200e7-152">The second example below shows a workaround using `Where-Object`.</span></span>

```
PS> Find-DSCResource -Name *Time*

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Carbon_EnvironmentVariable          2.6.0      Carbon                              PSGallery
Carbon_FirewallRule                 2.6.0      Carbon                              PSGallery
Carbon_Group                        2.6.0      Carbon                              PSGallery
Carbon_IniFile                      2.6.0      Carbon                              PSGallery
Carbon_Permission                   2.6.0      Carbon                              PSGallery
Carbon_Privilege                    2.6.0      Carbon                              PSGallery
Carbon_ScheduledTask                2.6.0      Carbon                              PSGallery
Carbon_Service                      2.6.0      Carbon                              PSGallery
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
xTimeZone                           1.8.0.0    xTimeZone                           PSGallery
xSqlServerDefaultDir                1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerMoveDatabaseFiles         1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerSQLDataRoot               1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerStartupParam              1.0.0      mlSqlServerDSC                      PSGallery
```

<span data-ttu-id="200e7-153">Is `Where-Object` szűrés részletesebb DSC-erőforrások megkereséséhez.</span><span class="sxs-lookup"><span data-stu-id="200e7-153">You can also use `Where-Object` to find DSC resources with more granular filtering.</span></span> <span data-ttu-id="200e7-154">Ez a megközelítés a szűrési paramétereket lévő beépített lassabb lesz.</span><span class="sxs-lookup"><span data-stu-id="200e7-154">This approach will be slower than using built in filtering parameters.</span></span>

```
PS> Find-DSCResource | Where-Object {$_.Name -like "Time*"}

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
```

<span data-ttu-id="200e7-155">A szűrés további információkért lásd: [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span><span class="sxs-lookup"><span data-stu-id="200e7-155">For more information on filtering, see [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span></span>

## <a name="installing-dsc-resources-using-powershellget"></a><span data-ttu-id="200e7-156">DSC-erőforrások a PowerShellGet-modul telepítése</span><span class="sxs-lookup"><span data-stu-id="200e7-156">Installing DSC Resources using PowerShellGet</span></span>

<span data-ttu-id="200e7-157">A DSC-erőforrások telepítéséhez használja a [Install-Module](/powershell/module/PowershellGet/Install-Module) megadása mezőben látható a modul neve, a parancsmag **modul** nevét a keresési eredmények között.</span><span class="sxs-lookup"><span data-stu-id="200e7-157">To install a DSC resource, use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet, specifying the name of the module shown under **Module** name in your search results.</span></span>

<span data-ttu-id="200e7-158">A "Időzóna" erőforrás ezért ez a modul telepíti a ebben a példában a "ComputerManagementDSC" modul létezik.</span><span class="sxs-lookup"><span data-stu-id="200e7-158">The "TimeZone" resource exists in the "ComputerManagementDSC" module, so that is the module this example installs.</span></span>

> [!NOTE]
> <span data-ttu-id="200e7-159">Nem bízik meg a PowerShell-galériából, ha az alábbi megerősítés a figyelmeztetést látja, és amely az ezt követő utasításokat elkerülésével telepíti.</span><span class="sxs-lookup"><span data-stu-id="200e7-159">If you have not trusted the PowerShell gallery, you see the warning below asking for confirmation, and instructing you how to avoid subsequent prompts on installs.</span></span>

```
PS> Install-Module -Name ComputerManagementDSC

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="200e7-160">Nyomja le az "y", a modul telepítésének folytatásához.</span><span class="sxs-lookup"><span data-stu-id="200e7-160">Press 'y' to continue installing the module.</span></span> <span data-ttu-id="200e7-161">Telepítés után ellenőrizheti, hogy az új erőforrás segítségével telepítve [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).</span><span class="sxs-lookup"><span data-stu-id="200e7-161">After install, you can verify that your new resource is installed using [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).</span></span>

```
PS> Get-DSCResource -Name TimeZone -Syntax

TimeZone [String] #ResourceName
{
    IsSingleInstance = [string]{ Yes }
    TimeZone = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

<span data-ttu-id="200e7-162">Megtekintheti továbbá más erőforrások az újonnan telepített modul megadásával a `-ModuleName` paraméter.</span><span class="sxs-lookup"><span data-stu-id="200e7-162">You can also view other resources in your newly installed module, by specifying the `-ModuleName` parameter.</span></span>

```
PS> Get-DSCResource -Module ComputerManagementDSC

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      Computer                  ComputerManagementDsc          6.0.0.0    {Name, Credential, DependsOn, ...
PowerShell      OfflineDomainJoin         ComputerManagementDsc          6.0.0.0    {IsSingleInstance, RequestFile...
PowerShell      PowerPlan                 ComputerManagementDsc          6.0.0.0    {IsSingleInstance, Name, Depen...
PowerShell      PowerShellExecutionPolicy ComputerManagementDsc          6.0.0.0    {ExecutionPolicy, ExecutionPol...
PowerShell      ScheduledTask             ComputerManagementDsc          6.0.0.0    {TaskName, ActionArguments, Ac...
PowerShell      TimeZone                  ComputerManagementDsc          6.0.0.0    {IsSingleInstance, TimeZone, D...
PowerShell      VirtualMemory             ComputerManagementDsc          6.0.0.0    {Drive, Type, DependsOn, Initi...
```

## <a name="see-also"></a><span data-ttu-id="200e7-163">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="200e7-163">See also</span></span>

- [<span data-ttu-id="200e7-164">Mik azok az erőforrások?</span><span class="sxs-lookup"><span data-stu-id="200e7-164">What are Resources?</span></span>](../resources/resources.md)
