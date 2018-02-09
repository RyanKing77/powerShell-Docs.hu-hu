---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell ISE objektummodell-referenciája"
ms.assetid: e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c
ms.openlocfilehash: 624ddca3895ba3e24bf52a27babdb07e8714baae
ms.sourcegitcommit: 18e3bfae83ffe282d3fd1a45f5386f3b7250f0c0
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/08/2018
---
# <a name="windows-powershell-ise-object-model-reference"></a>A Windows PowerShell ISE objektummodell-referenciája
  
## <a name="object-model-reference"></a>Objektumhivatkozás modell
 Ez a szakasz az alapul szolgáló osztályokat, amelyek meghatározzák a különböző objektumok inWindows PowerShell® integrált parancsfájl-kezelési környezet (ISE) hivatkozást biztosít. A saját hierarchiájukhoz rendezve objektumok megtekintéséhez lásd: [az ISE modell objektumhierarchia](The-ISE-Object-Model-Hierarchy.md).

 [The ISEAddOnTool Object](The-ISEAddOnTool-Object.md) Examples: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.

 [A ISEAddOnTool objektum](The-ISEAddOnTool-Object.md) [a ISEEditor objektum](The-ISEEditor-Object.md) példák: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.

 [The ISEFile Object](The-ISEFile-Object.md) Examples: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].

 [A ISEFileCollection objektum](The-ISEFileCollection-Object.md) példák: $psISE.PowerShellTabs.Files.

 [The ISEMenuItem Object](The-ISEMenuItem-Object.md) Examples: $psISE.CurrentPowerShellTab.AddOnsMenu , $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].

 [A ISEMenuItemCollection objektum](The-ISEMenuItemCollection-Object.md) példa: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.

 [A ISEOptions objektum](The-ISEOptions-Object.md) példák: $psISE.Options, $psISE.Options.DefaultOptions.

 [A ObjectModelRoot objektum](The-ObjectModelRoot-Object.md) példa: A legfelső szintű $psISE objektum.

 [A PowerShellTab objektum](The-PowerShellTab-Object.md) példák: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].

 [A PowerShellTabCollection objektum](The-PowerShellTabCollection-Object.md) példa: $psISE.PowerShellTabs.

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
