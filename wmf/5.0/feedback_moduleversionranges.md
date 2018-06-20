---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: f491e30859cbe6cbaa58f94389382ff231c52956
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225691"
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="d0be9-102">Modulok támogatása deklaráló verzió tartományok (1.\*, stb.)</span><span class="sxs-lookup"><span data-stu-id="d0be9-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="d0be9-103">Együtt **- MinimumVersion**, **- MaximumVersion** mostantól lehetővé teszi a felhasználónak az adott tartományon belüli get/importálás modul.</span><span class="sxs-lookup"><span data-stu-id="d0be9-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="d0be9-104">A paraméter is támogatja a **.** \*.</span><span class="sxs-lookup"><span data-stu-id="d0be9-104">The parameter also support **.**\*.</span></span> <span data-ttu-id="d0be9-105">A következő példa bemutatja, hogyan működik:</span><span class="sxs-lookup"><span data-stu-id="d0be9-105">The following example shows how it works:</span></span>

<span data-ttu-id="d0be9-106">Most, kombinálhatja **- MinimumVersion** és **- MaximumVersion** adott tartományon belüli modul importálásához:</span><span class="sxs-lookup"><span data-stu-id="d0be9-106">Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:</span></span>

```powershell
PS C:\> Import-Module psreadline -Verbose -MinimumVersion 1.0 -MaximumVersion 1.2.*

VERBOSE: Loading module from path 'C:\Program Files\WindowsPowerShell\Modules\psreadline\1.1\psreadline.psd1'.
VERBOSE: Importing cmdlet 'Get-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Get-PSReadlineOption'.
VERBOSE: Importing cmdlet 'Remove-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineKeyHandler'.
VERBOSE: Importing cmdlet 'Set-PSReadlineOption'.
VERBOSE: Importing function 'PSConsoleHostReadline'.
```
