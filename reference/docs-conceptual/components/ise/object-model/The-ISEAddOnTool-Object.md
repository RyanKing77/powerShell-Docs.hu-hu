---
ms.date: 06/05/2017
keywords: PowerShell, a parancsmag
title: Az ISEAddOnTool objektum
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: e091f37601c7a4fdaf5deff8c668b18ee7369e74
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62086799"
---
# <a name="the-iseaddontool-object"></a>Az ISEAddOnTool objektum

Egy **ISEAddonTool** objektum képviseli egy telepített kiegészítő eszköz, amely további funkciókat toWindows PowerShell ISE-t biztosít. Például a **parancsok** kattintva megjeleníthető eszköz **nézet**, majd **megjelenítése a parancs bővítmény**. Ez az eszköz érhető el majd, a különböző elérhető manipulálásával **ISEAddOnTool** objektumokat.

Minden egyes bővítménye, amellyel a függőleges vagy vízszintes ablaktáblán a vagy társítható. A függőleges ablaktáblán a jobb szélen Windows PowerShell ISE-ben való rögzítve van. A vízszintes ablaktábla alsó széle rögzítve van.

Egyes PowerShell-lap, a Windows PowerShell ISE-ben is rendelkezik a saját telepített kiegészítő eszközök. Lásd: [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) és [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) eléréséhez a jelenleg kijelölt lapon elérhető eszközök gyűjteményét, vagy a azonos tulajdonságokkal bármelyik a **PowerShellTab** az objektumok a [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) gyűjtemény objektumra vonatkozóan.

## <a name="methods"></a>Módszerek

Nincsenek elérhető a osztályú objektumok nem Windows PowerShell ISE-specifikus módszereket.

## <a name="properties"></a>Tulajdonságok

### <a name="control"></a>Szabályozás

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A **vezérlő** tulajdonság a parancsok bővítmény eszköz részletek nagy része olvasási hozzáférést biztosít.

```powershell
# View the properties of the Commands add-on tool.
# (assumes that it is visible in the vertical pane)
$psISE.CurrentVisibleVerticalTool.Control
HostObject                  : Microsoft.PowerShell.Host.ISE.ObjectModelRoot
Content                     :
HasContent                  :
ContentTemplate             :
ContentTemplateSelector     :
ContentStringFormat         :
BorderBrush                 :
BorderThickness             :
Background                  :
Foreground                  :
FontFamily                  :
FontSize                    :
FontStretch                 :
FontStyle                   :
FontWeight                  :
HorizontalContentAlignment  :
VerticalContentAlignment    :
TabIndex                    :
IsTabStop                   :
Padding                     :
Template                    : System.Windows.Controls.ControlTemplate
Style                       :
OverridesDefaultStyle       :
UseLayoutRounding           :
Triggers                    : {}
TemplatedParent             :
Resources                   : {System.Windows.Controls.TabItem}
DataContext                 :
BindingGroup                :
Language                    :
Name                        :
Tag                         :
InputScope                  :
ActualWidth                 : 370.75
ActualHeight                : 676.559097412109
LayoutTransform             :
Width                       :
MinWidth                    :
MaxWidth                    :
Height                      :
MinHeight                   :
MaxHeight                   :
FlowDirection               : LeftToRight
Margin                      :
HorizontalAlignment         :
VerticalAlignment           :
FocusVisualStyle            :
Cursor                      :
ForceCursor                 :
IsInitialized               : True
IsLoaded                    :
ToolTip                     :
ContextMenu                 :
Parent                      :
HasAnimatedProperties       :
InputBindings               :
CommandBindings             :
AllowDrop                   :
DesiredSize                 : 227.66,676.559097412109
IsMeasureValid              : True
IsArrangeValid              : True
RenderSize                  : 370.75,676.559097412109
RenderTransform             :
RenderTransformOrigin       :
IsMouseDirectlyOver         : False
IsMouseOver                 : False
IsStylusOver                : False
IsKeyboardFocusWithin       : False
IsMouseCaptured             :
IsMouseCaptureWithin        : False
IsStylusDirectlyOver        : False
IsStylusCaptured            :
IsStylusCaptureWithin       : False
IsKeyboardFocused           : False
IsInputMethodEnabled        :
Opacity                     :
OpacityMask                 :
BitmapEffect                :
Effect                      :
BitmapEffectInput           :
CacheMode                   :
Uid                         :
Visibility                  : Visible
ClipToBounds                : False
Clip                        :
SnapsToDevicePixels         : False
IsFocused                   :
IsEnabled                   :
IsHitTestVisible            :
IsVisible                   : True
Focusable                   :
PersistId                   : 1
IsManipulationEnabled       :
AreAnyTouchesOver           : False
AreAnyTouchesDirectlyOver   :
AreAnyTouchesCapturedWithin : False
AreAnyTouchesCaptured       :
TouchesCaptured             : {}
TouchesCapturedWithin       : {}
TouchesOver                 : {}
TouchesDirectlyOver         : {}
DependencyObjectType        : System.Windows.DependencyObjectType
IsSealed                    : False
Dispatcher                  : System.Windows.Threading.Dispatcher
```

### <a name="isvisible"></a>IsVisible

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A logikai tulajdonság, amely azt jelzi, hogy a bővítmény eszköz jelenleg látható a hozzárendelt ablaktáblán. Ha látható, beállíthatja a **IsVisible** tulajdonságot **$false** elrejtése az eszköz, vagy állítsa be a **IsVisible** tulajdonságot **$true** győződjön meg arról, hogy egy bővítmény eszköz, amely a PowerShell-lap látható. Vegye figyelembe, hogy egyik bővítménye, amellyel az elrejtett után már nem keresztül elérhető a **CurrentVisibleHorizontalTool** vagy **CurrentVisibleVerticalTool** objektumokat, és ezért nem tehető láthatóvá használatával Ez a tulajdonság az adott objektumhoz.

```powershell
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible = $true
```

### <a name="name"></a>Név

Támogatja a Windows PowerShell ISE-ben, 3.0-s és újabb verziók, és nem szerepel a korábbi verziók.

A csak olvasható tulajdonság, amely lekérdezi a bővítmény eszköz nevét.

```powershell
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.Name
Commands
```

## <a name="see-also"></a>Lásd még:

- [Az ISEAddOnToolCollection objektum](The-ISEAddOnToolCollection-Object.md)
- [A Windows PowerShell ISE parancsfájl-kezelési objektummodelljének célja](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [Az ISE objektummodell-hierarchiája](The-ISE-Object-Model-Hierarchy.md)