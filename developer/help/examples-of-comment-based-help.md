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
# <a name="examples-of-comment-based-help"></a><span data-ttu-id="d0520-102">Megjegyzésalapú súgótémakörök példái</span><span class="sxs-lookup"><span data-stu-id="d0520-102">Examples of Comment-Based Help</span></span>

<span data-ttu-id="d0520-103">Ez a témakör tartalmaz, amelyek bemutatják, hogyan használható a Megjegyzés-alapú súgó a parancsfájlokban és függvényekben példa.</span><span class="sxs-lookup"><span data-stu-id="d0520-103">This topic includes example that demonstrate how to use comment-based help for scripts and functions.</span></span>

## <a name="example-1-comment-based-help-for-a-function"></a><span data-ttu-id="d0520-104">1. példa: Megjegyzés-alapú súgó-függvény</span><span class="sxs-lookup"><span data-stu-id="d0520-104">Example 1: Comment-Based Help for a Function</span></span>

 <span data-ttu-id="d0520-105">A következő minta függvény Megjegyzés-alapú súgó tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="d0520-105">The following sample function includes comment-based Help.</span></span>

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

<span data-ttu-id="d0520-106">A következő kimenet egy Get-Help parancsot, amely megjeleníti a súgót az Add-bővítmény függvény eredményeit jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="d0520-106">The following output shows the results of a Get-Help command that displays the help for the Add-Extension function.</span></span>

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

## <a name="example-2-comment-based-help-for-a-script"></a><span data-ttu-id="d0520-107">2. példa: Parancsfájl Megjegyzés-alapú súgó</span><span class="sxs-lookup"><span data-stu-id="d0520-107">Example 2: Comment-Based Help for a Script</span></span>

<span data-ttu-id="d0520-108">A következő minta függvény Megjegyzés-alapú súgó tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="d0520-108">The following sample function includes comment-based Help.</span></span>

<span data-ttu-id="d0520-109">Figyelje meg, hogy az üres sorok közötti a záró **#>** és a `Param` utasítást.</span><span class="sxs-lookup"><span data-stu-id="d0520-109">Notice the blank lines between the closing **#>** and the `Param` statement.</span></span> <span data-ttu-id="d0520-110">Egy szkript, amely nem rendelkezik egy `Param` utasítással, legalább két üres sorok között lehet a végső Megjegyzés súgótémakör és az első függvény deklarációjában.</span><span class="sxs-lookup"><span data-stu-id="d0520-110">In a script that does not have a `Param` statement, there must be at least two blank lines between the final comment in the Help topic and the first function declaration.</span></span> <span data-ttu-id="d0520-111">Ezek üres sorok nélkül Get-Help társítja a Súgó-témakör a függvény helyett a parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="d0520-111">Without these blank lines, Get-Help associates the Help topic with the function, instead of the script.</span></span>

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

<span data-ttu-id="d0520-112">A következő parancsot a szkript súgó beolvasása.</span><span class="sxs-lookup"><span data-stu-id="d0520-112">The following command gets the script Help.</span></span> <span data-ttu-id="d0520-113">Mivel a szkript nem n egy könyvtárat, amely szerepel a Path környezeti változóhoz a Get-Help parancsot, amely lekérdezi a parancsfájl súgó a parancsfájl elérési útján kell megadnia.</span><span class="sxs-lookup"><span data-stu-id="d0520-113">Because the script is not n a directory that is listed in the Path environment variable, the Get-Help command that gets the script Help must specify the script path.</span></span>

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

## <a name="example-3-parameter-descriptions-in-a-param-statement"></a><span data-ttu-id="d0520-114">3. példa: A Param utasításban paraméter leírása</span><span class="sxs-lookup"><span data-stu-id="d0520-114">Example 3: Parameter Descriptions in a Param Statement</span></span>

<span data-ttu-id="d0520-115">Ebben a példában a parameterdescriptions beszúrása megjelenítése a `Param` egy függvény vagy parancsfájl-utasítás.</span><span class="sxs-lookup"><span data-stu-id="d0520-115">This example show how to insert parameterdescriptions in the `Param` statement of a function or script.</span></span> <span data-ttu-id="d0520-116">Ebben a formátumban akkor a leghasznosabb, ha a paraméterek leírásait rövid.</span><span class="sxs-lookup"><span data-stu-id="d0520-116">This format is most useful when the parameter descriptions are brief.</span></span>

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

<span data-ttu-id="d0520-117">Az eredmények ugyanazok, mint az eredményeket, például 1.</span><span class="sxs-lookup"><span data-stu-id="d0520-117">The results are the same as the results for Example 1.</span></span> <span data-ttu-id="d0520-118">Get-Help értelmezi a paraméterek leírásait, mintha azok kísérte az `.Parameter` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="d0520-118">Get-Help interprets the parameter descriptions as though they were accompanied by the `.Parameter` keyword.</span></span>

## <a name="example-4--redirecting-to-an-xml-file"></a><span data-ttu-id="d0520-119">4. példa:  XML-fájl átirányítása</span><span class="sxs-lookup"><span data-stu-id="d0520-119">Example 4:  Redirecting to an XML File</span></span>

<span data-ttu-id="d0520-120">XML-alapú súgó-témaköröket függvények és parancsfájlok írhat.</span><span class="sxs-lookup"><span data-stu-id="d0520-120">You can write XML-based Help topics for functions and scripts.</span></span> <span data-ttu-id="d0520-121">Bár a Megjegyzés-alapú súgó jóval egyszerűbb implementálni, XML-alapú súgó megadása kötelező Ha azt szeretné, hogy még pontosabban szabályozhatja a Súgó tartalma, vagy ha fordítása Súgó-témaköröket több nyelvre. Az alábbi példa bemutatja az első néhány sorának a frissítés-Month.ps1 parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="d0520-121">Although comment-based Help is easier to implement, XML-based Help is required if you want more precise control over Help content or if you are translating Help topics into multiple languages.The following example shows the first few lines of the Update-Month.ps1 script.</span></span> <span data-ttu-id="d0520-122">A szkript a `.ExternalHelp` kulcsszó használatával adjon meg egy XML-alapú súgó-témakört a parancsfájl elérési útját.</span><span class="sxs-lookup"><span data-stu-id="d0520-122">The script uses the `.ExternalHelp` keyword to specify the path to an XML-based Help topic for the script.</span></span>

```powershell
#  .ExternalHelp C:\MyScripts\Update-Month-Help.xml

    param ([string]$InputPath, [string]$OutPutPath)

    function Get-Data { }
```

<span data-ttu-id="d0520-123">Az alábbi példa bemutatja a használatát a `.ExternalHelp` kulcsszót a függvényt.</span><span class="sxs-lookup"><span data-stu-id="d0520-123">The following example shows the use of the `.ExternalHelp` keyword in a function.</span></span>

```powershell
function Add-Extension
{
    param ([string] $name, [string]$extension = "txt")
    $name = $name + "." + $extension
    $name

    # .ExternalHelp C:\ps-test\Add-Extension.xml
}
```

## <a name="example-5--redirecting-to-a-different-help-topic"></a><span data-ttu-id="d0520-124">5. példa:  Egy másik súgótémakör átirányítása</span><span class="sxs-lookup"><span data-stu-id="d0520-124">Example 5:  Redirecting to a Different Help Topic</span></span>

<span data-ttu-id="d0520-125">A következő kódot a beépített kezdetétől fogva cikkből szerint `Help` függvény a Windows PowerShell-lel, amely egyszerre jelenít meg a Súgó a szöveg egy képernyőt.</span><span class="sxs-lookup"><span data-stu-id="d0520-125">The following code is an excerpt from the beginning of the built-in `Help` function in Windows PowerShell, which displays one screen of Help text at a time.</span></span> <span data-ttu-id="d0520-126">A Get-Help parancsmag tartozó súgó-témakör ismerteti a Súgó funkciót, mert a Súgó funkciót használ a `.ForwardHelpTargetName` és `.ForwardHelpCategory` átirányítja a felhasználót a Get-Help parancsmag súgó-témakörének kulcsszavakkal.</span><span class="sxs-lookup"><span data-stu-id="d0520-126">Because the Help topic for the Get-Help cmdlet describes the Help function, the Help function uses the `.ForwardHelpTargetName` and `.ForwardHelpCategory` keywords to redirect the user to the Get-Help cmdlet Help topic.</span></span>

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

<span data-ttu-id="d0520-127">A következő parancsot használja ezt a szolgáltatást.</span><span class="sxs-lookup"><span data-stu-id="d0520-127">The following command uses this feature.</span></span> <span data-ttu-id="d0520-128">Ha a felhasználó a Súgó funkciót a Get-Help parancsot, a Get-Help a Get-Help parancsmag használatához súgótémakör jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="d0520-128">When a user types a Get-Help command for the Help function, Get-Help displays the Help topic for the Get-Help cmdlet.</span></span>

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