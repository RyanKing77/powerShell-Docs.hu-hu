---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 302a347b0f4c9c322f7701e8d6a721f9ffba9b59
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="convert-string"></a>Convert-String
**A Convert-karakterlánc** olyan funkciókkal rendelkezik "lecserélni Bűvös". Adja meg a előtt és után példák hogyan történjen az szöveget, és **Convert-karakterlánc** formázási automatikusan. Ez a bemutató - véve egy, a vezetéknevet és az utolsó, és cserélje le a nevük, vesszővel, a Vezetéknév, és egy pont első kezdeti. Próbálja ki a egy reguláris kifejezéssel, és tekintse meg, hogy mennyi ideig tart meg.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```