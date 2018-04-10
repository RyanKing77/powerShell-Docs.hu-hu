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
---
# <a name="the-isesnippetcollection-object"></a><span data-ttu-id="5e5da-103">Az ISESnippetCollection objektum</span><span class="sxs-lookup"><span data-stu-id="5e5da-103">The ISESnippetCollection Object</span></span>

<span data-ttu-id="5e5da-104">A **ISESnippetCollection** objektum gyűjteménye **ISESnippet** objektumok.</span><span class="sxs-lookup"><span data-stu-id="5e5da-104">The **ISESnippetCollection** object is a collection of **ISESnippet** objects.</span></span> <span data-ttu-id="5e5da-105">A fájlok gyűjteményt, amelyhez társítva van egy **PowerShellTab** objektum Ez az osztály tagja.</span><span class="sxs-lookup"><span data-stu-id="5e5da-105">The files collection that is associated with a **PowerShellTab** object is a member of this class.</span></span> <span data-ttu-id="5e5da-106">Példa: a **$psISE.CurrentPowerShellTab.Files** gyűjtemény.</span><span class="sxs-lookup"><span data-stu-id="5e5da-106">An example is the **$psISE.CurrentPowerShellTab.Files** collection.</span></span>

## <a name="methods"></a><span data-ttu-id="5e5da-107">Metódusok</span><span class="sxs-lookup"><span data-stu-id="5e5da-107">Methods</span></span>

### <a name="load-filepathname-"></a><span data-ttu-id="5e5da-108">Load\( FilePathName \)</span><span class="sxs-lookup"><span data-stu-id="5e5da-108">Load\( FilePathName \)</span></span>

<span data-ttu-id="5e5da-109">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="5e5da-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="5e5da-110">Betölti a. felhasználói kódtöredékek tartalmazó snippets.ps1xml fájlt.</span><span class="sxs-lookup"><span data-stu-id="5e5da-110">Loads a .snippets.ps1xml file that contains user-defined snippets.</span></span> <span data-ttu-id="5e5da-111">A részletek létrehozásához legkönnyebben automatikusan azokat a profil mappában tárolja, hogy-e töltve a Windows PowerShell ISE minden indításakor új-IseSnippet parancsmag használatával.</span><span class="sxs-lookup"><span data-stu-id="5e5da-111">The easiest way to create snippets is to use the New-IseSnippet cmdlet, which automatically stores them in your profile folder so that they are loaded every time that you start Windows PowerShell ISE.</span></span>

<span data-ttu-id="5e5da-112">**FilePathName** - karakterláncban az elérési út és fájlnév a egy. snippets.ps1xml fájlt, amely részlet definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="5e5da-112">**FilePathName** - String The path and file name to a .snippets.ps1xml file that contains snippet definitions.</span></span>

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a><span data-ttu-id="5e5da-113">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5e5da-113">See Also</span></span>

- [<span data-ttu-id="5e5da-114">A ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="5e5da-114">The ISESnippetObject</span></span>](The-ISESnippetObject.md)
- [<span data-ttu-id="5e5da-115">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="5e5da-115">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="5e5da-116">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="5e5da-116">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)