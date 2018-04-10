---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 1f165afbcd8fe8dc5f72cc7ea557d21ce2884e91
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="nonewline-parameter"></a><span data-ttu-id="759d6-102">NoNewLine paraméter</span><span class="sxs-lookup"><span data-stu-id="759d6-102">NoNewLine parameter</span></span>
<span data-ttu-id="759d6-103">**Out-File**, **Add-tartalom**, és **Set-tartalom** most már rendelkezik egy új **– NoNewline** kapcsolót, amely egyszerűen kihagyja a kimenet után egy új sort.</span><span class="sxs-lookup"><span data-stu-id="759d6-103">**Out-File**, **Add-Content**, and **Set-Content** now have a new **–NoNewline** switch which simply omits a new line after the output.</span></span>
```powershell
PS C:\> "This is " | Out-File -FilePath Example.txt -NoNewline

PS C:\>; "a single " | Add-Content -Path Example.txt -NoNewline

PS C:\> "sentence." | Add-Content -Path Example.txt -NoNewline

PS C:\> Get-Content .\Example.txt

This is a single sentence.
```
<span data-ttu-id="759d6-104">Nélkül **– NoNewline** megadott, minden egyes töredék lenne külön sorban:</span><span class="sxs-lookup"><span data-stu-id="759d6-104">Without **–NoNewline** specified, each fragment would be on a separate line:</span></span>
```powershell
PS C:\> "This is " | Out-File -FilePath Example.txt

PS C:\> "a single " | Add-Content -Path Example.txt

PS C:\> "sentence." | Add-Content -Path Example.txt

PS C:\> Get-Content .\Example.txt

This is

a single

sentence.
```