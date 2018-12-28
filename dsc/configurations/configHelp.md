---
ms.date: 12/12/2018
keywords: DSC, powershell, a konfigurációt, a beállítása
title: DSC-konfigurációk súgóinak összeállítása
ms.openlocfilehash: 498ec0f594ed3229e097903c4ea2ae34d3da03a2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404347"
---
# <a name="writing-help-for-dsc-configurations"></a><span data-ttu-id="bd038-103">DSC-konfigurációk súgóinak összeállítása</span><span class="sxs-lookup"><span data-stu-id="bd038-103">Writing help for DSC configurations</span></span>

><span data-ttu-id="bd038-104">Érvényes: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="bd038-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="bd038-105">A DSC-konfigurációk Megjegyzés-alapú súgó is használhatja.</span><span class="sxs-lookup"><span data-stu-id="bd038-105">You can use comment-based help in DSC configurations.</span></span> <span data-ttu-id="bd038-106">Felhasználók férhetnek hozzá a Súgó hívása a **konfigurációs** a `-?`, vagy a [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="bd038-106">Users can access the help by calling the **Configuration** with `-?`, or by using the [Get-Help](/powershell/module/Microsoft.PowerShell.Core/Get-Help) cmdlet.</span></span> <span data-ttu-id="bd038-107">Helyezze el a Megjegyzés-alapú súgó közvetlenül a fenti a `Configuration` kulcsszót.</span><span class="sxs-lookup"><span data-stu-id="bd038-107">Place your Comment-based help directly above the `Configuration` keyword.</span></span>
<span data-ttu-id="bd038-108">A megjegyzésblokkot, közvetlenül a paraméterdeklarációhoz vagy mindkettő az alábbi példában látható módon fölött a paraméter súgó beágyazott helyezheti.</span><span class="sxs-lookup"><span data-stu-id="bd038-108">You can place parameter help in-line with your comment block, directly above the parameter declaration, or both as in the example below.</span></span>

<span data-ttu-id="bd038-109">További információ a PowerShell Megjegyzés-alapú súgó: [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span><span class="sxs-lookup"><span data-stu-id="bd038-109">For more information about PowerShell comment-based help, see [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).</span></span>

> [!NOTE]
> <span data-ttu-id="bd038-110">PowerShell fejlesztési környezetekben, például a VSCode és az ISE-ben is kódrészletek automatikus beszúrását Megjegyzés blokk sablonok lehetővé teszi.</span><span class="sxs-lookup"><span data-stu-id="bd038-110">PowerShell development environments, like VSCode and the ISE, also have snippets to allow you to automatically insert comment block templates.</span></span>

<span data-ttu-id="bd038-111">Az alábbi példa bemutatja egy parancsfájlt, amely tartalmazza a konfigurációs és a hozzá tartozó megjegyzés-alapú súgó.</span><span class="sxs-lookup"><span data-stu-id="bd038-111">The following example shows a script that contains a configuration and comment-based help for it.</span></span> <span data-ttu-id="bd038-112">Ez a példa bemutatja egy konfigurációt a paramétereket.</span><span class="sxs-lookup"><span data-stu-id="bd038-112">This example shows a Configuration with parameters.</span></span> <span data-ttu-id="bd038-113">A konfigurációk a paraméterek használatával kapcsolatos további tudnivalókért lásd: [paraméterek hozzáadása a konfigurációk](add-parameters-to-a-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="bd038-113">To learn more about using parameters in your Configurations, see [Add Parameters to your Configurations](add-parameters-to-a-configuration.md).</span></span>

```powershell
<#
.SYNOPSIS
A brief description of the function or script. This keyword can be used only once for each configuration.


.DESCRIPTION
A detailed description of the function or script. This keyword can be used only once for each configuration.


.PARAMETER ComputerName
The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword.
Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description.
The description can include paragraph breaks.

The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters
(and their descriptions) appear in help topic. To change the order, change the syntax.

.EXAMPLE
HelpSample -ComputerName localhost

A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example.
PowerShell automatically prefaces the first line with a PowerShell prompt. Additional lines are treated as output and description. The example can contain spaces, newlines and PowerShell code.

If you have multiple examples, there is no need to number them. PowerShell will number the examples in help text.
.EXAMPLE
HelpSample -FilePath "C:\output.txt"

This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>
configuration HelpSample1
{
    param
    (
        [string]$ComputerName = 'localhost',
        # Provide a PARAMETER section for each parameter that your script or function accepts.
        [string]$FilePath = 'C:\Destination.txt'
    )

    Node $ComputerName
    {
        File HelloWorld
        {
            Contents="Hello World"
            DestinationPath = $FilePath
        }
    }
}
```

## <a name="viewing-configuration-help"></a><span data-ttu-id="bd038-114">Konfigurációs súgó megtekintése</span><span class="sxs-lookup"><span data-stu-id="bd038-114">Viewing configuration help</span></span>

<span data-ttu-id="bd038-115">Egy konfigurációs súgójának megtekintéséhez használja a `Get-Help` parancsmag és a függvény vagy a típus neve, amelyre a függvény neve követ `-?`.</span><span class="sxs-lookup"><span data-stu-id="bd038-115">To view the help for a configuration, use the `Get-Help` cmdlet with the name of the function, or type the name of the function followed by `-?`.</span></span> <span data-ttu-id="bd038-116">Az alábbiakban található a korábbi konfiguráció átadott kimenete `Get-Help`.</span><span class="sxs-lookup"><span data-stu-id="bd038-116">The following is the output of the previous Configuration passed to `Get-Help`.</span></span>

```powershell
Get-Help HelpSample1 -Detailed
```

```output
NAME
    HelpSample1

SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.


SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-PsDscRunAsCredential] <PSCredential>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName] <String>] [[-FilePath] <String>] [<CommonParameters>]


DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.


PARAMETERS
    -InstanceName <String>

    -DependsOn <String[]>

    -PsDscRunAsCredential <PSCredential>

    -OutputPath <String>

    -ConfigurationData <Hashtable>

    -ComputerName <String>
        The description of a parameter. Add a .PARAMETER keyword for each parameter in the function or script syntax.

        Type the parameter name on the same line as the .PARAMETER keyword. Type the parameter description on the lines following the .PARAMETER keyword.
        Windows PowerShell interprets all text between the .PARAMETER line and the next keyword or the end of the comment block as part of the parameter description.
        The description can include paragraph breaks.

        The Parameter keywords can appear in any order in the comment block, but the function or script syntax determines the order in which the parameters
        (and their descriptions) appear in help topic. To change the order, change the syntax.

    -FilePath <String>
        Provide a PARAMETER section for each parameter that your script or function accepts.

    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (https:/go.microsoft.com/fwlink/?LinkID=113216).

    -------------------------- EXAMPLE 1 --------------------------

    PS C:\>HelpSample -ComputerName localhost

    A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example.
    PowerShell automatically prefaces the first line with a PowerShell prompt. Additional lines are treated as output and description. The example can contain spaces, newlines and PowerShell code.

    If you have multiple examples, there is no need to number them. PowerShell will number the examples in help text.




    -------------------------- EXAMPLE 2 --------------------------

    PS C:\>HelpSample -FilePath "C:\output.txt"

    This example will be labeled "EXAMPLE 2" when help is displayed to the user.




REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

> [!NOTE]
> <span data-ttu-id="bd038-117">Szintaxis mezőket és a paraméter-attribútumok automatikusan jönnek létre az Ön számára PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bd038-117">Syntax fields and parameter attributes are automatically generated for you by PowerShell.</span></span>

## <a name="see-also"></a><span data-ttu-id="bd038-118">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bd038-118">See Also</span></span>

- [<span data-ttu-id="bd038-119">DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="bd038-119">DSC Configurations</span></span>](configurations.md)
- [<span data-ttu-id="bd038-120">Írási, fordítsa le és a konfiguráció alkalmazása</span><span class="sxs-lookup"><span data-stu-id="bd038-120">Write, Compile, and Apply a Configuration</span></span>](write-compile-apply-configuration.md)
- [<span data-ttu-id="bd038-121">A konfigurációs paraméterek hozzáadása</span><span class="sxs-lookup"><span data-stu-id="bd038-121">Add Parameters to a Configuration</span></span>](add-parameters-to-a-configuration.md)
