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
ms.openlocfilehash: b2a929a1724f77f0516ad24cfd90f6d6053ed19e
ms.sourcegitcommit: bc42c9166857147a1ecf9924b718d4a48eb901e3
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/03/2019
ms.locfileid: "66470798"
---
# <a name="how-to-write-a-powershell-script-module"></a><span data-ttu-id="09a32-102">PowerShell-szkriptmodul írása</span><span class="sxs-lookup"><span data-stu-id="09a32-102">How to Write a PowerShell Script Module</span></span>

<span data-ttu-id="09a32-103">Egy szkriptmodulba lényegében bármilyen érvényes PowerShell-példaszkript egy .psm1 bővítmény mentve.</span><span class="sxs-lookup"><span data-stu-id="09a32-103">A script module is essentially any valid PowerShell script saved in a .psm1 extension.</span></span> <span data-ttu-id="09a32-104">Ez a bővítmény lehetővé teszi, hogy a PowerShell motor szabályok és a parancsmagok használatához a fájlon.</span><span class="sxs-lookup"><span data-stu-id="09a32-104">This extension allows the PowerShell engine to use a number of rules and cmdlets on your file.</span></span> <span data-ttu-id="09a32-105">Ezek a képességek a legtöbb-e, valamint kezelhetik a felmerülő telepítheti a más rendszereken a kód segítségével.</span><span class="sxs-lookup"><span data-stu-id="09a32-105">Most of these capabilities are there to help you install your code on other systems, as well as manage scoping.</span></span> <span data-ttu-id="09a32-106">Modul jegyzékfájlt, leírhatja összetettebb telepítések és megoldások, amelyek is használható.</span><span class="sxs-lookup"><span data-stu-id="09a32-106">You can also use a module manifest file, which can describe even more complex installations and solutions.</span></span>

## <a name="writing-a-powershell-script-module"></a><span data-ttu-id="09a32-107">PowerShell-szkript-modul írása</span><span class="sxs-lookup"><span data-stu-id="09a32-107">Writing a PowerShell Script Module</span></span>

<span data-ttu-id="09a32-108">Létrehozhat egy szkriptmodulba mentése folyamatban van egy érvényes PowerShell-parancsprogram egy .psm1 fájlban, és ezután ezt a fájlt egy könyvtárban található, ahol PowerShell is megtalálhatják azt.</span><span class="sxs-lookup"><span data-stu-id="09a32-108">You create a script module by saving a valid PowerShell script to a .psm1 file, and then saving that file in a directory located where PowerShell can find it.</span></span> <span data-ttu-id="09a32-109">Abban a mappában is elhelyezhet a szkript futtatásához szükséges minden olyan erőforrásokat, valamint a jegyzékfájlt, amely a PowerShell a modul működését ismerteti.</span><span class="sxs-lookup"><span data-stu-id="09a32-109">In that folder you can also place any resources you need to run your script, as well as a manifest file that describes to PowerShell how your module works.</span></span>

#### <a name="to-create-a-basic-powershell-module"></a><span data-ttu-id="09a32-110">Egy egyszerű PowerShell-modul létrehozása</span><span class="sxs-lookup"><span data-stu-id="09a32-110">To create a basic PowerShell Module</span></span>

1. <span data-ttu-id="09a32-111">Egy meglévő PowerShell-parancsprogramot, és mentse a parancsfájlt egy .psm1 kiterjesztéssel.</span><span class="sxs-lookup"><span data-stu-id="09a32-111">Take an existing PowerShell script, and save the script with a .psm1 extension.</span></span>

   <span data-ttu-id="09a32-112">A .psm1 a parancsfájl mentése bővítmény azt jelenti, hogy a modul parancsmagjai például használható [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), rajta.</span><span class="sxs-lookup"><span data-stu-id="09a32-112">Saving a script with the .psm1 extension means that you can use the module cmdlets, such as [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), on it.</span></span> <span data-ttu-id="09a32-113">Ezek a parancsmagok elsősorban, hogy könnyen importálhatja és exportálhatja a kód más felhasználó rendszerek alakzatot létezik.</span><span class="sxs-lookup"><span data-stu-id="09a32-113">These cmdlets exist primarily so that you can easily import and export your code onto other user's systems.</span></span> <span data-ttu-id="09a32-114">(A másik megoldás lenne a kód a más rendszerekkel, és a pont – forrás-ba való betöltésének aktív memória, amely nem egy különösen méretezhető megoldás.) További információk: a **modul parancsmagjai és a változók** szakasz [Windows PowerShell-modulok](./understanding-a-windows-powershell-module.md) vegye figyelembe, hogy, alapértelmezés szerint a parancsfájl az összes függvényt elérhető-e a felhasználók, akik a .psm1 fájl importálása de tulajdonságait nem.</span><span class="sxs-lookup"><span data-stu-id="09a32-114">(The alternate solution would be to load up your code on other systems and then dot-source it into active memory, which isn't a particularly scalable solution.) For more information see the **Module Cmdlets and Variables** section in [Windows PowerShell Modules](./understanding-a-windows-powershell-module.md) Note that, by default, all functions in your script are accessible to users who import your .psm1 file, but properties are not.</span></span>

   <span data-ttu-id="09a32-115">PowerShell-parancsprogram, például jogosult `Show-Calendar`, ez a témakör végén található érhető el.</span><span class="sxs-lookup"><span data-stu-id="09a32-115">An example PowerShell script, entitled `Show-Calendar`, is available at the end of this topic.</span></span>

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

2. <span data-ttu-id="09a32-116">A felhasználói hozzáférésének bizonyos funkciók és a tulajdonságok, hívja [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) a szkript végén.</span><span class="sxs-lookup"><span data-stu-id="09a32-116">To control user access to certain functions or properties, call [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) at the end of your script.</span></span>

   <span data-ttu-id="09a32-117">A lap alján példakód csak egy függvény, amely alapértelmezés szerint lenne kitéve rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="09a32-117">The example code at the bottom of the page has only one function, which by default would be exposed.</span></span> <span data-ttu-id="09a32-118">Ajánlott azonban, hogy explicit módon hívja meg, melyik funkciókat kíván elérhetővé, a következő kód leírtak szerint:</span><span class="sxs-lookup"><span data-stu-id="09a32-118">However, it is recommended that you explicitly call out which functions you wish to expose, as described in the following code:</span></span>

   ```powershell
   function Show-Calendar {
         }
   Export-ModuleMember -Function Show-Calendar
   ```

   <span data-ttu-id="09a32-119">Milyen importált egy moduljegyzék használatával is korlátozhatja.</span><span class="sxs-lookup"><span data-stu-id="09a32-119">You can also restrict what is imported using a module manifest.</span></span> <span data-ttu-id="09a32-120">További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md) és [írásával, egy PowerShell modul Manifest](./how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="09a32-120">For more information, see [Importing a PowerShell Module](./importing-a-powershell-module.md) and [How to Write a PowerShell Module Manifest](./how-to-write-a-powershell-module-manifest.md).</span></span>

3. <span data-ttu-id="09a32-121">Ha saját modult töltött kell modulok, használhatja őket hívásával `Import-Module`, saját modult tetején.</span><span class="sxs-lookup"><span data-stu-id="09a32-121">If you have modules that your own module needs to have loaded, you can use them with a call to `Import-Module`, at the top of your own module.</span></span>

   <span data-ttu-id="09a32-122">`Import-Module` van olyan parancsmagot, amely importálja a megcélzott modult egy rendszerre.</span><span class="sxs-lookup"><span data-stu-id="09a32-122">`Import-Module` is a cmdlet that imports a targeted module onto a system.</span></span> <span data-ttu-id="09a32-123">Emiatt a is szolgál az eljárás későbbi időpontban, valamint a saját moduljának telepítéséhez.</span><span class="sxs-lookup"><span data-stu-id="09a32-123">As such, it is also used at a later point in the procedure to install your own module as well.</span></span> <span data-ttu-id="09a32-124">Ez az oldal alján található mintakód nem használ importálás modulokat.</span><span class="sxs-lookup"><span data-stu-id="09a32-124">The sample code at the bottom of this page does not use any import modules.</span></span> <span data-ttu-id="09a32-125">Zavartalanul azonban, ha azok lesz feltüntetve a fájl elején a következő kód leírtak szerint:</span><span class="sxs-lookup"><span data-stu-id="09a32-125">If it did, however, they would be listed at the top of the file, as described in the following code:</span></span>

   ```powershell
   Import-Module GenericModule
   ```

4. <span data-ttu-id="09a32-126">A modul PowerShell súgójában leírására, is szabványos súgó megjegyzések használata a fájl, vagy hozzon létre egy további segítséget fájlt.</span><span class="sxs-lookup"><span data-stu-id="09a32-126">To describe your module to the PowerShell Help system, you can either use standard help comments inside the file, or create an additional Help file.</span></span>

   <span data-ttu-id="09a32-127">A kódminta található, ez a témakör alján a megjegyzéseket a súgó információit tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="09a32-127">The code sample at the bottom of this topic includes the help information in the comments.</span></span> <span data-ttu-id="09a32-128">Bővített, további segítségért tartalmat tartalmazó XML-fájlok is is írható.</span><span class="sxs-lookup"><span data-stu-id="09a32-128">You could also write expanded XML files that contain additional help content.</span></span> <span data-ttu-id="09a32-129">További információkért lásd: [írása érdekében a Windows PowerShell-modulok](./writing-help-for-windows-powershell-modules.md).</span><span class="sxs-lookup"><span data-stu-id="09a32-129">For more information, see [Writing Help for Windows PowerShell Modules](./writing-help-for-windows-powershell-modules.md).</span></span>

5. <span data-ttu-id="09a32-130">Ha további modulok, XML-fájlok vagy más csomagolnia a modult kívánt tartalmat, és a egy moduljegyzék megteheti.</span><span class="sxs-lookup"><span data-stu-id="09a32-130">If you have additional modules, XML files, or other content you want to package up with your module, you can do so with a module manifest.</span></span>

   <span data-ttu-id="09a32-131">Egy moduljegyzék egy olyan fájl, más modulok tesznek, mappastruktúrát, versioning számok, szerzői adatok és egyéb információt nevét tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="09a32-131">A module manifest is a file that contains the names of other modules, directory layouts, versioning numbers, author data, and other pieces of information.</span></span> <span data-ttu-id="09a32-132">PowerShell modul jegyzékfájlt rendszerezése és üzembe helyezheti megoldását használja.</span><span class="sxs-lookup"><span data-stu-id="09a32-132">PowerShell uses the module manifest file to organize and deploy your solution.</span></span> <span data-ttu-id="09a32-133">Azonban ez a példa viszonylag egyszerű jellege miatt Alkalmazásjegyzék-fájl nem volt szükség.</span><span class="sxs-lookup"><span data-stu-id="09a32-133">However, due to the relatively simple nature of this example, a manifest file was not needed.</span></span> <span data-ttu-id="09a32-134">További információkért lásd: [modul jegyzékfájlok](./how-to-write-a-powershell-module-manifest.md).</span><span class="sxs-lookup"><span data-stu-id="09a32-134">For more information, see [Module Manifests](./how-to-write-a-powershell-module-manifest.md).</span></span>

6. <span data-ttu-id="09a32-135">Telepítése és futtatása a modul, a modul mentse a megfelelő PowerShell-elérési utak közül, és meghívásához `Import-Module`.</span><span class="sxs-lookup"><span data-stu-id="09a32-135">To install and run your module, save the module to one of the appropriate PowerShell paths, and make a call to `Import-Module`.</span></span>

   <span data-ttu-id="09a32-136">Az elérési utak, ahol telepítheti a modul találhatók a `$env:PSModulePath` globális változó.</span><span class="sxs-lookup"><span data-stu-id="09a32-136">The paths where you can install your module are located in the `$env:PSModulePath` global variable.</span></span> <span data-ttu-id="09a32-137">Például egy gyakori útvonalat, ahová a modul a rendszer lenne `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`.</span><span class="sxs-lookup"><span data-stu-id="09a32-137">For example, a common path to save a module on a system would be `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`.</span></span> <span data-ttu-id="09a32-138">Győződjön meg arról, a modul létezik, egy olyan mappa létrehozásához, akkor is, ha csak egy egyetlen .psm1 fájlban.</span><span class="sxs-lookup"><span data-stu-id="09a32-138">Be sure to create a folder for your module to exist in, even if it is only a single .psm1 file.</span></span> <span data-ttu-id="09a32-139">Ha a modul nem mentette az elérési utak egyik, kellene adja át a hívást a modul helye `Import-Module`.</span><span class="sxs-lookup"><span data-stu-id="09a32-139">If you did not save your module to one of these paths, you would have to pass in the location of your module in the call to `Import-Module`.</span></span> <span data-ttu-id="09a32-140">(Ellenkező esetben PowerShell nem tudná is megkeresheti.) PowerShell 3.0-s verziójával kezdődően, ha bejelölte a modul PowerShell modul elérési utak egyik, nem kell explicit módon importálásához.</span><span class="sxs-lookup"><span data-stu-id="09a32-140">(Otherwise, PowerShell would not be able to find it.) Starting with PowerShell 3.0, if you have placed your module in one of the PowerShell module paths, you do not need to explicitly import it.</span></span> <span data-ttu-id="09a32-141">Amikor egy felhasználó meghívja a függvényt, a modul automatikusan betöltődik.</span><span class="sxs-lookup"><span data-stu-id="09a32-141">You module is automatically loaded when a user calls your function.</span></span>
   <span data-ttu-id="09a32-142">A modul elérési úton további információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md) és [PSModulePath környezeti változó](./modifying-the-psmodulepath-installation-path.md).</span><span class="sxs-lookup"><span data-stu-id="09a32-142">For more information on the module path, see [Importing a PowerShell Module](./importing-a-powershell-module.md) and [PSModulePath Environment Variable](./modifying-the-psmodulepath-installation-path.md).</span></span>

7. <span data-ttu-id="09a32-143">Aktív szolgáltatás modul eltávolításához meghívásához [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).</span><span class="sxs-lookup"><span data-stu-id="09a32-143">To remove a module from active service, make a call to [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).</span></span>

   <span data-ttu-id="09a32-144">Vegye figyelembe, hogy [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) eltávolítja a modult az aktív memória - nem ténylegesen törli azt, ahová mentette a modul fájlokat.</span><span class="sxs-lookup"><span data-stu-id="09a32-144">Note that [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) removes your module from active memory - it does not actually delete it from where you saved the module files.</span></span>

### <a name="show-calendar-code-example"></a><span data-ttu-id="09a32-145">Példakód show-naptár</span><span class="sxs-lookup"><span data-stu-id="09a32-145">Show-Calendar code example</span></span>

<span data-ttu-id="09a32-146">Az alábbi példában egy egyszerű szkript modul, amely tartalmaz egy adott függvény nevű `Show-Calendar`.</span><span class="sxs-lookup"><span data-stu-id="09a32-146">The following example is a simple script module that contains a single function named `Show-Calendar`.</span></span>
<span data-ttu-id="09a32-147">Ez a funkció egy adott naptári vizuálisan jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="09a32-147">This function displays a visual representation of a calendar.</span></span> <span data-ttu-id="09a32-148">Emellett a minta tartalmaz a szinopszist, a leírás, a paraméterértékek és a példa a PowerShell súgója karakterláncok.</span><span class="sxs-lookup"><span data-stu-id="09a32-148">In addition, the sample contains the PowerShell Help strings for the synopsis, description, parameter values, and example.</span></span> <span data-ttu-id="09a32-149">Vegye figyelembe, hogy az utolsó kódsort biztosítja, hogy a `Show-Calendar` függvény modul tagjaként van exportálva, a modul importálása.</span><span class="sxs-lookup"><span data-stu-id="09a32-149">Note that the last line of code ensures that the `Show-Calendar` function is exported as a module member when the module is imported.</span></span>

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
    $width = ($calendar.Split("`n") | Measure-Object -Maximum Length).Maximum
    $header = "{0:MMMM yyyy}" -f $start
    $padding = " " * (($width - $header.Length) / 2)
    $displayCalendar = " `n" + $padding + $header + "`n " + $calendar
    $displayCalendar.TrimEnd()

    ## Move to the next month.
    $start = $start.AddMonths(1)

}
}
Export-ModuleMember -Function Show-Calendar
```
