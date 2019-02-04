---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: A kimeneti nézet módosítása formázási parancsokkal
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 97d3a9e04abb61bb80a0b8c67d9fb9e885a0b91b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55686452"
---
# <a name="using-format-commands-to-change-output-view"></a><span data-ttu-id="d2455-103">A kimeneti nézet módosítása formázási parancsokkal</span><span class="sxs-lookup"><span data-stu-id="d2455-103">Using Format Commands to Change Output View</span></span>

<span data-ttu-id="d2455-104">Windows PowerShell-parancsmagokat, amelyek lehetővé teszik annak ellenőrzését, milyen tulajdonságok jelennek meg az adott objektumok rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="d2455-104">Windows PowerShell has a set of cmdlets that allow you to control which properties are displayed for particular objects.</span></span> <span data-ttu-id="d2455-105">A parancsmagok minden kezdődik-e a művelet **formátum**.</span><span class="sxs-lookup"><span data-stu-id="d2455-105">The names of all the cmdlets begin with the verb **Format**.</span></span> <span data-ttu-id="d2455-106">Segítségével válassza ki egy vagy több tulajdonságának megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="d2455-106">They let you select one or more properties to show.</span></span>

<span data-ttu-id="d2455-107">A **formátum** parancsmagok a következők **formátum kiterjedő**, **Format-List**, **Format-Table**, és **formátumban – egyéni**.</span><span class="sxs-lookup"><span data-stu-id="d2455-107">The **Format** cmdlets are **Format-Wide**, **Format-List**, **Format-Table**, and **Format-Custom**.</span></span> <span data-ttu-id="d2455-108">Csak bemutatunk néhányat a **formátum kiterjedő**, **Format-List**, és **Format-Table** parancsmagok a felhasználói útmutató a.</span><span class="sxs-lookup"><span data-stu-id="d2455-108">We will only describe the **Format-Wide**, **Format-List**, and **Format-Table** cmdlets in this user's guide.</span></span>

<span data-ttu-id="d2455-109">Minden egyes formátum parancsmag rendelkezik, amelyek alkalmazva lesznek, ha nem adja meg a konkrét tulajdonságok megjeleníthető alapértelmezett tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="d2455-109">Each format cmdlet has default properties that will be used if you do not specify specific properties to display.</span></span> <span data-ttu-id="d2455-110">Minden parancsmagot is használ ugyanabban a paraméternév megadásához, **tulajdonság**, hogy melyik megjeleníteni kívánt tulajdonságokat határozza meg.</span><span class="sxs-lookup"><span data-stu-id="d2455-110">Each cmdlet also uses the same parameter name, **Property**, to specify which properties you want to display.</span></span> <span data-ttu-id="d2455-111">Mivel **formátum kiterjedő** csak jelenik meg, hogy egy adott tulajdonságra a **tulajdonság** paraméter mindössze egyetlen érték, de a tulajdonság paraméterei **Format-List** és **Format-Table** elfogadja a tulajdonság nevének listáját.</span><span class="sxs-lookup"><span data-stu-id="d2455-111">Because **Format-Wide** only shows a single property, its **Property** parameter only takes a single value, but the property parameters of **Format-List** and **Format-Table** will accept a list of property names.</span></span>

<span data-ttu-id="d2455-112">Ha a parancs **Get-Process - név powershell** két példánya fut a Windows PowerShell, a következőket kínálja a következőhöz hasonló kimenetet:</span><span class="sxs-lookup"><span data-stu-id="d2455-112">If you use the command **Get-Process -Name powershell** with two instances of Windows PowerShell running, you get output that looks like this:</span></span>

```output
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

<span data-ttu-id="d2455-113">Ez a szakasz a többi tárgyaljuk fog használata **formátum** parancsmagok megváltoztatni a parancs kimenetének jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="d2455-113">In the rest of this section, we will explore how to use **Format** cmdlets to change the way the output of this command is displayed.</span></span>

### <a name="using-format-wide-for-single-item-output"></a><span data-ttu-id="d2455-114">Egyetlen elemből kimeneti formátum kiterjedő használatával</span><span class="sxs-lookup"><span data-stu-id="d2455-114">Using Format-Wide for Single-Item Output</span></span>

<span data-ttu-id="d2455-115">A **formátum kiterjedő** parancsmag alapértelmezés szerint jeleníti meg az objektumok csak az alapértelmezett tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="d2455-115">The **Format-Wide** cmdlet, by default, displays only the default property of an object.</span></span> <span data-ttu-id="d2455-116">Az egyes objektumok társított információkat egy oszlopban jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="d2455-116">The information associated with each object is displayed in a single column:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

<span data-ttu-id="d2455-117">Megadhat egy nem alapértelmezett tulajdonságot is:</span><span class="sxs-lookup"><span data-stu-id="d2455-117">You can also specify a non-default property:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a><span data-ttu-id="d2455-118">Formátum kiterjedő megjelenítendő oszlop szabályozása</span><span class="sxs-lookup"><span data-stu-id="d2455-118">Controlling Format-Wide Display with Column</span></span>

<span data-ttu-id="d2455-119">Az a **formátum kiterjedő** parancsmagot egyszerre csak megjelenítheti egy-egy tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="d2455-119">With the **Format-Wide** cmdlet, you can only display a single property at a time.</span></span> <span data-ttu-id="d2455-120">Így egyszerű listák, azt mutatják be, soronként csak egy elem megjelenítése esetén hasznos.</span><span class="sxs-lookup"><span data-stu-id="d2455-120">This makes it useful for displaying simple lists that show only one element per line.</span></span> <span data-ttu-id="d2455-121">Egyszerű lista kapni, állítsa a **oszlop** paraméter 1 beírásával:</span><span class="sxs-lookup"><span data-stu-id="d2455-121">To get a simple listing, set the value of the **Column** parameter to 1 by typing:</span></span>

```powershell
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a><span data-ttu-id="d2455-122">Az adott nézet használata a Format-List</span><span class="sxs-lookup"><span data-stu-id="d2455-122">Using Format-List for a List View</span></span>

<span data-ttu-id="d2455-123">A **Format-List** címkével ellátott és a egy külön sorban jelenik meg minden egyes tulajdonság parancsmag megjeleníti az egy lista formájában objektum:</span><span class="sxs-lookup"><span data-stu-id="d2455-123">The **Format-List** cmdlet displays an object in the form of a listing, with each property labeled and displayed on a separate line:</span></span>

```
PS> Get-Process -Name powershell | Format-List

Id      : 2760
Handles : 1242
CPU     : 3.03125
Name    : powershell

Id      : 3448
Handles : 328
CPU     : 1.0625
Name    : powershell
```

<span data-ttu-id="d2455-124">A kívánt számú tulajdonságait is megadhatja:</span><span class="sxs-lookup"><span data-stu-id="d2455-124">You can specify as many properties as you want:</span></span>

```
PS> Get-Process -Name powershell | Format-List -Property ProcessName,FileVersion
,StartTime,Id

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:42:00
Id          : 2760

ProcessName : powershell
FileVersion : 1.0.9567.1
StartTime   : 2006-05-24 13:54:28
Id          : 3448
```

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a><span data-ttu-id="d2455-125">Kezdeti lépéseket ismertető részletes információkat a helyettesítő karakterek használatával Format-List</span><span class="sxs-lookup"><span data-stu-id="d2455-125">Getting Detailed Information by Using Format-List with Wildcards</span></span>

<span data-ttu-id="d2455-126">A **Format-List** parancsmag használatát teszi lehetővé egy helyettesítő karaktert tartalmazó értéket annak **tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="d2455-126">The **Format-List** cmdlet lets you use a wildcard as the value of its **Property** parameter.</span></span> <span data-ttu-id="d2455-127">Ezáltal részletes információk megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="d2455-127">This lets you display detailed information.</span></span> <span data-ttu-id="d2455-128">Objektumok tartozhat több információt van szüksége, ezért a Windows PowerShell nem jeleníti meg az összes tulajdonságértékek alapértelmezés szerint.</span><span class="sxs-lookup"><span data-stu-id="d2455-128">Often, objects include more information than you need, which is why Windows PowerShell does not show all property values by default.</span></span> <span data-ttu-id="d2455-129">Az összes objektum tulajdonságainak megjelenítéséhez használja a **Format-List-tulajdonság \&#42;** parancsot.</span><span class="sxs-lookup"><span data-stu-id="d2455-129">To show all of properties of an object, use the **Format-List -Property \&#42;** command.</span></span> <span data-ttu-id="d2455-130">A következő parancsot a folyamat egyetlen kimeneti több mint 60 sor hoz létre:</span><span class="sxs-lookup"><span data-stu-id="d2455-130">The following command generates over 60 lines of output for a single process:</span></span>

```powershell
Get-Process -Name powershell | Format-List -Property *
```

<span data-ttu-id="d2455-131">Bár a **Format-List** parancs hasznos, hogy a részletes, ha azt szeretné, hogy hány elemet tartalmazó kimeneti áttekintése, egy egyszerűbb táblázatos nézet gyakran több hasznos.</span><span class="sxs-lookup"><span data-stu-id="d2455-131">Although the **Format-List** command is useful for showing detail, if you want an overview of output that includes many items, a simpler tabular view is often more useful.</span></span>

### <a name="using-format-table-for-tabular-output"></a><span data-ttu-id="d2455-132">A táblázatos kimenet Format-Table használatával</span><span class="sxs-lookup"><span data-stu-id="d2455-132">Using Format-Table for Tabular Output</span></span>

<span data-ttu-id="d2455-133">Ha használja a **Format-Table** nincs tulajdonságnevekkel rendelkező parancsmag kimenetének formázására megadott a **Get-Process** parancsot, ugyanúgy mint formázás végrehajtása nélkül kimeneti kap.</span><span class="sxs-lookup"><span data-stu-id="d2455-133">If you use the **Format-Table** cmdlet with no property names specified to format the output of the **Get-Process** command, you get exactly the same output as you do without performing any formatting.</span></span> <span data-ttu-id="d2455-134">Az oka, hogy a folyamatok általában megjelenik, táblázatos formában, amelyek a legtöbb Windows PowerShell-objektumok.</span><span class="sxs-lookup"><span data-stu-id="d2455-134">The reason is that processes are usually displayed in a tabular format, as are most Windows PowerShell objects.</span></span>

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a><span data-ttu-id="d2455-135">Format-Table kimeneti (automatikus méretezése) javítása</span><span class="sxs-lookup"><span data-stu-id="d2455-135">Improving Format-Table Output (AutoSize)</span></span>

<span data-ttu-id="d2455-136">Bár egy táblázatos nézetben sok összehasonlítható adat megjelenítése esetén hasznos, nehéz értelmezni, ha a megjelenített adatok túl keskeny lehet.</span><span class="sxs-lookup"><span data-stu-id="d2455-136">Although a tabular view is useful for displaying a lot of comparable information, it may be difficult to interpret if the display is too narrow for the data.</span></span> <span data-ttu-id="d2455-137">Például ha folyamat útvonala, Azonosítóját, nevét és a vállalat megjelenítéséhez, megkapja rövidített kimenet a folyamat elérési út és a vállalati oszlopot:</span><span class="sxs-lookup"><span data-stu-id="d2455-137">For example, if you try to display process path, ID, name, and company, you get truncated output for the process path and the company column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

<span data-ttu-id="d2455-138">Ha megad a **AutoSize** paramétert, ha futtatja a **Format-Table** parancsot a Windows PowerShell Oszlopszélességek szeretné megjeleníteni a tényleges adatok alapján számítja ki.</span><span class="sxs-lookup"><span data-stu-id="d2455-138">If you specify the **AutoSize** parameter when you run the **Format-Table** command, Windows PowerShell will calculate column widths based on the actual data you are going to display.</span></span> <span data-ttu-id="d2455-139">Ez lehetővé teszi a **elérési út** olvasható oszlopot, de a céges oszlopot marad csonkolva:</span><span class="sxs-lookup"><span data-stu-id="d2455-139">This makes the **Path** column readable, but the company column remains truncated:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

<span data-ttu-id="d2455-140">A **Format-Table** parancsmag továbbra is előfordulhat, hogy csonkolja az adatokat, de azt fogja csak ehhez a képernyő alján.</span><span class="sxs-lookup"><span data-stu-id="d2455-140">The **Format-Table** cmdlet might still truncate data, but it will only do so at the end of the screen.</span></span> <span data-ttu-id="d2455-141">Tulajdonságok, nem az utolsó jelenik meg, akár mérete, a leghosszabb adatelem helyes megjelenítéséhez az igény szerinti vannak megadva.</span><span class="sxs-lookup"><span data-stu-id="d2455-141">Properties, other than the last one displayed, are given as much size as they need for their longest data element to display correctly.</span></span> <span data-ttu-id="d2455-142">Láthatja, hogy cég neve látható, de ha, cseréje a helyek, a rendszer csonkolja a elérési utat **elérési** és **vállalati** a a **tulajdonság** tartományérték-listája:</span><span class="sxs-lookup"><span data-stu-id="d2455-142">You can see that company name is visible but path is truncated if you swap the locations of **Path** and **Company** in the **Property** value list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

<span data-ttu-id="d2455-143">A **Format-Table** parancs feltételezi, hogy a nearer tulajdonságot, hogy a tulajdonságlistában elején minél többet a fontos.</span><span class="sxs-lookup"><span data-stu-id="d2455-143">The **Format-Table** command assumes that the nearer a property is to the beginning of the property list, the more important it is.</span></span> <span data-ttu-id="d2455-144">Így megkísérli a legközelebbi elején a tulajdonságainak megjelenítéséhez teljesen.</span><span class="sxs-lookup"><span data-stu-id="d2455-144">So it attempts to display the properties nearest the beginning completely.</span></span> <span data-ttu-id="d2455-145">Ha a **Format-Table** parancs nem jeleníthető meg az összes tulajdonság, az egyes oszlopok eltávolítása a képernyőt, és adja meg a figyelmeztetést.</span><span class="sxs-lookup"><span data-stu-id="d2455-145">If the **Format-Table** command cannot display all the properties, it will remove some columns from the display and provide a warning.</span></span> <span data-ttu-id="d2455-146">Ha választja ki láthatja ezt a viselkedést **neve** az utolsó tulajdonság a listában:</span><span class="sxs-lookup"><span data-stu-id="d2455-146">You can see this behavior if you make **Name** the last property in the list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

<span data-ttu-id="d2455-147">A fenti kimenetben a rendszer csonkolja az azonosító oszlop, hogy a listaelem illik, és az oszlopfejlécek vannak halmozott.</span><span class="sxs-lookup"><span data-stu-id="d2455-147">In the output above, the ID column is truncated to make it fit into the listing, and the column headings are stacked up.</span></span> <span data-ttu-id="d2455-148">Automatikus méretezés, az oszlopok nem mindig mit szeretne.</span><span class="sxs-lookup"><span data-stu-id="d2455-148">Automatically resizing the columns does not always do what you want.</span></span>

#### <a name="wrapping-format-table-output-in-columns-wrap"></a><span data-ttu-id="d2455-149">Alkalmazásburkoló Format-Table kimeneti oszlopok (sortörés)</span><span class="sxs-lookup"><span data-stu-id="d2455-149">Wrapping Format-Table Output in Columns (Wrap)</span></span>

<span data-ttu-id="d2455-150">Kényszerítheti hosszadalmas **Format-Table** burkolása belül a megjelenítendő oszlop használatával az adatokat a **burkolása** paraméter.</span><span class="sxs-lookup"><span data-stu-id="d2455-150">You can force lengthy **Format-Table** data to wrap within its display column by using the **Wrap** parameter.</span></span> <span data-ttu-id="d2455-151">Használatával a **burkolása** önálló paraméter nem feltétlenül tesz program működésére nézve, mivel ha akkor is nem ad meg alapértelmezett beállításokat használja **AutoSize**:</span><span class="sxs-lookup"><span data-stu-id="d2455-151">Using the **Wrap** parameter alone will not necessarily do what you expect, since it uses default settings if you do not also specify **AutoSize**:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

<span data-ttu-id="d2455-152">Egy használatának előnye a **burkolása** paraméter önmagában az, hogy azt ne lassítsa le nagy feldolgozási.</span><span class="sxs-lookup"><span data-stu-id="d2455-152">An advantage of using the **Wrap** parameter by itself is that it does not slow down processing very much.</span></span> <span data-ttu-id="d2455-153">Ha hajt végre egy nagy directory rendszer rekurzív fájl listája, akkor előfordulhat, hogy nagyon hosszú időt vehet igénybe, és sok memóriát használni, mielőtt az első kimeneti elemek megjelenítése, ha **AutoSize**.</span><span class="sxs-lookup"><span data-stu-id="d2455-153">If you perform a recursive file listing of a large directory system, it might take a very long time and use a lot of memory before displaying the first output items if you use **AutoSize**.</span></span>

<span data-ttu-id="d2455-154">Ha még nem érintett rendszer terhelési, majd **AutoSize** jól működik a **burkolása** paraméter.</span><span class="sxs-lookup"><span data-stu-id="d2455-154">If you are not concerned about system load, then **AutoSize** works well with the **Wrap** parameter.</span></span> <span data-ttu-id="d2455-155">A kezdeti oszlopokat mindig van leállítaná a lehető szélesség elemek megjelenítéséhez egy sorban, ugyanúgy, mint ha igény szerinti **AutoSize** nélkül a **burkolása** paraméter.</span><span class="sxs-lookup"><span data-stu-id="d2455-155">The initial columns are always allotted as much width as they need to display items on one line, just as when you specify **AutoSize** without the **Wrap** parameter.</span></span> <span data-ttu-id="d2455-156">Az egyetlen különbség, hogy az utolsó oszlopban besorolva szükség esetén:</span><span class="sxs-lookup"><span data-stu-id="d2455-156">The only difference is that the final column will be wrapped if necessary:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

<span data-ttu-id="d2455-157">Egyes oszlopok előfordulhat, hogy nem kell jelenik meg, ha először adja meg a legszélesebb körű oszlopokat, hogy legyen legbiztosabb megoldás, ha először adja meg a legkisebb adatelemeket.</span><span class="sxs-lookup"><span data-stu-id="d2455-157">Some columns might not be displayed if you specify the widest columns first, so it is safest to specify the smallest data elements first.</span></span> <span data-ttu-id="d2455-158">A következő példában azt adja meg a rendkívül széles elérésiút-elem először, és még az alkalmazásburkoló, hogy továbbra is elveszíti a végső **neve** oszlopban:</span><span class="sxs-lookup"><span data-stu-id="d2455-158">In the following example, we specify the extremely wide path element first, and even with wrapping, we still lose the final **Name** column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a><span data-ttu-id="d2455-159">Tábla kimeneti rendszerezése (-GroupBy)</span><span class="sxs-lookup"><span data-stu-id="d2455-159">Organizing Table Output (-GroupBy)</span></span>

<span data-ttu-id="d2455-160">Táblázatos kimenet ellenőrzése egy másik hasznos paraméter értéke nem **GroupBy**.</span><span class="sxs-lookup"><span data-stu-id="d2455-160">Another useful parameter for tabular output control is **GroupBy**.</span></span> <span data-ttu-id="d2455-161">Már táblázatos listaelemek különösen nehezen hasonlítsa össze lehet.</span><span class="sxs-lookup"><span data-stu-id="d2455-161">Longer tabular listings in particular may be hard to compare.</span></span> <span data-ttu-id="d2455-162">A **GroupBy** paraméter kimenete egy tulajdonság értéke alapján csoportosítja.</span><span class="sxs-lookup"><span data-stu-id="d2455-162">The **GroupBy** parameter groups output based on a property value.</span></span> <span data-ttu-id="d2455-163">Például hogy csoportosíthatók a folyamatok könnyebb vizsgálatra kihagyása a cég érték a tulajdonság lista a vállalat által:</span><span class="sxs-lookup"><span data-stu-id="d2455-163">For example, we can group processes by company for easier inspection, omitting the company value from the property listing:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```