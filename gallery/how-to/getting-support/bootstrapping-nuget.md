---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: NuGet rendszerindítása
ms.openlocfilehash: 6d8f106bc3b8741203e87e4c097948a843f06d6e
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002138"
---
# <a name="bootstrap-the-nuget-provider-and-nugetexe"></a><span data-ttu-id="07114-103">A NuGet-szolgáltató és a NuGet.exe bootstrap</span><span class="sxs-lookup"><span data-stu-id="07114-103">Bootstrap the NuGet provider and NuGet.exe</span></span>

<span data-ttu-id="07114-104">A legújabb NuGet-szolgáltató nem szerepel a NuGet.exe.</span><span class="sxs-lookup"><span data-stu-id="07114-104">NuGet.exe is not included in the latest NuGet provider.</span></span> <span data-ttu-id="07114-105">Közzé egy modul vagy a parancsfájl működésére, a PowerShellGet a bináris végrehajtható NuGet.exe igényel.</span><span class="sxs-lookup"><span data-stu-id="07114-105">For publish operations of either a module or script, PowerShellGet requires the binary executable NuGet.exe.</span></span> <span data-ttu-id="07114-106">Csak a NuGet-szolgáltató szükség minden egyéb művelet, beleértve a *található*, *telepítése*, *mentése*, és *eltávolítása*.</span><span class="sxs-lookup"><span data-stu-id="07114-106">Only the NuGet provider is required for all other operations, including *find*, *install*, *save*, and *uninstall*.</span></span>
<span data-ttu-id="07114-107">A PowerShellGet kezeléséhez vagy logikát tartalmaz, egy kombinált rendszerindítási a NuGet-szolgáltató és a NuGet.exe vagy rendszerindítási a NuGet-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="07114-107">PowerShellGet includes logic to handle either a combined bootstrap of the NuGet provider and NuGet.exe, or bootstrap of only the NuGet provider.</span></span> <span data-ttu-id="07114-108">Mindkét esetben csak egy egyetlen azonnali üzenet jelenhet meg.</span><span class="sxs-lookup"><span data-stu-id="07114-108">In either case, only a single prompt message should occur.</span></span> <span data-ttu-id="07114-109">Ha a gép nem csatlakozik az internethez, a felhasználó vagy rendszergazda kell másolnia a NuGet-szolgáltató és/vagy a NuGet.exe fájl egy megbízható példányát a leválasztott gép.</span><span class="sxs-lookup"><span data-stu-id="07114-109">If the machine is not connected to the Internet, the user or an administrator must copy a trusted instance of the NuGet provider and/or the NuGet.exe file to the disconnected machine.</span></span>

> [!NOTE]
> <span data-ttu-id="07114-110">A NuGet-szolgáltató része 6-os verziótól kezdődően a PowerShell telepítése.</span><span class="sxs-lookup"><span data-stu-id="07114-110">Starting with version 6, the NuGet provider is included in the installation of PowerShell.</span></span>

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="07114-111">Kapcsolódó hiba feloldása, ha a NuGet-szolgáltató nincs telepítve olyan számítógépen, amelyen Internet</span><span class="sxs-lookup"><span data-stu-id="07114-111">Resolving error when the NuGet provider has not been installed on a machine that is Internet connected</span></span>

```powershell
Find-Module -Repository PSGallery -Verbose -Name Contoso
```

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): n
Find-Module : NuGet provider is required to interact with NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed.
At line:1 char:1
+ Find-Module -Repository PSGallery -Verbose -Name Contoso
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Find-Module], InvalidOperationException
   + FullyQualifiedErrorId : CouldNotInstallNuGetProvider,Find-Module
```

```powershell
Find-Module -Repository PSGallery -Verbose -Name Contoso
```

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\manikb\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import the NuGet provider
now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.

Version    Name                                Type       Repository           Description
-------    ----                                ----       ----------           -----------
2.5        Contoso                             Module     PSGallery        Contoso module
```

## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="07114-112">Kapcsolódó hiba feloldása, amikor érhető el a NuGet-szolgáltató és a NuGet.exe nem áll rendelkezésre olyan számítógépen, amelyen Internet a közzétételi művelet során</span><span class="sxs-lookup"><span data-stu-id="07114-112">Resolving error when the NuGet provider is available and NuGet.exe is not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module
```

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a><span data-ttu-id="07114-113">Kapcsolódó hiba feloldása, ha a NuGet-szolgáltató és a NuGet.exe nem érhetők el olyan számítógépen, amelyen Internet a közzétételi művelet során</span><span class="sxs-lookup"><span data-stu-id="07114-113">Resolving error when both NuGet provider and NuGet.exe are not available during the publish operation on a machine that is Internet connected</span></span>

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Please ensure that '2.8.5.201' or newer version of NuGet provider is installed and NuGet.exe is available under
one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetBinaries,Publish-Module
```

```powershell
Publish-Module -Name Contoso -Repository PSGallery -Verbose
```

```output
NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="07114-114">Manuálisan rendszerindítása a NuGet-szolgáltató olyan gépen, amely nem csatlakozik az internethez</span><span class="sxs-lookup"><span data-stu-id="07114-114">Manually bootstrapping the NuGet provider on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="07114-115">A fent bemutatott eljárások azt feltételezik, a gép csatlakozik az internethez, és fájlokat tölthet le egy nyilvános helye.</span><span class="sxs-lookup"><span data-stu-id="07114-115">The processes demonstrated above assume the machine is connected to the Internet and can download files from a public location.</span></span> <span data-ttu-id="07114-116">Ha ez nem lehetséges, az egyetlen lehetősége egy gépen a fenti eljárások használatával elindíthat és manuális másolása a szolgáltató az elkülönített csomópont offline megbízható folyamatát.</span><span class="sxs-lookup"><span data-stu-id="07114-116">If that is not possible, the only option is to bootstrap a machine using the processes given above, and manually copy the provider to the isolated node through an offline trusted process.</span></span> <span data-ttu-id="07114-117">Ebben a forgatókönyvben a leggyakoribb használati eset akkor, ha a egy privát katalógust érhető el az elkülönített környezet támogatásához.</span><span class="sxs-lookup"><span data-stu-id="07114-117">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span>

<span data-ttu-id="07114-118">A fenti elindíthat egy internetkapcsolattal rendelkező gépen folyamat lépéseinek, található szolgáltató fájlok helyét:</span><span class="sxs-lookup"><span data-stu-id="07114-118">After following the process above to bootstrap an Internet connected machine, you will find provider files in the location:</span></span>

`C:\Program Files\PackageManagement\ProviderAssemblies\`

<span data-ttu-id="07114-119">A NuGet-szolgáltató fájl/mappa szerkezete lesz (valószínűleg egy eltérő verziószámot):</span><span class="sxs-lookup"><span data-stu-id="07114-119">The folder/file structure of the NuGet provider will be (possibly with a different version number):</span></span>

```
NuGet
--2.8.5.208
----Microsoft.PackageManagement.NuGetProvider.dll
```

<span data-ttu-id="07114-120">Másolja ki ezeket a mappákat és -fájlt egy megbízható folyamatot, hogy a kapcsolat nélküli gépek.</span><span class="sxs-lookup"><span data-stu-id="07114-120">Copy these folders and file using a trusted process to the offline machines.</span></span>

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a><span data-ttu-id="07114-121">Manuálisan a támogatásához a NuGet.exe rendszerindítása közzététele a műveletek olyan gépen, amely nem csatlakozik az internethez</span><span class="sxs-lookup"><span data-stu-id="07114-121">Manually bootstrapping NuGet.exe to support publish operations on a machine that is not connected to the Internet</span></span>

<span data-ttu-id="07114-122">A folyamat manuális elindíthat a NuGet-szolgáltató, ha a gép használandó modulok vagy parancsfájlok közzététele egy privát katalógust az mellett a `Publish-Module` vagy `Publish-Script` parancsmagok, a NuGet.exe bináris végrehajtható fájl lesz szükség.</span><span class="sxs-lookup"><span data-stu-id="07114-122">In addition to the process to manually bootstrap the NuGet provider, if the machine will be used to publish modules or scripts to a private gallery using the `Publish-Module` or `Publish-Script` cmdlets, the NuGet.exe binary executable file will be required.</span></span>

<span data-ttu-id="07114-123">Ebben a forgatókönyvben a leggyakoribb használati eset akkor, ha a egy privát katalógust érhető el az elkülönített környezet támogatásához.</span><span class="sxs-lookup"><span data-stu-id="07114-123">The most common use case for this scenario is when a private gallery is available to support an isolated environment.</span></span> <span data-ttu-id="07114-124">Szerezze be a NuGet.exe fájlt a két lehetőség van.</span><span class="sxs-lookup"><span data-stu-id="07114-124">There are two options to obtain the NuGet.exe file.</span></span>

<span data-ttu-id="07114-125">Az egyik lehetőség, hogy egy internetkapcsolattal rendelkező gépek elindíthat, és másolja a fájlokat a kapcsolat nélküli gépek, egy megbízható folyamattal.</span><span class="sxs-lookup"><span data-stu-id="07114-125">One option is to bootstrap a machine that is Internet connected and copy the files to the offline machines using a trusted process.</span></span> <span data-ttu-id="07114-126">Az internetkapcsolattal rendelkező gépen rendszerindítása, miután a NuGet.exe bináris két mappák egyikében található:</span><span class="sxs-lookup"><span data-stu-id="07114-126">After bootstrapping the Internet connected machine, the NuGet.exe binary will be located in one of two folders:</span></span>

<span data-ttu-id="07114-127">Ha a `Publish-Module` vagy `Publish-Script` parancsmagok végrehajtódtak emelt jogosultsági szintű (adminisztrátori):</span><span class="sxs-lookup"><span data-stu-id="07114-127">If the `Publish-Module` or `Publish-Script` cmdlets were executed with elevated permissions (As an Administrator):</span></span>

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="07114-128">Ha a parancsmagokat végrehajtódtak nem emelt szintű engedélyekkel rendelkező felhasználóként:</span><span class="sxs-lookup"><span data-stu-id="07114-128">If the cmdlets were executed as a user without elevated permissions:</span></span>

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

<span data-ttu-id="07114-129">A második lehetőség a NuGet.Org webhelyen NuGet.exe töltheti le: [ https://dist.nuget.org/index.html ](https://www.nuget.org/downloads) egy éles gépek Nuget verziót kiválasztásakor róla, hogy újabb, mint a 2.8.5.208, és azonosítja a verzióját, amely rendelkezik címkével lett " ajánlott".</span><span class="sxs-lookup"><span data-stu-id="07114-129">A second option is to download NuGet.exe from the NuGet.Org website: [https://dist.nuget.org/index.html](https://www.nuget.org/downloads) When selecting a NugGet version for production machines, make sure it is later than 2.8.5.208, and identify the version that has been labeled "recommended".</span></span> <span data-ttu-id="07114-130">Fontos, hogy a fájl feloldása, ha a böngésző segítségével lett letöltve.</span><span class="sxs-lookup"><span data-stu-id="07114-130">Remember to unblock the file if it was downloaded using a browser.</span></span> <span data-ttu-id="07114-131">Ennek segítségével hajtható végre a `Unblock-File` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="07114-131">This can be performed by using the `Unblock-File` cmdlet.</span></span>

<span data-ttu-id="07114-132">Mindkét esetben a NuGet.exe fájl átmásolható tetszőleges helyére `$env:path`, de a szabványos helyek:</span><span class="sxs-lookup"><span data-stu-id="07114-132">In either case, the NuGet.exe file can be copied to any location in `$env:path`, but the standard locations are:</span></span>

<span data-ttu-id="07114-133">A végrehajtható fájl elérhetővé tétele, hogy minden felhasználó használhatja `Publish-Module` és `Publish-Script` parancsmagok:</span><span class="sxs-lookup"><span data-stu-id="07114-133">To make the executable available so that all users can use `Publish-Module` and `Publish-Script` cmdlets:</span></span>

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

<span data-ttu-id="07114-134">Elérhetővé a végrehajtható fájl számára egy adott felhasználó, csak annak a felhasználónak a profilon belül a helyre másolja:</span><span class="sxs-lookup"><span data-stu-id="07114-134">To make the executable available to only a specific user, copy to the location within only that user's profile:</span></span>

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```
