---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEAddOnToolCollection objektum
ms.assetid: 634eab89-0845-4016-974b-361b09bb8f7b
ms.openlocfilehash: ff4f19d1a85a592f2f4f09c62caa0971751bdff7
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404468"
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="64dad-103">Az ISEAddOnToolCollection objektum</span><span class="sxs-lookup"><span data-stu-id="64dad-103">The ISEAddOnToolCollection Object</span></span>

<span data-ttu-id="64dad-104">A **ISEAddOnToolCollection** objektum olyan gyűjteménye, **ISEAddOnTool** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="64dad-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="64dad-105">Például a **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektum.</span><span class="sxs-lookup"><span data-stu-id="64dad-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="64dad-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="64dad-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="64dad-107">Adjon hozzá\( nevét, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="64dad-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>

<span data-ttu-id="64dad-108">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="64dad-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="64dad-109">Egy új bővítménye, amellyel hozzáadja a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="64dad-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="64dad-110">Az újonnan hozzáadott kiegészítő eszköz adja vissza.</span><span class="sxs-lookup"><span data-stu-id="64dad-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="64dad-111">A parancs futtatása előtt telepítse a bővítményt eszközt a helyi számítógépen, és a szerelvény betöltése.</span><span class="sxs-lookup"><span data-stu-id="64dad-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

<span data-ttu-id="64dad-112">**Név** -karakterláncot a bővítmény eszköz Windows PowerShell ISE-ben hozzáadott megjelenített nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="64dad-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

<span data-ttu-id="64dad-113">**ControlType** – azt adja meg a vezérlő, amely hozzá van adva.</span><span class="sxs-lookup"><span data-stu-id="64dad-113">**ControlType** -Type Specifies the control that is added.</span></span>

<span data-ttu-id="64dad-114">**\[IsVisible\]**  – nem kötelező logikai Ha **$true**, a bővítmény eszköz azonnal látható, a kapcsolódó eszköz panelen.</span><span class="sxs-lookup"><span data-stu-id="64dad-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="64dad-115">Távolítsa el\( elem \)</span><span class="sxs-lookup"><span data-stu-id="64dad-115">Remove\( Item \)</span></span>

<span data-ttu-id="64dad-116">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="64dad-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="64dad-117">Eltávolítja a bővítmény megadott eszköz a gyűjteményből.</span><span class="sxs-lookup"><span data-stu-id="64dad-117">Removes the specified add-on tool from the collection.</span></span>

<span data-ttu-id="64dad-118">**Elem** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool meghatározza az objektum, melyet távolítható el a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="64dad-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="64dad-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="64dad-119">SetSelectedPowerShellTab\( psTab \)</span></span>

<span data-ttu-id="64dad-120">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="64dad-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="64dad-121">Kiválasztja a PowerShell-lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="64dad-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="64dad-122">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="64dad-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a><span data-ttu-id="64dad-123">Távolítsa el\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="64dad-123">Remove\( psTab \)</span></span>

<span data-ttu-id="64dad-124">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="64dad-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="64dad-125">Eltávolítja a PowerShell lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="64dad-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="64dad-126">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell-lap eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="64dad-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="64dad-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="64dad-127">See Also</span></span>

- [<span data-ttu-id="64dad-128">Az PowerShellTab objektum</span><span class="sxs-lookup"><span data-stu-id="64dad-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="64dad-129">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="64dad-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="64dad-130">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="64dad-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)