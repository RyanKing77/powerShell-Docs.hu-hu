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
# <a name="the-iseaddontoolcollection-object"></a>Az ISEAddOnToolCollection objektum

A **ISEAddOnToolCollection** objektum olyan gyűjteménye, **ISEAddOnTool** objektumokat. An example is the **$psISE.CurrentPowerShellTab.VerticalAddOnTools** object.

## <a name="methods"></a>Metódusok

### <a name="add-name-controltype-isvisible-"></a>Adjon hozzá\( nevét, ControlType, \[IsVisible\] \)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Egy új bővítménye, amellyel hozzáadja a gyűjteményhez. Az újonnan hozzáadott kiegészítő eszköz adja vissza. A parancs futtatása előtt telepítse a bővítményt eszközt a helyi számítógépen, és a szerelvény betöltése.

**Név** -karakterláncot a bővítmény eszköz Windows PowerShell ISE-ben hozzáadott megjelenített nevét adja meg.

**ControlType** – azt adja meg a vezérlő, amely hozzá van adva.

**\[IsVisible\]**  – nem kötelező logikai Ha **$true**, a bővítmény eszköz azonnal látható, a kapcsolódó eszköz panelen.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="remove-item-"></a>Távolítsa el\( elem \)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Eltávolítja a bővítmény megadott eszköz a gyűjteményből.

**Elem** -Microsoft.PowerShell.Host.ISE.ISEAddOnTool meghatározza az objektum, melyet távolítható el a Windows PowerShell ISE-ben.

```powershell
# Load a DLL with an add-on and then add it to the ISE
[reflection.assembly]::LoadFile("c:\test\ISESimpleSolution\ISESimpleSolution.dll")
$psISE.CurrentPowerShellTab.VerticalAddOnTools.Add("Solutions", [ISESimpleSolution.Solution], $true)
```

### <a name="setselectedpowershelltab-pstab-"></a>SetSelectedPowerShellTab\( psTab \)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Kiválasztja a PowerShell-lap, amely a **psTab** paraméter határozza meg.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell fülre kattintva válassza ki.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'Brand New Tab'
```

### <a name="remove-pstab-"></a>Távolítsa el\( psTab \)

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

Eltávolítja a PowerShell lap, amely a **psTab** paraméter határozza meg.

**psTab** -Microsoft.PowerShell.Host.ISE.PowerShellTab a PowerShell-lap eltávolítása.

```powershell
$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab.
$newTab.DisplayName = 'This tab will go away in 5 seconds'
sleep 5
$psISE.PowerShellTabs.Remove($newTab)
```

## <a name="see-also"></a>Lásd még:

- [The PowerShellTab Object](The-PowerShellTab-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)
