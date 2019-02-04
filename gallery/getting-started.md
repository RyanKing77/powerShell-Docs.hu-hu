---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: A PowerShell-galériából használatának első lépései
ms.openlocfilehash: c8beba3009e462ce52cdecd34fc0313d9234f289
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688846"
---
# <a name="getting-started-with-the-powershell-gallery"></a><span data-ttu-id="1808a-103">A PowerShell-galériából – első lépések</span><span class="sxs-lookup"><span data-stu-id="1808a-103">Getting Started with the PowerShell Gallery</span></span>

<span data-ttu-id="1808a-104">A PowerShell-galériából tárháza csomagot tartalmazó parancsfájlok, a modulok és a DSC-erőforrások letöltheti és használhatja.</span><span class="sxs-lookup"><span data-stu-id="1808a-104">The PowerShell Gallery is a package repository containing scripts, modules, and DSC resources you can download and leverage.</span></span> <span data-ttu-id="1808a-105">A parancsmagok használata a [PowerShellGet](/powershell/module/powershellget) modul a PowerShell-galériából csomagok telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="1808a-105">You use the cmdlets in the [PowerShellGet](/powershell/module/powershellget) module to install packages from the PowerShell Gallery.</span></span> <span data-ttu-id="1808a-106">Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.</span><span class="sxs-lookup"><span data-stu-id="1808a-106">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="1808a-107">Lehetséges, hogy közvetlenül a PowerShell-galériából töltse le a csomag, de ez nem ajánlott eljárás.</span><span class="sxs-lookup"><span data-stu-id="1808a-107">It is possible to download a package from the PowerShell Gallery directly, but this is not a recommended approach.</span></span>
> <span data-ttu-id="1808a-108">További részletekért lásd: [manuális letöltés](/powershell/gallery/how-to/working-with-packages/manual-download).</span><span class="sxs-lookup"><span data-stu-id="1808a-108">For more details, see [Manual Package Download](/powershell/gallery/how-to/working-with-packages/manual-download).</span></span>

## <a name="discovering-packages-from-the-powershell-gallery"></a><span data-ttu-id="1808a-109">A PowerShell-galériából csomagok felderítése</span><span class="sxs-lookup"><span data-stu-id="1808a-109">Discovering packages from the PowerShell Gallery</span></span>

<span data-ttu-id="1808a-110">Található csomagokat a PowerShell-galériából használatával a **keresési** vezérlőelem a PowerShell-galériából [kezdőlap](https://www.powershellgallery.com), vagy keresse a modulok és a parancsfájlokat a a [csomagok lapján ](https://www.powershellgallery.com/packages).</span><span class="sxs-lookup"><span data-stu-id="1808a-110">You can find packages in the PowerShell Gallery by using the **Search** control on the PowerShell Gallery's [home page](https://www.powershellgallery.com), or by browsing through the Modules and Scripts from the [Packages page](https://www.powershellgallery.com/packages).</span></span> <span data-ttu-id="1808a-111">A PowerShell-galériából csomagok futtatásával is talál a [Find-Module][], [Find-DscResource], és [Find-Script][] parancsmagok, a csomag típusától függően a `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="1808a-111">You can also find packages from the PowerShell Gallery by running the [Find-Module][], [Find-DscResource], and [Find-Script][] cmdlets, depending on the package type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="1808a-112">A katalógus eredményeit az alábbi paraméterek használatával szűrheti:</span><span class="sxs-lookup"><span data-stu-id="1808a-112">You can filter results from the Gallery by using the following parameters:</span></span>

- <span data-ttu-id="1808a-113">Név</span><span class="sxs-lookup"><span data-stu-id="1808a-113">Name</span></span>
- <span data-ttu-id="1808a-114">Allversions paramétert</span><span class="sxs-lookup"><span data-stu-id="1808a-114">AllVersions</span></span>
- <span data-ttu-id="1808a-115">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="1808a-115">MinimumVersion</span></span>
- <span data-ttu-id="1808a-116">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="1808a-116">RequiredVersion</span></span>
- <span data-ttu-id="1808a-117">Címke</span><span class="sxs-lookup"><span data-stu-id="1808a-117">Tag</span></span>
- <span data-ttu-id="1808a-118">Magában foglalja</span><span class="sxs-lookup"><span data-stu-id="1808a-118">Includes</span></span>
- <span data-ttu-id="1808a-119">DscResource</span><span class="sxs-lookup"><span data-stu-id="1808a-119">DscResource</span></span>
- <span data-ttu-id="1808a-120">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="1808a-120">RoleCapability</span></span>
- <span data-ttu-id="1808a-121">Parancs</span><span class="sxs-lookup"><span data-stu-id="1808a-121">Command</span></span>
- <span data-ttu-id="1808a-122">Szűrő</span><span class="sxs-lookup"><span data-stu-id="1808a-122">Filter</span></span>

<span data-ttu-id="1808a-123">Ha érdekli csak a katalógus adott DSC-erőforrások felderítéséhez, akkor futtathatja a [Find-DscResource] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1808a-123">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="1808a-124">Find-DscResource DSC-erőforrások a katalógusban szereplő adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="1808a-124">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="1808a-125">DSC-erőforrások mindig érkezzenek a modul részét képező, mert továbbra is szeretné futtatni [Install-Module][] ezen DSC-erőforrások telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="1808a-125">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-packages-in-the-powershell-gallery"></a><span data-ttu-id="1808a-126">Tudnivalók a PowerShell-galériából-csomagok</span><span class="sxs-lookup"><span data-stu-id="1808a-126">Learning about packages in the PowerShell Gallery</span></span>

<span data-ttu-id="1808a-127">Egy csomagot, amely az Önt érdeklő azonosítása, után érdemes többet szeretne megtudni róla.</span><span class="sxs-lookup"><span data-stu-id="1808a-127">Once you've identified a package that you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="1808a-128">Ehhez megvizsgálja az adott oldalra a csomag a katalógusban.</span><span class="sxs-lookup"><span data-stu-id="1808a-128">You can do this by examining that package's specific page on the Gallery.</span></span> <span data-ttu-id="1808a-129">A oldalon láthatja az összes a metaadatokat a csomag feltöltése.</span><span class="sxs-lookup"><span data-stu-id="1808a-129">On that page, you'll be able to see all of the metadata uploaded with the package.</span></span> <span data-ttu-id="1808a-130">Ezeket a metaadatokat a csomag szerzője által biztosított, és a Microsoft nem ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="1808a-130">This metadata is provided by the package's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="1808a-131">A csomag tulajdonosát erősen vannak kötve, a katalógus fiók tesz közzé a csomagot, és több megbízható-e, mint az Author mező.</span><span class="sxs-lookup"><span data-stu-id="1808a-131">The Owner of the package is strongly tied to the Gallery account used to publish the package, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="1808a-132">Ha egy csomagot, amely úgy gondolja, hogy nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** a kérdéses csomag lapon.</span><span class="sxs-lookup"><span data-stu-id="1808a-132">If you discover a package that you feel is not published in good faith, click **Report Abuse** on that package's page.</span></span>

<span data-ttu-id="1808a-133">Ha [Find-Module][] vagy [Find-Script][], a visszaadott PSGetModuleInfo objektumban is megtekintheti ezeket az adatokat.</span><span class="sxs-lookup"><span data-stu-id="1808a-133">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="1808a-134">Ha például fut `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span><span class="sxs-lookup"><span data-stu-id="1808a-134">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span></span>
<span data-ttu-id="1808a-135">a katalógusban az PSReadLine modulban adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="1808a-135">returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-packages-from-the-powershell-gallery"></a><span data-ttu-id="1808a-136">A PowerShell-galériából csomagok letöltése</span><span class="sxs-lookup"><span data-stu-id="1808a-136">Downloading packages from the PowerShell Gallery</span></span>

<span data-ttu-id="1808a-137">A PowerShell-galériából való letöltése a csomagok esetén a következőket javasoljuk:</span><span class="sxs-lookup"><span data-stu-id="1808a-137">We encourage the following process when downloading packages from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="1808a-138">Vizsgálja meg</span><span class="sxs-lookup"><span data-stu-id="1808a-138">Inspect</span></span>

<span data-ttu-id="1808a-139">A csomag letöltéséhez vizsgálatra a katalógusból, futtathatja az alábbiak a [Save-Module][] vagy [Save-Script][] parancsmagot, a csomag típusától függően.</span><span class="sxs-lookup"><span data-stu-id="1808a-139">To download a package from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the package type.</span></span> <span data-ttu-id="1808a-140">Ez lehetővé teszi a csomag mentéséhez helyi telepítés nélküli, és vizsgálja meg a csomag tartalma.</span><span class="sxs-lookup"><span data-stu-id="1808a-140">This lets you save the package locally without installing it, and inspect the package contents.</span></span> <span data-ttu-id="1808a-141">Ne felejtse el kézzel törölje a mentett csomagot.</span><span class="sxs-lookup"><span data-stu-id="1808a-141">Remember to delete the saved package manually.</span></span>

<span data-ttu-id="1808a-142">Néhány ezeket a csomagokat a Microsoft által lett létrehozva, és mások vannak a PowerShell-Közösség által készített.</span><span class="sxs-lookup"><span data-stu-id="1808a-142">Some of these packages are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="1808a-143">A Microsoft azt javasolja, hogy tekintse át a tartalmát és kódját a csomagok a katalógusban a telepítés előtt.</span><span class="sxs-lookup"><span data-stu-id="1808a-143">Microsoft recommends that you review the contents and code of packages on this gallery prior to installation.</span></span>

<span data-ttu-id="1808a-144">Ha egy csomagot, amely úgy gondolja, hogy nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** a kérdéses csomag lapon.</span><span class="sxs-lookup"><span data-stu-id="1808a-144">If you discover a package that you feel is not published in good faith, click **Report Abuse** on that package's page.</span></span>

### <a name="install"></a><span data-ttu-id="1808a-145">Telepítés</span><span class="sxs-lookup"><span data-stu-id="1808a-145">Install</span></span>

<span data-ttu-id="1808a-146">A csomag telepítéséhez használható a katalógusból, futtathatja az alábbiak a [Install-Module][] vagy [Install-Script][] parancsmagot, a csomag típusától függően.</span><span class="sxs-lookup"><span data-stu-id="1808a-146">To install a package from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the package type.</span></span>

<span data-ttu-id="1808a-147">[Install-Module][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="1808a-147">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="1808a-148">Ehhez rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="1808a-148">This requires an administrator account.</span></span> <span data-ttu-id="1808a-149">Ha a `-Scope CurrentUser` paramétert, telepítve van a modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="1808a-149">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="1808a-150">[Install-Script][] a parancsfájl telepíti `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="1808a-150">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="1808a-151">Ehhez rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="1808a-151">This requires an administrator account.</span></span> <span data-ttu-id="1808a-152">Ha a `-Scope CurrentUser` paramétert, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="1808a-152">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="1808a-153">Alapértelmezés szerint [Install-Module][] és [Install-Script][] telepíti egy csomagot a legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="1808a-153">By default, [Install-Module][] and [Install-Script][] installs the most current version of a package.</span></span>
<span data-ttu-id="1808a-154">Egy régebbi verzióját a csomag telepítéséhez, adja hozzá a `-RequiredVersion` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1808a-154">To install an older version of the package, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="1808a-155">telepítése Telepítse a</span><span class="sxs-lookup"><span data-stu-id="1808a-155">Deploy</span></span>

<span data-ttu-id="1808a-156">Egy csomag az Azure Automation PowerShell-galériából történő üzembe helyezéséhez kattintson **Azure Automation**, majd kattintson a **üzembe helyezés az Azure Automation** csomag részleteit megjelenítő oldalon.</span><span class="sxs-lookup"><span data-stu-id="1808a-156">To deploy a package from the PowerShell Gallery to Azure Automation, click **Azure Automation**, then click **Deploy to Azure Automation** on the package details page.</span></span> <span data-ttu-id="1808a-157">Ekkor megnyílik az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiók hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="1808a-157">You are redirected to the Azure Management Portal where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="1808a-158">Vegye figyelembe, hogy függőségekkel rendelkező csomagok telepítése telepíti a függőségeket az Azure Automationhöz.</span><span class="sxs-lookup"><span data-stu-id="1808a-158">Note that deploying packages with dependencies deploys all the dependencies to Azure Automation.</span></span> <span data-ttu-id="1808a-159">Adja hozzá a "Üzembe helyezés az Azure Automation" gomb letiltható a **AzureAutomationNotSupported** a csomag metaadata címkét.</span><span class="sxs-lookup"><span data-stu-id="1808a-159">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your package metadata.</span></span>

<span data-ttu-id="1808a-160">Azure Automation kapcsolatos további információkért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="1808a-160">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-packages-from-the-powershell-gallery"></a><span data-ttu-id="1808a-161">A PowerShell-galériából csomagok frissítése</span><span class="sxs-lookup"><span data-stu-id="1808a-161">Updating packages from the PowerShell Gallery</span></span>

<span data-ttu-id="1808a-162">A PowerShell-galériából telepített csomagok frissítéséhez futtassa a [Update-modul] [-] vagy [frissítési parancsfájl] [] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1808a-162">To update packages installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="1808a-163">Ha további paraméterek nélkül futtatja, [Update-modul] [-] futtatásával telepített összes modul frissíteni próbálja [Install-Module][].</span><span class="sxs-lookup"><span data-stu-id="1808a-163">When run without any additional parameters, [Update-Module][] attempts to update all modules installed by running [Install-Module][].</span></span> <span data-ttu-id="1808a-164">Szelektív-modulok frissítése, adja hozzá a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1808a-164">To selectively update modules, add the `-Name` parameter.</span></span> 

<span data-ttu-id="1808a-165">Ehhez hasonlóan további paraméterek nélkül futtatásakor [frissítési parancsfájl] [-] is frissíteni próbálja az összes parancsfájl futtatásával telepített [Install-Script][].</span><span class="sxs-lookup"><span data-stu-id="1808a-165">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update all scripts installed by running [Install-Script][].</span></span> <span data-ttu-id="1808a-166">Külön-külön frissíteni a parancsfájlok, adja hozzá a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="1808a-166">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-packages-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="1808a-167">A PowerShell-galériából telepített csomagok</span><span class="sxs-lookup"><span data-stu-id="1808a-167">List packages that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="1808a-168">Ismerje meg, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule][] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1808a-168">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="1808a-169">Ez a parancs felsorolja az összes van a rendszeren telepített, közvetlenül a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="1808a-169">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="1808a-170">Hasonlóképpen, a PowerShell-galériából telepített parancsfájlok, futtassa a [Get-InstalledScript][] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1808a-170">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="1808a-171">Ez a parancs megjeleníti a parancsfájlokat a rendszeren telepített, közvetlenül a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="1808a-171">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-Module]: /powershell/module/powershellget/Find-Module
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-Module]: /powershell/module/powershellget/Install-Module
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[Save-Module]: /powershell/module/powershellget/Save-Module
[Save-Script]: /powershell/module/powershellget/Save-Script
