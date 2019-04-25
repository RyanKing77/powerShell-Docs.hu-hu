---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: e01f6ceea361f5a9b3de645346d0652986b6267d
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057230"
---
# <a name="nonewline-parameter"></a><span data-ttu-id="81da1-102">NoNewLine paraméter</span><span class="sxs-lookup"><span data-stu-id="81da1-102">NoNewLine parameter</span></span>
<span data-ttu-id="81da1-103">**Out-File**, **Add-tartalom**, és **Set-tartalom** most már rendelkezik egy új **– NoNewline** kapcsolót, amely egyszerűen kihagyja a kimenet után egy új sort.</span><span class="sxs-lookup"><span data-stu-id="81da1-103">**Out-File**, **Add-Content**, and **Set-Content** now have a new **–NoNewline** switch which simply omits a new line after the output.</span></span>
```powershell
PS C:\> "This is " | Out-File -FilePath Example.txt -NoNewline

PS C:\>; "a single " | Add-Content -Path Example.txt -NoNewline

PS C:\> "sentence." | Add-Content -Path Example.txt -NoNewline

PS C:\> Get-Content .\Example.txt

This is a single sentence.
```
<span data-ttu-id="81da1-104">Nélkül **– NoNewline** megadott, minden egyes töredék lenne külön sorban:</span><span class="sxs-lookup"><span data-stu-id="81da1-104">Without **–NoNewline** specified, each fragment would be on a separate line:</span></span>
```powershell
PS C:\> "This is " | Out-File -FilePath Example.txt

PS C:\> "a single " | Add-Content -Path Example.txt

PS C:\> "sentence." | Add-Content -Path Example.txt

PS C:\> Get-Content .\Example.txt

This is

a single

sentence.
```
