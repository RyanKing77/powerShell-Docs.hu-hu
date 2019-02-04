---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: WMF, powershell, beállítás
title: Hibajavításokat tartalmaz a WMF 5.1
ms.openlocfilehash: d2cf44753a7cb54897e76cf914a8fef0f4aecf1e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684149"
---
# <a name="bug-fixes-in-wmf-51"></a><span data-ttu-id="d5c17-103">Hibajavításokat tartalmaz a WMF 5.1-es #</span><span class="sxs-lookup"><span data-stu-id="d5c17-103">Bug Fixes in WMF 5.1#</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="d5c17-104">Hibajavítások</span><span class="sxs-lookup"><span data-stu-id="d5c17-104">Bug fixes</span></span> ##

<span data-ttu-id="d5c17-105">A következő jelentős programhibákat a WMF 5.1:</span><span class="sxs-lookup"><span data-stu-id="d5c17-105">The following notable bugs are fixed in WMF 5.1:</span></span>

### <a name="module-auto-discovery-fully-honors-envpsmodulepath"></a><span data-ttu-id="d5c17-106">Teljes körűen figyelembe veszi az automatikus felderítési modul `$env:PSModulePath`</span><span class="sxs-lookup"><span data-stu-id="d5c17-106">Module auto-discovery fully honors `$env:PSModulePath`</span></span> ###

<span data-ttu-id="d5c17-107">A modul automatikus felderítési (betöltése modulok automatikusan, egy explicit Import-Module-parancs meghívásakor nélkül) a WMF 3 jelent meg.</span><span class="sxs-lookup"><span data-stu-id="d5c17-107">Module auto-discovery (loading modules automatically without an explicit Import-Module when calling a command) was introduced in WMF 3.</span></span>
<span data-ttu-id="d5c17-108">Vezetett be, amikor PowerShell ellenőrzi a parancsok `$PSHome\Modules` használata előtt `$env:PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="d5c17-108">When introduced, PowerShell checked for commands in `$PSHome\Modules` before using `$env:PSModulePath`.</span></span>

<span data-ttu-id="d5c17-109">A WMF 5.1 módosítja ezt a viselkedést, hogy tartsa tiszteletben `$env:PSModulePath` teljesen.</span><span class="sxs-lookup"><span data-stu-id="d5c17-109">WMF 5.1 changes this behavior to honor `$env:PSModulePath` completely.</span></span>
<span data-ttu-id="d5c17-110">Ez lehetővé teszi egy felhasználó által létrehozott modul, amely meghatározza a PowerShell által biztosított parancsok (pl. `Get-ChildItem`) automatikus – betöltését és a beépített parancsa megfelelően felülírása.</span><span class="sxs-lookup"><span data-stu-id="d5c17-110">This allows for a user-authored module that defines commands provided by PowerShell (e.g. `Get-ChildItem`) to be auto-loaded and correctly overriding the built-in command.</span></span>

### <a name="file-redirection-no-longer-hard-codes--encoding-unicode"></a><span data-ttu-id="d5c17-111">Átirányítási fájlt nem hosszabb rögzített kódok `-Encoding Unicode`</span><span class="sxs-lookup"><span data-stu-id="d5c17-111">File redirection no longer hard-codes `-Encoding Unicode`</span></span> ###

<span data-ttu-id="d5c17-112">PowerShell korábbi verzióiban lehetetlen szabályozhatja, hogy a fájl kódolása például a fájl átirányítás operátor által használt volt `Get-ChildItem > out.txt` mert PowerShell hozzáadott `-Encoding Unicode`.</span><span class="sxs-lookup"><span data-stu-id="d5c17-112">In all previous versions of PowerShell, it was impossible to control the file encoding used by the file redirection operator, e.g. `Get-ChildItem > out.txt` because PowerShell added `-Encoding Unicode`.</span></span>

<span data-ttu-id="d5c17-113">A WMF 5.1-es verziótól kezdődően most módosíthatja a fájl kódolása átirányítás beállításával `$PSDefaultParameterValues`:</span><span class="sxs-lookup"><span data-stu-id="d5c17-113">Starting with WMF 5.1, you can now change the file encoding of redirection by setting `$PSDefaultParameterValues`:</span></span>

```
$PSDefaultParameterValues["Out-File:Encoding"] = "Ascii"
```

### <a name="fixed-a-regression-in-accessing-members-of-systemreflectiontypeinfo"></a><span data-ttu-id="d5c17-114">Rögzített elérése során tagjai regresszió `System.Reflection.TypeInfo`</span><span class="sxs-lookup"><span data-stu-id="d5c17-114">Fixed a regression in accessing members of `System.Reflection.TypeInfo`</span></span> ###

<span data-ttu-id="d5c17-115">A WMF 5.0 rendszerben bevezetett regresszió érvénytelenítése elérésére tagjai `System.Reflection.RuntimeType`, pl. `[int].ImplementedInterfaces`.</span><span class="sxs-lookup"><span data-stu-id="d5c17-115">A regression introduced in WMF 5.0 broke accessing members of `System.Reflection.RuntimeType`, e.g. `[int].ImplementedInterfaces`.</span></span>
<span data-ttu-id="d5c17-116">Ezt a hibát a WMF 5.1 megoldották.</span><span class="sxs-lookup"><span data-stu-id="d5c17-116">This bug has been fixed in WMF 5.1.</span></span>


### <a name="fixed-some-issues-with-com-objects"></a><span data-ttu-id="d5c17-117">Bizonyos problémák rögzített COM-objektumok</span><span class="sxs-lookup"><span data-stu-id="d5c17-117">Fixed some issues with COM objects</span></span> ###

<span data-ttu-id="d5c17-118">A WMF 5.0 bevezetett egy új COM vyvolání metody COM-objektumok és COM-objektumok elérésére tulajdonságait a Binder létrehozása.</span><span class="sxs-lookup"><span data-stu-id="d5c17-118">WMF 5.0 introduced a new COM binder for invoking methods on COM objects and accessing properties of COM objects.</span></span>
<span data-ttu-id="d5c17-119">Az új binder jelentősen javult a teljesítmény, de bizonyos hibák, amelyek kijavítása megtörtént a WMF 5.1 is bevezetett.</span><span class="sxs-lookup"><span data-stu-id="d5c17-119">This new binder improved performance significantly but also introduced some bugs which have been fixed in WMF 5.1.</span></span>

#### <a name="argument-conversions-were-not-always-performed-correctly"></a><span data-ttu-id="d5c17-120">Argumentum-átalakítás nem lettek mindig végrehajtva megfelelően</span><span class="sxs-lookup"><span data-stu-id="d5c17-120">Argument conversions were not always performed correctly</span></span> ####

<span data-ttu-id="d5c17-121">Az alábbi példában:</span><span class="sxs-lookup"><span data-stu-id="d5c17-121">In the following example:</span></span>

```
$obj = New-Object -ComObject WScript.Shell
$obj.SendKeys([char]173)
```

<span data-ttu-id="d5c17-122">A SendKeys metódus karakterláncot vár, de a PowerShell nem konvertálható a char egy karakterlánc IDispatch::Invoke, amely VariantChangeType használnak az átalakítást, amely ebben a példában az "1", "7" és "3" kulcsok küldése inkább eredményezett való átalakítás elhalasztása a várt Volume.Mute kulcs.</span><span class="sxs-lookup"><span data-stu-id="d5c17-122">The SendKeys method expects a string, but PowerShell did not convert the char to a string, deferring the conversion to IDispatch::Invoke, which uses VariantChangeType to do the conversion, which in this example resulted in sending the keys '1', '7', and '3' instead of the expected Volume.Mute key.</span></span>

#### <a name="enumerable-com-objects-not-always-handled-correctly"></a><span data-ttu-id="d5c17-123">COM-objektumok enumerálható nem mindig kezelése</span><span class="sxs-lookup"><span data-stu-id="d5c17-123">Enumerable COM objects not always handled correctly</span></span> ####

<span data-ttu-id="d5c17-124">PowerShell általában a legtöbb enumerálható objektumok enumerálása, de a WMF 5.0 rendszerben bevezetett regresszió miatt nem sikerült a valósítania az IEnumerable illesztőfelületet COM-objektumok enumerálása.</span><span class="sxs-lookup"><span data-stu-id="d5c17-124">PowerShell normally enumerates most enumerable objects, but a regression introduced in WMF 5.0 prevented the enumeration of COM objects that implement IEnumerable.</span></span>  <span data-ttu-id="d5c17-125">Például:</span><span class="sxs-lookup"><span data-stu-id="d5c17-125">For example:</span></span>

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

<span data-ttu-id="d5c17-126">A fenti példában a WMF 5.0 helytelenül írt a Scripting.Dictionary számbavétele a kulcs/érték párok helyett a folyamat számára.</span><span class="sxs-lookup"><span data-stu-id="d5c17-126">In the above example, WMF 5.0 incorrectly wrote the Scripting.Dictionary to the pipeline instead of enumerating the key/value pairs.</span></span>

<span data-ttu-id="d5c17-127">Ez a módosítás is címek [ki 1752224 a Connect webhelyen](https://connect.microsoft.com/PowerShell/feedback/details/1752224)</span><span class="sxs-lookup"><span data-stu-id="d5c17-127">This change also addresses [issue 1752224 on Connect](https://connect.microsoft.com/PowerShell/feedback/details/1752224)</span></span>

### <a name="ordered-was-not-allowed-inside-classes"></a><span data-ttu-id="d5c17-128">`[ordered]` nem volt engedélyezett osztályok</span><span class="sxs-lookup"><span data-stu-id="d5c17-128">`[ordered]` was not allowed inside classes</span></span> ###

<span data-ttu-id="d5c17-129">A WMF 5.0 osztályokat az osztályok a használt típusú literálok érvényesítése vezetett be.</span><span class="sxs-lookup"><span data-stu-id="d5c17-129">WMF 5.0 introduced classes with validation of type literals used in classes.</span></span>
<span data-ttu-id="d5c17-130">`[ordered]` néz ki egy típusú konstans azonban nem igaz typ .NET.</span><span class="sxs-lookup"><span data-stu-id="d5c17-130">`[ordered]` looks like a type literal but is not a true .NET type.</span></span>
<span data-ttu-id="d5c17-131">A WMF 5.0 helytelenül jelentett hiba `[ordered]` osztály belül:</span><span class="sxs-lookup"><span data-stu-id="d5c17-131">WMF 5.0 incorrectly reported an error on `[ordered]` inside a class:</span></span>

```
class CThing
{
    [object] foo($i)
    {
        [ordered]@{ Thing = $i }
    }
}
```


### <a name="help-on-about-topics-with-multiple-versions-does-not-work"></a><span data-ttu-id="d5c17-132">Súgó a többféle verzióját tartalmazó témakörök nem működik.</span><span class="sxs-lookup"><span data-stu-id="d5c17-132">Help on About topics with multiple versions does not work</span></span> ###

<span data-ttu-id="d5c17-133">A WMF 5.1-es, ha már telepített modulokban több verzióját, és azok minden megosztott súgótémakör, például about_PSReadline, mielőtt `help about_PSReadline` több témakörök a megfelelő módszer a valódi súgójának megtekintéséhez adna vissza.</span><span class="sxs-lookup"><span data-stu-id="d5c17-133">Before WMF 5.1, if you had multiple versions of a module installed and they all shared a help topic, for example, about_PSReadline, `help about_PSReadline` would return multiple topics with no obvious way to view the real help.</span></span>

<span data-ttu-id="d5c17-134">A WMF 5.1 javítja, ez visszaadó súgóját, a legújabb verzióra, a következő témakörben.</span><span class="sxs-lookup"><span data-stu-id="d5c17-134">WMF 5.1 fixes this by returning the help for the latest version of the topic.</span></span>

<span data-ttu-id="d5c17-135">`Get-Help` nem biztosít annak meghatározására, hogy melyik verziót szeretné súgóját.</span><span class="sxs-lookup"><span data-stu-id="d5c17-135">`Get-Help` does not provide a way to specify which version you want help for.</span></span>
<span data-ttu-id="d5c17-136">Ennek megoldásához keresse meg a modulok könyvtárát, és közvetlenül a olyan eszköz, például a kedvenc szerkesztőjében súgójának megtekintéséhez.</span><span class="sxs-lookup"><span data-stu-id="d5c17-136">To work around this, navigate to the modules directory and view the help directly with a tool like your favorite editor.</span></span>

### <a name="powershellexe-reading-from-stdin-stopped-working"></a><span data-ttu-id="d5c17-137">a PowerShell.exe STDIN olvasásakor leállt</span><span class="sxs-lookup"><span data-stu-id="d5c17-137">powershell.exe reading from STDIN stopped working</span></span>

<span data-ttu-id="d5c17-138">Az ügyfelek `powershell -command -` PowerShell végrehajtásához natív alkalmazásaitól a szkriptben Sajnos ez lett osztva más változtatások miatt STDIN keresztül adná azt át a konzol-gazdakörnyezethez.</span><span class="sxs-lookup"><span data-stu-id="d5c17-138">Customers use `powershell -command -` from native apps to execute PowerShell passing in the script via STDIN unfortunately this was broken due to other changes it the console host.</span></span>

https://windowsserver.uservoice.com/forums/301869-powershell/suggestions/15854689-powershell-exe-command-is-broken-on-windows-10

### <a name="powershellexe-creates-spike-in-cpu-usage-on-startup"></a><span data-ttu-id="d5c17-139">PowerShell.exe megnövekedett processzorhasználat az indítási hoz létre</span><span class="sxs-lookup"><span data-stu-id="d5c17-139">powershell.exe creates spike in CPU usage on startup</span></span>

<span data-ttu-id="d5c17-140">PowerShell egy WMI-lekérdezést használja annak ellenőrzéséhez, hogy a késleltetést okoz a bejelentkezési elkerülése érdekében a csoportházirend segítségével lett elindítva.</span><span class="sxs-lookup"><span data-stu-id="d5c17-140">PowerShell uses a WMI query to check if it was started via Group Policy to avoid causing delay in login.</span></span>
<span data-ttu-id="d5c17-141">A WMI-lekérdezést is említi tzres.mui.dll injektálásra összes folyamat, a rendszer, mivel a WMI Win32_Process osztály próbál lekérni a helyi időzóna adatait.</span><span class="sxs-lookup"><span data-stu-id="d5c17-141">The WMI query ends up injecting tzres.mui.dll into every process on the system since the WMI Win32_Process class attempts to retrieve local timezone information.</span></span>
<span data-ttu-id="d5c17-142">Ennek eredményeképpen a nagy CPU megnövekedett wmiprvse (a WMI szolgáltató gazda).</span><span class="sxs-lookup"><span data-stu-id="d5c17-142">This results in a large CPU spike in wmiprvse (the WMI provider host).</span></span>
<span data-ttu-id="d5c17-143">Javítsa ki, hogy ugyanazokat az információkat a WMI használata helyett Win32 API-hívás használatával.</span><span class="sxs-lookup"><span data-stu-id="d5c17-143">Fix is to use Win32 API calls to get the same information instead of using WMI.</span></span>
