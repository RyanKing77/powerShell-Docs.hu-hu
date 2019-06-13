---
ms.date: 08/27/2018
keywords: PowerShell, a parancsmag
title: Részletes súgóinformációk kérése
ms.openlocfilehash: 3f52de8c9963618c154b119d5f4859a92d61fbda
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030399"
---
# <a name="getting-detailed-help-information"></a><span data-ttu-id="6e189-103">Részletes súgóinformációk kérése</span><span class="sxs-lookup"><span data-stu-id="6e189-103">Getting detailed help information</span></span>

<span data-ttu-id="6e189-104">PowerShell, amelyek bemutatják a PowerShell alapfogalmai és a PowerShell nyelv részletes cikkeket tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="6e189-104">PowerShell includes detailed Help articles that explain PowerShell concepts and the PowerShell language.</span></span> <span data-ttu-id="6e189-105">Is találhatók Súgócikkek minden parancsmag és a szolgáltató, és számos függvények és parancsfájlok.</span><span class="sxs-lookup"><span data-stu-id="6e189-105">There are also Help articles for each cmdlet and provider and for many functions and scripts.</span></span>

<span data-ttu-id="6e189-106">Ezek Súgócikkek jeleníthetők meg a parancssort vagy a legutóbb frissített verzióit a következő cikkeket megtekintése a [PowerShell](/powershell/scripting/overview) online dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="6e189-106">You can display these Help articles at the command prompt or view the most recently updated versions of these articles in the [PowerShell](/powershell/scripting/overview) documentation online.</span></span>

## <a name="getting-help-for-cmdlets"></a><span data-ttu-id="6e189-107">Súgó a parancsmagokhoz</span><span class="sxs-lookup"><span data-stu-id="6e189-107">Getting help for cmdlets</span></span>

<span data-ttu-id="6e189-108">PowerShell-parancsmagokkal kapcsolatos súgó lekéréséhez használja a [Get-Help](/powershell/module/microsoft.powershell.core/Get-Help) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6e189-108">To get Help about PowerShell cmdlets, use the [Get-Help](/powershell/module/microsoft.powershell.core/Get-Help) cmdlet.</span></span> <span data-ttu-id="6e189-109">Segítség kérése az a példában a `Get-ChildItem` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-109">For example, to get Help for the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem
```

<span data-ttu-id="6e189-110">vagy a</span><span class="sxs-lookup"><span data-stu-id="6e189-110">or</span></span>

```powershell
Get-ChildItem -?
```

<span data-ttu-id="6e189-111">A Get-Help parancsmag kapcsolatos még is kaphat segítséget.</span><span class="sxs-lookup"><span data-stu-id="6e189-111">You can even get Help about the Get-Help cmdlet.</span></span> <span data-ttu-id="6e189-112">Például:</span><span class="sxs-lookup"><span data-stu-id="6e189-112">For example:</span></span>

```powershell
Get-Help Get-Help
```

<span data-ttu-id="6e189-113">Súgócikkek az összes parancsmag listájának lekérése a munkamenetben, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-113">To get a list of all the cmdlet Help articles in your session, type:</span></span>

```powershell
Get-Help -Category Cmdlet
```

<span data-ttu-id="6e189-114">Egyszerre csak egy oldal egyes súgócikk megjelenítéséhez használja a `help` függvény vagy az aliasával `man`.</span><span class="sxs-lookup"><span data-stu-id="6e189-114">To display one page of each Help article at a time, use the `help` function or its alias `man`.</span></span>
<span data-ttu-id="6e189-115">Például Súgó megjelenítése a `Get-ChildItem` parancsmag típusa</span><span class="sxs-lookup"><span data-stu-id="6e189-115">For example, to display Help for the `Get-ChildItem` cmdlet, type</span></span>

```powershell
man Get-ChildItem
```

<span data-ttu-id="6e189-116">vagy a</span><span class="sxs-lookup"><span data-stu-id="6e189-116">or</span></span>

```powershell
help Get-ChildItem
```

<span data-ttu-id="6e189-117">Részletes információk megjelenítéséhez használja a **részletes** paraméterében a `Get-Help` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6e189-117">To display detailed information, use the **Detailed** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="6e189-118">Például részletes információkhoz juthat a `Get-ChildItem` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-118">For example, to get detailed information about the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Detailed
```

<span data-ttu-id="6e189-119">A Súgó a cikkben minden tartalom megjelenítéséhez használja a **teljes** paraméterében a `Get-Help` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6e189-119">To display all content in the Help article, use the **Full** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="6e189-120">Ha például minden tartalom megjelenítéséhez a cikk segítséget a `Get-ChildItem` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-120">For example, to display all content in the Help article for the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Full
```

<span data-ttu-id="6e189-121">Első részletes súgó használatát egy parancsmag-paraméterekkel kapcsolatos a **paraméter** paraméterében a `Get-Help` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6e189-121">To get detailed Help about the parameters of a cmdlet, use the **Parameter** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="6e189-122">Például beolvasni a részletes súgót paramétereit a `Get-ChildItem` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-122">For example, to get detailed Help for all of the parameters of the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Parameter *
```

<span data-ttu-id="6e189-123">A példákban csak a Súgó a cikkben megjelenítéséhez használja a **példák** paraméterében a `Get-Help`.</span><span class="sxs-lookup"><span data-stu-id="6e189-123">To display only the examples in a Help article, use the **Examples** parameter of the `Get-Help`.</span></span>
<span data-ttu-id="6e189-124">Ha például csak a példák megjelenítése a Súgó cikk a `Get-ChildItem` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-124">For example, to display only the examples in the Help article for the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Examples
```

<span data-ttu-id="6e189-125">Súgócikkek az írást parancsmagok írásával kapcsolatban további információkért lásd: [arról, hogy miként írhat parancsmag](/powershell/developer/help/writing-help-for-windows-powershell-cmdlets).</span><span class="sxs-lookup"><span data-stu-id="6e189-125">For information about how to write Help articles for the cmdlets that you write, see [How to Write Cmdlet Help](/powershell/developer/help/writing-help-for-windows-powershell-cmdlets).</span></span>

## <a name="getting-conceptual-help"></a><span data-ttu-id="6e189-126">Fogalmi segítség kérése</span><span class="sxs-lookup"><span data-stu-id="6e189-126">Getting conceptual help</span></span>

<span data-ttu-id="6e189-127">A `Get-Help` parancsmag is információkat jelenít meg elméleti cikkek PowerShell-lel, beleértve a cikkeket a PowerShell nyelv tudnivalók.</span><span class="sxs-lookup"><span data-stu-id="6e189-127">The `Get-Help` cmdlet also displays information about conceptual articles in PowerShell, including articles about the PowerShell language.</span></span> <span data-ttu-id="6e189-128">Cikkek kezdje a "about_" előtaggal, például a about_line_editing fogalmi segítséget.</span><span class="sxs-lookup"><span data-stu-id="6e189-128">Conceptual Help articles begin with the "about_" prefix, such as about_line_editing.</span></span> <span data-ttu-id="6e189-129">(A fogalmi cikkeinek kell megadni angol nyelven még a PowerShell nem angol nyelvű verziója.)</span><span class="sxs-lookup"><span data-stu-id="6e189-129">(The name of the conceptual article must be entered in English even on non-English versions of PowerShell.)</span></span>

<span data-ttu-id="6e189-130">Elméleti cikkek listájának megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-130">To display a list of conceptual articles, type:</span></span>

```powershell
Get-Help about_*
```

<span data-ttu-id="6e189-131">Egy adott súgócikk megjelenítéséhez írja be például a cikk neve:</span><span class="sxs-lookup"><span data-stu-id="6e189-131">To display a particular Help article, type the article name, for example:</span></span>

```powershell
Get-Help about_command_syntax
```

<span data-ttu-id="6e189-132">A paraméterek a `Get-Help`, például **részletes**, **paraméter**, és **példák**, nem befolyásolják a fogalmi Súgócikkek megjelenítését.</span><span class="sxs-lookup"><span data-stu-id="6e189-132">The parameters of `Get-Help`, such as **Detailed**, **Parameter**, and **Examples**, have no effect on the display of conceptual Help articles.</span></span>

## <a name="getting-help-about-providers"></a><span data-ttu-id="6e189-133">Szolgáltatók kapcsolatos segítség</span><span class="sxs-lookup"><span data-stu-id="6e189-133">Getting help about providers</span></span>

<span data-ttu-id="6e189-134">A `Get-Help` parancsmag PowerShell szolgáltatók információit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="6e189-134">The `Get-Help` cmdlet displays information about PowerShell providers.</span></span> <span data-ttu-id="6e189-135">Súgó kérése egy szolgáltatót, írja be a `Get-Help` szolgáltató neve követ.</span><span class="sxs-lookup"><span data-stu-id="6e189-135">To get Help for a provider, type `Get-Help` followed by the provider name.</span></span> <span data-ttu-id="6e189-136">Például a beállításjegyzék-szolgáltatójának súgójának megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-136">For example, to get Help for the Registry provider, type:</span></span>

```powershell
Get-Help registry
```

<span data-ttu-id="6e189-137">Súgócikkek az összes szolgáltatót listájának lekérése a munkamenetben, írja be a következőt</span><span class="sxs-lookup"><span data-stu-id="6e189-137">To get a list of all the provider Help articles in your session, type</span></span>

```powershell
Get-Help -Category provider
```

<span data-ttu-id="6e189-138">A paraméterek a `Get-Help`, például **részletes**, **paraméter**, és **példák**, nem befolyásolják a szolgáltató Súgócikkek megjelenítését.</span><span class="sxs-lookup"><span data-stu-id="6e189-138">The parameters of `Get-Help`, such as **Detailed**, **Parameter**, and **Examples**, have no effect on the display of provider Help articles.</span></span>

## <a name="getting-help-about-scripts-and-functions"></a><span data-ttu-id="6e189-139">Parancsfájlokban és függvényekben kapcsolatos segítség</span><span class="sxs-lookup"><span data-stu-id="6e189-139">Getting help about scripts and functions</span></span>

<span data-ttu-id="6e189-140">Számos parancsfájlokban és függvényekben a PowerShellben kell a cikkeket.</span><span class="sxs-lookup"><span data-stu-id="6e189-140">Many scripts and functions in PowerShell have Help articles.</span></span> <span data-ttu-id="6e189-141">Használja a `Get-Help` parancsmaggal a Súgócikkek a parancsfájlokban és függvényekben.</span><span class="sxs-lookup"><span data-stu-id="6e189-141">Use the `Get-Help` cmdlet to display the Help articles for scripts and functions.</span></span>

<span data-ttu-id="6e189-142">A függvény súgójának megjelenítéséhez írja be a következőt `Get-Help` függvény neve követ.</span><span class="sxs-lookup"><span data-stu-id="6e189-142">To display the Help for a function, type `Get-Help` followed by the function name.</span></span> <span data-ttu-id="6e189-143">Segítség kérése az a példában a `Disable-PSRemoting` működik, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-143">For example, to get Help for the `Disable-PSRemoting` function, type:</span></span>

```powershell
Get-Help Disable-PSRemoting
```

<span data-ttu-id="6e189-144">A parancsfájl súgójának megjelenítéséhez írja be a parancsfájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="6e189-144">To display the Help for a script, type the path to the script file.</span></span> <span data-ttu-id="6e189-145">Ha a parancsfájl nem szerepelnek a Path környezeti változóhoz elérési út, teljes elérési útját kell használnia.</span><span class="sxs-lookup"><span data-stu-id="6e189-145">If the script is not in a path listed in the Path environment variable, you must use the fully qualified path.</span></span>

<span data-ttu-id="6e189-146">Ha például a c: "TestScript.ps1" nevű parancsfájl rendelkezik\\PS-tesztelési címtárat, megjelenítése a Súgó a cikk a parancsfájl típusa:</span><span class="sxs-lookup"><span data-stu-id="6e189-146">For example, if you have a script called "TestScript.ps1" in your C:\\PS-Test directory, to display the Help article for the script, type:</span></span>

```powershell
Get-Help c:\ps-test\TestScript.ps1
```

<span data-ttu-id="6e189-147">A paraméterek, a parancsmag súgójában működik a parancsfájl és a függvény értékek megjelenítésére lettek kialakítva segítségével túl.</span><span class="sxs-lookup"><span data-stu-id="6e189-147">The parameters that are designed for displaying cmdlet Help work for script and function Help, too.</span></span> <span data-ttu-id="6e189-148">Azonban súgó a függvények és parancsfájlok nem látható futtatásakor `Get-Help *`.</span><span class="sxs-lookup"><span data-stu-id="6e189-148">However, help for functions and scripts is not shown when you run `Get-Help *`.</span></span>

<span data-ttu-id="6e189-149">Súgócikkek a függvények és parancsfájlok írása kapcsolatos információkért tekintse meg a következő cikkeket:</span><span class="sxs-lookup"><span data-stu-id="6e189-149">For information about writing Help articles for your functions and scripts, see the following articles:</span></span>

- [<span data-ttu-id="6e189-150">about_Functions</span><span class="sxs-lookup"><span data-stu-id="6e189-150">about_Functions</span></span>](/powershell/module/microsoft.powershell.core/about/about_functions)
- [<span data-ttu-id="6e189-151">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="6e189-151">about_Scripts</span></span>](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [<span data-ttu-id="6e189-152">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="6e189-152">about_Comment_Based_Help</span></span>](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)

## <a name="getting-help-online"></a><span data-ttu-id="6e189-153">Online súgó elérése</span><span class="sxs-lookup"><span data-stu-id="6e189-153">Getting help online</span></span>

<span data-ttu-id="6e189-154">Online súgó cikkeinek az egyik legjobb módja, ha segítséget szeretne kérni.</span><span class="sxs-lookup"><span data-stu-id="6e189-154">Viewing the Help articles online is one of the best ways to get help.</span></span> <span data-ttu-id="6e189-155">Online témájú cikkei például könnyebben frissítése, és adja meg a legfrissebb tartalmakat.</span><span class="sxs-lookup"><span data-stu-id="6e189-155">Online articles are easier to update and provide the most current content.</span></span>

<span data-ttu-id="6e189-156">Online súgó lekéréséhez használja a **Online** paraméterében a `Get-Help` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="6e189-156">To get Help online, use the **Online** parameter of the `Get-Help` cmdlet.</span></span> <span data-ttu-id="6e189-157">A PowerShell-lel, beleértve a szolgáltató súgó származnak az összes Súgócikkek fogalmi (:), a cikkeket, és érhetők el online a [PowerShell](/powershell/scripting/powershell-scripting) dokumentációját.</span><span class="sxs-lookup"><span data-stu-id="6e189-157">All the Help articles that come with PowerShell, including provider Help and conceptual (About) Help articles, are available online in the [PowerShell](/powershell/scripting/powershell-scripting) documentation.</span></span>

> [!NOTE]
> <span data-ttu-id="6e189-158">Nem használhatja a **Online** fogalmi paraméterrel (about_\*) vagy a szolgáltató a cikkeket.</span><span class="sxs-lookup"><span data-stu-id="6e189-158">You can't use the **Online** parameter with conceptual (about_\*) or provider Help articles.</span></span>
> <span data-ttu-id="6e189-159">Online súgó nem kötelező, így minden parancsmag, függvény vagy parancsfájl nem működik.</span><span class="sxs-lookup"><span data-stu-id="6e189-159">Online help is optional, so it does not work for every cmdlet, function, or script.</span></span>

<span data-ttu-id="6e189-160">Például a súgócikk online verziójának beszerzéséhez a a `Get-ChildItem` parancsmagot, írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-160">For example, to get the online version of the Help article about the `Get-ChildItem` cmdlet, type:</span></span>

```powershell
Get-Help Get-ChildItem -Online
```

<span data-ttu-id="6e189-161">PowerShell a cikk az alapértelmezett böngészőben nyílik meg.</span><span class="sxs-lookup"><span data-stu-id="6e189-161">PowerShell opens the article in your default browser.</span></span> <span data-ttu-id="6e189-162">Online súgó egy súgócikk támogatott, ha az URL-címét a súgócikk is megtekintheti.</span><span class="sxs-lookup"><span data-stu-id="6e189-162">If online Help is supported for a Help article, you can also view the URL of the Help article.</span></span> <span data-ttu-id="6e189-163">Az URL-cím egy súgócikk kapcsolódó hivatkozások szakaszában jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="6e189-163">The URL appears in the Related Links section of a Help article.</span></span>

<span data-ttu-id="6e189-164">Például az URL-cím, az Add-Computer parancsmag online verziójának megtekintéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="6e189-164">For example, to see the URL for the online version of the Add-Computer cmdlet, type:</span></span>

```powershell
Get-Help Add-Computer
```

<span data-ttu-id="6e189-165">A cikk a kapcsolódó hivatkozások szakasz első sorában az alábbiakban látható.</span><span class="sxs-lookup"><span data-stu-id="6e189-165">The first line in the Related Links section of the article is shown below.</span></span>

```Output
Online version: http://go.microsoft.com/fwlink/?LinkId=821564
```

<span data-ttu-id="6e189-166">Online-támogatást nyújt a Súgócikkek kapcsolatos információkért lásd: [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span><span class="sxs-lookup"><span data-stu-id="6e189-166">For information about how to provide online support for your Help articles, see [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span></span>

## <a name="see-also"></a><span data-ttu-id="6e189-167">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6e189-167">See also</span></span>

- [<span data-ttu-id="6e189-168">about_Functions</span><span class="sxs-lookup"><span data-stu-id="6e189-168">about_Functions</span></span>](/powershell/module/microsoft.powershell.core/about/about_functions)
- [<span data-ttu-id="6e189-169">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="6e189-169">about_Scripts</span></span>](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [<span data-ttu-id="6e189-170">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="6e189-170">about_Comment_Based_Help</span></span>](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)
- [<span data-ttu-id="6e189-171">Get-Help</span><span class="sxs-lookup"><span data-stu-id="6e189-171">Get-Help</span></span>](/powershell/module/microsoft.powershell.core/get-help)
