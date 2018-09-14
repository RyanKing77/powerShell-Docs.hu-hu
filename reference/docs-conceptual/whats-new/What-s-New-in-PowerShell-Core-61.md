---
title: A PowerShell Core 6.1 újdonságai
description: Új szolgáltatásaival és módosításaival, amely a PowerShell Core 6.1
ms.date: 09/13/2018
ms.openlocfilehash: 27e7e846e9ba6ab34d83a084c2589b67a9d5cba9
ms.sourcegitcommit: b235c58b34d23317076540631f5cf83f1f309c0d
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45557304"
---
# <a name="whats-new-in-powershell-core-61"></a><span data-ttu-id="c1337-103">A PowerShell Core 6.1 újdonságai</span><span class="sxs-lookup"><span data-stu-id="c1337-103">What's New in PowerShell Core 6.1</span></span>

<span data-ttu-id="c1337-104">Alább néhány fontos új szolgáltatásokat és módosításokat vezettek be a PowerShell Core 6.1 egy kijelölt van.</span><span class="sxs-lookup"><span data-stu-id="c1337-104">Below is a selection of some of the major new features and changes that have been introduced in PowerShell Core 6.1.</span></span>

<span data-ttu-id="c1337-105">Is **tonna** "unalmas szolgáltatáshasználatot", amelyek gyorsabb és stabilabb (és sok és számos hibajavítás) PowerShell!</span><span class="sxs-lookup"><span data-stu-id="c1337-105">There's also **tons** of "boring stuff" that make PowerShell faster and more stable (plus lots and lots of bug fixes)!</span></span>
<span data-ttu-id="c1337-106">Változások teljes listájához tekintse meg a [a Githubon változásnaplójában](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="c1337-106">For a full list of changes, check out our [changelog on GitHub](https://github.com/PowerShell/PowerShell/blob/master/CHANGELOG.md).</span></span>

<span data-ttu-id="c1337-107">És közben ki az alábbi néhány nevet nevezzük, Köszönjük, hogy [összes a közösségi közreműködők](https://github.com/PowerShell/PowerShell/graphs/contributors) , amely ebben a kiadásban lehetővé tenni.</span><span class="sxs-lookup"><span data-stu-id="c1337-107">And while we call out some names below, thank you to [all of the community contributors](https://github.com/PowerShell/PowerShell/graphs/contributors) that made this release possible.</span></span>

## <a name="net-core-21"></a><span data-ttu-id="c1337-108">A .NET core 2.1-es verziója</span><span class="sxs-lookup"><span data-stu-id="c1337-108">.NET Core 2.1</span></span>

<span data-ttu-id="c1337-109">Után, a .NET Core 2.1 átkerül PowerShell Core 6.1 [májusban, amely a](https://blogs.msdn.microsoft.com/dotnet/2018/05/30/announcing-net-core-2-1/), számos fejlesztéssel a Powershellbe, így többek között:</span><span class="sxs-lookup"><span data-stu-id="c1337-109">PowerShell Core 6.1 moved to .NET Core 2.1 after it was [released in May](https://blogs.msdn.microsoft.com/dotnet/2018/05/30/announcing-net-core-2-1/), resulting in a number of improvements to PowerShell, including:</span></span>

- <span data-ttu-id="c1337-110">teljesítménnyel kapcsolatos fejlesztések (lásd: [alábbi](#performance-improvements))</span><span class="sxs-lookup"><span data-stu-id="c1337-110">performance improvements (see [below](#performance-improvements))</span></span>
- <span data-ttu-id="c1337-111">Az Alpine Linux-támogatás (előzetes verzió)</span><span class="sxs-lookup"><span data-stu-id="c1337-111">Alpine Linux support (preview)</span></span>
- <span data-ttu-id="c1337-112">[Globális eszköz támogatott .NET](/dotnet/core/tools/global-tools) – hamarosan a PowerShell az elkövetkező</span><span class="sxs-lookup"><span data-stu-id="c1337-112">[.NET global tool support](/dotnet/core/tools/global-tools) - coming soon to PowerShell</span></span>
- [`Span<T>`](/dotnet/api/system.span-1?view=netcore-2.1)

## <a name="windows-compatibility-pack-for-net-core"></a><span data-ttu-id="c1337-113">.NET Core for Windows kompatibilitási csomag</span><span class="sxs-lookup"><span data-stu-id="c1337-113">Windows Compatibility Pack for .NET Core</span></span>

<span data-ttu-id="c1337-114">A Windows, a .NET-csapattal szállított a [Windows kompatibilitási csomag a .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/11/16/announcing-the-windows-compatibility-pack-for-net-core/), szerelvényeket, amelyek számos hozzáadása egy készletét vissza a .NET Core Windows API-k eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="c1337-114">On Windows, the .NET team shipped the [Windows Compatibility Pack for .NET Core](https://blogs.msdn.microsoft.com/dotnet/2017/11/16/announcing-the-windows-compatibility-pack-for-net-core/), a set of assemblies that add a number of removed APIs back to .NET Core on Windows.</span></span>

<span data-ttu-id="c1337-115">Lehetőségekkel bővült a Windows-kompatibilitási csomag PowerShell Core 6.1-es kiadásra, hogy bármilyen modulok vagy ezekkel az API-parancsprogramok is használhatók legyenek elérhetők.</span><span class="sxs-lookup"><span data-stu-id="c1337-115">We've added the Windows Compatibility Pack to PowerShell Core 6.1 release so that any modules or scripts that use these APIs can rely on them being available.</span></span>

<span data-ttu-id="c1337-116">A Windows-kompatibilitási csomag lehetővé teszi, hogy a PowerShell Core használata **több mint 1900 parancsmagok a Windows rendszerrel szállított 2018. október 10. és a Windows Server 2019**.</span><span class="sxs-lookup"><span data-stu-id="c1337-116">The Windows Compatibility Pack enables PowerShell Core to use **more than 1900 cmdlets that ship with Windows 10 October 2018 Update and Windows Server 2019**.</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="c1337-117">Teljesítménnyel kapcsolatos fejlesztések</span><span class="sxs-lookup"><span data-stu-id="c1337-117">Performance improvements</span></span>

<span data-ttu-id="c1337-118">A PowerShell Core 6.0 végzett néhány jelentős teljesítménybeli fejlesztései.</span><span class="sxs-lookup"><span data-stu-id="c1337-118">PowerShell Core 6.0 made some significant performance improvements.</span></span>
<span data-ttu-id="c1337-119">PowerShell Core 6.1 továbbfejleszti bizonyos műveletek sebessége.</span><span class="sxs-lookup"><span data-stu-id="c1337-119">PowerShell Core 6.1 continues to improve the speed of certain operations.</span></span>

<span data-ttu-id="c1337-120">Ha például `Group-Object` 66 %-kal rendelkezik lett felgyorsul:</span><span class="sxs-lookup"><span data-stu-id="c1337-120">For example, `Group-Object` has been sped up by 66%:</span></span>

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Group-Object }
```

|              | <span data-ttu-id="c1337-121">Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="c1337-121">Windows PowerShell 5.1</span></span> | <span data-ttu-id="c1337-122">A PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="c1337-122">PowerShell Core 6.0</span></span> | <span data-ttu-id="c1337-123">A PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="c1337-123">PowerShell Core 6.1</span></span> |
|--------------|------------------------|---------------------|---------------------|
| <span data-ttu-id="c1337-124">Idő (mp)</span><span class="sxs-lookup"><span data-stu-id="c1337-124">Time (sec)</span></span>   | <span data-ttu-id="c1337-125">25.178</span><span class="sxs-lookup"><span data-stu-id="c1337-125">25.178</span></span>                 | <span data-ttu-id="c1337-126">19.653</span><span class="sxs-lookup"><span data-stu-id="c1337-126">19.653</span></span>              | <span data-ttu-id="c1337-127">6.641</span><span class="sxs-lookup"><span data-stu-id="c1337-127">6.641</span></span>               |
| <span data-ttu-id="c1337-128">Gyorsulás figyelhető meg (%)</span><span class="sxs-lookup"><span data-stu-id="c1337-128">Speed-up (%)</span></span> | <span data-ttu-id="c1337-129">N.a.</span><span class="sxs-lookup"><span data-stu-id="c1337-129">N/A</span></span>                    | <span data-ttu-id="c1337-130">21.9 %</span><span class="sxs-lookup"><span data-stu-id="c1337-130">21.9%</span></span>               | <span data-ttu-id="c1337-131">66.2 %</span><span class="sxs-lookup"><span data-stu-id="c1337-131">66.2%</span></span>               |

<span data-ttu-id="c1337-132">Hasonlóképpen az alábbihoz hasonló rendezési forgatókönyvek javult több mint 15 %-kal:</span><span class="sxs-lookup"><span data-stu-id="c1337-132">Similarly, sorting scenarios like this one have improved by more than 15%:</span></span>

```powershell
Measure-Command { 1..100000 | % {Get-Random -Minimum 1 -Maximum 10000} | Sort-Object }
```

|              | <span data-ttu-id="c1337-133">Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="c1337-133">Windows PowerShell 5.1</span></span> | <span data-ttu-id="c1337-134">A PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="c1337-134">PowerShell Core 6.0</span></span> | <span data-ttu-id="c1337-135">A PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="c1337-135">PowerShell Core 6.1</span></span> |
|--------------|------------------------|---------------------|---------------------|
| <span data-ttu-id="c1337-136">Idő (mp)</span><span class="sxs-lookup"><span data-stu-id="c1337-136">Time (sec)</span></span>   | <span data-ttu-id="c1337-137">12.170</span><span class="sxs-lookup"><span data-stu-id="c1337-137">12.170</span></span>                 | <span data-ttu-id="c1337-138">8.493</span><span class="sxs-lookup"><span data-stu-id="c1337-138">8.493</span></span>               | <span data-ttu-id="c1337-139">7.08</span><span class="sxs-lookup"><span data-stu-id="c1337-139">7.08</span></span>                |
| <span data-ttu-id="c1337-140">Gyorsulás figyelhető meg (%)</span><span class="sxs-lookup"><span data-stu-id="c1337-140">Speed-up (%)</span></span> | <span data-ttu-id="c1337-141">N.a.</span><span class="sxs-lookup"><span data-stu-id="c1337-141">N/A</span></span>                    | <span data-ttu-id="c1337-142">30.2 %</span><span class="sxs-lookup"><span data-stu-id="c1337-142">30.2%</span></span>               | <span data-ttu-id="c1337-143">16.6 %</span><span class="sxs-lookup"><span data-stu-id="c1337-143">16.6%</span></span>               |

<span data-ttu-id="c1337-144">`Import-Csv` azt is lett felgyorsul jelentősen regresszió után a Windows PowerShellben.</span><span class="sxs-lookup"><span data-stu-id="c1337-144">`Import-Csv` has also been sped up significantly after a regression from Windows PowerShell.</span></span>
<span data-ttu-id="c1337-145">Az alábbi példa egy teszt CSV 26,616 sorok és oszlopok hat használja:</span><span class="sxs-lookup"><span data-stu-id="c1337-145">The following example uses a test CSV with 26,616 rows and six columns:</span></span>

```powershell
Measure-Command {$a = Import-Csv foo.csv}
```

|              | <span data-ttu-id="c1337-146">Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="c1337-146">Windows PowerShell 5.1</span></span> | <span data-ttu-id="c1337-147">A PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="c1337-147">PowerShell Core 6.0</span></span> | <span data-ttu-id="c1337-148">A PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="c1337-148">PowerShell Core 6.1</span></span>    |
|--------------|------------------------|---------------------|------------------------|
| <span data-ttu-id="c1337-149">Idő (mp)</span><span class="sxs-lookup"><span data-stu-id="c1337-149">Time (sec)</span></span>   | <span data-ttu-id="c1337-150">0.441</span><span class="sxs-lookup"><span data-stu-id="c1337-150">0.441</span></span>                  | <span data-ttu-id="c1337-151">1.069</span><span class="sxs-lookup"><span data-stu-id="c1337-151">1.069</span></span>               | <span data-ttu-id="c1337-152">0.268</span><span class="sxs-lookup"><span data-stu-id="c1337-152">0.268</span></span>                  |
| <span data-ttu-id="c1337-153">Gyorsulás figyelhető meg (%)</span><span class="sxs-lookup"><span data-stu-id="c1337-153">Speed-up (%)</span></span> | <span data-ttu-id="c1337-154">N.a.</span><span class="sxs-lookup"><span data-stu-id="c1337-154">N/A</span></span>                    | <span data-ttu-id="c1337-155">-142.4 %</span><span class="sxs-lookup"><span data-stu-id="c1337-155">-142.4%</span></span>             | <span data-ttu-id="c1337-156">74.9 % (39.2 % WPS)</span><span class="sxs-lookup"><span data-stu-id="c1337-156">74.9% (39.2% from WPS)</span></span> |

<span data-ttu-id="c1337-157">Végül, a JSON-t átalakítás `PSObject` rendelkezik lett felgyorsul több mint 50 %-kal Windows PowerShell óta.</span><span class="sxs-lookup"><span data-stu-id="c1337-157">Lastly, conversion from JSON into `PSObject` has been sped up by more than 50% since Windows PowerShell.</span></span>
<span data-ttu-id="c1337-158">Az alábbi példa ~ 2 MB-os teszt JSON-fájlt használ:</span><span class="sxs-lookup"><span data-stu-id="c1337-158">The following example uses a ~2MB test JSON file:</span></span>

```powershell
Measure-Command {Get-Content .\foo.json | ConvertFrom-Json}
```

|              | <span data-ttu-id="c1337-159">Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="c1337-159">Windows PowerShell 5.1</span></span> | <span data-ttu-id="c1337-160">A PowerShell Core 6.0</span><span class="sxs-lookup"><span data-stu-id="c1337-160">PowerShell Core 6.0</span></span> | <span data-ttu-id="c1337-161">A PowerShell Core 6.1</span><span class="sxs-lookup"><span data-stu-id="c1337-161">PowerShell Core 6.1</span></span>    |
|--------------|------------------------|---------------------|------------------------|
| <span data-ttu-id="c1337-162">Idő (mp)</span><span class="sxs-lookup"><span data-stu-id="c1337-162">Time (sec)</span></span>   | <span data-ttu-id="c1337-163">0.259</span><span class="sxs-lookup"><span data-stu-id="c1337-163">0.259</span></span>                  | <span data-ttu-id="c1337-164">0.577</span><span class="sxs-lookup"><span data-stu-id="c1337-164">0.577</span></span>               | <span data-ttu-id="c1337-165">0.125</span><span class="sxs-lookup"><span data-stu-id="c1337-165">0.125</span></span>                  |
| <span data-ttu-id="c1337-166">Gyorsulás figyelhető meg (%)</span><span class="sxs-lookup"><span data-stu-id="c1337-166">Speed-up (%)</span></span> | <span data-ttu-id="c1337-167">N.a.</span><span class="sxs-lookup"><span data-stu-id="c1337-167">N/A</span></span>                    | <span data-ttu-id="c1337-168">-122.8 %</span><span class="sxs-lookup"><span data-stu-id="c1337-168">-122.8%</span></span>             | <span data-ttu-id="c1337-169">78.3 % (51.7 % WPS)</span><span class="sxs-lookup"><span data-stu-id="c1337-169">78.3% (51.7% from WPS)</span></span> |

## <a name="check-system32-for-compatible-inbox-modules-on-windows"></a><span data-ttu-id="c1337-170">Ellenőrizze `system32` a Windows kompatibilis Beérkezett üzenetek modulok</span><span class="sxs-lookup"><span data-stu-id="c1337-170">Check `system32` for compatible inbox modules on Windows</span></span>

<span data-ttu-id="c1337-171">A Windows 10-es 1809 update és a Windows Server 2019 frissítettük a Beérkezett üzenetek kell megjelölni kompatibilis PowerShell Core a PowerShell-modulok száma.</span><span class="sxs-lookup"><span data-stu-id="c1337-171">In the Windows 10 1809 update and Windows Server 2019, we updated a number of inbox PowerShell modules to mark them as compatible with PowerShell Core.</span></span>

<span data-ttu-id="c1337-172">PowerShell Core 6.1 indulásakor, automatikus módon kiegészül `$windir\System32` részeként a `PSModulePath` környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="c1337-172">When PowerShell Core 6.1 starts up, it will automatically include `$windir\System32` as part of the `PSModulePath` environment variable.</span></span>
<span data-ttu-id="c1337-173">Azonban csak jelezzék modulok `Get-Module` és `Import-Module` ha annak `CompatiblePSEdition` kompatibilis van megjelölve `Core`.</span><span class="sxs-lookup"><span data-stu-id="c1337-173">However, it only exposes modules to `Get-Module` and `Import-Module` if its `CompatiblePSEdition` is marked as compatible with `Core`.</span></span>


```powershell
Get-Module -ListAvailable
```

> [!NOTE]
> <span data-ttu-id="c1337-174">Attól függően, hogy milyen szerepkörök és szolgáltatások telepítve vannak a különböző elérhető modulok jelenhet meg.</span><span class="sxs-lookup"><span data-stu-id="c1337-174">You may see different available modules depending on what roles and features are installed.</span></span>

```Output
...
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                                PSEdition ExportedCommands
---------- -------    ----                                --------- ----------------
Manifest   2.0.1.0    Appx                                Core,Desk {Add-AppxPackage, Get-AppxPackage, Get-AppxPacka...
Manifest   1.0.0.0    BitLocker                           Core,Desk {Unlock-BitLocker, Suspend-BitLocker, Resume-Bit...
Manifest   1.0.0.0    DnsClient                           Core,Desk {Resolve-DnsName, Clear-DnsClientCache, Get-DnsC...
Manifest   1.0.0.0    HgsDiagnostics                      Core,Desk {New-HgsTraceTarget, Get-HgsTrace, Get-HgsTraceF...
Binary     2.0.0.0    Hyper-V                             Core,Desk {Add-VMAssignableDevice, Add-VMDvdDrive, Add-VMF...
Binary     1.1        Hyper-V                             Core,Desk {Add-VMDvdDrive, Add-VMFibreChannelHba, Add-VMHa...
Manifest   2.0.0.0    NetAdapter                          Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetEventPacketCapture               Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                             Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                              Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                              Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                         Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam                       Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetWNV                              Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   2.0.0.0    TrustedPlatformModule               Core,Desk {Get-Tpm, Initialize-Tpm, Clear-Tpm, Unblock-Tpm...
...
```

<span data-ttu-id="c1337-175">Minden modul használatával megjeleníthető a viselkedést felülírhatja a `-SkipEditionCheck` paraméter váltani.</span><span class="sxs-lookup"><span data-stu-id="c1337-175">You can override this behavior to show all modules using the `-SkipEditionCheck` switch parameter.</span></span>
<span data-ttu-id="c1337-176">Is elérhetővé tettünk egy `PSEdition` tulajdonság a táblázatos kimenetéhez.</span><span class="sxs-lookup"><span data-stu-id="c1337-176">We've also added a `PSEdition` property to the table output.</span></span>

```powershell
Get-Module Net* -ListAvailable -SkipEditionCheck
```

```Output
    Directory: C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules

ModuleType Version    Name                        PSEdition ExportedCommands
---------- -------    ----                        --------- ----------------
Manifest   2.0.0.0    NetAdapter                  Core,Desk {Disable-NetAdapter, Disable-NetAdapterBinding, ...
Manifest   1.0.0.0    NetConnection               Desk      {Get-NetConnectionProfile, Set-NetConnectionProf...
Manifest   1.0.0.0    NetDiagnostics              Desk      Get-NetView
Manifest   1.0.0.0    NetEventPacketCapture       Core,Desk {New-NetEventSession, Remove-NetEventSession, Ge...
Manifest   2.0.0.0    NetLbfo                     Core,Desk {Add-NetLbfoTeamMember, Add-NetLbfoTeamNic, Get-...
Manifest   1.0.0.0    NetNat                      Core,Desk {Get-NetNat, Get-NetNatExternalAddress, Get-NetN...
Manifest   2.0.0.0    NetQos                      Core,Desk {Get-NetQosPolicy, Set-NetQosPolicy, Remove-NetQ...
Manifest   2.0.0.0    NetSecurity                 Core,Desk {Get-DAPolicyChange, New-NetIPsecAuthProposal, N...
Manifest   1.0.0.0    NetSwitchTeam               Core,Desk {New-NetSwitchTeam, Remove-NetSwitchTeam, Get-Ne...
Manifest   1.0.0.0    NetTCPIP                    Desk      {Get-NetIPAddress, Get-NetIPInterface, Get-NetIP...
Manifest   1.0.0.0    NetWNV                      Core,Desk {Get-NetVirtualizationProviderAddress, Get-NetVi...
Manifest   1.0.0.0    NetworkConnectivityStatus   Desk      {Get-DAConnectionStatus, Get-NCSIPolicyConfigura...
Manifest   1.0.0.0    NetworkSwitchManager        Desk      {Disable-NetworkSwitchEthernetPort, Enable-Netwo...
Manifest   1.0.0.0    NetworkTransition           Desk      {Add-NetIPHttpsCertBinding, Disable-NetDnsTransi...
```

<span data-ttu-id="c1337-177">Ezzel a viselkedéssel kapcsolatos további információkért tekintse meg [PowerShell RFC0025](https://github.com/PowerShell/PowerShell-RFC/blob/master/2-Draft-Accepted/RFC0025-PSCore6-and-Windows-Modules.md).</span><span class="sxs-lookup"><span data-stu-id="c1337-177">For more information about this behavior, check out [PowerShell RFC0025](https://github.com/PowerShell/PowerShell-RFC/blob/master/2-Draft-Accepted/RFC0025-PSCore6-and-Windows-Modules.md).</span></span>

## <a name="markdown-cmdlets-and-rendering"></a><span data-ttu-id="c1337-178">Markdown-parancsmagok és megjelenítési szoftverek</span><span class="sxs-lookup"><span data-stu-id="c1337-178">Markdown cmdlets and rendering</span></span>

<span data-ttu-id="c1337-179">Markdown a olvasható egyszerű szöveges dokumentumok létrehozásának alapszintű formázását, amely szabványos HTML be jeleníthetők meg.</span><span class="sxs-lookup"><span data-stu-id="c1337-179">Markdown is a standard for creating readable plaintext documents with basic formatting that can be rendered into HTML.</span></span>

<span data-ttu-id="c1337-180">Bizonyos parancsmagok tettünk elérhetővé, amelyek lehetővé teszik az átalakítás és a konzolon Markdown-dokumentumok 6.1 többek között:</span><span class="sxs-lookup"><span data-stu-id="c1337-180">We've added some cmdlets in 6.1 that allow you to convert and render Markdown documents in the console, including:</span></span>

- `ConvertFrom-Markdown`
- `Get-MarkdownOption`
- `Set-MarkdownOption`
- `Show-Markdown`

<span data-ttu-id="c1337-181">Ha például `Show-Markdown` megjelenítve egy Markdown-fájlt a konzolon:</span><span class="sxs-lookup"><span data-stu-id="c1337-181">For example, `Show-Markdown` renders a Markdown file in the console:</span></span>

![Show-Markdown-példa](./images/markdown_example.png)

<span data-ttu-id="c1337-183">Hogyan működnek a ezekkel a parancsmagokkal kapcsolatos további információkért tekintse meg [az RFC](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-Native-Markdown-Rendering.md).</span><span class="sxs-lookup"><span data-stu-id="c1337-183">For more information about how these cmdlets work, check out [this RFC](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0025-Native-Markdown-Rendering.md).</span></span>

## <a name="experimental-feature-flags"></a><span data-ttu-id="c1337-184">Kísérleti funkció jelzők</span><span class="sxs-lookup"><span data-stu-id="c1337-184">Experimental feature flags</span></span>

<span data-ttu-id="c1337-185">Kísérleti funkció jelzők engedélyezése a felhasználók számára, kapcsolja be, amely még nem lett véglegesítése funkciókat.</span><span class="sxs-lookup"><span data-stu-id="c1337-185">Experimental feature flags enable users to turn on features that haven't been finalized.</span></span>
<span data-ttu-id="c1337-186">Ezek kísérleti funkciók nem támogatottak, és előfordulhat, hogy hibák.</span><span class="sxs-lookup"><span data-stu-id="c1337-186">These experimental features aren't supported and may have bugs.</span></span>

<span data-ttu-id="c1337-187">További információ ennek a funkciónak a [PowerShell RFC0029](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0029-Support-Experimental-Features.md).</span><span class="sxs-lookup"><span data-stu-id="c1337-187">You can learn more about this feature in [PowerShell RFC0029](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0029-Support-Experimental-Features.md).</span></span>

## <a name="web-cmdlet-improvements"></a><span data-ttu-id="c1337-188">Webes parancsmag fejlesztései</span><span class="sxs-lookup"><span data-stu-id="c1337-188">Web cmdlet improvements</span></span>

<span data-ttu-id="c1337-189">Köszönhetően @markekraus, egy teljes slew kapcsolatos fejlesztések történtek-e a webalkalmazás-parancsmagok: [`Invoke-WebRequest`](/powershell/module/microsoft.powershell.utility/invoke-webrequest)</span><span class="sxs-lookup"><span data-stu-id="c1337-189">Thanks to @markekraus, a whole slew of improvements have been made to our web cmdlets: [`Invoke-WebRequest`](/powershell/module/microsoft.powershell.utility/invoke-webrequest)</span></span>
<span data-ttu-id="c1337-190">és [ `Invoke-RestMethod` ](/powershell/module/microsoft.powershell.utility/invoke-restmethod).</span><span class="sxs-lookup"><span data-stu-id="c1337-190">and [`Invoke-RestMethod`](/powershell/module/microsoft.powershell.utility/invoke-restmethod).</span></span>

- <span data-ttu-id="c1337-191">[Lekéréses kérelem #6109](https://github.com/PowerShell/PowerShell/pull/6109) -kódolási értéke UTF-8 az alapértelmezett `application-json` válaszok</span><span class="sxs-lookup"><span data-stu-id="c1337-191">[PR #6109](https://github.com/PowerShell/PowerShell/pull/6109) - default encoding set to UTF-8 for `application-json` responses</span></span>
- <span data-ttu-id="c1337-192">[Lekéréses kérelem #6018](https://github.com/PowerShell/PowerShell/pull/6018)  -  `-SkipHeaderValidation` , hogy a paraméter `Content-Type` fejlécek, amelyek nem szabványokkal kompatibilis</span><span class="sxs-lookup"><span data-stu-id="c1337-192">[PR #6018](https://github.com/PowerShell/PowerShell/pull/6018) - `-SkipHeaderValidation` parameter to allow `Content-Type` headers that aren't standards-compliant</span></span>
- <span data-ttu-id="c1337-193">[Lekéréses kérelem #5972](https://github.com/PowerShell/PowerShell/pull/5972)  -  `Form` paraméter támogatása egyszerűsített `multipart/form-data` támogatása</span><span class="sxs-lookup"><span data-stu-id="c1337-193">[PR #5972](https://github.com/PowerShell/PowerShell/pull/5972) - `Form` parameter to support simplified `multipart/form-data` support</span></span>
- <span data-ttu-id="c1337-194">[Lekéréses kérelem #6338](https://github.com/PowerShell/PowerShell/pull/6338) – megfelelő, a kis-és kapcsolat kulcsok kezelése</span><span class="sxs-lookup"><span data-stu-id="c1337-194">[PR #6338](https://github.com/PowerShell/PowerShell/pull/6338) - Compliant, case-insensitive handling of relation keys</span></span>
- <span data-ttu-id="c1337-195">[Lekéréses kérelem #6447](https://github.com/PowerShell/PowerShell/pull/6447) -hozzáadása `-Resume` paraméter webes parancsmagok esetében</span><span class="sxs-lookup"><span data-stu-id="c1337-195">[PR #6447](https://github.com/PowerShell/PowerShell/pull/6447) - Add `-Resume` parameter for web cmdlets</span></span>

## <a name="remoting-improvements"></a><span data-ttu-id="c1337-196">Távoli eljáráshívás fejlesztései</span><span class="sxs-lookup"><span data-stu-id="c1337-196">Remoting improvements</span></span>

### <a name="powershell-direct-tries-to-use-powershell-core-first"></a><span data-ttu-id="c1337-197">PowerShell Directet elsőként próbálja használni a PowerShell Core</span><span class="sxs-lookup"><span data-stu-id="c1337-197">PowerShell Direct tries to use PowerShell Core first</span></span>

<span data-ttu-id="c1337-198">[PowerShell Directet](/virtualization/hyper-v-on-windows/user-guide/powershell-direct) PowerShell és a Hyper-V, amely lehetővé teszi, hogy csatlakozni a Hyper-V virtuális gép nincs hálózati kapcsolat vagy más távoli felügyeleti szolgáltatások szolgáltatása.</span><span class="sxs-lookup"><span data-stu-id="c1337-198">[PowerShell Direct](/virtualization/hyper-v-on-windows/user-guide/powershell-direct) is a feature of PowerShell and Hyper-V that allows you to connect to a Hyper-V VM without network connectivity or other remote management services.</span></span>

<span data-ttu-id="c1337-199">Múltbeli időpont a PowerShell Directet csatlakoztatva a virtuális gépen a Beérkezett fájlok Windows PowerShell-példány használatával.</span><span class="sxs-lookup"><span data-stu-id="c1337-199">In the past, PowerShell Direct connected using the inbox Windows PowerShell instance on the VM.</span></span>
<span data-ttu-id="c1337-200">Most, PowerShell Direct először használatával próbál kapcsolódni az elérhető `pwsh.exe` a a `PATH` környezeti változót.</span><span class="sxs-lookup"><span data-stu-id="c1337-200">Now, PowerShell Direct first attempts to connect using any available `pwsh.exe` on the `PATH` environment variable.</span></span>
<span data-ttu-id="c1337-201">Ha `pwsh.exe` nem érhető el, PowerShell Direct visszavált használandó `powershell.exe`.</span><span class="sxs-lookup"><span data-stu-id="c1337-201">If `pwsh.exe` isn't available, PowerShell Direct falls back to use `powershell.exe`.</span></span>

### <a name="enable-psremoting-now-creates-separate-remoting-endpoints-for-preview-versions"></a><span data-ttu-id="c1337-202">`Enable-PSRemoting` ekkor létrehozza az előzetes verziókban külön távoli eljáráshívás végpontok</span><span class="sxs-lookup"><span data-stu-id="c1337-202">`Enable-PSRemoting` now creates separate remoting endpoints for preview versions</span></span>

<span data-ttu-id="c1337-203">`Enable-PSRemoting` most létrehoz két távoli eljáráshívás munkamenet-konfigurációk:</span><span class="sxs-lookup"><span data-stu-id="c1337-203">`Enable-PSRemoting` now creates two remoting session configurations:</span></span>

- <span data-ttu-id="c1337-204">Egy a PowerShell főverziója.</span><span class="sxs-lookup"><span data-stu-id="c1337-204">One for the major version of PowerShell.</span></span> <span data-ttu-id="c1337-205">Ha például`PowerShell.6`.</span><span class="sxs-lookup"><span data-stu-id="c1337-205">For example,`PowerShell.6`.</span></span> <span data-ttu-id="c1337-206">Ezt a végpontot, amely képes lehet hivatkozni alverzió frissítések között, a "rendszerszintű" PowerShell 6-os munkamenet-konfiguráció</span><span class="sxs-lookup"><span data-stu-id="c1337-206">This endpoint that can be relied upon across minor version updates as the "system-wide" PowerShell 6 session configuration</span></span>
- <span data-ttu-id="c1337-207">Egy verzióspecifikus munkamenet-konfiguráció, például: `PowerShell.6.1.0`</span><span class="sxs-lookup"><span data-stu-id="c1337-207">One version-specific session configuration, for example: `PowerShell.6.1.0`</span></span>

<span data-ttu-id="c1337-208">Ez a viselkedés akkor hasznos, ha ugyanazon a gépen több PowerShell 6-os verzió telepítve, és elérhető legyen.</span><span class="sxs-lookup"><span data-stu-id="c1337-208">This behavior is useful if you want to have multiple PowerShell 6 versions installed and accessible on the same machine.</span></span>

<span data-ttu-id="c1337-209">Továbbá PowerShell előzetes verziója mostantól igénybe a saját távoli eljáráshívás a munkamenet-konfigurációk futtatása után a `Enable-PSRemoting` parancsmagot:</span><span class="sxs-lookup"><span data-stu-id="c1337-209">Additionally, preview versions of PowerShell now get their own remoting session configurations after running the `Enable-PSRemoting` cmdlet:</span></span>

```powershell
C:\WINDOWS\system32> Enable-PSRemoting
```

<span data-ttu-id="c1337-210">A kimeneti eltérő, ha még nem állított be a Rendszerfelügyeleti webszolgáltatások előtt lehet.</span><span class="sxs-lookup"><span data-stu-id="c1337-210">Your output may be different if you haven't set up WinRM before.</span></span>

```Output
WinRM is already set up to receive requests on this computer.
WinRM is already set up for remote management on this computer.
```

<span data-ttu-id="c1337-211">Ezután láthatja, hogy külön PowerShell-munkamenet konfigurációk az előzetes verzióra, és stabil összeállítja a PowerShell 6-os, és minden egyes adott verziójához.</span><span class="sxs-lookup"><span data-stu-id="c1337-211">Then you can see separate PowerShell session configurations for the preview and stable builds of PowerShell 6, and for each specific version.</span></span>

```powershell
Get-PSSessionConfiguration
```

```Output
Name          : PowerShell.6.2-preview.1
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : PowerShell.6-preview
PSVersion     : 6.2
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed

Name          : powershell.6.1.0
PSVersion     : 6.1
StartupScript :
RunAsUser     :
Permission    : NT AUTHORITY\INTERACTIVE AccessAllowed, BUILTIN\Administrators AccessAllowed, BUILTIN\Remote Management Users AccessAllowed
```

### <a name="userhostport-syntax-supported-for-ssh"></a><span data-ttu-id="c1337-212">`user@host:port` az SSH-hoz támogatott szintaxis</span><span class="sxs-lookup"><span data-stu-id="c1337-212">`user@host:port` syntax supported for SSH</span></span>

<span data-ttu-id="c1337-213">SSH ügyfelek általában támogatja a kapcsolati karakterlánc a következő formátumban `user@host:port`.</span><span class="sxs-lookup"><span data-stu-id="c1337-213">SSH clients typically support a connection string in the format `user@host:port`.</span></span>
<span data-ttu-id="c1337-214">Igény szerinti hozzáadásával SSH protokollt a PowerShell-táveléréssel lehetőségekkel bővült a kapcsolati karakterlánc-formátum támogatása:</span><span class="sxs-lookup"><span data-stu-id="c1337-214">With the addition of SSH as a protocol for PowerShell Remoting, we've added support for this format of connection string:</span></span>

`Enter-PSSession -HostName fooUser@ssh.contoso.com:2222`

## <a name="msi-option-to-add-explorer-shell-context-menu-on-windows"></a><span data-ttu-id="c1337-215">MSI lehetőség a Windows Intéző rendszerhéj helyi menüjének hozzáadása</span><span class="sxs-lookup"><span data-stu-id="c1337-215">MSI option to add explorer shell context menu on Windows</span></span>

<span data-ttu-id="c1337-216">Köszönhetően @bergmeister, engedélyezheti a Windows egy helyi menüjében.</span><span class="sxs-lookup"><span data-stu-id="c1337-216">Thanks to @bergmeister, now you can enable a context menu on Windows.</span></span> <span data-ttu-id="c1337-217">Most megnyithatja a PowerShell 6.1 a rendszerre telepített bármely mappából a Windows Explorerben:</span><span class="sxs-lookup"><span data-stu-id="c1337-217">Now you can open your system-wide installation of PowerShell 6.1 from any folder in the Windows Explorer:</span></span>

![A PowerShell 6-os rendszerhéj helyi menü](./images/shell_context_menu.png)

## <a name="goodies"></a><span data-ttu-id="c1337-219">Hasznos eszközök</span><span class="sxs-lookup"><span data-stu-id="c1337-219">Goodies</span></span>

### <a name="run-as-administrator-in-the-windows-shortcut-jump-list"></a><span data-ttu-id="c1337-220">"Futtatás rendszergazdaként" a Windows helyi jump listában</span><span class="sxs-lookup"><span data-stu-id="c1337-220">"Run as Administrator" in the Windows shortcut jump list</span></span>

<span data-ttu-id="c1337-221">Köszönhetően @bergmeister, a PowerShell Core helyi jump listában mostantól tartalmazza a "Futtatás mint rendszergazda":</span><span class="sxs-lookup"><span data-stu-id="c1337-221">Thanks to @bergmeister, the PowerShell Core shortcut's jump list now includes "Run as Administrator":</span></span>

![Futtatás a PowerShell 6-os helyettesítő listában rendszergazdaként](./images/jumplist.png)

### <a name="cd---returns-to-previous-directory"></a><span data-ttu-id="c1337-223">`cd -` adja vissza az előző könyvtár</span><span class="sxs-lookup"><span data-stu-id="c1337-223">`cd -` returns to previous directory</span></span>

```powershell
C:\Windows\System32> cd C:\
C:\> cd -
C:\Windows\System32>
```

<span data-ttu-id="c1337-224">Vagy a Linux rendszeren:</span><span class="sxs-lookup"><span data-stu-id="c1337-224">Or on Linux:</span></span>

```ShellSession
PS /etc> cd /usr/bin
PS /usr/bin> cd -
PS /etc>
```

<span data-ttu-id="c1337-225">Ezenkívül `cd --` vált `$HOME`.</span><span class="sxs-lookup"><span data-stu-id="c1337-225">Also, `cd --` changes to `$HOME`.</span></span>

### `Test-Connection`

<span data-ttu-id="c1337-226">Köszönhetően @iSazonov, a [ `Test-Connection` ](/powershell/module/microsoft.powershell.management/test-connection) parancsmag rendelkezik már a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="c1337-226">Thanks to @iSazonov, the [`Test-Connection`](/powershell/module/microsoft.powershell.management/test-connection) cmdlet has been ported to PowerShell Core.</span></span>

### <a name="update-help-as-non-admin"></a><span data-ttu-id="c1337-227">`Update-Help` a nem rendszergazda</span><span class="sxs-lookup"><span data-stu-id="c1337-227">`Update-Help` as non-admin</span></span>

<span data-ttu-id="c1337-228">Kérték `Update-Help` már nem kell rendszergazdaként kell futtatnia.</span><span class="sxs-lookup"><span data-stu-id="c1337-228">By popular demand, `Update-Help` no longer needs to be run as an administrator.</span></span>
<span data-ttu-id="c1337-229">`Update-Help` Mostantól alapértelmezés szerint súgó, felhasználói hatókörbe tartozó mappába menti.</span><span class="sxs-lookup"><span data-stu-id="c1337-229">`Update-Help` now defaults to saving help to a user-scoped folder.</span></span>

### <a name="new-methodsproperties-on-pscustomobject"></a><span data-ttu-id="c1337-230">Új módszerek/tulajdonságai `PSCustomObject`</span><span class="sxs-lookup"><span data-stu-id="c1337-230">New methods/properties on `PSCustomObject`</span></span>

<span data-ttu-id="c1337-231">Köszönhetően @iSazonov, új módszerek és a Tulajdonságok hozzáadtunk `PSCustomObject`.</span><span class="sxs-lookup"><span data-stu-id="c1337-231">Thanks to @iSazonov, we've added new methods and properties to `PSCustomObject`.</span></span>
<span data-ttu-id="c1337-232">`PSCustomObject` most már tartalmaz egy `Count` / `Length` tulajdonságot, amely lehetővé teszi az elemek száma.</span><span class="sxs-lookup"><span data-stu-id="c1337-232">`PSCustomObject` now includes a `Count`/`Length` property that gives the number of items.</span></span>

<span data-ttu-id="c1337-233">Mindkét példa vissza `2` számának `PSCustomObjects` a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="c1337-233">Both of these examples return `2` as the number of `PSCustomObjects` in the collection.</span></span>

```powershell
@(
[pscustomobject]@{foo = '1'},
[pscustomobject]@{bar = '2' }).Length
```

```powershell
@(
[pscustomobject]@{foo = '1'},
[pscustomobject]@{bar = '2' }).Count
```

<span data-ttu-id="c1337-234">Ezt a munkát is tartalmaz `ForEach` és `Where` módszereket, amelyek lehetővé teszik, hogy működjön, és szűrheti a `PSCustomObject` elemek:</span><span class="sxs-lookup"><span data-stu-id="c1337-234">This work also includes `ForEach` and `Where` methods that allow you to operate and filter on `PSCustomObject` items:</span></span>

```powershell
@(
>> [pscustomobject]@{foo = 1},
>> [pscustomobject]@{foo = 2 }).ForEach({$_.foo+1})
```

```Output
2
3
```

```powershell
@(
>> [pscustomobject]@{foo = 1},
>> [pscustomobject]@{foo = 2 }).Where({$_.foo -gt 1})
```

```Output
foo
---
  2
```

### `Where-Object -Not`

<span data-ttu-id="c1337-235">Köszönhetően @SimonWahlin, tettünk elérhetővé a `-Not` paramétert `Where-Object`.</span><span class="sxs-lookup"><span data-stu-id="c1337-235">Thanks to @SimonWahlin, we've added the `-Not` parameter to `Where-Object`.</span></span>
<span data-ttu-id="c1337-236">Egy objektum, a folyamat meglétét, tulajdonság vagy egy NULL értékű vagy üres tulajdonság értéke most már szűrheti.</span><span class="sxs-lookup"><span data-stu-id="c1337-236">Now you can filter an object at the pipeline for the non-existence of a property, or a null/empty property value.</span></span>

<span data-ttu-id="c1337-237">Ez a parancs például minden olyan szolgáltatás, amely nincs definiálva a függő szolgáltatások adja vissza:</span><span class="sxs-lookup"><span data-stu-id="c1337-237">For example, this command returns all services that don't have any dependent services defined:</span></span>

```powershell
Get-Service | Where-Object -Not DependentServices
```

### <a name="new-modulemanifest-creates-a-bom-less-utf-8-document"></a><span data-ttu-id="c1337-238">`New-ModuleManifest` AJ nélküli UTF-8 dokumentum létrehozása</span><span class="sxs-lookup"><span data-stu-id="c1337-238">`New-ModuleManifest` creates a BOM-less UTF-8 document</span></span>

<span data-ttu-id="c1337-239">Adja meg az áthelyezés AJ nélküli UTF-8, a PowerShell 6.0-s, frissítettük a `New-ModuleManifest` parancsmaggal hozzon létre egy egyik UTF-16 helyett AJ nélküli UTF-8-dokumentumot.</span><span class="sxs-lookup"><span data-stu-id="c1337-239">Given our move to BOM-less UTF-8 in PowerShell 6.0, we've updated the `New-ModuleManifest` cmdlet to create a BOM-less UTF-8 document instead of a UTF-16 one.</span></span>

### <a name="conversions-from-psmethod-to-delegate"></a><span data-ttu-id="c1337-240">Átváltás a PSMethod delegálása</span><span class="sxs-lookup"><span data-stu-id="c1337-240">Conversions from PSMethod to Delegate</span></span>

<span data-ttu-id="c1337-241">Köszönhetően @powercode, mostantól támogatjuk a átalakítása egy `PSMethod` delegált be.</span><span class="sxs-lookup"><span data-stu-id="c1337-241">Thanks to @powercode, we now support the conversion of a `PSMethod` into a delegate.</span></span>
<span data-ttu-id="c1337-242">Ez lehetővé teszi, hogy többek között a megadásának `PSMethod` `[M]::DoubleStrLen` be delegált értékként `[M]::AggregateString`:</span><span class="sxs-lookup"><span data-stu-id="c1337-242">This allows you to do things like passing `PSMethod` `[M]::DoubleStrLen` as a delegate value into `[M]::AggregateString`:</span></span>

```powershell
class M {
    static [int] DoubleStrLen([string] $value) { return 2 * $value.Length }

    static [long] AggregateString([string[]] $values, [func[string, int]] $selector) {
        [long] $res = 0
        foreach($s in $values){
            $res += $selector.Invoke($s)
        }
        return $res
    }
}

[M]::AggregateString((gci).Name, [M]::DoubleStrLen)
```

<span data-ttu-id="c1337-243">További információ az ezt a módosítást, tekintse meg [PR #5287](https://github.com/PowerShell/PowerShell/pull/5287).</span><span class="sxs-lookup"><span data-stu-id="c1337-243">For more info on this change, check out [PR #5287](https://github.com/PowerShell/PowerShell/pull/5287).</span></span>

### <a name="standard-deviation-in-measure-object"></a><span data-ttu-id="c1337-244">Szórás `Measure-Object`</span><span class="sxs-lookup"><span data-stu-id="c1337-244">Standard deviation in `Measure-Object`</span></span>

<span data-ttu-id="c1337-245">Köszönhetően @CloudyDino, hozzáadtunk egy `StandardDeviation` tulajdonságot `Measure-Object`:</span><span class="sxs-lookup"><span data-stu-id="c1337-245">Thanks to @CloudyDino, we've added a `StandardDeviation` property to `Measure-Object`:</span></span>

```powershell
Get-Process | Measure-Object -Property CPU -AllStats
```

```Output
Count             : 308
Average           : 31.3720576298701
Sum               : 9662.59375
Maximum           : 4416.046875
Minimum           :
StandardDeviation : 264.389544720926
Property          : CPU
```

### `GetPfxCertificate -Password`

<span data-ttu-id="c1337-246">Köszönhetően @maybe-hello-world, `Get-PfxCertificate` most már rendelkezik a `Password` paraméter, amely egy `SecureString`.</span><span class="sxs-lookup"><span data-stu-id="c1337-246">Thanks to @maybe-hello-world, `Get-PfxCertificate` now has the `Password` parameter, which takes a `SecureString`.</span></span> <span data-ttu-id="c1337-247">Ez lehetővé teszi, hogy azt nem interaktív módon:</span><span class="sxs-lookup"><span data-stu-id="c1337-247">This allows you to use it non-interactively:</span></span>

```powershell
$certFile = '\\server\share\pwd-protected.pfx'
$certPass = Read-Host -AsSecureString -Prompt 'Enter the password for certificate: '

$certThumbPrint = (Get-PfxCertificate -FilePath $certFile -Password $certPass ).ThumbPrint
```

### <a name="removal-of-the-more-function"></a><span data-ttu-id="c1337-248">Eltávolítását a `more` függvény</span><span class="sxs-lookup"><span data-stu-id="c1337-248">Removal of the `more` function</span></span>

<span data-ttu-id="c1337-249">A múltban PowerShell tartalmazza a szükséges a Windows nevű függvény `more` , hogy a burkolt be `more.com`.</span><span class="sxs-lookup"><span data-stu-id="c1337-249">In the past, PowerShell shipped a function on Windows called `more` that wrapped `more.com`.</span></span>
<span data-ttu-id="c1337-250">Ez a függvény már el lett távolítva.</span><span class="sxs-lookup"><span data-stu-id="c1337-250">That function has now been removed.</span></span>

<span data-ttu-id="c1337-251">Emellett a `help` függvény módosítása, hogy `more.com` Windows vagy a rendszer alapértelmezett személyi hívó által megadott `$env:PAGER` nem Windows platformokon.</span><span class="sxs-lookup"><span data-stu-id="c1337-251">Also the `help` function changed to use `more.com` on Windows, or the system's default pager specified by `$env:PAGER` on non-Windows platforms.</span></span>

### <a name="cd-drivename-now-returns-users-to-the-current-working-directory-in-that-drive"></a><span data-ttu-id="c1337-252">`cd DriveName:` most adja vissza a felhasználók a meghajtón található az aktuális munkakönyvtár</span><span class="sxs-lookup"><span data-stu-id="c1337-252">`cd DriveName:` now returns users to the current working directory in that drive</span></span>

<span data-ttu-id="c1337-253">Korábban, a `Set-Location` vagy `cd` térjen vissza a felhasználók az alapértelmezett hely a meghajtó küldött PSDrive.</span><span class="sxs-lookup"><span data-stu-id="c1337-253">Previously, using `Set-Location` or `cd` to return to a PSDrive sent users to the default location for that drive.</span></span>

<span data-ttu-id="c1337-254">Köszönhetően @mcbobke, felhasználók ekkor elküldi az utolsó ismert aktuális munkakönyvtár az adott munkamenethez.</span><span class="sxs-lookup"><span data-stu-id="c1337-254">Thanks to @mcbobke, users are now sent to the last known current working directory for that session.</span></span>

### <a name="windows-powershell-type-accelerators"></a><span data-ttu-id="c1337-255">Windows PowerShell-típus megoldásgyorsítók</span><span class="sxs-lookup"><span data-stu-id="c1337-255">Windows PowerShell type accelerators</span></span>

<span data-ttu-id="c1337-256">A Windows PowerShellben amelyet hozzáadott a következő típusú megoldásgyorsítók könnyebb megfelelő adattípusukkal együtt működik:</span><span class="sxs-lookup"><span data-stu-id="c1337-256">In Windows PowerShell, we included the following type accelerators to make it easier to work with their respective types:</span></span>

- <span data-ttu-id="c1337-257">`[adsi]`: `System.DirectoryServices.DirectoryEntry`</span><span class="sxs-lookup"><span data-stu-id="c1337-257">`[adsi]`: `System.DirectoryServices.DirectoryEntry`</span></span>
- <span data-ttu-id="c1337-258">`[adsisearcher]`: `System.DirectoryServices.DirectorySearcher`</span><span class="sxs-lookup"><span data-stu-id="c1337-258">`[adsisearcher]`: `System.DirectoryServices.DirectorySearcher`</span></span>
- <span data-ttu-id="c1337-259">`[wmi]`: `System.Management.ManagementObject`</span><span class="sxs-lookup"><span data-stu-id="c1337-259">`[wmi]`: `System.Management.ManagementObject`</span></span>
- <span data-ttu-id="c1337-260">`[wmiclass]`: `System.Management.ManagementClass`</span><span class="sxs-lookup"><span data-stu-id="c1337-260">`[wmiclass]`: `System.Management.ManagementClass`</span></span>
- <span data-ttu-id="c1337-261">`[wmisearcher]`: `System.Management.ManagementObjectSearcher`</span><span class="sxs-lookup"><span data-stu-id="c1337-261">`[wmisearcher]`: `System.Management.ManagementObjectSearcher`</span></span>

<span data-ttu-id="c1337-262">A típus gyorsítók nem szereplő PowerShell 6-os, de a futó Windows PowerShell 6.1 lettek hozzáadva.</span><span class="sxs-lookup"><span data-stu-id="c1337-262">These type accelerators were not included in PowerShell 6, but have been added to PowerShell 6.1 running on Windows.</span></span>

<span data-ttu-id="c1337-263">Ezek a típusok lehetnek hasznosak könnyedén hozhat létre, amely az AD és a WMI-objektumok.</span><span class="sxs-lookup"><span data-stu-id="c1337-263">These types are useful in easily constructing AD and WMI objects.</span></span>

<span data-ttu-id="c1337-264">Ha például lekérdezheti, ha az LDAP:</span><span class="sxs-lookup"><span data-stu-id="c1337-264">For example, you can query using LDAP:</span></span>

```powershell
[adsi]'LDAP://CN=FooUse,OU=People,DC=contoso,DC=com'
```

<span data-ttu-id="c1337-265">Mindkét példa Win32_OperatingSystem CIM objektum létrehozása:</span><span class="sxs-lookup"><span data-stu-id="c1337-265">Both of these examples create a Win32_OperatingSystem CIM object:</span></span>

```powershell
[wmi]"win32_operatingsystem=@"
[wmiclass]"win32_operatingsystem"
```

```Output
SystemDirectory : C:\WINDOWS\system32
Organization    : Contoso IT
BuildNumber     : 18234
RegisteredUser  : Contoso Corp.
SerialNumber    : 12345-67890-ABCDE-F0123
Version         : 10.0.18234
```

### <a name="-lp-alias-for-all--literalpath-parameters"></a><span data-ttu-id="c1337-266">`-lp` az összes alias `-LiteralPath` paraméterek</span><span class="sxs-lookup"><span data-stu-id="c1337-266">`-lp` alias for all `-LiteralPath` parameters</span></span>

<span data-ttu-id="c1337-267">Köszönhetően @kvprasoon, hogy most már megvannak a paraméter-alias `-lp` minden a beépített PowerShell-parancsmagok, amelyek rendelkeznek egy `-LiteralPath` paraméter.</span><span class="sxs-lookup"><span data-stu-id="c1337-267">Thanks to @kvprasoon, we now have a parameter alias `-lp` for all the built-in PowerShell cmdlets that have a `-LiteralPath` parameter.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="c1337-268">Használhatatlanná tévő változásai</span><span class="sxs-lookup"><span data-stu-id="c1337-268">Breaking Changes</span></span>

### <a name="msi-based-installation-paths-on-windows"></a><span data-ttu-id="c1337-269">MSI-alapú telepítési elérési utak a Windows</span><span class="sxs-lookup"><span data-stu-id="c1337-269">MSI-based installation paths on Windows</span></span>

<span data-ttu-id="c1337-270">A Windows az MSI-csomag most telepíti a következő elérési utat:</span><span class="sxs-lookup"><span data-stu-id="c1337-270">On Windows, the MSI package now installs to the following path:</span></span>

- <span data-ttu-id="c1337-271">`$env:ProgramFiles\PowerShell\6\` 6.x stabil telepítéséhez</span><span class="sxs-lookup"><span data-stu-id="c1337-271">`$env:ProgramFiles\PowerShell\6\` for the stable installation of 6.x</span></span>
- <span data-ttu-id="c1337-272">`$env:ProgramFiles\PowerShell\6-preview\` az előzetes verzió telepítésének 6.x</span><span class="sxs-lookup"><span data-stu-id="c1337-272">`$env:ProgramFiles\PowerShell\6-preview\` for the preview installation of 6.x</span></span>

<span data-ttu-id="c1337-273">Ez a változás biztosítja, hogy a PowerShell Core, hogy a Microsoft Update frissíteni/szolgáltatója.</span><span class="sxs-lookup"><span data-stu-id="c1337-273">This change ensures that PowerShell Core can be updated/serviced by Microsoft Update.</span></span>

<span data-ttu-id="c1337-274">További információkért tekintse meg [PowerShell RFC0026](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0026-MSI-Installation-Path.md).</span><span class="sxs-lookup"><span data-stu-id="c1337-274">For more information, check out [PowerShell RFC0026](https://github.com/PowerShell/PowerShell-RFC/blob/master/5-Final/RFC0026-MSI-Installation-Path.md).</span></span>

### <a name="telemetry-can-only-be-disabled-with-an-environment-variable"></a><span data-ttu-id="c1337-275">Telemetria csak letiltható a környezeti változó</span><span class="sxs-lookup"><span data-stu-id="c1337-275">Telemetry can only be disabled with an environment variable</span></span>

<span data-ttu-id="c1337-276">A PowerShell Core alapvető telemetriai adatokat küld a Microsoftnak, amikor indul el.</span><span class="sxs-lookup"><span data-stu-id="c1337-276">PowerShell Core sends basic telemetry data to Microsoft when it is launched.</span></span> <span data-ttu-id="c1337-277">Az operációs rendszer neve, az operációs rendszer verziójára és a PowerShell-verzió szerepel.</span><span class="sxs-lookup"><span data-stu-id="c1337-277">The data includes the OS name, OS version, and PowerShell version.</span></span> <span data-ttu-id="c1337-278">Ezek az adatok jobb megértése érdekében a környezetekben, ahol a PowerShell szolgál, és lehetővé teszi számunkra, új funkciókkal és javításokkal rangsorolására tesz lehetővé.</span><span class="sxs-lookup"><span data-stu-id="c1337-278">This data allows us to better understand the environments where PowerShell is used and enables us to prioritize new features and fixes.</span></span>

<span data-ttu-id="c1337-279">Kapcsolnia ezt a telemetriát, állítsa be a környezeti változó `POWERSHELL_TELEMETRY_OPTOUT` való `true`, `yes`, vagy `1`.</span><span class="sxs-lookup"><span data-stu-id="c1337-279">To opt-out of this telemetry, set the environment variable `POWERSHELL_TELEMETRY_OPTOUT` to `true`, `yes`, or `1`.</span></span> <span data-ttu-id="c1337-280">Már nem támogatjuk a fájl törlésének `DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` telemetria letiltása.</span><span class="sxs-lookup"><span data-stu-id="c1337-280">We no longer support deletion of the file `DELETE_ME_TO_DISABLE_CONSOLEHOST_TELEMETRY` to disable telemetry.</span></span>

### <a name="disallowed-basic-auth-over-http-in-powershell-remoting-on-unix-platforms"></a><span data-ttu-id="c1337-281">Alapszintű hitelesítés PowerShell-táveléréssel a HTTP-kapcsolaton keresztül a UNIX rendszerű platformokon nem engedélyezett</span><span class="sxs-lookup"><span data-stu-id="c1337-281">Disallowed Basic Auth over HTTP in PowerShell Remoting on Unix platforms</span></span>

<span data-ttu-id="c1337-282">Letilthatja a nem titkosított forgalmat, a PowerShell-táveléréssel a UNIX rendszerű platformokon mostantól csak NTLM/egyeztetés vagy a HTTPS használatát.</span><span class="sxs-lookup"><span data-stu-id="c1337-282">To prevent the use of unencrypted traffic, PowerShell Remoting on Unix platforms now requires usage of NTLM/Negotiate or HTTPS.</span></span>

<span data-ttu-id="c1337-283">További információ ezekről a változásokról, tekintse meg [PR #6799](https://github.com/PowerShell/PowerShell/pull/6799).</span><span class="sxs-lookup"><span data-stu-id="c1337-283">For more information on these changes, check out [PR #6799](https://github.com/PowerShell/PowerShell/pull/6799).</span></span>

### <a name="removed-visualbasic-as-a-supported-language-in-add-type"></a><span data-ttu-id="c1337-284">Eltávolított `VisualBasic` egy támogatott nyelv az Add-Type</span><span class="sxs-lookup"><span data-stu-id="c1337-284">Removed `VisualBasic` as a supported language in Add-Type</span></span>

<span data-ttu-id="c1337-285">A múltban sikerült összeállíthatja a Visual Basic-kód használatával a `Add-Type` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="c1337-285">In the past, you could compile Visual Basic code using the `Add-Type` cmdlet.</span></span>
<span data-ttu-id="c1337-286">A Visual Basic a ritkán használt `Add-Type`.</span><span class="sxs-lookup"><span data-stu-id="c1337-286">Visual Basic was rarely used with `Add-Type`.</span></span> <span data-ttu-id="c1337-287">Ez a funkció PowerShell méretének csökkentésére eltávolítottuk.</span><span class="sxs-lookup"><span data-stu-id="c1337-287">We removed this feature to reduce the size of PowerShell.</span></span>

### <a name="cleaned-up-uses-of-commandtypesworkflow-and-workflowinfocleaned"></a><span data-ttu-id="c1337-288">Használati tisztítani `CommandTypes.Workflow` és `WorkflowInfoCleaned`</span><span class="sxs-lookup"><span data-stu-id="c1337-288">Cleaned up uses of `CommandTypes.Workflow` and `WorkflowInfoCleaned`</span></span>

<span data-ttu-id="c1337-289">További információ ezekről a változásokról, tekintse meg [PR #6708](https://github.com/PowerShell/PowerShell/pull/6708).</span><span class="sxs-lookup"><span data-stu-id="c1337-289">For more information on these changes, check out [PR #6708](https://github.com/PowerShell/PowerShell/pull/6708).</span></span>