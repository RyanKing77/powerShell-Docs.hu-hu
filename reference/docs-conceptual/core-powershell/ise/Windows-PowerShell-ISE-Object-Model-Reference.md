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
# <a name="windows-powershell-ise-object-model-reference"></a><span data-ttu-id="75b67-103">A Windows PowerShell ISE objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="75b67-103">Windows PowerShell ISE Object Model Reference</span></span>
  
## <a name="object-model-reference"></a><span data-ttu-id="75b67-104">Objektumhivatkozás modell</span><span class="sxs-lookup"><span data-stu-id="75b67-104">Object Model Reference</span></span>
 <span data-ttu-id="75b67-105">Ez a szakasz az alapul szolgáló osztályokat, amelyek meghatározzák a különböző objektumok inWindows PowerShell® integrált parancsfájl-kezelési környezet (ISE) hivatkozást biztosít.</span><span class="sxs-lookup"><span data-stu-id="75b67-105">This section provides a reference on the underlying classes that define the various objects inWindows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="75b67-106">A saját hierarchiájukhoz rendezve objektumok megtekintéséhez lásd: [az ISE modell objektumhierarchia](The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="75b67-106">To see the objects organized in their hierarchy, see [The ISE Object Model Hierarchy](The-ISE-Object-Model-Hierarchy.md).</span></span>

 <span data-ttu-id="75b67-107">[A ISEAddOnTool objektum](The-ISEAddOnTool-Object.md) példák: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.</span><span class="sxs-lookup"><span data-stu-id="75b67-107">[The ISEAddOnTool Object](The-ISEAddOnTool-Object.md) Examples: $psISE.CurrentVisibleHorizontalTool, $psISE.CurrentVisibleVerticalTool.</span></span>

 <span data-ttu-id="75b67-108">[A ISEAddOnTool objektum](The-ISEAddOnTool-Object.md) [a ISEEditor objektum](The-ISEEditor-Object.md) példák: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.</span><span class="sxs-lookup"><span data-stu-id="75b67-108">[The ISEAddOnTool Object](The-ISEAddOnTool-Object.md) [The ISEEditor Object](The-ISEEditor-Object.md) Examples: $psISE.CurrentFile.Editor, $psISE.CurrentPowerShellTab.Output, $psISE.CurrentPowerShellTab.CommandPane.</span></span>

 <span data-ttu-id="75b67-109">[A ISEFile objektum](The-ISEFile-Object.md) példák: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].</span><span class="sxs-lookup"><span data-stu-id="75b67-109">[The ISEFile Object](The-ISEFile-Object.md) Examples: $psISE.CurrentFile, $psISE.PowerShellTabs.Files\[0\].</span></span>

 <span data-ttu-id="75b67-110">[A ISEFileCollection objektum](The-ISEFileCollection-Object.md) példák: $psISE.PowerShellTabs.Files.</span><span class="sxs-lookup"><span data-stu-id="75b67-110">[The ISEFileCollection Object](The-ISEFileCollection-Object.md) Examples: $psISE.PowerShellTabs.Files.</span></span>

 <span data-ttu-id="75b67-111">[A ISEMenuItem objektum](The-ISEMenuItem-Object.md) példák: $psISE.CurrentPowerShellTab.AddOnsMenu, $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].</span><span class="sxs-lookup"><span data-stu-id="75b67-111">[The ISEMenuItem Object](The-ISEMenuItem-Object.md) Examples: $psISE.CurrentPowerShellTab.AddOnsMenu , $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus\[0\].</span></span>

 <span data-ttu-id="75b67-112">[A ISEMenuItemCollection objektum](The-ISEMenuItemCollection-Object.md) példa: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.</span><span class="sxs-lookup"><span data-stu-id="75b67-112">[The ISEMenuItemCollection Object](The-ISEMenuItemCollection-Object.md) Example: $psISE.CurrentPowerShellTab.AddOnsMenu.Submenus.</span></span>

 <span data-ttu-id="75b67-113">[A ISEOptions objektum](The-ISEOptions-Object.md) példák: $psISE.Options, $psISE.Options.DefaultOptions.</span><span class="sxs-lookup"><span data-stu-id="75b67-113">[The ISEOptions Object](The-ISEOptions-Object.md) Examples: $psISE.Options, $psISE.Options.DefaultOptions.</span></span>

 <span data-ttu-id="75b67-114">[A ObjectModelRoot objektum](The-ObjectModelRoot-Object.md) példa: A legfelső szintű $psISE objektum.</span><span class="sxs-lookup"><span data-stu-id="75b67-114">[The ObjectModelRoot Object](The-ObjectModelRoot-Object.md) Example: The root $psISE object.</span></span>

 <span data-ttu-id="75b67-115">[A PowerShellTab objektum](The-PowerShellTab-Object.md) példák: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].</span><span class="sxs-lookup"><span data-stu-id="75b67-115">[The PowerShellTab Object](The-PowerShellTab-Object.md) Examples: $psISE.CurrentPowerShellTab, $psISE.PowerShellTabs\[0\].</span></span>

 <span data-ttu-id="75b67-116">[A PowerShellTabCollection objektum](The-PowerShellTabCollection-Object.md) példa: $psISE.PowerShellTabs.</span><span class="sxs-lookup"><span data-stu-id="75b67-116">[The PowerShellTabCollection Object](The-PowerShellTabCollection-Object.md) Example: $psISE.PowerShellTabs.</span></span>

## <a name="see-also"></a><span data-ttu-id="75b67-117">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="75b67-117">See Also</span></span>
- [<span data-ttu-id="75b67-118">A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje</span><span class="sxs-lookup"><span data-stu-id="75b67-118">The Windows PowerShell ISE Scripting Object Model</span></span>](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
