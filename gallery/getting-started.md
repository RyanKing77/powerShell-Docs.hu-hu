---
ms.date: 06/12/2017
contributor: JKeithB
keywords: katalógus, a powershell, a parancsmag, a psgallery
title: A PowerShell-galériából használatának első lépései
ms.openlocfilehash: 39998df1a2bf9363dd008dc96a802157c8d691d7
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523053"
---
# <a name="get-started-with-the-powershell-gallery"></a><span data-ttu-id="2ff8d-103">A PowerShell-galériából használatának első lépései</span><span class="sxs-lookup"><span data-stu-id="2ff8d-103">Get Started with the PowerShell Gallery</span></span>

<span data-ttu-id="2ff8d-104">A megfelelő elemeket telepíthet a PowerShell-galériából módja a parancsmagok használata a [PowerShellGet](/powershell/module/powershellget) modul.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-104">The proper way to install items from the PowerShell Gallery is to use the cmdlets in the [PowerShellGet](/powershell/module/powershellget) module.</span></span> <span data-ttu-id="2ff8d-105">Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-105">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff8d-106">Lehetséges, hogy közvetlenül a PowerShell-galériából töltse le a csomag, de ez nem ajánlott eljárás.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-106">It is possible to download a package from the PowerShell Gallery directly, but this is not a recommended approach.</span></span> <span data-ttu-id="2ff8d-107">További részletekért lásd: [manuális letöltés](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/how-to/working-with-items/manual-download.md).</span><span class="sxs-lookup"><span data-stu-id="2ff8d-107">For more details, see [Manual Package Download](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/how-to/working-with-items/manual-download.md).</span></span>  


## <a name="discovering-items-from-the-powershell-gallery"></a><span data-ttu-id="2ff8d-108">A PowerShell-galériából elemek felderítése...</span><span class="sxs-lookup"><span data-stu-id="2ff8d-108">Discovering items from the PowerShell Gallery</span></span>

<span data-ttu-id="2ff8d-109">Található elemek a PowerShell-galériából használatával a **keresési** vezérlőelem ezen a webhelyen, vagy a modulok és a parancsfájlok lapok tallózva.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-109">You can find items in the PowerShell Gallery by using the **Search** control on this website, or by browsing through the Modules and Scripts pages.</span></span> <span data-ttu-id="2ff8d-110">A PowerShell-galériából elemek futtatásával is találhatók a [Find-Module][] és [Find-Script][] parancsmagok, az elem típusa, attól függően `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-110">You can also find items from the PowerShell Gallery by running the [Find-Module][] and [Find-Script][] cmdlets, depending on the item type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="2ff8d-111">A katalógus eredményeinek szűrése hajtható végre a következő paraméterekkel:</span><span class="sxs-lookup"><span data-stu-id="2ff8d-111">Filtering results from the Gallery can be done by using the following parameters:</span></span>

- <span data-ttu-id="2ff8d-112">Név</span><span class="sxs-lookup"><span data-stu-id="2ff8d-112">Name</span></span>
- <span data-ttu-id="2ff8d-113">Allversions paramétert</span><span class="sxs-lookup"><span data-stu-id="2ff8d-113">AllVersions</span></span>
- <span data-ttu-id="2ff8d-114">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="2ff8d-114">MinimumVersion</span></span>
- <span data-ttu-id="2ff8d-115">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="2ff8d-115">RequiredVersion</span></span>
- <span data-ttu-id="2ff8d-116">Címke</span><span class="sxs-lookup"><span data-stu-id="2ff8d-116">Tag</span></span>
- <span data-ttu-id="2ff8d-117">Magában foglalja</span><span class="sxs-lookup"><span data-stu-id="2ff8d-117">Includes</span></span>
- <span data-ttu-id="2ff8d-118">DscResource</span><span class="sxs-lookup"><span data-stu-id="2ff8d-118">DscResource</span></span>
- <span data-ttu-id="2ff8d-119">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="2ff8d-119">RoleCapability</span></span>
- <span data-ttu-id="2ff8d-120">Parancs</span><span class="sxs-lookup"><span data-stu-id="2ff8d-120">Command</span></span>
- <span data-ttu-id="2ff8d-121">Szűrő</span><span class="sxs-lookup"><span data-stu-id="2ff8d-121">Filter</span></span>

<span data-ttu-id="2ff8d-122">Ha érdekli csak a katalógus adott DSC-erőforrások felderítéséhez, akkor futtathatja a [Find-DscResource] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-122">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="2ff8d-123">Find-DscResource DSC-erőforrások a katalógusban szereplő adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-123">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="2ff8d-124">DSC-erőforrások mindig érkezzenek a modul részét képező, mert továbbra is szeretné futtatni [Install-Module][] ezen DSC-erőforrások telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-124">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-items-in-the-powershell-gallery"></a><span data-ttu-id="2ff8d-125">A PowerShell-galériából elemeinek megismerése</span><span class="sxs-lookup"><span data-stu-id="2ff8d-125">Learning about items in the PowerShell Gallery</span></span>

<span data-ttu-id="2ff8d-126">Egy elem érdekli azonosítása, után érdemes többet szeretne megtudni róla.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-126">Once you've identified an item you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="2ff8d-127">Ehhez megvizsgálja az adott lapon adott elemet a katalógusban.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-127">You can do this by examining that item's specific page on the Gallery.</span></span> <span data-ttu-id="2ff8d-128">A oldalon láthatja az összes elem a hardvertokenfájlok feltöltése a metaadatok.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-128">On that page, you'll be able to see all of the metadata uploaded with the item.</span></span> <span data-ttu-id="2ff8d-129">Ezeket a metaadatokat egy elem a cikk szerzője által biztosított, és a Microsoft nem ellenőrzi.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-129">This metadata for an item is provided by the item's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="2ff8d-130">A tulajdonos elem erősen vannak kötve, a katalógus fiók tesz közzé az elemet, és több megbízható-e, mint az Author mező.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-130">The Owner of the item is strongly tied to the Gallery account used to publish the item, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="2ff8d-131">Ha úgy gondolja, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** adott elemet oldalon.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-131">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

<span data-ttu-id="2ff8d-132">Ha [Find-Module][] vagy [Find-Script][], a visszaadott PSGetModuleInfo objektumban is megtekintheti ezeket az adatokat.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-132">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="2ff8d-133">Ha például fut `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span><span class="sxs-lookup"><span data-stu-id="2ff8d-133">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`</span></span>
<span data-ttu-id="2ff8d-134">a katalógusban az PSReadLine modulban adatokat ad vissza.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-134">returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-items-from-the-powershell-gallery"></a><span data-ttu-id="2ff8d-135">PowerShell-galériából történő elemletöltés</span><span class="sxs-lookup"><span data-stu-id="2ff8d-135">Downloading items from the PowerShell Gallery</span></span>

<span data-ttu-id="2ff8d-136">Ha a PowerShell-galériából történő elemletöltés javasoljuk a következő folyamatot:</span><span class="sxs-lookup"><span data-stu-id="2ff8d-136">We encourage the following process when downloading items from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="2ff8d-137">Vizsgálja meg</span><span class="sxs-lookup"><span data-stu-id="2ff8d-137">Inspect</span></span>

<span data-ttu-id="2ff8d-138">Egy elem a katalógusból vizsgálatra letöltéséhez futtathatja az alábbiak a [Save-Module][] vagy [Save-Script][] parancsmagot, a konfigurációelem típusától függően.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-138">To download an item from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the item type.</span></span> <span data-ttu-id="2ff8d-139">Ez lehetővé teszi az elem mentése helyi telepítés nélküli, és vizsgálja meg az elem tartalma.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-139">This lets you save the item locally without installing it, and inspect the item contents.</span></span> <span data-ttu-id="2ff8d-140">Ne felejtse el kézzel törölje a mentett elemet.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-140">Remember to delete the saved item manually.</span></span>

<span data-ttu-id="2ff8d-141">Ezek az elemek egyes készült Microsoft és mások vannak a PowerShell-Közösség által készített.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-141">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="2ff8d-142">A Microsoft azt javasolja, hogy tekintse át a tartalmát, és a telepítés előtt a katalógus elemeinek kódot.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-142">Microsoft recommends that you review the contents and code of items on this gallery prior to installation.</span></span>

<span data-ttu-id="2ff8d-143">Ha úgy gondolja, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **visszaélés jelentése** adott elemet oldalon.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-143">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

### <a name="install"></a><span data-ttu-id="2ff8d-144">Telepítés</span><span class="sxs-lookup"><span data-stu-id="2ff8d-144">Install</span></span>

<span data-ttu-id="2ff8d-145">Egy elem telepíteni a galériából való használatra, futtathatja az alábbiak a [Install-Module][] vagy [Install-Script][] parancsmagot, a konfigurációelem típusától függően.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-145">To install an item from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the item type.</span></span>

<span data-ttu-id="2ff8d-146">[Install-Module][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-146">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="2ff8d-147">Ehhez rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-147">This requires an administrator account.</span></span> <span data-ttu-id="2ff8d-148">Ha a `-Scope CurrentUser` paramétert, telepítve van a modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="2ff8d-148">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="2ff8d-149">[Install-Script][] a parancsfájl telepíti `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-149">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="2ff8d-150">Ehhez rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-150">This requires an administrator account.</span></span> <span data-ttu-id="2ff8d-151">Ha a `-Scope CurrentUser` paramétert, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="2ff8d-151">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="2ff8d-152">Alapértelmezés szerint [Install-Module][] és [Install-Script][] telepíti egy elemet a legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-152">By default, [Install-Module][] and [Install-Script][] installs the most current version of an item.</span></span>
<span data-ttu-id="2ff8d-153">A cikk egy régebbi verziója hozzáadásával a `-RequiredVersion` paraméter.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-153">To install an older version of the item, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="2ff8d-154">telepítése Telepítse a</span><span class="sxs-lookup"><span data-stu-id="2ff8d-154">Deploy</span></span>

<span data-ttu-id="2ff8d-155">Egy elemet az Azure Automation PowerShell-galériából történő üzembe helyezéséhez kattintson **üzembe helyezés az Azure Automation** elem részleteit megjelenítő oldalon.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-155">To deploy an item from the PowerShell Gallery to Azure Automation, click **Deploy to Azure Automation** on the item details page.</span></span> <span data-ttu-id="2ff8d-156">Átirányítjuk az Azure felügyeleti portálon, ha bejelentkezik az Azure-fiók hitelesítő adataival.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-156">You will be redirected to the Azure Management Portal, where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="2ff8d-157">Vegye figyelembe, hogy telepítése függőségekkel rendelkező elemek telepíti a függőségeket az Azure Automationhöz.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-157">Note that deploying items with dependencies will deploy all the dependencies to Azure Automation.</span></span> <span data-ttu-id="2ff8d-158">Adja hozzá a "Üzembe helyezés az Azure Automation" gomb letiltható a **AzureAutomationNotSupported** a elemmetaadatok címkét.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-158">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your item metadata.</span></span>

<span data-ttu-id="2ff8d-159">Azure Automation kapcsolatos további információkért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-159">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-items-from-the-powershell-gallery"></a><span data-ttu-id="2ff8d-160">A PowerShell-galériából elemek frissítése</span><span class="sxs-lookup"><span data-stu-id="2ff8d-160">Updating items from the PowerShell Gallery</span></span>

<span data-ttu-id="2ff8d-161">A PowerShell-galériából származó elemek frissítéséhez futtassa a [Update-modul] [-] vagy [frissítési parancsfájl] [] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-161">To update items installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="2ff8d-162">Ha további paraméterek nélkül futtatja, [Update-modul] [-] próbál meg minden egyes futtatásával telepített modulok frissítésére, [Install-Module][].</span><span class="sxs-lookup"><span data-stu-id="2ff8d-162">When run without any additional parameters, [Update-Module][] attempts to update each module installed by running [Install-Module][].</span></span> <span data-ttu-id="2ff8d-163">Szelektív-modulok frissítése, adja hozzá a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-163">To selectively update modules, add the `-Name` parameter.</span></span>

<span data-ttu-id="2ff8d-164">Ehhez hasonlóan ha további paraméterek nélkül futtatja, [frissítési parancsfájl] [-] is frissíteni próbálja minden parancsprogram futtatásával telepített [Install-Script][].</span><span class="sxs-lookup"><span data-stu-id="2ff8d-164">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update each script installed by running [Install-Script][].</span></span> <span data-ttu-id="2ff8d-165">Külön-külön frissíteni a parancsfájlok, adja hozzá a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-165">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="2ff8d-166">A PowerShell-galériából telepített listaelemek</span><span class="sxs-lookup"><span data-stu-id="2ff8d-166">List items that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="2ff8d-167">Ismerje meg, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule][] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-167">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="2ff8d-168">Ez a parancs felsorolja az összes van a rendszeren telepített, közvetlenül a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-168">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="2ff8d-169">Hasonlóképpen, a PowerShell-galériából telepített parancsfájlok, futtassa a [Get-InstalledScript][] parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-169">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="2ff8d-170">Ez a parancs megjeleníti a parancsfájlokat a rendszeren telepített, közvetlenül a PowerShell-galériából.</span><span class="sxs-lookup"><span data-stu-id="2ff8d-170">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

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