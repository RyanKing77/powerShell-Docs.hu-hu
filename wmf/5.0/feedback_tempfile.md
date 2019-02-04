---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: aa2e9540af8b3d4c5de5e00377a84e0e5edd6e4a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685115"
---
# <a name="new-temporaryfile"></a>New-TemporaryFile
Egyes esetekben a parancsfájlok kell létrehoznia egy ideiglenes fájlt. Könnyedén megteheti az ezt a **New-TemporaryFile** parancsmagot:

PS C:\\ &gt; $tempFile = New-TemporaryFile

PS C:\\&gt; $tempFile.FullName

C:\\felhasználók\\slee\\AppData\\helyi\\Temp\\tmp375.tmp
