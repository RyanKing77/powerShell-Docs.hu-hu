---
ms.date: 06/05/2017
keywords: PowerShell parancsmag
title: Az ISEAddOnTool objektum
ms.assetid: ce84d8bc-07ba-41f6-bdde-d6f3fddcd1e3
ms.openlocfilehash: e091f37601c7a4fdaf5deff8c668b18ee7369e74
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954806"
---
# <a name="the-iseaddontool-object"></a><span data-ttu-id="91841-103">Az ISEAddOnTool objektum</span><span class="sxs-lookup"><span data-stu-id="91841-103">The ISEAddOnTool Object</span></span>

<span data-ttu-id="91841-104">Egy **ISEAddonTool** objektum által jelképezett egy telepített bővítmény eszköz, amely további funkciókat toWindows PowerShell ISE biztosít.</span><span class="sxs-lookup"><span data-stu-id="91841-104">An **ISEAddonTool** object represents an installed add-on tool that provides additional functionality toWindows PowerShell ISE.</span></span> <span data-ttu-id="91841-105">Példa: a **parancsok** kattintva megjeleníthető eszköz **nézet**, majd **megjelenítése parancs bővítmény**.</span><span class="sxs-lookup"><span data-stu-id="91841-105">An example is the **Commands** tool that you can display by clicking **View**, then **Show Command Add-on**.</span></span> <span data-ttu-id="91841-106">Ez az eszköz érhető majd meg a különböző elérhető kezelésével **ISEAddOnTool** objektumok.</span><span class="sxs-lookup"><span data-stu-id="91841-106">This tool is then accessible to you by manipulating the various available **ISEAddOnTool** objects.</span></span>

<span data-ttu-id="91841-107">Lehet, hogy minden bővítménye, amellyel a függőleges vagy vízszintes ablaktáblában vagy társítani.</span><span class="sxs-lookup"><span data-stu-id="91841-107">Each add-on tool can be associated with either the vertical pane or the horizontal pane.</span></span> <span data-ttu-id="91841-108">A függőleges ablaktáblán a jobb oldali széle és a Windows PowerShell ISE rögzítve van.</span><span class="sxs-lookup"><span data-stu-id="91841-108">The vertical pane is docked to the right edge of Windows PowerShell ISE.</span></span> <span data-ttu-id="91841-109">A vízszintes ablaktábla alsó széle van rögzítve.</span><span class="sxs-lookup"><span data-stu-id="91841-109">The horizontal pane is docked to the bottom edge.</span></span>

<span data-ttu-id="91841-110">A Windows PowerShell ISE PowerShell lapokon is rendelkeznek a saját bővítmény eszközök vannak telepítve.</span><span class="sxs-lookup"><span data-stu-id="91841-110">Each PowerShell tab in Windows PowerShell ISE can have its own set of add-on tools installed.</span></span> <span data-ttu-id="91841-111">Lásd: [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) és [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) az eszközök rendelkezésére a jelenleg kiválasztott lap-gyűjtemény eléréséhez vagy a bármely ugyanazok a tulajdonságok a **PowerShellTab** objektumokat a [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) gyűjtemény objektumhoz.</span><span class="sxs-lookup"><span data-stu-id="91841-111">See [$psISE.CurrentPowerShellTab.HorizontalAddOnTools](The-PowerShellTab-Object.md) and [$psISE.CurrentPowerShellTab.VerticalAddOnTools](The-PowerShellTab-Object.md) to access the collection of tools available to the currently selected tab or the same properties on any of the **PowerShellTab** objects in the [$psISE.PowerShellTabs](The-PowerShellTabCollection-Object.md) collection object.</span></span>

## <a name="methods"></a><span data-ttu-id="91841-112">Metódusok</span><span class="sxs-lookup"><span data-stu-id="91841-112">Methods</span></span>

<span data-ttu-id="91841-113">Nincsenek elérhető objektumok az osztály egyetlen Windows PowerShell ISE-specifikus módszer.</span><span class="sxs-lookup"><span data-stu-id="91841-113">There are no Windows PowerShell ISE-specific methods available for objects of this class.</span></span>

## <a name="properties"></a><span data-ttu-id="91841-114">Tulajdonságok</span><span class="sxs-lookup"><span data-stu-id="91841-114">Properties</span></span>

### <a name="control"></a><span data-ttu-id="91841-115">Szabályozás</span><span class="sxs-lookup"><span data-stu-id="91841-115">Control</span></span>

<span data-ttu-id="91841-116">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="91841-116">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="91841-117">A **vezérlő** tulajdonság a parancsok bővítmény eszköz részleteit számos olvasási hozzáférést biztosít.</span><span class="sxs-lookup"><span data-stu-id="91841-117">The **Control** property provides read access to many of the details of the Commands add-on tool.</span></span>

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

### <a name="isvisible"></a><span data-ttu-id="91841-118">IsVisible</span><span class="sxs-lookup"><span data-stu-id="91841-118">IsVisible</span></span>

<span data-ttu-id="91841-119">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="91841-119">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="91841-120">A logikai tulajdonság, amely azt jelzi, hogy a bővítmény eszköz jelenleg a hozzárendelt ablaktáblán látható.</span><span class="sxs-lookup"><span data-stu-id="91841-120">The Boolean property that indicates whether the add-on tool is currently visible in its assigned pane.</span></span> <span data-ttu-id="91841-121">Ha látható, beállíthatja a **IsVisible** tulajdonságot **$false** elrejtése az eszközt, vagy állítsa be a **IsVisible** tulajdonságot **$true** végrehajtásához egy bővítmény eszköz, amely a PowerShell lapon látható. Ne feledje, hogy egy bővítmény eszköz rejtett, után már nem elérhető a **CurrentVisibleHorizontalTool** vagy **CurrentVisibleVerticalTool** objektumokat, és ezért nem tehető láthatóvá használatával Ez a tulajdonság az adott objektumhoz.</span><span class="sxs-lookup"><span data-stu-id="91841-121">If it is visible, you can set the **IsVisible** property to **$false** to hide the tool, or set the **IsVisible** property to **$true** to make an add-on tool visible on its PowerShell tab. Note that after an add-on tool is hidden, it is no longer accessible through the **CurrentVisibleHorizontalTool** or **CurrentVisibleVerticalTool** objects, and therefore cannot be made visible by using this property on that object.</span></span>

```powershell
# Hide the current tool in the vertical tool pane
$psISE.CurrentVisibleVerticalTool.IsVisible = $false
# Show the first tool on the currently selected PowerShell tab
$psISE.CurrentPowerShellTab.VerticalAddOnTools[0].IsVisible = $true
```

### <a name="name"></a><span data-ttu-id="91841-122">Név</span><span class="sxs-lookup"><span data-stu-id="91841-122">Name</span></span>

<span data-ttu-id="91841-123">Támogatja a Windows PowerShell ISE 3.0-s és újabb verziók, és nem található meg a korábbi verziók.</span><span class="sxs-lookup"><span data-stu-id="91841-123">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>

<span data-ttu-id="91841-124">A csak olvasható tulajdonság, amely lekérdezi a bővítmény eszköz neve.</span><span class="sxs-lookup"><span data-stu-id="91841-124">The read-only property that gets the name of the add-on tool.</span></span>

```powershell
# Gets the name of the visible vertical pane add-on tool.
$psISE.CurrentVisibleVerticalTool.Name
Commands
```

## <a name="see-also"></a><span data-ttu-id="91841-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="91841-125">See Also</span></span>

- [<span data-ttu-id="91841-126">A ISEAddOnToolCollection objektum</span><span class="sxs-lookup"><span data-stu-id="91841-126">The ISEAddOnToolCollection Object</span></span>](The-ISEAddOnToolCollection-Object.md)
- [<span data-ttu-id="91841-127">A Windows PowerShell ISE objektummodell Scripting célja</span><span class="sxs-lookup"><span data-stu-id="91841-127">Purpose of the Windows PowerShell ISE Scripting Object Model</span></span>](Purpose-of-the-Windows-PowerShell-ISE-Scripting-Object-Model.md)
- [<span data-ttu-id="91841-128">Az ISE objektummodell-hierarchiája</span><span class="sxs-lookup"><span data-stu-id="91841-128">The ISE Object Model Hierarchy</span></span>](The-ISE-Object-Model-Hierarchy.md)