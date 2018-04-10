---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az PowerShellTabCollection objektum
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="2ffd0-103">Az PowerShellTabCollection objektum</span><span class="sxs-lookup"><span data-stu-id="2ffd0-103">The PowerShellTabCollection Object</span></span>

<span data-ttu-id="2ffd0-104">A **PowerShellTab** gyűjteményobjektumot gyűjteménye **PowerShellTab** objektumok.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="2ffd0-105">Minden egyes **PowerShellTab** objektum funkciókkal, mint egy külön futtatókörnyezetben.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="2ffd0-106">Microsoft.PowerShell.Host.ISE.PowerShellTabs osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="2ffd0-107">Példa: a **$psISE.PowerShellTabs** objektum.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="2ffd0-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="2ffd0-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="2ffd0-109">Add\(\)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-109">Add\(\)</span></span>

<span data-ttu-id="2ffd0-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="2ffd0-111">Új PowerShell lap hozzáadása a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="2ffd0-112">Az újonnan hozzáadott lapon adja vissza.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-112">It returns the newly added tab.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="2ffd0-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="2ffd0-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="2ffd0-115">Eltávolítja a megadott lapot a **psTab** paraméter.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

<span data-ttu-id="2ffd0-116">**psTab** távolítsa el a PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-116">**psTab** The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="2ffd0-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="2ffd0-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="2ffd0-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="2ffd0-119">A PowerShell lapon megadott kiválasztja a **psTab** paraméter abba, hogy a jelenleg aktív PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

<span data-ttu-id="2ffd0-120">**psTab** a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="2ffd0-120">**psTab** The PowerShell tab to select.</span></span>

```powershell
# Save the current tab in a variable and rename it
$oldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName = 'Old Tab'
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab = $oldTab
```

## <a name="see-also"></a><span data-ttu-id="2ffd0-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2ffd0-121">See Also</span></span>

- [<span data-ttu-id="2ffd0-122">The PowerShellTab Object</span><span class="sxs-lookup"><span data-stu-id="2ffd0-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="2ffd0-123">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="2ffd0-123">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="2ffd0-124">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="2ffd0-124">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)