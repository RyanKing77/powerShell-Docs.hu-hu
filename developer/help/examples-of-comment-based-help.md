---
title: Megjegyzés-alapú súgó példáit |} A Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 868194a2-17e9-4184-bc36-c04a33f26494
caps.latest.revision: 4
ms.openlocfilehash: dbccaf5b8e48a1c4d924bc0ec4ea09b25e10adf0
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848187"
---
# <a name="examples-of-comment-based-help"></a>Megjegyzésalapú súgótémakörök példái

Ez a témakör tartalmaz, amelyek bemutatják, hogyan használható a Megjegyzés-alapú súgó a parancsfájlokban és függvényekben példa.

## <a name="example-1-comment-based-help-for-a-function"></a>1. példa: Megjegyzés-alapú súgó-függvény

 A következő minta függvény Megjegyzés-alapú súgó tartalmaz.

```powershell
function Add-Extension
{
    param ([string]$Name,[string]$Extension = "txt")
    $name = $name + "." + $extension
    $name

    <#
        .SYNOPSIS
        Adds a file name extension to a supplied name.

        .DESCRIPTION
        Adds a file name extension to a supplied name.
        Takes any strings for the file name or extension.

        .PARAMETER Name
        Specifies the file name.

        .PARAMETER Extension
        Specifies the extension. "Txt" is the default.

        .INPUTS
        None. You cannot pipe objects to Add-Extension.

        .OUTPUTS
        System.String. Add-Extension returns a string with the extension or file name.

        .EXAMPLE
        C:\PS> extension -name "File"
        File.txt

        .EXAMPLE
        C:\PS> extension -name "File" -extension "doc"
        File.doc

        .EXAMPLE
        C:\PS> extension "File" "doc"
        File.doc

        .LINK
        Online version: http://www.fabrikam.com/extension.html

        .LINK
        Set-Item
    #>
}
```

A következő kimenet egy Get-Help parancsot, amely megjeleníti a súgót az Add-bővítmény függvény eredményeit jeleníti meg.

```powershell
C:\PS> get-help add-extension -full
```

```output
        NAME
            Add-Extension

        SYNOPSIS
            Adds a file name extension to a supplied name.

        SYNTAX
            Add-Extension [[-Name] <String>] [[-Extension] <String>] [<CommonParameters>]

        DESCRIPTION
            Adds a file name extension to a supplied name. Takes any strings for the file name or extension.

        PARAMETERS
           -Name
               Specifies the file name.

               Required?                    false
               Position?                    0
               Default value
               Accept pipeline input?       false
               Accept wildcard characters?

           -Extension
               Specifies the extension. "Txt" is the default.

               Required?                    false
               Position?                    1
               Default value
               Accept pipeline input?       false
               Accept wildcard characters?

            <CommonParameters>
               This cmdlet supports the common parameters: -Verbose, -Debug,
               -ErrorAction, -ErrorVariable, -WarningAction, -WarningVariable,
               -OutBuffer and -OutVariable. For more information, type
               "get-help about_commonparameters".

        INPUTS
            None. You cannot pipe objects to Add-Extension.

        OUTPUTS
            System.String. Add-Extension returns a string with the extension or file name.

            -------------------------- EXAMPLE 1 --------------------------

            C:\PS> extension -name "File"
            File.txt

            -------------------------- EXAMPLE 2 --------------------------

            C:\PS> extension -name "File" -extension "doc"
            File.doc

            -------------------------- EXAMPLE 3 --------------------------

            C:\PS> extension "File" "doc"
            File.doc

        RELATED LINKS
            Online version: http://www.fabrikam.com/extension.html
            Set-Item
```

## <a name="example-2-comment-based-help-for-a-script"></a>2. példa: Parancsfájl Megjegyzés-alapú súgó

A következő minta függvény Megjegyzés-alapú súgó tartalmaz.

Figyelje meg, hogy az üres sorok közötti a záró **#>** és a `Param` utasítást. Egy szkript, amely nem rendelkezik egy `Param` utasítással, legalább két üres sorok között lehet a végső Megjegyzés súgótémakör és az első függvény deklarációjában. Ezek üres sorok nélkül Get-Help társítja a Súgó-témakör a függvény helyett a parancsfájl.

```powershell
<#
  .SYNOPSIS
  Performs monthly data updates.

  .DESCRIPTION
  The Update-Month.ps1 script updates the registry with new data generated
  during the past month and generates a report.

  .PARAMETER InputPath
  Specifies the path to the CSV-based input file.

  .PARAMETER OutputPath
  Specifies the name and path for the CSV-based output file. By default,
  MonthlyUpdates.ps1 generates a name from the date and time it runs, and
  saves the output in the local directory.

  .INPUTS
  None. You cannot pipe objects to Update-Month.ps1.

  .OUTPUTS
  None. Update-Month.ps1 does not generate any output.

  .EXAMPLE
  C:\PS> .\Update-Month.ps1

  .EXAMPLE
  C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv

  .EXAMPLE
  C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv -outputPath C:\Reports\2009\January.csv
#>

param ([string]$InputPath, [string]$OutPutPath)

function Get-Data { }
```

A következő parancsot a szkript súgó beolvasása. Mivel a szkript nem n egy könyvtárat, amely szerepel a Path környezeti változóhoz a Get-Help parancsot, amely lekérdezi a parancsfájl súgó a parancsfájl elérési útján kell megadnia.

```powershell
C:\PS> get-help c:\ps-test\update-month.ps1 -full
```

```output
            NAME
                C:\ps-test\Update-Month.ps1

            SYNOPSIS
                Performs monthly data updates.

            SYNTAX
                C:\ps-test\Update-Month.ps1 [-InputPath] <String> [[-OutputPath]
                <String>] [<CommonParameters>]

            DESCRIPTION
                The Update-Month.ps1 script updates the registry with new data
                generated during the past month and generates a report.

            PARAMETERS
               -InputPath
                   Specifies the path to the CSV-based input file.

                   Required?                    true
                   Position?                    0
                   Default value
                   Accept pipeline input?       false
                   Accept wildcard characters?

               -OutputPath
                   Specifies the name and path for the CSV-based output file. By
                   default, MonthlyUpdates.ps1 generates a name from the date
                   and time it runs, and saves the output in the local directory.

                   Required?                    false
                   Position?                    1
                   Default value
                   Accept pipeline input?       false
                   Accept wildcard characters?

               <CommonParameters>
                   This cmdlet supports the common parameters: -Verbose, -Debug,
                   -ErrorAction, -ErrorVariable, -WarningAction, -WarningVariable,
                   -OutBuffer and -OutVariable. For more information, type,
                   "get-help about_commonparameters".

            INPUTS
                   None. You cannot pipe objects to Update-Month.ps1.

            OUTPUTS
                   None. Update-Month.ps1 does not generate any output.

            -------------------------- EXAMPLE 1 --------------------------

            C:\PS> .\Update-Month.ps1

            -------------------------- EXAMPLE 2 --------------------------

            C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv

            -------------------------- EXAMPLE 3 --------------------------

            C:\PS> .\Update-Month.ps1 -inputpath C:\Data\January.csv -outputPath
            C:\Reports\2009\January.csv

            RELATED LINKS
```

## <a name="example-3-parameter-descriptions-in-a-param-statement"></a>3. példa: A Param utasításban paraméter leírása

Ebben a példában a parameterdescriptions beszúrása megjelenítése a `Param` egy függvény vagy parancsfájl-utasítás. Ebben a formátumban akkor a leghasznosabb, ha a paraméterek leírásait rövid.

```powershell
function Add-Extension
{
    param
    (
        [string]
        # Specifies the file name.
        $name,

        [string]
        # Specifies the file name extension. "Txt" is the default.
        $extension = "txt"
    )
    $name = $name + "." + $extension
    $name

    <#
        .SYNOPSIS
        Adds a file name extension to a supplied name.
...
    #>
```

Az eredmények ugyanazok, mint az eredményeket, például 1. Get-Help értelmezi a paraméterek leírásait, mintha azok kísérte az `.Parameter` kulcsszót.

## <a name="example-4--redirecting-to-an-xml-file"></a>4. példa:  XML-fájl átirányítása

XML-alapú súgó-témaköröket függvények és parancsfájlok írhat. Bár a Megjegyzés-alapú súgó jóval egyszerűbb implementálni, XML-alapú súgó megadása kötelező Ha azt szeretné, hogy még pontosabban szabályozhatja a Súgó tartalma, vagy ha fordítása Súgó-témaköröket több nyelvre. Az alábbi példa bemutatja az első néhány sorának a frissítés-Month.ps1 parancsfájlt. A szkript a `.ExternalHelp` kulcsszó használatával adjon meg egy XML-alapú súgó-témakört a parancsfájl elérési útját.

```powershell
#  .ExternalHelp C:\MyScripts\Update-Month-Help.xml

    param ([string]$InputPath, [string]$OutPutPath)

    function Get-Data { }
```

Az alábbi példa bemutatja a használatát a `.ExternalHelp` kulcsszót a függvényt.

```powershell
function Add-Extension
{
    param ([string] $name, [string]$extension = "txt")
    $name = $name + "." + $extension
    $name

    # .ExternalHelp C:\ps-test\Add-Extension.xml
}
```

## <a name="example-5--redirecting-to-a-different-help-topic"></a>5. példa:  Egy másik súgótémakör átirányítása

A következő kódot a beépített kezdetétől fogva cikkből szerint `Help` függvény a Windows PowerShell-lel, amely egyszerre jelenít meg a Súgó a szöveg egy képernyőt. A Get-Help parancsmag tartozó súgó-témakör ismerteti a Súgó funkciót, mert a Súgó funkciót használ a `.ForwardHelpTargetName` és `.ForwardHelpCategory` átirányítja a felhasználót a Get-Help parancsmag súgó-témakörének kulcsszavakkal.

```powershell
function help
{

    <#
      .FORWARDHELPTARGETNAME Get-Help
      .FORWARDHELPCATEGORY Cmdlet
    #>
    [CmdletBinding(DefaultParameterSetName='AllUsersView')]
    param(
            [Parameter(Position=0, ValueFromPipelineByPropertyName=$true)]
            [System.String]
            ${Name},
    ...
```

A következő parancsot használja ezt a szolgáltatást. Ha a felhasználó a Súgó funkciót a Get-Help parancsot, a Get-Help a Get-Help parancsmag használatához súgótémakör jeleníti meg.

```powershell
C:\PS> get-help help
```

```output
            NAME
                Get-Help

            SYNOPSIS
                Displays information about Windows PowerShell cmdlets and concepts.
            ...
```