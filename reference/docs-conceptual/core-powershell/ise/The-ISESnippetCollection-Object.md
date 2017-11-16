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
# <a name="the-isesnippetcollection-object"></a><span data-ttu-id="d6c56-103">A ISESnippetCollection objektum</span><span class="sxs-lookup"><span data-stu-id="d6c56-103">The ISESnippetCollection Object</span></span>
  <span data-ttu-id="d6c56-104">A **ISESnippetCollection** objektum gyűjteménye **ISESnippet** objektumok.</span><span class="sxs-lookup"><span data-stu-id="d6c56-104">The **ISESnippetCollection** object is a collection of **ISESnippet** objects.</span></span> <span data-ttu-id="d6c56-105">A fájlok gyűjteményt, amelyhez társítva van egy **PowerShellTab** objektum Ez az osztály tagja.</span><span class="sxs-lookup"><span data-stu-id="d6c56-105">The files collection that is associated with a **PowerShellTab** object is a member of this class.</span></span> <span data-ttu-id="d6c56-106">Példa: a **$psISE.CurrentPowerShellTab.Files** gyűjtemény.</span><span class="sxs-lookup"><span data-stu-id="d6c56-106">An example is the **$psISE.CurrentPowerShellTab.Files** collection.</span></span>

## <a name="methods"></a><span data-ttu-id="d6c56-107">Metódusok</span><span class="sxs-lookup"><span data-stu-id="d6c56-107">Methods</span></span>

### <a name="load-filepathname-"></a><span data-ttu-id="d6c56-108">Betöltési\( FilePathName\)</span><span class="sxs-lookup"><span data-stu-id="d6c56-108">Load\( FilePathName \)</span></span>
  <span data-ttu-id="d6c56-109">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="d6c56-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="d6c56-110">Betölti a. felhasználói kódtöredékek tartalmazó snippets.ps1xml fájlt.</span><span class="sxs-lookup"><span data-stu-id="d6c56-110">Loads a .snippets.ps1xml file that contains user-defined snippets.</span></span> <span data-ttu-id="d6c56-111">A részletek létrehozásához legkönnyebben automatikusan azokat a profil mappában tárolja, hogy-e töltve a Windows PowerShell ISE minden indításakor új-IseSnippet parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="d6c56-111">The easiest way to create snippets is to use the New-IseSnippet cmdlet, which automatically stores them in your profile folder so that they are loaded every time that you start Windows PowerShell ISE.</span></span>

 <span data-ttu-id="d6c56-112">**FilePathName** - karakterláncban az elérési út és fájlnév a egy. snippets.ps1xml fájlt, amely részlet definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="d6c56-112">**FilePathName** - String The path and file name to a .snippets.ps1xml file that contains snippet definitions.</span></span>

```
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) “Snippets\MySnips.snippets.ps1xml” $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)

```

## <a name="see-also"></a><span data-ttu-id="d6c56-113">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d6c56-113">See Also</span></span>
- [<span data-ttu-id="d6c56-114">A ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="d6c56-114">The ISESnippetObject</span></span>](The-ISESnippetObject.md) 
- [<span data-ttu-id="d6c56-115">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="d6c56-115">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="d6c56-116">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="d6c56-116">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="d6c56-117">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="d6c56-117">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
