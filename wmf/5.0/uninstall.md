---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
ms.openlocfilehash: 64a29aa87507e65a182837df538c5e695c420cb3
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2018
---
# <a name="uninstallation-instructions"></a>Az eltávolítás utasításokat

## <a name="using-command-prompt"></a>Parancssor használatával
1.  Nyissa meg **parancssort.**
2.  Futtassa a [Windows Update önálló indító](https://support.microsoft.com/en-us/kb/934307) alább látható módon:

A Windows Server 2012 R2 és Windows 8.1:
```powershell
wusa /uninstall /kb:3134758
```
A Windows Server 2012:
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
