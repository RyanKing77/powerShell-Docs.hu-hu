---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e2c9233734a6ede04e8ec2bbad05950cbb31cbba
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057506"
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a><span data-ttu-id="294e9-102">Modultámogatás a deklaráló verzió tartományok (1.\* stb.)</span><span class="sxs-lookup"><span data-stu-id="294e9-102">Modules support for declaring version ranges (1.\*, etc)</span></span>
<span data-ttu-id="294e9-103">Kombinálva **- MinimumVersion**, **- MaximumVersion** mostantól lehetővé teszi a felhasználó adott tartományon belüli/importálás modul számára.</span><span class="sxs-lookup"><span data-stu-id="294e9-103">Combined with **-MinimumVersion**, **-MaximumVersion** now allows user to get/import module within specific range.</span></span> <span data-ttu-id="294e9-104">A paraméter is támogatja **.** \*.</span><span class="sxs-lookup"><span data-stu-id="294e9-104">The parameter also support **.**\*.</span></span> <span data-ttu-id="294e9-105">Az alábbi példa bemutatja, hogyan működik:</span><span class="sxs-lookup"><span data-stu-id="294e9-105">The following example shows how it works:</span></span>

<span data-ttu-id="294e9-106">Most, kombinálhatja **- MinimumVersion** és **- MaximumVersion** adott tartományon belüli modul importálásához:</span><span class="sxs-lookup"><span data-stu-id="294e9-106">Now, you can combine **-MinimumVersion** and **-MaximumVersion** to import module within specific range:</span></span>

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
