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
# <a name="the-powershelltab-object"></a>Az PowerShellTab objektum

A **PowerShellTab** objektum által jelképezett egy Windows PowerShell futtatókörnyezetben.

## <a name="methods"></a>Metódusok

### <a name="invoke-script-"></a>Invoke\( parancsfájl \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A megadott parancsfájlt futtatja a PowerShell-lapon.

> [!NOTE]
> Ez a módszer csak akkor működik a többi PowerShell lap nem a PowerShell fülre, amelyből futtatni. Nem ad vissza semmilyen objektum vagy -érték. Ha a kód bármely változó módosítja, akkor ezeket a módosításokat továbbra is fennáll, a lapon, amely a parancs lett meghívva.

**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatásához a script blokkból.

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a>InvokeSynchronous\( parancsfájl, \[useNewScope\], millisecondsTimeout \)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A megadott parancsfájlt futtatja a PowerShell-lapon.

> [!NOTE]
> Ez a módszer csak akkor működik a többi PowerShell lap nem a PowerShell fülre, amelyből futtatni. A parancsprogram-blokkot tartalmazzon fut, és, hogy a parancsfájl által visszaadott értéket ad vissza, amelyből a parancs meghívása a futtatási környezetet. Ha a parancs futtatásához, mint hosszabb időbe telik a **millesecondsTimeout** az érték határozza meg, akkor a parancs futása sikertelen, kivétel miatt: "a művelet túllépte az időkorlátot."

**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatásához a script blokkból.

**\[useNewScope\]**  -választható logikai, amely alapértelmezés szerint az **$true** Ha beállítása **$true**, majd az új hatókör jön létre a parancs futtatásához. A művelet nem módosítja a futtatási környezetet a PowerShell lap, a parancs által megadott.

**\[millisecondsTimeout\]**  -választható egész szám, amely alapértelmezés szerint az **500**.
Ha a parancs nem fejeződik be a megadott időn belül, akkor a parancs létrehoz egy **TimeoutException** üzenettel "a művelet túllépte az időkorlátot."

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

## <a name="properties"></a>Tulajdonságok

### <a name="addonsmenu"></a>AddOnsMenu

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely a bővítmények menü beolvassa a PowerShell fülre.

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

### <a name="caninvoke"></a>CanInvoke

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható logikai tulajdonsággal adja vissza egy **$true** értéket, ha egy parancsfájl indítható a [Invoke (parancsfájl)](#invoke-script-) metódust.

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

### <a name="consolepane"></a>Consolepane

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.  A Windows PowerShell ISE 2.0 Ez nevű **CommandPane**.

A csak olvasható tulajdonság, amely lekérdezi a konzol ablaktáblában [szerkesztő](../ise/The-ISEEditor-Object.md) objektum.

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a>DisplayName

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az írható-olvasható tulajdonság, amely lekérdezi vagy beállítja a szöveg, amelyet a PowerShell lapon jelenik meg. Alapértelmezés szerint lapfülek neve "PowerShell #", ahol a # számot jelöl.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a>ExpandedScript

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási és írási logikai tulajdonság, amely meghatározza, hogy a parancssori panelbe kibontva vagy rejtett.

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a>Fájlok

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a [parancsfájl fájlok](../ise/The-ISEFileCollection-Object.md) , amelyek nyissa meg a PowerShell-lapon.

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a>Kimenet

Ez a funkció megtalálható-e a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE későbbi verzióiban is.  A Windows PowerShell ISE újabb verzióit, használhatja a **ConsolePane** célból objektum.

A csak olvasható tulajdonság, amely lekérdezi a Tesztkimenet ablaktáblán, az aktuális [szerkesztő](../ise/The-ISEEditor-Object.md).

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a>parancssor

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi az aktuális adatkérés szövegét. Megjegyzés: a **Rákérdezés** függvény felülbírálhatja a felhasználó "™ s profil. Ha az eredmény egy egyszerű karakterlánc, majd a tulajdonság adja vissza semmi sem.

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a>ShowCommands

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Az írható-olvasható tulajdonság, amely jelzi, ha a parancsok panelt jelenleg jelenik meg.

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a>StatusText

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a **PowerShellTab** állapotleíró szöveg.

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a>HorizontalAddOnToolsPaneOpened

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A csak olvasható tulajdonság, amely azt jelzi, hogy a vízszintes bővítmények eszközpanelt megnyitott.

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a>VerticalAddOnToolsPaneOpened

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A csak olvasható tulajdonság, amely azt jelzi, hogy a bővítmények függőleges eszközpanelt megnyitott.

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a>Lásd még:

- [A PowerShellTabCollection objektum](The-PowerShellTabCollection-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)