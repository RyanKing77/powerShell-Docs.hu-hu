---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISESnippetCollection objektum
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: bd5ed4a1f15e0a398b7c6a17f0071cad889be4a7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55684611"
---
# <a name="the-isesnippetcollection-object"></a>Az ISESnippetCollection objektum

A **ISESnippetCollection** objektum olyan gyűjteménye, **ISESnippet** objektumokat. A fájlok gyűjteményt, amelyhez társítva van egy **PowerShellTab** objektum a tagja, ez az osztály. Például a **$psISE.CurrentPowerShellTab.Files** gyűjtemény.

## <a name="methods"></a>Metódusok

### <a name="load-filepathname-"></a>Load\( FilePathName \)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Betölti a. snippets.ps1xml fájlt, amely tartalmazza a felhasználói kódrészletek. A kódrészletek létrehozásának legegyszerűbb módja, hogy használja a New-IseSnippet parancsmagot, amely automatikusan tárolja őket a profil-mappában, hogy be töltve Windows PowerShell ISE-ben minden egyes indításakor.

**FilePathName** – az elérési út karakterláncot, és a fájlnév egy. snippets.ps1xml fájlt, amely a kódrészlet kapcsolatos definíciókat tartalmazza.

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a>Lásd még:

- [Az ISESnippetObject](The-ISESnippetObject.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)