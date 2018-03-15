---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: Az ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: f1b023291826d5568eb8bdf5a898a00228825276
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="the-isesnippetobject"></a>Az ISESnippetObject
  Egy **ISESnippet** célja a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát. A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény valamennyien **ISESnippet** objektumok. Hozzon létre egy kódrészletet a legegyszerűbb módja használatára a [New-IseSnippet&#91;PSITPro5_ISE&#93; ](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmag.

## <a name="properties"></a>Tulajdonságok

### <a name="author"></a>Szerző
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

 A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szerzőjének nevét.

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

### <a name="codefragment"></a>CodeFragment
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

 A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szúrhatók be a szerkesztőt.

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

### <a name="shortcut"></a>Shortcut
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

 A csak olvasható tulajdonság, amely lekérdezi a Windows a menüelemhez tartozó billentyűparancsot.

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a>Lásd még:
- [A ISESnippetCollection objektum](The-ISESnippetCollection-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](purpose-of-the-windows-powershell-ise-scripting-object-model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)
