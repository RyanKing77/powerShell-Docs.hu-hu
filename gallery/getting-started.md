---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gyűjtemény, a powershell, a parancsmag, a psgallery
title: Ismerkedjen meg a PowerShell-galériában
ms.openlocfilehash: 83974698152e75efac66ea725a9c220486676d6f
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190162"
---
# <a name="get-started-with-the-powershell-gallery"></a><span data-ttu-id="3d6db-103">Ismerkedjen meg a PowerShell-galériában</span><span class="sxs-lookup"><span data-stu-id="3d6db-103">Get Started with the PowerShell Gallery</span></span>

<span data-ttu-id="3d6db-104">Elemek letöltése a PowerShell-galériából a rendszerre van szükség a [PowerShellGet](/powershell/module/powershellget) modul.</span><span class="sxs-lookup"><span data-stu-id="3d6db-104">Downloading items from the PowerShell Gallery to your system requires the [PowerShellGet](/powershell/module/powershellget) module.</span></span> <span data-ttu-id="3d6db-105">A PowerShellGet modul megtalálható a következők bármelyike lehet.</span><span class="sxs-lookup"><span data-stu-id="3d6db-105">You can find the PowerShellGet module in any of the following.</span></span> <span data-ttu-id="3d6db-106">Jelentkezzen be a PowerShell-galériából töltse le a cikkek nem kell.</span><span class="sxs-lookup"><span data-stu-id="3d6db-106">You do not need to sign in to download items from the PowerShell Gallery.</span></span>

## <a name="discovering-items-from-the-powershell-gallery"></a><span data-ttu-id="3d6db-107">A PowerShell-galériából elemek felfedezése</span><span class="sxs-lookup"><span data-stu-id="3d6db-107">Discovering items from the PowerShell Gallery</span></span>

<span data-ttu-id="3d6db-108">Az elemek találhatók a PowerShell-galériában használatával a **keresési** ezen a webhelyen, vagy keresse meg a modulok és a parancsfájlok lap vezérlőelem.</span><span class="sxs-lookup"><span data-stu-id="3d6db-108">You can find items in the PowerShell Gallery by using the **Search** control on this website, or by browsing through the Modules and Scripts pages.</span></span> <span data-ttu-id="3d6db-109">A PowerShell-galériából elemek futtatásával is találhatók a [keresés-modul][] és [keresés-parancsfájl][] elemtípus, attól függően, a parancsmagok `-Repository PSGallery`.</span><span class="sxs-lookup"><span data-stu-id="3d6db-109">You can also find items from the PowerShell Gallery by running the [Find-Module][] and [Find-Script][] cmdlets, depending on the item type, with `-Repository PSGallery`.</span></span>

<span data-ttu-id="3d6db-110">A gyűjteményből eredmények szűréséhez hajtható végre a következő paraméterekkel:</span><span class="sxs-lookup"><span data-stu-id="3d6db-110">Filtering results from the Gallery can be done by using the following parameters:</span></span>

- <span data-ttu-id="3d6db-111">Név</span><span class="sxs-lookup"><span data-stu-id="3d6db-111">Name</span></span>
- <span data-ttu-id="3d6db-112">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3d6db-112">AllVersions</span></span>
- <span data-ttu-id="3d6db-113">MinimumVersion</span><span class="sxs-lookup"><span data-stu-id="3d6db-113">MinimumVersion</span></span>
- <span data-ttu-id="3d6db-114">RequiredVersion</span><span class="sxs-lookup"><span data-stu-id="3d6db-114">RequiredVersion</span></span>
- <span data-ttu-id="3d6db-115">Címke</span><span class="sxs-lookup"><span data-stu-id="3d6db-115">Tag</span></span>
- <span data-ttu-id="3d6db-116">Magában foglalja</span><span class="sxs-lookup"><span data-stu-id="3d6db-116">Includes</span></span>
- <span data-ttu-id="3d6db-117">DscResource</span><span class="sxs-lookup"><span data-stu-id="3d6db-117">DscResource</span></span>
- <span data-ttu-id="3d6db-118">RoleCapability</span><span class="sxs-lookup"><span data-stu-id="3d6db-118">RoleCapability</span></span>
- <span data-ttu-id="3d6db-119">Parancs</span><span class="sxs-lookup"><span data-stu-id="3d6db-119">Command</span></span>
- <span data-ttu-id="3d6db-120">Szűrő</span><span class="sxs-lookup"><span data-stu-id="3d6db-120">Filter</span></span>

<span data-ttu-id="3d6db-121">Ha csak kíváncsiak vagyunk a katalógusban adott DSC-erőforrások felderítéséhez, futtathatja a [keresés-DscResource] parancsmag.</span><span class="sxs-lookup"><span data-stu-id="3d6db-121">If you're only interested in discovering specific DSC resources in the Gallery, you can run the [Find-DscResource] cmdlet.</span></span> <span data-ttu-id="3d6db-122">Keresés – DscResource a gyűjteményben található DSC erőforrást adatait jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="3d6db-122">Find-DscResource returns data on DSC resources contained in the Gallery.</span></span>
<span data-ttu-id="3d6db-123">A DSC-erőforrások mindig érkeznek modul részeként, mert továbbra is szeretné futtatni [Install-modul][] ezen DSC-erőforrások telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="3d6db-123">Because DSC resources are always delivered as part of a module, you still need to run [Install-Module][] to install those DSC resources.</span></span>

## <a name="learning-about-items-in-the-powershell-gallery"></a><span data-ttu-id="3d6db-124">A PowerShell-galériában elemeinek megismerése</span><span class="sxs-lookup"><span data-stu-id="3d6db-124">Learning about items in the PowerShell Gallery</span></span>

<span data-ttu-id="3d6db-125">Ha érdekli a cikk állapította meg, érdemes lehet további információ.</span><span class="sxs-lookup"><span data-stu-id="3d6db-125">Once you've identified an item you're interested in, you may want to learn more about it.</span></span> <span data-ttu-id="3d6db-126">Ehhez úgy, hogy az elem adott oldalon, a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="3d6db-126">You can do this by examining that item's specific page on the Gallery.</span></span> <span data-ttu-id="3d6db-127">Adott oldalon, képes lesz látható az összes, a metaadatok feltöltése a cikkhez.</span><span class="sxs-lookup"><span data-stu-id="3d6db-127">On that page, you'll be able to see all of the metadata uploaded with the item.</span></span> <span data-ttu-id="3d6db-128">Ezeket a metaadatokat egy elem az elem szerzői szolgáltatja, és nem ellenőrzi a Microsoft által.</span><span class="sxs-lookup"><span data-stu-id="3d6db-128">This metadata for an item is provided by the item's author, and is not verified by Microsoft.</span></span> <span data-ttu-id="3d6db-129">A tulajdonos elem a cikk közzétételéhez használt gyűjtemény fiók erősen kötődik, és több megbízható, mint az Author mező.</span><span class="sxs-lookup"><span data-stu-id="3d6db-129">The Owner of the item is strongly tied to the Gallery account used to publish the item, and is more trustworthy than the Author field.</span></span>

<span data-ttu-id="3d6db-130">Ha úgy érzi, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **jelentés visszaélés** , hogy az elem oldalon.</span><span class="sxs-lookup"><span data-stu-id="3d6db-130">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

<span data-ttu-id="3d6db-131">Ha fut [keresés-modul][] vagy [keresés-parancsfájl][], a visszaadott PSGetModuleInfo objektumot meg tudja tekinteni ezeket az adatokat.</span><span class="sxs-lookup"><span data-stu-id="3d6db-131">If you're running [Find-Module][] or [Find-Script][], you can view this data in the returned PSGetModuleInfo object.</span></span> <span data-ttu-id="3d6db-132">Ahhoz például, `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member` adatait jeleníti meg a PSReadLine modul a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="3d6db-132">For example, running `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member` returns data on the PSReadLine module in the Gallery.</span></span>

## <a name="downloading-items-from-the-powershell-gallery"></a><span data-ttu-id="3d6db-133">Elemek letöltése a PowerShell-galériából</span><span class="sxs-lookup"><span data-stu-id="3d6db-133">Downloading items from the PowerShell Gallery</span></span>

<span data-ttu-id="3d6db-134">Ha elemek letöltése a PowerShell-galériából javasoljuk a következő folyamat:</span><span class="sxs-lookup"><span data-stu-id="3d6db-134">We encourage the following process when downloading items from the PowerShell Gallery:</span></span>

### <a name="inspect"></a><span data-ttu-id="3d6db-135">Vizsgálja meg</span><span class="sxs-lookup"><span data-stu-id="3d6db-135">Inspect</span></span>

<span data-ttu-id="3d6db-136">Egy elemet a gyűjteményből, a vizsgálathoz letöltéséhez futtassa vagy a [mentés-modul][] vagy [mentés-parancsfájl][] parancsmag, attól függően, hogy az elem típusa.</span><span class="sxs-lookup"><span data-stu-id="3d6db-136">To download an item from the Gallery for inspection, run either the [Save-Module][] or [Save-Script][] cmdlet, depending on the item type.</span></span> <span data-ttu-id="3d6db-137">Ez lehetővé teszi a helyileg menteni az elemet a telepítés nélküli, és vizsgálja meg a cikk tartalma.</span><span class="sxs-lookup"><span data-stu-id="3d6db-137">This lets you save the item locally without installing it, and inspect the item contents.</span></span> <span data-ttu-id="3d6db-138">Ne felejtse el kézzel törölje a mentett elemet.</span><span class="sxs-lookup"><span data-stu-id="3d6db-138">Remember to delete the saved item manually.</span></span>

<span data-ttu-id="3d6db-139">Ezek az elemek egy része felhasználók a Microsoft által készített, és más felhasználók által a PowerShell közösségi készített.</span><span class="sxs-lookup"><span data-stu-id="3d6db-139">Some of these items are authored by Microsoft, and others are authored by the PowerShell community.</span></span>
<span data-ttu-id="3d6db-140">A Microsoft azt javasolja, hogy tekintse át a tartalom és a kód elemeknek a telepítés előtti tár.</span><span class="sxs-lookup"><span data-stu-id="3d6db-140">Microsoft recommends that you review the contents and code of items on this gallery prior to installation.</span></span>

<span data-ttu-id="3d6db-141">Ha úgy érzi, hogy egy elem nincs közzétéve jóhiszeműen, kattintson a **jelentés visszaélés** , hogy az elem oldalon.</span><span class="sxs-lookup"><span data-stu-id="3d6db-141">If you discover an item that you feel is not published in good faith, click **Report Abuse** on that item's page.</span></span>

### <a name="install"></a><span data-ttu-id="3d6db-142">Telepítés</span><span class="sxs-lookup"><span data-stu-id="3d6db-142">Install</span></span>

<span data-ttu-id="3d6db-143">Egy elem a katalógusból való használatra telepítéséhez futtassa vagy a [Install-modul][] vagy [telepítési-parancsfájl][] parancsmag, attól függően, hogy az elem típusa.</span><span class="sxs-lookup"><span data-stu-id="3d6db-143">To install an item from the Gallery for use, run either the [Install-Module][] or [Install-Script][] cmdlet, depending on the item type.</span></span>

<span data-ttu-id="3d6db-144">[Install-modul][] telepíti a modult `$env:ProgramFiles\WindowsPowerShell\Modules` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="3d6db-144">[Install-Module][] installs the module to `$env:ProgramFiles\WindowsPowerShell\Modules` by default.</span></span>
<span data-ttu-id="3d6db-145">Ehhez szükséges, hogy rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="3d6db-145">This requires an administrator account.</span></span> <span data-ttu-id="3d6db-146">Ha ad hozzá a `-Scope CurrentUser` paraméter, a modul telepítve van a `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span><span class="sxs-lookup"><span data-stu-id="3d6db-146">If you add the `-Scope CurrentUser` parameter, the module is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .</span></span>

<span data-ttu-id="3d6db-147">[telepítési-parancsfájl][] telepíti a parancsfájlt, amellyel `$env:ProgramFiles\WindowsPowerShell\Scripts` alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="3d6db-147">[Install-Script][] installs the script to `$env:ProgramFiles\WindowsPowerShell\Scripts` by default.</span></span>
<span data-ttu-id="3d6db-148">Ehhez szükséges, hogy rendszergazdai fiókkal.</span><span class="sxs-lookup"><span data-stu-id="3d6db-148">This requires an administrator account.</span></span> <span data-ttu-id="3d6db-149">Ha ad hozzá a `-Scope CurrentUser` paraméter, telepítve van a parancsfájl `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span><span class="sxs-lookup"><span data-stu-id="3d6db-149">If you add the `-Scope CurrentUser` parameter, the script is installed to `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .</span></span>

<span data-ttu-id="3d6db-150">Alapértelmezés szerint [Install-modul][] és [telepítési-parancsfájl][] elem legfrissebb verzióját telepíti.</span><span class="sxs-lookup"><span data-stu-id="3d6db-150">By default, [Install-Module][] and [Install-Script][] installs the most current version of an item.</span></span>
<span data-ttu-id="3d6db-151">A cikk korábbi verziója telepítéséhez adja hozzá a `-RequiredVersion` paraméter.</span><span class="sxs-lookup"><span data-stu-id="3d6db-151">To install an older version of the item, add the `-RequiredVersion` parameter.</span></span>

### <a name="deploy"></a><span data-ttu-id="3d6db-152">telepítése Telepítse a</span><span class="sxs-lookup"><span data-stu-id="3d6db-152">Deploy</span></span>

<span data-ttu-id="3d6db-153">Azure Automation a PowerShell-galériából elemet telepítéséhez kattintson **központi telepítése az Azure Automation** elem részleteit megjelenítő oldalon.</span><span class="sxs-lookup"><span data-stu-id="3d6db-153">To deploy an item from the PowerShell Gallery to Azure Automation, click **Deploy to Azure Automation** on the item details page.</span></span> <span data-ttu-id="3d6db-154">Az Azure felügyeleti portálra, ahol regisztrál Azure-fiók hitelesítő adataival irányítja.</span><span class="sxs-lookup"><span data-stu-id="3d6db-154">You will be redirected to the Azure Management Portal, where you sign in by using your Azure account credentials.</span></span> <span data-ttu-id="3d6db-155">Vegye figyelembe, hogy függőségekkel rendelkező elemek telepítését helyezik üzembe a függőségek az Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="3d6db-155">Note that deploying items with dependencies will deploy all the dependencies to Azure Automation.</span></span> <span data-ttu-id="3d6db-156">A "Központi telepítése az Azure Automation" gomb letiltható hozzáadásával a **AzureAutomationNotSupported** címkén belül, hogy a konfigurációelem-metaadatok.</span><span class="sxs-lookup"><span data-stu-id="3d6db-156">The 'Deploy to Azure Automation' button can be disabled by adding the **AzureAutomationNotSupported** tag to your item metadata.</span></span>

<span data-ttu-id="3d6db-157">Azure Automation kapcsolatos további tudnivalókért tekintse meg a [Azure Automation](/azure/automation) dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="3d6db-157">To learn more about Azure Automation, see the [Azure Automation](/azure/automation) documentation.</span></span>

## <a name="updating-items-from-the-powershell-gallery"></a><span data-ttu-id="3d6db-158">A PowerShell-galériából elemek frissítése</span><span class="sxs-lookup"><span data-stu-id="3d6db-158">Updating items from the PowerShell Gallery</span></span>

<span data-ttu-id="3d6db-159">Elemek telepítve a PowerShell-galériából frissítéséhez futtassa a [frissítés-modul] [-] vagy az [Update-parancsfájl] [] parancsmag.</span><span class="sxs-lookup"><span data-stu-id="3d6db-159">To update items installed from the PowerShell Gallery, run either the [Update-Module][] or [Update-Script][] cmdlet.</span></span> <span data-ttu-id="3d6db-160">További paraméterek nélküli futtatásakor [frissítés-modul] [-] minden egyes futtatásával telepített modulokban frissíteni próbálja [Install-modul][].</span><span class="sxs-lookup"><span data-stu-id="3d6db-160">When run without any additional parameters, [Update-Module][] attempts to update each module installed by running [Install-Module][].</span></span> <span data-ttu-id="3d6db-161">Modulok szelektív frissítéséhez vegye fel a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="3d6db-161">To selectively update modules, add the `-Name` parameter.</span></span>

<span data-ttu-id="3d6db-162">Hasonlóképpen, további paraméterek nélküli futtatásakor [parancsfájl-frissítés] [-] is frissíteni próbálja minden parancsfájl futtatásával telepítve [telepítési-parancsfájl][].</span><span class="sxs-lookup"><span data-stu-id="3d6db-162">Similarly, when run without any additional parameters, [Update-Script][] also attempts to update each script installed by running [Install-Script][].</span></span> <span data-ttu-id="3d6db-163">Parancsfájlok szelektív frissítéséhez vegye fel a `-Name` paraméter.</span><span class="sxs-lookup"><span data-stu-id="3d6db-163">To selectively update scripts, add the `-Name` parameter.</span></span>

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a><span data-ttu-id="3d6db-164">A PowerShell-galériából telepített listaelemek</span><span class="sxs-lookup"><span data-stu-id="3d6db-164">List items that you have installed from the PowerShell Gallery</span></span>

<span data-ttu-id="3d6db-165">Szeretné tudni, melyik modulokat a PowerShell-galériából telepítette, futtassa a [Get-InstalledModule][] parancsmag.</span><span class="sxs-lookup"><span data-stu-id="3d6db-165">To find out which modules you have installed from the PowerShell Gallery, run the [Get-InstalledModule][] cmdlet.</span></span> <span data-ttu-id="3d6db-166">Ez a parancs megjeleníti a modulok, a rendszeren, hogy közvetlenül a PowerShell-galériából telepített.</span><span class="sxs-lookup"><span data-stu-id="3d6db-166">This command lists all of the modules you have on your system that were installed directly from the PowerShell Gallery.</span></span>

<span data-ttu-id="3d6db-167">Hasonlóképpen, a PowerShell-galériából telepítése parancsfájlok tudni, futtassa a [Get-InstalledScript][] parancsmag.</span><span class="sxs-lookup"><span data-stu-id="3d6db-167">Similarly, to find out which scripts you have installed from the PowerShell Gallery, run the [Get-InstalledScript][] cmdlet.</span></span> <span data-ttu-id="3d6db-168">Ez a parancs felsorolja az összes parancsfájlját a rendszeren, hogy közvetlenül a PowerShell-galériából telepített.</span><span class="sxs-lookup"><span data-stu-id="3d6db-168">This command lists all of the scripts you have on your system that were installed directly from the PowerShell Gallery.</span></span>

[keresés-DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[keresés-modul]: /powershell/module/powershellget/Find-Module
[Find-Module]: /powershell/module/powershellget/Find-Module
[keresés-parancsfájl]: /powershell/module/powershellget/Find-Script
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-modul]: /powershell/module/powershellget/Install-Module
[Install-Module]: /powershell/module/powershellget/Install-Module
[telepítési-parancsfájl]: /powershell/module/powershellget/Install-Script
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[mentés-modul]: /powershell/module/powershellget/Save-Module
[Save-Module]: /powershell/module/powershellget/Save-Module
[mentés-parancsfájl]: /powershell/module/powershellget/Save-Script
[Save-Script]: /powershell/module/powershellget/Save-Script