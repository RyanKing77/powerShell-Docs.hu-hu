---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az PowerShellTab objektum
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: c10f9106e31bb05828f1e76554ebe40ddb778340
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
---
# <a name="the-powershelltab-object"></a><span data-ttu-id="9e88a-103">Az PowerShellTab objektum</span><span class="sxs-lookup"><span data-stu-id="9e88a-103">The PowerShellTab Object</span></span>

<span data-ttu-id="9e88a-104">A **PowerShellTab** objektum által jelképezett egy Windows PowerShell futtatókörnyezetben.</span><span class="sxs-lookup"><span data-stu-id="9e88a-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="9e88a-105">Metódusok</span><span class="sxs-lookup"><span data-stu-id="9e88a-105">Methods</span></span>

### <a name="invoke-script-"></a><span data-ttu-id="9e88a-106">Invoke\( parancsfájl \)</span><span class="sxs-lookup"><span data-stu-id="9e88a-106">Invoke\( Script \)</span></span>

<span data-ttu-id="9e88a-107">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-108">A megadott parancsfájlt futtatja a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="9e88a-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="9e88a-109">Ez a módszer csak akkor működik a többi PowerShell lap nem a PowerShell fülre, amelyből futtatni.</span><span class="sxs-lookup"><span data-stu-id="9e88a-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="9e88a-110">Nem ad vissza semmilyen objektum vagy -érték.</span><span class="sxs-lookup"><span data-stu-id="9e88a-110">It does not return any object or value.</span></span> <span data-ttu-id="9e88a-111">Ha a kód bármely változó módosítja, akkor ezeket a módosításokat továbbra is fennáll, a lapon, amely a parancs lett meghívva.</span><span class="sxs-lookup"><span data-stu-id="9e88a-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

<span data-ttu-id="9e88a-112">**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatásához a script blokkból.</span><span class="sxs-lookup"><span data-stu-id="9e88a-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="9e88a-113">InvokeSynchronous\( parancsfájl, \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="9e88a-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>

<span data-ttu-id="9e88a-114">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="9e88a-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="9e88a-115">A megadott parancsfájlt futtatja a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="9e88a-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="9e88a-116">Ez a módszer csak akkor működik a többi PowerShell lap nem a PowerShell fülre, amelyből futtatni.</span><span class="sxs-lookup"><span data-stu-id="9e88a-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="9e88a-117">A parancsprogram-blokkot tartalmazzon fut, és, hogy a parancsfájl által visszaadott értéket ad vissza, amelyből a parancs meghívása a futtatási környezetet.</span><span class="sxs-lookup"><span data-stu-id="9e88a-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="9e88a-118">Ha a parancs futtatásához, mint hosszabb időbe telik a **millesecondsTimeout** az érték határozza meg, akkor a parancs futása sikertelen, kivétel miatt: "a művelet túllépte az időkorlátot."</span><span class="sxs-lookup"><span data-stu-id="9e88a-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

<span data-ttu-id="9e88a-119">**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatásához a script blokkból.</span><span class="sxs-lookup"><span data-stu-id="9e88a-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

<span data-ttu-id="9e88a-120">**\[useNewScope\]**  -választható logikai, amely alapértelmezés szerint az **$true** Ha beállítása **$true**, majd az új hatókör jön létre a parancs futtatásához.</span><span class="sxs-lookup"><span data-stu-id="9e88a-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true** If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="9e88a-121">A művelet nem módosítja a futtatási környezetet a PowerShell lap, a parancs által megadott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

<span data-ttu-id="9e88a-122">**\[millisecondsTimeout\]**  -választható egész szám, amely alapértelmezés szerint az **500**.</span><span class="sxs-lookup"><span data-stu-id="9e88a-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="9e88a-123">Ha a parancs nem fejeződik be a megadott időn belül, akkor a parancs létrehoz egy **TimeoutException** üzenettel "a művelet túllépte az időkorlátot."</span><span class="sxs-lookup"><span data-stu-id="9e88a-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

```powershell
# Create a new PowerShell tab and then switch back to the first
$psISE.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0])

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1', $false)
# You can switch to the other tab and type '$x' to see that the value is saved there.

# This example sets a value in the other tab (in a different scope)
# and returns it through the pipeline to this tab to store in $a
$a = $psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z')
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
Measure-Command {$psISE.PowerShellTabs[1].InvokeSynchronous('sleep 10', $false, 5000)}
```

## <a name="properties"></a><span data-ttu-id="9e88a-124">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="9e88a-124">Properties</span></span>

### <a name="addonsmenu"></a><span data-ttu-id="9e88a-125">AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="9e88a-125">AddOnsMenu</span></span>

<span data-ttu-id="9e88a-126">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-127">A csak olvasható tulajdonság, amely a bővítmények menü beolvassa a PowerShell fülre.</span><span class="sxs-lookup"><span data-stu-id="9e88a-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

```powershell
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('_Process', {Get-Process}, 'Alt+P')
# Add a nested menu.
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add('Parent', $null, $null)
$parentAdded.SubMenus.Add('_Dir', {dir}, 'Alt+D')
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

### <a name="caninvoke"></a><span data-ttu-id="9e88a-128">CanInvoke</span><span class="sxs-lookup"><span data-stu-id="9e88a-128">CanInvoke</span></span>

<span data-ttu-id="9e88a-129">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-130">A csak olvasható logikai tulajdonsággal adja vissza egy **$true** értéket, ha egy parancsfájl indítható a [Invoke (parancsfájl)](#invoke-script-) metódust.</span><span class="sxs-lookup"><span data-stu-id="9e88a-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke-script-) method.</span></span>

```powershell
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab.
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psISE.PowerShellTabs[1]
$secondTab.CanInvoke
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke
```

### <a name="consolepane"></a><span data-ttu-id="9e88a-131">Consolepane</span><span class="sxs-lookup"><span data-stu-id="9e88a-131">Consolepane</span></span>

<span data-ttu-id="9e88a-132">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="9e88a-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="9e88a-133">A Windows PowerShell ISE 2.0 Ez nevű **CommandPane**.</span><span class="sxs-lookup"><span data-stu-id="9e88a-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

<span data-ttu-id="9e88a-134">A csak olvasható tulajdonság, amely lekérdezi a konzol ablaktáblában [szerkesztő](../ise/The-ISEEditor-Object.md) objektum.</span><span class="sxs-lookup"><span data-stu-id="9e88a-134">The read-only property that gets the Console pane [editor](../ise/The-ISEEditor-Object.md) object.</span></span>

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a><span data-ttu-id="9e88a-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="9e88a-135">DisplayName</span></span>

<span data-ttu-id="9e88a-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-137">Az írható-olvasható tulajdonság, amely lekérdezi vagy beállítja a szöveg, amelyet a PowerShell lapon jelenik meg. Alapértelmezés szerint lapfülek neve "PowerShell #", ahol a # számot jelöl.</span><span class="sxs-lookup"><span data-stu-id="9e88a-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab. By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a><span data-ttu-id="9e88a-138">ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="9e88a-138">ExpandedScript</span></span>

<span data-ttu-id="9e88a-139">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-139">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-140">Az olvasási és írási logikai tulajdonság, amely meghatározza, hogy a parancssori panelbe kibontva vagy rejtett.</span><span class="sxs-lookup"><span data-stu-id="9e88a-140">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a><span data-ttu-id="9e88a-141">Fájlok</span><span class="sxs-lookup"><span data-stu-id="9e88a-141">Files</span></span>

<span data-ttu-id="9e88a-142">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-142">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-143">A csak olvasható tulajdonság, amely lekérdezi a [parancsfájl fájlok](../ise/The-ISEFileCollection-Object.md) , amelyek nyissa meg a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="9e88a-143">The read-only property that gets the [collection of script files](../ise/The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a><span data-ttu-id="9e88a-144">Kimenet</span><span class="sxs-lookup"><span data-stu-id="9e88a-144">Output</span></span>

<span data-ttu-id="9e88a-145">Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="9e88a-145">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="9e88a-146">A Windows PowerShell ISE újabb verzióit, használhatja a **ConsolePane** célból objektum.</span><span class="sxs-lookup"><span data-stu-id="9e88a-146">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

<span data-ttu-id="9e88a-147">A csak olvasható tulajdonság, amely lekérdezi a Tesztkimenet ablaktáblán, az aktuális [szerkesztő](../ise/The-ISEEditor-Object.md).</span><span class="sxs-lookup"><span data-stu-id="9e88a-147">The read-only property that gets the Output pane of the current [editor](../ise/The-ISEEditor-Object.md).</span></span>

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a><span data-ttu-id="9e88a-148">parancssor</span><span class="sxs-lookup"><span data-stu-id="9e88a-148">Prompt</span></span>

<span data-ttu-id="9e88a-149">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-149">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-150">A csak olvasható tulajdonság, amely lekérdezi az aktuális adatkérés szövegét.</span><span class="sxs-lookup"><span data-stu-id="9e88a-150">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="9e88a-151">Megjegyzés: a **Rákérdezés** függvény felülbírálhatja a felhasználó "™ s profil.</span><span class="sxs-lookup"><span data-stu-id="9e88a-151">Note: the **Prompt** function can be overridden by the user'™s profile.</span></span> <span data-ttu-id="9e88a-152">Ha az eredmény egy egyszerű karakterlánc, majd a tulajdonság adja vissza semmi sem.</span><span class="sxs-lookup"><span data-stu-id="9e88a-152">If the result is other than a simple string, then this property returns nothing.</span></span>

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a><span data-ttu-id="9e88a-153">ShowCommands</span><span class="sxs-lookup"><span data-stu-id="9e88a-153">ShowCommands</span></span>

<span data-ttu-id="9e88a-154">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="9e88a-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="9e88a-155">Az írható-olvasható tulajdonság, amely jelzi, ha a parancsok panelt jelenleg jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="9e88a-155">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a><span data-ttu-id="9e88a-156">StatusText</span><span class="sxs-lookup"><span data-stu-id="9e88a-156">StatusText</span></span>

<span data-ttu-id="9e88a-157">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-157">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="9e88a-158">A csak olvasható tulajdonság, amely lekérdezi a **PowerShellTab** állapotleíró szöveg.</span><span class="sxs-lookup"><span data-stu-id="9e88a-158">The read-only property that gets the **PowerShellTab** status text.</span></span>

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a><span data-ttu-id="9e88a-159">HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="9e88a-159">HorizontalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="9e88a-160">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="9e88a-160">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="9e88a-161">A csak olvasható tulajdonság, amely azt jelzi, hogy a vízszintes bővítmények eszközpanelt megnyitott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-161">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a><span data-ttu-id="9e88a-162">VerticalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="9e88a-162">VerticalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="9e88a-163">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="9e88a-163">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="9e88a-164">A csak olvasható tulajdonság, amely azt jelzi, hogy a bővítmények függőleges eszközpanelt megnyitott.</span><span class="sxs-lookup"><span data-stu-id="9e88a-164">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="9e88a-165">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9e88a-165">See Also</span></span>

- [<span data-ttu-id="9e88a-166">A PowerShellTabCollection objektum</span><span class="sxs-lookup"><span data-stu-id="9e88a-166">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md)
- [<span data-ttu-id="9e88a-167">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="9e88a-167">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="9e88a-168">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="9e88a-168">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)