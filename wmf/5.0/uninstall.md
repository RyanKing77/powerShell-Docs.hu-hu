---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, a powershell, a beállítása"
ms.openlocfilehash: 3392db954c22030bb64ae5093619d23952e1fcdb
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2017
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

