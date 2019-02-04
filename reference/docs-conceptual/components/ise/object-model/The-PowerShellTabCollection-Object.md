---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az PowerShellTabCollection objektum
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "55688734"
---
# <a name="the-powershelltabcollection-object"></a><span data-ttu-id="7baed-103">Az PowerShellTabCollection objektum</span><span class="sxs-lookup"><span data-stu-id="7baed-103">The PowerShellTabCollection Object</span></span>

<span data-ttu-id="7baed-104">A **PowerShellTab** objektum olyan gyűjteménye, **PowerShellTab** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="7baed-104">The **PowerShellTab** collection object is a collection of **PowerShellTab** objects.</span></span> <span data-ttu-id="7baed-105">Minden egyes **PowerShellTab** objektum egy önálló futtatókörnyezet funkcionál.</span><span class="sxs-lookup"><span data-stu-id="7baed-105">Each **PowerShellTab** object functions as a separate runtime environment.</span></span> <span data-ttu-id="7baed-106">Fontos Microsoft.PowerShell.Host.ISE.PowerShellTabs osztály egy példányát.</span><span class="sxs-lookup"><span data-stu-id="7baed-106">It is an instance of Microsoft.PowerShell.Host.ISE.PowerShellTabs class.</span></span> <span data-ttu-id="7baed-107">Például a **$psISE.PowerShellTabs** objektum.</span><span class="sxs-lookup"><span data-stu-id="7baed-107">An example is the **$psISE.PowerShellTabs** object.</span></span>

## <a name="methods"></a><span data-ttu-id="7baed-108">Metódusok</span><span class="sxs-lookup"><span data-stu-id="7baed-108">Methods</span></span>

### <a name="add"></a><span data-ttu-id="7baed-109">Hozzáadása\(\)</span><span class="sxs-lookup"><span data-stu-id="7baed-109">Add\(\)</span></span>

<span data-ttu-id="7baed-110">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7baed-110">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7baed-111">Új PowerShell-lap hozzáadása a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="7baed-111">Adds a new PowerShell tab to the collection.</span></span> <span data-ttu-id="7baed-112">Az újonnan hozzáadott lapon ad vissza.</span><span class="sxs-lookup"><span data-stu-id="7baed-112">It returns the newly added tab.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="7baed-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="7baed-113">Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="7baed-114">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7baed-114">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7baed-115">Eltávolítja a megadott lapot az **psTab** paraméter.</span><span class="sxs-lookup"><span data-stu-id="7baed-115">Removes the tab that is specified by the **psTab** parameter.</span></span>

<span data-ttu-id="7baed-116">**psTab** eltávolítása a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="7baed-116">**psTab** The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a><span data-ttu-id="7baed-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span><span class="sxs-lookup"><span data-stu-id="7baed-117">SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)</span></span>

<span data-ttu-id="7baed-118">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7baed-118">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7baed-119">A megadott PowerShell-lap kiválasztása a **psTab** paramétert, hogy a jelenleg aktív PowerShell-lap.</span><span class="sxs-lookup"><span data-stu-id="7baed-119">Selects the PowerShell tab that is specified by the **psTab** parameter to make it the currently active PowerShell tab.</span></span>

<span data-ttu-id="7baed-120">**psTab** a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="7baed-120">**psTab** The PowerShell tab to select.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="7baed-121">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7baed-121">See Also</span></span>

- [<span data-ttu-id="7baed-122">The PowerShellTab Object</span><span class="sxs-lookup"><span data-stu-id="7baed-122">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="7baed-123">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="7baed-123">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="7baed-124">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="7baed-124">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)