---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: "A Windows PowerShell ISE objektumhivatkozás modell"
ms.assetid: e1a9e7d1-0fd5-47de-8d9b-f1be1ed13b0c
ms.openlocfilehash: 624ddca3895ba3e24bf52a27babdb07e8714baae
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/08/2017
---
# <a name="windows-powershell-ise-object-model-reference"></a>A Windows PowerShell ISE objektumhivatkozás modell
  
## <a name="object-model-reference"></a>Objektumhivatkozás modell
 Ez a szakasz az alapul szolgáló osztályokat, amelyek meghatározzák a különböző objektumok inWindows PowerShell® integrált parancsfájl-kezelési környezet (ISE) hivatkozást biztosít. A saját hierarchiájukhoz rendezve objektumok megtekintéséhez lásd: [az ISE modell objektumhierarchia](The-ISE-Object-Model-Hierarchy.md).

 [A ISEAddOnTool objektum](The-ISEAddOnTool-Object.md) példák: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.

 [A ISEAddOnTool objektum](The-ISEAddOnTool-Object.md) [a ISEEditor objektum](The-ISEEditor-Object.md) példák: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.

 [A ISEFile objektum](The-ISEFile-Object.md) példák: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].

 [A ISEFileCollection objektum](The-ISEFileCollection-Object.md) példák: $psISE.PowerShellTabs.Files.

 [A ISEMenuItem objektum](The-ISEMenuItem-Object.md) példák: $psISE.CurrentPowerShellTab.AddOnsMenu, $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].

 [A ISEMenuItemCollection objektum](The-ISEMenuItemCollection-Object.md) példa: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.

 [A ISEOptions objektum](The-ISEOptions-Object.md) példák: $psISE.Options, $psISE.Options.DefaultOptions.

 [A ObjectModelRoot objektum](The-ObjectModelRoot-Object.md) példa: A legfelső szintű $psISE objektum.

 [A PowerShellTab objektum](The-PowerShellTab-Object.md) példák: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].

 [A PowerShellTabCollection objektum](The-PowerShellTabCollection-Object.md) példa: $psISE.PowerShellTabs.

## <a name="see-also"></a>Lásd még:
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
