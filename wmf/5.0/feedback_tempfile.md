---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: aa2e9540af8b3d4c5de5e00377a84e0e5edd6e4a
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057850"
---
# <a name="new-temporaryfile"></a>New-TemporaryFile
Egyes esetekben a parancsfájlok kell létrehoznia egy ideiglenes fájlt. Könnyedén megteheti az ezt a **New-TemporaryFile** parancsmagot:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\&gt; $tempFile.FullName

C:\\felhasználók\\slee\\AppData\\helyi\\Temp\\tmp375.tmp
