---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A PowerShellTabCollection objektum
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: dcdc16ae126453b6ade64917ac4950cc05e5f8ad
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="b7868-103">A PowerShellTabCollection objektum</span><span class="sxs-lookup"><span data-stu-id="b7868-103">The PowerShellTabCollection Object</span></span>
  <span data-ttu-id="b7868-104">A **PowerShellTab** gyűjteményobjektumot gyűjteménye **PowerShellTab** objektumok.</span><span class="sxs-lookup"><span data-stu-id="b7868-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="b7868-105">Minden egyes **PowerShellTab** objektum funkciókkal, mint egy külön futtatókörnyezetben.</span><span class="sxs-lookup"><span data-stu-id="b7868-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="b7868-106">Microsoft.PowerShell.Host.ISE.PowerShellTabs osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="b7868-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="b7868-107">Példa: a **$psISE.PowerShellTabs** objektum.</span><span class="sxs-lookup"><span data-stu-id="b7868-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="b7868-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="b7868-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="b7868-109">Hozzáadása\(\)</span><span class="sxs-lookup"><span data-stu-id="b7868-109">Add\(\)</span></span>
  <span data-ttu-id="b7868-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="b7868-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="b7868-111">Új PowerShell lap hozzáadása a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="b7868-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="b7868-112">Az újonnan hozzáadott lapon adja vissza.</span><span class="sxs-lookup"><span data-stu-id="b7868-112">It returns the newly added tab.</span></span>

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="b7868-113">Távolítsa el\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="b7868-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>
  <span data-ttu-id="b7868-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="b7868-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="b7868-115">Eltávolítja a megadott lapot a **psTab** paraméter.</span><span class="sxs-lookup"><span data-stu-id="b7868-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

 <span data-ttu-id="b7868-116">**psTab** távolítsa el a PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="b7868-116">**psTab** The PowerShell tab to remove.</span></span>

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="b7868-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="b7868-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>
  <span data-ttu-id="b7868-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="b7868-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="b7868-119">A PowerShell lapon megadott kiválasztja a **psTab** paraméter abba, hogy a jelenleg aktív PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="b7868-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

 <span data-ttu-id="b7868-120">**psTab** a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="b7868-120">**psTab** The PowerShell tab to select.</span></span>

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## <a name="see-also"></a><span data-ttu-id="b7868-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b7868-121">See Also</span></span>
- [<span data-ttu-id="b7868-122">A PowerShellTab objektum</span><span class="sxs-lookup"><span data-stu-id="b7868-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="b7868-123">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="b7868-123">The Windows PowerShell ISE Scripting Object Model</span></span>](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="b7868-124">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="b7868-124">Windows PowerShell ISE Object Model Reference</span></span>](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="b7868-125">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="b7868-125">The ISE Object Model Hierarchy</span></span>](../ise/The-ISE-Object-Model-Hierarchy.md)

  
