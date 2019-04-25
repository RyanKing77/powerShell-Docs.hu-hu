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
# <a name="archive-cmdlets"></a><span data-ttu-id="ef290-102">Archív parancsmagok</span><span class="sxs-lookup"><span data-stu-id="ef290-102">Archive cmdlets</span></span>

<span data-ttu-id="ef290-103">Két új parancsmagot **Compress archiválása** és **Expand-archívum**, hagyjuk, hogy tömöríteni, és bontsa ki a ZIP-fájlokat.</span><span class="sxs-lookup"><span data-stu-id="ef290-103">Two new cmdlets, **Compress-Archive** and **Expand-Archive**, let you compress and expand ZIP files.</span></span>

## <a name="compress-archive"></a><span data-ttu-id="ef290-104">Compress-Archive</span><span class="sxs-lookup"><span data-stu-id="ef290-104">Compress-Archive</span></span>
<span data-ttu-id="ef290-105">A **Compress archiválása** parancsmag egy új fájlt hoz létre a megadott fájlok.</span><span class="sxs-lookup"><span data-stu-id="ef290-105">The **Compress-Archive** cmdlet creates a new archive file from specified files.</span></span> <span data-ttu-id="ef290-106">Archív fájl több csomagolni, és igény szerint egyszerűbb kezelését és a storage egyetlen fájlba tömörített fájlok teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="ef290-106">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span> <span data-ttu-id="ef290-107">Archív fájl a megadott tömörítési algoritmust tömörítheti a **- CompressionLevel** paraméter.</span><span class="sxs-lookup"><span data-stu-id="ef290-107">An archive file can be compressed by using a compression algorithm specified in the **-CompressionLevel** parameter.</span></span>
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a><span data-ttu-id="ef290-108">Bontsa ki a csomópontot archív</span><span class="sxs-lookup"><span data-stu-id="ef290-108">Expand-Archive</span></span>
<span data-ttu-id="ef290-109">A **Expand-archívum** parancsmag fájlok kibontása a megadott archívum fájlból.</span><span class="sxs-lookup"><span data-stu-id="ef290-109">The **Expand-Archive** cmdlet extracts files from a specified archive file.</span></span> <span data-ttu-id="ef290-110">Archív fájl több csomagolni, és igény szerint egyszerűbb kezelését és a storage egyetlen fájlba tömörített fájlok teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="ef290-110">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span>
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
