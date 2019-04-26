---
title: A PowerShell Core támogatási életciklusa
description: A PowerShell Core támogatási szabályzatok betartatását
ms.date: 08/06/2018
ms.openlocfilehash: 178e5c43520f9a392ca219b9f785eb18b1ec5436
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086974"
---
# <a name="powershell-core-support-lifecycle"></a><span data-ttu-id="6abbb-103">A PowerShell Core támogatási életciklusa</span><span class="sxs-lookup"><span data-stu-id="6abbb-103">PowerShell Core Support Lifecycle</span></span>

<span data-ttu-id="6abbb-104">A PowerShell Core a meghatározott készletét eszközök és -összetevők, amely tartalmazza a szükséges, telepítve van, és külön konfigurálni a Windows Powershellből.</span><span class="sxs-lookup"><span data-stu-id="6abbb-104">PowerShell Core is a distinct set of tools and components that is shipped, installed, and configured separately from Windows PowerShell.</span></span>
<span data-ttu-id="6abbb-105">Így a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy Windows Server licencelési megállapodások.</span><span class="sxs-lookup"><span data-stu-id="6abbb-105">So, PowerShell Core is not included in the Windows 7/8.1/10 or Windows Server licensing agreements.</span></span>

<span data-ttu-id="6abbb-106">Azonban a PowerShell Core a hagyományos Microsoft támogatási szerződés, beleértve a támogatott [A Premier szintű][], [Microsoft Enterprise-megállapodások][enterprise-agreement], és [Microsoft frissítési garanciával rendelkező][assurance].</span><span class="sxs-lookup"><span data-stu-id="6abbb-106">However, PowerShell Core is supported under traditional Microsoft support agreements, including [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement], and [Microsoft Software Assurance][assurance].</span></span>
<span data-ttu-id="6abbb-107">Is fizethet a szolgáltatásért [tanácsadással][] a PowerShell Core ügyfélszolgálatunknak küldött támogatási kérelmet a problémát.</span><span class="sxs-lookup"><span data-stu-id="6abbb-107">You can also pay for [assisted support][] for PowerShell Core by filing a support request for your problem.</span></span>

## <a name="community-support"></a><span data-ttu-id="6abbb-108">Közösségi támogatás</span><span class="sxs-lookup"><span data-stu-id="6abbb-108">Community Support</span></span>

<span data-ttu-id="6abbb-109">Emellett [közösségi támogatás][] a Githubon, ahol egy problémát, programhiba vagy funkcióigénylés fájlt is.</span><span class="sxs-lookup"><span data-stu-id="6abbb-109">We also offer [community support][] on GitHub where you can file an issue, bug, or feature request.</span></span>
<span data-ttu-id="6abbb-110">Ezenkívül előfordulhat, a Közösség más tagjai segítséget az általános [A Microsoft Community][] vagy a Microsoft [PowerShell technikai Közösség][].</span><span class="sxs-lookup"><span data-stu-id="6abbb-110">Also, you may find help from other members of the community on the general [Microsoft Community][] or the Microsoft [PowerShell Tech Community][].</span></span>
<span data-ttu-id="6abbb-111">Nincs garancia van, hogy a Közösség cím vagy a probléma megoldásához időben nem kínál.</span><span class="sxs-lookup"><span data-stu-id="6abbb-111">We offer no guarantee there that the community will address or resolve your issue in a timely manner.</span></span>
<span data-ttu-id="6abbb-112">Ha azonnali figyelmet igénylő problémával rendelkezik, használja a hagyományos, fizetős támogatási lehetőségek.</span><span class="sxs-lookup"><span data-stu-id="6abbb-112">If you have a problem that requires immediate attention, you should use the traditional, paid support options.</span></span>

## <a name="lifecycle-of-powershell-core"></a><span data-ttu-id="6abbb-113">A PowerShell Core élettartama</span><span class="sxs-lookup"><span data-stu-id="6abbb-113">Lifecycle of PowerShell Core</span></span>

<span data-ttu-id="6abbb-114">A PowerShell Core kíván bevezetni a [Microsoft Modern életciklus-szabályzat][modern].</span><span class="sxs-lookup"><span data-stu-id="6abbb-114">PowerShell Core is adopting the [Microsoft Modern Lifecycle Policy][modern].</span></span>
<span data-ttu-id="6abbb-115">A támogatási életciklusa célja, hogy az ügyfelek naprakészen tartása a legújabb verzióra.</span><span class="sxs-lookup"><span data-stu-id="6abbb-115">This support lifecycle is intended to keep customers up-to-date with the latest versions.</span></span>

<span data-ttu-id="6abbb-116">A PowerShell Core verzió 6.x ága körülbelül hat havonta frissül (példák: 6.0-s, 6.1, 6.2, stb.)</span><span class="sxs-lookup"><span data-stu-id="6abbb-116">The version 6.x branch of PowerShell Core will be updated approximately once every six months (examples: 6.0, 6.1, 6.2, etc.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6abbb-117">Miután minden egyes új alverzió kiadási támogatás folytatásához hat hónapon belül kell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="6abbb-117">You must update within six months after each new minor version release to continue receiving support.</span></span>

<span data-ttu-id="6abbb-118">Például ha a PowerShell Core 6.1-es kiadás dátuma: 2018. július 1., elvárják, hogy a PowerShell Core 6.1-es verzióját 2019. január 1. támogatás frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="6abbb-118">For example, if PowerShell Core 6.1 is released on July 1, 2018, you would be expected to update to PowerShell Core 6.1 by January 1, 2019 to maintain support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6abbb-119">Minden egyes új javítás verziója engedje támogatás folytatásához követő 30 napon belül kell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="6abbb-119">You must update within 30 days after each new patch version release to continue receiving support.</span></span>

<span data-ttu-id="6abbb-120">Például ha futtatja a PowerShell Core 6.1-es és 6.1.3 fel lett oldva, a 2019. február 19., akkor elvárják, hogy a PowerShell Core 6.1.3 által 2019. március 21., amely támogatás a kiadása után 30 nappal való frissítéséhez.</span><span class="sxs-lookup"><span data-stu-id="6abbb-120">For example, If you are running PowerShell Core 6.1 and 6.1.3 was released on February 19, 2019, you would be expected to update to PowerShell Core 6.1.3 by March 21, 2019, which is 30 days after the release to maintain support.</span></span>
<span data-ttu-id="6abbb-121">Ha bármely javításokat szükség talál, a javítások a következő összegző frissítés elérhető lesz.</span><span class="sxs-lookup"><span data-stu-id="6abbb-121">If any fixes are found to be required, the fixes will be released in our next cumulative update.</span></span>

![A PowerShell Core ág életciklusa][lifecycle-chart]

<span data-ttu-id="6abbb-123">A Modern életciklus-szabályzat is megköveteli, hogy a Microsoft értesítést ügyfelek 12 hónapig előtt megszűnő támogatás a termék (azaz a PowerShell Core).</span><span class="sxs-lookup"><span data-stu-id="6abbb-123">The Modern Lifecycle Policy also requires that Microsoft give customers 12 months notice before discontinuing support for a product (that is, PowerShell Core).</span></span>

<span data-ttu-id="6abbb-124">Idővel várhatóan a alkalmazni a PowerShell Core, a "hosszú távú karbantartási" megközelítést.</span><span class="sxs-lookup"><span data-stu-id="6abbb-124">Eventually, we expect PowerShell Core will adopt the "long-term servicing" approach.</span></span>
<span data-ttu-id="6abbb-125">A karbantartási módszert használja, az csak karbantartási és biztonsági frissítések belül egy adott ág/verzióját 6.x támogatását lenne szükség van.</span><span class="sxs-lookup"><span data-stu-id="6abbb-125">In this servicing approach, we would require only servicing and security updates to stay in support on a specific branch/version of 6.x.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="6abbb-126">Támogatott platformok</span><span class="sxs-lookup"><span data-stu-id="6abbb-126">Supported platforms</span></span>

<span data-ttu-id="6abbb-127">Az alábbi táblázat segítségével tekintse meg a platform a verzióját használja a PowerShell Core hivatalosan támogatott.</span><span class="sxs-lookup"><span data-stu-id="6abbb-127">The following table to see what platform the version of PowerShell Core you are using is officially supported.</span></span>

<span data-ttu-id="6abbb-128">Közösségünkhöz is hozzájárult a csomagokat, az egyes platformok esetében, de ez nem hivatalosan támogatott.</span><span class="sxs-lookup"><span data-stu-id="6abbb-128">Our community has also contributed packages for some platforms, but they are not officially supported.</span></span>
<span data-ttu-id="6abbb-129">Ezek a csomagok vannak megjelölve `Community` a táblában.</span><span class="sxs-lookup"><span data-stu-id="6abbb-129">These packages are marked as `Community` in the table.</span></span>

<span data-ttu-id="6abbb-130">Felsorolt platformok `Experimental` hivatalosan nem támogatottak, de a Kísérletezési és visszajelzés elérhető.</span><span class="sxs-lookup"><span data-stu-id="6abbb-130">Platforms listed as `Experimental` are not officially supported, but are available for experimentation and feedback.</span></span>

|                                                   | <span data-ttu-id="6abbb-131">6.1</span><span class="sxs-lookup"><span data-stu-id="6abbb-131">6.1</span></span>         | <span data-ttu-id="6abbb-132">6.2</span><span class="sxs-lookup"><span data-stu-id="6abbb-132">6.2</span></span>         |
|---------------------------------------------------|:-----------:|:-----------:|
| <span data-ttu-id="6abbb-133">Windows 7, 8.1 és 10</span><span class="sxs-lookup"><span data-stu-id="6abbb-133">Windows 7, 8.1, and 10</span></span>                            | <span data-ttu-id="6abbb-134">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-134">Supported</span></span>   | <span data-ttu-id="6abbb-135">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-135">Supported</span></span>   |
| <span data-ttu-id="6abbb-136">Windows Server 2008 R2, 2012 R2, 2016</span><span class="sxs-lookup"><span data-stu-id="6abbb-136">Windows Server 2008 R2, 2012 R2, 2016</span></span>             | <span data-ttu-id="6abbb-137">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-137">Supported</span></span>   | <span data-ttu-id="6abbb-138">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-138">Supported</span></span>   |
| <span data-ttu-id="6abbb-139">[A Windows Server féléves csatorna][semi-annual]</span><span class="sxs-lookup"><span data-stu-id="6abbb-139">[Windows Server Semi-Annual Channel][semi-annual]</span></span> | <span data-ttu-id="6abbb-140">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-140">Supported</span></span>   | <span data-ttu-id="6abbb-141">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-141">Supported</span></span>   |
| <span data-ttu-id="6abbb-142">Ubuntu 16.04 és 18.04</span><span class="sxs-lookup"><span data-stu-id="6abbb-142">Ubuntu 16.04 and 18.04</span></span>                            | <span data-ttu-id="6abbb-143">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-143">Supported</span></span>   | <span data-ttu-id="6abbb-144">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-144">Supported</span></span>   |
| <span data-ttu-id="6abbb-145">Ubuntu 18.10 (keresztül Számértékekhez igazodnak, a csomag)</span><span class="sxs-lookup"><span data-stu-id="6abbb-145">Ubuntu 18.10 (via Snap Package)</span></span>                   | <span data-ttu-id="6abbb-146">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-146">Community</span></span>   | <span data-ttu-id="6abbb-147">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-147">Community</span></span>   |
| <span data-ttu-id="6abbb-148">Debian 9</span><span class="sxs-lookup"><span data-stu-id="6abbb-148">Debian 9</span></span>                                          | <span data-ttu-id="6abbb-149">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-149">Supported</span></span>   | <span data-ttu-id="6abbb-150">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-150">Supported</span></span>   |
| <span data-ttu-id="6abbb-151">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="6abbb-151">CentOS 7</span></span>                                          | <span data-ttu-id="6abbb-152">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-152">Supported</span></span>   | <span data-ttu-id="6abbb-153">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-153">Supported</span></span>   |
| <span data-ttu-id="6abbb-154">Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="6abbb-154">Red Hat Enterprise Linux 7</span></span>                        | <span data-ttu-id="6abbb-155">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-155">Supported</span></span>   | <span data-ttu-id="6abbb-156">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-156">Supported</span></span>   |
| <span data-ttu-id="6abbb-157">openSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="6abbb-157">openSUSE 42.3</span></span>                                     | <span data-ttu-id="6abbb-158">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-158">Supported</span></span>   | <span data-ttu-id="6abbb-159">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-159">Supported</span></span>   |
| <span data-ttu-id="6abbb-160">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="6abbb-160">Fedora 28</span></span>                                         | <span data-ttu-id="6abbb-161">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-161">Supported</span></span>   | <span data-ttu-id="6abbb-162">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-162">Supported</span></span>   |
| <span data-ttu-id="6abbb-163">macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="6abbb-163">macOS 10.12+</span></span>                                      | <span data-ttu-id="6abbb-164">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-164">Supported</span></span>   | <span data-ttu-id="6abbb-165">Támogatott</span><span class="sxs-lookup"><span data-stu-id="6abbb-165">Supported</span></span>   |
| <span data-ttu-id="6abbb-166">Arch</span><span class="sxs-lookup"><span data-stu-id="6abbb-166">Arch</span></span>                                              | <span data-ttu-id="6abbb-167">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-167">Community</span></span>   | <span data-ttu-id="6abbb-168">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-168">Community</span></span>   |
| <span data-ttu-id="6abbb-169">Raspbian</span><span class="sxs-lookup"><span data-stu-id="6abbb-169">Raspbian</span></span>                                          | <span data-ttu-id="6abbb-170">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-170">Community</span></span>   | <span data-ttu-id="6abbb-171">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-171">Community</span></span>   |
| <span data-ttu-id="6abbb-172">Kali</span><span class="sxs-lookup"><span data-stu-id="6abbb-172">Kali</span></span>                                              | <span data-ttu-id="6abbb-173">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-173">Community</span></span>   | <span data-ttu-id="6abbb-174">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-174">Community</span></span>   |
| <span data-ttu-id="6abbb-175">AppImage (több Linux platformon működik)</span><span class="sxs-lookup"><span data-stu-id="6abbb-175">AppImage  (works on multiple Linux platforms)</span></span>     | <span data-ttu-id="6abbb-176">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-176">Community</span></span>   | <span data-ttu-id="6abbb-177">Közösségi</span><span class="sxs-lookup"><span data-stu-id="6abbb-177">Community</span></span>   |
| [<span data-ttu-id="6abbb-178">Oszlopokhoz illesztés csomag</span><span class="sxs-lookup"><span data-stu-id="6abbb-178">Snap Package</span></span>](https://snapcraft.io/powershell)   | <span data-ttu-id="6abbb-179">Lásd a megjegyzést</span><span class="sxs-lookup"><span data-stu-id="6abbb-179">See note</span></span>    | <span data-ttu-id="6abbb-180">Lásd a megjegyzést</span><span class="sxs-lookup"><span data-stu-id="6abbb-180">See note</span></span>    |

> [!NOTE]
> <span data-ttu-id="6abbb-181">Oszlopokhoz illesztés csomagok támogatottak ugyanaz, mint a terjesztési futtat a csomagot.</span><span class="sxs-lookup"><span data-stu-id="6abbb-181">Snap packages are supported the same as the distribution you are running the package on.</span></span>

## <a name="powershell-release-end-of-life"></a><span data-ttu-id="6abbb-182">PowerShell kiadás végéhez közeledik</span><span class="sxs-lookup"><span data-stu-id="6abbb-182">PowerShell release end of life</span></span>

<span data-ttu-id="6abbb-183">Alapján [a PowerShell Core életciklus](#lifecycle-of-powershell-core), az alábbi táblázat tartalmazza a dátumokat, amikor különböző kiadás már nem lesz támogatott.</span><span class="sxs-lookup"><span data-stu-id="6abbb-183">Based on [Lifecycle of PowerShell Core](#lifecycle-of-powershell-core), the following table lists the dates when various release will no longer be supported.</span></span>

| <span data-ttu-id="6abbb-184">Verzió</span><span class="sxs-lookup"><span data-stu-id="6abbb-184">Version</span></span> | <span data-ttu-id="6abbb-185">Élettartam végéhez közeledik</span><span class="sxs-lookup"><span data-stu-id="6abbb-185">End Of Life</span></span>                   |
|---------|-------------------------------|
| <span data-ttu-id="6abbb-186">6.0</span><span class="sxs-lookup"><span data-stu-id="6abbb-186">6.0</span></span>     | <span data-ttu-id="6abbb-187">2019. február 13.</span><span class="sxs-lookup"><span data-stu-id="6abbb-187">February 13, 2019</span></span>             |
| <span data-ttu-id="6abbb-188">6.1</span><span class="sxs-lookup"><span data-stu-id="6abbb-188">6.1</span></span>     | <span data-ttu-id="6abbb-189">2019. szeptember 28.</span><span class="sxs-lookup"><span data-stu-id="6abbb-189">September 28, 2019</span></span>            |
| <span data-ttu-id="6abbb-190">6.2</span><span class="sxs-lookup"><span data-stu-id="6abbb-190">6.2</span></span>     | <span data-ttu-id="6abbb-191">6 hónapon belül 6.3-kiadások</span><span class="sxs-lookup"><span data-stu-id="6abbb-191">6 months after 6.3 releases</span></span>   |

## <a name="platforms-which-are-out-of-support"></a><span data-ttu-id="6abbb-192">A nem támogatott platformokon</span><span class="sxs-lookup"><span data-stu-id="6abbb-192">Platforms, which are out of support</span></span>

<span data-ttu-id="6abbb-193">Amikor egy platformverzió eléri a teljes életciklusa, a platform tulajdonosa által meghatározott, a PowerShell Core is megszűnik a platform verzió támogatására.</span><span class="sxs-lookup"><span data-stu-id="6abbb-193">When a platform version reaches end-of-life as defined by the platform owner, PowerShell Core will also cease to support that platform version.</span></span>
<span data-ttu-id="6abbb-194">Korábban kiadott csomagok továbbra is elérhető marad a hozzáférés, de a hivatalos támogatási ügyfeleket, és bármilyen típusú frissítések már nem adható meg.</span><span class="sxs-lookup"><span data-stu-id="6abbb-194">Previously released packages will remain available for customers needing access but formal support and updates of any kind will no longer be provided.</span></span>

<span data-ttu-id="6abbb-195">Így a terjesztési tulajdonosai a következő verziók támogatása véget ért, és nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="6abbb-195">So, the distribution owners ended support for the following versions and are not supported.</span></span>

| <span data-ttu-id="6abbb-196">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="6abbb-196">OS</span></span>       | <span data-ttu-id="6abbb-197">Verzió</span><span class="sxs-lookup"><span data-stu-id="6abbb-197">Version</span></span> | <span data-ttu-id="6abbb-198">Élettartam végéhez közeledik</span><span class="sxs-lookup"><span data-stu-id="6abbb-198">End of Life</span></span>                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="6abbb-199">Fedora</span><span class="sxs-lookup"><span data-stu-id="6abbb-199">Fedora</span></span>   | <span data-ttu-id="6abbb-200">24</span><span class="sxs-lookup"><span data-stu-id="6abbb-200">24</span></span>      | [<span data-ttu-id="6abbb-201">2017. augusztus</span><span class="sxs-lookup"><span data-stu-id="6abbb-201">August 2017</span></span>](https://fedoramagazine.org/fedora-24-eol/)                                    |
| <span data-ttu-id="6abbb-202">Fedora</span><span class="sxs-lookup"><span data-stu-id="6abbb-202">Fedora</span></span>   | <span data-ttu-id="6abbb-203">25</span><span class="sxs-lookup"><span data-stu-id="6abbb-203">25</span></span>      | [<span data-ttu-id="6abbb-204">2017. december</span><span class="sxs-lookup"><span data-stu-id="6abbb-204">December 2017</span></span>](https://fedoramagazine.org/fedora-25-end-life/)                             |
| <span data-ttu-id="6abbb-205">Fedora</span><span class="sxs-lookup"><span data-stu-id="6abbb-205">Fedora</span></span>   | <span data-ttu-id="6abbb-206">26</span><span class="sxs-lookup"><span data-stu-id="6abbb-206">26</span></span>      | [<span data-ttu-id="6abbb-207">2018. május</span><span class="sxs-lookup"><span data-stu-id="6abbb-207">May 2018</span></span>](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| <span data-ttu-id="6abbb-208">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6abbb-208">openSUSE</span></span> | <span data-ttu-id="6abbb-209">42.1</span><span class="sxs-lookup"><span data-stu-id="6abbb-209">42.1</span></span>    | [<span data-ttu-id="6abbb-210">2017. május</span><span class="sxs-lookup"><span data-stu-id="6abbb-210">May 2017</span></span>](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| <span data-ttu-id="6abbb-211">openSUSE</span><span class="sxs-lookup"><span data-stu-id="6abbb-211">openSUSE</span></span> | <span data-ttu-id="6abbb-212">42.2</span><span class="sxs-lookup"><span data-stu-id="6abbb-212">42.2</span></span>    | [<span data-ttu-id="6abbb-213">2018. január</span><span class="sxs-lookup"><span data-stu-id="6abbb-213">January 2018</span></span>](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| <span data-ttu-id="6abbb-214">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6abbb-214">Ubuntu</span></span>   | <span data-ttu-id="6abbb-215">16.10</span><span class="sxs-lookup"><span data-stu-id="6abbb-215">16.10</span></span>   | [<span data-ttu-id="6abbb-216">2017. július</span><span class="sxs-lookup"><span data-stu-id="6abbb-216">July 2017</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| <span data-ttu-id="6abbb-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6abbb-217">Ubuntu</span></span>   | <span data-ttu-id="6abbb-218">17.04</span><span class="sxs-lookup"><span data-stu-id="6abbb-218">17.04</span></span>   | [<span data-ttu-id="6abbb-219">2018. január</span><span class="sxs-lookup"><span data-stu-id="6abbb-219">January 2018</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| <span data-ttu-id="6abbb-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6abbb-220">Ubuntu</span></span>   | <span data-ttu-id="6abbb-221">17.10</span><span class="sxs-lookup"><span data-stu-id="6abbb-221">17.10</span></span>   | [<span data-ttu-id="6abbb-222">2018. július</span><span class="sxs-lookup"><span data-stu-id="6abbb-222">July 2018</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |
| <span data-ttu-id="6abbb-223">Debian</span><span class="sxs-lookup"><span data-stu-id="6abbb-223">Debian</span></span>   | <span data-ttu-id="6abbb-224">8</span><span class="sxs-lookup"><span data-stu-id="6abbb-224">8</span></span>       | [<span data-ttu-id="6abbb-225">2018. június</span><span class="sxs-lookup"><span data-stu-id="6abbb-225">June 2018</span></span>](https://lists.debian.org/debian-security-announce/2018/msg00132.html)           |
| <span data-ttu-id="6abbb-226">Fedora</span><span class="sxs-lookup"><span data-stu-id="6abbb-226">Fedora</span></span>   | <span data-ttu-id="6abbb-227">27</span><span class="sxs-lookup"><span data-stu-id="6abbb-227">27</span></span>      | [<span data-ttu-id="6abbb-228">A 2018. november</span><span class="sxs-lookup"><span data-stu-id="6abbb-228">November 2018</span></span>](https://fedoramagazine.org/fedora-27-end-of-life/)                          |
| <span data-ttu-id="6abbb-229">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6abbb-229">Ubuntu</span></span>   | <span data-ttu-id="6abbb-230">14.04</span><span class="sxs-lookup"><span data-stu-id="6abbb-230">14.04</span></span>   | [<span data-ttu-id="6abbb-231">Április 2019</span><span class="sxs-lookup"><span data-stu-id="6abbb-231">April 2019</span></span>](https://wiki.ubuntu.com/Releases)                                              |

## <a name="notes-on-licensing"></a><span data-ttu-id="6abbb-232">Tudnivalók a licencelés</span><span class="sxs-lookup"><span data-stu-id="6abbb-232">Notes on licensing</span></span>

<span data-ttu-id="6abbb-233">A PowerShell Core alatt jelent a [MIT licenccel][].</span><span class="sxs-lookup"><span data-stu-id="6abbb-233">PowerShell Core is released under the [MIT license][].</span></span>
<span data-ttu-id="6abbb-234">Jelen licenc, és egy fizetős támogatási megállapodás nélkül, a felhasználók korlátozva, [közösségi támogatás][].</span><span class="sxs-lookup"><span data-stu-id="6abbb-234">Under this license, and without a paid support agreement, users are limited to [community support][].</span></span>
<span data-ttu-id="6abbb-235">Közösségi támogatás, a Microsoft nem vállal garanciát válaszkészségének vagy javításokat nem.</span><span class="sxs-lookup"><span data-stu-id="6abbb-235">With community support, Microsoft makes no guarantees of responsiveness or fixes.</span></span>

## <a name="windows-powershell-module"></a><span data-ttu-id="6abbb-236">Windows PowerShell-modul</span><span class="sxs-lookup"><span data-stu-id="6abbb-236">Windows PowerShell Module</span></span>

<span data-ttu-id="6abbb-237">Támogatja a PowerShell Core nem tartalmazza a termék-modulok, ha az ilyen modulokhoz explicit módon támogatja a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="6abbb-237">Support for PowerShell Core does not include product modules, unless those modules explicitly support PowerShell Core.</span></span>
<span data-ttu-id="6abbb-238">Például a `ActiveDirectory` modul részét képező Windows Server része nem támogatott forgatókönyv szerint.</span><span class="sxs-lookup"><span data-stu-id="6abbb-238">For example, using the `ActiveDirectory` module that ships as part of Windows Server is an unsupported scenario.</span></span>

<span data-ttu-id="6abbb-239">Előfordulhat azonban, a PowerShell Core explicit módon nem támogató modulok kompatibilis bizonyos esetekben.</span><span class="sxs-lookup"><span data-stu-id="6abbb-239">However, modules that do not explicitly support PowerShell Core may be compatible in some cases.</span></span>
<span data-ttu-id="6abbb-240">Telepítse a [ `WindowsPSModulePath` ][] modult, hozzáadhatja a Windows PowerShell `PSModulePath` , a PowerShell Core `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="6abbb-240">By installing the [`WindowsPSModulePath`][] module, you can add the Windows PowerShell `PSModulePath` to your PowerShell Core `PSModulePath`.</span></span>

<span data-ttu-id="6abbb-241">Először telepítse a `WindowsPSModulePath` modul a PowerShell-galériából:</span><span class="sxs-lookup"><span data-stu-id="6abbb-241">First, install the `WindowsPSModulePath` module from the PowerShell Gallery:</span></span>

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

<span data-ttu-id="6abbb-242">Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` adja hozzá a Windows PowerShell-parancsmagot `PSModulePath` a PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="6abbb-242">After installing this module, run the `Add-WindowsPSModulePath` cmdlet to add the Windows PowerShell `PSModulePath` to PowerShell Core:</span></span>

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

## <a name="experimental-features"></a><span data-ttu-id="6abbb-243">Kísérleti funkciók</span><span class="sxs-lookup"><span data-stu-id="6abbb-243">Experimental features</span></span>

<span data-ttu-id="6abbb-244">[Kísérleti funkciók][] korlátozódnak [közösségi támogatás](#community-support).</span><span class="sxs-lookup"><span data-stu-id="6abbb-244">[Experimental features][] are limited to [community support](#community-support).</span></span>

[A Premier szintű]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[Közösségi támogatás]: https://github.com/powershell/powershell/issues
[community support]: https://github.com/powershell/powershell/issues
[A Microsoft Community]: https://answers.microsoft.com/
[Microsoft Community]: https://answers.microsoft.com/
[PowerShell technikai Közösség]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[tanácsadással]: https://support.microsoft.com/assistedsupportproducts
[assisted support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenccel]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[Kísérleti funkciók]: /powershell/module/microsoft.powershell.core/about/about_powershell_config?view=powershell-6#experimentalfeatures
[Experimental features]: /powershell/module/microsoft.powershell.core/about/about_powershell_config?view=powershell-6#experimentalfeatures
