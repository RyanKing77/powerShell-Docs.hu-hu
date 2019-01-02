---
title: A PowerShell Core támogatási életciklusa
description: A PowerShell Core támogatási szabályzatok betartatását
ms.date: 08/06/2018
ms.openlocfilehash: 2e0ca1b9c133e6f316a40aff13365d0489059165
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53405594"
---
# <a name="powershell-core-support-lifecycle"></a><span data-ttu-id="1f9a2-103">A PowerShell Core támogatási életciklusa</span><span class="sxs-lookup"><span data-stu-id="1f9a2-103">PowerShell Core Support Lifecycle</span></span>

<span data-ttu-id="1f9a2-104">A PowerShell Core a meghatározott készletét eszközök és -összetevők, amely tartalmazza a szükséges, telepítve van, és külön konfigurálni a Windows Powershellből.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-104">PowerShell Core is a distinct set of tools and components that is shipped, installed, and configured separately from Windows PowerShell.</span></span>
<span data-ttu-id="1f9a2-105">Ezért a PowerShell Core nem szerepel a Windows 7/8.1/10 vagy Windows Server licencelési megállapodások.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-105">Therefore, PowerShell Core is not included in the Windows 7/8.1/10 or Windows Server licensing agreements.</span></span>

<span data-ttu-id="1f9a2-106">Azonban a PowerShell Core a hagyományos Microsoft támogatási szerződés, beleértve a támogatott [Premier][], [Microsoft Enterprise-megállapodások][enterprise-agreement], és [Microsoft frissítési garanciával rendelkező][assurance].</span><span class="sxs-lookup"><span data-stu-id="1f9a2-106">However, PowerShell Core is supported under traditional Microsoft support agreements, including [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement], and [Microsoft Software Assurance][assurance].</span></span>
<span data-ttu-id="1f9a2-107">Is fizethet a szolgáltatásért [személyes támogatás][] a PowerShell Core ügyfélszolgálatunknak küldött támogatási kérelmet a problémát.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-107">You can also pay for [assisted support][] for PowerShell Core by filing a support request for your problem.</span></span>

<span data-ttu-id="1f9a2-108">Emellett [közösségi támogatás][] a Githubon, ahol egy problémát, programhiba vagy funkcióigénylés fájlt is.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-108">We also offer [community support][] on GitHub where you can file an issue, bug, or feature request.</span></span>
<span data-ttu-id="1f9a2-109">Is előfordulhat, hogy megtalálja a Közösség más tagjai segítséget az általános [Microsoft Community][] vagy a Microsoft [PowerShell technikai Közösség][].</span><span class="sxs-lookup"><span data-stu-id="1f9a2-109">Alternatively, you may find help from other members of the community on the general [Microsoft Community][] or the Microsoft [PowerShell Tech Community][].</span></span>
<span data-ttu-id="1f9a2-110">Nem kínál nincs garancia van, hogy a probléma megoldásához címzett vagy időben fog állni.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-110">We offer no guarantee there that your issue will be addressed or resolved in a timely manner.</span></span>
<span data-ttu-id="1f9a2-111">Ha azonnali figyelmet igénylő problémával rendelkezik, használja a hagyományos, fizetős támogatási lehetőségek.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-111">If you have a problem that requires immediate attention, you should use the traditional, paid support options.</span></span>

## <a name="lifecycle-of-powershell-core"></a><span data-ttu-id="1f9a2-112">A PowerShell Core élettartama</span><span class="sxs-lookup"><span data-stu-id="1f9a2-112">Lifecycle of PowerShell Core</span></span>

<span data-ttu-id="1f9a2-113">A PowerShell Core kíván bevezetni a [Microsoft Modern életciklus-szabályzat][modern].</span><span class="sxs-lookup"><span data-stu-id="1f9a2-113">PowerShell Core is adopting the [Microsoft Modern Lifecycle Policy][modern].</span></span>
<span data-ttu-id="1f9a2-114">A támogatási életciklusa célja, hogy az ügyfelek naprakészen tartása a legújabb verzióra.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-114">This support lifecycle is intended to keep customers up-to-date with the latest versions.</span></span>

<span data-ttu-id="1f9a2-115">A PowerShell Core verzió 6.x ága körülbelül hat havonta frissül (pl. 6.0-s, 6.1, 6.2, stb.)</span><span class="sxs-lookup"><span data-stu-id="1f9a2-115">The version 6.x branch of PowerShell Core will be updated approximately once every six months (e.g. 6.0, 6.1, 6.2, etc.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f9a2-116">Miután minden egyes új alverzió kiadási támogatás folytatásához hat hónapon belül kell frissíteni.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-116">You must update within six months after each new minor version release to continue receiving support.</span></span>

<span data-ttu-id="1f9a2-117">Például ha a PowerShell Core 6.1-es kiadás dátuma: 2018. július 1-től., akkor elvárják, hogy frissítheti a PowerShell Core 6.1-es verzióját 2019. január 1-től. a támogatás.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-117">For example, if PowerShell Core 6.1 is released on July 1st, 2018, you would be expected to update to PowerShell Core 6.1 by January 1st, 2019 to maintain support.</span></span>

![A PowerShell Core ág életciklusa][lifecycle-chart]

<span data-ttu-id="1f9a2-119">A Modern életciklus-szabályzat is megköveteli, hogy a Microsoft értesítést ügyfelek 12 hónapig előtt megszűnő támogatás a termék (azaz a PowerShell Core).</span><span class="sxs-lookup"><span data-stu-id="1f9a2-119">The Modern Lifecycle Policy also requires that Microsoft give customers 12 months notice before discontinuing support for a product (i.e. PowerShell Core).</span></span>

<span data-ttu-id="1f9a2-120">Idővel várhatóan a alkalmazni a PowerShell Core, a "hosszú távú karbantartási" megközelítést kellene, hogy csak a karbantartási és biztonsági frissítések belül egy adott ág/verzióját 6.x támogatását.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-120">Eventually, we expect PowerShell Core will adopt the "long-term servicing" approach where we would require only servicing and security updates to stay in support on a specific branch/version of 6.x.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="1f9a2-121">Támogatott platformok</span><span class="sxs-lookup"><span data-stu-id="1f9a2-121">Supported platforms</span></span>

<span data-ttu-id="1f9a2-122">Tekintse át az alábbi táblázat megtekintéséhez használja a PowerShell Core verziója hivatalosan támogatott platform.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-122">Please see the following table to see what platform the version of PowerShell Core you are using is officially supported.</span></span>

<span data-ttu-id="1f9a2-123">Közösségünkhöz is hozzájárult a csomagokat, az egyes platformok esetében, de ez nem hivatalosan támogatott.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-123">Our community has also contributed packages for some platforms, but they are not officially supported.</span></span>
<span data-ttu-id="1f9a2-124">Ezek a csomagok vannak megjelölve `Community` a táblában.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-124">These packages are marked as `Community` in the table.</span></span>

<span data-ttu-id="1f9a2-125">Felsorolt platformok `Experimental` hivatalosan nem támogatottak, de a Kísérletezési és visszajelzés elérhető.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-125">Platforms listed as `Experimental` are not officially supported, but are available for experimentation and feedback.</span></span>

|                                                   | <span data-ttu-id="1f9a2-126">6.0</span><span class="sxs-lookup"><span data-stu-id="1f9a2-126">6.0</span></span>         | <span data-ttu-id="1f9a2-127">6.1</span><span class="sxs-lookup"><span data-stu-id="1f9a2-127">6.1</span></span>         |
|---------------------------------------------------|:-----------:|:-----------:|
| <span data-ttu-id="1f9a2-128">Windows 7, 8.1 és 10</span><span class="sxs-lookup"><span data-stu-id="1f9a2-128">Windows 7, 8.1, and 10</span></span>                            | <span data-ttu-id="1f9a2-129">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-129">Supported</span></span>   | <span data-ttu-id="1f9a2-130">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-130">Supported</span></span>   |
| <span data-ttu-id="1f9a2-131">Windows Server 2008 R2, 2012 R2, 2016</span><span class="sxs-lookup"><span data-stu-id="1f9a2-131">Windows Server 2008 R2, 2012 R2, 2016</span></span>             | <span data-ttu-id="1f9a2-132">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-132">Supported</span></span>   | <span data-ttu-id="1f9a2-133">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-133">Supported</span></span>   |
| <span data-ttu-id="1f9a2-134">[A Windows Server féléves csatorna][semi-annual]</span><span class="sxs-lookup"><span data-stu-id="1f9a2-134">[Windows Server Semi-Annual Channel][semi-annual]</span></span> | <span data-ttu-id="1f9a2-135">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-135">Supported</span></span>   | <span data-ttu-id="1f9a2-136">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-136">Supported</span></span>   |
| <span data-ttu-id="1f9a2-137">Ubuntu 14.04, és 16.04</span><span class="sxs-lookup"><span data-stu-id="1f9a2-137">Ubuntu 14.04 and, 16.04</span></span>                           | <span data-ttu-id="1f9a2-138">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-138">Supported</span></span>   | <span data-ttu-id="1f9a2-139">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-139">Supported</span></span>   |
| <span data-ttu-id="1f9a2-140">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="1f9a2-140">Ubuntu 18.04</span></span>                                      |             | <span data-ttu-id="1f9a2-141">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-141">Supported</span></span>   |
| <span data-ttu-id="1f9a2-142">Ubuntu 18.10 (keresztül Számértékekhez igazodnak, a csomag)</span><span class="sxs-lookup"><span data-stu-id="1f9a2-142">Ubuntu 18.10 (via Snap Package)</span></span>                   |             | <span data-ttu-id="1f9a2-143">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-143">Community</span></span>   |
| <span data-ttu-id="1f9a2-144">Debian 8.7 + és 9</span><span class="sxs-lookup"><span data-stu-id="1f9a2-144">Debian 8.7+, and 9</span></span>                                | <span data-ttu-id="1f9a2-145">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-145">Supported</span></span>   | <span data-ttu-id="1f9a2-146">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-146">Supported</span></span>   |
| <span data-ttu-id="1f9a2-147">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="1f9a2-147">CentOS 7</span></span>                                          | <span data-ttu-id="1f9a2-148">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-148">Supported</span></span>   | <span data-ttu-id="1f9a2-149">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-149">Supported</span></span>   |
| <span data-ttu-id="1f9a2-150">Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="1f9a2-150">Red Hat Enterprise Linux 7</span></span>                        | <span data-ttu-id="1f9a2-151">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-151">Supported</span></span>   | <span data-ttu-id="1f9a2-152">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-152">Supported</span></span>   |
| <span data-ttu-id="1f9a2-153">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="1f9a2-153">OpenSUSE 42.3</span></span>                                     | <span data-ttu-id="1f9a2-154">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-154">Supported</span></span>   | <span data-ttu-id="1f9a2-155">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-155">Supported</span></span>   |
| <span data-ttu-id="1f9a2-156">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="1f9a2-156">Fedora 27</span></span>                                         | <span data-ttu-id="1f9a2-157">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-157">Supported</span></span>   | <span data-ttu-id="1f9a2-158">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-158">Supported</span></span>   |
| <span data-ttu-id="1f9a2-159">28 Fedora</span><span class="sxs-lookup"><span data-stu-id="1f9a2-159">Fedora 28</span></span>                                         |             | <span data-ttu-id="1f9a2-160">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-160">Supported</span></span>   |
| <span data-ttu-id="1f9a2-161">macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="1f9a2-161">macOS 10.12+</span></span>                                      | <span data-ttu-id="1f9a2-162">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-162">Supported</span></span>   | <span data-ttu-id="1f9a2-163">Támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-163">Supported</span></span>   |
| <span data-ttu-id="1f9a2-164">Arch</span><span class="sxs-lookup"><span data-stu-id="1f9a2-164">Arch</span></span>                                              | <span data-ttu-id="1f9a2-165">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-165">Community</span></span>   | <span data-ttu-id="1f9a2-166">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-166">Community</span></span>   |
| <span data-ttu-id="1f9a2-167">Raspbian</span><span class="sxs-lookup"><span data-stu-id="1f9a2-167">Raspbian</span></span>                                          | <span data-ttu-id="1f9a2-168">Kísérleti</span><span class="sxs-lookup"><span data-stu-id="1f9a2-168">Experimental</span></span>| <span data-ttu-id="1f9a2-169">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-169">Community</span></span>   |
| <span data-ttu-id="1f9a2-170">Kali</span><span class="sxs-lookup"><span data-stu-id="1f9a2-170">Kali</span></span>                                              | <span data-ttu-id="1f9a2-171">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-171">Community</span></span>   | <span data-ttu-id="1f9a2-172">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-172">Community</span></span>   |
| <span data-ttu-id="1f9a2-173">AppImage (több Linux platformon működik)</span><span class="sxs-lookup"><span data-stu-id="1f9a2-173">AppImage  (works on multiple Linux platforms)</span></span>     | <span data-ttu-id="1f9a2-174">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-174">Community</span></span>   | <span data-ttu-id="1f9a2-175">Közösség</span><span class="sxs-lookup"><span data-stu-id="1f9a2-175">Community</span></span>   |
| [<span data-ttu-id="1f9a2-176">Oszlopokhoz illesztés csomag</span><span class="sxs-lookup"><span data-stu-id="1f9a2-176">Snap Package</span></span>](https://snapcraft.io/powershell)   | <span data-ttu-id="1f9a2-177">Lásd a megjegyzést</span><span class="sxs-lookup"><span data-stu-id="1f9a2-177">See note</span></span>    | <span data-ttu-id="1f9a2-178">Lásd a megjegyzést</span><span class="sxs-lookup"><span data-stu-id="1f9a2-178">See note</span></span>    |

> [!NOTE]
> <span data-ttu-id="1f9a2-179">Az illesztési csomagok kísérleti lesz egy ideig.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-179">Snap packages will be experimental for a period.</span></span>  <span data-ttu-id="1f9a2-180">Miután vagyunk abban, hogy a beépülő modul nem vezet be új támogatási problémák, a támogatási követi a futtatja, a csomag terjesztési.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-180">After, we are confident that Snap does not introduce new support issues, the support will follow the distribution you are running the package on.</span></span>

## <a name="platform-which-are-out-of-support"></a><span data-ttu-id="1f9a2-181">Platform, amely nem támogatott</span><span class="sxs-lookup"><span data-stu-id="1f9a2-181">Platform which are out of support</span></span>

<span data-ttu-id="1f9a2-182">Amikor egy platformverzió eléri a teljes életciklusa a platform tulajdonosa által meghatározott, a PowerShell Core is megszűnik támogatást nyújt a platform verziója.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-182">When a platform version reaches end-of-life as defined by the platform owner, PowerShell Core will also cease to provide support for that platform version.</span></span> <span data-ttu-id="1f9a2-183">Korábban kiadott csomagok továbbra is elérhető marad a hozzáférés, de a hivatalos támogatási ügyfeleket, és bármilyen típusú frissítések már nem adható meg.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-183">Previously released packages will remain available for customers needing access but formal support and updates of any kind will no longer be provided.</span></span>

<span data-ttu-id="1f9a2-184">Ezért támogatja a következő verziók által a terjesztési tulajdonosok befejeződött, és nem támogatottak.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-184">Therefore, support for the following versions was ended by the distribution owners and are not supported.</span></span>

| <span data-ttu-id="1f9a2-185">Operációs rendszer</span><span class="sxs-lookup"><span data-stu-id="1f9a2-185">OS</span></span>       | <span data-ttu-id="1f9a2-186">Verzió</span><span class="sxs-lookup"><span data-stu-id="1f9a2-186">Version</span></span> | <span data-ttu-id="1f9a2-187">Élettartam végéhez közeledik</span><span class="sxs-lookup"><span data-stu-id="1f9a2-187">End of Life</span></span>                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="1f9a2-188">Fedora</span><span class="sxs-lookup"><span data-stu-id="1f9a2-188">Fedora</span></span>   | <span data-ttu-id="1f9a2-189">24</span><span class="sxs-lookup"><span data-stu-id="1f9a2-189">24</span></span>      | [<span data-ttu-id="1f9a2-190">2017. augusztus</span><span class="sxs-lookup"><span data-stu-id="1f9a2-190">August 2017</span></span>](https://fedoramagazine.org/fedora-24-eol/)                                    |
| <span data-ttu-id="1f9a2-191">Fedora</span><span class="sxs-lookup"><span data-stu-id="1f9a2-191">Fedora</span></span>   | <span data-ttu-id="1f9a2-192">25</span><span class="sxs-lookup"><span data-stu-id="1f9a2-192">25</span></span>      | [<span data-ttu-id="1f9a2-193">2017. december</span><span class="sxs-lookup"><span data-stu-id="1f9a2-193">December 2017</span></span>](https://fedoramagazine.org/fedora-25-end-life/)                             |
| <span data-ttu-id="1f9a2-194">Fedora</span><span class="sxs-lookup"><span data-stu-id="1f9a2-194">Fedora</span></span>   | <span data-ttu-id="1f9a2-195">26</span><span class="sxs-lookup"><span data-stu-id="1f9a2-195">26</span></span>      | [<span data-ttu-id="1f9a2-196">2018. május</span><span class="sxs-lookup"><span data-stu-id="1f9a2-196">May 2018</span></span>](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| <span data-ttu-id="1f9a2-197">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="1f9a2-197">openSUSE</span></span> | <span data-ttu-id="1f9a2-198">42.1</span><span class="sxs-lookup"><span data-stu-id="1f9a2-198">42.1</span></span>    | [<span data-ttu-id="1f9a2-199">2017. május</span><span class="sxs-lookup"><span data-stu-id="1f9a2-199">May 2017</span></span>](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| <span data-ttu-id="1f9a2-200">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="1f9a2-200">openSUSE</span></span> | <span data-ttu-id="1f9a2-201">42.2</span><span class="sxs-lookup"><span data-stu-id="1f9a2-201">42.2</span></span>    | [<span data-ttu-id="1f9a2-202">2018. január</span><span class="sxs-lookup"><span data-stu-id="1f9a2-202">January 2018</span></span>](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| <span data-ttu-id="1f9a2-203">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1f9a2-203">Ubuntu</span></span>   | <span data-ttu-id="1f9a2-204">16.10</span><span class="sxs-lookup"><span data-stu-id="1f9a2-204">16.10</span></span>   | [<span data-ttu-id="1f9a2-205">2017. július</span><span class="sxs-lookup"><span data-stu-id="1f9a2-205">July 2017</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| <span data-ttu-id="1f9a2-206">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1f9a2-206">Ubuntu</span></span>   | <span data-ttu-id="1f9a2-207">17.04</span><span class="sxs-lookup"><span data-stu-id="1f9a2-207">17.04</span></span>   | [<span data-ttu-id="1f9a2-208">2018. január</span><span class="sxs-lookup"><span data-stu-id="1f9a2-208">January 2018</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| <span data-ttu-id="1f9a2-209">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1f9a2-209">Ubuntu</span></span>   | <span data-ttu-id="1f9a2-210">17.10</span><span class="sxs-lookup"><span data-stu-id="1f9a2-210">17.10</span></span>   | [<span data-ttu-id="1f9a2-211">2018. július</span><span class="sxs-lookup"><span data-stu-id="1f9a2-211">July 2018</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |

## <a name="notes-on-licensing"></a><span data-ttu-id="1f9a2-212">Tudnivalók a licencelés</span><span class="sxs-lookup"><span data-stu-id="1f9a2-212">Notes on licensing</span></span>

<span data-ttu-id="1f9a2-213">A PowerShell Core alatt jelent a [MIT licenccel][].</span><span class="sxs-lookup"><span data-stu-id="1f9a2-213">PowerShell Core is released under the [MIT license][].</span></span>
<span data-ttu-id="1f9a2-214">Jelen licenc, és a egy fizetős támogatási szerződés hiányában a felhasználók korlátozva, [közösségi támogatás][].</span><span class="sxs-lookup"><span data-stu-id="1f9a2-214">Under this license, and in the absence of a paid support agreement, users are limited to [community support][].</span></span>
<span data-ttu-id="1f9a2-215">Közösségi támogatás, a Microsoft nem vállal garanciát válaszkészségének vagy javításokat nem.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-215">With community support, Microsoft makes no guarantees of responsiveness or fixes.</span></span>

## <a name="windows-powershell-module"></a><span data-ttu-id="1f9a2-216">Windows PowerShell-modul</span><span class="sxs-lookup"><span data-stu-id="1f9a2-216">Windows PowerShell Module</span></span>

<span data-ttu-id="1f9a2-217">Támogatja a PowerShell Core nem terjed ki a többi termék modulok, ha az ilyen modulokhoz explicit módon támogatja a PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-217">Support for PowerShell Core does not extend to other product modules unless those modules explicitly support PowerShell Core.</span></span>
<span data-ttu-id="1f9a2-218">Például a `ActiveDirectory` modul részét képező Windows Server része nem támogatott forgatókönyv szerint.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-218">For example, using the `ActiveDirectory` module that ships as part of Windows Server is an unsupported scenario.</span></span>

<span data-ttu-id="1f9a2-219">Előfordulhat azonban, a PowerShell Core explicit módon nem támogató modulok kompatibilis bizonyos esetekben.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-219">However, modules that do not explicitly support PowerShell Core may be compatible in some cases.</span></span>
<span data-ttu-id="1f9a2-220">Telepítse a [ `WindowsPSModulePath` ][] modult, fűzze hozzá a Windows PowerShell `PSModulePath` , a PowerShell Core `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="1f9a2-220">By installing the [`WindowsPSModulePath`][] module, you can append the Windows PowerShell `PSModulePath` to your PowerShell Core `PSModulePath`.</span></span>

<span data-ttu-id="1f9a2-221">Először telepítse a `WindowsPSModulePath` modul a PowerShell-galériából:</span><span class="sxs-lookup"><span data-stu-id="1f9a2-221">First, install the `WindowsPSModulePath` module from the PowerShell Gallery:</span></span>

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

<span data-ttu-id="1f9a2-222">Ez a modul telepítése után futtassa a `Add-WindowsPSModulePath` adja hozzá a Windows PowerShell-parancsmagot `PSModulePath` a PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="1f9a2-222">After installing this module, run the `Add-WindowsPSModulePath` cmdlet to add the Windows PowerShell `PSModulePath` to PowerShell Core:</span></span>

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
[PowerShell technikai Közösség]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[személyes támogatás]: https://support.microsoft.com/assistedsupportproducts
[assisted support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[MIT licenccel]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath"]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
