---
ms.date: 2017-06-05
keywords: PowerShell parancsmag
title: A ISEAddOnTool objektum
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: b813fcac547c8069e84741081a3ceb00044bab87
ms.sourcegitcommit: 3720ce4efb6735694cfb53a1b793d949af5d1bc5
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 09/29/2017
---
# <a name="the-iseaddontool-object"></a>A ISEAddOnTool objektum
  Egy **ISEAddonTool** objektum által jelképezett egy telepített bővítmény eszköz, amely további funkciókat toWindows PowerShell ISE biztosít. Példa: a **parancsok** kattintva megjeleníthető eszköz **nézet**, majd **megjelenítése parancs bővítmény**. Ez az eszköz érhető majd meg a különböző elérhető kezelésével **ISEAddOnTool** objektumok.

 Lehet, hogy minden bővítménye, amellyel a függőleges vagy vízszintes ablaktáblában vagy társítani. A függőleges ablaktáblán a jobb oldali széle és a Windows PowerShell ISE rögzítve van. A vízszintes ablaktábla alsó széle van rögzítve.

 A Windows PowerShell ISE PowerShell lapokon is rendelkeznek a saját bővítmény eszközök vannak telepítve. Lásd: [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) és [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) az eszközök rendelkezésére a jelenleg kiválasztott lap-gyűjtemény eléréséhez vagy a bármely ugyanazok a tulajdonságok a **PowerShellTab** objektumokat a [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) gyűjtemény objektumhoz.

## <a name="methods"></a>Metódusok
 Nincsenek elérhető objektumok az osztály egyetlen Windows PowerShell ISE-specifikus módszer.

## <a name="properties"></a>Tulajdonságok

### <a name="control"></a>Szabályozás
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

 A **vezérlő** tulajdonság a parancsok bővítmény eszköz részleteit számos olvasási hozzáférést biztosít.

```
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
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

 A logikai tulajdonság, amely azt jelzi, hogy a bővítmény eszköz jelenleg a hozzárendelt ablaktáblán látható. Ha látható, beállíthatja a **IsVisible** tulajdonságot **$false** elrejtése az eszközt, vagy állítsa be a **IsVisible** tulajdonságot **$true** végrehajtásához egy bővítmény eszköz, amely a PowerShell lapon látható. Ne feledje, hogy egy bővítmény eszköz rejtett, után már nem elérhető a **CurrentVisibleHorizontalTool** vagy **CurrentVisibleVerticalTool** objektumokat, és ezért nem tehető láthatóvá használatával Ez a tulajdonság az adott objektumhoz.

```
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible=$true

```

### <a name="name"></a>Név
  Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.

 A csak olvasható tulajdonság, amely lekérdezi a bővítmény eszköz neve.

```
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.name
Commands

```

## <a name="see-also"></a>Lásd még:
- [A ISEAddOnToolCollection objektum](The-ISEAddOnToolCollection-Object.md)
- [A Windows PowerShell ISE Scripting Hálózatiobjektum-modellje](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [A Windows PowerShell ISE objektumhivatkozás modell](Windows-PowerShell-ISE-Object-Model-Reference.md)
- [A ISE objektum modell hierarchia](The-ISE-Object-Model-Hierarchy.md)

