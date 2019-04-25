---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 5280ef5ff95679dc8721be8f5f81031a4ffe796f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62085246"
---
# <a name="updates-to-fileinfo-object"></a>A FileInfo objektum frissítései
Fájlverzió-információkat is félrevezető lehet, különösen olyan esetekben, ahol a fájl javítva lett. Ebben a kiadásban a WMF 5.0 ad hozzá új **FileVersionRaw** és **ProductVersionRaw** parancsfájl FileInfo objektum tulajdonságait. A powershell.exe (feltéve, hogy $pid a PowerShell-folyamat azonosítója) jelenik meg az alábbiakban a tulajdonságai:

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117
