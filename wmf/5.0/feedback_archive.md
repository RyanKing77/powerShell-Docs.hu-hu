---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9ca12ad3f0729a2e9595d7ca5ccf9041e47658a3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="archive-cmdlets"></a>Archív parancsmagok

Két új parancsmagok **Compress-archívum** és **kibontott-archívum**, hogy tömöríti, és bontsa ki a ZIP-fájl.

## <a name="compress-archive"></a>Compress-archívum
A **Compress-archívum** parancsmag létrehoz egy új fájlt a megadott fájlok. Archív fájlba kell csomagolni, és opcionálisan az egyszerűbb kezelés és tárolás egyetlen fájlba tömörített több fájlok teszi lehetővé. Az archív fájl a megadott tömörítési algoritmust tömörítheti a **- CompressionLevel** paraméter.
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a>Bontsa ki a archív
A **kibontott-archívum** parancsmag fájlok kibontása a megadott archívum fájlból. Archív fájlba kell csomagolni, és opcionálisan az egyszerűbb kezelés és tárolás egyetlen fájlba tömörített több fájlok teszi lehetővé.
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
