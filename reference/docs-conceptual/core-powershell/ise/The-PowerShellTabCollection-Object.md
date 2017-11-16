---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A PowerShellTabCollection objektum
ms.assetid: 81f4bf4a-83bf-415e-8378-1703792fbb58
ms.openlocfilehash: dcdc16ae126453b6ade64917ac4950cc05e5f8ad
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 08/03/2017
---
# <a name="the-powershelltabcollection-object"></a>A PowerShellTabCollection objektum
  A **PowerShellTab** gyűjteményobjektumot gyűjteménye **PowerShellTab** objektumok. Minden egyes **PowerShellTab** objektum funkciókkal, mint egy külön futtatókörnyezetben. Microsoft.PowerShell.Host.ISE.PowerShellTabs osztály egy példányát. Példa: a **$psISE.PowerShellTabs** objektum.

## <a name="methods"></a>Metódusok

### <a name="add"></a>Hozzáadása\(\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 Új PowerShell lap hozzáadása a gyűjteményhez. Az újonnan hozzáadott lapon adja vissza.

```
$NewTab=$psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab"
```

### <a name="removemicrosoftpowershellhostisepowershelltab-pstab"></a>Távolítsa el\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 Eltávolítja a megadott lapot a **psTab** paraméter.

 **psTab** távolítsa el a PowerShell fülre.

```

$newTab = $psISE.PowerShellTabs.Add()
Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="This tab will go away in 5 seconds" 
sleep 5 
$psISE.PowerShellTabs.Remove($newTab)
```

### <a name="setselectedpowershelltabmicrosoftpowershellhostisepowershelltab-pstab"></a>SetSelectedPowerShellTab\(Microsoft.PowerShell.Host.ISE.PowerShellTab psTab\)
  A Windows PowerShell ISE 2.0-s és újabb verzióiban támogatott. 

 A PowerShell lapon megadott kiválasztja a **psTab** paraméter abba, hogy a jelenleg aktív PowerShell fülre.

 **psTab** a PowerShell fülre kattintva válassza ki.

```
# Save the current tab in a variable and rename it
$OldTab = $psISE.CurrentPowerShellTab
$psISE.CurrentPowerShellTab.DisplayName="Old Tab"
# Create a new tab and give it a new display name
$newTab = $psISE.PowerShellTabs.Add()
$newTab.DisplayName="Brand New Tab" 
# Switch back to the original tab
$psISE.PowerShellTabs.SelectedPowerShellTab=$oldtab
```

## <a name="see-also"></a>Lásd még:
- [A PowerShellTab objektum](The-PowerShellTab-Object.md) 
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [A Windows PowerShell ISE objektumhivatkozás modell](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [A ISE objektum modell hierarchia](../ise/The-ISE-Object-Model-Hierarchy.md)

  
