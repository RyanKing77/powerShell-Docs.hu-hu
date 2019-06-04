---
ms.date: 12/14/2018
keywords: PowerShell, a parancsmag
title: Hordozható modulok írása
ms.openlocfilehash: 237f6aaea0ed019c54d04a8477d7a456edf00910
ms.sourcegitcommit: bc42c9166857147a1ecf9924b718d4a48eb901e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/03/2019
ms.locfileid: "66470978"
---
# <a name="portable-modules"></a>Hordozható modulok

Windows PowerShell íródott [.NET-keretrendszer][] Bár a PowerShell Core íródott [.NET Core][]. Hordozható modulok olyan modulok, amelyek a Windows PowerShell és a PowerShell Core. .NET-keretrendszer és a .NET Core erősen kompatibilis, amelyek nincsenek az elérhető API-kat a kettő közötti különbségeket. Emellett különbségek vannak az API-k a Windows PowerShell és a PowerShell Core. Mindkét környezetben használandó modulok kell figyelembe venni a különbségeket.

## <a name="porting-an-existing-module"></a>Egy meglévő modul portolása

### <a name="porting-a-pssnapin"></a>Egy PSSnapIn portolása

PowerShell [beépített modulok](/powershell/developer/cmdlet/modules-and-snap-ins) a PowerShell Core nem támogatottak. Azt azonban nagyon egyszerű, egy PowerShell-modul egy PSSnapIn átalakítása. A PSSnapIn regisztrációs kód általában egy fájlban egyetlen forrásai osztály származó [PSSnapIn][].
A forrásfájl eltávolítása a build; már nincs rá szükség.

Használat [New-ModuleManifest][] hozhat létre egy új moduljegyzék, amely a PSSnapIn regisztrációs kód nincs szükség. Egyes az értékek a **PSSnapIn** (például **leírás**) használható fel újra, a modul a jegyzékfájlban.

A **RootModule** a moduljegyzékben tulajdonság állítható a parancsmagok végrehajtása szerelvényfájlba (dll) nevére.

### <a name="the-net-portability-analyzer-aka-apiport"></a>A .NET-hordozhatóságot Analyzer (más néven APIPort)

Port modulokkal készült Windows PowerShell használata a PowerShell Core, kezdje a [.NET hordozhatóságot elemző][]. Futtassa ezt az eszközt annak meghatározásához, hogy a .NET API-k, a modul használt kompatibilisek-e a .NET-keretrendszer, a .NET Core és az egyéb .NET-modulok a lefordított szerelvényben. Az eszköz másik API-k javasol, ha vannak ilyenek. Ellenkező esetben előfordulhat, hogy hozzá kell [futásidejű ellenőrzés][] , és korlátozhatja a funkciókat adott modulok nem érhetők el.

## <a name="creating-a-new-module"></a>Új modul létrehozása

Új modul létrehozása, ha a javaslat használatára-e a [.NET CLI][].

### <a name="installing-the-powershell-standard-module-template"></a>A PowerShell szabványos modul sablon telepítése

A .NET parancssori felület telepítése után telepítse a könyvtár létrehozni egy egyszerű PowerShell-modul.
A modul Windows PowerShell, a PowerShell Core, Windows, Linux és macOS kompatibilis lesz.

Az alábbi példa bemutatja, hogyan telepítheti a sablont:

```powershell
dotnet new -i Microsoft.PowerShell.Standard.Module.Template
```

```output
  Restoring packages for C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\restore.csproj...
  Installing Microsoft.PowerShell.Standard.Module.Template 0.1.3.
  Generating MSBuild file C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\obj\restore.csproj.nuget.g.props.
  Generating MSBuild file C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\obj\restore.csproj.nuget.g.targets.
  Restore completed in 1.66 sec for C:\Users\Steve\.templateengine\dotnetcli\v2.1.302\scratch\restore.csproj.

Usage: new [options]

Options:
  -h, --help          Displays help for this command.
  -l, --list          Lists templates containing the specified name. If no name is specified, lists all templates.
  -n, --name          The name for the output being created. If no name is specified, the name of the current directory is used.
  -o, --output        Location to place the generated output.
  -i, --install       Installs a source or a template pack.
  -u, --uninstall     Uninstalls a source or a template pack.
  --nuget-source      Specifies a NuGet source to use during install.
  --type              Filters templates based on available types. Predefined values are "project", "item" or "other".
  --force             Forces content to be generated even if it would change existing files.
  -lang, --language   Filters templates based on language and specifies the language of the template to create.


Templates                                         Short Name         Language          Tags
----------------------------------------------------------------------------------------------------------------------------
Console Application                               console            [C#], F#, VB      Common/Console
Class library                                     classlib           [C#], F#, VB      Common/Library
PowerShell Standard Module                        psmodule           [C#]              Library/PowerShell/Module
...
```

### <a name="creating-a-new-module-project"></a>Új modul-projekt létrehozása

A sablon telepítése után létrehozhat egy új PowerShell modul projektet, hogy a sablon használatával. Ebben a példában a mintamodul nevezik "myModule".

```
PS> mkdir myModule

    Directory: C:\Users\Steve

Mode LastWriteTime Length Name
---- ------------- ------ ----
d----- 8/3/2018 2:41 PM myModule

PS> cd myModule
PS C:\Users\Steve\myModule> dotnet new psmodule

The template "PowerShell Standard Module" was created successfully.

Processing post-creation actions...
Running 'dotnet restore' on C:\Users\Steve\myModule\myModule.csproj...
  Restoring packages for C:\Users\Steve\myModule\myModule.csproj...
  Installing PowerShellStandard.Library 5.1.0.
  Generating MSBuild file C:\Users\Steve\myModule\obj\myModule.csproj.nuget.g.props.
  Generating MSBuild file C:\Users\Steve\myModule\obj\myModule.csproj.nuget.g.targets.
  Restore completed in 1.76 sec for C:\Users\Steve\myModule\myModule.csproj.

Restore succeeded.
```

### <a name="building-the-module"></a>A modul

Standard szintű .NET CLI-parancsok használatával állítsa össze a projektet.

```powershell
dotnet build
```

```output
PS C:\Users\Steve\myModule> dotnet build
Microsoft (R) Build Engine version 15.7.179.6572 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 76.85 ms for C:\Users\Steve\myModule\myModule.csproj.
  myModule -> C:\Users\Steve\myModule\bin\Debug\netstandard2.0\myModule.dll

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:05.40
```

### <a name="testing-the-module"></a>A modul tesztelése

Ha a modul, importálás, és hajtsa végre a minta parancsmagot.

```powershell
ipmo .\bin\Debug\netstandard2.0\myModule.dll
Test-SampleCmdlet -?
Test-SampleCmdlet -FavoriteNumber 7 -FavoritePet Cat
```

```output
PS C:\Users\Steve\myModule> ipmo .\bin\Debug\netstandard2.0\myModule.dll
PS C:\Users\Steve\myModule> Test-SampleCmdlet -?

NAME
    Test-SampleCmdlet

SYNTAX
    Test-SampleCmdlet [-FavoriteNumber] <int> [[-FavoritePet] {Cat | Dog | Horse}] [<CommonParameters>]


ALIASES
    None


REMARKS
    None


PS C:\Users\Steve\myModule> Test-SampleCmdlet -FavoriteNumber 7 -FavoritePet Cat

FavoriteNumber FavoritePet
-------------- -----------
             7 Cat
```

A következő szakaszok ismertetik részletesebben néhány, az a sablon által használt technológiák.

## <a name="net-standard-library"></a>.NET standard kódtár

[.NET standard][] .NET API-k minden .NET-implementációkban elérhető formális meghatározását. A felügyelt kód a .NET-keretrendszer és a .NET Core verziók, amelyek kompatibilisek a .NET Standard verzió a .NET Standard együttműködik.

> [!NOTE]
> Bár az API-k .NET standardban is létezik, a .NET Core API-implementáció generálhat egy `PlatformNotSupportedException` futásidőben, így a Windows PowerShell és a PowerShell Core, a kompatibilitás ellenőrzéséhez az ajánlott eljárás, hogy a modul mindkét környezetekben tesztek futtatása.
> Is futtathatja tesztek Linux és MacOS rendszereken, ha a modul az célja, hogy a platformok közötti lehet.

.NET Standard célcsoportkezelés segítségével győződjön meg arról, hogy alakul ki a modult, mert inkompatibilis API-k nem véletlenül ismerje meg a modulba. Kompatibilitási problémák észlelésekor a fordítás során futásidejű helyett.

Azonban nem szükséges a .NET Standard-modul a Windows PowerShell és a PowerShell Core, mind a cél kompatibilis API-kkal is. A köztes nyelv (Illinois), a két modulok között kompatibilis. Célba .NET-keretrendszer 4.6.1-es verziója, amely nagy .NET Standard 2.0-val kompatibilis. Ha nem használja a .NET Standard 2.0 kívül API-k, majd a modul együttműködik PowerShell Core 6-os jelölője nélkül.

## <a name="powershell-standard-library"></a>PowerShell Standard kódtár

A [PowerShell Standard][] könyvtár a PowerShell API-k elérhető az összes PowerShell nagyobb vagy egyenlő a verzióra, a standard verzióban formális meghatározását.

Ha például [PowerShell szabványos 5.1][] kompatibilis a Windows PowerShell 5.1-es és a PowerShell Core 6.0 vagy újabb.

Azt javasoljuk, hogy a modul PowerShell Standard kódtár használatával összeállíthatja. A kódtár biztosítja, hogy az API-k rendelkezésre álló és a Windows PowerShell és a PowerShell Core 6-os megvalósított.
Mindig legyen továbbítást-kompatibilis PowerShell szabványos célja. A modul PowerShell szabványos könyvtár 5.1 használatával létrehozott mindig lesz kompatibilis PowerShell jövőbeli verzióiban.

## <a name="module-manifest"></a>Moduljegyzék

### <a name="indicating-compatibility-with-windows-powershell-and-powershell-core"></a>A Windows PowerShell és a PowerShell Core kompatibilitásukat

Miután ellenőrizte, hogy a modul Windows PowerShell és a PowerShell Core is működik, a moduljegyzékben explicit módon jelzi, hogy kompatibilitási használatával a [CompatiblePSEditions][] tulajdonság. Érték `Desktop` azt jelenti, hogy a modul kompatibilis a Windows PowerShell-lel, miközben érték `Core` azt jelenti, hogy a modul a PowerShell Core kompatibilis. Mind `Desktop` és `Core` azt jelenti, hogy a modul Windows PowerShell és a PowerShell Core kompatibilis.

> [!NOTE]
> `Core` nem automatikusan jelenti, hogy a modul Windows, Linux és macOS kompatibilis.
> A **CompatiblePSEditions** tulajdonság a PowerShell 5-ös verziójának jelent meg. Modul jegyzékfájlok használó a **CompatiblePSEditions** tulajdonság nem sikerült betölteni a PowerShell 5-ös verziójának korábbi verziók.

### <a name="indicating-os-compatibility"></a>Operációsrendszer-kompatibilitás jelző

Először ellenőrizze, hogy a modul a Linux és MacOS rendszeren működik. Ezután adja meg az operációs rendszereket a moduljegyzékben való kompatibilitás érdekében. Ez megkönnyíti a felhasználók számára való a modul az operációs rendszer, ha közzé a [PowerShell-galéria][].

A modul a jegyzékfájlban a `PrivateData` tulajdonság egy `PSData` alárendelt tulajdonság. A választható `Tags` tulajdonsága `PSData` egy diagnosztikakonfigurációs tömböt foglal értékek láthatók a PowerShell-galériában. A PowerShell-galériából a következő kompatibilitási értékeket támogatja:

| Címke               | Leírás                                |
|-------------------|--------------------------------------------|
| PSEdition_Core    | A PowerShell Core 6-kompatibilis          |
| PSEdition_Desktop | Kompatibilis a Windows PowerShell-lel         |
| Windows           | Windows-kompatibilis                    |
| Linux             | Linux (nincs megadott disztribúció) kompatibilis |
| macOS             | MacOS-kompatibilis                      |

Példa:

```powershell
@{
    GUID = "4ae9fd46-338a-459c-8186-07f910774cb8"
    Author = "Microsoft Corporation"
    CompanyName = "Microsoft Corporation"
    Copyright = "(C) Microsoft Corporation. All rights reserved."
    HelpInfoUri = "https://go.microsoft.com/fwlink/?linkid=855962"
    ModuleVersion = "1.2.4"
    PowerShellVersion = "3.0"
    ClrVersion = "4.0"
    RootModule = "PackageManagement.psm1"
    Description = 'PackageManagement (a.k.a. OneGet) is a new way to discover and install software packages from around the web.
 It is a manager or multiplexer of existing package managers (also called package providers) that unifies Windows package management with a single Windows PowerShell interface. With PackageManagement, you can do the following.
  - Manage a list of software repositories in which packages can be searched, acquired and installed
  - Discover software packages
  - Seamlessly install, uninstall, and inventory packages from one or more software repositories'

    CmdletsToExport = @(
        'Find-Package',
        'Get-Package',
        'Get-PackageProvider',
        'Get-PackageSource',
        'Install-Package',
        'Import-PackageProvider'
        'Find-PackageProvider'
        'Install-PackageProvider'
        'Register-PackageSource',
        'Set-PackageSource',
        'Unregister-PackageSource',
        'Uninstall-Package'
        'Save-Package'
    )

    FormatsToProcess  = @('PackageManagement.format.ps1xml')

    PrivateData = @{
        PSData = @{
            Tags = @('PackageManagement', 'PSEdition_Core', 'PSEdition_Desktop', 'Windows', 'Linux', 'macOS')
            ProjectUri = 'https://oneget.org'
        }
    }
}
```

<!-- reference links -->
[.NET-keretrendszer]: /dotnet/framework/
[.NET Core]: /dotnet/core/
[PSSnapIn]: /dotnet/api/system.management.automation.pssnapin
[New-ModuleManifest]: /powershell/module/microsoft.powershell.core/new-modulemanifest
[futásidejű ellenőrzés]: /dotnet/api/system.runtime.interopservices.runtimeinformation.frameworkdescription#System_Runtime_InteropServices_RuntimeInformation_FrameworkDescription
[.NET CLI]: /dotnet/core/tools/?tabs=netcore2x
[.NET Standard]: /dotnet/standard/net-standard
[PowerShell Standard]: https://github.com/PowerShell/PowerShellStandard
[PowerShell szabványos 5.1]: https://www.nuget.org/packages/PowerShellStandard.Library/5.1.0
[PowerShell-galéria]: https://www.powershellgallery.com
[.NET hordozhatóságot elemző]: https://github.com/Microsoft/dotnet-apiport
[CompatiblePSEditions]: /powershell/gallery/concepts/module-psedition-support
