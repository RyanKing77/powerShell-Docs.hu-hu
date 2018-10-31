---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: A PowerShell-galériából használatának első lépései
ms.openlocfilehash: 85b0a754aba25d850dc918024419318554f92b33
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225675"
---
# <a name="getting-started-with-the-powershell-gallery"></a><span data-ttu-id="a216e-103">A PowerShell-galériából – első lépések</span><span class="sxs-lookup"><span data-stu-id="a216e-103">Getting Started with the PowerShell Gallery</span></span>

<span data-ttu-id="a216e-104">A megfelelő lehetőség a csomagok telepítéséhez a PowerShell-galériából, hogy a parancsmagok használata a [PowerShellGet](/powershell/module/powershellget) modul.</span><span class="sxs-lookup"><span data-stu-id="a216e-104">The proper way to install packages from the PowerShell Gallery is to use the cmdlets in the [PowerShellGet](/powershell/module/powershellget) module.</span></span> <span data-ttu-id="a216e-105">Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.</span><span class="sxs-lookup"><span data-stu-id="a216e-105">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="a216e-106">Lehetséges, hogy közvetlenül a PowerShell-galériából töltse le a csomag, de ez nem ajánlott eljárás.</span><span class="sxs-lookup"><span data-stu-id="a216e-106">It is possible to download a package from the PowerShell Gallery directly, but this is not a recommended approach.</span></span>
> <span data-ttu-id="a216e-107">További részletekért lásd: [manuális letöltés](/powershell/gallery/how-to/working-with-packages/manual-download).</span><span class="sxs-lookup"><span data-stu-id="a216e-107">For more details, see [Manual Package Download](/powershell/gallery/how-to/working-with-packages/manual-download).</span></span>

## <a name="discovering-packages-from-the-powershell-gallery"></a><span data-ttu-id="a216e-108">A PowerShell-galériából csomagok felderítése</span><span class="sxs-lookup"><span data-stu-id="a216e-108">Discovering packages from the PowerShell Gallery</span></span>

<span data-ttu-id="a216e-109">Található csomagokat a PowerShell-galériából használatával a **keresési** vezérlőelem ezen a webhelyen, vagy a modulok és a parancsfájlok lapok tallózva.</span><span class="sxs-lookup"><span data-stu-id="a216e-109">You can find packages in the PowerShell Gallery by using the **Search** control on this website, or by browsing through the Modules and Scripts pages.</span></span> <span data-ttu-id="a216e-110">A PowerShell-galériából csomagok futtatásával is talál a [Find-Module][] és [Find-Script][] parancsmagok, az elem típusa, attól függően `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="a216e-110">You can also find packages from the PowerShell Gallery by running the [Find-Module][] and [Find-Script][] cmdlets, depending on the item type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="a216e-111">A katalógus eredményeinek szűrése hajtható végre a következő paraméterekkel:</span><span class="sxs-lookup"><span data-stu-id="a216e-111">Filtering results from the Gallery can be done by using the following parameters:</span></span>

- <span data-ttu-id="a216e-112">Név</span><span class="sxs-lookup"><span data-stu-id="a216e-112">Name</span></span>
- <span data-ttu-id="a216e-113">Allversions paramétert</span><span class="sxs-lookup"><span data-stu-id="a216e-113">AllVersions</span></span>
- <span data-ttu-id="a216e-114">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="a216e-114">MinimumVersion</span></span>
- <span data-ttu-id="a216e-115">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="a216e-115">RequiredVersion</span></span>
- <span data-ttu-id="a216e-116">Címke</span><span class="sxs-lookup"><span data-stu-id="a216e-116">Tag</span></span>
- <span data-ttu-id="a216e-117">Magában foglalja</span><span class="sxs-lookup"><span data-stu-id="a216e-117">Includes</span></span>
- <span data-ttu-id="a216e-118">DscResource</span><span class="sxs-lookup"><span data-stu-id="a216e-118">DscResource</span></span>
- <span data-ttu-id="a216e-119">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="a216e-119">RoleCapability</span></span>
- <span data-ttu-id="a216e-120">Parancs</span><span class="sxs-lookup"><span data-stu-id="a216e-120">Command</span></span>
- <span data-ttu-id="a216e-121">Szűrő</span><span class="sxs-lookup"><span data-stu-id="a216e-121">Filter</span></span>

<span data-ttu-id="a216e-122">Ha érdekli csak a katalógus adott DSC-erőforrások felderítéséhez, akkor futtathatja a [Find-DscResource] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a216e-122">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="a216e-123">Find-DscResource DSC-erőforrások a katalógusban szereplő adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a216e-123">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="a216e-124">DSC-erőforrások mindig érkezzenek a modul részét képező, mert továbbra is szeretné futtatni [Install-Module][] ezen DSC-erőforrások telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="a216e-124">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-packages-in-the-powershell-gallery"></a><span data-ttu-id="a216e-125">Tudnivalók a PowerShell-galériából-csomagok</span><span class="sxs-lookup"><span data-stu-id="a216e-125">Learning about packages in the PowerShell Gallery</span></span>

<span data-ttu-id="a216e-126">Egy csomagot, amely az Önt érdeklő azonosítása, után érdemes többet szeretne megtudni róla.</span><span class="sxs-lookup"><span data-stu-id="a216e-126">Once you've identified a package that you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="a216e-127">Ehhez megvizsgálja az adott oldalra a csomag a katalógusban.</span><span class="sxs-lookup"><span data-stu-id="a216e-127">You can do this by examining that package's specific page on the Gallery.</span></span> <span data-ttu-id="a216e-128">A oldalon láthatja az összes a metaadatokat a csomag feltöltése.</span><span class="sxs-lookup"><span data-stu-id="a216e-128">On that page, you'll be able to see all of the metadata uploaded with the package.</span></span> <span data-ttu-id="a216e-129">Ezeket a metaadatokat a csomag szerzője által biztosított, és a Microsoft nem ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="a216e-129">This metadata is provided by the package's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="a216e-130">A csomag tulajdonosát erősen vannak kötve, a katalógus fiók tesz közzé a csomagot, és több megbízható-e, mint az Author mező.</span><span class="sxs-lookup"><span data-stu-id="a216e-130">The Owner of the package is strongly tied to the Gallery account used to publish the package, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="a216e-131">Ha egy csomagot, amely úgy gondolja, hogy nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** a kérdéses csomag lapon.</span><span class="sxs-lookup"><span data-stu-id="a216e-131">If you discover a package that you feel is not published in good faith, click **Report Abuse** on that package's page.</span></span>

<span data-ttu-id="a216e-132">Ha [Find-Module][] vagy [Find-Script][], a visszaadott PSGetModuleInfo objektumban is megtekintheti ezeket az adatokat.</span><span class="sxs-lookup"><span data-stu-id="a216e-132">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="a216e-133">Ha például fut `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span><span class="sxs-lookup"><span data-stu-id="a216e-133">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span></span>
<span data-ttu-id="a216e-134">a katalógusban az PSReadLine modulban adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="a216e-134">returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-packages-from-the-powershell-gallery"></a><span data-ttu-id="a216e-135">A PowerShell-galériából csomagok letöltése</span><span class="sxs-lookup"><span data-stu-id="a216e-135">Downloading packages from the PowerShell Gallery</span></span>

<span data-ttu-id="a216e-136">A PowerShell-galériából való letöltése a csomagok esetén a következőket javasoljuk:</span><span class="sxs-lookup"><span data-stu-id="a216e-136">We encourage the following process when downloading packages from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="a216e-137">Vizsgálja meg</span><span class="sxs-lookup"><span data-stu-id="a216e-137">Inspect</span></span>

<span data-ttu-id="a216e-138">A csomag letöltéséhez vizsgálatra a katalógusból, futtathatja az alábbiak a [Save-Module][] vagy [Save-Script][] parancsmagot, a csomag típusától függően.</span><span class="sxs-lookup"><span data-stu-id="a216e-138">To download a package from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the package type.</span></span> <span data-ttu-id="a216e-139">Ez lehetővé teszi a csomag mentéséhez helyi telepítés nélküli, és vizsgálja meg a csomag tartalma.</span><span class="sxs-lookup"><span data-stu-id="a216e-139">This lets you save the package locally without installing it, and inspect the package contents.</span></span> <span data-ttu-id="a216e-140">Ne felejtse el kézzel törölje a mentett csomagot.</span><span class="sxs-lookup"><span data-stu-id="a216e-140">Remember to delete the saved package manually.</span></span>

<span data-ttu-id="a216e-141">Néhány ezeket a csomagokat a Microsoft által lett létrehozva, és mások vannak a PowerShell-Közösség által készített.</span><span class="sxs-lookup"><span data-stu-id="a216e-141">Some of these packages are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="a216e-142">A Microsoft azt javasolja, hogy tekintse át a tartalmát és kódját a csomagok a katalógusban a telepítés előtt.</span><span class="sxs-lookup"><span data-stu-id="a216e-142">Microsoft recommends that you review the contents and code of packages on this gallery prior to installation.</span></span>

<span data-ttu-id="a216e-143">Ha egy csomagot, amely úgy gondolja, hogy nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** a kérdéses csomag lapon.</span><span class="sxs-lookup"><span data-stu-id="a216e-143">If you discover a package that you feel is not published in good faith, click **Report Abuse** on that package's page.</span></span>

### <a name="install"></a><span data-ttu-id="a216e-144">Telepítés</span><span class="sxs-lookup"><span data-stu-id="a216e-144">Install</span></span>

<span data-ttu-id="a216e-145">A csomag telepítéséhez használható a katalógusból, futtathatja az alábbiak a [Install-Module][] vagy [Install-Script][] parancsmagot, a csomag típusától függően.</span><span class="sxs-lookup"><span data-stu-id="a216e-145">To install a package from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the package type.</span></span>

<span data-ttu-id="a216e-146">[Install-Module][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="a216e-146">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="a216e-147">Ehhez rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="a216e-147">This requires an administrator account.</span></span> <span data-ttu-id="a216e-148">Ha a `-Scope CurrentUser` paramétert, telepítve van a modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="a216e-148">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="a216e-149">[Install-Script][] a parancsfájl telepíti `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="a216e-149">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="a216e-150">Ehhez rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="a216e-150">This requires an administrator account.</span></span> <span data-ttu-id="a216e-151">Ha a `-Scope CurrentUser` paramétert, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="a216e-151">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="a216e-152">Alapértelmezés szerint [Install-Module][] és [Install-Script][] telepíti egy csomagot a legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="a216e-152">By default, [Install-Module][] and [Install-Script][] installs the most current version of a package.</span></span>
<span data-ttu-id="a216e-153">Egy régebbi verzióját a csomag telepítéséhez, adja hozzá a `-RequiredVersion` paraméter.</span><span class="sxs-lookup"><span data-stu-id="a216e-153">To install an older version of the package, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="a216e-154">telepítése Telepítse a</span><span class="sxs-lookup"><span data-stu-id="a216e-154">Deploy</span></span>

<span data-ttu-id="a216e-155">Egy csomag az Azure Automation PowerShell-galériából történő üzembe helyezéséhez kattintson **üzembe helyezés az Azure Automation** csomag részleteit megjelenítő oldalon.</span><span class="sxs-lookup"><span data-stu-id="a216e-155">To deploy a package from the PowerShell Gallery to Azure Automation, click **Deploy to Azure Automation** on the package details page.</span></span> <span data-ttu-id="a216e-156">Átirányítjuk az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiók hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="a216e-156">You will be redirected to the Azure Management Portal where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="a216e-157">Vegye figyelembe, hogy függőségekkel rendelkező csomagok telepítése telepíti a függőségeket az Azure Automationhöz.</span><span class="sxs-lookup"><span data-stu-id="a216e-157">Note that deploying packages with dependencies will deploy all the dependencies to Azure Automation.</span></span> <span data-ttu-id="a216e-158">Adja hozzá a "Üzembe helyezés az Azure Automation" gomb letiltható a **AzureAutomationNotSupported** a csomag metaadata címkét.</span><span class="sxs-lookup"><span data-stu-id="a216e-158">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your package metadata.</span></span>

<span data-ttu-id="a216e-159">Azure Automation kapcsolatos további információkért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="a216e-159">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-packages-from-the-powershell-gallery"></a><span data-ttu-id="a216e-160">A PowerShell-galériából csomagok frissítése</span><span class="sxs-lookup"><span data-stu-id="a216e-160">Updating packages from the PowerShell Gallery</span></span>

<span data-ttu-id="a216e-161">A PowerShell-galériából telepített csomagok frissítéséhez futtassa a [Update-modul] [-] vagy [frissítési parancsfájl] [] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a216e-161">To update packages installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="a216e-162">Ha további paraméterek nélkül futtatja, [Update-modul] [-] próbál meg minden egyes futtatásával telepített modulok frissítésére, [Install-Module][].</span><span class="sxs-lookup"><span data-stu-id="a216e-162">When run without any additional parameters, [Update-Module][] attempts to update each module installed by running [Install-Module][].</span></span> <span data-ttu-id="a216e-163">Szelektív-modulok frissítése, adja hozzá a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="a216e-163">To selectively update modules, add the `-Name` parameter.</span></span>

<span data-ttu-id="a216e-164">Ehhez hasonlóan ha további paraméterek nélkül futtatja, [frissítési parancsfájl] [-] is frissíteni próbálja minden parancsprogram futtatásával telepített [Install-Script][].</span><span class="sxs-lookup"><span data-stu-id="a216e-164">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update each script installed by running [Install-Script][].</span></span> <span data-ttu-id="a216e-165">Külön-külön frissíteni a parancsfájlok, adja hozzá a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="a216e-165">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-packages-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="a216e-166">A PowerShell-galériából telepített csomagok</span><span class="sxs-lookup"><span data-stu-id="a216e-166">List packages that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="a216e-167">Ismerje meg, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule][] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a216e-167">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="a216e-168">Ez a parancs felsorolja az összes van a rendszeren telepített, közvetlenül a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="a216e-168">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="a216e-169">Hasonlóképpen, a PowerShell-galériából telepített parancsfájlok, futtassa a [Get-InstalledScript][] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="a216e-169">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="a216e-170">Ez a parancs megjeleníti a parancsfájlokat a rendszeren telepített, közvetlenül a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="a216e-170">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

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
