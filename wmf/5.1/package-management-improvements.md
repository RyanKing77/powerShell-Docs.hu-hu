---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
contributor: jianyunt, quoctruong
title: A WMF 5.1 csomagkezelés fejlesztései
ms.openlocfilehash: 30ef59ed9dc0d56636d85cc6e53523a9a73963a4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62055615"
---
# <a name="improvements-to-package-management-in-wmf-51"></a><span data-ttu-id="dfde5-103">A WMF 5.1 csomagkezelés fejlesztései</span><span class="sxs-lookup"><span data-stu-id="dfde5-103">Improvements to Package Management in WMF 5.1</span></span>

## <a name="improvements-in-packagemanagement"></a><span data-ttu-id="dfde5-104">A PackageManagement fejlesztései</span><span class="sxs-lookup"><span data-stu-id="dfde5-104">Improvements in PackageManagement</span></span>

<span data-ttu-id="dfde5-105">A WMF 5.1 a javításokat az alábbiak:</span><span class="sxs-lookup"><span data-stu-id="dfde5-105">The following are the fixes made in the WMF 5.1:</span></span>

### <a name="version-alias"></a><span data-ttu-id="dfde5-106">Version Alias</span><span class="sxs-lookup"><span data-stu-id="dfde5-106">Version Alias</span></span>

<span data-ttu-id="dfde5-107">**A forgatókönyv**: 1.0-s és a egy csomagot, P1, a rendszerre telepített 2.0-s verziót használja-e, és el szeretné távolítani az 1.0-s verzióját, futtatná `Uninstall-Package -Name P1 -Version 1.0` és a parancsmag futtatása után el kell távolítani az 1.0-s verzióját.</span><span class="sxs-lookup"><span data-stu-id="dfde5-107">**Scenario**: If you have version 1.0 and 2.0 of a package, P1, installed on your system, and you want to uninstall version 1.0, you would run `Uninstall-Package -Name P1 -Version 1.0` and expect version 1.0 to be uninstalled after running the cmdlet.</span></span> <span data-ttu-id="dfde5-108">Azonban az eredmény a 2.0-s verziójának beolvasása eltávolítja.</span><span class="sxs-lookup"><span data-stu-id="dfde5-108">However the result is that version 2.0 gets uninstalled.</span></span>

<span data-ttu-id="dfde5-109">Ez akkor fordul elő, mert a `-Version` paraméter egy aliast a `-MinimumVersion` paraméter.</span><span class="sxs-lookup"><span data-stu-id="dfde5-109">This occurs because the `-Version` parameter is an alias of the `-MinimumVersion` parameter.</span></span> <span data-ttu-id="dfde5-110">A PackageManagement az 1.0-s verziójával minősített csomagot keres, ha a legújabb verziót adja vissza.</span><span class="sxs-lookup"><span data-stu-id="dfde5-110">When PackageManagement is looking for a qualified package with the minimum version of 1.0, it returns the latest version.</span></span> <span data-ttu-id="dfde5-111">Ez a viselkedés a normál esetben elvárható, hiszen a keresés, a legújabb verzióra általában a kívánt eredményt.</span><span class="sxs-lookup"><span data-stu-id="dfde5-111">This behavior is expected in normal cases because finding the latest version is usually the desired result.</span></span> <span data-ttu-id="dfde5-112">Azonban ez nem vonatkozik a `Uninstall-Package` eset.</span><span class="sxs-lookup"><span data-stu-id="dfde5-112">However, it should not apply to the `Uninstall-Package` case.</span></span>

<span data-ttu-id="dfde5-113">**Megoldás**: eltávolított `-Version` alias teljes egészében a PackageManagement (más néven)</span><span class="sxs-lookup"><span data-stu-id="dfde5-113">**Solution**:removed `-Version` alias entirely in PackageManagement (a.k.a.</span></span> <span data-ttu-id="dfde5-114">OneGet), és a PowerShellGet.</span><span class="sxs-lookup"><span data-stu-id="dfde5-114">OneGet) and PowerShellGet.</span></span>

### <a name="multiple-prompts-for-bootstrapping-the-nuget-provider"></a><span data-ttu-id="dfde5-115">A NuGet-szolgáltató rendszerindításra több utasításokat</span><span class="sxs-lookup"><span data-stu-id="dfde5-115">Multiple prompts for bootstrapping the NuGet provider</span></span>

<span data-ttu-id="dfde5-116">**A forgatókönyv**: Futtatásakor `Find-Module` vagy `Install-Module` vagy más PackageManagement-parancsmagok a számítógép első elindításakor a PackageManagement próbál meg a NuGet-szolgáltató elindíthat.</span><span class="sxs-lookup"><span data-stu-id="dfde5-116">**Scenario**: When you run `Find-Module` or `Install-Module` or other PackageManagement cmdlets on your computer for the first time, PackageManagement tries to bootstrap the NuGet provider.</span></span> <span data-ttu-id="dfde5-117">Ezt hajtja végre, mert a PowerShellGet szolgáltató is használ a NuGet-szolgáltató letöltése a PowerShell-modulok.</span><span class="sxs-lookup"><span data-stu-id="dfde5-117">It does this because the PowerShellGet provider also uses the NuGet provider to download PowerShell modules.</span></span> <span data-ttu-id="dfde5-118">A PackageManagement majd felszólítja a felhasználót, telepítse a NuGet-szolgáltató engedélyt.</span><span class="sxs-lookup"><span data-stu-id="dfde5-118">PackageManagement then prompts the user for permission to install the NuGet provider.</span></span> <span data-ttu-id="dfde5-119">Miután a felhasználó az "Igen", a rendszerindításra választja, a NuGet-szolgáltató legújabb verzióját telepíti.</span><span class="sxs-lookup"><span data-stu-id="dfde5-119">After the user selects "yes" for the bootstrapping, the latest version of the NuGet provider will be installed.</span></span>

<span data-ttu-id="dfde5-120">Azonban bizonyos esetekben egy régi verziója NuGet-szolgáltató ugyanarra a számítógépre telepítve, a régebbi verzió néha lekérdezi betöltötte először (Ez a versenyhelyzet PackageManagement) PowerShell-munkamenetbe.</span><span class="sxs-lookup"><span data-stu-id="dfde5-120">However, in some cases, when you have an old version of NuGet provider installed on your computer, the older version of NuGet sometimes gets loaded first into the PowerShell session (that's the race condition in PackageManagement).</span></span> <span data-ttu-id="dfde5-121">Azonban az PowerShellGet a NuGet-szolgáltató használatát újabb verziója szükséges, így a PowerShellGet PackageManagement újra elindíthat a NuGet-szolgáltató.</span><span class="sxs-lookup"><span data-stu-id="dfde5-121">However PowerShellGet requires the later version of the NuGet provider to work, so PowerShellGet asks PackageManagement to bootstrap the NuGet provider again.</span></span> <span data-ttu-id="dfde5-122">Ennek eredményeképpen a NuGet-szolgáltató rendszerindításra több utasításokat.</span><span class="sxs-lookup"><span data-stu-id="dfde5-122">This results in multiple prompts for bootstrapping the NuGet provider.</span></span>

<span data-ttu-id="dfde5-123">**Megoldás**: PackageManagement WMF5.1, betölti a NuGet-szolgáltató rendszerindításra több utasításokat elkerülése érdekében a NuGet-szolgáltató legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="dfde5-123">**Solution**: In WMF5.1, PackageManagement loads the latest version of the NuGet provider to avoid multiple prompts for bootstrapping the NuGet provider.</span></span>

<span data-ttu-id="dfde5-124">Ezt a problémát úgy is működhetnek (NuGet-Anycpu.exe) NuGet-szolgáltató régebbi verzióját manuálisan törlésével, ha a probléma $env létezik: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies</span><span class="sxs-lookup"><span data-stu-id="dfde5-124">You could also work around this issue by manually deleting the old version of the NuGet provider (NuGet-Anycpu.exe) if exists from $env:ProgramFiles\PackageManagement\ProviderAssemblies $env:LOCALAPPDATA\PackageManagement\ProviderAssemblies</span></span>


### <a name="support-for-packagemanagement-on-computers-with-intranet-access-only"></a><span data-ttu-id="dfde5-125">A PackageManagement a számítógépeken csak az intranetes hozzáférés támogatása</span><span class="sxs-lookup"><span data-stu-id="dfde5-125">Support for PackageManagement on computers with Intranet access only</span></span>

<span data-ttu-id="dfde5-126">**A forgatókönyv**: A vállalati forgatókönyvhöz az ember dolgozik környezet alapján, ha ott nem nincs Internet-hozzáférést, de az intranetes csak.</span><span class="sxs-lookup"><span data-stu-id="dfde5-126">**Scenario**: For the enterprise scenario, people are working under an environment where there is no Internet access but Intranet only.</span></span> <span data-ttu-id="dfde5-127">A PackageManagement ebben az esetben a WMF 5.0 nem támogat.</span><span class="sxs-lookup"><span data-stu-id="dfde5-127">PackageManagement did not support this case in WMF 5.0.</span></span>

<span data-ttu-id="dfde5-128">**A forgatókönyv**: A WMF 5.0-s PackageManagement nem támogatták a csak Intranet (de nem az interneten) rendelkező számítógépek hozzáférést.</span><span class="sxs-lookup"><span data-stu-id="dfde5-128">**Scenario**: In WMF 5.0, PackageManagement did not support computers that have only Intranet (but not Internet) access.</span></span>

<span data-ttu-id="dfde5-129">**Megoldás**: A WMF 5.1 hajtsa végre ezeket a lépéseket, hogy az intranetes számítógépekhez PackageManagement használatára:</span><span class="sxs-lookup"><span data-stu-id="dfde5-129">**Solution**: In WMF 5.1, you can follow these steps to allow Intranet computers to use PackageManagement:</span></span>

1. <span data-ttu-id="dfde5-130">Töltse le a NuGet-szolgáltató használatával egy másik számítógépre, az internetkapcsolattal rendelkező `Install-PackageProvider -Name NuGet`.</span><span class="sxs-lookup"><span data-stu-id="dfde5-130">Download the NuGet provider using another computer that has an Internet connection by using `Install-PackageProvider -Name NuGet`.</span></span>

2. <span data-ttu-id="dfde5-131">Keresse meg a NuGet-szolgáltató szakaszban `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget` vagy `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.</span><span class="sxs-lookup"><span data-stu-id="dfde5-131">Find the NuGet provider under either `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget`  or  `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.</span></span>

3. <span data-ttu-id="dfde5-132">A bináris fájlok másolását egy mappát vagy hálózati megosztási helyre, amely az intranetes számítógép eléréséhez, és telepítse a NuGet-szolgáltató `Install-PackageProvider -Name NuGet -Source <Path to folder>`.</span><span class="sxs-lookup"><span data-stu-id="dfde5-132">Copy the binaries to a folder or network share location that the Intranet computer can access, and then install the NuGet provider with `Install-PackageProvider -Name NuGet -Source <Path to folder>`.</span></span>


### <a name="event-logging-improvements"></a><span data-ttu-id="dfde5-133">Esemény naplózása fejlesztései</span><span class="sxs-lookup"><span data-stu-id="dfde5-133">Event logging improvements</span></span>

<span data-ttu-id="dfde5-134">Csomagokat telepíteni, ha módosítja a számítógép állapotát.</span><span class="sxs-lookup"><span data-stu-id="dfde5-134">When you install packages, you are changing the state of the computer.</span></span> <span data-ttu-id="dfde5-135">A WMF 5.1-es, a PackageManagement mostantól rögzíti eseményeket, a Windows eseménynaplójában keresse meg a `Install-Package`, `Uninstall-Package`, és `Save-Package` tevékenységeket.</span><span class="sxs-lookup"><span data-stu-id="dfde5-135">In WMF 5.1, PackageManagement now logs events to the Windows event log for `Install-Package`, `Uninstall-Package`, and `Save-Package` activities.</span></span> <span data-ttu-id="dfde5-136">Az Eseménynapló rendszer ugyanaz, mint a PowerShell-lel, azt jelenti, `Microsoft-Windows-PowerShell, Operational`.</span><span class="sxs-lookup"><span data-stu-id="dfde5-136">The Event log  is the same as for PowerShell, that is, `Microsoft-Windows-PowerShell, Operational`.</span></span>

### <a name="support-for-basic-authentication"></a><span data-ttu-id="dfde5-137">Alapszintű hitelesítés támogatása</span><span class="sxs-lookup"><span data-stu-id="dfde5-137">Support for basic authentication</span></span>

<span data-ttu-id="dfde5-138">A WMF 5.1-es a PackageManagement támogatja a Keresés és a egy adattárból, amely egyszerű hitelesítés szükséges csomagok telepítése.</span><span class="sxs-lookup"><span data-stu-id="dfde5-138">In WMF 5.1, PackageManagement supports finding and installing packages from a repository that requires basic authentication.</span></span> <span data-ttu-id="dfde5-139">A hitelesítő adatokat, megadhatja a `Find-Package` és `Install-Package` parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="dfde5-139">You can supply your credentials to the `Find-Package` and `Install-Package` cmdlets.</span></span> <span data-ttu-id="dfde5-140">Például:</span><span class="sxs-lookup"><span data-stu-id="dfde5-140">For example:</span></span>

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```

### <a name="support-for-using-packagemanagement-behind-a-proxy"></a><span data-ttu-id="dfde5-141">PackageManagement használatával a rendszer proxy mögött támogatása</span><span class="sxs-lookup"><span data-stu-id="dfde5-141">Support for using PackageManagement behind a proxy</span></span>

<span data-ttu-id="dfde5-142">A WMF 5.1-es, a PackageManagement mostantól új proxy paraméter szükséges `-ProxyCredential` és `-Proxy`.</span><span class="sxs-lookup"><span data-stu-id="dfde5-142">In WMF 5.1, PackageManagement now takes new proxy parameters `-ProxyCredential` and `-Proxy`.</span></span> <span data-ttu-id="dfde5-143">Ezeket a paramétereket használja, megadhatja a proxykiszolgáló URL-cím és a PackageManagement-parancsmagok hitelesítő adatait.</span><span class="sxs-lookup"><span data-stu-id="dfde5-143">Using these parameters, you can specify the proxy URL and credentials to PackageManagement cmdlets.</span></span> <span data-ttu-id="dfde5-144">Alapértelmezés szerint systémová nastavení proxy serveru szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="dfde5-144">By default, system proxy settings are used.</span></span> <span data-ttu-id="dfde5-145">Például:</span><span class="sxs-lookup"><span data-stu-id="dfde5-145">For example:</span></span>

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```
