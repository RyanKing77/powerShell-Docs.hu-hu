---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az PowerShellTab objektum
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: 577e2aaaddf3071801816d9ae91dbf0006dd5072
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62057672"
---
# <a name="the-powershelltab-object"></a><span data-ttu-id="7e03d-103">Az PowerShellTab objektum</span><span class="sxs-lookup"><span data-stu-id="7e03d-103">The PowerShellTab Object</span></span>

<span data-ttu-id="7e03d-104">A **PowerShellTab** objektum képviseli egy Windows PowerShell-modul környezetben.</span><span class="sxs-lookup"><span data-stu-id="7e03d-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="7e03d-105">Módszerek</span><span class="sxs-lookup"><span data-stu-id="7e03d-105">Methods</span></span>

### <a name="invoke-script-"></a><span data-ttu-id="7e03d-106">Meghívása\( parancsfájl \)</span><span class="sxs-lookup"><span data-stu-id="7e03d-106">Invoke\( Script \)</span></span>

<span data-ttu-id="7e03d-107">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-108">A megadott parancsfájlt futtatja a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="7e03d-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="7e03d-109">Ez a módszer csak használható többi PowerShell-lap nem a PowerShell lap, amelyből futtatni.</span><span class="sxs-lookup"><span data-stu-id="7e03d-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="7e03d-110">Nem ad vissza minden olyan objektumot, vagy értéket.</span><span class="sxs-lookup"><span data-stu-id="7e03d-110">It does not return any object or value.</span></span> <span data-ttu-id="7e03d-111">Ha a kód módosítja bármely változó, majd ezeket a módosításokat továbbra is fennáll, amelyre vonatkozóan a parancs meghívása lapján.</span><span class="sxs-lookup"><span data-stu-id="7e03d-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

<span data-ttu-id="7e03d-112">**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatandó a parancsfájlblokkban.</span><span class="sxs-lookup"><span data-stu-id="7e03d-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="7e03d-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="7e03d-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>

<span data-ttu-id="7e03d-114">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="7e03d-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7e03d-115">A megadott parancsfájlt futtatja a PowerShell-lapon.</span><span class="sxs-lookup"><span data-stu-id="7e03d-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
> <span data-ttu-id="7e03d-116">Ez a módszer csak használható többi PowerShell-lap nem a PowerShell lap, amelyből futtatni.</span><span class="sxs-lookup"><span data-stu-id="7e03d-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="7e03d-117">A parancsprogram-blokkot fut, és, hogy a parancsfájl által visszaadott értéket adja vissza, amelyről a parancs meghívása a futtatási környezetet.</span><span class="sxs-lookup"><span data-stu-id="7e03d-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="7e03d-118">Ha a parancs több időt vesz igénybe, mint a **millesecondsTimeout** az érték határozza meg, akkor a parancs futása sikertelen, egy kivétellel: "A művelet túllépte az időkorlátot."</span><span class="sxs-lookup"><span data-stu-id="7e03d-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

<span data-ttu-id="7e03d-119">**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatandó a parancsfájlblokkban.</span><span class="sxs-lookup"><span data-stu-id="7e03d-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

<span data-ttu-id="7e03d-120">**\[useNewScope\]**  -választható logikai alapértelmezés szerint **$true** Ha beállítása **$true**, majd az új hatókör létrehozása belül, amely a parancs futtatásához.</span><span class="sxs-lookup"><span data-stu-id="7e03d-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true** If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="7e03d-121">Nem módosítja a futtatási környezetet a PowerShell-lap, a parancs által megadott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

<span data-ttu-id="7e03d-122">**\[millisecondsTimeout\]**  – nem kötelező egész szám, amely alapértelmezés szerint a **500**.</span><span class="sxs-lookup"><span data-stu-id="7e03d-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="7e03d-123">Ha a parancs nem fejeződik be a meghatározott időn belül, akkor a parancs létrehoz egy **TimeoutException** üzenettel "a művelet túllépte az időkorlátot."</span><span class="sxs-lookup"><span data-stu-id="7e03d-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

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

## <a name="properties"></a><span data-ttu-id="7e03d-124">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="7e03d-124">Properties</span></span>

### <a name="addonsmenu"></a><span data-ttu-id="7e03d-125">AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="7e03d-125">AddOnsMenu</span></span>

<span data-ttu-id="7e03d-126">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-127">A csak olvasható tulajdonság, amely lekérdezi a bővítmények menü a PowerShell-lap.</span><span class="sxs-lookup"><span data-stu-id="7e03d-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

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

### <a name="caninvoke"></a><span data-ttu-id="7e03d-128">CanInvoke</span><span class="sxs-lookup"><span data-stu-id="7e03d-128">CanInvoke</span></span>

<span data-ttu-id="7e03d-129">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-130">A csak olvasható logikai tulajdonság, amely visszaadja a **$true** értékét, ha a parancsfájl indítható a [Invoke (szkript)](#invoke-script-) metódus.</span><span class="sxs-lookup"><span data-stu-id="7e03d-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke-script-) method.</span></span>

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

### <a name="consolepane"></a><span data-ttu-id="7e03d-131">Consolepane</span><span class="sxs-lookup"><span data-stu-id="7e03d-131">Consolepane</span></span>

<span data-ttu-id="7e03d-132">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="7e03d-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="7e03d-133">A Windows PowerShell ISE 2.0 Ez nevű **CommandPane**.</span><span class="sxs-lookup"><span data-stu-id="7e03d-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

<span data-ttu-id="7e03d-134">A csak olvasható tulajdonság, amely lekérdezi a konzol ablaktáblában [szerkesztő](The-ISEEditor-Object.md) objektum.</span><span class="sxs-lookup"><span data-stu-id="7e03d-134">The read-only property that gets the Console pane [editor](The-ISEEditor-Object.md) object.</span></span>

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a><span data-ttu-id="7e03d-135">DisplayName</span><span class="sxs-lookup"><span data-stu-id="7e03d-135">DisplayName</span></span>

<span data-ttu-id="7e03d-136">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-137">Lekérdezi vagy beállítja a szöveg, amely az olvasási és írási tulajdonság a PowerShell-lap jelenik meg. Lap neve alapértelmezés szerint "PowerShell #", ahol a # számot jelöl.</span><span class="sxs-lookup"><span data-stu-id="7e03d-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab. By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a><span data-ttu-id="7e03d-138">ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="7e03d-138">ExpandedScript</span></span>

<span data-ttu-id="7e03d-139">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-139">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-140">Az olvasási és írási logikai tulajdonság, amely meghatározza, hogy a parancsfájl panelen megjelenített vagy rejtett.</span><span class="sxs-lookup"><span data-stu-id="7e03d-140">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a><span data-ttu-id="7e03d-141">Fájlok</span><span class="sxs-lookup"><span data-stu-id="7e03d-141">Files</span></span>

<span data-ttu-id="7e03d-142">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-142">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-143">A csak olvasható tulajdonság, amely lekérdezi a [parancsfájlok gyűjteményét](The-ISEFileCollection-Object.md) , amelyek a PowerShell-lap megnyitása.</span><span class="sxs-lookup"><span data-stu-id="7e03d-143">The read-only property that gets the [collection of script files](The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a><span data-ttu-id="7e03d-144">Kimenet</span><span class="sxs-lookup"><span data-stu-id="7e03d-144">Output</span></span>

<span data-ttu-id="7e03d-145">Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.</span><span class="sxs-lookup"><span data-stu-id="7e03d-145">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="7e03d-146">A Windows PowerShell ISE-ben újabb verziói esetén használhatja a **ConsolePane** objektum ugyanarra a célra.</span><span class="sxs-lookup"><span data-stu-id="7e03d-146">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

<span data-ttu-id="7e03d-147">A csak olvasható tulajdonság, amely lekérdezi a Tesztkimenet ablaktáblán, az aktuális [szerkesztő](The-ISEEditor-Object.md).</span><span class="sxs-lookup"><span data-stu-id="7e03d-147">The read-only property that gets the Output pane of the current [editor](The-ISEEditor-Object.md).</span></span>

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a><span data-ttu-id="7e03d-148">Kérdés</span><span class="sxs-lookup"><span data-stu-id="7e03d-148">Prompt</span></span>

<span data-ttu-id="7e03d-149">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-149">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-150">A csak olvasható tulajdonság, amely lekérdezi az aktuális adatkérési szöveget.</span><span class="sxs-lookup"><span data-stu-id="7e03d-150">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="7e03d-151">Megjegyzés: a **Rákérdezés** függvény a felhasználó felülbírálhatja "™ s profil.</span><span class="sxs-lookup"><span data-stu-id="7e03d-151">Note: the **Prompt** function can be overridden by the user'™s profile.</span></span> <span data-ttu-id="7e03d-152">Ha az eredmény nem eltérő egy egyszerű karakterláncot, majd ezt a tulajdonságot függvény semmi.</span><span class="sxs-lookup"><span data-stu-id="7e03d-152">If the result is other than a simple string, then this property returns nothing.</span></span>

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a><span data-ttu-id="7e03d-153">ShowCommands</span><span class="sxs-lookup"><span data-stu-id="7e03d-153">ShowCommands</span></span>

<span data-ttu-id="7e03d-154">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="7e03d-154">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7e03d-155">Az olvasási és írási tulajdonság, amely azt jelzi, ha a parancsok ablaktáblán látható.</span><span class="sxs-lookup"><span data-stu-id="7e03d-155">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a><span data-ttu-id="7e03d-156">StatusText</span><span class="sxs-lookup"><span data-stu-id="7e03d-156">StatusText</span></span>

<span data-ttu-id="7e03d-157">A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-157">Supported in Windows PowerShell ISE 2.0 and later.</span></span>

<span data-ttu-id="7e03d-158">A csak olvasható tulajdonság, amely lekérdezi a **PowerShellTab** Állapotszöveg részén.</span><span class="sxs-lookup"><span data-stu-id="7e03d-158">The read-only property that gets the **PowerShellTab** status text.</span></span>

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a><span data-ttu-id="7e03d-159">HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="7e03d-159">HorizontalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="7e03d-160">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="7e03d-160">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7e03d-161">A csak olvasható tulajdonság, amely azt jelzi, hogy a vízszintes bővítmények eszköz panel megnyitott.</span><span class="sxs-lookup"><span data-stu-id="7e03d-161">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a><span data-ttu-id="7e03d-162">VerticalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="7e03d-162">VerticalAddOnToolsPaneOpened</span></span>

<span data-ttu-id="7e03d-163">Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="7e03d-163">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="7e03d-164">A csak olvasható tulajdonság, amely azt jelzi, hogy nyitva-e a függőleges bővítmények eszköz panel.</span><span class="sxs-lookup"><span data-stu-id="7e03d-164">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="7e03d-165">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7e03d-165">See Also</span></span>

- [<span data-ttu-id="7e03d-166">Az PowerShellTabCollection objektum</span><span class="sxs-lookup"><span data-stu-id="7e03d-166">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md)
- [<span data-ttu-id="7e03d-167">A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja</span><span class="sxs-lookup"><span data-stu-id="7e03d-167">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="7e03d-168">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="7e03d-168">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)