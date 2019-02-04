---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e01f6ceea361f5a9b3de645346d0652986b6267d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55685913"
---
# <a name="nonewline-parameter"></a>NoNewLine paraméter
**Out-File**, **Add-tartalom**, és **Set-tartalom** most már rendelkezik egy új **– NoNewline** kapcsolót, amely egyszerűen kihagyja a kimenet után egy új sort.
```powershell
PS C:\> "This is " | Out-File -FilePath Example.txt -NoNewline

PS C:\>; "a single " | Add-Content -Path Example.txt -NoNewline

PS C:\> "sentence." | Add-Content -Path Example.txt -NoNewline

PS C:\> Get-Content .\Example.txt

This is a single sentence.
```
Nélkül **– NoNewline** megadott, minden egyes töredék lenne külön sorban:
```powershell
PS C:\> "This is " | Out-File -FilePath Example.txt

PS C:\> "a single " | Add-Content -Path Example.txt

PS C:\> "sentence." | Add-Content -Path Example.txt

PS C:\> Get-Content .\Example.txt

This is

a single

sentence.
```
