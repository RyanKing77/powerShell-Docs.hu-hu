---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISESnippetCollection objektum
ms.assetid: ae974955-4282-4cbc-8c42-0fff1904ef32
ms.openlocfilehash: b19c5b5c88f7c8bd0d0c466c7861fa9288bdc7a2
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="the-isesnippetcollection-object"></a>A ISESnippetCollection objektum
  A **ISESnippetCollection** objektum gyűjteménye **ISESnippet** objektumok. A fájlok gyűjteményt, amelyhez társítva van egy **PowerShellTab** objektum Ez az osztály tagja. Példa: a **$psISE.CurrentPowerShellTab.Files** gyűjtemény.

## <a name="methods"></a>Metódusok

### <a name="load-filepathname-"></a>Betöltési\( FilePathName\)
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók. 

 Betölti a. felhasználói kódtöredékek tartalmazó snippets.ps1xml fájlt. A részletek létrehozásához legkönnyebben automatikusan azokat a profil mappában tárolja, hogy-e töltve a Windows PowerShell ISE minden indításakor új-IseSnippet parancsmag használatával.

 **FilePathName** - karakterláncban az elérési út és fájlnév a egy. snippets.ps1xml fájlt, amely részlet definíciókat tartalmazza.

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## <a name="see-also"></a>Lásd még:
- [A ISESnippetObject](The-ISESnippetObject.md) 
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)

  
