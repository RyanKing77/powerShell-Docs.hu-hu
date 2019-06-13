---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISESnippetCollection objektum
ms.openlocfilehash: 6c392c08767fba004f63155d5a469777856a0b59
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030499"
---
# <a name="the-isesnippetcollection-object"></a><span data-ttu-id="4c320-103">Az ISESnippetCollection objektum</span><span class="sxs-lookup"><span data-stu-id="4c320-103">The ISESnippetCollection Object</span></span>

<span data-ttu-id="4c320-104">A **ISESnippetCollection** objektum olyan gyűjteménye, **ISESnippet** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="4c320-104">The **ISESnippetCollection** object is a collection of **ISESnippet** objects.</span></span> <span data-ttu-id="4c320-105">A fájlok gyűjteményt, amelyhez társítva van egy **PowerShellTab** objektum a tagja, ez az osztály.</span><span class="sxs-lookup"><span data-stu-id="4c320-105">The files collection that is associated with a **PowerShellTab** object is a member of this class.</span></span> <span data-ttu-id="4c320-106">Például a **$psISE.CurrentPowerShellTab.Files** gyűjtemény.</span><span class="sxs-lookup"><span data-stu-id="4c320-106">An example is the **$psISE.CurrentPowerShellTab.Files** collection.</span></span>

## <a name="methods"></a><span data-ttu-id="4c320-107">Metódusok</span><span class="sxs-lookup"><span data-stu-id="4c320-107">Methods</span></span>

### <a name="load-filepathname-"></a><span data-ttu-id="4c320-108">Load\( FilePathName \)</span><span class="sxs-lookup"><span data-stu-id="4c320-108">Load\( FilePathName \)</span></span>

<span data-ttu-id="4c320-109">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="4c320-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="4c320-110">Betölti a. snippets.ps1xml fájlt, amely tartalmazza a felhasználói kódrészletek.</span><span class="sxs-lookup"><span data-stu-id="4c320-110">Loads a .snippets.ps1xml file that contains user-defined snippets.</span></span> <span data-ttu-id="4c320-111">A kódrészletek létrehozásának legegyszerűbb módja, hogy használja a New-IseSnippet parancsmagot, amely automatikusan tárolja őket a profil-mappában, hogy be töltve Windows PowerShell ISE-ben minden egyes indításakor.</span><span class="sxs-lookup"><span data-stu-id="4c320-111">The easiest way to create snippets is to use the New-IseSnippet cmdlet, which automatically stores them in your profile folder so that they are loaded every time that you start Windows PowerShell ISE.</span></span>

<span data-ttu-id="4c320-112">**FilePathName** – az elérési út karakterláncot, és a fájlnév egy. snippets.ps1xml fájlt, amely a kódrészlet kapcsolatos definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="4c320-112">**FilePathName** - String The path and file name to a .snippets.ps1xml file that contains snippet definitions.</span></span>

```powershell
# Loads a custom snippet file into the current PowerShell tab.
$SnipFile = Join-Path ( Split-Path $profile) 'Snippets\MySnips.snippets.ps1xml' $psISE.CurrentPowerShellTab.Snippets.Add($SnipPath)
```

## <a name="see-also"></a><span data-ttu-id="4c320-113">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4c320-113">See Also</span></span>

- [<span data-ttu-id="4c320-114">Az ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="4c320-114">The ISESnippetObject</span></span>](The-ISESnippetObject.md)
- [<span data-ttu-id="4c320-115">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="4c320-115">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="4c320-116">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="4c320-116">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
