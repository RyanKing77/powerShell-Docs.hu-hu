---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7730912707bb14e90a9926b387fb3a859d7ca26d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="convert-string"></a><span data-ttu-id="d98fd-102">Convert-String</span><span class="sxs-lookup"><span data-stu-id="d98fd-102">Convert-String</span></span>
<span data-ttu-id="d98fd-103">**A Convert-karakterlánc** olyan funkciókkal rendelkezik "lecserélni Bűvös".</span><span class="sxs-lookup"><span data-stu-id="d98fd-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="d98fd-104">Adja meg a előtt és után példák hogyan történjen az szöveget, és **Convert-karakterlánc** formázási automatikusan.</span><span class="sxs-lookup"><span data-stu-id="d98fd-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="d98fd-105">Ez a bemutató - véve egy, a vezetéknevet és az utolsó, és cserélje le a nevük, vesszővel, a Vezetéknév, és egy pont első kezdeti.</span><span class="sxs-lookup"><span data-stu-id="d98fd-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="d98fd-106">Próbálja ki a egy reguláris kifejezéssel, és tekintse meg, hogy mennyi ideig tart meg.</span><span class="sxs-lookup"><span data-stu-id="d98fd-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```
