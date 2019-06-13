---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEAddOnToolCollection objektum
ms.openlocfilehash: 28ab9747e573b7a76ee655289b341870b1728bc2
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030626"
---
# <a name="the-iseaddontoolcollection-object"></a><span data-ttu-id="30a1f-103">Az ISEAddOnToolCollection objektum</span><span class="sxs-lookup"><span data-stu-id="30a1f-103">The ISEAddOnToolCollection Object</span></span>

<span data-ttu-id="30a1f-104">A **ISEAddOnToolCollection** objektum olyan gyűjteménye, **ISEAddOnTool** objektumokat.</span><span class="sxs-lookup"><span data-stu-id="30a1f-104">The **ISEAddOnToolCollection** object is a collection of **ISEAddOnTool** objects.</span></span> <span data-ttu-id="30a1f-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span><span class="sxs-lookup"><span data-stu-id="30a1f-105">An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.</span></span>

## <a name="methods"></a><span data-ttu-id="30a1f-106">Metódusok</span><span class="sxs-lookup"><span data-stu-id="30a1f-106">Methods</span></span>

### <a name="add-name-controltype-isvisible-"></a><span data-ttu-id="30a1f-107">Adjon hozzá\( nevét, ControlType, \[IsVisible\] \)</span><span class="sxs-lookup"><span data-stu-id="30a1f-107">Add\( Name, ControlType, \[IsVisible\] \)</span></span>

<span data-ttu-id="30a1f-108">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="30a1f-108">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="30a1f-109">Egy új bővítménye, amellyel hozzáadja a gyűjteményhez.</span><span class="sxs-lookup"><span data-stu-id="30a1f-109">Adds a new add-on tool to the collection.</span></span> <span data-ttu-id="30a1f-110">Az újonnan hozzáadott kiegészítő eszköz adja vissza.</span><span class="sxs-lookup"><span data-stu-id="30a1f-110">It returns the newly added add-on tool.</span></span> <span data-ttu-id="30a1f-111">A parancs futtatása előtt telepítse a bővítményt eszközt a helyi számítógépen, és a szerelvény betöltése.</span><span class="sxs-lookup"><span data-stu-id="30a1f-111">Before you run this command, you must install the add-on tool on the local computer and load the assembly.</span></span>

<span data-ttu-id="30a1f-112">**Név** -karakterláncot a bővítmény eszköz Windows PowerShell ISE-ben hozzáadott megjelenített nevét adja meg.</span><span class="sxs-lookup"><span data-stu-id="30a1f-112">**Name** - String Specifies the display name of the add-on tool that is added to Windows PowerShell ISE.</span></span>

<span data-ttu-id="30a1f-113">**ControlType** – azt adja meg a vezérlő, amely hozzá van adva.</span><span class="sxs-lookup"><span data-stu-id="30a1f-113">**ControlType** -Type Specifies the control that is added.</span></span>

<span data-ttu-id="30a1f-114">**\[IsVisible\]**  – nem kötelező logikai Ha **$true**, a bővítmény eszköz azonnal látható, a kapcsolódó eszköz panelen.</span><span class="sxs-lookup"><span data-stu-id="30a1f-114">**\[IsVisible\]** - optional Boolean If set to **$true**, the add-on tool is immediately visible in the associated tool pane.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a><span data-ttu-id="30a1f-115">Távolítsa el\( elem \)</span><span class="sxs-lookup"><span data-stu-id="30a1f-115">Remove\( Item \)</span></span>

<span data-ttu-id="30a1f-116">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="30a1f-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="30a1f-117">Eltávolítja a bővítmény megadott eszköz a gyűjteményből.</span><span class="sxs-lookup"><span data-stu-id="30a1f-117">Removes the specified add-on tool from the collection.</span></span>

<span data-ttu-id="30a1f-118">**Elem** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool meghatározza az objektum, melyet távolítható el a Windows PowerShell ISE-ben.</span><span class="sxs-lookup"><span data-stu-id="30a1f-118">**Item** - Microsoft.PowerShell.Host.ISE.ISEAddOnTool Specifies the object to be removed from Windows PowerShell ISE.</span></span>

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a><span data-ttu-id="30a1f-119">SetSelectedPowerShellTab\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="30a1f-119">SetSelectedPowerShellTab\( psTab \)</span></span>

<span data-ttu-id="30a1f-120">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="30a1f-120">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="30a1f-121">Kiválasztja a PowerShell-lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="30a1f-121">Selects the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="30a1f-122">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre kattintva válassza ki.</span><span class="sxs-lookup"><span data-stu-id="30a1f-122">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to select.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a><span data-ttu-id="30a1f-123">Távolítsa el\( psTab \)</span><span class="sxs-lookup"><span data-stu-id="30a1f-123">Remove\( psTab \)</span></span>

<span data-ttu-id="30a1f-124">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="30a1f-124">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="30a1f-125">Eltávolítja a PowerShell lap, amely a **psTab** paraméter határozza meg.</span><span class="sxs-lookup"><span data-stu-id="30a1f-125">Removes the PowerShell tab that the **psTab** parameter specifies.</span></span>

<span data-ttu-id="30a1f-126">**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell-lap eltávolítása.</span><span class="sxs-lookup"><span data-stu-id="30a1f-126">**psTab** - Microsoft.PowerShell.Host.ISE.PowerShellTab The PowerShell tab to remove.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a><span data-ttu-id="30a1f-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="30a1f-127">See Also</span></span>

- [<span data-ttu-id="30a1f-128">The PowerShellTab Object</span><span class="sxs-lookup"><span data-stu-id="30a1f-128">The PowerShellTab Object</span></span>](The-PowerShellTab-Object.md)
- [<span data-ttu-id="30a1f-129">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="30a1f-129">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="30a1f-130">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="30a1f-130">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)
