---
ms.date: 06/12/2017
keywords: WMF, powershell, beállítás
title: Távolítsa el a WMF 5.0
ms.openlocfilehash: f562a4a4506bfdede6b23bd186b80f40cc9e45ca
ms.sourcegitcommit: 01b81317029b28dd9b61d167045fd31f1ec7bc06
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 05/17/2019
ms.locfileid: "65856188"
---
# <a name="uninstallation-instructions"></a>Az Eltávolítás utasítások

## <a name="using-command-prompt"></a>Parancssor használatával

1. Nyissa meg **parancssort.**
2. Futtassa a [Windows Update önálló indítója](https://support.microsoft.com/en-us/kb/934307) alább látható módon:

A Windows Server 2012 R2 és Windows 8.1:

```powershell
wusa /uninstall /kb:3134758
```

A Windows Server 2012:

```powershell
wusa /uninstall /kb:3134759
```

A Windows Server 2008 R2 SP1 és Windows 7 SP1 esetén:

```powershell
wusa /uninstall /kb:3134760
```

## <a name="using-control-panel"></a>Vezérlőpult használatával

1. Nyissa meg **vezérlőpultot.**
2. Nyissa meg a **programok**, majd nyissa meg **program eltávolítása lehetőségre.**
3. Kattintson a **telepített frissítések megjelenítése.**
4. Válassza ki **Windows Management Framework 5.0** telepített frissítések listájából. Ez megfelel *KB3134758*, *KB3134759*, vagy *KB3134760*. Kattintson a **eltávolítása.**
