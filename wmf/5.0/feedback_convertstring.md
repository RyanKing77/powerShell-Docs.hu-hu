---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 27541d903748738675917941dc6b60bc9acdc3f4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684499"
---
# <a name="convert-string"></a>Convert-String
**A Convert-karakterlánc** "Magic Quadrant lecseréléshez" funkciókkal rendelkezik. Adja meg a előtt és után példák a kívánt hely, szöveg és **Convert-karakterlánc** automatikusan formázza a szöveget. Íme egy demó - véve valakinek a első és utolsó nevét, és cserélje a Vezetéknév, vesszővel, a Vezetéknév, és a egy pont első kezdeti. Próbálja ki a reguláris kifejezést, és tekintse meg, hogy mennyi ideig tart meg.

```powershell
"Lee Holmes", "Steve Lee", "Jeffrey Snover" | Convert-String -Example "Bill Gates=Gates, B.","John Smith=Smith, J."

Holmes, L.
Lee, S.
Snover, J.
```
