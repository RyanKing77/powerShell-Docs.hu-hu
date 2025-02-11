---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az PowerShellTabCollection objektum
ms.openlocfilehash: 5a1318534ddce19c2f5faa0d2013e2b38d8b79e5
ms.sourcegitcommit: a6f13c16a535acea279c0ddeca72f1f0d8a8ce4c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 06/12/2019
ms.locfileid: "67030484"
---
# <a name="the-powershelltabcollection-object"></a>Az PowerShellTabCollection objektum

A **PowerShellTab** objektum olyan gyűjteménye, **PowerShellTab** objektumokat. Minden egyes **PowerShellTab** objektum egy önálló futtatókörnyezet funkcionál. Fontos Microsoft.PowerShell.Host.ISE.PowerShellTabs osztály egy példányát. Például a **$psISE.PowerShellTabs** objektum.

## <a name="methods"></a>Metódusok

### <a name="add"></a>Hozzáadása\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Új PowerShell-lap hozzáadása a gyűjteményhez. Az újonnan hozzáadott lapon ad vissza.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Eltávolítja a megadott lapot az **psTab** paraméter.

**psTab** eltávolítása a PowerShell-lapon.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A megadott PowerShell-lap kiválasztása a **psTab** paramétert, hogy a jelenleg aktív PowerShell-lap.

**psTab** a PowerShell fülre kattintva válassza ki.

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

## <a name="see-also"></a>Lásd még:

- [The PowerShellTab Object](The-PowerShellTab-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)
