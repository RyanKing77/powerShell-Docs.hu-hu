---
title: Egy PowerShell-szkript-modul írása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ed7645ea-5e52-4a45-81a7-aa3c2d605cde
caps.latest.revision: 16
ms.openlocfilehash: e8b7151538235cdf7183b78aa8df7e596d6bcfd9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848915"
---
# <a name="how-to-write-a-powershell-script-module"></a><span data-ttu-id="b5445-102">PowerShell-szkriptmodul írása</span><span class="sxs-lookup"><span data-stu-id="b5445-102">How to Write a PowerShell Script Module</span></span>

<span data-ttu-id="b5445-103">Egy szkriptmodulba lényegében bármilyen érvényes PowerShell-példaszkript egy .psm1 bővítmény mentve.</span><span class="sxs-lookup"><span data-stu-id="b5445-103">A script module is essentially any valid PowerShell script saved in a .psm1 extension.</span></span> <span data-ttu-id="b5445-104">Ez a bővítmény lehetővé teszi, hogy a PowerShell motor szabályok és a parancsmagok használatához a fájlon.</span><span class="sxs-lookup"><span data-stu-id="b5445-104">This extension allows the PowerShell engine to use a number of rules and cmdlets on your file.</span></span> <span data-ttu-id="b5445-105">Ezek a képességek a legtöbb-e, valamint kezelhetik a felmerülő telepítheti a más rendszereken a kód segítségével.</span><span class="sxs-lookup"><span data-stu-id="b5445-105">Most of these capabilities are there to help you install your code on other systems, as well as manage scoping.</span></span> <span data-ttu-id="b5445-106">Modul jegyzékfájlt, leírhatja összetettebb telepítések és megoldások, amelyek is használható.</span><span class="sxs-lookup"><span data-stu-id="b5445-106">You can also use a module manifest file, which can describe even more complex installations and solutions.</span></span>

## <a name="writing-a-powershell-script-module"></a><span data-ttu-id="b5445-107">PowerShell-szkript-modul írása</span><span class="sxs-lookup"><span data-stu-id="b5445-107">Writing a PowerShell Script Module</span></span>

<span data-ttu-id="b5445-108">Létrehozhat egy szkriptmodulba mentése folyamatban van egy érvényes PowerShell-parancsprogram egy .psm1 fájlban, és ezután ezt a fájlt egy könyvtárban található, ahol PowerShell is megtalálhatják azt.</span><span class="sxs-lookup"><span data-stu-id="b5445-108">You create a script module by saving a valid PowerShell script to a .psm1 file, and then saving that file in a directory located where PowerShell can find it.</span></span> <span data-ttu-id="b5445-109">Abban a mappában is elhelyezhet a szkript futtatásához szükséges minden olyan erőforrásokat, valamint a jegyzékfájlt, amely a PowerShell a modul működését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="b5445-109">In that folder you can also place any resources you need to run your script, as well as a manifest file that describes to PowerShell how your module works.</span></span>

#### <a name="to-create-a-basic-powershell-module"></a><span data-ttu-id="b5445-110">Egy egyszerű PowerShell-modul létrehozása</span><span class="sxs-lookup"><span data-stu-id="b5445-110">To create a basic PowerShell Module</span></span>

1. <span data-ttu-id="b5445-111">Egy meglévő PowerShell-parancsprogramot, és mentse a parancsfájlt egy .psm1 kiterjesztéssel.</span><span class="sxs-lookup"><span data-stu-id="b5445-111">Take an existing PowerShell script, and save the script with a .psm1 extension.</span></span>

   <span data-ttu-id="b5445-112">A .psm1 a parancsfájl mentése bővítmény azt jelenti, hogy a modul parancsmagjai például használható [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), rajta.</span><span class="sxs-lookup"><span data-stu-id="b5445-112">Saving a script with the .psm1 extension means that you can use the module cmdlets, such as [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), on it.</span></span> <span data-ttu-id="b5445-113">Ezek a parancsmagok elsősorban, hogy könnyen importálhatja és exportálhatja a kód más felhasználó rendszerek alakzatot létezik.</span><span class="sxs-lookup"><span data-stu-id="b5445-113">These cmdlets exist primarily so that you can easily import and export your code onto other user's systems.</span></span> <span data-ttu-id="b5445-114">(A másik megoldás lenne a kód a más rendszerekkel, és a pont – forrás-ba való betöltésének aktív memória, amely nem egy különösen méretezhető megoldás.) További információ: a **modul parancsmagjai és a változók** szakasz [Windows PowerShell-modulok](./understanding-a-windows-powershell-module.md) vegye figyelembe, hogy alapértelmezés szerint a parancsfájl az összes függvényt lesz elérhető a felhasználók, akik a .psm1 importálása fájl, de a tulajdonságok nem lesz.</span><span class="sxs-lookup"><span data-stu-id="b5445-114">(The alternate solution would be to load up your code on other systems and then dot-source it into active memory, which isn't a particularly scalable solution.) For more information see the **Module Cmdlets and Variables** section in [Windows PowerShell Modules](./understanding-a-windows-powershell-module.md) Note that, by default, all functions in your script will be accessible to users who import your .psm1 file, but properties will not.</span></span>

   <span data-ttu-id="b5445-115">Ez a témakör végén található PowerShell-parancsprogram, például Show-naptárban, jogosult érhető el.</span><span class="sxs-lookup"><span data-stu-id="b5445-115">An example PowerShell script, entitled Show-Calendar, is available at the end of this topic.</span></span>

   ```powershell
   function Show-Calendar {
   param(
       [DateTime] $start = [DateTime]::Today,
       [DateTime] $end = $start,
       $firstDayOfWeek,
       [int[]] $highlightDay,
       [string[]] $highlightDate = [DateTime]::Today.ToString()
       )

       #actual code for the function goes here see the end of the topic for the complete code sample
   }
   ```

2. <span data-ttu-id="b5445-116">Ha szeretne az egyes funkciók vagy a Tulajdonságok felhasználók hozzáférését, [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) a szkript végén.</span><span class="sxs-lookup"><span data-stu-id="b5445-116">If you wish to control user access to certain functions or properties, call [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) at the end of your script.</span></span>

   <span data-ttu-id="b5445-117">A lap alján példakód csak egy függvény, amely alapértelmezés szerint lenne kitéve rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="b5445-117">The example code at the bottom of the page has only one function, which by default would be exposed.</span></span> <span data-ttu-id="b5445-118">Ajánlott azonban, hogy explicit módon hívja meg, melyik funkciókat kíván elérhetővé, a következő kód leírtak szerint:</span><span class="sxs-lookup"><span data-stu-id="b5445-118">However, it is recommended that you explicitly call out which functions you wish to expose, as described in the following code:</span></span>

   ```powershell
   function Show-Calendar {
         }
   Export-ModuleMember -Function Show-Calendar
   ```

   <span data-ttu-id="b5445-119">Milyen importált egy moduljegyzék használatával is korlátozhatja.</span><span class="sxs-lookup"><span data-stu-id="b5445-119">You can also restrict what is imported using a module manifest.</span></span> <span data-ttu-id="b5445-120">További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md) és [írásával, egy PowerShell modul Manifest](./how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="b5445-120">For more information, see [Importing a PowerShell Module](./importing-a-powershell-module.md) and [How to Write a PowerShell Module Manifest](./how-to-write-a-powershell-module-manifest.md).</span></span>

3. <span data-ttu-id="b5445-121">Ha saját modult töltött kell modulok, használhatja őket hívásával `Import-Module`, saját modult tetején.</span><span class="sxs-lookup"><span data-stu-id="b5445-121">If you have modules that your own module needs to have loaded, you can use them with a call to `Import-Module`, at the top of your own module.</span></span>

   <span data-ttu-id="b5445-122">`Import-Module` van olyan parancsmagot, amely importálja a megcélzott modult egy rendszerre.</span><span class="sxs-lookup"><span data-stu-id="b5445-122">`Import-Module` is a cmdlet that imports a targeted module onto a system.</span></span> <span data-ttu-id="b5445-123">Emiatt a is szolgál az eljárás későbbi időpontban, valamint a saját moduljának telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="b5445-123">As such, it is also used at a later point in the procedure to install your own module as well.</span></span> <span data-ttu-id="b5445-124">Ez az oldal alján található mintakód nem használ importálás modulokat.</span><span class="sxs-lookup"><span data-stu-id="b5445-124">The sample code at the bottom of this page does not use any import modules.</span></span> <span data-ttu-id="b5445-125">Zavartalanul azonban, ha azok lesz feltüntetve a fájl elején a következő kód leírtak szerint:</span><span class="sxs-lookup"><span data-stu-id="b5445-125">If it did, however, they would be listed at the top of the file, as described in the following code:</span></span>

   ```powershell
   Import-Module GenericModule
   ```

4. <span data-ttu-id="b5445-126">Ha azt szeretné, a modul PowerShell súgójában leírására, megteheti a standard szintű súgó megjegyzéseket, a fájl, vagy egy további súgófájl.</span><span class="sxs-lookup"><span data-stu-id="b5445-126">If you want to describe your module to the PowerShell Help system, you can do so either with the standard help comments inside the file, or with an additional Help file.</span></span>

   <span data-ttu-id="b5445-127">A kódminta található, ez a témakör alján a megjegyzéseket a súgó információit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b5445-127">The code sample at the bottom of this topic includes the help information in the comments.</span></span> <span data-ttu-id="b5445-128">Ha úgy dönt, a bővített, további segítségért tartalmat tartalmazó XML-fájlok is létrehozható.</span><span class="sxs-lookup"><span data-stu-id="b5445-128">If you so choose, you could also write expanded XML files that contain additional help content.</span></span> <span data-ttu-id="b5445-129">További információkért lásd: [írása érdekében a Windows PowerShell-modulok](./writing-help-for-windows-powershell-modules.md).</span><span class="sxs-lookup"><span data-stu-id="b5445-129">For more information, see [Writing Help for Windows PowerShell Modules](./writing-help-for-windows-powershell-modules.md).</span></span>

5. <span data-ttu-id="b5445-130">Ha további modulok, XML-fájlok vagy más csomagolnia a modult kívánt tartalmat, és a egy moduljegyzék megteheti.</span><span class="sxs-lookup"><span data-stu-id="b5445-130">If you have additional modules, XML files, or other content you want to package up with your module, you can do so with a module manifest.</span></span>

   <span data-ttu-id="b5445-131">Egy moduljegyzék egy olyan fájl, más modulok tesznek, mappastruktúrát, versioning számok, szerzői adatok és egyéb információt nevét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b5445-131">A module manifest is a file that contains the names of other modules, directory layouts, versioning numbers, author data, and other pieces of information.</span></span> <span data-ttu-id="b5445-132">PowerShell modul jegyzékfájlt rendszerezése és üzembe helyezheti megoldását használja.</span><span class="sxs-lookup"><span data-stu-id="b5445-132">PowerShell uses the module manifest file to organize and deploy your solution.</span></span> <span data-ttu-id="b5445-133">Azonban ez a példa viszonylag egyszerű jellege miatt Alkalmazásjegyzék-fájl nem volt szükség.</span><span class="sxs-lookup"><span data-stu-id="b5445-133">However, due to the relatively simple nature of this example, a manifest file was not needed.</span></span> <span data-ttu-id="b5445-134">További információkért lásd: [modul jegyzékfájlok](./how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="b5445-134">For more information, see [Module Manifests](./how-to-write-a-powershell-module-manifest.md).</span></span>

6. <span data-ttu-id="b5445-135">Telepítése és futtatása a modul, a modul mentse a megfelelő PowerShell-elérési utak közül, és meghívásához `Import-Module`.</span><span class="sxs-lookup"><span data-stu-id="b5445-135">To install and run your module, save the module to one of the appropriate PowerShell paths, and make a call to `Import-Module`.</span></span>

   <span data-ttu-id="b5445-136">Az elérési utak, ahol telepítheti a modul találhatók a `$env:PSModulePath` globális változó.</span><span class="sxs-lookup"><span data-stu-id="b5445-136">The paths where you can install your module are located in the `$env:PSModulePath` global variable.</span></span> <span data-ttu-id="b5445-137">Például egy gyakori útvonalat, ahová a modul a rendszer lenne `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`.</span><span class="sxs-lookup"><span data-stu-id="b5445-137">For example, a common path to save a module on a system would be `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`.</span></span> <span data-ttu-id="b5445-138">Győződjön meg arról, a modul létezik, egy olyan mappa létrehozásához, akkor is, ha csak egy egyetlen .psm1 fájlban.</span><span class="sxs-lookup"><span data-stu-id="b5445-138">Be sure to create a folder for your module to exist in, even if it is only a single .psm1 file.</span></span> <span data-ttu-id="b5445-139">Ha a modul nem mentette az elérési utak egyik, kellene adja át a hívást a modul helye `Import-Module`.</span><span class="sxs-lookup"><span data-stu-id="b5445-139">If you did not save your module to one of these paths, you would have to pass in the location of your module in the call to `Import-Module`.</span></span> <span data-ttu-id="b5445-140">(Ellenkező esetben PowerShell nem tudná is megkeresheti.) A PowerShell 3.0, ha bejelölte a modul a PowerShell-modul elérési utak egyik verziótól kezdődően nem explicit módon importálnia kell azt: a függvény meghívása felhasználó rendelkezik automatikusan betölti azt.</span><span class="sxs-lookup"><span data-stu-id="b5445-140">(Otherwise, PowerShell would not be able to find it.) Starting with PowerShell 3.0, if you have placed your module on one of the PowerShell module paths, you do not need to explicitly import it: simply having a user call your function will automatically load it.</span></span> <span data-ttu-id="b5445-141">A modul elérési úton további információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md) és [PSModulePath környezeti változó](./modifying-the-psmodulepath-installation-path.md).</span><span class="sxs-lookup"><span data-stu-id="b5445-141">For more information on the module path, see [Importing a PowerShell Module](./importing-a-powershell-module.md) and [PSModulePath Environment Variable](./modifying-the-psmodulepath-installation-path.md).</span></span>

7. <span data-ttu-id="b5445-142">Aktív szolgáltatás modul eltávolításához meghívásához [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).</span><span class="sxs-lookup"><span data-stu-id="b5445-142">To remove a module from active service, make a call to [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).</span></span>

<span data-ttu-id="b5445-143">Vegye figyelembe, hogy [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) eltávolítja a modult az aktív memória - nem ténylegesen törli azt, ahová mentette a modul fájlokat.</span><span class="sxs-lookup"><span data-stu-id="b5445-143">Note that [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) removes your module from active memory - it does not actually delete it from where you saved the module files.</span></span>

### <a name="show-calendar-code-example"></a><span data-ttu-id="b5445-144">Példakód show-naptár</span><span class="sxs-lookup"><span data-stu-id="b5445-144">Show-Calendar code example</span></span>

<span data-ttu-id="b5445-145">Az alábbi példában egy egyszerű szkript modul, amely tartalmaz egy adott függvény Show-naptár nevű.</span><span class="sxs-lookup"><span data-stu-id="b5445-145">The following example is a simple script module that contains a single function named Show-Calendar.</span></span> <span data-ttu-id="b5445-146">Ez a funkció egy adott naptári vizuálisan jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="b5445-146">This function displays a visual representation of a calendar.</span></span> <span data-ttu-id="b5445-147">Emellett a minta tartalmaz a szinopszist, a leírás, a paraméterértékek és a példa a PowerShell súgója karakterláncok.</span><span class="sxs-lookup"><span data-stu-id="b5445-147">In addition, the sample contains the PowerShell Help strings for the synopsis, description, parameter values, and example.</span></span> <span data-ttu-id="b5445-148">Vegye figyelembe, hogy az utolsó kódsort azt jelzi, hogy a modul tagként a Show-Calendar függvénynek lesznek exportálva, a modul importálása.</span><span class="sxs-lookup"><span data-stu-id="b5445-148">Note that the last line of code indicates that the Show-Calendar function will be exported as a module member when the module is imported.</span></span>

```powershell
<#
 .Synopsis
  Displays a visual representation of a calendar.

 .Description
  Displays a visual representation of a calendar. This function supports multiple months
  and lets you highlight specific date ranges or days.

 .Parameter Start
  The first month to display.

 .Parameter End
  The last month to display.

 .Parameter FirstDayOfWeek
  The day of the month on which the week begins.

 .Parameter HighlightDay
  Specific days (numbered) to highlight. Used for date ranges like (25..31).
  Date ranges are specified by the Windows PowerShell range syntax. These dates are
  enclosed in square brackets.

 .Parameter HighlightDate
  Specific days (named) to highlight. These dates are surrounded by asterisks.

 .Example
   # Show a default display of this month.
   Show-Calendar

 .Example
   # Display a date range.
   Show-Calendar -Start "March, 2010" -End "May, 2010"

 .Example
   # Highlight a range of days.
   Show-Calendar -HighlightDay (1..10 + 22) -HighlightDate "December 25, 2008"
#>
function Show-Calendar {
param(
    [DateTime] $start = [DateTime]::Today,
    [DateTime] $end = $start,
    $firstDayOfWeek,
    [int[]] $highlightDay,
    [string[]] $highlightDate = [DateTime]::Today.ToString()
    )

## Determine the first day of the start and end months.
$start = New-Object DateTime $start.Year,$start.Month,1
$end = New-Object DateTime $end.Year,$end.Month,1

## Convert the highlighted dates into real dates.
[DateTime[]] $highlightDate = [DateTime[]] $highlightDate

## Retrieve the DateTimeFormat information so that the
## calendar can be manipulated.
$dateTimeFormat  = (Get-Culture).DateTimeFormat
if($firstDayOfWeek)
{
    $dateTimeFormat.FirstDayOfWeek = $firstDayOfWeek
}

$currentDay = $start

## Process the requested months.
while($start -le $end)
{
    ## Return to an earlier point in the function if the first day of the month
    ## is in the middle of the week.
    while($currentDay.DayOfWeek -ne $dateTimeFormat.FirstDayOfWeek)
    {
        $currentDay = $currentDay.AddDays(-1)
    }

    ## Prepare to store information about this date range.
    $currentWeek = New-Object PsObject
    $dayNames = @()
    $weeks = @()

    ## Continue processing dates until the function reaches the end of the month.
    ## The function continues until the week is completed with
    ## days from the next month.
    while(($currentDay -lt $start.AddMonths(1)) -or
        ($currentDay.DayOfWeek -ne $dateTimeFormat.FirstDayOfWeek))
    {
        ## Determine the day names to use to label the columns.
        $dayName = "{0:ddd}" -f $currentDay
        if($dayNames -notcontains $dayName)
        {
            $dayNames += $dayName
        }

        ## Pad the day number for display, highlighting if necessary.
        $displayDay = " {0,2} " -f $currentDay.Day

        ## Determine whether to highlight a specific date.
        if($highlightDate)
        {
            $compareDate = New-Object DateTime $currentDay.Year,
                $currentDay.Month,$currentDay.Day
            if($highlightDate -contains $compareDate)
            {
                $displayDay = "*" + ("{0,2}" -f $currentDay.Day) + "*"
            }
        }

        ## Otherwise, highlight as part of a date range.
        if($highlightDay -and ($highlightDay[0] -eq $currentDay.Day))
        {
            $displayDay = "[" + ("{0,2}" -f $currentDay.Day) + "]"
            $null,$highlightDay = $highlightDay
        }

        ## Add the day of the week and the day of the month as note properties.
        $currentWeek | Add-Member NoteProperty $dayName $displayDay

        ## Move to the next day of the month.
        $currentDay = $currentDay.AddDays(1)

        ## If the function reaches the next week, store the current week
        ## in the week list and continue.
        if($currentDay.DayOfWeek -eq $dateTimeFormat.FirstDayOfWeek)
        {
            $weeks += $currentWeek
            $currentWeek = New-Object PsObject
        }
    }

    ## Format the weeks as a table.
    $calendar = $weeks | Format-Table $dayNames -AutoSize | Out-String

    ## Add a centered header.
    $width = ($calendar.Split("'n") | Measure-Object -Maximum Length).Maximum
    $header = "{0:MMMM yyyy}" -f $start
    $padding = " " * (($width - $header.Length) / 2)
    $displayCalendar = " 'n" + $padding + $header + "'n " + $calendar
    $displayCalendar.TrimEnd()

    ## Move to the next month.
    $start = $start.AddMonths(1)

}
}
Export-ModuleMember -Function Show-Calendar
```
