---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Adatátirányítás az Out-parancsmagokkal
ms.assetid: 2a4acd33-041d-43a5-a3e9-9608a4c52b0c
ms.openlocfilehash: 7c601b09cc53524eb55014b8ea19a5d79cb98b0e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086153"
---
# <a name="redirecting-data-with-out--cmdlets"></a><span data-ttu-id="2d95f-103">Adatátirányítás az Out-\* parancsmagokkal</span><span class="sxs-lookup"><span data-stu-id="2d95f-103">Redirecting Data with Out-\* Cmdlets</span></span>

<span data-ttu-id="2d95f-104">Windows PowerShell számos-parancsmagokat kínál, amelyek segítségével szabályozhatja, hogy közvetlenül a kimeneti adatokat.</span><span class="sxs-lookup"><span data-stu-id="2d95f-104">Windows PowerShell provides several cmdlets that let you control data output directly.</span></span> <span data-ttu-id="2d95f-105">Ezek a parancsmagok két lényeges, azonosítandó paraméterek megosztani.</span><span class="sxs-lookup"><span data-stu-id="2d95f-105">These cmdlets share two important characteristics.</span></span>

<span data-ttu-id="2d95f-106">Először azok általánosan adatok átalakítása a valamilyen szöveget.</span><span class="sxs-lookup"><span data-stu-id="2d95f-106">First, they generally transform data to some form of text.</span></span> <span data-ttu-id="2d95f-107">Van így, mert ezek az adatok kimenetét szövegbevitel igénylő-összetevőkkel.</span><span class="sxs-lookup"><span data-stu-id="2d95f-107">They do this because they output the data to system components that require text input.</span></span> <span data-ttu-id="2d95f-108">Ez azt jelenti, hogy az objektumok tartozik szöveg van szükségük.</span><span class="sxs-lookup"><span data-stu-id="2d95f-108">This means they need to represent the objects as text.</span></span> <span data-ttu-id="2d95f-109">A szöveg formátuma, ezért a Windows PowerShell konzol ablakában látható módon.</span><span class="sxs-lookup"><span data-stu-id="2d95f-109">Therefore, the text is formatted as you see it in the Windows PowerShell console window.</span></span>

<span data-ttu-id="2d95f-110">A második, ezeket a parancsmagokat használja-e a Windows PowerShell-műveletet **ki** mert azok adatokat küld a Windows Powershellből valahol máshol.</span><span class="sxs-lookup"><span data-stu-id="2d95f-110">Second, these cmdlets use the Windows PowerShell verb **Out** because they send information out from Windows PowerShell to somewhere else.</span></span> <span data-ttu-id="2d95f-111">A **élekről gazdagép** parancsmag ez sem kivétel: a fogadó ablakban megjelenített Windows PowerShell kívül esik.</span><span class="sxs-lookup"><span data-stu-id="2d95f-111">The **Out-Host** cmdlet is no exception: the host window display is outside of Windows PowerShell.</span></span> <span data-ttu-id="2d95f-112">Ez azért fontos, mert adatküldést kívül a Windows PowerShell, ténylegesen eltávolítja azt.</span><span class="sxs-lookup"><span data-stu-id="2d95f-112">This is important because when data is sent out of Windows PowerShell, it is actually removed.</span></span> <span data-ttu-id="2d95f-113">Ez, láthatja, ha létrehoz egy folyamatot, hogy a fogadó ablakban oldalak adatok próbálja, majd próbálja meg egy listaként formázandó itt látható módon:</span><span class="sxs-lookup"><span data-stu-id="2d95f-113">You can see this if you try to create a pipeline that pages data to the host window, and then attempt to format it as a list, as shown here:</span></span>

```powershell
Get-Process | Out-Host -Paging | Format-List
```

<span data-ttu-id="2d95f-114">Így várhatóan a parancs formátuma folyamatra vonatkozó információ a lapok megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="2d95f-114">You might expect the command to display pages of process information in list format.</span></span> <span data-ttu-id="2d95f-115">Ehelyett azt jeleníti meg az alapértelmezett táblázatos listájában:</span><span class="sxs-lookup"><span data-stu-id="2d95f-115">Instead, it displays the default tabular list:</span></span>

```output
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

<span data-ttu-id="2d95f-116">A **élekről gazdagép** parancsmag elküldi az adatokat a konzolon, így a **Format-List** parancs soha nem kap semmit sem kell formázni.</span><span class="sxs-lookup"><span data-stu-id="2d95f-116">The **Out-Host** cmdlet sends the data directly to the console, so the **Format-List** command never receives anything to format.</span></span>

<span data-ttu-id="2d95f-117">Építse fel a parancs a megfelelő módon, hogy helyezze a **élekről gazdagép** parancsmag az alább látható módon a folyamat végén.</span><span class="sxs-lookup"><span data-stu-id="2d95f-117">The correct way to structure this command is to put the **Out-Host** cmdlet at the end of the pipeline as shown below.</span></span> <span data-ttu-id="2d95f-118">Ennek hatására az adatfeldolgozás előtt lapozható és a megjelenő listában formázott.</span><span class="sxs-lookup"><span data-stu-id="2d95f-118">This causes the process data to be formatted in a list before being paged and displayed.</span></span>

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

<span data-ttu-id="2d95f-119">Ez vonatkozik az összes a **ki** parancsmagok.</span><span class="sxs-lookup"><span data-stu-id="2d95f-119">This applies to all of the **Out** cmdlets.</span></span> <span data-ttu-id="2d95f-120">Egy **ki** parancsmag mindig meg kell jelennie a folyamat végén.</span><span class="sxs-lookup"><span data-stu-id="2d95f-120">An **Out** cmdlet should always appear at the end of the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="2d95f-121">Az összes a **ki** parancsmagok az kimeneti használatával a formázás érvényben a konzolablakban, beleértve a sor hosszának korlátozása, szöveges formában jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="2d95f-121">All the **Out** cmdlets render output as text, using the formatting in effect for the console window, including line length limits.</span></span>

## <a name="paging-console-output-out-host"></a><span data-ttu-id="2d95f-122">Lapozófájl-konzolkimenet (élekről gazdagép)</span><span class="sxs-lookup"><span data-stu-id="2d95f-122">Paging Console Output (Out-Host)</span></span>

<span data-ttu-id="2d95f-123">Alapértelmezés szerint Windows PowerShell a gazdagép ablak, amely pontosan mit küld adatokat a kimenő irányú gazdagép parancsmag biztosítja.</span><span class="sxs-lookup"><span data-stu-id="2d95f-123">By default, Windows PowerShell sends data to the host window, which is exactly what the Out-Host cmdlet does.</span></span> <span data-ttu-id="2d95f-124">Az elsődleges funkciója a élekről gazdagép parancsmag a már volt szó korábbi lapozófájlok lehetőség.</span><span class="sxs-lookup"><span data-stu-id="2d95f-124">The primary use for the Out-Host cmdlet is paging data as we discussed earlier.</span></span> <span data-ttu-id="2d95f-125">A következő parancsot használja például élekről tárolni a lapon a Get-Command parancsmag kimenete:</span><span class="sxs-lookup"><span data-stu-id="2d95f-125">For example, the following command uses Out-Host to page the output of the Get-Command cmdlet:</span></span>

```powershell
Get-Command | Out-Host -Paging
```

<span data-ttu-id="2d95f-126">Is használhatja a **további** oldaladatokat függvényt.</span><span class="sxs-lookup"><span data-stu-id="2d95f-126">You can also use the **more** function to page data.</span></span> <span data-ttu-id="2d95f-127">A Windows PowerShellben **további** egy függvény meghívásához **élekről gazdagép-lapozás**.</span><span class="sxs-lookup"><span data-stu-id="2d95f-127">In Windows PowerShell, **more** is a function that calls **Out-Host -Paging**.</span></span> <span data-ttu-id="2d95f-128">A következő parancs használatát mutatja be a **további** függvény lapon a Get-parancs kimenetében:</span><span class="sxs-lookup"><span data-stu-id="2d95f-128">The following command demonstrates using the **more** function to page the output of Get-Command:</span></span>

```powershell
Get-Command | more
```

<span data-ttu-id="2d95f-129">Ha további függvény argumentumaként adja meg egy vagy több fájlt, a függvény a megadott fájlok olvasásához, és azok tartalmát, a fogadó oldalon:</span><span class="sxs-lookup"><span data-stu-id="2d95f-129">If you include one or more filenames as arguments to the more function, the function will read the specified files and page their contents to the host:</span></span>

```
PS> more c:\boot.ini
[boot loader]
timeout=5
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
...
```

## <a name="discarding-output-out-null"></a><span data-ttu-id="2d95f-130">Kimeneti elvetése (élekről Null)</span><span class="sxs-lookup"><span data-stu-id="2d95f-130">Discarding Output (Out-Null)</span></span>

<span data-ttu-id="2d95f-131">A **élekről Null** célja, hogy a parancsmag azonnal elveti fogad semmilyen bemenetet.</span><span class="sxs-lookup"><span data-stu-id="2d95f-131">The **Out-Null** cmdlet is designed to immediately discard any input it receives.</span></span> <span data-ttu-id="2d95f-132">Ez akkor hasznos, ami miatt elvetette a szükségtelen adatokat, mellékhatása futtat egy parancsot kap.</span><span class="sxs-lookup"><span data-stu-id="2d95f-132">This is useful for discarding unnecessary data that you get as a side-effect of running a command.</span></span> <span data-ttu-id="2d95f-133">Amikor beírja a következő parancsot, nem kap semmit újra a parancsot:</span><span class="sxs-lookup"><span data-stu-id="2d95f-133">When type the following command, you do not get anything back from the command:</span></span>

```powershell
Get-Command | Out-Null
```

<span data-ttu-id="2d95f-134">A **élekről Null** parancsmag nem elveti hibakimenet.</span><span class="sxs-lookup"><span data-stu-id="2d95f-134">The **Out-Null** cmdlet does not discard error output.</span></span> <span data-ttu-id="2d95f-135">Például ha ad meg a következő parancsot, megjelenik egy üzenet, amely tájékoztatja, hogy Windows PowerShell nem ismeri fel a "Van – NotACommand":</span><span class="sxs-lookup"><span data-stu-id="2d95f-135">For example, if you enter the following command, a message is displayed informing you that Windows PowerShell does not recognize 'Is-NotACommand':</span></span>

```
PS> Get-Command Is-NotACommand | Out-Null
Get-Command : 'Is-NotACommand' is not recognized as a cmdlet, function, operabl
e program, or script file.
At line:1 char:12
+ Get-Command  <<<< Is-NotACommand | Out-Null
```

## <a name="printing-data-out-printer"></a><span data-ttu-id="2d95f-136">Nyomtatás adatok (Out-nyomtató)</span><span class="sxs-lookup"><span data-stu-id="2d95f-136">Printing Data (Out-Printer)</span></span>

<span data-ttu-id="2d95f-137">Adatok használatával kinyomtathatja a **Out-nyomtató** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2d95f-137">You can print data by using the **Out-Printer** cmdlet.</span></span> <span data-ttu-id="2d95f-138">A **Out-nyomtató** parancsmag fogja használni az alapértelmezett nyomtató, ha nem ad meg a nyomtató neve.</span><span class="sxs-lookup"><span data-stu-id="2d95f-138">The **Out-Printer** cmdlet will use your default printer if you do not provide a printer name.</span></span> <span data-ttu-id="2d95f-139">Bármely Windows-alapú nyomtató használhatja a megjelenített név megadásával.</span><span class="sxs-lookup"><span data-stu-id="2d95f-139">You can use any Windows-based printer by specifying its display name.</span></span> <span data-ttu-id="2d95f-140">Hiba esetén nem kell a nyomtató- vagy a tényleges fizikai nyomtató bármilyen típusú.</span><span class="sxs-lookup"><span data-stu-id="2d95f-140">There is no need for any kind of printer port mapping or even a real physical printer.</span></span> <span data-ttu-id="2d95f-141">Például ha rendelkezik a Microsoft Office dokumentum lemezkép-készítési eszközök telepíteni, elküldheti az adatok képfájlra mutató beírásával:</span><span class="sxs-lookup"><span data-stu-id="2d95f-141">For example, if you have the Microsoft Office document imaging tools installed, you can send the data to an image file by typing:</span></span>

```powershell
Get-Command Get-Command | Out-Printer -Name 'Microsoft Office Document Image Writer'
```

## <a name="saving-data-out-file"></a><span data-ttu-id="2d95f-142">Adatok mentése (out-File)</span><span class="sxs-lookup"><span data-stu-id="2d95f-142">Saving Data (Out-File)</span></span>

<span data-ttu-id="2d95f-143">Egy fájl helyett a konzolablakban kimeneti a használatával küldhet a **out-File** parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="2d95f-143">You can send output to a file instead of the console window by using the **Out-File** cmdlet.</span></span> <span data-ttu-id="2d95f-144">A következő parancsot a folyamatok listáját küld a fájl **C:\\temp\\processlist.txt**:</span><span class="sxs-lookup"><span data-stu-id="2d95f-144">The following command line sends a list of processes to the file **C:\\temp\\processlist.txt**:</span></span>

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt
```

<span data-ttu-id="2d95f-145">Az eredményeket a a **out-File** parancsmag nem lehet várt hagyományos kimenet átirányítása való használatakor.</span><span class="sxs-lookup"><span data-stu-id="2d95f-145">The results of using the **Out-File** cmdlet may not be what you expect if you are used to traditional output redirection.</span></span> <span data-ttu-id="2d95f-146">Szeretné megtudni, annak viselkedését, figyelembe kell venni a környezet, amelyben a **out-File** parancsmag működik.</span><span class="sxs-lookup"><span data-stu-id="2d95f-146">To understand its behavior, you must be aware of the context in which the **Out-File** cmdlet operates.</span></span>

<span data-ttu-id="2d95f-147">Alapértelmezés szerint a **out-File** parancsmag létrehoz egy Unicode-fájlt.</span><span class="sxs-lookup"><span data-stu-id="2d95f-147">By default, the **Out-File** cmdlet creates a Unicode file.</span></span> <span data-ttu-id="2d95f-148">Ez az ajánlott alapértelmezett hosszú távon, de az azt jelenti, hogy eszközöket, amelyek hatással vannak az ASCII-fájlokat nem működik megfelelően az alapértelmezett kimeneti formátum.</span><span class="sxs-lookup"><span data-stu-id="2d95f-148">This is the best default in the long run, but it means that tools that expect ASCII files will not work correctly with the default output format.</span></span> <span data-ttu-id="2d95f-149">ASCII az alapértelmezett kimeneti formátum a használatával módosíthatja a **kódolás** paramétert:</span><span class="sxs-lookup"><span data-stu-id="2d95f-149">You can change the default output format to ASCII by using the **Encoding** parameter:</span></span>

```powershell
Get-Process | Out-File -FilePath C:\temp\processlist.txt -Encoding ASCII
```

<span data-ttu-id="2d95f-150">**Out-File** formátumok tartalmát a konzol kimenete a következőképpen néznek fájlt.</span><span class="sxs-lookup"><span data-stu-id="2d95f-150">**Out-file** formats file contents to look like console output.</span></span> <span data-ttu-id="2d95f-151">Ez azt eredményezi, hogy az eredmény csonkolva lesznek, mint a legtöbb esetben a konzolablakban van.</span><span class="sxs-lookup"><span data-stu-id="2d95f-151">This causes the output to be truncated just as it is in a console window in most circumstances.</span></span> <span data-ttu-id="2d95f-152">Ha például a következő parancsot:</span><span class="sxs-lookup"><span data-stu-id="2d95f-152">For example, if you run the following command:</span></span>

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt
```

<span data-ttu-id="2d95f-153">A kimenet a következőképpen jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="2d95f-153">The output will look like this:</span></span>

```output
CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Add-Content                     Add-Content [-Path] <String[...
Cmdlet          Add-History                     Add-History [[-InputObject] ...
...
```

<span data-ttu-id="2d95f-154">Szeretne kapni, amely nem kényszeríti a sor burkolja szélességét a megfelelő kimeneti, használhatja a **szélesség** paraméterrel megadhatja a vonal vastagsága.</span><span class="sxs-lookup"><span data-stu-id="2d95f-154">To get output that does not force line wraps to match the screen width, you can use the **Width** parameter to specify line width.</span></span> <span data-ttu-id="2d95f-155">Mivel **szélesség** van a 32 bites egész szám paramétert, a maximális megadható értéke 2147483647.</span><span class="sxs-lookup"><span data-stu-id="2d95f-155">Because **Width** is a 32-bit integer parameter, the maximum value it can have is 2147483647.</span></span> <span data-ttu-id="2d95f-156">Írja be a következő, a maximális értékre a vonalvastagság:</span><span class="sxs-lookup"><span data-stu-id="2d95f-156">Type the following to set the line width to this maximum value:</span></span>

```powershell
Get-Command | Out-File -FilePath c:\temp\output.txt -Width 2147483647
```

<span data-ttu-id="2d95f-157">A **out-File** parancsmag akkor hasznos, ha a kimeneti menti, ahogyan kellene rendelkeznek a konzolon.</span><span class="sxs-lookup"><span data-stu-id="2d95f-157">The **Out-File** cmdlet is most useful when you want to save output as it would have displayed on the console.</span></span> <span data-ttu-id="2d95f-158">Kimeneti formátum szabályozásához kell speciális eszközök.</span><span class="sxs-lookup"><span data-stu-id="2d95f-158">For finer control over output format, you need more advanced tools.</span></span> <span data-ttu-id="2d95f-159">Az alábbiakban tájékozódhat a következő fejezet, és néhány információ az objektum adatkezelési lévőket.</span><span class="sxs-lookup"><span data-stu-id="2d95f-159">We will look at those in the next chapter, along with some details about object manipulation.</span></span>