---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 9ca12ad3f0729a2e9595d7ca5ccf9041e47658a3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34218093"
---
# <a name="archive-cmdlets"></a><span data-ttu-id="36b8c-102">Archív parancsmagok</span><span class="sxs-lookup"><span data-stu-id="36b8c-102">Archive cmdlets</span></span>

<span data-ttu-id="36b8c-103">Két új parancsmagok **Compress-archívum** és **kibontott-archívum**, hogy tömöríti, és bontsa ki a ZIP-fájl.</span><span class="sxs-lookup"><span data-stu-id="36b8c-103">Two new cmdlets, **Compress-Archive** and **Expand-Archive**, let you compress and expand ZIP files.</span></span>

## <a name="compress-archive"></a><span data-ttu-id="36b8c-104">Compress-archívum</span><span class="sxs-lookup"><span data-stu-id="36b8c-104">Compress-Archive</span></span>
<span data-ttu-id="36b8c-105">A **Compress-archívum** parancsmag létrehoz egy új fájlt a megadott fájlok.</span><span class="sxs-lookup"><span data-stu-id="36b8c-105">The **Compress-Archive** cmdlet creates a new archive file from specified files.</span></span> <span data-ttu-id="36b8c-106">Archív fájlba kell csomagolni, és opcionálisan az egyszerűbb kezelés és tárolás egyetlen fájlba tömörített több fájlok teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="36b8c-106">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span> <span data-ttu-id="36b8c-107">Az archív fájl a megadott tömörítési algoritmust tömörítheti a **- CompressionLevel** paraméter.</span><span class="sxs-lookup"><span data-stu-id="36b8c-107">An archive file can be compressed by using a compression algorithm specified in the **-CompressionLevel** parameter.</span></span>
```powershell
Compress-Archive -LiteralPath <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
Compress-Archive [-Path] <String[]> [-DestinationPath] <String> [-Update] [-CompressionLevel <Microsoft.PowerShell.Commands.CompressionLevel>]
```

## <a name="expand-archive"></a><span data-ttu-id="36b8c-108">Bontsa ki a archív</span><span class="sxs-lookup"><span data-stu-id="36b8c-108">Expand-Archive</span></span>
<span data-ttu-id="36b8c-109">A **kibontott-archívum** parancsmag fájlok kibontása a megadott archívum fájlból.</span><span class="sxs-lookup"><span data-stu-id="36b8c-109">The **Expand-Archive** cmdlet extracts files from a specified archive file.</span></span> <span data-ttu-id="36b8c-110">Archív fájlba kell csomagolni, és opcionálisan az egyszerűbb kezelés és tárolás egyetlen fájlba tömörített több fájlok teszi lehetővé.</span><span class="sxs-lookup"><span data-stu-id="36b8c-110">An archive file allows multiple files to be packaged and optionally compressed into a single file for easier handling and storage.</span></span>
```powershell
Expand-Archive -LiteralPath <String> [-DestinationPath] <String>
Expand-Archive [-Path] <String> [-DestinationPath] <String>
```
