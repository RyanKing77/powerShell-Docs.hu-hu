---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 89e908969641afd9ad9541dcfedcc8eb6315d07c
ms.sourcegitcommit: ece1794c94be4880a2af5a2605ed4721593643b6
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/16/2018
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a>Modulok támogatása deklaráló verzió tartományok (1.*, stb.)
Együtt **- MinimumVersion**, **- MaximumVersion** mostantól lehetővé teszi a felhasználónak az adott tartományon belüli get/importálás modul. A paraméter is támogatja a **.** \*. A következő példa bemutatja, hogyan működik:

Most, kombinálhatja **- MinimumVersion** és **- MaximumVersion** adott tartományon belüli modul importálásához:

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
