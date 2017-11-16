---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 7ad4a00f7beba0de70696d88cd5448c7c638c50c
ms.sourcegitcommit: a5c0795ca6ec9332967bff9c151a8572feb1a53a
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 07/27/2017
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

