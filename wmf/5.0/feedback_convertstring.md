---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 27541d903748738675917941dc6b60bc9acdc3f4
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057791"
---
# <a name="convert-string"></a><span data-ttu-id="45e4b-102">Convert-String</span><span class="sxs-lookup"><span data-stu-id="45e4b-102">Convert-String</span></span>
<span data-ttu-id="45e4b-103">**A Convert-karakterlánc** "Magic Quadrant lecseréléshez" funkciókkal rendelkezik.</span><span class="sxs-lookup"><span data-stu-id="45e4b-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="45e4b-104">Adja meg a előtt és után példák a kívánt hely, szöveg és **Convert-karakterlánc** automatikusan formázza a szöveget.</span><span class="sxs-lookup"><span data-stu-id="45e4b-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="45e4b-105">Íme egy demó - véve valakinek a első és utolsó nevét, és cserélje a Vezetéknév, vesszővel, a Vezetéknév, és a egy pont első kezdeti.</span><span class="sxs-lookup"><span data-stu-id="45e4b-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="45e4b-106">Próbálja ki a reguláris kifejezést, és tekintse meg, hogy mennyi ideig tart meg.</span><span class="sxs-lookup"><span data-stu-id="45e4b-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```
