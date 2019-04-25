---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISESnippetObject
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: f80080f4207cf226fb7466c4842446d08c081347
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057978"
---
# <a name="the-isesnippetobject"></a><span data-ttu-id="60569-103">Az ISESnippetObject</span><span class="sxs-lookup"><span data-stu-id="60569-103">The ISESnippetObject</span></span>

<span data-ttu-id="60569-104">Egy **ISESnippet** objektum a Microsoft.PowerShell.Host.ISE.ISESnippet osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="60569-104">An **ISESnippet** object is an instance of the Microsoft.PowerShell.Host.ISE.ISESnippet class.</span></span> <span data-ttu-id="60569-105">A tagjai a **$psISE.CurrentPowerShellTab.Snippets** gyűjtemény összes példák a **ISESnippet** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="60569-105">The members of the **$psISE.CurrentPowerShellTab.Snippets** collection are all examples of **ISESnippet** objects.</span></span> <span data-ttu-id="60569-106">Hozzon létre egy kódrészletet legegyszerűbb módja az, hogy használja a [New-IseSnippet&#91;PSITPro5_ISE&#93; ](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="60569-106">The easiest way to create a snippet is to use the [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) cmdlet.</span></span>

## <a name="properties"></a><span data-ttu-id="60569-107">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="60569-107">Properties</span></span>

### <a name="author"></a><span data-ttu-id="60569-108">Szerző</span><span class="sxs-lookup"><span data-stu-id="60569-108">Author</span></span>

<span data-ttu-id="60569-109">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="60569-109">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="60569-110">A csak olvasható tulajdonság, amely lekérdezi a kódrészlet szerzőjének nevét.</span><span class="sxs-lookup"><span data-stu-id="60569-110">The read-only property that gets the name of the author of the snippet.</span></span>

```powershell
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author
```

### <a name="codefragment"></a><span data-ttu-id="60569-111">CodeFragment</span><span class="sxs-lookup"><span data-stu-id="60569-111">CodeFragment</span></span>

<span data-ttu-id="60569-112">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="60569-112">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="60569-113">A csak olvasható tulajdonság, amely lekérdezi a kódrészletet a szerkesztő beszúrni.</span><span class="sxs-lookup"><span data-stu-id="60569-113">The read-only property that gets the code fragment to be inserted into the editor.</span></span>

```powershell
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment
```

### <a name="shortcut"></a><span data-ttu-id="60569-114">Helyi</span><span class="sxs-lookup"><span data-stu-id="60569-114">Shortcut</span></span>

<span data-ttu-id="60569-115">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="60569-115">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="60569-116">A csak olvasható tulajdonság, amely lekérdezi a Windows a menüelem billentyűparancsot.</span><span class="sxs-lookup"><span data-stu-id="60569-116">The read-only property that gets the Windows keyboard shortcut for the menu item.</span></span>

```powershell
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.Add('_Process', {Get-Process}, 'Alt+P')
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a><span data-ttu-id="60569-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="60569-117">See Also</span></span>

- [<span data-ttu-id="60569-118">Az ISESnippetCollection objektum</span><span class="sxs-lookup"><span data-stu-id="60569-118">The ISESnippetCollection Object</span></span>](The-ISESnippetCollection-Object.md)
- [<span data-ttu-id="60569-119">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="60569-119">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](purpose-of-the-windows-powershell-ise-scripting-object-model.md)
- [<span data-ttu-id="60569-120">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="60569-120">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)