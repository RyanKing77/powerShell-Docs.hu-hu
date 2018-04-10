---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 6356902193fc6ec651b2f7e53f8885cb59f17542
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="updates-to-fileinfo-object"></a>A FileInfo objektum frissítései
Fájlverzió-információkat is lehet félrevezető, különösen olyan esetekben, ahol a fájl telepítve lett. Ebben a kiadásban a WMF 5.0 hozzáadja az új **FileVersionRaw** és **ProductVersionRaw** parancsfájl-FileInfo objektumok tulajdonságai. A powershell.exe (feltéve, hogy $pid a PowerShell folyamat azonosítója) jelenik meg, az alábbiakban a tulajdonságok:

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117