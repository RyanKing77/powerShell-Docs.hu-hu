---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 587f3f592f4aab53c95bbc6d37ea37d7f2364aec
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="updates-to-fileinfo-object"></a>Frissítések FileInfo objektumhoz
Fájlverzió-információkat is lehet félrevezető, különösen olyan esetekben, ahol a fájl telepítve lett. Ebben a kiadásban a WMF 5.0 hozzáadja az új **FileVersionRaw** és **ProductVersionRaw** parancsfájl-FileInfo objektumok tulajdonságai. A powershell.exe (feltéve, hogy $pid a PowerShell folyamat azonosítója) jelenik meg, az alábbiakban a tulajdonságok:

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117

