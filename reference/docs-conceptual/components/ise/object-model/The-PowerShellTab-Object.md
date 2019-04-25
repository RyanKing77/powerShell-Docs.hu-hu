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
# <a name="the-powershelltab-object"></a>Az PowerShellTab objektum

A **PowerShellTab** objektum képviseli egy Windows PowerShell-modul környezetben.

## <a name="methods"></a>Módszerek

### <a name="invoke-script-"></a>Meghívása\( parancsfájl \)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A megadott parancsfájlt futtatja a PowerShell-lapon.

> [!NOTE]
> Ez a módszer csak használható többi PowerShell-lap nem a PowerShell lap, amelyből futtatni. Nem ad vissza minden olyan objektumot, vagy értéket. Ha a kód módosítja bármely változó, majd ezeket a módosításokat továbbra is fennáll, amelyre vonatkozóan a parancs meghívása lapján.

**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatandó a parancsfájlblokkban.

```powershell
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psISE.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a>InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A megadott parancsfájlt futtatja a PowerShell-lapon.

> [!NOTE]
> Ez a módszer csak használható többi PowerShell-lap nem a PowerShell lap, amelyből futtatni. A parancsprogram-blokkot fut, és, hogy a parancsfájl által visszaadott értéket adja vissza, amelyről a parancs meghívása a futtatási környezetet. Ha a parancs több időt vesz igénybe, mint a **millesecondsTimeout** az érték határozza meg, akkor a parancs futása sikertelen, egy kivétellel: "A művelet túllépte az időkorlátot."

**Parancsfájl** -System.Management.Automation.ScriptBlock vagy karakterlánc futtatandó a parancsfájlblokkban.

**\[useNewScope\]**  -választható logikai alapértelmezés szerint **$true** Ha beállítása **$true**, majd az új hatókör létrehozása belül, amely a parancs futtatásához. Nem módosítja a futtatási környezetet a PowerShell-lap, a parancs által megadott.

**\[millisecondsTimeout\]**  – nem kötelező egész szám, amely alapértelmezés szerint a **500**.
Ha a parancs nem fejeződik be a meghatározott időn belül, akkor a parancs létrehoz egy **TimeoutException** üzenettel "a művelet túllépte az időkorlátot."

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

A csak olvasható tulajdonság, amely lekérdezi a bővítmények menü a PowerShell-lap.

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

A csak olvasható logikai tulajdonság, amely visszaadja a **$true** értékét, ha a parancsfájl indítható a [Invoke (szkript)](#invoke-script-) metódus.

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

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.  A Windows PowerShell ISE 2.0 Ez nevű **CommandPane**.

A csak olvasható tulajdonság, amely lekérdezi a konzol ablaktáblában [szerkesztő](The-ISEEditor-Object.md) objektum.

```powershell
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane
```

### <a name="displayname"></a>DisplayName

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Lekérdezi vagy beállítja a szöveg, amely az olvasási és írási tulajdonság a PowerShell-lap jelenik meg. Lap neve alapértelmezés szerint "PowerShell #", ahol a # számot jelöl.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="expandedscript"></a>ExpandedScript

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Az olvasási és írási logikai tulajdonság, amely meghatározza, hogy a parancsfájl panelen megjelenített vagy rejtett.

```powershell
# Toggle the expanded script property to see its effect.
$psISE.CurrentPowerShellTab.ExpandedScript = !$psISE.CurrentPowerShellTab.ExpandedScript
```

### <a name="files"></a>Fájlok

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a [parancsfájlok gyűjteményét](The-ISEFileCollection-Object.md) , amelyek a PowerShell-lap megnyitása.

```powershell
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb"
# Gets the line count
$newFile.Editor.LineCount
```

### <a name="output"></a>Kimenet

Ez a funkció megtalálható a Windows PowerShell ISE 2.0-s volt, de eltávolították vagy átnevezték az ISE-ben későbbi verzióiban is.  A Windows PowerShell ISE-ben újabb verziói esetén használhatja a **ConsolePane** objektum ugyanarra a célra.

A csak olvasható tulajdonság, amely lekérdezi a Tesztkimenet ablaktáblán, az aktuális [szerkesztő](The-ISEEditor-Object.md).

```powershell
# Clears the text in the Output pane.
$psISE.CurrentPowerShellTab.output.clear()
```

### <a name="prompt"></a>Kérdés

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi az aktuális adatkérési szöveget. Megjegyzés: a **Rákérdezés** függvény a felhasználó felülbírálhatja "™ s profil. Ha az eredmény nem eltérő egy egyszerű karakterláncot, majd ezt a tulajdonságot függvény semmi.

```powershell
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

### <a name="showcommands"></a>ShowCommands

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Az olvasási és írási tulajdonság, amely azt jelzi, ha a parancsok ablaktáblán látható.

```powershell
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $true
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands = $true}
```

### <a name="statustext"></a>StatusText

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A csak olvasható tulajdonság, amely lekérdezi a **PowerShellTab** Állapotszöveg részén.

```powershell
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

### <a name="horizontaladdontoolspaneopened"></a>HorizontalAddOnToolsPaneOpened

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható tulajdonság, amely azt jelzi, hogy a vízszintes bővítmények eszköz panel megnyitott.

```powershell
# Gets the current state of the horizontal Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

### <a name="verticaladdontoolspaneopened"></a>VerticalAddOnToolsPaneOpened

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható tulajdonság, amely azt jelzi, hogy nyitva-e a függőleges bővítmények eszköz panel.

```powershell
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands = $true
# Gets the current state of the vertical Add-ons tool pane.
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a>Lásd még:

- [Az PowerShellTabCollection objektum](The-PowerShellTabCollection-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)