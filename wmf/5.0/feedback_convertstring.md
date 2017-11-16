---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 6caff8c06174a1dcb990ed8e5062ccca5848dbb8
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
---
# <a name="convert-string"></a><span data-ttu-id="f021c-102">A Convert-karakterlánc</span><span class="sxs-lookup"><span data-stu-id="f021c-102">Convert-String</span></span>
<span data-ttu-id="f021c-103">**A Convert-karakterlánc** olyan funkciókkal rendelkezik "lecserélni Bűvös".</span><span class="sxs-lookup"><span data-stu-id="f021c-103">**Convert-String** exposes "replace by magic" functionality.</span></span> <span data-ttu-id="f021c-104">Adja meg a előtt és után példák hogyan történjen az szöveget, és **Convert-karakterlánc** formázási automatikusan.</span><span class="sxs-lookup"><span data-stu-id="f021c-104">Provide before and after examples of how you want text to look, and **Convert-String** formats your text automatically.</span></span> <span data-ttu-id="f021c-105">Ez a bemutató - véve egy, a vezetéknevet és az utolsó, és cserélje le a nevük, vesszővel, a Vezetéknév, és egy pont első kezdeti.</span><span class="sxs-lookup"><span data-stu-id="f021c-105">Here's a demo - taking somebody's first and last name, and replacing it with their last name, a comma, the first initial of their last name, and a dot.</span></span> <span data-ttu-id="f021c-106">Próbálja ki a egy reguláris kifejezéssel, és tekintse meg, hogy mennyi ideig tart meg.</span><span class="sxs-lookup"><span data-stu-id="f021c-106">Try it with a regex, and see how long it takes you.</span></span>

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```

