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
---
# <a name="the-iseaddontoolcollection-object"></a>Az ISEAddOnToolCollection objektum

A **ISEAddOnToolCollection** objektum gyűjteménye **ISEAddOnTool** objektumok. Példa: a **$psISE.CurrentPowerShellTab.VerticalAddOnTools** objektum.

## <a name="methods"></a>Metódusok

### <a name="add-name-controltype-isvisible-"></a>Adja hozzá\( nevét, ControlType, \[IsVisible\] \)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Egy új bővítménye, amellyel hozzáadja a gyűjteményben. Az újonnan hozzáadott bővítmény eszközt ad vissza. Ez a parancs futtatása előtt telepítse a bővítmény eszközt a helyi számítógépen, és a szerelvény betöltése.

**Név** -karakterláncot határozza meg a Windows PowerShell ISE hozzáadott bővítmény eszköz megjelenítési neve.

**ControlType** – azt adja meg a hozzáadott vezérlő.

**\[IsVisible\]**  -választható logikai Ha **$true**, a bővítmény eszköz azonnal látható, a kapcsolódó eszköz panelen.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a>Távolítsa el\( elem \)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

A megadott bővítmény eszköz eltávolítása a gyűjteményben.

**Elem** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool eltávolítsa őket a Windows PowerShell ISE-objektumot adja meg.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a>SetSelectedPowerShellTab\( psTab \)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Kiválasztja a PowerShell lap, amely a **psTab** paraméter határozza meg.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre kattintva válassza ki.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a>Távolítsa el\( psTab \)

Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

Eltávolítja a PowerShell lap, amely a **psTab** paraméter határozza meg.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre, és távolítsa el.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a>Lásd még:

- [The PowerShellTab Object](The-PowerShellTab-Object.md)
- [A Windows PowerShell ISE objektummodell Scripting célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)