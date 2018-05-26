---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Részletes súgóinformációk kérése
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 29c24af3f688f9388893044952442910e793842d
ms.sourcegitcommit: 735ccab3fb3834ccd8559fab6700b798e8e5ffbf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/25/2018
---
# <a name="getting-detailed-help-information"></a><span data-ttu-id="cfec0-103">Részletes súgóinformációk kérése</span><span class="sxs-lookup"><span data-stu-id="cfec0-103">Getting Detailed Help Information</span></span>
<span data-ttu-id="cfec0-104">Windows PowerShell Windows PowerShell fogalmak és a Windows PowerShell nyelvi részletes súgó-témaköröket tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="cfec0-104">Windows PowerShell includes detailed Help topics that explain Windows PowerShell concepts and the Windows PowerShell language.</span></span> <span data-ttu-id="cfec0-105">Megtalálhatók az egyes parancsmag és a szolgáltató Súgó-témaköröket és sok függvények és parancsfájlok Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="cfec0-105">There are also Help topics for each cmdlet and provider and Help topics for many functions and scripts.</span></span>

<span data-ttu-id="cfec0-106">E súgótémakörök útmutatást megjelenítéséhez a parancssorba, vagy tekintse meg a Microsoft TechNet Library az alábbi témakörök a közelmúltban frissített verziói.</span><span class="sxs-lookup"><span data-stu-id="cfec0-106">You can display these Help topics at the command prompt or view the most recently updated versions of these topics in the Microsoft TechNet Library.</span></span> <span data-ttu-id="cfec0-107">Számos olyan programok, amelyek futtatni a Windows PowerShell, például a Windows PowerShell integrált parancsfájlkezelési környezet, adja meg a Súgó további szolgáltatásokat, például a környezetfüggő súgó és lefordított súgófájl (.chm).</span><span class="sxs-lookup"><span data-stu-id="cfec0-107">Many programs that host Windows PowerShell, such as Windows PowerShell Integrated Scripting Environment, provide additional Help features, such as context-sensitive Help and compiled Help file (.chm).</span></span>

## <a name="getting-help-for-cmdlets"></a><span data-ttu-id="cfec0-108">Parancsmag súgójának megjelenítése</span><span class="sxs-lookup"><span data-stu-id="cfec0-108">Getting Help for Cmdlets</span></span>
<span data-ttu-id="cfec0-109">A Windows PowerShell-parancsmagokkal kapcsolatos súgó megjelenítéséhez használja a [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="cfec0-109">To get Help about Windows PowerShell cmdlets, use the [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) cmdlet.</span></span> <span data-ttu-id="cfec0-110">Segítség a példában a [Get-ChildItem [m2]](https://technet.microsoft.com/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) parancsmag, típus:</span><span class="sxs-lookup"><span data-stu-id="cfec0-110">For example, to get Help for the [Get-ChildItem [m2]](https://technet.microsoft.com/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) cmdlet, type:</span></span>

```
get-help get-childitem
```

<span data-ttu-id="cfec0-111">vagy a</span><span class="sxs-lookup"><span data-stu-id="cfec0-111">or</span></span>

```
get-childitem -?
```

<span data-ttu-id="cfec0-112">Akkor is kaphat a Get-Help parancsmag kapcsolatban.</span><span class="sxs-lookup"><span data-stu-id="cfec0-112">You can even get Help about the Get-Help cmdlet.</span></span> <span data-ttu-id="cfec0-113">Például:</span><span class="sxs-lookup"><span data-stu-id="cfec0-113">For example:</span></span>

```
get-help get-help
```

<span data-ttu-id="cfec0-114">A parancsmag súgótémakörök listájának lekérése a munkamenetben, írja be:</span><span class="sxs-lookup"><span data-stu-id="cfec0-114">To get a list of all the cmdlet Help topics in your session, type:</span></span>

```
get-help -category cmdlet
```

<span data-ttu-id="cfec0-115">Egyszerre csak egy lapot minden súgótémakör megjelenítéséhez használja a **súgó** függvény vagy az alias **man**.</span><span class="sxs-lookup"><span data-stu-id="cfec0-115">To display one page of each Help topic at a time, use the **help** function or its alias **man**.</span></span> <span data-ttu-id="cfec0-116">Például a Get-ChildItem parancsmag súgójának megjelenítéséhez írja be a következőt</span><span class="sxs-lookup"><span data-stu-id="cfec0-116">For example, to display Help for the Get-ChildItem cmdlet, type</span></span>

```
man get-childitem
```

<span data-ttu-id="cfec0-117">vagy a</span><span class="sxs-lookup"><span data-stu-id="cfec0-117">or</span></span>

```
help get-childitem
```

<span data-ttu-id="cfec0-118">Egy parancsmag, függvény vagy parancsfájl, például a paraméterek és a használati példák leírást kapcsolatos részletes információk megjelenítéséhez használja a *részletes* paramétert a Get-Help parancsmag.</span><span class="sxs-lookup"><span data-stu-id="cfec0-118">To display detailed information about a cmdlet, function, or script, including descriptions of its parameters and examples of its use, use the *Detailed* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="cfec0-119">Például a Get-ChildItem parancsmag részletes információkat kaphat, írja be:</span><span class="sxs-lookup"><span data-stu-id="cfec0-119">For example, to get detailed information about the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -detailed
```

<span data-ttu-id="cfec0-120">Minden tartalom súgójának megjelenítéséhez használja a *teljes* a Get-Help parancsmag paraméter.</span><span class="sxs-lookup"><span data-stu-id="cfec0-120">To display all content in the Help topic, use the *Full* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="cfec0-121">Például a Get-ChildItem parancsmag Súgó-témakör minden tartalom megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="cfec0-121">For example, to display all content in the Help topic for the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -full
```

<span data-ttu-id="cfec0-122">Beolvasandó részletes súgó parancsmag, használja a paraméterekről a *paraméter* paramétert a Get-Help parancsmag.</span><span class="sxs-lookup"><span data-stu-id="cfec0-122">To get detailed Help about the parameters of a cmdlet, use the *Parameter* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="cfec0-123">Például beolvasandó részletes súgó a Get-ChildItem parancsmag típusú paraméterek mindegyikét:</span><span class="sxs-lookup"><span data-stu-id="cfec0-123">For example, to get detailed Help for all of the parameters of the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -parameter *
```

<span data-ttu-id="cfec0-124">Csak a példák a súgótémakörök megjelenítéséhez használja a *példa* a Get-Help paramétere.</span><span class="sxs-lookup"><span data-stu-id="cfec0-124">To display only the examples in a Help topic, use the *Example* parameter of the Get-Help.</span></span> <span data-ttu-id="cfec0-125">Például a Get-ChildItem parancsmag Súgó-témakör csak a példák megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="cfec0-125">For example, to display only the examples in the Help topic for the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -examples
```

<span data-ttu-id="cfec0-126">A parancsmagok írást Súgó-témaköröket írásával kapcsolatban további információkért lásd: [arról, hogy miként írási parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415) az MSDN könyvtárában.</span><span class="sxs-lookup"><span data-stu-id="cfec0-126">For information about how to write Help topics for the cmdlets that you write, see [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415) in the MSDN library.</span></span>

## <a name="getting-conceptual-help"></a><span data-ttu-id="cfec0-127">Fogalmi kapcsolatos segítség kérése</span><span class="sxs-lookup"><span data-stu-id="cfec0-127">Getting Conceptual Help</span></span>
<span data-ttu-id="cfec0-128">A Get-Help parancsmag a Windows PowerShellben, beleértve a Windows PowerShell nyelvi kapcsolatos témakörök szintén elméleti témaköreit információkat jelenít meg.</span><span class="sxs-lookup"><span data-stu-id="cfec0-128">The Get-Help cmdlet also displays information about conceptual topics in Windows PowerShell, including topics about the Windows PowerShell language.</span></span> <span data-ttu-id="cfec0-129">Fogalmi Súgó-témaköröket a "about_" előtaggal, például about_line_editing kezdődik.</span><span class="sxs-lookup"><span data-stu-id="cfec0-129">Conceptual Help topics begin with the "about_" prefix, such as about_line_editing.</span></span> <span data-ttu-id="cfec0-130">(Az elméleti téma nevét kell megadni angol még akkor is, a Windows PowerShell nem angol nyelvű verzióiban.)</span><span class="sxs-lookup"><span data-stu-id="cfec0-130">(The name of the conceptual topic must be entered in English even on non-English versions of Windows PowerShell.)</span></span>

<span data-ttu-id="cfec0-131">Elméleti témaköreit listájának megjelenítéséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="cfec0-131">To display a list of conceptual topics, type:</span></span>

```
get-help about_*
```

<span data-ttu-id="cfec0-132">Adott megjelenítéséhez írja be például a témakör neve:</span><span class="sxs-lookup"><span data-stu-id="cfec0-132">To display a particular Help topic, type the topic name, for example:</span></span>

```
get-help about_command_syntax
```

<span data-ttu-id="cfec0-133">A paraméterek, a Get-Help, például a *részletes*, *paraméter*, és *példák*, nincsenek hatással az elméleti súgótémakörök megjelenítését.</span><span class="sxs-lookup"><span data-stu-id="cfec0-133">The parameters of Get-Help, such as *Detailed*, *Parameter*, and *Examples*, have no effect on the display of conceptual Help topics.</span></span>

## <a name="getting-help-about-providers"></a><span data-ttu-id="cfec0-134">Szolgáltatók kapcsolatos súgó elérése</span><span class="sxs-lookup"><span data-stu-id="cfec0-134">Getting Help About Providers</span></span>
<span data-ttu-id="cfec0-135">A Get-Help parancsmag Windows PowerShell-szolgáltató információit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="cfec0-135">The Get-Help cmdlet displays information about Windows PowerShell providers.</span></span> <span data-ttu-id="cfec0-136">Ha segítséget szeretne kérni a szolgáltató, írja be a "Get-Help" szolgáltató neve követ.</span><span class="sxs-lookup"><span data-stu-id="cfec0-136">To get Help for a provider, type "Get-Help" followed by the provider name.</span></span> <span data-ttu-id="cfec0-137">Például a beállításjegyzék-szolgáltatójának súgójának, írja be:</span><span class="sxs-lookup"><span data-stu-id="cfec0-137">For example, to get Help for the Registry provider, type:</span></span>

```
get-help registry
```

<span data-ttu-id="cfec0-138">A szolgáltató súgótémakörök a munkamenetet, írja be az összes listáját</span><span class="sxs-lookup"><span data-stu-id="cfec0-138">To get a list of all the provider Help topics in your session, type</span></span>

```
get-help -category provider
```

<span data-ttu-id="cfec0-139">A paraméterek, a Get-Help, például a *részletes*, *paraméter*, és *példák*, hatástalan szolgáltató súgótémakörök megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="cfec0-139">The parameters of Get-Help, such as *Detailed*, *Parameter*, and *Examples*, have no effect on the display of provider Help topics.</span></span>

## <a name="getting-help-about-scripts-and-functions"></a><span data-ttu-id="cfec0-140">Kapcsolatos parancsfájlokban és függvényekben kapcsolatos segítség kérése</span><span class="sxs-lookup"><span data-stu-id="cfec0-140">Getting Help About Scripts and Functions</span></span>
<span data-ttu-id="cfec0-141">Sok parancsfájlokban és függvényekben, a Windows PowerShell rendelkezik Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="cfec0-141">Many scripts and functions in Windows PowerShell have Help topics.</span></span> <span data-ttu-id="cfec0-142">A Get-Help parancsmag segítségével megjelenítheti a parancsfájlokban és függvényekben Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="cfec0-142">Use the Get-Help cmdlet to display the Help topics for scripts and functions.</span></span>

<span data-ttu-id="cfec0-143">A függvény a súgó megjelenítéséhez írja be a "get-help" függvény nevével kiegészítve.</span><span class="sxs-lookup"><span data-stu-id="cfec0-143">To display the Help for a function, type "get-help" followed by the function name.</span></span> <span data-ttu-id="cfec0-144">Ha segítséget szeretne kérni a Disable-PSRemoting függvény, például:</span><span class="sxs-lookup"><span data-stu-id="cfec0-144">For example, to get Help for the Disable-PSRemoting function, type:</span></span>

```
get-help disable-psremoting
```

<span data-ttu-id="cfec0-145">A parancsfájl a súgó megjelenítéséhez írja be a parancsfájlban a teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="cfec0-145">To display the Help for a script, type the fully qualified path to the script file.</span></span> <span data-ttu-id="cfec0-146">Ha a parancsfájl elérési út szerepel-e a Path környezeti változóba, akkor kihagyhatja a parancs az elérési út.</span><span class="sxs-lookup"><span data-stu-id="cfec0-146">If the script is in a path that is listed in the Path environment variable, you can omit the path from the command.</span></span>

<span data-ttu-id="cfec0-147">Például, ha a c: "TestScript.ps1" nevű parancsfájl\\PS-teszt címtár megjeleníthető a Súgó-témakört a parancsfájl típusát:</span><span class="sxs-lookup"><span data-stu-id="cfec0-147">For example, if you have a script called "TestScript.ps1" in your C:\\PS-Test directory, to display the Help topic for the script, type:</span></span>

```
get-help c:\ps-test\TestScript.ps1
```

<span data-ttu-id="cfec0-148">A paraméterek, a parancsmag megjelenő tervezett segítenek, például a *részletes*, *teljes*, *példák*, és *paraméter*, a munkahelyi parancsfájl Súgó és függvény segítségével, túl.</span><span class="sxs-lookup"><span data-stu-id="cfec0-148">The parameters that were designed for displaying cmdlet Help, such as *Detailed*, *Full*, *Examples*, and *Parameter*, work for script Help and function Help, too.</span></span> <span data-ttu-id="cfec0-149">Azonban ha azt minden Súgó megjelenítése, írja be a "get-help \*", Súgó függvények és parancsfájlok nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="cfec0-149">However, when you display all Help, by typing "get-help \*", Help for functions and scripts does not appear.</span></span>

<span data-ttu-id="cfec0-150">További információ a Súgó-témaköröket a függvények és parancsfájlok írása: [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af), és [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).</span><span class="sxs-lookup"><span data-stu-id="cfec0-150">For information about writing Help topics for your functions and scripts, see [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af), and [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).</span></span>

## <a name="getting-help-online"></a><span data-ttu-id="cfec0-151">Online súgó</span><span class="sxs-lookup"><span data-stu-id="cfec0-151">Getting Help Online</span></span>
<span data-ttu-id="cfec0-152">Ha az Internethez csatlakoznak, a legjobb részleteket a segítségkéréshez egyik online a segítő súgótémakörök megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="cfec0-152">If you are connected to the Internet, one of the best ways to get Help is to view the Help topics online.</span></span> <span data-ttu-id="cfec0-153">Mivel az online témakörök könnyen lehet frissíteni, akkor ezeknél valószínűleg adja meg a legújabb tartalom.</span><span class="sxs-lookup"><span data-stu-id="cfec0-153">Because online topics are easy to update, they are likely to provide the most current content.</span></span>

<span data-ttu-id="cfec0-154">Ha segítséget szeretne kérni online, próbálja meg a *Online* a Get-Help parancsmag paraméter.</span><span class="sxs-lookup"><span data-stu-id="cfec0-154">To get Help online, try the *Online* parameter of the Get-Help cmdlet.</span></span> <span data-ttu-id="cfec0-155">A *Online* paraméter csak a parancsmag súgójában, a Get-Help parancsmag munkálatok súgó működik, és parancsfájl-súgó.</span><span class="sxs-lookup"><span data-stu-id="cfec0-155">The *Online* parameter of the Get-Help cmdlet works only for cmdlet Help, function Help, and script Help.</span></span> <span data-ttu-id="cfec0-156">Nem használhatja a *Online* paraméterrel fogalmi (:) témakörök vagy szolgáltató Súgó-témaköröket.</span><span class="sxs-lookup"><span data-stu-id="cfec0-156">You cannot use the *Online* parameter with conceptual (About) topics or provider Help topics.</span></span> <span data-ttu-id="cfec0-157">Emellett ez a szolgáltatás nem választható, mert nem működik minden parancsmagot, függvény vagy parancsfájl súgótémakör.</span><span class="sxs-lookup"><span data-stu-id="cfec0-157">Also, because this feature is optional, it does not work for every cmdlet, function, or script Help topic.</span></span>

<span data-ttu-id="cfec0-158">Azonban a súgótémakörök, amelyek rendelkeznek a Windows PowerShell, beleértve a szolgáltató Súgó és fogalmi (:) Súgó-témaköröket érhetők el online a [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) a Microsoft TechNet Library szakasza.</span><span class="sxs-lookup"><span data-stu-id="cfec0-158">However, all the Help topics that come with Windows PowerShell, including provider Help and conceptual (About) Help topics, are available online in the [Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) section of the Microsoft TechNet Library.</span></span>

<span data-ttu-id="cfec0-159">Használatához a *Online* paramétert a Get-Help parancsmag használata a következő parancs formátuma.</span><span class="sxs-lookup"><span data-stu-id="cfec0-159">To use the *Online* parameter of the Get-Help cmdlet, use the following command format.</span></span>

```
get-help <command-name> -online
```

<span data-ttu-id="cfec0-160">Ahhoz, hogy a Get-ChildItem parancsmaggal kapcsolatban a témakör online verzióját, például:</span><span class="sxs-lookup"><span data-stu-id="cfec0-160">For example, to get the online version of the Help topic about the Get-ChildItem cmdlet, type:</span></span>

```
get-help get-childitem -online
```

<span data-ttu-id="cfec0-161">A Súgó-témakör online verzióját érhető el, ha az alapértelmezett böngészőben nyílik.</span><span class="sxs-lookup"><span data-stu-id="cfec0-161">If an online version of the Help topic is available, it will open in your default browser.</span></span>

<span data-ttu-id="cfec0-162">Online súgó súgótémakör esetén támogatott, ha az internetes URL-címét a témakör is megtekintheti.</span><span class="sxs-lookup"><span data-stu-id="cfec0-162">If online Help is supported for a Help topic, you can also view the Internet address (URL) of the Help topic.</span></span> <span data-ttu-id="cfec0-163">Az internetcím súgótémakör kapcsolódó hivatkozások szakaszában jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="cfec0-163">The Internet address appears in the Related Links section of a Help topic.</span></span>

<span data-ttu-id="cfec0-164">Például az URL-cím, az Add-Computer parancsmag online verziójához parancsot kell beírnia:</span><span class="sxs-lookup"><span data-stu-id="cfec0-164">For example, to see the URL for the online version of the Add-Computer cmdlet, type:</span></span>

```
get-help add-computer
```

<span data-ttu-id="cfec0-165">Az első sor a kapcsolódó hivatkozások szakaszban, a következő témakörben alább láthatók.</span><span class="sxs-lookup"><span data-stu-id="cfec0-165">The first line in the Related Links section of the topic is shown below.</span></span>

```
Online version: http://go.microsoft.com/fwlink/?LinkID=135194
```

<span data-ttu-id="cfec0-166">Online támogatást nyújt a súgótémakörök kapcsolatos információkért lásd: [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf), és mit [arról, hogy miként írási parancsmag](https://go.microsoft.com/fwlink/?LinkID=123415) az MSDN könyvtárában.</span><span class="sxs-lookup"><span data-stu-id="cfec0-166">For information about how to provide online support for your Help topics, see [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf), and see [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415) in the MSDN library.</span></span>

## <a name="see-also"></a><span data-ttu-id="cfec0-167">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cfec0-167">See Also</span></span>
- <span data-ttu-id="cfec0-168">[about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105)</span><span class="sxs-lookup"><span data-stu-id="cfec0-168">[about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105)</span></span>
- [<span data-ttu-id="cfec0-169">about_Scripts</span><span class="sxs-lookup"><span data-stu-id="cfec0-169">about_Scripts</span></span>](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af)
- [<span data-ttu-id="cfec0-170">about_Comment_Based_Help</span><span class="sxs-lookup"><span data-stu-id="cfec0-170">about_Comment_Based_Help</span></span>](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)
- <span data-ttu-id="cfec0-171">[Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)</span><span class="sxs-lookup"><span data-stu-id="cfec0-171">[Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)</span></span>