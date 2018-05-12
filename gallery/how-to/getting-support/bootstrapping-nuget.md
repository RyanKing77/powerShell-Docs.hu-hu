
---
MS.Date: 06/12/2017 közreműködői: manikb ms.topic: kulcsszavak hivatkozni: gyűjtemény, a powershell, a parancsmag, a psget cím: NuGet rendszerindítása
---
# <a name="bootstrap-the-nuget-provider-and-nugetexe"></a>A NuGet-szolgáltató és NuGet.exe bootstrap

NuGet.exe nem szerepel a legújabb NuGet-szolgáltató.
A modul vagy a parancsfájl működésére közzétételéhez PowerShellGet a bináris végrehajtható NuGet.exe van szükség.
Csak a NuGet-szolgáltató szükség, minden más műveletek, beleértve a *található*, *telepítése*, *mentése*, és *eltávolítása*.
PowerShellGet kezeléséhez vagy logikát tartalmaz, a kombinált rendszerindítási a NuGet-szolgáltató és NuGet.exe vagy rendszerindítási csak a NuGet-szolgáltató.
Mindkét esetben csak egyetlen azonnali üzenetben jöjjön létre.
Ha a számítógép nem csatlakozik az internethez, a felhasználónak vagy rendszergazdának át kell másolnia a NuGet-szolgáltató és/vagy a NuGet.exe fájl megbízható példánya a leválasztott gép.

>**Megjegyzés:**: 6-os verziótól kezdődően a NuGet-szolgáltató része a PowerShell telepítése. [http://github.com/powershell/powershell](http://github.com/powershell/powershell)

## <a name="resolving-error-when-the-nuget-provider-has-not-been-installed-on-a-machine-that-is-internet-connected"></a>Kapcsolódó hiba elhárításához, amikor a NuGet-szolgáltató nem telepíthető olyan számítógépen, amelyen Internet

```powershell
PS> Find-Module -Repository PSGallery -Verbose -Name Contoso

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

PS> Find-Module -Repository PSGallery -Verbose -Name Contoso

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

## <a name="resolving-error-when-the-nuget-provider-is-available-and-nugetexe-is-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Kapcsolódó hiba elhárításához, amikor a NuGet-szolgáltató nem érhető el, és NuGet.exe nem érhető el az olyan gépen, amely internetes közzététel művelet során

```powershell
PS> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): N
Publish-Module : NuGet.exe is required to interact with NuGet-based repositories. Please ensure that NuGet.exe is available under one of the paths specified in PATH environment variable value.
At line:1 char:1
+ Publish-Module -Name Contoso -Repository PSGallery -Verbose
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Publish-Module], InvalidOperationException
    + FullyQualifiedErrorId : CouldNotInstallNuGetExe,Publish-Module

PS> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe is required to continue
PowerShellGet requires NuGet.exe to publish an item to the NuGet-based repositories. NuGet.exe must be available under one of the paths specified in PATH environment variable value. Do you want PowerShellGet to install NuGet.exe now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="resolving-error-when-both-nuget-provider-and-nugetexe-are-not-available-during-the-publish-operation-on-a-machine-that-is-internet-connected"></a>Kapcsolódó hiba elhárításához, amikor NuGet-szolgáltató és NuGet.exe is nem érhető el az olyan gépen, amely internetes közzététel művelet során

```powershell
PS> Publish-Module -Name Contoso -Repository PSGallery -Verbose

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

PS> Publish-Module -Name Contoso -Repository PSGallery -Verbose

NuGet.exe and NuGet provider are required to continue
PowerShellGet requires NuGet.exe and NuGet provider version '2.8.5.201' or newer to interact with the NuGet-based repositories. Do you want PowerShellGet to install both NuGet.exe and NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
VERBOSE: Installing NuGet provider.
VERBOSE: Installing NuGet.exe.
VERBOSE: Successfully published module 'Contoso' to the module publish location 'https://www.powershellgallery.com/api/v2/'. Please allow few minutes for 'Contoso' to show up in the search results.
```

## <a name="manually-bootstrapping-the-nuget-provider-on-a-machine-that-is-not-connected-to-the-internet"></a>A NuGet-szolgáltató olyan gépen, amely nem kapcsolódik az internethez manuálisan rendszerindítása

A fenti bemutatott folyamatok tegyük fel, a számítógép csatlakozik az internethez, és letöltheti a fájlokat egy nyilvános helyről.
Ha ez nem lehetséges, az egyetlen lehetősége a gépek a fenti eljárások bootstrap, és manuálisan másolja a szolgáltató a folyamatot, az offline megbízható elkülönített csomópont.
Ebben a forgatókönyvben a leggyakrabban használt használati eset akkor, ha egy titkos gyűjtemény érhető el egy elkülönített környezet támogatásához.

Egy internethez csatlakoztatott számítógép rendszerindításának a fenti folyamatot követve, miután található szolgáltató fájlok helyét:

```
C:\Program Files\PackageManagement\ProviderAssemblies\
```

A fájl/mappa szerkezete a NuGet-szolgáltató (és valószínűleg különböző verziószámú) lesz:

NuGet<br>
--2.8.5.208<br>
---Microsoft.PackageManagement.NuGetProvider.dll

Ezeket a mappákat és a kapcsolat nélküli gépekre megbízható eljárással fájl másolása.

## <a name="manually-bootstrapping-nugetexe-to-support-publish-operations-on-a-machine-that-is-not-connected-to-the-internet"></a>Olyan gépen, amely nem kapcsolódik az internethez műveletek manuálisan rendszerindítása támogatásához NuGet.exe közzététele

A folyamat a NuGet-szolgáltatót, manuálisan bootstrap, ha a gép használandó modulok vagy parancsfájlok közzététele egy titkos gyűjtemény használata mellett a *Publish-modul* vagy *Publish-parancsfájl* parancsmagok a NuGet.exe bináris végrehajtható fájl lesz szükség.
Ebben a forgatókönyvben a leggyakrabban használt használati eset akkor, ha egy titkos gyűjtemény érhető el egy elkülönített környezet támogatásához.
A NuGet.exe fájl két lehetőség áll rendelkezésre.

Egy lehetőség egy olyan számítógépen, amelyen az internethez csatlakoztatott bootstrap, és másolja a fájlokat megbízható folyamatok használata a kapcsolat nélküli gépek.
Az Internet csatlakoztatott számítógép rendszerindítása, miután a NuGet.exe bináris két mappák egyikében található:

Ha a *Publish-modul* vagy *Publish-parancsfájl* parancsmagok végrehajtódtak emelt szintű engedélyekkel (egy rendszergazdaként):

```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

Ha a parancsmagok végrehajtása nem emelt szintű engedélyekkel rendelkező felhasználóként történt:

```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```

Egy második lehetőség a NuGet.Org webhely NuGet.exe töltheti le: [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)<br>
Ha egy éles gépek Nuget verziót választja, ellenőrizze, hogy az újabb, mint 2.8.5.208, és azonosítja a verzióját, amely "ajánlott" lett címkézve.
Fontos, hogy a fájl feloldása, ha a böngésző használatával lett letöltve.
Ennek segítségével hajtható végre a *Unblock-fájl* parancsmag.

Mindkét esetben a NuGet.exe fájl másolhat tetszőleges helyére *$env: elérési*, azonban a szabványos helyekre:

A végrehajtható fájl elérhetővé tétele, hogy minden felhasználó használhatja *Publish-modul* és *Publish-parancsfájl* parancsmagokat:

```
$env:ProgramData\Microsoft\Windows\PowerShell\PowerShellGet
```

A végrehajtható fájl csak egy adott felhasználó rendelkezésre állásúvá tételéhez másolja a hely csak a felhasználó profiljában:

```
$env:userprofile\AppData\Local\Microsoft\Windows\PowerShell\PowerShellGet\
```