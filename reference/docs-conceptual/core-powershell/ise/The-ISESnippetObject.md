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
# <a name="the-isesnippetobject"></a><span data-ttu-id="58d64-103">A ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="58d64-103">The ISESnippetObject</span></span>
  <span data-ttu-id="58d64-104">Egy **ISESnippet** célja a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="58d64-104">An **ISESnippet** object is an instance of the Microsoft.PowerShell.Host.ISE.ISESnippet class.</span></span> <span data-ttu-id="58d64-105">A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény valamennyien **ISESnippet** objektumok.</span><span class="sxs-lookup"><span data-stu-id="58d64-105">The members of the **$psISE.CurrentPowerShellTab.Snippets** collection are all examples of **ISESnippet** objects.</span></span> <span data-ttu-id="58d64-106">Hozzon létre egy kódrészletet a legegyszerűbb módja használatára a [új-IseSnippet &#91; PSITPro5_ISE &#93; ](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="58d64-106">The easiest way to create a snippet is to use the [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) cmdlet.</span></span>

## <a name="properties"></a><span data-ttu-id="58d64-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="58d64-107">Properties</span></span>

### <a name="author"></a><span data-ttu-id="58d64-108">Szerző</span><span class="sxs-lookup"><span data-stu-id="58d64-108">Author</span></span>
  <span data-ttu-id="58d64-109">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="58d64-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="58d64-110">A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szerzőjének nevét.</span><span class="sxs-lookup"><span data-stu-id="58d64-110">The read-only property that gets the name of the author of the snippet.</span></span>

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

### <a name="codefragment"></a><span data-ttu-id="58d64-111">CodeFragment</span><span class="sxs-lookup"><span data-stu-id="58d64-111">CodeFragment</span></span>
  <span data-ttu-id="58d64-112">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="58d64-112">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="58d64-113">A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szúrhatók be a szerkesztőt.</span><span class="sxs-lookup"><span data-stu-id="58d64-113">The read-only property that gets the code fragment to be inserted into the editor.</span></span>

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

### <a name="shortcut"></a><span data-ttu-id="58d64-114">Helyi</span><span class="sxs-lookup"><span data-stu-id="58d64-114">Shortcut</span></span>
  <span data-ttu-id="58d64-115">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="58d64-115">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="58d64-116">A csak olvasható tulajdonság, amely lekérdezi a Windows a menüelemhez tartozó billentyűparancsot.</span><span class="sxs-lookup"><span data-stu-id="58d64-116">The read-only property that gets the Windows keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a><span data-ttu-id="58d64-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="58d64-117">See Also</span></span>
- [<span data-ttu-id="58d64-118">A ISESnippetCollection objektum</span><span class="sxs-lookup"><span data-stu-id="58d64-118">The ISESnippetCollection Object</span></span>](The-ISESnippetCollection-Object.md) 
- [<span data-ttu-id="58d64-119">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="58d64-119">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="58d64-120">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="58d64-120">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="58d64-121">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="58d64-121">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
