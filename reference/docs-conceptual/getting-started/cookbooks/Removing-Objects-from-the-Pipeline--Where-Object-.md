---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Objektumok eltávolítása a feldolgozási sor az adott objektum
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: 2d89defdb1b234a9d0021fc06e1f05a95bb1bce9
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="ee5a3-103">Objektumok eltávolítása a láncból (Where-Object)</span><span class="sxs-lookup"><span data-stu-id="ee5a3-103">Removing Objects from the Pipeline (Where-Object)</span></span>

<span data-ttu-id="ee5a3-104">A Windows PowerShellben Ön gyakran hozza létre és adják át a több objektumot egy folyamat szükségesnél.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="ee5a3-105">Megadhatja, hogy a megjelenített adott objektumoknak azon tulajdonságait a **formátum** parancsmagok, de ez nem segíthetnek a probléma által megjelenített teljes objektumokat eltávolításával.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="ee5a3-106">Érdemes lehet egy sorban, végéig-objektumok szűrése a így műveleteket tudják végrehajtani a kezdetben által létrehozott objektumok csak egy részét.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="ee5a3-107">A Windows PowerShell tartalmaz egy **Where-Object** parancsmag, amely lehetővé teszi az egyes objektumok tesztelése a folyamat, és csak adja át a feldolgozási sor mentén ha megfelel-e egy adott feltétel.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-107">Windows PowerShell includes a **Where-Object** cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="ee5a3-108">A teszt nem továbbítja objektumok el lesznek távolítva a folyamatot.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="ee5a3-109">A feltétel értékeként adja meg a **Where-ObjectFilterScript** paraméter.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-109">You supply the test condition as the value of the **Where-ObjectFilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="ee5a3-110">A Where-Object egyszerű tesztek végrehajtása</span><span class="sxs-lookup"><span data-stu-id="ee5a3-110">Performing Simple Tests with Where-Object</span></span>

<span data-ttu-id="ee5a3-111">Értékének **FilterScript** van egy *parancsfájlblokkban* - egy vagy több Windows PowerShell-parancsok csúcsos zárójelek {} között -, amely kiértékelésének eredménye true vagy false.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="ee5a3-112">Lehet, hogy a parancsfájl-blokkokban nagyon egyszerű, de szükséges hozza létre őket egy másik Windows PowerShell koncepció összehasonlító operátorok tudomása.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="ee5a3-113">Egy összehasonlító operátor mindkét oldalán megjelenő elemek hasonlítja össze.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="ee5a3-114">Összehasonlító operátorok kezdődhet a "-" karakter, és van egy neve követ.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="ee5a3-115">Alapszintű összehasonlító operátorok működik a szinte bármilyen típusú objektumot.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="ee5a3-116">A speciális összehasonlító operátorok csak lehet, hogy működni szöveg vagy tömb.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="ee5a3-117">Alapértelmezés szerint az szöveg használatakor a Windows PowerShell összehasonlító operátorok értékek azonban nem.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="ee5a3-118">Szempontok elemzése, mert szimbólumok szerepelhetnek, például <>, és = összehasonlító operátorok nem használatosak.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="ee5a3-119">Ehelyett összehasonlító operátorok rétegből betűket.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="ee5a3-120">Az alapvető összehasonlító operátorok a következő táblázatban láthatók.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="ee5a3-121">Összehasonlító operátor</span><span class="sxs-lookup"><span data-stu-id="ee5a3-121">Comparison Operator</span></span>|<span data-ttu-id="ee5a3-122">Jelentés</span><span class="sxs-lookup"><span data-stu-id="ee5a3-122">Meaning</span></span>|<span data-ttu-id="ee5a3-123">(Igaz) – Példa</span><span class="sxs-lookup"><span data-stu-id="ee5a3-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="ee5a3-124">-eq</span><span class="sxs-lookup"><span data-stu-id="ee5a3-124">-eq</span></span>|<span data-ttu-id="ee5a3-125">egyenlő</span><span class="sxs-lookup"><span data-stu-id="ee5a3-125">is equal to</span></span>|<span data-ttu-id="ee5a3-126">1 - eq 1</span><span class="sxs-lookup"><span data-stu-id="ee5a3-126">1 -eq 1</span></span>|
|<span data-ttu-id="ee5a3-127">-ne</span><span class="sxs-lookup"><span data-stu-id="ee5a3-127">-ne</span></span>|<span data-ttu-id="ee5a3-128">Nem egyenlő</span><span class="sxs-lookup"><span data-stu-id="ee5a3-128">Is not equal to</span></span>|<span data-ttu-id="ee5a3-129">1 - ne 2</span><span class="sxs-lookup"><span data-stu-id="ee5a3-129">1 -ne 2</span></span>|
|<span data-ttu-id="ee5a3-130">-lt</span><span class="sxs-lookup"><span data-stu-id="ee5a3-130">-lt</span></span>|<span data-ttu-id="ee5a3-131">Értéke kisebb, mint</span><span class="sxs-lookup"><span data-stu-id="ee5a3-131">Is less than</span></span>|<span data-ttu-id="ee5a3-132">1 -lt 2</span><span class="sxs-lookup"><span data-stu-id="ee5a3-132">1 -lt 2</span></span>|
|<span data-ttu-id="ee5a3-133">-le</span><span class="sxs-lookup"><span data-stu-id="ee5a3-133">-le</span></span>|<span data-ttu-id="ee5a3-134">Kisebb vagy egyenlő, mint</span><span class="sxs-lookup"><span data-stu-id="ee5a3-134">Is less than or equal to</span></span>|<span data-ttu-id="ee5a3-135">1 – le 2</span><span class="sxs-lookup"><span data-stu-id="ee5a3-135">1 -le 2</span></span>|
|<span data-ttu-id="ee5a3-136">-gt</span><span class="sxs-lookup"><span data-stu-id="ee5a3-136">-gt</span></span>|<span data-ttu-id="ee5a3-137">Nagyobb, mint</span><span class="sxs-lookup"><span data-stu-id="ee5a3-137">Is greater than</span></span>|<span data-ttu-id="ee5a3-138">2 - gt 1</span><span class="sxs-lookup"><span data-stu-id="ee5a3-138">2 -gt 1</span></span>|
|<span data-ttu-id="ee5a3-139">-ge</span><span class="sxs-lookup"><span data-stu-id="ee5a3-139">-ge</span></span>|<span data-ttu-id="ee5a3-140">Nagyobb vagy egyenlő</span><span class="sxs-lookup"><span data-stu-id="ee5a3-140">Is greater than or equal to</span></span>|<span data-ttu-id="ee5a3-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="ee5a3-141">2 -ge 1</span></span>|
|<span data-ttu-id="ee5a3-142">– például a</span><span class="sxs-lookup"><span data-stu-id="ee5a3-142">-like</span></span>|<span data-ttu-id="ee5a3-143">Olyan, mint (helyettesítő szöveg a összehasonlítását)</span><span class="sxs-lookup"><span data-stu-id="ee5a3-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="ee5a3-144">"file.doc" -like "f\*.do?"</span><span class="sxs-lookup"><span data-stu-id="ee5a3-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="ee5a3-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="ee5a3-145">-notlike</span></span>|<span data-ttu-id="ee5a3-146">Nincs (a szöveg helyettesítő összehasonlítását) például</span><span class="sxs-lookup"><span data-stu-id="ee5a3-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="ee5a3-147">"file.doc" -notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="ee5a3-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="ee5a3-148">-tartalmaz</span><span class="sxs-lookup"><span data-stu-id="ee5a3-148">-contains</span></span>|<span data-ttu-id="ee5a3-149">tartalmazza</span><span class="sxs-lookup"><span data-stu-id="ee5a3-149">Contains</span></span>|<span data-ttu-id="ee5a3-150">1,2,3 - 1 tartalmazza</span><span class="sxs-lookup"><span data-stu-id="ee5a3-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="ee5a3-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="ee5a3-151">-notcontains</span></span>|<span data-ttu-id="ee5a3-152">Nem tartalmaz</span><span class="sxs-lookup"><span data-stu-id="ee5a3-152">Does not contain</span></span>|<span data-ttu-id="ee5a3-153">1,2,3 - notcontains 4</span><span class="sxs-lookup"><span data-stu-id="ee5a3-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="ee5a3-154">Where-Object parancsfájlblokkokban a '$_' speciális változó segítségével tekintse meg a folyamat az aktuális objektum.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-154">Where-Object script blocks use the special variable '$_' to refer to the current object in the pipeline.</span></span> <span data-ttu-id="ee5a3-155">Íme egy példa annak működéséről.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-155">Here is an example of how it works.</span></span> <span data-ttu-id="ee5a3-156">Ha számokból álló listát, és csak a meglévők közül, amelyek kevesebb mint 3 vissza szeretné, Where-Object segítségével írja be a számok szűrése:</span><span class="sxs-lookup"><span data-stu-id="ee5a3-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="ee5a3-157">Szűrés alapján objektum tulajdonságai</span><span class="sxs-lookup"><span data-stu-id="ee5a3-157">Filtering Based on Object Properties</span></span>

<span data-ttu-id="ee5a3-158">Az aktuális folyamat objektum $_ hivatkozik, azt a tesztek érhessék el a tulajdonságai.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-158">Since $_ refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="ee5a3-159">Tegyük fel azt is megtekinthetik a Win32_SystemDriver osztály a WMI-ben.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="ee5a3-160">Előfordulhat, hogy egy adott rendszer illesztőprogramja több száz, de csak érdekelheti a rendszer-illesztőprogramok, például azokkal, amely jelenleg fut egy adott készletét.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="ee5a3-161">Ha a Get-tag Win32_SystemDriver tagok megtekintéséhez használja (**Get-WmiObject – osztály Win32_SystemDriver |} Get-Member - MemberType tulajdonsága**) jelenik meg, hogy a megfelelő tulajdonság állapotát, és, hogy az illesztőprogram futtatásakor "Fut" értékkel rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="ee5a3-162">Szűrheti a rendszer illesztőprogramokat, írja be a csak a futó ők kiválasztása:</span><span class="sxs-lookup"><span data-stu-id="ee5a3-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

<span data-ttu-id="ee5a3-163">Ez továbbra is szolgáltat hosszú listáját.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-163">This still produces a long list.</span></span> <span data-ttu-id="ee5a3-164">Előfordulhat, hogy szűrni kívánt csak jelölje be az illesztőprogramok által a StartMode értéket is vizsgálati automatikus indításra állítva:</span><span class="sxs-lookup"><span data-stu-id="ee5a3-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

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

<span data-ttu-id="ee5a3-165">Ez biztosítja, nagy mennyiségű információt azt már nem szükséges, mert tudjuk, hogy fut-e az illesztőprogramok.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="ee5a3-166">Az egyetlen adat valószínűleg kell ezen a ponton, nevét és megjelenítendő nevét.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="ee5a3-167">A következő parancs csak két tulajdonságokhoz, így sokkal egyszerűbb kimeneti tartalmazza:</span><span class="sxs-lookup"><span data-stu-id="ee5a3-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

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

<span data-ttu-id="ee5a3-168">A fenti parancsban két Where-Object-eleme van, de ezek lehetnek a Where-Object elemet használatával a - és logikai operátor, ehhez hasonló:</span><span class="sxs-lookup"><span data-stu-id="ee5a3-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="ee5a3-169">A szabványos logikai operátorok a következő táblázatban láthatók.</span><span class="sxs-lookup"><span data-stu-id="ee5a3-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="ee5a3-170">Logikai operátor</span><span class="sxs-lookup"><span data-stu-id="ee5a3-170">Logical Operator</span></span>|<span data-ttu-id="ee5a3-171">Jelentés</span><span class="sxs-lookup"><span data-stu-id="ee5a3-171">Meaning</span></span>|<span data-ttu-id="ee5a3-172">(Igaz) – Példa</span><span class="sxs-lookup"><span data-stu-id="ee5a3-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="ee5a3-173">- és</span><span class="sxs-lookup"><span data-stu-id="ee5a3-173">-and</span></span>|<span data-ttu-id="ee5a3-174">Logikai és; Igaz kétoldalas teljesülése esetén</span><span class="sxs-lookup"><span data-stu-id="ee5a3-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="ee5a3-175">(1 - eq 1.) - és (2 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="ee5a3-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="ee5a3-176">- vagy</span><span class="sxs-lookup"><span data-stu-id="ee5a3-176">-or</span></span>|<span data-ttu-id="ee5a3-177">Logikai vagy; IGAZ, ha bármelyik oldal igaz</span><span class="sxs-lookup"><span data-stu-id="ee5a3-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="ee5a3-178">(1 - eq 1) – vagy (1 - eq 2).</span><span class="sxs-lookup"><span data-stu-id="ee5a3-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="ee5a3-179">-nem</span><span class="sxs-lookup"><span data-stu-id="ee5a3-179">-not</span></span>|<span data-ttu-id="ee5a3-180">Logikai nem; Megfordítja a true és false</span><span class="sxs-lookup"><span data-stu-id="ee5a3-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="ee5a3-181">-nem (1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="ee5a3-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="ee5a3-182">Logikai nem; Megfordítja a true és false</span><span class="sxs-lookup"><span data-stu-id="ee5a3-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="ee5a3-183">\!(1 - eq 2)</span><span class="sxs-lookup"><span data-stu-id="ee5a3-183">\!(1 -eq 2)</span></span>|