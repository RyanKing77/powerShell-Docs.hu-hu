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
# <a name="how-to-write-a-powershell-script-module"></a>PowerShell-szkriptmodul írása

Egy szkriptmodulba lényegében bármilyen érvényes PowerShell-példaszkript egy .psm1 bővítmény mentve. Ez a bővítmény lehetővé teszi, hogy a PowerShell motor szabályok és a parancsmagok használatához a fájlon. Ezek a képességek a legtöbb-e, valamint kezelhetik a felmerülő telepítheti a más rendszereken a kód segítségével. Modul jegyzékfájlt, leírhatja összetettebb telepítések és megoldások, amelyek is használható.

## <a name="writing-a-powershell-script-module"></a>PowerShell-szkript-modul írása

Létrehozhat egy szkriptmodulba mentése folyamatban van egy érvényes PowerShell-parancsprogram egy .psm1 fájlban, és ezután ezt a fájlt egy könyvtárban található, ahol PowerShell is megtalálhatják azt. Abban a mappában is elhelyezhet a szkript futtatásához szükséges minden olyan erőforrásokat, valamint a jegyzékfájlt, amely a PowerShell a modul működését ismerteti.

#### <a name="to-create-a-basic-powershell-module"></a>Egy egyszerű PowerShell-modul létrehozása

1. Egy meglévő PowerShell-parancsprogramot, és mentse a parancsfájlt egy .psm1 kiterjesztéssel.

   A .psm1 a parancsfájl mentése bővítmény azt jelenti, hogy a modul parancsmagjai például használható [Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module), rajta. Ezek a parancsmagok elsősorban, hogy könnyen importálhatja és exportálhatja a kód más felhasználó rendszerek alakzatot létezik. (A másik megoldás lenne a kód a más rendszerekkel, és a pont – forrás-ba való betöltésének aktív memória, amely nem egy különösen méretezhető megoldás.) További információk: a **modul parancsmagjai és a változók** szakasz [Windows PowerShell-modulok](./understanding-a-windows-powershell-module.md) vegye figyelembe, hogy, alapértelmezés szerint a parancsfájl az összes függvényt elérhető-e a felhasználók, akik a .psm1 fájl importálása de tulajdonságait nem.

   PowerShell-parancsprogram, például jogosult `Show-Calendar`, ez a témakör végén található érhető el.

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

2. A felhasználói hozzáférésének bizonyos funkciók és a tulajdonságok, hívja [Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) a szkript végén.

   A lap alján példakód csak egy függvény, amely alapértelmezés szerint lenne kitéve rendelkezik. Ajánlott azonban, hogy explicit módon hívja meg, melyik funkciókat kíván elérhetővé, a következő kód leírtak szerint:

   ```powershell
   function Show-Calendar {
         }
   Export-ModuleMember -Function Show-Calendar
   ```

   Milyen importált egy moduljegyzék használatával is korlátozhatja. További információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md) és [írásával, egy PowerShell modul Manifest](./how-to-write-a-powershell-module-manifest.md).

3. Ha saját modult töltött kell modulok, használhatja őket hívásával `Import-Module`, saját modult tetején.

   `Import-Module` van olyan parancsmagot, amely importálja a megcélzott modult egy rendszerre. Emiatt a is szolgál az eljárás későbbi időpontban, valamint a saját moduljának telepítéséhez. Ez az oldal alján található mintakód nem használ importálás modulokat. Zavartalanul azonban, ha azok lesz feltüntetve a fájl elején a következő kód leírtak szerint:

   ```powershell
   Import-Module GenericModule
   ```

4. A modul PowerShell súgójában leírására, is szabványos súgó megjegyzések használata a fájl, vagy hozzon létre egy további segítséget fájlt.

   A kódminta található, ez a témakör alján a megjegyzéseket a súgó információit tartalmazza. Bővített, további segítségért tartalmat tartalmazó XML-fájlok is is írható. További információkért lásd: [írása érdekében a Windows PowerShell-modulok](./writing-help-for-windows-powershell-modules.md).

5. Ha további modulok, XML-fájlok vagy más csomagolnia a modult kívánt tartalmat, és a egy moduljegyzék megteheti.

   Egy moduljegyzék egy olyan fájl, más modulok tesznek, mappastruktúrát, versioning számok, szerzői adatok és egyéb információt nevét tartalmazza. PowerShell modul jegyzékfájlt rendszerezése és üzembe helyezheti megoldását használja. Azonban ez a példa viszonylag egyszerű jellege miatt Alkalmazásjegyzék-fájl nem volt szükség. További információkért lásd: [modul jegyzékfájlok](./how-to-write-a-powershell-module-manifest.md).

6. Telepítése és futtatása a modul, a modul mentse a megfelelő PowerShell-elérési utak közül, és meghívásához `Import-Module`.

   Az elérési utak, ahol telepítheti a modul találhatók a `$env:PSModulePath` globális változó. Például egy gyakori útvonalat, ahová a modul a rendszer lenne `%SystemRoot%/users/<user>/Documents/WindowsPowerShell/Modules/<moduleName>`. Győződjön meg arról, a modul létezik, egy olyan mappa létrehozásához, akkor is, ha csak egy egyetlen .psm1 fájlban. Ha a modul nem mentette az elérési utak egyik, kellene adja át a hívást a modul helye `Import-Module`. (Ellenkező esetben PowerShell nem tudná is megkeresheti.) PowerShell 3.0-s verziójával kezdődően, ha bejelölte a modul PowerShell modul elérési utak egyik, nem kell explicit módon importálásához. Amikor egy felhasználó meghívja a függvényt, a modul automatikusan betöltődik.
   A modul elérési úton további információkért lásd: [egy PowerShell-modul importálása](./importing-a-powershell-module.md) és [PSModulePath környezeti változó](./modifying-the-psmodulepath-installation-path.md).

7. Aktív szolgáltatás modul eltávolításához meghívásához [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module).

   Vegye figyelembe, hogy [Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) eltávolítja a modult az aktív memória - nem ténylegesen törli azt, ahová mentette a modul fájlokat.

### <a name="show-calendar-code-example"></a>Példakód show-naptár

Az alábbi példában egy egyszerű szkript modul, amely tartalmaz egy adott függvény nevű `Show-Calendar`.
Ez a funkció egy adott naptári vizuálisan jeleníti meg. Emellett a minta tartalmaz a szinopszist, a leírás, a paraméterértékek és a példa a PowerShell súgója karakterláncok. Vegye figyelembe, hogy az utolsó kódsort biztosítja, hogy a `Show-Calendar` függvény modul tagjaként van exportálva, a modul importálása.

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
