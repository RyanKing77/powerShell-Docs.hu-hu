---
ms.date: 06/12/2017
contributor: manikb
keywords: katalógus, powershell, a parancsmag, psget
title: NuGet rendszerindítása
ms.openlocfilehash: e82fe7bec2e6b7a321fb173cdf9a54c5a97d5f18
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267847"
---
# <a name="bootstrap-the-nuget-provider-and-nugetexe"></a>A NuGet-szolgáltató és a NuGet.exe bootstrap

A legújabb NuGet-szolgáltató nem szerepel a NuGet.exe. Közzé egy modul vagy a parancsfájl működésére, a PowerShellGet a bináris végrehajtható NuGet.exe igényel. Csak a NuGet-szolgáltató szükség minden egyéb művelet, beleértve a *található*, *telepítése*, *mentése*, és *eltávolítása*.
A PowerShellGet kezeléséhez vagy logikát tartalmaz, egy kombinált rendszerindítási a NuGet-szolgáltató és a NuGet.exe vagy rendszerindítási a NuGet-szolgáltató. Mindkét esetben csak egy egyetlen azonnali üzenet jelenhet meg. Ha a gép nem csatlakozik az internethez, a felhasználó vagy rendszergazda kell másolnia a NuGet-szolgáltató és/vagy a NuGet.exe fájl egy megbízható példányát a leválasztott gép.

> [!NOTE]
> A NuGet-szolgáltató része 6-os verziótól kezdődően a PowerShell telepítése.

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a>Kapcsolódó hiba feloldása, ha a NuGet-szolgáltató nincs telepítve olyan számítógépen, amelyen Internet

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

## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Kapcsolódó hiba feloldása, amikor érhető el a NuGet-szolgáltató és a NuGet.exe nem áll rendelkezésre olyan számítógépen, amelyen Internet a közzétételi művelet során

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

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Kapcsolódó hiba feloldása, ha a NuGet-szolgáltató és a NuGet.exe nem érhetők el olyan számítógépen, amelyen Internet a közzétételi művelet során

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

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a>Manuálisan rendszerindítása a NuGet-szolgáltató olyan gépen, amely nem csatlakozik az internethez

A fent bemutatott eljárások azt feltételezik, a gép csatlakozik az internethez, és fájlokat tölthet le egy nyilvános helye. Ha ez nem lehetséges, az egyetlen lehetősége egy gépen a fenti eljárások használatával elindíthat és manuális másolása a szolgáltató az elkülönített csomópont offline megbízható folyamatát. Ebben a forgatókönyvben a leggyakoribb használati eset akkor, ha a egy privát katalógust érhető el az elkülönített környezet támogatásához.

A fenti elindíthat egy internetkapcsolattal rendelkező gépen folyamat lépéseinek, található szolgáltató fájlok helyét:

`C:\Program Files\PackageManagement\ProviderAssemblies\`

A NuGet-szolgáltató fájl/mappa szerkezete lesz (valószínűleg egy eltérő verziószámot):

```
NuGet
--2.8.5.208
----Microsoft.PackageManagement.NuGetProvider.dll
```

Másolja ki ezeket a mappákat és -fájlt egy megbízható folyamatot, hogy a kapcsolat nélküli gépek.

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a>Manuálisan a támogatásához a NuGet.exe rendszerindítása közzététele a műveletek olyan gépen, amely nem csatlakozik az internethez

A folyamat manuális elindíthat a NuGet-szolgáltató, ha a gép használandó modulok vagy parancsfájlok közzététele egy privát katalógust az mellett a `Publish-Module` vagy `Publish-Script` parancsmagok, a NuGet.exe bináris végrehajtható fájl lesz szükség.

Ebben a forgatókönyvben a leggyakoribb használati eset akkor, ha a egy privát katalógust érhető el az elkülönített környezet támogatásához. Szerezze be a NuGet.exe fájlt a két lehetőség van.

Az egyik lehetőség, hogy egy internetkapcsolattal rendelkező gépek elindíthat, és másolja a fájlokat a kapcsolat nélküli gépek, egy megbízható folyamattal. Az internetkapcsolattal rendelkező gépen rendszerindítása, miután a NuGet.exe bináris két mappák egyikében található:

Ha a `Publish-Module` vagy `Publish-Script` parancsmagok végrehajtódtak emelt jogosultsági szintű (adminisztrátori):

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Ha a parancsmagokat végrehajtódtak nem emelt szintű engedélyekkel rendelkező felhasználóként:

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

A második lehetőség a NuGet.Org webhelyen NuGet.exe töltheti le: [ https://dist.nuget.org/index.html ](https://www.nuget.org/downloads) egy éles gépek Nuget verziót kiválasztásakor róla, hogy újabb, mint a 2.8.5.208, és azonosítja a verzióját, amely rendelkezik címkével lett " ajánlott". Fontos, hogy a fájl feloldása, ha a böngésző segítségével lett letöltve. Ennek segítségével hajtható végre a `Unblock-File` parancsmagot.

Mindkét esetben a NuGet.exe fájl átmásolható tetszőleges helyére `$env:path`, de a szabványos helyek:

A végrehajtható fájl elérhetővé tétele, hogy minden felhasználó használhatja `Publish-Module` és `Publish-Script` parancsmagok:

```powershell
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Elérhetővé a végrehajtható fájl számára egy adott felhasználó, csak annak a felhasználónak a profilon belül a helyre másolja:

```powershell
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```