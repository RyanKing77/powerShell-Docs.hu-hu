---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 0c450d765531c18c0b73c5c64262e9895f92068a
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="archive-cmdlets"></a>Archív parancsmagok

Két új parancsmagok **Compress-archívum** és **kibontott-archívum**, hogy tömöríti, és bontsa ki a ZIP-fájl.

## <a name="compress-archive"></a>Compress-Archive
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