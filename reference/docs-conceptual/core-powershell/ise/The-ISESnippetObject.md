---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: Az ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: f1b023291826d5568eb8bdf5a898a00228825276
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/15/2018
---
# <a name="the-isesnippetobject"></a><span data-ttu-id="4b1b4-103">Az ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="4b1b4-103">The ISESnippetObject</span></span>
  <span data-ttu-id="4b1b4-104">Egy **ISESnippet** célja a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-104">An **ISESnippet** object is an instance of the Microsoft.PowerShell.Host.ISE.ISESnippet class.</span></span> <span data-ttu-id="4b1b4-105">A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény valamennyien **ISESnippet** objektumok.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-105">The members of the **$psISE.CurrentPowerShellTab.Snippets** collection are all examples of **ISESnippet** objects.</span></span> <span data-ttu-id="4b1b4-106">Hozzon létre egy kódrészletet a legegyszerűbb módja használatára a [New-IseSnippet&#91;PSITPro5_ISE&#93; ](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmag.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-106">The easiest way to create a snippet is to use the [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) cmdlet.</span></span>

## <a name="properties"></a><span data-ttu-id="4b1b4-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="4b1b4-107">Properties</span></span>

### <a name="author"></a><span data-ttu-id="4b1b4-108">Szerző</span><span class="sxs-lookup"><span data-stu-id="4b1b4-108">Author</span></span>
  <span data-ttu-id="4b1b4-109">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="4b1b4-110">A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szerzőjének nevét.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-110">The read-only property that gets the name of the author of the snippet.</span></span>

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

### <a name="codefragment"></a><span data-ttu-id="4b1b4-111">CodeFragment</span><span class="sxs-lookup"><span data-stu-id="4b1b4-111">CodeFragment</span></span>
  <span data-ttu-id="4b1b4-112">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-112">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="4b1b4-113">A csak olvasható tulajdonság, amely lekérdezi a kódrészletet szúrhatók be a szerkesztőt.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-113">The read-only property that gets the code fragment to be inserted into the editor.</span></span>

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

### <a name="shortcut"></a><span data-ttu-id="4b1b4-114">Shortcut</span><span class="sxs-lookup"><span data-stu-id="4b1b4-114">Shortcut</span></span>
  <span data-ttu-id="4b1b4-115">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-115">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

 <span data-ttu-id="4b1b4-116">A csak olvasható tulajdonság, amely lekérdezi a Windows a menüelemhez tartozó billentyűparancsot.</span><span class="sxs-lookup"><span data-stu-id="4b1b4-116">The read-only property that gets the Windows keyboard shortcut for the menu item.</span></span>

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a><span data-ttu-id="4b1b4-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4b1b4-117">See Also</span></span>
- [<span data-ttu-id="4b1b4-118">A ISESnippetCollection objektum</span><span class="sxs-lookup"><span data-stu-id="4b1b4-118">The ISESnippetCollection Object</span></span>](The-ISESnippetCollection-Object.md)
- [<span data-ttu-id="4b1b4-119">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="4b1b4-119">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](purpose-of-the-windows-powershell-ise-scripting-object-model.md)
- [<span data-ttu-id="4b1b4-120">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="4b1b4-120">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
