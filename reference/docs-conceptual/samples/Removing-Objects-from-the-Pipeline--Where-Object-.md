---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Objektumok eltávolítása az adatcsatornából Where-Object
ms.openlocfilehash: c47efd38e2ff40ce3b7bf50b161cc38de922c5da
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030881"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="6a43a-103">Objektumok eltávolítása az adatcsatornából (Where-Object)</span><span class="sxs-lookup"><span data-stu-id="6a43a-103">Removing Objects from the Pipeline (Where-Object)</span></span>

<span data-ttu-id="6a43a-104">A Windows PowerShellben Ön gyakran hozza létre és azt szeretné, hogy egy folyamat több objektum adják át.</span><span class="sxs-lookup"><span data-stu-id="6a43a-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="6a43a-105">Adott lehetőségével szűkítheti a megjelenített objektumok tulajdonságait is megadhat a **formátum** parancsmagok, de ez nem segíthetnek a probléma, és a teljes objektumok eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="6a43a-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="6a43a-106">Érdemes a folyamat vége előtt-objektumok szűrése, így elvégezhető műveletek a kezdetben által létrehozott objektumok egy részhalmazára.</span><span class="sxs-lookup"><span data-stu-id="6a43a-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="6a43a-107">Windows PowerShell tartalmaz egy `Where-Object` parancsmagot, amely lehetővé teszi, hogy a folyamat minden egyes objektum tesztelése, és csak azt adják át a folyamat megfelel egy adott teszt feltételt.</span><span class="sxs-lookup"><span data-stu-id="6a43a-107">Windows PowerShell includes a `Where-Object` cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="6a43a-108">Objektumok, amelyek nem adnak át a vizsgálat a folyamat törlődnek.</span><span class="sxs-lookup"><span data-stu-id="6a43a-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="6a43a-109">A feltétel értékeként adja meg a `Where-Object` **FilterScript** paraméter.</span><span class="sxs-lookup"><span data-stu-id="6a43a-109">You supply the test condition as the value of the `Where-Object` **FilterScript** parameter.</span></span>

## <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="6a43a-110">A Where-Object egyszerű tesztek végrehajtása</span><span class="sxs-lookup"><span data-stu-id="6a43a-110">Performing Simple Tests with Where-Object</span></span>

<span data-ttu-id="6a43a-111">Értékét **FilterScript** van egy *parancsfájlblokkban* – egy vagy több Windows PowerShell-parancsok csúcsos zárójelek között {} –, amely kiértékeli a true vagy FALSE (hamis).</span><span class="sxs-lookup"><span data-stu-id="6a43a-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="6a43a-112">Lehet, hogy a parancsfájl-blokkokban nagyon egyszerű, de tudomása a másik a Windows PowerShell-fogalmat, összehasonlító operátorok hozza létre őket igényel.</span><span class="sxs-lookup"><span data-stu-id="6a43a-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="6a43a-113">Egy összehasonlító operátor hasonlítja össze az egyes oldalán megjelenő elemek.</span><span class="sxs-lookup"><span data-stu-id="6a43a-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="6a43a-114">Összehasonlító operátorok kezdődik a "-" karakter, és a egy neve követi.</span><span class="sxs-lookup"><span data-stu-id="6a43a-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="6a43a-115">Alapszintű összehasonlító operátorok szinte bármilyen típusú objektumot működik.</span><span class="sxs-lookup"><span data-stu-id="6a43a-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="6a43a-116">A speciális összehasonlító operátorok csak a szöveges vagy tömbök előfordulhat, hogy működik.</span><span class="sxs-lookup"><span data-stu-id="6a43a-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="6a43a-117">Alapesetben, amikor szöveg dolgozik a Windows PowerShell összehasonlító operátorok nincsenek megkülönböztetve.</span><span class="sxs-lookup"><span data-stu-id="6a43a-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="6a43a-118">Megfontolandó szempontok elemzés, mert szimbólumokat <>, például és = összehasonlító operátorok nem képeznek.</span><span class="sxs-lookup"><span data-stu-id="6a43a-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="6a43a-119">Ehelyett összehasonlító operátorok rétegből betűt.</span><span class="sxs-lookup"><span data-stu-id="6a43a-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="6a43a-120">Az alapszintű összehasonlító operátorok az alábbi táblázatban láthatók.</span><span class="sxs-lookup"><span data-stu-id="6a43a-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="6a43a-121">Összehasonlító operátor</span><span class="sxs-lookup"><span data-stu-id="6a43a-121">Comparison Operator</span></span>|<span data-ttu-id="6a43a-122">Jelentés</span><span class="sxs-lookup"><span data-stu-id="6a43a-122">Meaning</span></span>|<span data-ttu-id="6a43a-123">Példa (igaz értéket ad vissza)</span><span class="sxs-lookup"><span data-stu-id="6a43a-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="6a43a-124">-eq</span><span class="sxs-lookup"><span data-stu-id="6a43a-124">-eq</span></span>|<span data-ttu-id="6a43a-125">egyenlő</span><span class="sxs-lookup"><span data-stu-id="6a43a-125">is equal to</span></span>|<span data-ttu-id="6a43a-126">1 -eq 1</span><span class="sxs-lookup"><span data-stu-id="6a43a-126">1 -eq 1</span></span>|
|<span data-ttu-id="6a43a-127">-ne</span><span class="sxs-lookup"><span data-stu-id="6a43a-127">-ne</span></span>|<span data-ttu-id="6a43a-128">Nem egyenlő</span><span class="sxs-lookup"><span data-stu-id="6a43a-128">Is not equal to</span></span>|<span data-ttu-id="6a43a-129">1 - ne 2</span><span class="sxs-lookup"><span data-stu-id="6a43a-129">1 -ne 2</span></span>|
|<span data-ttu-id="6a43a-130">-lt</span><span class="sxs-lookup"><span data-stu-id="6a43a-130">-lt</span></span>|<span data-ttu-id="6a43a-131">A kisebb, mint</span><span class="sxs-lookup"><span data-stu-id="6a43a-131">Is less than</span></span>|<span data-ttu-id="6a43a-132">1 – lt 2</span><span class="sxs-lookup"><span data-stu-id="6a43a-132">1 -lt 2</span></span>|
|<span data-ttu-id="6a43a-133">-le</span><span class="sxs-lookup"><span data-stu-id="6a43a-133">-le</span></span>|<span data-ttu-id="6a43a-134">kisebb vagy egyenlő</span><span class="sxs-lookup"><span data-stu-id="6a43a-134">Is less than or equal to</span></span>|<span data-ttu-id="6a43a-135">1 – le 2</span><span class="sxs-lookup"><span data-stu-id="6a43a-135">1 -le 2</span></span>|
|<span data-ttu-id="6a43a-136">-gt</span><span class="sxs-lookup"><span data-stu-id="6a43a-136">-gt</span></span>|<span data-ttu-id="6a43a-137">Nagyobb, mint</span><span class="sxs-lookup"><span data-stu-id="6a43a-137">Is greater than</span></span>|<span data-ttu-id="6a43a-138">2 – gt 1</span><span class="sxs-lookup"><span data-stu-id="6a43a-138">2 -gt 1</span></span>|
|<span data-ttu-id="6a43a-139">-ge</span><span class="sxs-lookup"><span data-stu-id="6a43a-139">-ge</span></span>|<span data-ttu-id="6a43a-140">nagyobb vagy egyenlő</span><span class="sxs-lookup"><span data-stu-id="6a43a-140">Is greater than or equal to</span></span>|<span data-ttu-id="6a43a-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="6a43a-141">2 -ge 1</span></span>|
|<span data-ttu-id="6a43a-142">– például a</span><span class="sxs-lookup"><span data-stu-id="6a43a-142">-like</span></span>|<span data-ttu-id="6a43a-143">Hasonló (helyettesítő összehasonlítás szöveg)</span><span class="sxs-lookup"><span data-stu-id="6a43a-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="6a43a-144">"file.doc" – például "f\*.do?"</span><span class="sxs-lookup"><span data-stu-id="6a43a-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="6a43a-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="6a43a-145">-notlike</span></span>|<span data-ttu-id="6a43a-146">Nem hasonló (helyettesítő összehasonlítás szöveg)</span><span class="sxs-lookup"><span data-stu-id="6a43a-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="6a43a-147">"file.doc"-notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="6a43a-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="6a43a-148">-tartalmaz</span><span class="sxs-lookup"><span data-stu-id="6a43a-148">-contains</span></span>|<span data-ttu-id="6a43a-149">tartalmaz</span><span class="sxs-lookup"><span data-stu-id="6a43a-149">Contains</span></span>|<span data-ttu-id="6a43a-150">1,2,3 – 1 tartalmaz</span><span class="sxs-lookup"><span data-stu-id="6a43a-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="6a43a-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="6a43a-151">-notcontains</span></span>|<span data-ttu-id="6a43a-152">Nem tartalmazza</span><span class="sxs-lookup"><span data-stu-id="6a43a-152">Does not contain</span></span>|<span data-ttu-id="6a43a-153">1,2,3 - notcontains 4</span><span class="sxs-lookup"><span data-stu-id="6a43a-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="6a43a-154">Where-Object parancsfájl-blokkokban használja a speciális változó `$_` , tekintse meg a folyamat az aktuális objektum.</span><span class="sxs-lookup"><span data-stu-id="6a43a-154">Where-Object script blocks use the special variable `$_` to refer to the current object in the pipeline.</span></span> <span data-ttu-id="6a43a-155">Íme egy példa annak működését.</span><span class="sxs-lookup"><span data-stu-id="6a43a-155">Here is an example of how it works.</span></span> <span data-ttu-id="6a43a-156">Ha rendelkezik egy számokból álló listát, és csak be szeretné olvasni azokat, amelyek kevesebb mint 3, használhatja a Where-Object számok szűréséhez írja be:</span><span class="sxs-lookup"><span data-stu-id="6a43a-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

## <a name="filtering-based-on-object-properties"></a><span data-ttu-id="6a43a-157">Szűrés alapján objektum tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="6a43a-157">Filtering Based on Object Properties</span></span>

<span data-ttu-id="6a43a-158">Mivel `$_` hivatkozik a jelenlegi folyamat objektumba, elérheti a tulajdonságait a tesztek.</span><span class="sxs-lookup"><span data-stu-id="6a43a-158">Since `$_` refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="6a43a-159">Például hogy megtekinthessük WMI Win32_SystemDriver osztályt.</span><span class="sxs-lookup"><span data-stu-id="6a43a-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="6a43a-160">Előfordulhat, hogy a rendszer-illesztőprogramok egy adott rendszer több száz, de Ön csak hasznos lehet egy adott készletét a rendszer-illesztőprogramok, például azok, amelyek jelenleg futnak.</span><span class="sxs-lookup"><span data-stu-id="6a43a-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="6a43a-161">Ha a Get-Member Win32_SystemDriver tagok megtekintéséhez használja (**Get-WmiObject – osztály Win32_SystemDriver |} Get-Member - MemberType tulajdonság**) látni fogja, hogy a megfelelő tulajdonság állapotát, és, hogy az illesztőprogram futtatásakor az "Fut" értékkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="6a43a-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="6a43a-162">A rendszer-illesztőprogramok, jelölje ki a kívánt csak futó beírásával szűrheti:</span><span class="sxs-lookup"><span data-stu-id="6a43a-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

<span data-ttu-id="6a43a-163">Ez egy hosszú listában továbbra is hoz létre.</span><span class="sxs-lookup"><span data-stu-id="6a43a-163">This still produces a long list.</span></span> <span data-ttu-id="6a43a-164">Előfordulhat, hogy szeretné szűrni, csak az illesztőprogramokat a StartMode értéket is tesztelésével automatikus indításra állítva:</span><span class="sxs-lookup"><span data-stu-id="6a43a-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

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

<span data-ttu-id="6a43a-165">Ez olyan biztosít, amely nagy mennyiségű információt, hogy már nincs szüksége, mivel tudjuk, hogy, hogy futnak-e az illesztőprogramok.</span><span class="sxs-lookup"><span data-stu-id="6a43a-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="6a43a-166">Sőt valószínűleg kell ezen a ponton csak annyi információ a nevét és megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="6a43a-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="6a43a-167">A következő parancs csak két tulajdonságot, ami sokkal egyszerűbb kimeneti tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="6a43a-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

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

<span data-ttu-id="6a43a-168">Két Where-Object-elemek a fenti parancsban, de azok kifejezhető egyetlen Where-Object elem használatával a - és logikai operátor szerinti szűrése, ehhez hasonló:</span><span class="sxs-lookup"><span data-stu-id="6a43a-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="6a43a-169">A standard szintű logikai operátorokat az alábbi táblázatban láthatók.</span><span class="sxs-lookup"><span data-stu-id="6a43a-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="6a43a-170">Logikai operátor</span><span class="sxs-lookup"><span data-stu-id="6a43a-170">Logical Operator</span></span>|<span data-ttu-id="6a43a-171">Jelentés</span><span class="sxs-lookup"><span data-stu-id="6a43a-171">Meaning</span></span>|<span data-ttu-id="6a43a-172">Példa (igaz értéket ad vissza)</span><span class="sxs-lookup"><span data-stu-id="6a43a-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="6a43a-173">- és</span><span class="sxs-lookup"><span data-stu-id="6a43a-173">-and</span></span>|<span data-ttu-id="6a43a-174">Logikai és; IGAZ, ha mindkét oldal igaz</span><span class="sxs-lookup"><span data-stu-id="6a43a-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="6a43a-175">(1 - eq (1.) - és (2 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="6a43a-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="6a43a-176">- vagy</span><span class="sxs-lookup"><span data-stu-id="6a43a-176">-or</span></span>|<span data-ttu-id="6a43a-177">Logikai vagy; IGAZ, ha bármelyik oldal igaz</span><span class="sxs-lookup"><span data-stu-id="6a43a-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="6a43a-178">(1 - eq 1) – vagy (1 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="6a43a-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="6a43a-179">-nem</span><span class="sxs-lookup"><span data-stu-id="6a43a-179">-not</span></span>|<span data-ttu-id="6a43a-180">Logikai not; Megfordítja a true és false</span><span class="sxs-lookup"><span data-stu-id="6a43a-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="6a43a-181">-nem (1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="6a43a-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="6a43a-182">Logikai not; Megfordítja a true és false</span><span class="sxs-lookup"><span data-stu-id="6a43a-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="6a43a-183">\!(1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="6a43a-183">\!(1 -eq 2)</span></span>|
