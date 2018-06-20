---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: f80080f4207cf226fb7466c4842446d08c081347
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954194"
---
# <a name="the-isesnippetobject"></a>Az ISESnippetObject

Egy **ISESnippet** célja a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát. A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény valamennyien **ISESnippet** objektumok. Hozzon létre egy kódrészletet a legegyszerűbb módja használatára a [New-IseSnippet&#91;PSITPro5_ISE&#93; ](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmag.

## <a name="properties"></a>Tulajdonságok

### <a name="author"></a>Szerző

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szerzőjének nevét.

```powershell
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author
```

### <a name="codefragment"></a>CodeFragment

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szúrhatók be a szerkesztőt.

```powershell
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment
```

### <a name="shortcut"></a>Shortcut

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a Windows a menüelemhez tartozó billentyűparancsot.

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a>Lásd még:

- [A ISESnippetCollection objektum](The-ISESnippetCollection-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](purpose-of-the-windows-powershell-ise-scripting-object-model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)