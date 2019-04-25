---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: db9c630bcb8e9e0da423c779976739f1ae76f13e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057432"
---
# <a name="archive-cmdlets"></a>Archív parancsmagok

Két új parancsmagot **Compress archiválása** és **Expand-archívum**, hagyjuk, hogy tömöríteni, és bontsa ki a ZIP-fájlokat.

## <a name="compress-archive"></a>Compress-Archive
A **Compress archiválása** parancsmag egy új fájlt hoz létre a megadott fájlok. Archív fájl több csomagolni, és igény szerint egyszerűbb kezelését és a storage egyetlen fájlba tömörített fájlok teszi lehetővé. Archív fájl a megadott tömörítési algoritmust tömörítheti a **- CompressionLevel** paraméter.
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a>Bontsa ki a csomópontot archív
A **Expand-archívum** parancsmag fájlok kibontása a megadott archívum fájlból. Archív fájl több csomagolni, és igény szerint egyszerűbb kezelését és a storage egyetlen fájlba tömörített fájlok teszi lehetővé.
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
