---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 90e0ab3579e1840598cc3050c27db0b73ba6f69d
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="new-temporaryfile"></a>Új TemporaryFile
Egyes esetekben a parancsfájlokban kell létrehoznia egy ideiglenes fájlt. Könnyen ehhez a a **New-TemporaryFile** parancsmagot:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\ &gt; $tempFile.FullName

C:\\felhasználók\\slee\\AppData\\helyi\\Temp\\tmp375.tmp

