---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 78ae7ecd40b4d8ad0a6750f43002986483ab18a7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="uninstallation-instructions"></a>Az eltávolítás utasításokat

## <a name="using-command-prompt"></a>Parancssor használatával
1.  Nyissa meg **parancssort.**
2.  Futtassa a [Windows Update önálló indító](https://support.microsoft.com/en-us/kb/934307) alább látható módon:

A Windows Server 2012 R2 és Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
On Windows Server 2012:
```powershell
wusa /uninstall /kb:3134759
```
A Windows Server 2008 R2 SP1 és Windows 7 SP1:
```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a>Vezérlőpult segítségével
1.  Nyissa meg **vezérlőpultot.**
2.  Nyissa meg a **programok**, majd nyissa meg **program eltávolítása.**
3.  Kattintson a **telepített frissítések megjelenítése.**
4.  Válassza ki **Windows Management Framework 5.0** telepített frissítések a listából. Ez megfelel *KB3134758*, *KB3134759*, vagy *KB3134760*. Kattintson a **eltávolítása.**