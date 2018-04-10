# <a name="powershell-core-support-lifecycle"></a><span data-ttu-id="4c235-101">A PowerShell Core támogatási életciklusa</span><span class="sxs-lookup"><span data-stu-id="4c235-101">PowerShell Core Support Lifecycle</span></span>

<span data-ttu-id="4c235-102">PowerShell Core egy meghatározott készletét eszközök és összetevők rendszerrel szállított, telepített, és a Windows PowerShell külön kell beállítani.</span><span class="sxs-lookup"><span data-stu-id="4c235-102">PowerShell Core is a distinct set of tools and components that is shipped, installed, and configured separately from Windows PowerShell.</span></span>
<span data-ttu-id="4c235-103">Ezért a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy Windows Server licencelési szerződést.</span><span class="sxs-lookup"><span data-stu-id="4c235-103">Therefore, PowerShell Core is not included in the Windows 7/8.1/10 or Windows Server licensing agreements.</span></span>

<span data-ttu-id="4c235-104">Azonban esetében támogatott a PowerShell Core hagyományos a Microsoft támogatási szerződésből, beleértve a [Premier][], [Microsofttal kötött nagyvállalati szerződése][enterprise-agreement], és [Microsoft Szoftverbiztosítással][assurance].</span><span class="sxs-lookup"><span data-stu-id="4c235-104">However, PowerShell Core is supported under traditional Microsoft support agreements, including [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement], and [Microsoft Software Assurance][assurance].</span></span>
<span data-ttu-id="4c235-105">Is is kell fizetnie [tanácsadással][] a PowerShell Core által tervátalakítási a problémára vonatkozó támogatási kérelmet.</span><span class="sxs-lookup"><span data-stu-id="4c235-105">You can also pay for [assisted support][] for PowerShell Core by filing a support request for your problem.</span></span>

<span data-ttu-id="4c235-106">Is kínál [közösségi támogatás][] a Githubon, ahol egy problémát, a hiba, vagy a szolgáltatás kérése fájlt is.</span><span class="sxs-lookup"><span data-stu-id="4c235-106">We also offer [community support][] on GitHub where you can file an issue, bug, or feature request.</span></span>
<span data-ttu-id="4c235-107">Azt is megteheti, előfordulhat, hogy talál segítséget a Közösség más tagjai az általános [Microsoft Community][] vagy a Microsoft [PowerShell műszaki közösségi][].</span><span class="sxs-lookup"><span data-stu-id="4c235-107">Alternatively, you may find help from other members of the community on the general [Microsoft Community][] or the Microsoft [PowerShell Tech Community][].</span></span>
<span data-ttu-id="4c235-108">Azt garanciát nem létezik, hogy a probléma címzett vagy időben feloldva.</span><span class="sxs-lookup"><span data-stu-id="4c235-108">We offer no guarantee there that your issue will be addressed or resolved in a timely manner.</span></span>
<span data-ttu-id="4c235-109">Ha a probléma azonnali figyelmet igénylő, használja a hagyományos fizetős támogatási lehetőségeket.</span><span class="sxs-lookup"><span data-stu-id="4c235-109">If you have a problem that requires immediate attention, you should use the traditional, paid support options.</span></span>

## <a name="lifecycle-of-powershell-core"></a><span data-ttu-id="4c235-110">A PowerShell Core életciklusa</span><span class="sxs-lookup"><span data-stu-id="4c235-110">Lifecycle of PowerShell Core</span></span>

<span data-ttu-id="4c235-111">PowerShell Core bevezetni a [Microsoft Modern életciklusra vonatkozó szabályzata][modern].</span><span class="sxs-lookup"><span data-stu-id="4c235-111">PowerShell Core is adopting the [Microsoft Modern Lifecycle Policy][modern].</span></span>
<span data-ttu-id="4c235-112">Támogatási életciklus célja, hogy naprakészen tartsák az ügyfelek legújabb verziójú.</span><span class="sxs-lookup"><span data-stu-id="4c235-112">This support lifecycle is intended to keep customers up-to-date with the latest versions.</span></span>

<span data-ttu-id="4c235-113">PowerShell Core verzió 6.x ága frissíti körülbelül hat havonta (pl. 6.0, 6.1, 6.2, stb.)</span><span class="sxs-lookup"><span data-stu-id="4c235-113">The version 6.x branch of PowerShell Core will be updated approximately once every six months (e.g. 6.0, 6.1, 6.2, etc.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c235-114">Után minden új alverzió kiadásáról továbbra is megkapja az támogatási hat hónapban frissíteni kell.</span><span class="sxs-lookup"><span data-stu-id="4c235-114">You must update within six months after each new minor version release to continue receiving support.</span></span>

<span data-ttu-id="4c235-115">Például ha PowerShell Core 6.1 van szabadítva. július 1., 2018, várhatóan frissíteni a PowerShell Core 6.1 2019. január 1-jétől. támogatási fenntartásához.</span><span class="sxs-lookup"><span data-stu-id="4c235-115">For example, if PowerShell Core 6.1 is released on July 1st, 2018, you would be expected to update to PowerShell Core 6.1 by January 1st, 2019 to maintain support.</span></span>

![PowerShell Core fiókirodai életciklusa][lifecycle-chart]

<span data-ttu-id="4c235-117">A Modern életciklusra vonatkozó szabályzata is szükséges, hogy a Microsoft értesítést küldenek az ügyfelek 12 hónapon keresztül megszűnő támogatás (azaz a PowerShell Core) termék előtt.</span><span class="sxs-lookup"><span data-stu-id="4c235-117">The Modern Lifecycle Policy also requires that Microsoft give customers 12 months notice before discontinuing support for a product (i.e. PowerShell Core).</span></span>

<span data-ttu-id="4c235-118">Végül várhatóan PowerShell Core fogad el, a "hosszú távú karbantartási" megközelítést, ahol azt igényel csak karbantartása és biztonsági frissítések támogatását a meghatározott fiókirodai/verzióját 6.x belül.</span><span class="sxs-lookup"><span data-stu-id="4c235-118">Eventually, we expect PowerShell Core will adopt the "long-term servicing" approach where we would require only servicing and security updates to stay in support on a specific branch/version of 6.x.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4c235-119">Támogatott platformok</span><span class="sxs-lookup"><span data-stu-id="4c235-119">Supported platforms</span></span>

<span data-ttu-id="4c235-120">PowerShell Core hivatalosan a következő platformokon támogatott:</span><span class="sxs-lookup"><span data-stu-id="4c235-120">PowerShell Core is officially supported on the following platforms:</span></span>

* <span data-ttu-id="4c235-121">Windows 7, 8.1 és 10</span><span class="sxs-lookup"><span data-stu-id="4c235-121">Windows 7, 8.1, and 10</span></span>
* <span data-ttu-id="4c235-122">Windows Server 2008 R2, 2012 R2, 2016</span><span class="sxs-lookup"><span data-stu-id="4c235-122">Windows Server 2008 R2, 2012 R2, 2016</span></span>
* <span data-ttu-id="4c235-123">[Windows Server pontosvesszővel éves csatorna][semi-annual]</span><span class="sxs-lookup"><span data-stu-id="4c235-123">[Windows Server Semi-Annual Channel][semi-annual]</span></span>
* <span data-ttu-id="4c235-124">Ubuntu 14.04, 16.04 és 17.04</span><span class="sxs-lookup"><span data-stu-id="4c235-124">Ubuntu 14.04, 16.04, and 17.04</span></span>
* <span data-ttu-id="4c235-125">Debian 8.7 + és 9</span><span class="sxs-lookup"><span data-stu-id="4c235-125">Debian 8.7+, and 9</span></span>
* <span data-ttu-id="4c235-126">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="4c235-126">CentOS 7</span></span>
* <span data-ttu-id="4c235-127">Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="4c235-127">Red Hat Enterprise Linux 7</span></span>
* <span data-ttu-id="4c235-128">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="4c235-128">OpenSUSE 42.2</span></span>
* <span data-ttu-id="4c235-129">Fedora 25, 26</span><span class="sxs-lookup"><span data-stu-id="4c235-129">Fedora 25, 26</span></span>
* <span data-ttu-id="4c235-130">macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="4c235-130">macOS 10.12+</span></span>

<span data-ttu-id="4c235-131">A Közösség emellett hozzájárult csomagok a következő platformokat, de nem hivatalosan suppported:</span><span class="sxs-lookup"><span data-stu-id="4c235-131">Our community has also contributed packages for the following platforms, but they are not officially suppported:</span></span>

* <span data-ttu-id="4c235-132">Linux architektúrája</span><span class="sxs-lookup"><span data-stu-id="4c235-132">Arch Linux</span></span>
* <span data-ttu-id="4c235-133">Kali Linux</span><span class="sxs-lookup"><span data-stu-id="4c235-133">Kali Linux</span></span>
* <span data-ttu-id="4c235-134">AppImage (működik a több Linux platformon)</span><span class="sxs-lookup"><span data-stu-id="4c235-134">AppImage (works on multiple Linux platforms)</span></span>

## <a name="notes-on-licensing"></a><span data-ttu-id="4c235-135">Tudnivalók a licencelés</span><span class="sxs-lookup"><span data-stu-id="4c235-135">Notes on licensing</span></span>

<span data-ttu-id="4c235-136">PowerShell Core alatt megjelenik a [MIT licenccel][].</span><span class="sxs-lookup"><span data-stu-id="4c235-136">PowerShell Core is released under the [MIT license][].</span></span>
<span data-ttu-id="4c235-137">A licenc, és egy fizetős támogatási megállapodás hiányában, a felhasználók korlátozva [közösségi támogatás][].</span><span class="sxs-lookup"><span data-stu-id="4c235-137">Under this license, and in the absence of a paid support agreement, users are limited to [community support][].</span></span>
<span data-ttu-id="4c235-138">Közösségi-támogatással rendelkező Microsoft teszi nincs garancia válaszkészsége vagy javításokat.</span><span class="sxs-lookup"><span data-stu-id="4c235-138">With community support, Microsoft makes no guarantees of responsiveness or fixes.</span></span>

## <a name="windows-powershell-module"></a><span data-ttu-id="4c235-139">A Windows PowerShell-modul</span><span class="sxs-lookup"><span data-stu-id="4c235-139">Windows PowerShell Module</span></span>

<span data-ttu-id="4c235-140">Támogatja a PowerShell Core nem terjed ki a más termék modulok kivéve, ha az ilyen modulokhoz explicit módon támogatja a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="4c235-140">Support for PowerShell Core does not extend to other product modules unless those modules explicitly support PowerShell Core.</span></span>
<span data-ttu-id="4c235-141">Használata esetén például a `ActiveDirectory` modul részét képező, mert a Windows Server részét egy nem támogatott forgatókönyvet.</span><span class="sxs-lookup"><span data-stu-id="4c235-141">For example, using the `ActiveDirectory` module that ships as part of Windows Server is an unsupported scenario.</span></span>

<span data-ttu-id="4c235-142">Előfordulhat azonban, modulokat, amelyek kifejezetten nem támogatják a PowerShell Core kompatibilis bizonyos esetekben.</span><span class="sxs-lookup"><span data-stu-id="4c235-142">However, modules that do not explicitly support PowerShell Core may be compatible in some cases.</span></span>
<span data-ttu-id="4c235-143">Telepítse a [`WindowsPSModulePath`][] modul, fűzze hozzá a Windows PowerShell `PSModulePath` a PowerShell képességének `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="4c235-143">By installing the [`WindowsPSModulePath`][] module, you can append the Windows PowerShell `PSModulePath` to your PowerShell Core `PSModulePath`.</span></span>

<span data-ttu-id="4c235-144">Először telepítse a `WindowsPSModulePath` a PowerShell-galériából modul:</span><span class="sxs-lookup"><span data-stu-id="4c235-144">First, install the `WindowsPSModulePath` module from the PowerShell Gallery:</span></span>

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

<span data-ttu-id="4c235-145">Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` parancsmaggal adja hozzá a Windows PowerShell `PSModulePath` képességének PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4c235-145">After installing this module, run the `Add-WindowsPSModulePath` cmdlet to add the Windows PowerShell `PSModulePath` to PowerShell Core:</span></span>

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[közösségi támogatás]: https://github.com/powershell/powershell/issues
[community support]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[PowerShell műszaki közösségi]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[tanácsadással]: https://support.microsoft.com/assistedsupportproducts
[assisted support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenccel]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/