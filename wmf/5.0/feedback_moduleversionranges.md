---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e2c9233734a6ede04e8ec2bbad05950cbb31cbba
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55687985"
---
# <a name="modules-support-for-declaring-version-ranges-1-etc"></a>Modultámogatás a deklaráló verzió tartományok (1.* stb.)
Kombinálva **- MinimumVersion**, **- MaximumVersion** mostantól lehetővé teszi a felhasználó adott tartományon belüli/importálás modul számára. A paraméter is támogatja **.** \*. Az alábbi példa bemutatja, hogyan működik:

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
