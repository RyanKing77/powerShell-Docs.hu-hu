---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumok eltávolítása az adatcsatornából Where-Object
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: c060b93a3823be26ad6c7757acc633bb4fc2fcfa
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404531"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="881e0-103">Objektumok eltávolítása az adatcsatornából (Where-Object)</span><span class="sxs-lookup"><span data-stu-id="881e0-103">Removing Objects from the Pipeline (Where-Object)</span></span>

<span data-ttu-id="881e0-104">A Windows PowerShellben Ön gyakran hozza létre és azt szeretné, hogy egy folyamat több objektum adják át.</span><span class="sxs-lookup"><span data-stu-id="881e0-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="881e0-105">Adott lehetőségével szűkítheti a megjelenített objektumok tulajdonságait is megadhat a **formátum** parancsmagok, de ez nem segíthetnek a probléma, és a teljes objektumok eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="881e0-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="881e0-106">Érdemes a folyamat vége előtt-objektumok szűrése, így elvégezhető műveletek a kezdetben által létrehozott objektumok egy részhalmazára.</span><span class="sxs-lookup"><span data-stu-id="881e0-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="881e0-107">Windows PowerShell tartalmaz egy `Where-Object` parancsmagot, amely lehetővé teszi, hogy a folyamat minden egyes objektum tesztelése, és csak azt adják át a folyamat megfelel egy adott teszt feltételt.</span><span class="sxs-lookup"><span data-stu-id="881e0-107">Windows PowerShell includes a `Where-Object` cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="881e0-108">Objektumok, amelyek nem adnak át a vizsgálat a folyamat törlődnek.</span><span class="sxs-lookup"><span data-stu-id="881e0-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="881e0-109">A feltétel értékeként adja meg a `Where-Object` **FilterScript** paraméter.</span><span class="sxs-lookup"><span data-stu-id="881e0-109">You supply the test condition as the value of the `Where-Object` **FilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="881e0-110">A Where-Object egyszerű tesztek végrehajtása</span><span class="sxs-lookup"><span data-stu-id="881e0-110">Performing Simple Tests with Where-Object</span></span>

<span data-ttu-id="881e0-111">Értékét **FilterScript** van egy *parancsfájlblokkban* – egy vagy több Windows PowerShell-parancsok csúcsos zárójelek között {} –, amely kiértékeli a true vagy FALSE (hamis).</span><span class="sxs-lookup"><span data-stu-id="881e0-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="881e0-112">Lehet, hogy a parancsfájl-blokkokban nagyon egyszerű, de tudomása a másik a Windows PowerShell-fogalmat, összehasonlító operátorok hozza létre őket igényel.</span><span class="sxs-lookup"><span data-stu-id="881e0-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="881e0-113">Egy összehasonlító operátor hasonlítja össze az egyes oldalán megjelenő elemek.</span><span class="sxs-lookup"><span data-stu-id="881e0-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="881e0-114">Összehasonlító operátorok kezdődik a "-" karakter, és a egy neve követi.</span><span class="sxs-lookup"><span data-stu-id="881e0-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="881e0-115">Alapszintű összehasonlító operátorok szinte bármilyen típusú objektumot működik.</span><span class="sxs-lookup"><span data-stu-id="881e0-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="881e0-116">A speciális összehasonlító operátorok csak a szöveges vagy tömbök előfordulhat, hogy működik.</span><span class="sxs-lookup"><span data-stu-id="881e0-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="881e0-117">Alapesetben, amikor szöveg dolgozik a Windows PowerShell összehasonlító operátorok nincsenek megkülönböztetve.</span><span class="sxs-lookup"><span data-stu-id="881e0-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="881e0-118">Megfontolandó szempontok elemzés, mert szimbólumokat <>, például és = összehasonlító operátorok nem képeznek.</span><span class="sxs-lookup"><span data-stu-id="881e0-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="881e0-119">Ehelyett összehasonlító operátorok rétegből betűt.</span><span class="sxs-lookup"><span data-stu-id="881e0-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="881e0-120">Az alapszintű összehasonlító operátorok az alábbi táblázatban láthatók.</span><span class="sxs-lookup"><span data-stu-id="881e0-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="881e0-121">Összehasonlító operátor</span><span class="sxs-lookup"><span data-stu-id="881e0-121">Comparison Operator</span></span>|<span data-ttu-id="881e0-122">Jelentés</span><span class="sxs-lookup"><span data-stu-id="881e0-122">Meaning</span></span>|<span data-ttu-id="881e0-123">Példa (igaz értéket ad vissza)</span><span class="sxs-lookup"><span data-stu-id="881e0-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="881e0-124">-eq</span><span class="sxs-lookup"><span data-stu-id="881e0-124">-eq</span></span>|<span data-ttu-id="881e0-125">egyenlő</span><span class="sxs-lookup"><span data-stu-id="881e0-125">is equal to</span></span>|<span data-ttu-id="881e0-126">1 - eq 1</span><span class="sxs-lookup"><span data-stu-id="881e0-126">1 -eq 1</span></span>|
|<span data-ttu-id="881e0-127">-ne</span><span class="sxs-lookup"><span data-stu-id="881e0-127">-ne</span></span>|<span data-ttu-id="881e0-128">Nem egyenlő</span><span class="sxs-lookup"><span data-stu-id="881e0-128">Is not equal to</span></span>|<span data-ttu-id="881e0-129">1 - ne 2</span><span class="sxs-lookup"><span data-stu-id="881e0-129">1 -ne 2</span></span>|
|<span data-ttu-id="881e0-130">-lt</span><span class="sxs-lookup"><span data-stu-id="881e0-130">-lt</span></span>|<span data-ttu-id="881e0-131">a kisebb, mint</span><span class="sxs-lookup"><span data-stu-id="881e0-131">Is less than</span></span>|<span data-ttu-id="881e0-132">1 – lt 2</span><span class="sxs-lookup"><span data-stu-id="881e0-132">1 -lt 2</span></span>|
|<span data-ttu-id="881e0-133">-le</span><span class="sxs-lookup"><span data-stu-id="881e0-133">-le</span></span>|<span data-ttu-id="881e0-134">Kisebb vagy egyenlő</span><span class="sxs-lookup"><span data-stu-id="881e0-134">Is less than or equal to</span></span>|<span data-ttu-id="881e0-135">1 – le 2</span><span class="sxs-lookup"><span data-stu-id="881e0-135">1 -le 2</span></span>|
|<span data-ttu-id="881e0-136">-gt</span><span class="sxs-lookup"><span data-stu-id="881e0-136">-gt</span></span>|<span data-ttu-id="881e0-137">nagyobb, mint</span><span class="sxs-lookup"><span data-stu-id="881e0-137">Is greater than</span></span>|<span data-ttu-id="881e0-138">2 – gt 1</span><span class="sxs-lookup"><span data-stu-id="881e0-138">2 -gt 1</span></span>|
|<span data-ttu-id="881e0-139">-ge</span><span class="sxs-lookup"><span data-stu-id="881e0-139">-ge</span></span>|<span data-ttu-id="881e0-140">Nagyobb vagy egyenlő</span><span class="sxs-lookup"><span data-stu-id="881e0-140">Is greater than or equal to</span></span>|<span data-ttu-id="881e0-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="881e0-141">2 -ge 1</span></span>|
|<span data-ttu-id="881e0-142">– például a</span><span class="sxs-lookup"><span data-stu-id="881e0-142">-like</span></span>|<span data-ttu-id="881e0-143">Hasonló (helyettesítő összehasonlítás szöveg)</span><span class="sxs-lookup"><span data-stu-id="881e0-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="881e0-144">"file.doc" – például "f\*.do?"</span><span class="sxs-lookup"><span data-stu-id="881e0-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="881e0-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="881e0-145">-notlike</span></span>|<span data-ttu-id="881e0-146">Nem hasonló (helyettesítő összehasonlítás szöveg)</span><span class="sxs-lookup"><span data-stu-id="881e0-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="881e0-147">"file.doc"-notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="881e0-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="881e0-148">-tartalmaz</span><span class="sxs-lookup"><span data-stu-id="881e0-148">-contains</span></span>|<span data-ttu-id="881e0-149">tartalmaz</span><span class="sxs-lookup"><span data-stu-id="881e0-149">Contains</span></span>|<span data-ttu-id="881e0-150">1,2,3 – 1 tartalmaz</span><span class="sxs-lookup"><span data-stu-id="881e0-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="881e0-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="881e0-151">-notcontains</span></span>|<span data-ttu-id="881e0-152">nem tartalmazza</span><span class="sxs-lookup"><span data-stu-id="881e0-152">Does not contain</span></span>|<span data-ttu-id="881e0-153">1,2,3 - notcontains 4</span><span class="sxs-lookup"><span data-stu-id="881e0-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="881e0-154">Where-Object parancsfájl-blokkokban használja a speciális változó `$_` , tekintse meg a folyamat az aktuális objektum.</span><span class="sxs-lookup"><span data-stu-id="881e0-154">Where-Object script blocks use the special variable `$_` to refer to the current object in the pipeline.</span></span> <span data-ttu-id="881e0-155">Íme egy példa annak működését.</span><span class="sxs-lookup"><span data-stu-id="881e0-155">Here is an example of how it works.</span></span> <span data-ttu-id="881e0-156">Ha rendelkezik egy számokból álló listát, és csak be szeretné olvasni azokat, amelyek kevesebb mint 3, használhatja a Where-Object számok szűréséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="881e0-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="881e0-157">Szűrés alapján objektum tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="881e0-157">Filtering Based on Object Properties</span></span>

<span data-ttu-id="881e0-158">Mivel `$_` hivatkozik a jelenlegi folyamat objektumba, elérheti a tulajdonságait a tesztek.</span><span class="sxs-lookup"><span data-stu-id="881e0-158">Since `$_` refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="881e0-159">Például hogy megtekinthessük WMI Win32_SystemDriver osztályt.</span><span class="sxs-lookup"><span data-stu-id="881e0-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="881e0-160">Előfordulhat, hogy a rendszer-illesztőprogramok egy adott rendszer több száz, de Ön csak hasznos lehet egy adott készletét a rendszer-illesztőprogramok, például azok, amelyek jelenleg futnak.</span><span class="sxs-lookup"><span data-stu-id="881e0-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="881e0-161">Ha a Get-Member Win32_SystemDriver tagok megtekintéséhez használja (**Get-WmiObject – osztály Win32_SystemDriver |} Get-Member - MemberType tulajdonság**) látni fogja, hogy a megfelelő tulajdonság állapotát, és, hogy az illesztőprogram futtatásakor az "Fut" értékkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="881e0-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="881e0-162">A rendszer-illesztőprogramok, jelölje ki a kívánt csak futó beírásával szűrheti:</span><span class="sxs-lookup"><span data-stu-id="881e0-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

<span data-ttu-id="881e0-163">Ez egy hosszú listában továbbra is hoz létre.</span><span class="sxs-lookup"><span data-stu-id="881e0-163">This still produces a long list.</span></span> <span data-ttu-id="881e0-164">Előfordulhat, hogy szeretné szűrni, csak az illesztőprogramokat a StartMode értéket is tesztelésével automatikus indításra állítva:</span><span class="sxs-lookup"><span data-stu-id="881e0-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

<span data-ttu-id="881e0-165">Ez olyan biztosít, amely nagy mennyiségű információt, hogy már nincs szüksége, mivel tudjuk, hogy, hogy futnak-e az illesztőprogramok.</span><span class="sxs-lookup"><span data-stu-id="881e0-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="881e0-166">Sőt valószínűleg kell ezen a ponton csak annyi információ a nevét és megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="881e0-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="881e0-167">A következő parancs csak két tulajdonságot, ami sokkal egyszerűbb kimeneti tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="881e0-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

<span data-ttu-id="881e0-168">Két Where-Object-elemek a fenti parancsban, de azok kifejezhető egyetlen Where-Object elem használatával a - és logikai operátor szerinti szűrése, ehhez hasonló:</span><span class="sxs-lookup"><span data-stu-id="881e0-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="881e0-169">A standard szintű logikai operátorokat az alábbi táblázatban láthatók.</span><span class="sxs-lookup"><span data-stu-id="881e0-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="881e0-170">Logikai operátor</span><span class="sxs-lookup"><span data-stu-id="881e0-170">Logical Operator</span></span>|<span data-ttu-id="881e0-171">Jelentés</span><span class="sxs-lookup"><span data-stu-id="881e0-171">Meaning</span></span>|<span data-ttu-id="881e0-172">Példa (igaz értéket ad vissza)</span><span class="sxs-lookup"><span data-stu-id="881e0-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="881e0-173">- és</span><span class="sxs-lookup"><span data-stu-id="881e0-173">-and</span></span>|<span data-ttu-id="881e0-174">Logikai és; IGAZ, ha mindkét oldal igaz</span><span class="sxs-lookup"><span data-stu-id="881e0-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="881e0-175">(1 - eq (1.) - és (2 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="881e0-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="881e0-176">- vagy</span><span class="sxs-lookup"><span data-stu-id="881e0-176">-or</span></span>|<span data-ttu-id="881e0-177">Logikai vagy; IGAZ, ha bármelyik oldal igaz</span><span class="sxs-lookup"><span data-stu-id="881e0-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="881e0-178">(1 - eq 1) – vagy (1 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="881e0-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="881e0-179">-nem</span><span class="sxs-lookup"><span data-stu-id="881e0-179">-not</span></span>|<span data-ttu-id="881e0-180">Logikai not; Megfordítja a true és false</span><span class="sxs-lookup"><span data-stu-id="881e0-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="881e0-181">-nem (1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="881e0-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="881e0-182">Logikai not; Megfordítja a true és false</span><span class="sxs-lookup"><span data-stu-id="881e0-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="881e0-183">\!(1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="881e0-183">\!(1 -eq 2)</span></span>|
