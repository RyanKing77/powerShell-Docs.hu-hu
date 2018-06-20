---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az PowerShellTabCollection objektum
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: d9088b26de35360b8258d3f15924b3010a986d15
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953072"
---
# <a name="the-powershelltabcollection-object"></a>Az PowerShellTabCollection objektum

A **PowerShellTab** gyűjteményobjektumot gyűjteménye **PowerShellTab** objektumok. Minden egyes **PowerShellTab** objektum funkciókkal, mint egy külön futtatókörnyezetben. Microsoft.PowerShell.Host.ISE.PowerShellTabs osztály egy példányát. Példa: a **$psISE.PowerShellTabs** objektum.

## <a name="methods"></a>Metódusok

### <a name="add"></a>Add\(\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Új PowerShell lap hozzáadása a gyűjteményhez. Az újonnan hozzáadott lapon adja vissza.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Remove\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

Eltávolítja a megadott lapot a **psTab** paraméter.

**psTab** távolítsa el a PowerShell fülre.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)

A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott.

A PowerShell lapon megadott kiválasztja a **psTab** paraméter abba, hogy a jelenleg aktív PowerShell fülre.

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
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)