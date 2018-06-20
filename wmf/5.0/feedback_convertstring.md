---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 7730912707bb14e90a9926b387fb3a859d7ca26d
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219266"
---
# <a name="convert-string"></a>Convert-String
**A Convert-karakterlánc** olyan funkciókkal rendelkezik "lecserélni Bűvös". Adja meg a előtt és után példák hogyan történjen az szöveget, és **Convert-karakterlánc** formázási automatikusan. Ez a bemutató - véve egy, a vezetéknevet és az utolsó, és cserélje le a nevük, vesszővel, a Vezetéknév, és egy pont első kezdeti. Próbálja ki a egy reguláris kifejezéssel, és tekintse meg, hogy mennyi ideig tart meg.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```
