---
ms.date: 06/12/2017
keywords: a DSC, a powershell, a konfiguráció, a beállítása
title: DSC-konfigurációk súgóinak összeállítása
ms.openlocfilehash: 316fd69ab1eae66ebe141b2575a05b502fc261ea
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222663"
---
# <a name="writing-help-for-dsc-configurations"></a><span data-ttu-id="86efd-103">DSC-konfigurációk súgóinak összeállítása</span><span class="sxs-lookup"><span data-stu-id="86efd-103">Writing help for DSC configurations</span></span>

><span data-ttu-id="86efd-104">Vonatkozik: Windows Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="86efd-104">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="86efd-105">A DSC-konfigurációk Megjegyzés-alapú súgó használható.</span><span class="sxs-lookup"><span data-stu-id="86efd-105">You can use comment-based help in DSC configurations.</span></span> <span data-ttu-id="86efd-106">Felhasználók férhetnek hozzá a Súgó a konfigurációs függvény meghívásával `-?`, vagy a [Get-Help](https://technet.microsoft.com/library/hh849696.aspx) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="86efd-106">Users can access the help by calling the configuration function with `-?`, or by using the [Get-Help](https://technet.microsoft.com/library/hh849696.aspx) cmdlet.</span></span> <span data-ttu-id="86efd-107">További információ a PowerShell Megjegyzés-alapú súgó: [about_Comment_Based_Help](https://technet.microsoft.com/library/hh847834.aspx).</span><span class="sxs-lookup"><span data-stu-id="86efd-107">For more information about PowerShell comment-based help, see [about_Comment_Based_Help](https://technet.microsoft.com/library/hh847834.aspx).</span></span>

<span data-ttu-id="86efd-108">A következő példa bemutatja egy parancsfájlt, amely tartalmazza a konfigurációs és a Megjegyzés-alapú súgó hozzá:</span><span class="sxs-lookup"><span data-stu-id="86efd-108">The following example shows a script that contains a configuration and comment-based help for it:</span></span>

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

.PARAMETER FilePath
Provide a PARAMETER section for each parameter that your script or function accepts.

.EXAMPLE
A sample command that uses the function or script, optionally followed by sample output and a description. Repeat this keyword for each example. If you have multiple examples,
there is no need to number them. PowerShell will number the examples in help text.

.EXAMPLE
This example will be labeled "EXAMPLE 2" when help is displayed to the user.
#>

configuration HelpSample1
{
    param([string]$ComputerName,[string]$FilePath)
    File f
    {
        Contents="Hello World"
        DestinationPath = "c:\Destination.txt"
    }
}
```

## <a name="viewing-configuration-help"></a><span data-ttu-id="86efd-109">Konfigurációs súgó megtekintése</span><span class="sxs-lookup"><span data-stu-id="86efd-109">Viewing configuration help</span></span>

<span data-ttu-id="86efd-110">A Súgó gombra a konfiguráció megtekintéséhez használja a **Get-Help** parancsmagot típus vagy függvény nevével, amelyre a függvény neve követ `-?`.</span><span class="sxs-lookup"><span data-stu-id="86efd-110">To view the help for a configuration, use the **Get-Help** cmdlet with the name of the function, or type the name of the function followed by `-?`.</span></span> <span data-ttu-id="86efd-111">Az alábbiakban található a korábbi függvény átadott kimenete **Get-Help**:</span><span class="sxs-lookup"><span data-stu-id="86efd-111">The following is the output of the previous function when passed to **Get-Help**:</span></span>

```powershell
PS C:\> Get-Help HelpSample1

NAME
    HelpSample1

SYNOPSIS
    A brief description of the function or script. This keyword can be used only once for each configuration.


SYNTAX
    HelpSample1 [[-InstanceName] <String>] [[-DependsOn] <String[]>] [[-OutputPath] <String>] [[-ConfigurationData] <Hashtable>] [[-ComputerName]
    <String>] [[-FilePath] <String>] [<CommonParameters>]


DESCRIPTION
    A detailed description of the function or script. This keyword can be used only once for each configuration.


RELATED LINKS

REMARKS
    To see the examples, type: "get-help HelpSample1 -examples".
    For more information, type: "get-help HelpSample1 -detailed".
    For technical information, type: "get-help HelpSample1 -full".
```

## <a name="see-also"></a><span data-ttu-id="86efd-112">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="86efd-112">See Also</span></span>
* [<span data-ttu-id="86efd-113">A DSC-konfigurációk</span><span class="sxs-lookup"><span data-stu-id="86efd-113">DSC Configurations</span></span>](configurations.md)