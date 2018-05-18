---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: A WMF 5.1 hibajavítások
ms.openlocfilehash: 1e46d6d0419b3497450e6eaddbaa47456b004691
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="bug-fixes-in-wmf-51"></a><span data-ttu-id="2c935-103">A WMF 5.1# hibajavítások</span><span class="sxs-lookup"><span data-stu-id="2c935-103">Bug Fixes in WMF 5.1#</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2c935-104">Hibajavítások</span><span class="sxs-lookup"><span data-stu-id="2c935-104">Bug fixes</span></span> ##

<span data-ttu-id="2c935-105">A következő fontos hibákat WMF 5.1 Fix:</span><span class="sxs-lookup"><span data-stu-id="2c935-105">The following notable bugs are fixed in WMF 5.1:</span></span>

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a><span data-ttu-id="2c935-106">A modul automatikus felderítési teljesen eleget tegyen `$env:PSModulePath`</span><span class="sxs-lookup"><span data-stu-id="2c935-106">Module auto-discovery fully honors `$env:PSModulePath`</span></span> ###

<span data-ttu-id="2c935-107">WMF 3 bevezetett modul automatikus felderítését (betöltése modulok automatikusan egy explicit Import-Module parancs meghívásakor nélkül).</span><span class="sxs-lookup"><span data-stu-id="2c935-107">Module auto-discovery (loading modules automatically without an explicit Import-Module when calling a command) was introduced in WMF 3.</span></span>
<span data-ttu-id="2c935-108">Amikor jelenik meg, PowerShell-parancsok ellenőrzi `$PSHome\Modules` használata előtt `$env:PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="2c935-108">When introduced, PowerShell checked for commands in `$PSHome\Modules` before using `$env:PSModulePath`.</span></span>

<span data-ttu-id="2c935-109">WMF 5.1 módosítja ezt a viselkedést tiszteletben `$env:PSModulePath` teljesen.</span><span class="sxs-lookup"><span data-stu-id="2c935-109">WMF 5.1 changes this behavior to honor `$env:PSModulePath` completely.</span></span>
<span data-ttu-id="2c935-110">Ez lehetővé teszi, hogy egy felhasználó által létrehozott modul, amely meghatározza a PowerShell által biztosított parancsok (pl. `Get-ChildItem`) automatikus-betöltését és megfelelően felülírja a beépített parancsot.</span><span class="sxs-lookup"><span data-stu-id="2c935-110">This allows for a user-authored module that defines commands provided by PowerShell (e.g. `Get-ChildItem`) to be auto-loaded and correctly overriding the built-in command.</span></span>

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a><span data-ttu-id="2c935-111">Átirányítás nem hosszabb paraméterekként fájl `-Encoding Unicode`</span><span class="sxs-lookup"><span data-stu-id="2c935-111">File redirection no longer hard-codes `-Encoding Unicode`</span></span> ###

<span data-ttu-id="2c935-112">PowerShell korábbi verzióiban szabályozásához használja a fájl átirányító operátort, pl. kódolása lehetetlen volt `Get-ChildItem > out.txt` mivel adja meg a PowerShell `-Encoding Unicode`.</span><span class="sxs-lookup"><span data-stu-id="2c935-112">In all previous versions of PowerShell, it was impossible to control the file encoding used by the file redirection operator, e.g. `Get-ChildItem > out.txt` because PowerShell added `-Encoding Unicode`.</span></span>

<span data-ttu-id="2c935-113">WMF 5.1 kezdve, módosíthatja a fájlkódolás átirányítás úgy, hogy `$PSDefaultParameterValues`:</span><span class="sxs-lookup"><span data-stu-id="2c935-113">Starting with WMF 5.1, you can now change the file encoding of redirection by setting `$PSDefaultParameterValues`:</span></span>

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a><span data-ttu-id="2c935-114">Rögzített egy regressziós tagjai eléréséhez `System.Reflection.TypeInfo`</span><span class="sxs-lookup"><span data-stu-id="2c935-114">Fixed a regression in accessing members of `System.Reflection.TypeInfo`</span></span> ###

<span data-ttu-id="2c935-115">A WMF 5.0 rendszerben bevezetett regressziós túllépte elérése során tagjai `System.Reflection.RuntimeType`, pl. `[int].ImplementedInterfaces`.</span><span class="sxs-lookup"><span data-stu-id="2c935-115">A regression introduced in WMF 5.0 broke accessing members of `System.Reflection.RuntimeType`, e.g. `[int].ImplementedInterfaces`.</span></span>
<span data-ttu-id="2c935-116">Ez a hiba kijavítása WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="2c935-116">This bug has been fixed in WMF 5.1.</span></span>


### <a name="fixed-some-issues-with-com-objects"></a><span data-ttu-id="2c935-117">Bizonyos problémák rögzített COM-objektumok</span><span class="sxs-lookup"><span data-stu-id="2c935-117">Fixed some issues with COM objects</span></span> ###

<span data-ttu-id="2c935-118">WMF 5.0 rendszerben jelent meg egy új COM kötő hívása módszerek COM objektum és a COM-objektumok tulajdonságainak elérése során.</span><span class="sxs-lookup"><span data-stu-id="2c935-118">WMF 5.0 introduced a new COM binder for invoking methods on COM objects and accessing properties of COM objects.</span></span>
<span data-ttu-id="2c935-119">Az új kötő jelentősen növeli a teljesítményt, de is bevezetni az egyes hibák, amelyek WMF 5.1 rögzített.</span><span class="sxs-lookup"><span data-stu-id="2c935-119">This new binder improved performance significantly but also introduced some bugs which have been fixed in WMF 5.1.</span></span>

#### <a name="argument-conversions-were-not-always-performed-correctly"></a><span data-ttu-id="2c935-120">Argumentum átalakítások nem mindig elvégzett megfelelően</span><span class="sxs-lookup"><span data-stu-id="2c935-120">Argument conversions were not always performed correctly</span></span> ####

<span data-ttu-id="2c935-121">A következő példa:</span><span class="sxs-lookup"><span data-stu-id="2c935-121">In the following example:</span></span>

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

<span data-ttu-id="2c935-122">A SendKeys metódus karakterláncot vár, de a PowerShell nem konvertálható a char, karakterlánc késleltető IDispatch::Invoke, amely VariantChangeType használja az átalakítás, amely ebben a példában a kulcsokat, "1", "7" és "3" helyett küldése átalakítása a várt Volume.Mute kulcs.</span><span class="sxs-lookup"><span data-stu-id="2c935-122">The SendKeys method expects a string, but PowerShell did not convert the char to a string, deferring the conversion to IDispatch::Invoke, which uses VariantChangeType to do the conversion, which in this example resulted in sending the keys '1', '7', and '3' instead of the expected Volume.Mute key.</span></span>

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a><span data-ttu-id="2c935-123">Enumerálható COM-objektumok nem mindig megfelelő kezelése</span><span class="sxs-lookup"><span data-stu-id="2c935-123">Enumerable COM objects not always handled correctly</span></span> ####

<span data-ttu-id="2c935-124">PowerShell általában a legtöbb enumerálható objektum enumerálása, de a WMF 5.0 rendszerben bevezetett regressziós miatt nem sikerült az IEnumerable illesztőfelületet megvalósító COM-objektumok számbavétele.</span><span class="sxs-lookup"><span data-stu-id="2c935-124">PowerShell normally enumerates most enumerable objects, but a regression introduced in WMF 5.0 prevented the enumeration of COM objects that implement IEnumerable.</span></span>  <span data-ttu-id="2c935-125">Például:</span><span class="sxs-lookup"><span data-stu-id="2c935-125">For example:</span></span>

```
function Get-COMDictionary
{
    $d = New-Object -ComObject Scripting.Dictionary
    $d.Add('a', 2)
    $d.Add('b', 2)
    return $d
}

$x = Get-COMDictionary
```

<span data-ttu-id="2c935-126">A fenti példában WMF 5.0 nem megfelelően megírt a Scripting.Dictionary az adatcsatornához helyett a kulcs/érték párok enumerálása.</span><span class="sxs-lookup"><span data-stu-id="2c935-126">In the above example, WMF 5.0 incorrectly wrote the Scripting.Dictionary to the pipeline instead of enumerating the key/value pairs.</span></span>

<span data-ttu-id="2c935-127">Ez is módosítja címek [adja ki a Connect 1752224](https://connect.microsoft.com/PowerShell/feedback/details/1752224)</span><span class="sxs-lookup"><span data-stu-id="2c935-127">This change also addresses [issue 1752224 on Connect](https://connect.microsoft.com/PowerShell/feedback/details/1752224)</span></span>

### <a name="ordered-was-not-allowed-inside-classes"></a><span data-ttu-id="2c935-128">`[ordered]` nem volt engedélyezett osztályok</span><span class="sxs-lookup"><span data-stu-id="2c935-128">`[ordered]` was not allowed inside classes</span></span> ###

<span data-ttu-id="2c935-129">WMF 5.0 rendszerben jelent meg osztályok osztályok használt típus szövegkonstans-érvényesítéssel.</span><span class="sxs-lookup"><span data-stu-id="2c935-129">WMF 5.0 introduced classes with validation of type literals used in classes.</span></span>
<span data-ttu-id="2c935-130">`[ordered]` a következőképpen néz típusú szövegkonstansnak, de nincs true .NET-típus.</span><span class="sxs-lookup"><span data-stu-id="2c935-130">`[ordered]` looks like a type literal but is not a true .NET type.</span></span>
<span data-ttu-id="2c935-131">WMF 5.0 helytelenül jelentett hiba `[ordered]` osztály belül:</span><span class="sxs-lookup"><span data-stu-id="2c935-131">WMF 5.0 incorrectly reported an error on `[ordered]` inside a class:</span></span>

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a><span data-ttu-id="2c935-132">A használatára vonatkozó súgó megjelenítéséhez többféle verzióját tartalmazó témakörök nem működik.</span><span class="sxs-lookup"><span data-stu-id="2c935-132">Help on About topics with multiple versions does not work</span></span> ###

<span data-ttu-id="2c935-133">WMF 5.1, ha volt a telepített modulokban különböző verzióinak és állnak az adott témakör, például megosztott about_PSReadline, mielőtt `help about_PSReadline` meghaladná a megfelelő módszer valós súgójának megtekintéséhez több témakör.</span><span class="sxs-lookup"><span data-stu-id="2c935-133">Before WMF 5.1, if you had multiple versions of a module installed and they all shared a help topic, for example, about_PSReadline, `help about_PSReadline` would return multiple topics with no obvious way to view the real help.</span></span>

<span data-ttu-id="2c935-134">WMF 5.1 Ez javítja, vissza a Súgó gombra a témakör a legújabb verzióját.</span><span class="sxs-lookup"><span data-stu-id="2c935-134">WMF 5.1 fixes this by returning the help for the latest version of the topic.</span></span>

<span data-ttu-id="2c935-135">`Get-Help` nem biztosít annak meghatározására, hogy melyik verzió a súgóját meg szeretné tekinteni.</span><span class="sxs-lookup"><span data-stu-id="2c935-135">`Get-Help` does not provide a way to specify which version you want help for.</span></span>
<span data-ttu-id="2c935-136">Ez elkerülhető, keresse meg a modulok könyvtárát, és tekintse át a közvetlenül az egy eszköz, például a kedvenc szerkesztő súgóját.</span><span class="sxs-lookup"><span data-stu-id="2c935-136">To work around this, navigate to the modules directory and view the help directly with a tool like your favorite editor.</span></span>

### <a name="powershellexe-reading-from-stdin-stopped-working"></a><span data-ttu-id="2c935-137">a STDIN olvasásakor PowerShell.exe leállt</span><span class="sxs-lookup"><span data-stu-id="2c935-137">powershell.exe reading from STDIN stopped working</span></span>

<span data-ttu-id="2c935-138">Az ügyfelek `powershell -command -` a PowerShell végrehajtása natív alkalmazás való átadása a parancsfájlban szereplő keresztül STDIN Sajnos ez volt miatt hibás más jellegű módosítását a konzol állomás.</span><span class="sxs-lookup"><span data-stu-id="2c935-138">Customers use `powershell -command -` from native apps to execute PowerShell passing in the script via STDIN unfortunately this was broken due to other changes it the console host.</span></span>

https://windowsserver.uservoice.com/forums/301869-powershell/suggestions/15854689-powershell-exe-command-is-broken-on-windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a><span data-ttu-id="2c935-139">PowerShell.exe csúcs a CPU-használat indításakor hoz létre.</span><span class="sxs-lookup"><span data-stu-id="2c935-139">powershell.exe creates spike in CPU usage on startup</span></span>

<span data-ttu-id="2c935-140">PowerShell WMI-lekérdezés segítségével ellenőrizze, hogy a késleltetést okoz a bejelentkezési elkerülése érdekében a csoportházirend segítségével indítása.</span><span class="sxs-lookup"><span data-stu-id="2c935-140">PowerShell uses a WMI query to check if it was started via Group Policy to avoid causing delay in login.</span></span>
<span data-ttu-id="2c935-141">A WMI-lekérdezést említi tzres.mui.dll beszúrva a rendszer minden folyamatba, mivel a WMI Win32_Process osztály megpróbálja beolvasni a helyi időzóna adatait.</span><span class="sxs-lookup"><span data-stu-id="2c935-141">The WMI query ends up injecting tzres.mui.dll into every process on the system since the WMI Win32_Process class attempts to retrieve local timezone information.</span></span>
<span data-ttu-id="2c935-142">Ennek eredményeképp a nagy CPU-csúcs az igények wmiprvse (a WMI szolgáltató fogadó).</span><span class="sxs-lookup"><span data-stu-id="2c935-142">This results in a large CPU spike in wmiprvse (the WMI provider host).</span></span>
<span data-ttu-id="2c935-143">Javítsa ki, hogy Win32 API-hívások használja ugyanazokat az információkat a WMI használata helyett.</span><span class="sxs-lookup"><span data-stu-id="2c935-143">Fix is to use Win32 API calls to get the same information instead of using WMI.</span></span>
