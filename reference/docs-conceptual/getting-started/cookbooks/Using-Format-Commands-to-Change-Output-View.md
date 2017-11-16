---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "Módosítandó formátum parancsaival kimeneti megtekintése"
ms.assetid: 63515a06-a6f7-4175-a45e-a0537f4f6d05
ms.openlocfilehash: 0163fcb21d586fc98902d9bdcfab6fe4eb97c225
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="using-format-commands-to-change-output-view"></a><span data-ttu-id="73b20-103">Módosítandó formátum parancsaival kimeneti megtekintése</span><span class="sxs-lookup"><span data-stu-id="73b20-103">Using Format Commands to Change Output View</span></span>
<span data-ttu-id="73b20-104">A Windows PowerShell-parancsmagok lehetővé teszik annak ellenőrzését, mely tulajdonságok jelennek meg az adott objektumok rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="73b20-104">Windows PowerShell has a set of cmdlets that allow you to control which properties are displayed for particular objects.</span></span> <span data-ttu-id="73b20-105">A parancsmagok neve kezdődhet művelet **formátum**.</span><span class="sxs-lookup"><span data-stu-id="73b20-105">The names of all the cmdlets begin with the verb **Format**.</span></span> <span data-ttu-id="73b20-106">Segítségükkel jelöljön ki egy vagy több tulajdonságot megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="73b20-106">They let you select one or more properties to show.</span></span>

<span data-ttu-id="73b20-107">A **formátum** parancsmagok **formátum kiterjedő**, **Format-List**, **Format-Table**, és **formátum-egyéni**.</span><span class="sxs-lookup"><span data-stu-id="73b20-107">The **Format** cmdlets are **Format-Wide**, **Format-List**, **Format-Table**, and **Format-Custom**.</span></span> <span data-ttu-id="73b20-108">Csak ismerteti, hogy a **formátum kiterjedő**, **Format-List**, és **Format-Table** parancsmagok a felhasználói útmutatóban.</span><span class="sxs-lookup"><span data-stu-id="73b20-108">We will only describe the **Format-Wide**, **Format-List**, and **Format-Table** cmdlets in this user's guide.</span></span>

<span data-ttu-id="73b20-109">Mindegyik formátum parancsmagja rendelkezik, amelyek alkalmazva lesznek, ha nem adja meg a megjelenítendő tulajdonságokat alapértelmezett tulajdonságok.</span><span class="sxs-lookup"><span data-stu-id="73b20-109">Each format cmdlet has default properties that will be used if you do not specify specific properties to display.</span></span> <span data-ttu-id="73b20-110">Minden parancsmagot is ugyanolyan névvel paraméter, **tulajdonság**, mely tulajdonságainak kívánja megjeleníteni.</span><span class="sxs-lookup"><span data-stu-id="73b20-110">Each cmdlet also uses the same parameter name, **Property**, to specify which properties you want to display.</span></span> <span data-ttu-id="73b20-111">Mivel **formátum kiterjedő** csak mutatja egy-egy tulajdonság, a **tulajdonság** paraméter mindössze egyetlen értéket, de a tulajdonság paraméterei **Format-List** és **Format-Table** elfogadja a tulajdonságnevek listáját.</span><span class="sxs-lookup"><span data-stu-id="73b20-111">Because **Format-Wide** only shows a single property, its **Property** parameter only takes a single value, but the property parameters of **Format-List** and **Format-Table** will accept a list of property names.</span></span>

<span data-ttu-id="73b20-112">A parancs **Get-Process - név powershell** két példányban fut a Windows PowerShell, a kapott kimenete a következőképpen néz ki:</span><span class="sxs-lookup"><span data-stu-id="73b20-112">If you use the command **Get-Process -Name powershell** with two instances of Windows PowerShell running, you get output that looks like this:</span></span>

```
Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
    995       9    30308      27996   152     2.73   2760 powershell
    331       9    23284      29084   143     1.06   3448 powershell
```

<span data-ttu-id="73b20-113">Ez a szakasz a többi, hogyan használhatja néhány **formátum** parancsmagok segítségével módosíthatja, miként jelenik meg ez a parancs kimenetét.</span><span class="sxs-lookup"><span data-stu-id="73b20-113">In the rest of this section, we will explore how to use **Format** cmdlets to change the way the output of this command is displayed.</span></span>

### <a name="using-format-wide-for-single-item-output"></a><span data-ttu-id="73b20-114">Egyetlen elem kimeneti formátum kiterjedő használatával</span><span class="sxs-lookup"><span data-stu-id="73b20-114">Using Format-Wide for Single-Item Output</span></span>
<span data-ttu-id="73b20-115">A **formátum kiterjedő** parancsmag, alapértelmezés szerint csak az alapértelmezett tulajdonság az objektum megjeleníti.</span><span class="sxs-lookup"><span data-stu-id="73b20-115">The **Format-Wide** cmdlet, by default, displays only the default property of an object.</span></span> <span data-ttu-id="73b20-116">Az információk is társítva vannak az egyes objektumok egy oszlopban jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="73b20-116">The information associated with each object is displayed in a single column:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide

powershell                              powershell
```

<span data-ttu-id="73b20-117">Azt is megadhatja a nem alapértelmezett tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="73b20-117">You can also specify a non-default property:</span></span>

```
PS> Get-Process -Name powershell | Format-Wide -Property Id

2760                                    3448
```

#### <a name="controlling-format-wide-display-with-column"></a><span data-ttu-id="73b20-118">Ellenőrző formátum kiterjedő megjelenített oszlop</span><span class="sxs-lookup"><span data-stu-id="73b20-118">Controlling Format-Wide Display with Column</span></span>
<span data-ttu-id="73b20-119">Az a **formátum kiterjedő** parancsmag, egy adott tulajdonságra egyszerre csak megjeleníteni.</span><span class="sxs-lookup"><span data-stu-id="73b20-119">With the **Format-Wide** cmdlet, you can only display a single property at a time.</span></span> <span data-ttu-id="73b20-120">Így hasznos, ha csak egy elem soronként egyszerű listák megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="73b20-120">This makes it useful for displaying simple lists that show only one element per line.</span></span> <span data-ttu-id="73b20-121">Ahhoz, hogy egy egyszerű listázása, állítsa a **oszlop** paraméter 1 beírásával:</span><span class="sxs-lookup"><span data-stu-id="73b20-121">To get a simple listing, set the value of the **Column** parameter to 1 by typing:</span></span>

```
Get-Command Format-Wide -Property Name -Column 1
```

### <a name="using-format-list-for-a-list-view"></a><span data-ttu-id="73b20-122">Az adott nézet formátum-lista használatával</span><span class="sxs-lookup"><span data-stu-id="73b20-122">Using Format-List for a List View</span></span>
<span data-ttu-id="73b20-123">A **Format-List** parancsmag formátumban jeleníti meg az objektum a listaelem, minden egyes tulajdonsággal címkével, és külön sorban jelenik meg:</span><span class="sxs-lookup"><span data-stu-id="73b20-123">The **Format-List** cmdlet displays an object in the form of a listing, with each property labeled and displayed on a separate line:</span></span>

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

<span data-ttu-id="73b20-124">Megadhatja, hogy a kívánt annyi tulajdonságokat:</span><span class="sxs-lookup"><span data-stu-id="73b20-124">You can specify as many properties as you want:</span></span>

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

#### <a name="getting-detailed-information-by-using-format-list-with-wildcards"></a><span data-ttu-id="73b20-125">A helyettesítő karakterek formátum-lista használatával beolvasásakor részletes információk</span><span class="sxs-lookup"><span data-stu-id="73b20-125">Getting Detailed Information by Using Format-List with Wildcards</span></span>
<span data-ttu-id="73b20-126">A **Format-List** parancsmag lehetővé teszi, hogy egy helyettesítő értékeként a **tulajdonság** paraméter.</span><span class="sxs-lookup"><span data-stu-id="73b20-126">The **Format-List** cmdlet lets you use a wildcard as the value of its **Property** parameter.</span></span> <span data-ttu-id="73b20-127">Ez lehetővé teszi a részletes információk megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="73b20-127">This lets you display detailed information.</span></span> <span data-ttu-id="73b20-128">Objektumok gyakran, például a több információt van szüksége, ezért a Windows PowerShell nem szerepelnek alapértelmezés szerint minden tulajdonság értékével.</span><span class="sxs-lookup"><span data-stu-id="73b20-128">Often, objects include more information than you need, which is why Windows PowerShell does not show all property values by default.</span></span> <span data-ttu-id="73b20-129">Az összes objektum tulajdonságainak megjelenítéséhez használja a **Format-List-tulajdonság \&#42;** parancsot.</span><span class="sxs-lookup"><span data-stu-id="73b20-129">To show all of properties of an object, use the **Format-List -Property \&#42;** command.</span></span> <span data-ttu-id="73b20-130">A következő parancsot a folyamat egyetlen kimeneti több mint 60 sort hoz létre:</span><span class="sxs-lookup"><span data-stu-id="73b20-130">The following command generates over 60 lines of output for a single process:</span></span>

```
Get-Process -Name powershell | Format-List -Property *
```

<span data-ttu-id="73b20-131">Bár a **Format-List** parancs akkor hasznos, ha a bemutató részletes, ha azt szeretné, hogy hány elemet tartalmazó kimeneti áttekintése, egy egyszerűbb táblázatos nézet gyakran több hasznos.</span><span class="sxs-lookup"><span data-stu-id="73b20-131">Although the **Format-List** command is useful for showing detail, if you want an overview of output that includes many items, a simpler tabular view is often more useful.</span></span>

### <a name="using-format-table-for-tabular-output"></a><span data-ttu-id="73b20-132">Táblázat formázása használatával táblázatos kimenet</span><span class="sxs-lookup"><span data-stu-id="73b20-132">Using Format-Table for Tabular Output</span></span>
<span data-ttu-id="73b20-133">Használatakor a **Format-Table** nem tulajdonságnevek parancsmagnak megadott formázásához kimenetét a **Get-Process** parancsban, ugyanúgy kimeneti, végrehajtása formázás nélkül teszi elérhetővé.</span><span class="sxs-lookup"><span data-stu-id="73b20-133">If you use the **Format-Table** cmdlet with no property names specified to format the output of the **Get-Process** command, you get exactly the same output as you do without performing any formatting.</span></span> <span data-ttu-id="73b20-134">Oka az, hogy folyamatok táblázatos formában, általában megjelenik, amelyek a legtöbb Windows PowerShell-objektum.</span><span class="sxs-lookup"><span data-stu-id="73b20-134">The reason is that processes are usually displayed in a tabular format, as are most Windows PowerShell objects.</span></span>

```
PS> Get-Process -Name powershell | Format-Table

Handles  NPM(K)    PM(K)      WS(K) VM(M)   CPU(s)     Id ProcessName
-------  ------    -----      ----- -----   ------     -- -----------
   1488       9    31568      29460   152     3.53   2760 powershell
    332       9    23140        632   141     1.06   3448 powershell
```

#### <a name="improving-format-table-output-autosize"></a><span data-ttu-id="73b20-135">Táblázat formázása kimeneti (AutoSize) javítása</span><span class="sxs-lookup"><span data-stu-id="73b20-135">Improving Format-Table Output (AutoSize)</span></span>
<span data-ttu-id="73b20-136">Bár a táblázatos nézet akkor hasznos, ha nagy mennyiségű összehasonlítható információk megjelenítése, ha a megjelenítési túl széleskörű, az adatok értelmezése nehéz lehet.</span><span class="sxs-lookup"><span data-stu-id="73b20-136">Although a tabular view is useful for displaying a lot of comparable information, it may be difficult to interpret if the display is too narrow for the data.</span></span> <span data-ttu-id="73b20-137">Például ha folyamat elérési útját, Azonosítóját, nevét és vállalati megjelenítéséhez, akkor érhető el csonkolt kimeneti folyamat elérési útját és a vállalat oszlop:</span><span class="sxs-lookup"><span data-stu-id="73b20-137">For example, if you try to display process path, ID, name, and company, you get truncated output for the process path and the company column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company

Path                Name                                 Id Company
----                ----                                 -- -------
C:\Program Files... powershell                         2836 Microsoft Corpor...
```

<span data-ttu-id="73b20-138">Ha megadja a **AutoSize** paraméter futtatásakor a **Format-Table** parancsot a Windows PowerShell oszlopszélességet is szeretné megjeleníteni a tényleges adatai alapján számítja ki.</span><span class="sxs-lookup"><span data-stu-id="73b20-138">If you specify the **AutoSize** parameter when you run the **Format-Table** command, Windows PowerShell will calculate column widths based on the actual data you are going to display.</span></span> <span data-ttu-id="73b20-139">Ez lehetővé teszi a **elérési** olvasható oszlop, de a vállalati oszlop marad csonkolt:</span><span class="sxs-lookup"><span data-stu-id="73b20-139">This makes the **Path** column readable, but the company column remains truncated:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Path,Name,Id,Company -
AutoSize

Path                                                    Name         Id Company
----                                                    ----         -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe powershell 2836 Micr...
```

<span data-ttu-id="73b20-140">A **Format-Table** parancsmag továbbra is előfordulhat, hogy csonkolja adatokat, de ez csak elvégzi, a képernyő végén.</span><span class="sxs-lookup"><span data-stu-id="73b20-140">The **Format-Table** cmdlet might still truncate data, but it will only do so at the end of the screen.</span></span> <span data-ttu-id="73b20-141">Tulajdonságok, nem az utolsó jelenik meg, adta mértékű mérete, a leghosszabb adatelem helyes megjelenítéséhez van szükségük.</span><span class="sxs-lookup"><span data-stu-id="73b20-141">Properties, other than the last one displayed, are given as much size as they need for their longest data element to display correctly.</span></span> <span data-ttu-id="73b20-142">Láthatja, hogy vállalatnév látható, de a elérési utat a függvény egésszé csonkítja helyeinek felcserélése, ha **elérési** és **vállalati** a a **tulajdonság** értékek listájából:</span><span class="sxs-lookup"><span data-stu-id="73b20-142">You can see that company name is visible but path is truncated if you swap the locations of **Path** and **Company** in the **Property** value list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Name,Id,Path -
AutoSize

Company               Name         Id Path
-------               ----         -- ----
Microsoft Corporation powershell 2836 C:\Program Files\Windows PowerShell\v1...
```

<span data-ttu-id="73b20-143">A **Format-Table** parancs feltételezi, hogy a nearer egy tulajdonság az keresésitulajdonság-lista elejére annál a fontos.</span><span class="sxs-lookup"><span data-stu-id="73b20-143">The **Format-Table** command assumes that the nearer a property is to the beginning of the property list, the more important it is.</span></span> <span data-ttu-id="73b20-144">A rendszer megkísérli a kezdő legközelebbi tulajdonságok megjelenítése teljesen.</span><span class="sxs-lookup"><span data-stu-id="73b20-144">So it attempts to display the properties nearest the beginning completely.</span></span> <span data-ttu-id="73b20-145">Ha a **Format-Table** parancs nem jeleníti meg az összes tulajdonság, az egyes oszlopok eltávolítása a képernyőt, és adja meg a figyelmeztetést.</span><span class="sxs-lookup"><span data-stu-id="73b20-145">If the **Format-Table** command cannot display all the properties, it will remove some columns from the display and provide a warning.</span></span> <span data-ttu-id="73b20-146">Ha ez a viselkedés látható **neve** a lista utolsó tulajdonság:</span><span class="sxs-lookup"><span data-stu-id="73b20-146">You can see this behavior if you make **Name** the last property in the list:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Property Company,Path,Id,Name -
AutoSize

WARNING: column "Name" does not fit into the display and was removed.

Company               Path                                                    I
                                                                              d
-------               ----                                                    -
Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\powershell.exe 6
```

<span data-ttu-id="73b20-147">A fenti kimenetben azonosító oszlopban a függvény egésszé csonkítja abba, hogy felelnek meg az átjáróra a listában, és az oszlopfejlécek vannak halmozott.</span><span class="sxs-lookup"><span data-stu-id="73b20-147">In the output above, the ID column is truncated to make it fit into the listing, and the column headings are stacked up.</span></span> <span data-ttu-id="73b20-148">Automatikus méretezés, az oszlopok nem mindig tegye azt szeretné.</span><span class="sxs-lookup"><span data-stu-id="73b20-148">Automatically resizing the columns does not always do what you want.</span></span>

#### <a name="wrapping-format-table-output-in-columns-wrap"></a><span data-ttu-id="73b20-149">Alkalmazásburkoló táblázat formázása kimeneti oszlopok (sortörés)</span><span class="sxs-lookup"><span data-stu-id="73b20-149">Wrapping Format-Table Output in Columns (Wrap)</span></span>
<span data-ttu-id="73b20-150">Beállíthatja, hogy a hosszú **Format-Table** burkolása belül a megjelenítendő oszlop használatával adatok a **burkolása** paraméter.</span><span class="sxs-lookup"><span data-stu-id="73b20-150">You can force lengthy **Format-Table** data to wrap within its display column by using the **Wrap** parameter.</span></span> <span data-ttu-id="73b20-151">Használja a **burkolása** paraméter csak feltétlenül nem várt, mert az alapértelmezett beállítást használja, ha nem is meg **AutoSize**:</span><span class="sxs-lookup"><span data-stu-id="73b20-151">Using the **Wrap** parameter alone will not necessarily do what you expect, since it uses default settings if you do not also specify **AutoSize**:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -Property Name,Id,Company,
Path

Name                                 Id Company             Path
----                                 -- -------             ----
powershell                         2836 Microsoft Corporati C:\Program Files\Wi
                                        on                  ndows PowerShell\v1
                                                            .0\powershell.exe
```

<span data-ttu-id="73b20-152">Egy használatának előnye a **burkolása** önmagában paraméter megadása, hogy azt ne lassítsa le nagyon kevés feldolgozása.</span><span class="sxs-lookup"><span data-stu-id="73b20-152">An advantage of using the **Wrap** parameter by itself is that it does not slow down processing very much.</span></span> <span data-ttu-id="73b20-153">Egy rekurzív felsoroló nagy directory rendszert, akkor előfordulhat, hogy nagyon hosszú időt vehet igénybe, és nagy mennyiségű memóriát használja az első kimeneti elemek megjelenítése, ha használata előtt **AutoSize**.</span><span class="sxs-lookup"><span data-stu-id="73b20-153">If you perform a recursive file listing of a large directory system, it might take a very long time and use a lot of memory before displaying the first output items if you use **AutoSize**.</span></span>

<span data-ttu-id="73b20-154">Ha aggódik nem rendszerterhelés, majd **AutoSize** jól működik a **burkolása** paraméter.</span><span class="sxs-lookup"><span data-stu-id="73b20-154">If you are not concerned about system load, then **AutoSize** works well with the **Wrap** parameter.</span></span> <span data-ttu-id="73b20-155">A kezdeti oszlopok vannak mindig engedélyezett módon elemek megjelenítése egy sorban, ugyanúgy, mint ha a szükséges mértékű szélesség **AutoSize** nélkül a **burkolása** paraméter.</span><span class="sxs-lookup"><span data-stu-id="73b20-155">The initial columns are always allotted as much width as they need to display items on one line, just as when you specify **AutoSize** without the **Wrap** parameter.</span></span> <span data-ttu-id="73b20-156">Az egyetlen különbség az, hogy az utolsó oszlopban lesz kell csomagolni, ha szükséges:</span><span class="sxs-lookup"><span data-stu-id="73b20-156">The only difference is that the final column will be wrapped if necessary:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Company,Path

Name         Id Company               Path
----         -- -------               ----
powershell 2836 Microsoft Corporation C:\Program Files\Windows PowerShell\v1.0\
                                      powershell.exe
```

<span data-ttu-id="73b20-157">Egyes oszlopok előfordulhat nem jelenik meg, ha először adja meg a legszélesebb oszlopok, hogy először a legkisebb adatelemek megadását legbiztonságosabb.</span><span class="sxs-lookup"><span data-stu-id="73b20-157">Some columns might not be displayed if you specify the widest columns first, so it is safest to specify the smallest data elements first.</span></span> <span data-ttu-id="73b20-158">A következő példában azt adja meg a rendkívül nagy elérésiút-elem első, és még az alkalmazásburkoló, azt még elveszíti a végleges **neve** oszlop:</span><span class="sxs-lookup"><span data-stu-id="73b20-158">In the following example, we specify the extremely wide path element first, and even with wrapping, we still lose the final **Name** column:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Path,I
d,Company,Name

WARNING: column "Name" does not fit into the display and was removed.

Path                                                      Id Company
----                                                      -- -------
C:\Program Files\Windows PowerShell\v1.0\powershell.exe 2836 Microsoft Corporat
                                                             ion
```

#### <a name="organizing-table-output--groupby"></a><span data-ttu-id="73b20-159">Táblázatos kimenete rendszerezéséhez (-GroupBy)</span><span class="sxs-lookup"><span data-stu-id="73b20-159">Organizing Table Output (-GroupBy)</span></span>
<span data-ttu-id="73b20-160">Egy másik hasznos táblázatos kimeneti vezérlővel paramétere **GroupBy**.</span><span class="sxs-lookup"><span data-stu-id="73b20-160">Another useful parameter for tabular output control is **GroupBy**.</span></span> <span data-ttu-id="73b20-161">Már táblázatos listaelemek különösen nehezen összehasonlítása lehet.</span><span class="sxs-lookup"><span data-stu-id="73b20-161">Longer tabular listings in particular may be hard to compare.</span></span> <span data-ttu-id="73b20-162">A **GroupBy** paraméter kimeneti tulajdonság értéke alapján csoportosítja.</span><span class="sxs-lookup"><span data-stu-id="73b20-162">The **GroupBy** parameter groups output based on a property value.</span></span> <span data-ttu-id="73b20-163">Például azt csoportosíthatja, a vállalat értéket a tulajdonság listaelem kihagyásával könnyebb ellenőrzésre, vállalat által folyamatok:</span><span class="sxs-lookup"><span data-stu-id="73b20-163">For example, we can group processes by company for easier inspection, omitting the company value from the property listing:</span></span>

```
PS> Get-Process -Name powershell | Format-Table -Wrap -AutoSize -Property Name,I
d,Path -GroupBy Company

   Company: Microsoft Corporation

Name         Id Path
----         -- ----
powershell 1956 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
powershell 2656 C:\Program Files\Windows PowerShell\v1.0\powershell.exe
```

