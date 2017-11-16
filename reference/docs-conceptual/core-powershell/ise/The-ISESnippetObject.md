---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: 6112f5252d2d1e868092da4a6cd04feb1875b597
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/31/2017
---
# <a name="the-isesnippetobject"></a>A ISESnippetObject
  Egy **ISESnippet** célja a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát. A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény valamennyien **ISESnippet** objektumok. Hozzon létre egy kódrészletet a legegyszerűbb módja használatára a [új-IseSnippet &#91; PSITPro5_ISE &#93; ](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmag.

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

### <a name="shortcut"></a>Helyi
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
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)

  
