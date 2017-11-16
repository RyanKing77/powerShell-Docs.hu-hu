---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEAddOnToolCollection objektum
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ba8b4e0e3952226407f00dea8b32785633256089
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="8dea2-103">A ISEAddOnToolCollection objektum</span><span class="sxs-lookup"><span data-stu-id="8dea2-103">The ISEAddOnToolCollection Object</span></span>
  <span data-ttu-id="8dea2-104">A **ISEAddOnToolCollection** objektum gyűjteménye **ISEAddOnTool** objektumok.</span><span class="sxs-lookup"><span data-stu-id="8dea2-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="8dea2-105">Példa: a **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektum.</span><span class="sxs-lookup"><span data-stu-id="8dea2-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="8dea2-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="8dea2-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="8dea2-107">Adja hozzá\( nevét, ControlType, \[IsVisible\]\)</span><span class="sxs-lookup"><span data-stu-id="8dea2-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>
  <span data-ttu-id="8dea2-108">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="8dea2-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="8dea2-109">Egy új bővítménye, amellyel hozzáadja a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="8dea2-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="8dea2-110">Az újonnan hozzáadott bővítmény eszközt ad vissza.</span><span class="sxs-lookup"><span data-stu-id="8dea2-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="8dea2-111">Ez a parancs futtatása előtt telepítse a bővítmény eszközt a helyi számítógépen, és a szerelvény betöltése.</span><span class="sxs-lookup"><span data-stu-id="8dea2-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

 <span data-ttu-id="8dea2-112">**Név** -karakterláncot határozza meg a Windows PowerShell ISE hozzáadott bővítmény eszköz megjelenítési neve.</span><span class="sxs-lookup"><span data-stu-id="8dea2-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

 <span data-ttu-id="8dea2-113">**ControlType** – azt adja meg a hozzáadott vezérlő.</span><span class="sxs-lookup"><span data-stu-id="8dea2-113">**ControlType** -Type Specifies the control that is added.</span></span>

 <span data-ttu-id="8dea2-114">**\[IsVisible\]**  -választható logikai Ha **$true**, a bővítmény eszköz azonnal látható, a kapcsolódó eszköz panelen.</span><span class="sxs-lookup"><span data-stu-id="8dea2-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="8dea2-115">Távolítsa el\( elem\)</span><span class="sxs-lookup"><span data-stu-id="8dea2-115">Remove\( Item \)</span></span>
  <span data-ttu-id="8dea2-116">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="8dea2-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="8dea2-117">A megadott bővítmény eszköz eltávolítása a gyűjteményben.</span><span class="sxs-lookup"><span data-stu-id="8dea2-117">Removes the specified add-on tool from the collection.</span></span>

 <span data-ttu-id="8dea2-118">**Elem** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool eltávolítsa őket a Windows PowerShell ISE-objektumot adja meg.</span><span class="sxs-lookup"><span data-stu-id="8dea2-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="8dea2-119">SetSelectedPowerShellTab\( psTab\)</span><span class="sxs-lookup"><span data-stu-id="8dea2-119">SetSelectedPowerShellTab\( psTab \)</span></span>
  <span data-ttu-id="8dea2-120">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="8dea2-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="8dea2-121">Kiválasztja a PowerShell lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="8dea2-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

 <span data-ttu-id="8dea2-122">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="8dea2-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
      $newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

### <a name="remove-pstab-"></a><span data-ttu-id="8dea2-123">Távolítsa el\( psTab\)</span><span class="sxs-lookup"><span data-stu-id="8dea2-123">Remove\( psTab \)</span></span>
  <span data-ttu-id="8dea2-124">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="8dea2-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="8dea2-125">Eltávolítja a PowerShell lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="8dea2-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

 <span data-ttu-id="8dea2-126">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre, és távolítsa el.</span><span class="sxs-lookup"><span data-stu-id="8dea2-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="8dea2-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8dea2-127">See Also</span></span>
- [<span data-ttu-id="8dea2-128">A PowerShellTab objektum</span><span class="sxs-lookup"><span data-stu-id="8dea2-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md) 
- [<span data-ttu-id="8dea2-129">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="8dea2-129">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="8dea2-130">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="8dea2-130">Windows PowerShell ISE Object Model Reference</span></span>](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="8dea2-131">A ISE objektum modell hierarchia</span><span class="sxs-lookup"><span data-stu-id="8dea2-131">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)

  
