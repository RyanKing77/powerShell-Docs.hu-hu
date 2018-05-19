---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 63c3b8237a9883b147380dfe9cb173107cea9aa9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="updates-to-fileinfo-object"></a>A FileInfo objektum frissítései
Fájlverzió-információkat is lehet félrevezető, különösen olyan esetekben, ahol a fájl telepítve lett. Ebben a kiadásban a WMF 5.0 hozzáadja az új **FileVersionRaw** és **ProductVersionRaw** parancsfájl-FileInfo objektumok tulajdonságai. A powershell.exe (feltéve, hogy $pid a PowerShell folyamat azonosítója) jelenik meg, az alábbiakban a tulajdonságok:

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117
