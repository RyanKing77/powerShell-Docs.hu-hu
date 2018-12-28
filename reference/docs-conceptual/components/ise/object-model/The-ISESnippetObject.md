---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: f80080f4207cf226fb7466c4842446d08c081347
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404591"
---
# <a name="the-isesnippetobject"></a>Az ISESnippetObject

Egy **ISESnippet** objektum a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát. A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény összes példák a **ISESnippet** objektumokat. Hozzon létre egy kódrészletet legegyszerűbb módja az, hogy használja a [New-IseSnippet&#91;PSITPro5_ISE&#93; ](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmagot.

## <a name="properties"></a>Tulajdonságok

### <a name="author"></a>Szerző

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a kódrészlet szerzőjének nevét.

```powershell
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author
```

### <a name="codefragment"></a>CodeFragment

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a kódrészletet a szerkesztő beszúrni.

```powershell
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment
```

### <a name="shortcut"></a>Helyi

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a Windows a menüelem billentyűparancsot.

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a>Lásd még:

- [Az ISESnippetCollection objektum](The-ISESnippetCollection-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](purpose-of-the-windows-powershell-ise-scripting-object-model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)