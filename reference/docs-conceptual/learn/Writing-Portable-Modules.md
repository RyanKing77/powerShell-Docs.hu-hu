---
ms.date: 12/14/2018
keywords: PowerShell, a parancsmag
title: Hordozható modulok írása
ms.openlocfilehash: 38a93b5b030d58784b91292e2cd060b3a2c19a00
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086408"
---
# <a name="portable-modules"></a><span data-ttu-id="9ba85-103">Hordozható modulok</span><span class="sxs-lookup"><span data-stu-id="9ba85-103">Portable Modules</span></span>

<span data-ttu-id="9ba85-104">Windows PowerShell íródott [.NET-keretrendszer][] Bár a PowerShell Core íródott [.NET Core][].</span><span class="sxs-lookup"><span data-stu-id="9ba85-104">Windows PowerShell is written for [.NET Framework][] while PowerShell Core is written for [.NET Core][].</span></span> <span data-ttu-id="9ba85-105">Hordozható modulok olyan modulok, amelyek a Windows PowerShell és a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="9ba85-105">Portable modules are modules that work in both Windows PowerShell and PowerShell Core.</span></span> <span data-ttu-id="9ba85-106">.NET-keretrendszer és a .NET Core erősen kompatibilis, amelyek nincsenek az elérhető API-kat a kettő közötti különbségeket.</span><span class="sxs-lookup"><span data-stu-id="9ba85-106">While .NET Framework and .NET Core are highly compatible, there are differences in the available APIs between the two.</span></span> <span data-ttu-id="9ba85-107">Emellett különbségek vannak az API-k a Windows PowerShell és a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="9ba85-107">There are also differences in the APIs available in Windows PowerShell and PowerShell Core.</span></span> <span data-ttu-id="9ba85-108">Mindkét környezetben használandó modulok kell figyelembe venni a különbségeket.</span><span class="sxs-lookup"><span data-stu-id="9ba85-108">Modules intended to be used in both environments need to be aware of these differences.</span></span>

## <a name="porting-an-existing-module"></a><span data-ttu-id="9ba85-109">Egy meglévő modul portolása</span><span class="sxs-lookup"><span data-stu-id="9ba85-109">Porting an Existing Module</span></span>

### <a name="porting-a-pssnapin"></a><span data-ttu-id="9ba85-110">Egy PSSnapIn portolása</span><span class="sxs-lookup"><span data-stu-id="9ba85-110">Porting a PSSnapIn</span></span>

<span data-ttu-id="9ba85-111">A PowerShell Core (PSSnapIn) beépített PowerShell-modulok nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="9ba85-111">PowerShell SnapIns (PSSnapIn) aren't supported in PowerShell Core.</span></span> <span data-ttu-id="9ba85-112">Azt azonban nagyon egyszerű, egy PowerShell-modul egy PSSnapIn átalakítása.</span><span class="sxs-lookup"><span data-stu-id="9ba85-112">However, it's trivial to convert a PSSnapIn to a PowerShell module.</span></span> <span data-ttu-id="9ba85-113">A PSSnapIn regisztrációs kód általában egy fájlban egyetlen forrásai osztály származó [PSSnapIn][].</span><span class="sxs-lookup"><span data-stu-id="9ba85-113">Typically, the PSSnapIn registration code is in a single source file of a class that derives from [PSSnapIn][].</span></span> <span data-ttu-id="9ba85-114">A forrásfájl eltávolítása a build; már nincs rá szükség.</span><span class="sxs-lookup"><span data-stu-id="9ba85-114">Remove this source file from the build; it's no longer needed.</span></span>

<span data-ttu-id="9ba85-115">Használat [New-ModuleManifest][] hozhat létre egy új moduljegyzék, amely a PSSnapIn regisztrációs kód nincs szükség.</span><span class="sxs-lookup"><span data-stu-id="9ba85-115">Use [New-ModuleManifest][] to create a new module manifest that replaces the need for the PSSnapIn registration code.</span></span> <span data-ttu-id="9ba85-116">Egyes értékek (például leírás) az PSSnapIn a felhasználhatók a modul a jegyzékfájlban.</span><span class="sxs-lookup"><span data-stu-id="9ba85-116">Some of the values from the PSSnapIn (such as Description) can be reused within the module manifest.</span></span>

<span data-ttu-id="9ba85-117">A `RootModule` a moduljegyzékben tulajdonság állítható a parancsmagok végrehajtása szerelvényfájlba (dll) nevére.</span><span class="sxs-lookup"><span data-stu-id="9ba85-117">The `RootModule` property in the module manifest should be set to the name of the assembly (dll) implementing the cmdlets.</span></span>

### <a name="the-net-portability-analyzer-aka-apiport"></a><span data-ttu-id="9ba85-118">A .NET-hordozhatóságot Analyzer (más néven APIPort)</span><span class="sxs-lookup"><span data-stu-id="9ba85-118">The .NET Portability Analyzer (aka APIPort)</span></span>

<span data-ttu-id="9ba85-119">Port modulokkal készült Windows PowerShell használata a PowerShell Core, kezdje a [.NET hordozhatóságot elemző][].</span><span class="sxs-lookup"><span data-stu-id="9ba85-119">To port modules written for Windows PowerShell to work with PowerShell Core, start with the [.NET Portability Analyzer][].</span></span> <span data-ttu-id="9ba85-120">Futtassa ezt az eszközt annak meghatározásához, hogy a .NET API-k, a modul használt kompatibilisek-e a .NET-keretrendszer, a .NET Core és az egyéb .NET-modulok a lefordított szerelvényben.</span><span class="sxs-lookup"><span data-stu-id="9ba85-120">Run this tool against your compiled assembly to determine if the .NET APIs used in the module are compatible with .NET Framework, .NET Core, and other .NET runtimes.</span></span> <span data-ttu-id="9ba85-121">Az eszköz másik API-k javasol, ha vannak ilyenek.</span><span class="sxs-lookup"><span data-stu-id="9ba85-121">The tool suggests alternate APIs if they exist.</span></span> <span data-ttu-id="9ba85-122">Ellenkező esetben előfordulhat, hogy hozzá kell [futásidejű ellenőrzés][] , és korlátozhatja a funkciókat adott modulok nem érhetők el.</span><span class="sxs-lookup"><span data-stu-id="9ba85-122">Otherwise, you may need to add [runtime checks][] and restrict capabilities not available in specific runtimes.</span></span>

## <a name="creating-a-new-module"></a><span data-ttu-id="9ba85-123">Új modul létrehozása</span><span class="sxs-lookup"><span data-stu-id="9ba85-123">Creating a New Module</span></span>

<span data-ttu-id="9ba85-124">Új modul létrehozása, ha a javaslat használatára-e a [.NET CLI][].</span><span class="sxs-lookup"><span data-stu-id="9ba85-124">If creating a new module, the recommendation is to use the [.NET CLI][].</span></span>

### <a name="installing-the-powershell-standard-module-template"></a><span data-ttu-id="9ba85-125">A PowerShell szabványos modul sablon telepítése</span><span class="sxs-lookup"><span data-stu-id="9ba85-125">Installing the PowerShell Standard Module Template</span></span>

<span data-ttu-id="9ba85-126">A .NET parancssori felület telepítése után telepítse a könyvtár létrehozni egy egyszerű PowerShell-modul.</span><span class="sxs-lookup"><span data-stu-id="9ba85-126">Once the .NET CLI is installed, install a template library to generate a simple PowerShell module.</span></span>
<span data-ttu-id="9ba85-127">A modul Windows PowerShell, a PowerShell Core, Windows, Linux és macOS kompatibilis lesz.</span><span class="sxs-lookup"><span data-stu-id="9ba85-127">The module will be compatible with Windows PowerShell, PowerShell Core, Windows, Linux, and macOS.</span></span>

<span data-ttu-id="9ba85-128">Az alábbi példa bemutatja, hogyan telepítheti a sablont:</span><span class="sxs-lookup"><span data-stu-id="9ba85-128">The following example shows how to install the template:</span></span>

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

### <a name="creating-a-new-module-project"></a><span data-ttu-id="9ba85-129">Új modul-projekt létrehozása</span><span class="sxs-lookup"><span data-stu-id="9ba85-129">Creating a New Module Project</span></span>

<span data-ttu-id="9ba85-130">A sablon telepítése után létrehozhat egy új PowerShell modul projektet, hogy a sablon használatával.</span><span class="sxs-lookup"><span data-stu-id="9ba85-130">After the template is installed, you can create a new PowerShell module project using that template.</span></span> <span data-ttu-id="9ba85-131">Ebben a példában a mintamodul nevezik "myModule".</span><span class="sxs-lookup"><span data-stu-id="9ba85-131">In this example, the sample module is called 'myModule'.</span></span>

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

### <a name="building-the-module"></a><span data-ttu-id="9ba85-132">A modul</span><span class="sxs-lookup"><span data-stu-id="9ba85-132">Building the Module</span></span>

<span data-ttu-id="9ba85-133">Standard szintű .NET CLI-parancsok használatával állítsa össze a projektet.</span><span class="sxs-lookup"><span data-stu-id="9ba85-133">Use standard .NET CLI commands to build the project.</span></span>

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

### <a name="testing-the-module"></a><span data-ttu-id="9ba85-134">A modul tesztelése</span><span class="sxs-lookup"><span data-stu-id="9ba85-134">Testing the Module</span></span>

<span data-ttu-id="9ba85-135">Ha a modul, importálás, és hajtsa végre a minta parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="9ba85-135">After building the module, you can import it and execute the sample cmdlet.</span></span>

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

<span data-ttu-id="9ba85-136">A következő szakaszok ismertetik részletesebben néhány, az a sablon által használt technológiák.</span><span class="sxs-lookup"><span data-stu-id="9ba85-136">The following sections describe in detail some of the technologies used by this template.</span></span>

## <a name="net-standard-library"></a><span data-ttu-id="9ba85-137">.NET standard kódtár</span><span class="sxs-lookup"><span data-stu-id="9ba85-137">.NET Standard Library</span></span>

<span data-ttu-id="9ba85-138">[.NET standard][] .NET API-k minden .NET-implementációkban elérhető formális meghatározását.</span><span class="sxs-lookup"><span data-stu-id="9ba85-138">[.NET Standard][] is a formal specification of .NET APIs that are available in all .NET implementations.</span></span> <span data-ttu-id="9ba85-139">A felügyelt kód a .NET-keretrendszer és a .NET Core verziók, amelyek kompatibilisek a .NET Standard verzió a .NET Standard együttműködik.</span><span class="sxs-lookup"><span data-stu-id="9ba85-139">Managed code targeting .NET Standard works with the .NET Framework and .NET Core versions that are compatible with that version of the .NET Standard.</span></span>

> [!NOTE]
> <span data-ttu-id="9ba85-140">Bár az API-k .NET standardban is létezik, a .NET Core API-implementáció generálhat egy `PlatformNotSupportedException` futásidőben, így a Windows PowerShell és a PowerShell Core, a kompatibilitás ellenőrzéséhez az ajánlott eljárás, hogy a modul mindkét környezetekben tesztek futtatása.</span><span class="sxs-lookup"><span data-stu-id="9ba85-140">Although an API may exist in .NET Standard, the API implementation in .NET Core may throw a `PlatformNotSupportedException` at runtime, so to verify compatibility with Windows PowerShell and PowerShell Core, the best practice is to run tests for your module within both environments.</span></span>
> <span data-ttu-id="9ba85-141">Is futtathatja tesztek Linux és MacOS rendszereken, ha a modul az célja, hogy a platformok közötti lehet.</span><span class="sxs-lookup"><span data-stu-id="9ba85-141">Also run tests on Linux and macOS if your module is intended to be cross-platform.</span></span>

<span data-ttu-id="9ba85-142">.NET Standard célcsoportkezelés segítségével győződjön meg arról, hogy alakul ki a modult, mert inkompatibilis API-k nem véletlenül ismerje meg a modulba.</span><span class="sxs-lookup"><span data-stu-id="9ba85-142">Targeting .NET Standard helps ensure that, as the module evolves, incompatible APIs don't accidentally get introduced into the module.</span></span> <span data-ttu-id="9ba85-143">Kompatibilitási problémák észlelésekor a fordítás során futásidejű helyett.</span><span class="sxs-lookup"><span data-stu-id="9ba85-143">Incompatibilities are discovered at compile time instead of runtime.</span></span>

<span data-ttu-id="9ba85-144">Azonban nem szükséges a .NET Standard-modul a Windows PowerShell és a PowerShell Core, mind a cél kompatibilis API-kkal is.</span><span class="sxs-lookup"><span data-stu-id="9ba85-144">However, it isn't required to target .NET Standard for a module to work with both Windows PowerShell and PowerShell Core, as long as you use compatible APIs.</span></span> <span data-ttu-id="9ba85-145">A köztes nyelv (Illinois), a két modulok között kompatibilis.</span><span class="sxs-lookup"><span data-stu-id="9ba85-145">The Intermediate Language (IL) is compatible between the two runtimes.</span></span> <span data-ttu-id="9ba85-146">Célba .NET-keretrendszer 4.6.1-es verziója, amely nagy .NET Standard 2.0-val kompatibilis.</span><span class="sxs-lookup"><span data-stu-id="9ba85-146">You can target .NET Framework 4.6.1, which is compatible with .NET Standard 2.0.</span></span> <span data-ttu-id="9ba85-147">Ha nem használja a .NET Standard 2.0 kívül API-k, majd a modul együttműködik PowerShell Core 6-os jelölője nélkül.</span><span class="sxs-lookup"><span data-stu-id="9ba85-147">If you don't use APIs outside of .NET Standard 2.0, then your module works with PowerShell Core 6 without recompilation.</span></span>

## <a name="powershell-standard-library"></a><span data-ttu-id="9ba85-148">PowerShell Standard kódtár</span><span class="sxs-lookup"><span data-stu-id="9ba85-148">PowerShell Standard Library</span></span>

<span data-ttu-id="9ba85-149">A [PowerShell Standard][] könyvtár a PowerShell API-k elérhető az összes PowerShell nagyobb vagy egyenlő a verzióra, a standard verzióban formális meghatározását.</span><span class="sxs-lookup"><span data-stu-id="9ba85-149">The [PowerShell Standard][] library is a formal specification of PowerShell APIs available in all PowerShell versions greater than or equal to the version of that standard.</span></span>

<span data-ttu-id="9ba85-150">Ha például [PowerShell szabványos 5.1][] kompatibilis a Windows PowerShell 5.1-es és a PowerShell Core 6.0 vagy újabb.</span><span class="sxs-lookup"><span data-stu-id="9ba85-150">For example, [PowerShell Standard 5.1][] is compatible with both Windows PowerShell 5.1 and PowerShell Core 6.0 or newer.</span></span>

<span data-ttu-id="9ba85-151">Azt javasoljuk, hogy a modul PowerShell Standard kódtár használatával összeállíthatja.</span><span class="sxs-lookup"><span data-stu-id="9ba85-151">We recommend you compile your module using PowerShell Standard Library.</span></span> <span data-ttu-id="9ba85-152">A kódtár biztosítja, hogy az API-k rendelkezésre álló és a Windows PowerShell és a PowerShell Core 6-os megvalósított.</span><span class="sxs-lookup"><span data-stu-id="9ba85-152">The library ensures the APIs are available and implemented in both Windows PowerShell and PowerShell Core 6.</span></span>
<span data-ttu-id="9ba85-153">Mindig legyen továbbítást-kompatibilis PowerShell szabványos célja.</span><span class="sxs-lookup"><span data-stu-id="9ba85-153">PowerShell Standard is intended to always be forwards-compatible.</span></span> <span data-ttu-id="9ba85-154">A modul PowerShell szabványos könyvtár 5.1 használatával létrehozott mindig lesz kompatibilis PowerShell jövőbeli verzióiban.</span><span class="sxs-lookup"><span data-stu-id="9ba85-154">A module built using PowerShell Standard Library 5.1 will always be compatible with future versions of PowerShell.</span></span>

## <a name="module-manifest"></a><span data-ttu-id="9ba85-155">Moduljegyzék</span><span class="sxs-lookup"><span data-stu-id="9ba85-155">Module Manifest</span></span>

### <a name="indicating-compatibility-with-windows-powershell-and-powershell-core"></a><span data-ttu-id="9ba85-156">A Windows PowerShell és a PowerShell Core kompatibilitásukat</span><span class="sxs-lookup"><span data-stu-id="9ba85-156">Indicating Compatibility With Windows PowerShell and PowerShell Core</span></span>

<span data-ttu-id="9ba85-157">Miután ellenőrizte, hogy a modul Windows PowerShell és a PowerShell Core is működik, a moduljegyzékben explicit módon jelzi, hogy kompatibilitási használatával a [CompatiblePSEditions][] tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="9ba85-157">After validating that your module works with both Windows PowerShell and PowerShell Core, the module manifest should explicitly indicate compatibility by using the [CompatiblePSEditions][] property.</span></span> <span data-ttu-id="9ba85-158">Érték `Desktop` azt jelenti, hogy a modul kompatibilis a Windows PowerShell-lel, miközben érték `Core` azt jelenti, hogy a modul a PowerShell Core kompatibilis.</span><span class="sxs-lookup"><span data-stu-id="9ba85-158">A value of `Desktop` means that the module is compatible with Windows PowerShell, while a value of `Core` means that the module is compatible with PowerShell Core.</span></span> <span data-ttu-id="9ba85-159">Mind `Desktop` és `Core` azt jelenti, hogy a modul Windows PowerShell és a PowerShell Core kompatibilis.</span><span class="sxs-lookup"><span data-stu-id="9ba85-159">Including both `Desktop` and `Core` means that the module is compatible with both Windows PowerShell and PowerShell Core.</span></span>

> [!NOTE]
> <span data-ttu-id="9ba85-160">`Core` nem automatikusan jelenti, hogy a modul Windows, Linux és macOS kompatibilis.</span><span class="sxs-lookup"><span data-stu-id="9ba85-160">`Core` does not automatically mean that the module is compatible with Windows, Linux, and macOS.</span></span>
> <span data-ttu-id="9ba85-161">A **CompatiblePSEditions** tulajdonság a PowerShell 5-ös verziójának jelent meg.</span><span class="sxs-lookup"><span data-stu-id="9ba85-161">The **CompatiblePSEditions** property was introduced in PowerShell v5.</span></span> <span data-ttu-id="9ba85-162">Modul jegyzékfájlok használó a **CompatiblePSEditions** tulajdonság nem sikerült betölteni a PowerShell 5-ös verziójának korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="9ba85-162">Module manifests that use the **CompatiblePSEditions** property fail to load in versions prior to PowerShell v5.</span></span>

### <a name="indicating-os-compatibility"></a><span data-ttu-id="9ba85-163">Operációsrendszer-kompatibilitás jelző</span><span class="sxs-lookup"><span data-stu-id="9ba85-163">Indicating OS Compatibility</span></span>

<span data-ttu-id="9ba85-164">Először ellenőrizze, hogy a modul a Linux és MacOS rendszeren működik.</span><span class="sxs-lookup"><span data-stu-id="9ba85-164">First, validate that your module works on Linux and macOS.</span></span> <span data-ttu-id="9ba85-165">Ezután adja meg az operációs rendszereket a moduljegyzékben való kompatibilitás érdekében.</span><span class="sxs-lookup"><span data-stu-id="9ba85-165">Next, indicate compatibility with those operating systems in the module manifest.</span></span> <span data-ttu-id="9ba85-166">Ez megkönnyíti a felhasználók számára való a modul az operációs rendszer, ha közzé a [PowerShell-galéria][].</span><span class="sxs-lookup"><span data-stu-id="9ba85-166">This makes it easier for users to find your module for their operating system when published to the [PowerShell Gallery][].</span></span>

<span data-ttu-id="9ba85-167">A modul a jegyzékfájlban a `PrivateData` tulajdonság egy `PSData` alárendelt tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="9ba85-167">Within the module manifest, the `PrivateData` property has a `PSData` sub-property.</span></span> <span data-ttu-id="9ba85-168">A választható `Tags` tulajdonsága `PSData` egy diagnosztikakonfigurációs tömböt foglal értékek láthatók a PowerShell-galériában.</span><span class="sxs-lookup"><span data-stu-id="9ba85-168">The optional `Tags` property of `PSData` takes an array of values that show up in PowerShell Gallery.</span></span> <span data-ttu-id="9ba85-169">A PowerShell-galériából a következő kompatibilitási értékeket támogatja:</span><span class="sxs-lookup"><span data-stu-id="9ba85-169">The PowerShell Gallery supports the following compatibility values:</span></span>

| <span data-ttu-id="9ba85-170">Címke</span><span class="sxs-lookup"><span data-stu-id="9ba85-170">Tag</span></span>               | <span data-ttu-id="9ba85-171">Leírás</span><span class="sxs-lookup"><span data-stu-id="9ba85-171">Description</span></span>                                |
|-------------------|--------------------------------------------|
| <span data-ttu-id="9ba85-172">PSEdition_Core</span><span class="sxs-lookup"><span data-stu-id="9ba85-172">PSEdition_Core</span></span>    | <span data-ttu-id="9ba85-173">A PowerShell Core 6-kompatibilis</span><span class="sxs-lookup"><span data-stu-id="9ba85-173">Compatible with PowerShell Core 6</span></span>          |
| <span data-ttu-id="9ba85-174">PSEdition_Desktop</span><span class="sxs-lookup"><span data-stu-id="9ba85-174">PSEdition_Desktop</span></span> | <span data-ttu-id="9ba85-175">Kompatibilis a Windows PowerShell-lel</span><span class="sxs-lookup"><span data-stu-id="9ba85-175">Compatible with Windows PowerShell</span></span>         |
| <span data-ttu-id="9ba85-176">Windows</span><span class="sxs-lookup"><span data-stu-id="9ba85-176">Windows</span></span>           | <span data-ttu-id="9ba85-177">Windows-kompatibilis</span><span class="sxs-lookup"><span data-stu-id="9ba85-177">Compatible with Windows</span></span>                    |
| <span data-ttu-id="9ba85-178">Linux</span><span class="sxs-lookup"><span data-stu-id="9ba85-178">Linux</span></span>             | <span data-ttu-id="9ba85-179">Linux (nincs megadott disztribúció) kompatibilis</span><span class="sxs-lookup"><span data-stu-id="9ba85-179">Compatible with Linux (no specific distro)</span></span> |
| <span data-ttu-id="9ba85-180">macOS</span><span class="sxs-lookup"><span data-stu-id="9ba85-180">macOS</span></span>             | <span data-ttu-id="9ba85-181">MacOS-kompatibilis</span><span class="sxs-lookup"><span data-stu-id="9ba85-181">Compatible with macOS</span></span>                      |

<span data-ttu-id="9ba85-182">Példa:</span><span class="sxs-lookup"><span data-stu-id="9ba85-182">Example:</span></span>

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
[.NET Framework]: /dotnet/framework/
[.NET Core]: /dotnet/core/
[PSSnapIn]: /dotnet/api/system.management.automation.pssnapin
[New-ModuleManifest]: /powershell/module/microsoft.powershell.core/new-modulemanifest
[futásidejű ellenőrzés]: /dotnet/api/system.runtime.interopservices.runtimeinformation.frameworkdescription#System_Runtime_InteropServices_RuntimeInformation_FrameworkDescription
[runtime checks]: /dotnet/api/system.runtime.interopservices.runtimeinformation.frameworkdescription#System_Runtime_InteropServices_RuntimeInformation_FrameworkDescription
[.NET CLI]: /dotnet/core/tools/?tabs=netcore2x
[.NET Standard]: /dotnet/standard/net-standard
[PowerShell Standard]: https://github.com/PowerShell/PowerShellStandard
[PowerShell szabványos 5.1]: https://www.nuget.org/packages/PowerShellStandard.Library/5.1.0
[PowerShell Standard 5.1]: https://www.nuget.org/packages/PowerShellStandard.Library/5.1.0
[PowerShell-galéria]: https://www.powershellgallery.com
[PowerShell Gallery]: https://www.powershellgallery.com
[.NET hordozhatóságot elemző]: https://github.com/Microsoft/dotnet-apiport
[.NET Portability Analyzer]: https://github.com/Microsoft/dotnet-apiport
[CompatiblePSEditions]: /powershell/gallery/concepts/module-psedition-support
