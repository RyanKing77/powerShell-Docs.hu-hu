---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEAddOnToolCollection objektum
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953055"
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="abc62-103">Az ISEAddOnToolCollection objektum</span><span class="sxs-lookup"><span data-stu-id="abc62-103">The ISEAddOnToolCollection Object</span></span>

<span data-ttu-id="abc62-104">A **ISEAddOnToolCollection** objektum gyűjteménye **ISEAddOnTool** objektumok.</span><span class="sxs-lookup"><span data-stu-id="abc62-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="abc62-105">Példa: a **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektum.</span><span class="sxs-lookup"><span data-stu-id="abc62-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="abc62-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="abc62-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="abc62-107">Adja hozzá\( nevét, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="abc62-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>

<span data-ttu-id="abc62-108">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="abc62-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="abc62-109">Egy új bővítménye, amellyel hozzáadja a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="abc62-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="abc62-110">Az újonnan hozzáadott bővítmény eszközt ad vissza.</span><span class="sxs-lookup"><span data-stu-id="abc62-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="abc62-111">Ez a parancs futtatása előtt telepítse a bővítmény eszközt a helyi számítógépen, és a szerelvény betöltése.</span><span class="sxs-lookup"><span data-stu-id="abc62-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

<span data-ttu-id="abc62-112">**Név** -karakterláncot határozza meg a Windows PowerShell ISE hozzáadott bővítmény eszköz megjelenítési neve.</span><span class="sxs-lookup"><span data-stu-id="abc62-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

<span data-ttu-id="abc62-113">**ControlType** – azt adja meg a hozzáadott vezérlő.</span><span class="sxs-lookup"><span data-stu-id="abc62-113">**ControlType** -Type Specifies the control that is added.</span></span>

<span data-ttu-id="abc62-114">**\[IsVisible\]**  -választható logikai Ha **$true**, a bővítmény eszköz azonnal látható, a kapcsolódó eszköz panelen.</span><span class="sxs-lookup"><span data-stu-id="abc62-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="abc62-115">Távolítsa el\( elem \)</span><span class="sxs-lookup"><span data-stu-id="abc62-115">Remove\( Item \)</span></span>

<span data-ttu-id="abc62-116">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="abc62-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="abc62-117">A megadott bővítmény eszköz eltávolítása a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="abc62-117">Removes the specified add-on tool from the collection.</span></span>

<span data-ttu-id="abc62-118">**Elem** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool eltávolítsa őket a Windows PowerShell ISE-objektumot adja meg.</span><span class="sxs-lookup"><span data-stu-id="abc62-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="abc62-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="abc62-119">SetSelectedPowerShellTab\( psTab \)</span></span>

<span data-ttu-id="abc62-120">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="abc62-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="abc62-121">Kiválasztja a PowerShell lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="abc62-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="abc62-122">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="abc62-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a><span data-ttu-id="abc62-123">Távolítsa el\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="abc62-123">Remove\( psTab \)</span></span>

<span data-ttu-id="abc62-124">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="abc62-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="abc62-125">Eltávolítja a PowerShell lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="abc62-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="abc62-126">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre, és távolítsa el.</span><span class="sxs-lookup"><span data-stu-id="abc62-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="abc62-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="abc62-127">See Also</span></span>

- [<span data-ttu-id="abc62-128">The PowerShellTab Object</span><span class="sxs-lookup"><span data-stu-id="abc62-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="abc62-129">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="abc62-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="abc62-130">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="abc62-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)