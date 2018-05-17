---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 08f431c27cd0ee769518b5246af2fa95aa499d54
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="new-temporaryfile"></a>New-TemporaryFile
Egyes esetekben a parancsfájlokban kell létrehoznia egy ideiglenes fájlt. Könnyen ehhez a a **New-TemporaryFile** parancsmagot:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\ &gt; $tempFile.FullName

C:\\felhasználók\\slee\\AppData\\helyi\\Temp\\tmp375.tmp
