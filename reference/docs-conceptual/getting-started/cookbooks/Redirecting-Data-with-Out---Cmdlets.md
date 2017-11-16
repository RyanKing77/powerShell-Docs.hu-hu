---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Kimenő parancsmagok adatok átirányítása"
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: e570ca1c2c665a4a5d23abb50d4102a012b160e9
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="redirecting-data-with-out--cmdlets"></a><span data-ttu-id="a09bf-103">Az Out - adatok átirányítása * parancsmagok</span><span class="sxs-lookup"><span data-stu-id="a09bf-103">Redirecting Data with Out-* Cmdlets</span></span>
<span data-ttu-id="a09bf-104">A Windows PowerShell számos-parancsmagokat kínál, amelyekkel szabályozhatja, hogy közvetlenül a kimeneti adatok.</span><span class="sxs-lookup"><span data-stu-id="a09bf-104">Windows PowerShell provides several cmdlets that let you control data output directly.</span></span> <span data-ttu-id="a09bf-105">Ezeket a parancsmagokat a megosztás két lényeges, azonosítandó paraméterek.</span><span class="sxs-lookup"><span data-stu-id="a09bf-105">These cmdlets share two important characteristics.</span></span>

<span data-ttu-id="a09bf-106">Először azokat általában átalakítási valamilyen szöveges adatokat.</span><span class="sxs-lookup"><span data-stu-id="a09bf-106">First, they generally transform data to some form of text.</span></span> <span data-ttu-id="a09bf-107">Van így, mert azok kimeneti szöveg beavatkozást igénylő rendszerösszetevők az adatokat.</span><span class="sxs-lookup"><span data-stu-id="a09bf-107">They do this because they output the data to system components that require text input.</span></span> <span data-ttu-id="a09bf-108">Ez azt jelenti, hogy az objektumokat képviseli szövegként van szükségük.</span><span class="sxs-lookup"><span data-stu-id="a09bf-108">This means they need to represent the objects as text.</span></span> <span data-ttu-id="a09bf-109">A-szöveg formátuma, ezért a Windows PowerShell konzol ablakban látható módon.</span><span class="sxs-lookup"><span data-stu-id="a09bf-109">Therefore, the text is formatted as you see it in the Windows PowerShell console window.</span></span>

<span data-ttu-id="a09bf-110">Második, ezek a parancsmagok a Windows PowerShell-művelet használata **kimenő** mert azok adatokat küld a Windows PowerShell valahol máshol.</span><span class="sxs-lookup"><span data-stu-id="a09bf-110">Second, these cmdlets use the Windows PowerShell verb **Out** because they send information out from Windows PowerShell to somewhere else.</span></span> <span data-ttu-id="a09bf-111">A **kimenő gazdagép** parancsmag nincs kivétel: a fogadó ablakban megjelenített Windows PowerShell kívül esik.</span><span class="sxs-lookup"><span data-stu-id="a09bf-111">The **Out-Host** cmdlet is no exception: the host window display is outside of Windows PowerShell.</span></span> <span data-ttu-id="a09bf-112">Ez azért fontos, mert a Windows PowerShell kívül adatokat küldi el, ha az ténylegesen törlődik.</span><span class="sxs-lookup"><span data-stu-id="a09bf-112">This is important because when data is sent out of Windows PowerShell, it is actually removed.</span></span> <span data-ttu-id="a09bf-113">Erre úgy tekinthet, ha hozzon létre egy folyamatot, hogy a fogadó ablakban lapok az adatok, majd próbálja meg formázni a listában, ahogy az itt látható:</span><span class="sxs-lookup"><span data-stu-id="a09bf-113">You can see this if you try to create a pipeline that pages data to the host window, and then attempt to format it as a list, as shown here:</span></span>

```
PS> Get-Process | Out-Host -Paging | Format-List
```

<span data-ttu-id="a09bf-114">A parancs folyamatra vonatkozó információ oldalain megjelenő listaformátumot várt.</span><span class="sxs-lookup"><span data-stu-id="a09bf-114">You might expect the command to display pages of process information in list format.</span></span> <span data-ttu-id="a09bf-115">Ehelyett az alapértelmezett táblázatos listáját jeleníti meg:</span><span class="sxs-lookup"><span data-stu-id="a09bf-115">Instead, it displays the default tabular list:</span></span>

```
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    101       5     1076       3316    32     0.05   2888 alg
...
    618      18    39348      51108   143   211.20    740 explorer
    257       8     9752      16828    79     3.02   2560 explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="a09bf-116">A **kimenő gazdagép** parancsmag elküldi az adatokat közvetlenül a konzol, ezért a **Format-List** parancs soha nem kap semmit formázásához.</span><span class="sxs-lookup"><span data-stu-id="a09bf-116">The **Out-Host** cmdlet sends the data directly to the console, so the **Format-List** command never receives anything to format.</span></span>

<span data-ttu-id="a09bf-117">A helyes-e ez a parancs szerkezeti módja, amelyre az a **kimenő gazdagép** parancsmag az alább látható módon a folyamat végén.</span><span class="sxs-lookup"><span data-stu-id="a09bf-117">The correct way to structure this command is to put the **Out-Host** cmdlet at the end of the pipeline as shown below.</span></span> <span data-ttu-id="a09bf-118">Ez azt eredményezi, hogy a folyamat adatok listaként lapozható és a megjelenített előtt kell formázni.</span><span class="sxs-lookup"><span data-stu-id="a09bf-118">This causes the process data to be formatted in a list before being paged and displayed.</span></span>

```
PS> Get-Process | Format-List | Out-Host -Paging

Id      : 2888
Handles : 101
CPU     : 0.046875
Name    : alg
...

Id      : 740
Handles : 612
CPU     : 211.703125
Name    : explorer

Id      : 2560
Handles : 257
CPU     : 3.015625
Name    : explorer
...
<SPACE> next page; <CR> next line; Q quit
...
```

<span data-ttu-id="a09bf-119">Ez vonatkozik az összes a **kimenő** parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="a09bf-119">This applies to all of the **Out** cmdlets.</span></span> <span data-ttu-id="a09bf-120">Egy **kimenő** parancsmag mindig megjelenjen-e a folyamat végén.</span><span class="sxs-lookup"><span data-stu-id="a09bf-120">An **Out** cmdlet should always appear at the end of the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="a09bf-121">Minden a **kimenő** parancsmagok szöveg, a formázást érvényben a konzolablakban, ideértve a sor hossza határok kimenet megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="a09bf-121">All the **Out** cmdlets render output as text, using the formatting in effect for the console window, including line length limits.</span></span>

#### <a name="paging-console-output-out-host"></a><span data-ttu-id="a09bf-122">Lapozás a konzol kimeneti (kimenő gazdagép)</span><span class="sxs-lookup"><span data-stu-id="a09bf-122">Paging Console Output (Out-Host)</span></span>
<span data-ttu-id="a09bf-123">Alapértelmezés szerint a Windows PowerShell adatokat küldi el a gazdagép ablak, amely pontosan mi a kimenő gazdagép parancsmag biztosítja.</span><span class="sxs-lookup"><span data-stu-id="a09bf-123">By default, Windows PowerShell sends data to the host window, which is exactly what the Out-Host cmdlet does.</span></span> <span data-ttu-id="a09bf-124">Az elsődleges funkciója a kimenő gazdagép parancsmag lapozófájlok, mint korábban tárgyalt.</span><span class="sxs-lookup"><span data-stu-id="a09bf-124">The primary use for the Out-Host cmdlet is paging data as we discussed earlier.</span></span> <span data-ttu-id="a09bf-125">Például a következő parancs használatát kimenő gazdagépről a Get-Command parancsmag kimenetét lapon:</span><span class="sxs-lookup"><span data-stu-id="a09bf-125">For example, the following command uses Out-Host to page the output of the Get-Command cmdlet:</span></span>

```
PS> Get-Command | Out-Host -Paging
```

<span data-ttu-id="a09bf-126">Használhatja a **további** oldaladatokat függvényt.</span><span class="sxs-lookup"><span data-stu-id="a09bf-126">You can also use the **more** function to page data.</span></span> <span data-ttu-id="a09bf-127">A Windows PowerShell parancssorába **további** egy funkciója, amely behívja **kimenő gazdagép-lapozást**.</span><span class="sxs-lookup"><span data-stu-id="a09bf-127">In Windows PowerShell, **more** is a function that calls **Out-Host -Paging**.</span></span> <span data-ttu-id="a09bf-128">Az alábbi parancs bemutatja, használja a **további** működnek, mint a Get-parancs kimenetében lapon:</span><span class="sxs-lookup"><span data-stu-id="a09bf-128">The following command demonstrates using the **more** function to page the output of Get-Command:</span></span>

```
PS> Get-Command | more
```

<span data-ttu-id="a09bf-129">Ha egy vagy több fájlt adja meg a további függvény argumentumaként, a függvény a megadott fájlok olvasását, és azok tartalmát, a fogadó oldalon:</span><span class="sxs-lookup"><span data-stu-id="a09bf-129">If you include one or more filenames as arguments to the more function, the function will read the specified files and page their contents to the host:</span></span>

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

#### <a name="discarding-output-out-null"></a><span data-ttu-id="a09bf-130">Kimeneti elvetése (kimenő Null)</span><span class="sxs-lookup"><span data-stu-id="a09bf-130">Discarding Output (Out-Null)</span></span>
<span data-ttu-id="a09bf-131">A **kimenő Null** parancsmag arra tervezték, hogy azonnal elveti az összes beviteli kap.</span><span class="sxs-lookup"><span data-stu-id="a09bf-131">The **Out-Null** cmdlet is designed to immediately discard any input it receives.</span></span> <span data-ttu-id="a09bf-132">Ez akkor hasznos, a kapott egyik mellékhatása fut egy parancs, mint a szükségtelen adatok törlésével.</span><span class="sxs-lookup"><span data-stu-id="a09bf-132">This is useful for discarding unnecessary data that you get as a side-effect of running a command.</span></span> <span data-ttu-id="a09bf-133">Ha írja be a következő parancsot, nem kap semmit újra a parancsot:</span><span class="sxs-lookup"><span data-stu-id="a09bf-133">When type the following command, you do not get anything back from the command:</span></span>

```
PS> Get-Command | Out-Null
```

<span data-ttu-id="a09bf-134">A **kimenő Null** parancsmag dobja kimeneti hiba.</span><span class="sxs-lookup"><span data-stu-id="a09bf-134">The **Out-Null** cmdlet does not discard error output.</span></span> <span data-ttu-id="a09bf-135">Például, ha a következő parancsot adja meg, egy üzenet jelenik meg tájékoztat, hogy a Windows PowerShell nem ismeri fel a "Rendszer-NotACommand":</span><span class="sxs-lookup"><span data-stu-id="a09bf-135">For example, if you enter the following command, a message is displayed informing you that Windows PowerShell does not recognize 'Is-NotACommand':</span></span>

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

#### <a name="printing-data-out-printer"></a><span data-ttu-id="a09bf-136">Nyomtatás adatok (Out-nyomtató)</span><span class="sxs-lookup"><span data-stu-id="a09bf-136">Printing Data (Out-Printer)</span></span>
<span data-ttu-id="a09bf-137">Adatok használatával kinyomtathatja a **Out-nyomtató** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="a09bf-137">You can print data by using the **Out-Printer** cmdlet.</span></span> <span data-ttu-id="a09bf-138">A **Out-nyomtató** parancsmag fogja használni az alapértelmezett nyomtató, ha a nyomtató neve nincs megadva.</span><span class="sxs-lookup"><span data-stu-id="a09bf-138">The **Out-Printer** cmdlet will use your default printer if you do not provide a printer name.</span></span> <span data-ttu-id="a09bf-139">Bármely Windows-alapú nyomtató használhatja a megjelenített név megadásával.</span><span class="sxs-lookup"><span data-stu-id="a09bf-139">You can use any Windows-based printer by specifying its display name.</span></span> <span data-ttu-id="a09bf-140">Nincs szükség a nyomtató- vagy a tényleges fizikai nyomtató bármilyen típusú.</span><span class="sxs-lookup"><span data-stu-id="a09bf-140">There is no need for any kind of printer port mapping or even a real physical printer.</span></span> <span data-ttu-id="a09bf-141">Például ha a Microsoft Office dokumentum a lemezképkészítés eszközöket, akkor is küldheti az adatokat képfájlra mutató beírásával:</span><span class="sxs-lookup"><span data-stu-id="a09bf-141">For example, if you have the Microsoft Office document imaging tools installed, you can send the data to an image file by typing:</span></span>

```
PS> Get-Command Get-Command | Out-Printer -Name "Microsoft Office Document Image Writer"
```

#### <a name="saving-data-out-file"></a><span data-ttu-id="a09bf-142">Adatok mentése (out-File)</span><span class="sxs-lookup"><span data-stu-id="a09bf-142">Saving Data (Out-File)</span></span>
<span data-ttu-id="a09bf-143">Egy fájl helyett a konzolablakban kimeneti a használatával küldhet a **out-File** parancsmag.</span><span class="sxs-lookup"><span data-stu-id="a09bf-143">You can send output to a file instead of the console window by using the **Out-File** cmdlet.</span></span> <span data-ttu-id="a09bf-144">A következő parancssori folyamatok listájának küld a fájl **C:\\temp\\processlist.txt**:</span><span class="sxs-lookup"><span data-stu-id="a09bf-144">The following command line sends a list of processes to the file **C:\\temp\\processlist.txt**:</span></span>

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

<span data-ttu-id="a09bf-145">Az eredmények használatával a **out-File** parancsmag nem lehet várt a hagyományos kimenet átirányítása használata.</span><span class="sxs-lookup"><span data-stu-id="a09bf-145">The results of using the **Out-File** cmdlet may not be what you expect if you are used to traditional output redirection.</span></span> <span data-ttu-id="a09bf-146">Szeretné megtudni, annak viselkedését, figyelembe kell venni a környezet, amelyben a **out-File** parancsmag működik.</span><span class="sxs-lookup"><span data-stu-id="a09bf-146">To understand its behavior, you must be aware of the context in which the **Out-File** cmdlet operates.</span></span>

<span data-ttu-id="a09bf-147">Alapértelmezés szerint a **out-File** parancsmag létrehoz egy Unicode-fájlt.</span><span class="sxs-lookup"><span data-stu-id="a09bf-147">By default, the **Out-File** cmdlet creates a Unicode file.</span></span> <span data-ttu-id="a09bf-148">Ez az ajánlott alapértelmezett hosszú távon, de az azt jelenti, hogy eszközök, amelyek ASCII fájlokat nem fog megfelelően működni az alapértelmezett kimeneti formátummal.</span><span class="sxs-lookup"><span data-stu-id="a09bf-148">This is the best default in the long run, but it means that tools that expect ASCII files will not work correctly with the default output format.</span></span> <span data-ttu-id="a09bf-149">Módosíthatja az alapértelmezett kimeneti formátum ASCII használatával a **kódolás** paraméter:</span><span class="sxs-lookup"><span data-stu-id="a09bf-149">You can change the default output format to ASCII by using the **Encoding** parameter:</span></span>

```
PS> Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

<span data-ttu-id="a09bf-150">**Out-File** formátumok fájl tartalmát a konzol kimeneti tűnik.</span><span class="sxs-lookup"><span data-stu-id="a09bf-150">**Out-file** formats file contents to look like console output.</span></span> <span data-ttu-id="a09bf-151">Ez azt eredményezi, hogy a kimeneti kell csonkolni, akárcsak a legtöbb esetben a konzolablakban.</span><span class="sxs-lookup"><span data-stu-id="a09bf-151">This causes the output to be truncated just as it is in a console window in most circumstances.</span></span> <span data-ttu-id="a09bf-152">Ha például a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="a09bf-152">For example, if you run the following command:</span></span>

```
PS> Get-Command | Out-File -FilePath c:\temp\output.txt
```

<span data-ttu-id="a09bf-153">A kimeneti fog kinézni:</span><span class="sxs-lookup"><span data-stu-id="a09bf-153">The output will look like this:</span></span>

```
CommandType     Name                            Definition                     
-----------     ----                            ----------                     
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

<span data-ttu-id="a09bf-154">Ahhoz, hogy a kimenet nem kényszerítik ki a sor becsomagolja szélességét a megfelelő, használhatja a **szélesség** paramétert vonalvastagságát.</span><span class="sxs-lookup"><span data-stu-id="a09bf-154">To get output that does not force line wraps to match the screen width, you can use the **Width** parameter to specify line width.</span></span> <span data-ttu-id="a09bf-155">Mivel **szélesség** 32 bites egész paraméter, a megadható maximális érték érték 2147483647.</span><span class="sxs-lookup"><span data-stu-id="a09bf-155">Because **Width** is a 32-bit integer parameter, the maximum value it can have is 2147483647.</span></span> <span data-ttu-id="a09bf-156">A vonalvastagság ezen maximális értékre állítva a következőket írja be:</span><span class="sxs-lookup"><span data-stu-id="a09bf-156">Type the following to set the line width to this maximum value:</span></span>

```
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

<span data-ttu-id="a09bf-157">A **out-File** parancsmag akkor hasznos, ha a kimeneti menti, akkor rendelkezik jelenik meg a konzolon.</span><span class="sxs-lookup"><span data-stu-id="a09bf-157">The **Out-File** cmdlet is most useful when you want to save output as it would have displayed on the console.</span></span> <span data-ttu-id="a09bf-158">A kimeneti formátum részletesebben vezérelheti speciális eszközök kell.</span><span class="sxs-lookup"><span data-stu-id="a09bf-158">For finer control over output format, you need more advanced tools.</span></span> <span data-ttu-id="a09bf-159">A következő fejezet bizonyos adatai használható együtt a következő fog keresni.</span><span class="sxs-lookup"><span data-stu-id="a09bf-159">We will look at those in the next chapter, along with some details about object manipulation.</span></span>

