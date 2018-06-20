---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISESnippetCollection objektum
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: bd5ed4a1f15e0a398b7c6a17f0071cad889be4a7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30950950"
---
# <a name="the-isesnippetcollection-object"></a>Az ISESnippetCollection objektum

A **ISESnippetCollection** objektum gyűjteménye **ISESnippet** objektumok. A fájlok gyűjteményt, amelyhez társítva van egy **PowerShellTab** objektum Ez az osztály tagja. Példa: a **$psISE.CurrentPowerShellTab.Files** gyűjtemény.

## <a name="methods"></a>Metódusok

### <a name="load-filepathname-"></a>Load\( FilePathName \)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Betölti a. felhasználói kódtöredékek tartalmazó snippets.ps1xml fájlt. A részletek létrehozásához legkönnyebben automatikusan azokat a profil mappában tárolja, hogy-e töltve a Windows PowerShell ISE minden indításakor új-IseSnippet parancsmag használatával.

**FilePathName** - karakterláncban az elérési út és fájlnév a egy. snippets.ps1xml fájlt, amely részlet definíciókat tartalmazza.

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a>Lásd még:

- [A ISESnippetObject](The-ISESnippetObject.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)