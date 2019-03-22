---
ms.date: 3/18/2019
title: Get-WinEvent lekérdezések FilterHashtable létrehozása
ms.openlocfilehash: fae01cc8be5c1805e2aae008e1f21ed387efa325
ms.sourcegitcommit: 396509cd0d415acc306b68758b6f833406e26bf5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/21/2019
ms.locfileid: "58320487"
---
# <a name="creating-get-winevent-queries-with-filterhashtable"></a><span data-ttu-id="3f47d-102">Get-WinEvent lekérdezések FilterHashtable létrehozása</span><span class="sxs-lookup"><span data-stu-id="3f47d-102">Creating Get-WinEvent queries with FilterHashtable</span></span>

<span data-ttu-id="3f47d-103">Olvassa el az eredeti 2014. június 3, a **Scripting Guy** blog post, lásd: [használata FilterHashTable szűrő eseménynaplóba való a PowerShell-lel](https://devblogs.microsoft.com/scripting/use-filterhashtable-to-filter-event-log-with-powershell/).</span><span class="sxs-lookup"><span data-stu-id="3f47d-103">To read the original June 3, 2014 **Scripting Guy** blog post, see [Use FilterHashTable to Filter Event Log with PowerShell](https://devblogs.microsoft.com/scripting/use-filterhashtable-to-filter-event-log-with-powershell/).</span></span>

<span data-ttu-id="3f47d-104">Ez a cikk egy olyan, az eredeti blogbejegyzés, és azt ismerteti, hogyan használható a `Get-WinEvent` parancsmag **FilterHashtable** paraméter eseménynaplók szűréséhez.</span><span class="sxs-lookup"><span data-stu-id="3f47d-104">This article is an excerpt of the original blog post and explains how to use the `Get-WinEvent` cmdlet's **FilterHashtable** parameter to filter event logs.</span></span> <span data-ttu-id="3f47d-105">A PowerShell `Get-WinEvent` parancsmagot a Windows esemény- és diagnosztikai naplók szűrése hatékony módszer.</span><span class="sxs-lookup"><span data-stu-id="3f47d-105">PowerShell's `Get-WinEvent` cmdlet is a powerful method to filter Windows event and diagnostic logs.</span></span> <span data-ttu-id="3f47d-106">Javítja a teljesítményt, ha egy `Get-WinEvent` lekérdezéséhez használja a **FilterHashtable** paraméter.</span><span class="sxs-lookup"><span data-stu-id="3f47d-106">Performance improves when a `Get-WinEvent` query uses the **FilterHashtable** parameter.</span></span>

<span data-ttu-id="3f47d-107">Ha nagy eseménynaplók dolgozik, akkor sem hatékony küldeni lefelé a folyamat objektumok egy `Where-Object` parancsot.</span><span class="sxs-lookup"><span data-stu-id="3f47d-107">When you work with large event logs, it's not efficient to send objects down the pipeline to a `Where-Object` command.</span></span> <span data-ttu-id="3f47d-108">PowerShell 6-os, mielőtt a `Get-EventLog` parancsmag lett egy másik lehetőség a naplóadatok lekérése.</span><span class="sxs-lookup"><span data-stu-id="3f47d-108">Prior to PowerShell 6, the `Get-EventLog` cmdlet was another option to get log data.</span></span> <span data-ttu-id="3f47d-109">Például az alábbi parancsok olyan hatékony szűrő a **Microsoft-Windows-töredezettségmentesítési** naplók:</span><span class="sxs-lookup"><span data-stu-id="3f47d-109">For example, the following commands are inefficient to filter the **Microsoft-Windows-Defrag** logs:</span></span>

`Get-EventLog -LogName Application | Where-Object Source -Match defrag`

`Get-WinEvent -LogName Application | Where-Object { $_.ProviderName -Match 'defrag' }`

<span data-ttu-id="3f47d-110">A következő parancsot használja egy kivonattábla, amely növeli a teljesítményt:</span><span class="sxs-lookup"><span data-stu-id="3f47d-110">The following command uses a hash table that improves the performance:</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='*defrag'
}
```

### <a name="blog-posts-about-enumeration"></a><span data-ttu-id="3f47d-111">Enumerálás információ blogbejegyzések</span><span class="sxs-lookup"><span data-stu-id="3f47d-111">Blog posts about enumeration</span></span>

<span data-ttu-id="3f47d-112">Ez a cikk egy kivonattáblát a felsorolt értékek használata adatait jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="3f47d-112">This article presents information about how to use enumerated values in a hash table.</span></span> <span data-ttu-id="3f47d-113">Az enumerálás kapcsolatos további információkért olvassa el ezeket **Scripting Guy** blogbejegyzések.</span><span class="sxs-lookup"><span data-stu-id="3f47d-113">For more information about enumeration, read these **Scripting Guy** blog posts.</span></span> <span data-ttu-id="3f47d-114">Függvény, amely visszaadja a felsorolt értékek létrehozásához lásd: [enumerálások és értékek](https://devblogs.microsoft.com/scripting/hey-scripting-guy-weekend-scripter-enumerations-and-values).</span><span class="sxs-lookup"><span data-stu-id="3f47d-114">To create a function that returns the enumerated values, see [Enumerations and Values](https://devblogs.microsoft.com/scripting/hey-scripting-guy-weekend-scripter-enumerations-and-values).</span></span>
<span data-ttu-id="3f47d-115">További információkért lásd: a [Scripting Guy sorozatát blogon tesz közzé, enumerálás kapcsolatos](https://devblogs.microsoft.com/scripting/?s=about+enumeration).</span><span class="sxs-lookup"><span data-stu-id="3f47d-115">For more information, see the [Scripting Guy series of blog posts about enumeration](https://devblogs.microsoft.com/scripting/?s=about+enumeration).</span></span>

### <a name="hash-table-keyvalue-pairs"></a><span data-ttu-id="3f47d-116">Ujjlenyomat-tábla, kulcs/érték párok</span><span class="sxs-lookup"><span data-stu-id="3f47d-116">Hash table key/value pairs</span></span>

<span data-ttu-id="3f47d-117">Hatékony lekérdezések felépítését, használja a `Get-WinEvent` parancsmagot a **FilterHashtable** paraméter.</span><span class="sxs-lookup"><span data-stu-id="3f47d-117">To build efficient queries, use the `Get-WinEvent` cmdlet with the **FilterHashtable** parameter.</span></span>
<span data-ttu-id="3f47d-118">**FilterHashtable** fogad el egy kivonattáblát információkat lehet lekérni a Windows-eseménynaplók szűrőként.</span><span class="sxs-lookup"><span data-stu-id="3f47d-118">**FilterHashtable** accepts a hash table as a filter to get specific information from Windows event logs.</span></span> <span data-ttu-id="3f47d-119">Egy kivonattáblát használ **kulcs/érték** párokat.</span><span class="sxs-lookup"><span data-stu-id="3f47d-119">A hash table uses **key/value** pairs.</span></span> <span data-ttu-id="3f47d-120">Kivonattáblákkal kapcsolatos további információkért lásd: [about_Hash_Tables](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span><span class="sxs-lookup"><span data-stu-id="3f47d-120">For more information about hash tables, see [about_Hash_Tables](/powershell/module/microsoft.powershell.core/about/about_hash_tables).</span></span>

<span data-ttu-id="3f47d-121">Ha a **kulcs/érték** értékpárok ugyanabban a sorban, azok pontosvesszővel kell elválasztani.</span><span class="sxs-lookup"><span data-stu-id="3f47d-121">If the **key/value** pairs are on the same line, they must be separated by a semicolon.</span></span> <span data-ttu-id="3f47d-122">Ha minden egyes **kulcs/érték** párnak külön sorban van, a pontosvessző nem szükséges.</span><span class="sxs-lookup"><span data-stu-id="3f47d-122">If each **key/value** pair is on a separate line, the semicolon isn't needed.</span></span> <span data-ttu-id="3f47d-123">Például ez a cikk helyek **kulcs/érték** külön sorban párosítja, és nem használja a pontosvesszővel válassza el.</span><span class="sxs-lookup"><span data-stu-id="3f47d-123">For example, this article places **key/value** pairs on separate lines and doesn't use semicolons.</span></span>

<span data-ttu-id="3f47d-124">Ez a minta számos használja a **FilterHashtable** paraméter **kulcs/érték** párokat.</span><span class="sxs-lookup"><span data-stu-id="3f47d-124">This sample uses several of the **FilterHashtable** parameter's **key/value** pairs.</span></span> <span data-ttu-id="3f47d-125">A befejezett lekérdezés tartalmaz **naplónév**, **ProviderName**, **kulcsszavak**, **azonosító**, és **szint**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-125">The completed query includes **LogName**, **ProviderName**, **Keywords**, **ID**, and **Level**.</span></span>

<span data-ttu-id="3f47d-126">Az elfogadott **kulcs/érték** párok az alábbi táblázatban láthatók, és a dokumentációban szerepelnek a [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent)
**FilterHashtable** a paraméter.</span><span class="sxs-lookup"><span data-stu-id="3f47d-126">The accepted **key/value** pairs are shown in the following table and are included in the documentation for the [Get-WinEvent](/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent)
**FilterHashtable** parameter.</span></span>

<span data-ttu-id="3f47d-127">Az alábbi táblázatban láthatók a kulcsnevek, adattípusok, és hogy helyettesítő karakterek az adatértéket elfogadás.</span><span class="sxs-lookup"><span data-stu-id="3f47d-127">The following table displays the key names, data types, and whether wildcard characters are accepted for a data value.</span></span>

| <span data-ttu-id="3f47d-128">Kulcs neve</span><span class="sxs-lookup"><span data-stu-id="3f47d-128">Key name</span></span>     | <span data-ttu-id="3f47d-129">Adatok értéktípusa</span><span class="sxs-lookup"><span data-stu-id="3f47d-129">Value data type</span></span>    | <span data-ttu-id="3f47d-130">Elfogadja a helyettesítő karakterek?</span><span class="sxs-lookup"><span data-stu-id="3f47d-130">Accepts wildcard characters?</span></span> |
|------------- | ------------------ | ---------------------------- |
| <span data-ttu-id="3f47d-131">Naplónév</span><span class="sxs-lookup"><span data-stu-id="3f47d-131">LogName</span></span>      | `<String[]>`       | <span data-ttu-id="3f47d-132">Igen</span><span class="sxs-lookup"><span data-stu-id="3f47d-132">Yes</span></span> |
| <span data-ttu-id="3f47d-133">ProviderName</span><span class="sxs-lookup"><span data-stu-id="3f47d-133">ProviderName</span></span> | `<String[]>`       | <span data-ttu-id="3f47d-134">Igen</span><span class="sxs-lookup"><span data-stu-id="3f47d-134">Yes</span></span> |
| <span data-ttu-id="3f47d-135">Elérési út</span><span class="sxs-lookup"><span data-stu-id="3f47d-135">Path</span></span>         | `<String[]>`       | <span data-ttu-id="3f47d-136">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-136">No</span></span>  |
| <span data-ttu-id="3f47d-137">Kulcsszavak</span><span class="sxs-lookup"><span data-stu-id="3f47d-137">Keywords</span></span>     | `<Long[]>`         | <span data-ttu-id="3f47d-138">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-138">No</span></span>  |
| <span data-ttu-id="3f47d-139">ID</span><span class="sxs-lookup"><span data-stu-id="3f47d-139">ID</span></span>           | `<Int32[]>`        | <span data-ttu-id="3f47d-140">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-140">No</span></span>  |
| <span data-ttu-id="3f47d-141">Szint</span><span class="sxs-lookup"><span data-stu-id="3f47d-141">Level</span></span>        | `<Int32[]>`        | <span data-ttu-id="3f47d-142">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-142">No</span></span>  |
| <span data-ttu-id="3f47d-143">Kezdés időpontja</span><span class="sxs-lookup"><span data-stu-id="3f47d-143">StartTime</span></span>    | `<DateTime>`       | <span data-ttu-id="3f47d-144">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-144">No</span></span>  |
| <span data-ttu-id="3f47d-145">Befejezés időpontja:</span><span class="sxs-lookup"><span data-stu-id="3f47d-145">EndTime</span></span>      | `<DateTime>`       | <span data-ttu-id="3f47d-146">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-146">No</span></span>  |
| <span data-ttu-id="3f47d-147">Felhasználói azonosító</span><span class="sxs-lookup"><span data-stu-id="3f47d-147">UserID</span></span>       | `<SID>`            | <span data-ttu-id="3f47d-148">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-148">No</span></span>  |
| <span data-ttu-id="3f47d-149">Adatok</span><span class="sxs-lookup"><span data-stu-id="3f47d-149">Data</span></span>         | `<String[]>`       | <span data-ttu-id="3f47d-150">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-150">No</span></span>  |
| *            | `<String[]>`       | <span data-ttu-id="3f47d-151">Nem</span><span class="sxs-lookup"><span data-stu-id="3f47d-151">No</span></span>  |

### <a name="building-a-query-with-a-hash-table"></a><span data-ttu-id="3f47d-152">Egy kivonattáblát a lekérdezés létrehozása</span><span class="sxs-lookup"><span data-stu-id="3f47d-152">Building a query with a hash table</span></span>

<span data-ttu-id="3f47d-153">Ellenőrizze az eredményeket, és problémák elhárításához, hozhat létre a kivonattábla egy segít **kulcs/érték** pár egyszerre.</span><span class="sxs-lookup"><span data-stu-id="3f47d-153">To verify results and troubleshoot problems, it helps to build the hash table one **key/value** pair at a time.</span></span> <span data-ttu-id="3f47d-154">A lekérdezés lekérdezi az adatokat a **alkalmazás** napló.</span><span class="sxs-lookup"><span data-stu-id="3f47d-154">The query gets data from the **Application** log.</span></span> <span data-ttu-id="3f47d-155">A kivonattáblában 03T00 `Get-WinEvent –LogName Application`.</span><span class="sxs-lookup"><span data-stu-id="3f47d-155">The hash table is equivalent to `Get-WinEvent –LogName Application`.</span></span>

<span data-ttu-id="3f47d-156">Első lépésként hozzon létre a `Get-WinEvent` lekérdezés.</span><span class="sxs-lookup"><span data-stu-id="3f47d-156">To begin, create the `Get-WinEvent` query.</span></span> <span data-ttu-id="3f47d-157">Használja a **FilterHashtable** paraméter **kulcs/érték** párosítsa a kulccsal **naplónév**, és az érték **alkalmazás**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-157">Use the **FilterHashtable** parameter's **key/value** pair with the key, **LogName**, and the value, **Application**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
}
```

<span data-ttu-id="3f47d-158">A kivonattáblában, és létrehozza a **ProviderName** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="3f47d-158">Continue to build the hash table with the **ProviderName** key.</span></span> <span data-ttu-id="3f47d-159">A **ProviderName** a neve jelenik meg a **forrás** mezőbe a **Windows Eseménynapló**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-159">The **ProviderName** is the name that appears in the **Source** field in the **Windows Event Viewer**.</span></span> <span data-ttu-id="3f47d-160">Ha például **.NET-futtatórendszer** a következő képernyőfelvételen látható:</span><span class="sxs-lookup"><span data-stu-id="3f47d-160">For example, **.NET Runtime** in the following screenshot:</span></span>

![Kép a Windows Eseménynapló-források.](./media/creating-get-winEvent-queries-with-filterhashtable/providername.png)

<span data-ttu-id="3f47d-162">Frissítse a kivonattáblában, és tartalmazza a **kulcs/érték** párosítsa a kulcs \*\* ProviderName, és az érték **.NET-futtatórendszer**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-162">Update the hash table and include the **key/value** pair with the key, \*\*ProviderName, and the value, **.NET Runtime**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
}
```

<span data-ttu-id="3f47d-163">Ha a lekérdezés adatokat kíván gyűjteni archivált eseménynaplók van szüksége, használja a **elérési út** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="3f47d-163">If your query needs to get data from archived event logs, use the **Path** key.</span></span> <span data-ttu-id="3f47d-164">A **elérési út** az érték határozza meg a naplófájl teljes elérési útja.</span><span class="sxs-lookup"><span data-stu-id="3f47d-164">The **Path** value specifies the full path to the log file.</span></span> <span data-ttu-id="3f47d-165">További információkért lásd: a **Scripting Guy** blogbejegyzésben [használja a Powershellt, elemezni a mentett eseménynaplóiban hibák](https://devblogs.microsoft.com/scripting/use-powershell-to-parse-saved-event-logs-for-errors).</span><span class="sxs-lookup"><span data-stu-id="3f47d-165">For more information, see the **Scripting Guy** blog post, [Use PowerShell to Parse Saved Event Logs for Errors](https://devblogs.microsoft.com/scripting/use-powershell-to-parse-saved-event-logs-for-errors).</span></span>

### <a name="using-enumerated-values-in-a-hash-table"></a><span data-ttu-id="3f47d-166">Egy kivonattáblát a felsorolt értékek használatával</span><span class="sxs-lookup"><span data-stu-id="3f47d-166">Using enumerated values in a hash table</span></span>

<span data-ttu-id="3f47d-167">**A kulcsszavak** a következő kulcs van a kivonattáblában.</span><span class="sxs-lookup"><span data-stu-id="3f47d-167">**Keywords** is the next key in the hash table.</span></span> <span data-ttu-id="3f47d-168">A **kulcsszavak** adattípusa tömbjét a `[long]` értéktípus sok társításához.</span><span class="sxs-lookup"><span data-stu-id="3f47d-168">The **Keywords** data type is an array of the `[long]` value type that holds a large number.</span></span> <span data-ttu-id="3f47d-169">Keresse meg a maximális értéke a következő paranccsal `[long]`:</span><span class="sxs-lookup"><span data-stu-id="3f47d-169">Use the following command to find the maximum value of `[long]`:</span></span>

```powershell
[long]::MaxValue
```

```Output
9223372036854775807
```

<span data-ttu-id="3f47d-170">Az a **kulcsszavak** kulcs PowerShell használ egy szám, karakterlánc például **biztonsági**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-170">For the **Keywords** key, PowerShell uses a number, not a string such as **Security**.</span></span> <span data-ttu-id="3f47d-171">**Windows-Eseménynapló** jeleníti meg a **kulcsszavak** , karakterláncok, de a felsorolt értékek.</span><span class="sxs-lookup"><span data-stu-id="3f47d-171">**Windows Event Viewer** displays the **Keywords** as strings, but they are enumerated values.</span></span> <span data-ttu-id="3f47d-172">A kivonattáblában, ha a **kulcsszavak** kulcsot karakterlánc-érték, egy hibaüzenet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3f47d-172">In the hash table, if you use the **Keywords** key with a string value, an error message is displayed.</span></span>

<span data-ttu-id="3f47d-173">Nyissa meg a **Windows Eseménynapló** és a **műveletek** panelen kattintson a **aktuális napló szűrése**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-173">Open the **Windows Event Viewer** and from the **Actions** pane, click on **Filter current log**.</span></span>
<span data-ttu-id="3f47d-174">A **kulcsszavak** legördülő menüből a rendelkezésre álló kulcsszavak jeleníti meg, az alábbi képernyőképen látható módon:</span><span class="sxs-lookup"><span data-stu-id="3f47d-174">The **Keywords** drop-down menu displays the available keywords, as shown in the following screenshot:</span></span>

![Kép a Windows Eseménynapló kulcsszavak.](./media/creating-get-winEvent-queries-with-filterhashtable/keywords.png)

<span data-ttu-id="3f47d-176">A következő parancs használatával megjelenítheti az `StandardEventKeywords` nevei.</span><span class="sxs-lookup"><span data-stu-id="3f47d-176">Use the following command to display the `StandardEventKeywords` property names.</span></span>

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventKeywords] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventKeywords
Name             MemberType Definition
—-             ———- ———-
AuditFailure     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
AuditSuccess     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
CorrelationHint2 Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
EventLogClassic  Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
None             Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
ResponseTime     Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
Sqm              Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiContext       Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
WdiDiagnostic    Property   static System.Diagnostics.Eventing.Reader.StandardEventKey…
```

<span data-ttu-id="3f47d-177">A felsorolt értékek vannak dokumentálva az **.NET-keretrendszer**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-177">The enumerated values are documented in the **.NET Framework**.</span></span> <span data-ttu-id="3f47d-178">További információkért lásd: [StandardEventKeywords enumerálás](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventkeywords?redirectedfrom=MSDN&view=netframework-4.7.2).</span><span class="sxs-lookup"><span data-stu-id="3f47d-178">For more information, see [StandardEventKeywords Enumeration](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventkeywords?redirectedfrom=MSDN&view=netframework-4.7.2).</span></span>

<span data-ttu-id="3f47d-179">A **kulcsszavak** neveket és a felsorolt értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="3f47d-179">The **Keywords** names and enumerated values are as follows:</span></span>

| <span data-ttu-id="3f47d-180">Név</span><span class="sxs-lookup"><span data-stu-id="3f47d-180">Name</span></span>             |  <span data-ttu-id="3f47d-181">Érték</span><span class="sxs-lookup"><span data-stu-id="3f47d-181">Value</span></span>            |
| ---------------- | ------------------|
| <span data-ttu-id="3f47d-182">AuditFailure</span><span class="sxs-lookup"><span data-stu-id="3f47d-182">AuditFailure</span></span>     | <span data-ttu-id="3f47d-183">4503599627370496</span><span class="sxs-lookup"><span data-stu-id="3f47d-183">4503599627370496</span></span>  |
| <span data-ttu-id="3f47d-184">AuditSuccess</span><span class="sxs-lookup"><span data-stu-id="3f47d-184">AuditSuccess</span></span>     | <span data-ttu-id="3f47d-185">9007199254740992</span><span class="sxs-lookup"><span data-stu-id="3f47d-185">9007199254740992</span></span>  |
| <span data-ttu-id="3f47d-186">CorrelationHint2</span><span class="sxs-lookup"><span data-stu-id="3f47d-186">CorrelationHint2</span></span> | <span data-ttu-id="3f47d-187">18014398509481984</span><span class="sxs-lookup"><span data-stu-id="3f47d-187">18014398509481984</span></span> |
| <span data-ttu-id="3f47d-188">EventLogClassic</span><span class="sxs-lookup"><span data-stu-id="3f47d-188">EventLogClassic</span></span>  | <span data-ttu-id="3f47d-189">36028797018963968</span><span class="sxs-lookup"><span data-stu-id="3f47d-189">36028797018963968</span></span> |
| <span data-ttu-id="3f47d-190">Sqm</span><span class="sxs-lookup"><span data-stu-id="3f47d-190">Sqm</span></span>              | <span data-ttu-id="3f47d-191">2251799813685248</span><span class="sxs-lookup"><span data-stu-id="3f47d-191">2251799813685248</span></span>  |
| <span data-ttu-id="3f47d-192">WdiDiagnostic</span><span class="sxs-lookup"><span data-stu-id="3f47d-192">WdiDiagnostic</span></span>    | <span data-ttu-id="3f47d-193">1125899906842624</span><span class="sxs-lookup"><span data-stu-id="3f47d-193">1125899906842624</span></span>  |
| <span data-ttu-id="3f47d-194">WdiContext</span><span class="sxs-lookup"><span data-stu-id="3f47d-194">WdiContext</span></span>       | <span data-ttu-id="3f47d-195">562949953421312</span><span class="sxs-lookup"><span data-stu-id="3f47d-195">562949953421312</span></span>   |
| <span data-ttu-id="3f47d-196">Válaszidő</span><span class="sxs-lookup"><span data-stu-id="3f47d-196">ResponseTime</span></span>     | <span data-ttu-id="3f47d-197">281474976710656</span><span class="sxs-lookup"><span data-stu-id="3f47d-197">281474976710656</span></span>   |
| <span data-ttu-id="3f47d-198">Egyik sem</span><span class="sxs-lookup"><span data-stu-id="3f47d-198">None</span></span>             | <span data-ttu-id="3f47d-199">0</span><span class="sxs-lookup"><span data-stu-id="3f47d-199">0</span></span>                 |

<span data-ttu-id="3f47d-200">Frissítse a kivonattáblában, és tartalmazza a **kulcs/érték** párosítsa a kulccsal **kulcsszavak**, és a **EventLogClassic** felsorolási érték **36028797018963968** .</span><span class="sxs-lookup"><span data-stu-id="3f47d-200">Update the hash table and include the **key/value** pair with the key, **Keywords**, and the **EventLogClassic** enumeration value, **36028797018963968**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
}
```

#### <a name="keywords-static-property-value-optional"></a><span data-ttu-id="3f47d-201">A kulcsszavak statikus tulajdonság értéke (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="3f47d-201">Keywords static property value (optional)</span></span>

<span data-ttu-id="3f47d-202">A **kulcsszavak** kulcs számbavétele megtörtént, de a Jelszókivonat-tábla lekérdezése a statikus tulajdonság nevét is használhatja.</span><span class="sxs-lookup"><span data-stu-id="3f47d-202">The **Keywords** key is enumerated, but you can use a static property name in the hash table query.</span></span>
<span data-ttu-id="3f47d-203">Ahelyett, hogy a visszaadott karakterláncban használja, a tulajdonság nevét kell konvertálni egy értéket a **Value__** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3f47d-203">Rather than using the returned string, the property name must be converted to a value with the **Value__** property.</span></span>

<span data-ttu-id="3f47d-204">Ha például az alábbi szkript a **Value__** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3f47d-204">For example, the following script uses the **Value__** property.</span></span>

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventKeywords]::EventLogClassic
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=$C.Value__
}
```

### <a name="filtering-by-event-id"></a><span data-ttu-id="3f47d-205">Eseményazonosító szerinti szűrés</span><span class="sxs-lookup"><span data-stu-id="3f47d-205">Filtering by Event Id</span></span>

<span data-ttu-id="3f47d-206">Részletesebb adatok lekéréséhez a lekérdezési eredmények alapján vannak szűrve **eseményazonosító**. A **eseményazonosító** hivatkozik a kivonattábla kulcsa **azonosító** és a egy adott érték **eseményazonosító**. A **Windows Eseménynapló** jeleníti meg a **eseményazonosító**. Ez a példa **Event Id 1023**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-206">To get more specific data, the query's results are filtered by **Event Id**. The **Event Id** is referenced in the hash table as the key **ID** and the value is a specific **Event Id**. The **Windows Event Viewer** displays the **Event Id**. This example uses **Event Id 1023**.</span></span>

<span data-ttu-id="3f47d-207">Frissítse a kivonattáblában, és tartalmazza a **kulcs/érték** párosítsa a kulccsal **azonosító** és az érték **1023**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-207">Update the hash table and include the **key/value** pair with the key, **ID** and the value, **1023**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
}
```

### <a name="filtering-by-level"></a><span data-ttu-id="3f47d-208">Szűrési szint szerint</span><span class="sxs-lookup"><span data-stu-id="3f47d-208">Filtering by Level</span></span>

<span data-ttu-id="3f47d-209">További eredmények szűkítéséhez, és csak a hibák események tartalmazzák, használja a **szint** kulcsot.</span><span class="sxs-lookup"><span data-stu-id="3f47d-209">To further refine the results and include only events that are errors, use the **Level** key.</span></span>
<span data-ttu-id="3f47d-210">**Windows-Eseménynapló** jeleníti meg a **szint** , karakterlánc-értékeket, de a felsorolt értékek.</span><span class="sxs-lookup"><span data-stu-id="3f47d-210">**Windows Event Viewer** displays the **Level** as string values, but they are enumerated values.</span></span> <span data-ttu-id="3f47d-211">A kivonattáblában, ha a **szint** kulcsot karakterlánc-érték, egy hibaüzenet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3f47d-211">In the hash table, if you use the **Level** key with a string value, an error message is displayed.</span></span>

<span data-ttu-id="3f47d-212">**Szint** értékkel rendelkezik, mint például **hiba**, **figyelmeztetés**, vagy **tájékoztató**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-212">**Level** has values such as **Error**, **Warning**, or **Informational**.</span></span> <span data-ttu-id="3f47d-213">A következő parancs használatával megjelenítheti az `StandardEventLevel` nevei.</span><span class="sxs-lookup"><span data-stu-id="3f47d-213">Use the following command to display the `StandardEventLevel` property names.</span></span>

```powershell
[System.Diagnostics.Eventing.Reader.StandardEventLevel] | Get-Member -Static -MemberType Property
```

```Output
   TypeName: System.Diagnostics.Eventing.Reader.StandardEventLevel

Name          MemberType Definition
----          ---------- ----------
Critical      Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Critical {get;}
Error         Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Error {get;}
Informational Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Informational {get;}
LogAlways     Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel LogAlways {get;}
Verbose       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Verbose {get;}
Warning       Property   static System.Diagnostics.Eventing.Reader.StandardEventLevel Warning {get;}
```

<span data-ttu-id="3f47d-214">A felsorolt értékek vannak dokumentálva az **.NET-keretrendszer**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-214">The enumerated values are documented in the **.NET Framework**.</span></span> <span data-ttu-id="3f47d-215">További információkért lásd: [StandardEventLevel enumerálás](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventlevel?redirectedfrom=MSDN&view=netframework-4.7.2).</span><span class="sxs-lookup"><span data-stu-id="3f47d-215">For more information, see [StandardEventLevel Enumeration](https://docs.microsoft.com/en-us/dotnet/api/system.diagnostics.eventing.reader.standardeventlevel?redirectedfrom=MSDN&view=netframework-4.7.2).</span></span>

<span data-ttu-id="3f47d-216">A **szint** kulcs nevét és a felsorolt értékek a következők:</span><span class="sxs-lookup"><span data-stu-id="3f47d-216">The **Level** key's names and enumerated values are as follows:</span></span>

| <span data-ttu-id="3f47d-217">Név</span><span class="sxs-lookup"><span data-stu-id="3f47d-217">Name</span></span>           | <span data-ttu-id="3f47d-218">Érték</span><span class="sxs-lookup"><span data-stu-id="3f47d-218">Value</span></span> |
| -------------- | ----- |
| <span data-ttu-id="3f47d-219">Részletes</span><span class="sxs-lookup"><span data-stu-id="3f47d-219">Verbose</span></span>        |   <span data-ttu-id="3f47d-220">5</span><span class="sxs-lookup"><span data-stu-id="3f47d-220">5</span></span>   |
| <span data-ttu-id="3f47d-221">Tájékoztatás</span><span class="sxs-lookup"><span data-stu-id="3f47d-221">Informational</span></span>  |   <span data-ttu-id="3f47d-222">4</span><span class="sxs-lookup"><span data-stu-id="3f47d-222">4</span></span>   |
| <span data-ttu-id="3f47d-223">Figyelmeztetés</span><span class="sxs-lookup"><span data-stu-id="3f47d-223">Warning</span></span>        |   <span data-ttu-id="3f47d-224">3</span><span class="sxs-lookup"><span data-stu-id="3f47d-224">3</span></span>   |
| <span data-ttu-id="3f47d-225">Hiba</span><span class="sxs-lookup"><span data-stu-id="3f47d-225">Error</span></span>          |   <span data-ttu-id="3f47d-226">2</span><span class="sxs-lookup"><span data-stu-id="3f47d-226">2</span></span>   |
| <span data-ttu-id="3f47d-227">Kritikus</span><span class="sxs-lookup"><span data-stu-id="3f47d-227">Critical</span></span>       |   <span data-ttu-id="3f47d-228">1</span><span class="sxs-lookup"><span data-stu-id="3f47d-228">1</span></span>   |
| <span data-ttu-id="3f47d-229">LogAlways</span><span class="sxs-lookup"><span data-stu-id="3f47d-229">LogAlways</span></span>      |   <span data-ttu-id="3f47d-230">0</span><span class="sxs-lookup"><span data-stu-id="3f47d-230">0</span></span>   |

<span data-ttu-id="3f47d-231">A kivonattábla a befejezett lekérdezés tartalmazza a kulcs **szint**, és az érték **2**.</span><span class="sxs-lookup"><span data-stu-id="3f47d-231">The hash table for the completed query includes the key, **Level**, and the value, **2**.</span></span>

```powershell
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=2
}
```

#### <a name="level-static-property-in-enumeration-optional"></a><span data-ttu-id="3f47d-232">Szolgáltatói statikus tulajdonság frissítése az enumerálás (nem kötelező)</span><span class="sxs-lookup"><span data-stu-id="3f47d-232">Level static property in enumeration (optional)</span></span>

<span data-ttu-id="3f47d-233">A **szint** kulcs számbavétele megtörtént, de a Jelszókivonat-tábla lekérdezése a statikus tulajdonság nevét is használhatja.</span><span class="sxs-lookup"><span data-stu-id="3f47d-233">The **Level** key is enumerated, but you can use a static property name in the hash table query.</span></span>
<span data-ttu-id="3f47d-234">Ahelyett, hogy a visszaadott karakterláncban használja, a tulajdonság nevét kell konvertálni egy értéket a **Value__** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3f47d-234">Rather than using the returned string, the property name must be converted to a value with the **Value__** property.</span></span>

<span data-ttu-id="3f47d-235">Ha például az alábbi szkript a **Value__** tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3f47d-235">For example, the following script uses the **Value__** property.</span></span>

```powershell
$C = [System.Diagnostics.Eventing.Reader.StandardEventLevel]::Informational
Get-WinEvent -FilterHashtable @{
   LogName='Application'
   ProviderName='.NET Runtime'
   Keywords=36028797018963968
   ID=1023
   Level=$C.Value__
}
```