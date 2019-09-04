---
ms.date: 09/11/2018
contributor: JKeithB
keywords: Galéria, PowerShell, psgallery
title: Csomagok manuális letöltése
ms.openlocfilehash: c0a96e866dfd27f9b2170ea540ec6dd0c67701fd
ms.sourcegitcommit: 02eed65c526ef19cf952c2129f280bb5615bf0c8
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/03/2019
ms.locfileid: "70215462"
---
# <a name="manual-package-download"></a><span data-ttu-id="1f445-103">Csomagok manuális letöltése</span><span class="sxs-lookup"><span data-stu-id="1f445-103">Manual Package Download</span></span>

<span data-ttu-id="1f445-104">A PowerShell-galéria támogatja a csomagok közvetlen letöltését a webhelyről a PowerShellGet-parancsmagok használata nélkül.</span><span class="sxs-lookup"><span data-stu-id="1f445-104">The PowerShell Gallery supports downloading a package from the website directly, without using the PowerShellGet cmdlets.</span></span> <span data-ttu-id="1f445-105">A csomagokat letöltheti NuGet Package (`.nupkg`) fájlként, amelyet aztán egy belső tárházba másolhat.</span><span class="sxs-lookup"><span data-stu-id="1f445-105">You can download any package as a NuGet package (`.nupkg`) file, which you can then copy to an internal repository.</span></span>

> [!NOTE]
> <span data-ttu-id="1f445-106">A manuális csomagok letöltése **nem** helyettesíti a `Install-Module` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="1f445-106">Manual package download is **not** intended as a replacement for the `Install-Module` cmdlet.</span></span>
> <span data-ttu-id="1f445-107">A csomag letöltése nem telepíti a modult vagy a parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="1f445-107">Downloading the package doesn't install the module or script.</span></span> <span data-ttu-id="1f445-108">A NuGet csomag nem tartalmazza a függőségeket.</span><span class="sxs-lookup"><span data-stu-id="1f445-108">Dependencies aren't included in the NuGet package downloaded.</span></span> <span data-ttu-id="1f445-109">A következő utasítások csak referenciául szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="1f445-109">The following instructions are provided for reference purposes only.</span></span>

## <a name="using-manual-download-to-acquire-a-package"></a><span data-ttu-id="1f445-110">Manuális Letöltés használata csomag beolvasásához</span><span class="sxs-lookup"><span data-stu-id="1f445-110">Using manual download to acquire a package</span></span>

<span data-ttu-id="1f445-111">Minden oldalon a manuális letöltésre mutató hivatkozás található, ahogy az itt látható:</span><span class="sxs-lookup"><span data-stu-id="1f445-111">Each page has a link for Manual Download, as shown here:</span></span>

![Manuális Letöltés](../../Images/packagedisplaypagewithpseditions.png)

<span data-ttu-id="1f445-113">A manuális letöltéshez kattintson a **RAW nupkg fájl letöltése**elemre.</span><span class="sxs-lookup"><span data-stu-id="1f445-113">To download manually, click on **Download the raw nupkg file**.</span></span> <span data-ttu-id="1f445-114">A rendszer átmásolja a csomag egy példányát a böngésző letöltési mappájába a névvel `<name>.<version>.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="1f445-114">A copy of the package is copied to the download folder for your browser with the name `<name>.<version>.nupkg`.</span></span>

<span data-ttu-id="1f445-115">A NuGet-csomag egy ZIP-archívum, amely további, a csomag tartalmával kapcsolatos információkat tartalmazó fájlokat tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="1f445-115">A NuGet package is a ZIP archive with extra files containing information about the contents of the package.</span></span> <span data-ttu-id="1f445-116">Egyes böngészők, például az Internet Explorer, automatikusan lecserélik a `.zip`fájlkiterjesztést a `.nupkg` következővel:.</span><span class="sxs-lookup"><span data-stu-id="1f445-116">Some browsers, like Internet Explorer, automatically replace the `.nupkg` file extension with `.zip`.</span></span> <span data-ttu-id="1f445-117">A csomag kibontásához nevezze át `.nupkg` a `.zip`fájlt, ha szükséges, majd bontsa ki a tartalmat egy helyi mappába.</span><span class="sxs-lookup"><span data-stu-id="1f445-117">To expand the package, rename the `.nupkg` file to `.zip`, if needed, then extract the contents to a local folder.</span></span>

<span data-ttu-id="1f445-118">A NuGet-csomagfájl a következő **NuGet-specifikus elemeket** tartalmazza, amelyek nem részei az eredeti csomagolt kódnak:</span><span class="sxs-lookup"><span data-stu-id="1f445-118">A NuGet package file includes the following **NuGet-specific elements** that aren't part of the original packaged code:</span></span>

- <span data-ttu-id="1f445-119">Egy nevű `_rels` mappa – tartalmaz egy `.rels` fájlt, amely felsorolja a függőségeket.</span><span class="sxs-lookup"><span data-stu-id="1f445-119">A folder named `_rels` - contains a `.rels` file that lists the dependencies</span></span>
- <span data-ttu-id="1f445-120">Egy nevű `package` mappa – tartalmazza a NuGet-specifikus adatkészletet.</span><span class="sxs-lookup"><span data-stu-id="1f445-120">A folder named `package` - contains the NuGet-specific data</span></span>
- <span data-ttu-id="1f445-121">Egy nevű `[Content_Types].xml` fájl – leírja, hogyan működik együtt a PowerShellGet a NuGet-mel</span><span class="sxs-lookup"><span data-stu-id="1f445-121">A file named `[Content_Types].xml` - describes how extensions like PowerShellGet work with NuGet</span></span>
- <span data-ttu-id="1f445-122">Egy nevű `<name>.nuspec` fájl – a metaadatok nagy részét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="1f445-122">A file named `<name>.nuspec` - contains the bulk of the metadata</span></span>

## <a name="installing-powershell-modules-from-a-nuget-package"></a><span data-ttu-id="1f445-123">PowerShell-modulok telepítése NuGet-csomagból</span><span class="sxs-lookup"><span data-stu-id="1f445-123">Installing PowerShell modules from a NuGet package</span></span>

> [!NOTE]
> <span data-ttu-id="1f445-124">Ezek az utasítások **nem** adják meg ugyanazt az eredményt, `Install-Module`mint a Futtatás.</span><span class="sxs-lookup"><span data-stu-id="1f445-124">These instructions **DO NOT** give the same result as running `Install-Module`.</span></span> <span data-ttu-id="1f445-125">Ezek az utasítások megfelelnek a minimális követelményeknek.</span><span class="sxs-lookup"><span data-stu-id="1f445-125">These instructions fulfill the minimum requirements.</span></span> <span data-ttu-id="1f445-126">Nem helyettesíti a következőt: `Install-Module`.</span><span class="sxs-lookup"><span data-stu-id="1f445-126">They aren't intended to be a replacement for `Install-Module`.</span></span>
> <span data-ttu-id="1f445-127">A `Install-Module` nem tartalmaz néhány lépést.</span><span class="sxs-lookup"><span data-stu-id="1f445-127">Some steps performed by `Install-Module` aren't included.</span></span>

<span data-ttu-id="1f445-128">A legegyszerűbb módszer a NuGet-specifikus elemek eltávolítása a mappából.</span><span class="sxs-lookup"><span data-stu-id="1f445-128">The easiest approach is to remove the NuGet-specific elements from the folder.</span></span> <span data-ttu-id="1f445-129">Az elemek eltávolítása elhagyja a csomag szerzője által létrehozott PowerShell-kódot.</span><span class="sxs-lookup"><span data-stu-id="1f445-129">Removing the elements leaves the PowerShell code created by the package author.</span></span>
<span data-ttu-id="1f445-130">A NuGet-specifikus elemek listáját lásd: a [manuális Letöltés használata a csomagok beolvasásához](#using-manual-download-to-acquire-a-package).</span><span class="sxs-lookup"><span data-stu-id="1f445-130">For the list of NuGet-specific elements, see [Using manual download to acquire a package](#using-manual-download-to-acquire-a-package).</span></span>

<span data-ttu-id="1f445-131">A lépések a következők:</span><span class="sxs-lookup"><span data-stu-id="1f445-131">The steps are as follows:</span></span>

1. <span data-ttu-id="1f445-132">Bontsa ki a NuGet-csomag tartalmát egy helyi mappába.</span><span class="sxs-lookup"><span data-stu-id="1f445-132">Extract the contents of the NuGet package to a local folder.</span></span>
2. <span data-ttu-id="1f445-133">Törölje a NuGet-specifikus elemeket a mappából.</span><span class="sxs-lookup"><span data-stu-id="1f445-133">Delete the NuGet-specific elements from the folder.</span></span>
3. <span data-ttu-id="1f445-134">Nevezze át a mappát.</span><span class="sxs-lookup"><span data-stu-id="1f445-134">Rename the folder.</span></span> <span data-ttu-id="1f445-135">Az alapértelmezett mappa neve általában `<name>.<version>`.</span><span class="sxs-lookup"><span data-stu-id="1f445-135">The default folder name is usually `<name>.<version>`.</span></span> <span data-ttu-id="1f445-136">A verzió tartalmazhat `-prerelease` , ha a modul előzetes verzióként van megjelölve.</span><span class="sxs-lookup"><span data-stu-id="1f445-136">The version can include `-prerelease` if the module is tagged as a prerelease version.</span></span> <span data-ttu-id="1f445-137">Nevezze át a mappát csak a modul nevére.</span><span class="sxs-lookup"><span data-stu-id="1f445-137">Rename the folder to just the module name.</span></span> <span data-ttu-id="1f445-138">Például `azurerm.storage.5.0.4-preview` a következő lesz `azurerm.storage`:.</span><span class="sxs-lookup"><span data-stu-id="1f445-138">For example, `azurerm.storage.5.0.4-preview` becomes `azurerm.storage`.</span></span>
4. <span data-ttu-id="1f445-139">Másolja a mappát az egyik mappájába `$env:PSModulePath value`.</span><span class="sxs-lookup"><span data-stu-id="1f445-139">Copy the folder to one of the folders in the `$env:PSModulePath value`.</span></span> <span data-ttu-id="1f445-140">`$env:PSModulePath`a egy pontosvesszővel tagolt készlet, amelyben a PowerShellnek a modulokat kell keresnie.</span><span class="sxs-lookup"><span data-stu-id="1f445-140">`$env:PSModulePath` is a semicolon-delimited set of paths in which PowerShell should look for modules.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f445-141">A manuális letöltés nem tartalmazza a modul által igényelt függőségeket.</span><span class="sxs-lookup"><span data-stu-id="1f445-141">The manual download doesn't include any dependencies required by the module.</span></span> <span data-ttu-id="1f445-142">Ha a csomag függőségei vannak, a modul megfelelő működéséhez telepítve kell lennie a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="1f445-142">If the package has dependencies, they must be installed on the system for this module to work correctly.</span></span> <span data-ttu-id="1f445-143">A PowerShell-galéria megjeleníti a csomag által igényelt összes függőséget.</span><span class="sxs-lookup"><span data-stu-id="1f445-143">The PowerShell Gallery shows all dependencies required by the package.</span></span>

## <a name="installing-powershell-scripts-from-a-nuget-package"></a><span data-ttu-id="1f445-144">PowerShell-parancsfájlok telepítése NuGet-csomagból</span><span class="sxs-lookup"><span data-stu-id="1f445-144">Installing PowerShell scripts from a NuGet package</span></span>

> [!NOTE]
> <span data-ttu-id="1f445-145">Ezek az utasítások **nem** adják meg ugyanazt az eredményt, `Install-Script`mint a Futtatás.</span><span class="sxs-lookup"><span data-stu-id="1f445-145">These instructions **DO NOT** give the same result as running `Install-Script`.</span></span> <span data-ttu-id="1f445-146">Ezek az utasítások megfelelnek a minimális követelményeknek.</span><span class="sxs-lookup"><span data-stu-id="1f445-146">These instructions fulfill the minimum requirements.</span></span> <span data-ttu-id="1f445-147">Nem helyettesíti a következőt: `Install-Script`.</span><span class="sxs-lookup"><span data-stu-id="1f445-147">They aren't intended to be a replacement for `Install-Script`.</span></span>

<span data-ttu-id="1f445-148">A legegyszerűbb módszer a NuGet-csomag kibontása, majd közvetlenül a szkript használata.</span><span class="sxs-lookup"><span data-stu-id="1f445-148">The easiest approach is to extract the NuGet package, then use the script directly.</span></span>

<span data-ttu-id="1f445-149">A lépések a következők:</span><span class="sxs-lookup"><span data-stu-id="1f445-149">The steps are as follows:</span></span>

1. <span data-ttu-id="1f445-150">Bontsa ki a NuGet-csomag tartalmát.</span><span class="sxs-lookup"><span data-stu-id="1f445-150">Extract the contents of the NuGet package.</span></span>
2. <span data-ttu-id="1f445-151">A mappában található fájl közvetlenül ezen a helyen használható. `.PS1`</span><span class="sxs-lookup"><span data-stu-id="1f445-151">The `.PS1` file in the folder can be used directly from this location.</span></span>
3. <span data-ttu-id="1f445-152">A mappában lévő NuGet-specifikus elemeket is törölheti.</span><span class="sxs-lookup"><span data-stu-id="1f445-152">You may delete the NuGet-specific elements in the folder.</span></span>

<span data-ttu-id="1f445-153">A NuGet-specifikus elemek listáját lásd: a [manuális Letöltés használata a csomagok beolvasásához](#using-manual-download-to-acquire-a-package).</span><span class="sxs-lookup"><span data-stu-id="1f445-153">For the list of NuGet-specific elements, see [Using manual download to acquire a package](#using-manual-download-to-acquire-a-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f445-154">A manuális letöltés nem tartalmazza a modul által igényelt függőségeket.</span><span class="sxs-lookup"><span data-stu-id="1f445-154">The manual download doesn't include any dependencies required by the module.</span></span> <span data-ttu-id="1f445-155">Ha a csomag függőségei vannak, a modul megfelelő működéséhez telepítve kell lennie a rendszeren.</span><span class="sxs-lookup"><span data-stu-id="1f445-155">If the package has dependencies, they must be installed on the system for this module to work correctly.</span></span> <span data-ttu-id="1f445-156">A PowerShell-galéria megjeleníti a csomag által igényelt összes függőséget.</span><span class="sxs-lookup"><span data-stu-id="1f445-156">The PowerShell Gallery shows all dependencies required by the package.</span></span>
