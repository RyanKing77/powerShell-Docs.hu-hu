---
title: Széles körű nézetek létrehozásával |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2d4303c5-b451-4ccb-9831-b17a17ceac20
caps.latest.revision: 16
ms.openlocfilehash: 651de5d3bc2619f20438f3951ac5a8c4b0bf46d4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848558"
---
# <a name="creating-a-wide-view"></a><span data-ttu-id="3834f-102">Széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="3834f-102">Creating a Wide View</span></span>

<span data-ttu-id="3834f-103">Egy széles nézetben minden objektum megjelenített egyetlen értéket jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-103">A wide view displays a single value for each object that is displayed.</span></span> <span data-ttu-id="3834f-104">A megjelenített érték lehet egy .NET-objektum tulajdonságának értéke vagy egy parancsfájl értékét.</span><span class="sxs-lookup"><span data-stu-id="3834f-104">The displayed value can be the value of a .NET object property or the value of a script.</span></span> <span data-ttu-id="3834f-105">Alapértelmezés szerint nincs címke vagy fejléc ehhez a nézethez.</span><span class="sxs-lookup"><span data-stu-id="3834f-105">By default, there is no label or header for this view.</span></span>

## <a name="a-wide-view-display"></a><span data-ttu-id="3834f-106">Egy széles nézet megjelenítése</span><span class="sxs-lookup"><span data-stu-id="3834f-106">A Wide View Display</span></span>

<span data-ttu-id="3834f-107">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) által visszaadott objektum a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmagot, ha a kimenetet eredményez a [ Formátum kiterjedő](/powershell/module/Microsoft.PowerShell.Utility/Format-Wide) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="3834f-107">The following example shows how Windows PowerShell displays the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object that is returned by the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet when its output is piped to the [Format-Wide](/powershell/module/Microsoft.PowerShell.Utility/Format-Wide) cmdlet.</span></span> <span data-ttu-id="3834f-108">(Alapértelmezés szerint a [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) parancsmag adja vissza egy táblázat nézet.) Ebben a példában a két oszlop segítségével a folyamat minden visszaadott objektum neve jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-108">(By default, the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet returns a table view.) In this example, the two columns are used to display the name of the process for each returned object.</span></span> <span data-ttu-id="3834f-109">Az objektum tulajdonság neve nem jelenik meg, csak a tulajdonság értékét.</span><span class="sxs-lookup"><span data-stu-id="3834f-109">The name of the object's property is not displayed, only the value of the property.</span></span>

```
Get-Process | format-wide
AEADISRV                     agrsmsvc
Ati2evxx                     Ati2evxx
audiodg                      CCC
CcmExec                      communicator
Crypserv                     csrss
csrss                        DevDtct2
DM1Service                   dpupdchk
dwm                          DxStudio
EXCEL                        explorer
GoogleToolbarNotifier        GrooveMonitor
hpqwmiex                     hpservice
Idle                         InoRpc
InoRT                        InoTask
ipoint                       lsass
lsm                          MOM
MSASCui                      notepad
...                          ...

```

## <a name="defining-the-wide-view"></a><span data-ttu-id="3834f-110">A széles nézet definiálása</span><span class="sxs-lookup"><span data-stu-id="3834f-110">Defining the Wide View</span></span>

<span data-ttu-id="3834f-111">A következő XML formátumú széles nézet sémáját jeleníti meg a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="3834f-111">The following XML shows the wide view schema for the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
View>
  <Name>process</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <GroupBy>...</GroupBy>
  <Controls>...</Controls>
  <WideControl>
    <WideEntries>
      <WideEntry>
        <WideItem>
          <PropertyName>ProcessName</PropertyName>
        </WideItem>
      </WideEntry>
    </WideEntries>
  </WideControl>
</View>

```

<span data-ttu-id="3834f-112">A következő XML-elemeket egy széles nézet meghatározásához használják:</span><span class="sxs-lookup"><span data-stu-id="3834f-112">The following XML elements are used to define a wide view:</span></span>

- <span data-ttu-id="3834f-113">A [nézet](./view-element-format.md) elem a szülőelemet, a széles nézet.</span><span class="sxs-lookup"><span data-stu-id="3834f-113">The [View](./view-element-format.md) element is the parent element of the wide view.</span></span> <span data-ttu-id="3834f-114">(Ez a táblázat, lista, és egyéni vezérlő nézetek az ugyanazon szülőelem.)</span><span class="sxs-lookup"><span data-stu-id="3834f-114">(This is the same parent element for the table, list, and custom control views.)</span></span>

- <span data-ttu-id="3834f-115">A [neve](./name-element-for-view-format.md) elem azt határozza meg a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="3834f-115">The [Name](./name-element-for-view-format.md) element specifies the name of the view.</span></span> <span data-ttu-id="3834f-116">Ehhez az elemhez kötelező megadni az összes nézetben megtekinthetők.</span><span class="sxs-lookup"><span data-stu-id="3834f-116">This element is required for all views.</span></span>

- <span data-ttu-id="3834f-117">A [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja az objektumok, amelyek a nézetet.</span><span class="sxs-lookup"><span data-stu-id="3834f-117">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines the objects that use the view.</span></span> <span data-ttu-id="3834f-118">Ez az elem megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-118">This element is required.</span></span>

- <span data-ttu-id="3834f-119">A [GroupBy](./groupby-element-for-view-format.md) elem határozza meg, ha az objektumok egy új csoport megjelenik.</span><span class="sxs-lookup"><span data-stu-id="3834f-119">The [GroupBy](./groupby-element-for-view-format.md) element defines when a new group of objects is displayed.</span></span> <span data-ttu-id="3834f-120">Egy új csoportot, ha az érték egy adott tulajdonságra vagy parancsfájl el van indítva.</span><span class="sxs-lookup"><span data-stu-id="3834f-120">A new group is started whenever the value of a specific property or script changes.</span></span> <span data-ttu-id="3834f-121">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-121">This element is optional.</span></span>

- <span data-ttu-id="3834f-122">A [vezérlők](./controls-element-for-view-format.md) elemek határozza meg az egyéni vezérlők, a széles nézet által meghatározott.</span><span class="sxs-lookup"><span data-stu-id="3834f-122">The [Controls](./controls-element-for-view-format.md) elements defines the custom controls that are defined by the wide view.</span></span> <span data-ttu-id="3834f-123">Vezérlők további adja meg, hogyan jelenjen meg az adatokat egy módot biztosít.</span><span class="sxs-lookup"><span data-stu-id="3834f-123">Controls give you a way to further specify how the data is displayed.</span></span> <span data-ttu-id="3834f-124">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-124">This element is optional.</span></span> <span data-ttu-id="3834f-125">Nézet definiálhat a saját egyéni vezérlők, vagy telepítheti a nézeten a formázási fájlban használt Gyakori vezérlők.</span><span class="sxs-lookup"><span data-stu-id="3834f-125">A view can define its own custom controls, or it can use common controls that can be used by any view in the formatting file.</span></span> <span data-ttu-id="3834f-126">Egyéni vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-126">For more information about custom controls, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

- <span data-ttu-id="3834f-127">A [WideControl](./widecontrol-element-format.md) elem, és gyermekelemeinek határozza meg a nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-127">The [WideControl](./widecontrol-element-format.md) element and its child elements define what is displayed in the view.</span></span> <span data-ttu-id="3834f-128">Az előző példában a nézet célja, hogy megjeleníti a [System.Diagnostics.Process.Processname](/dotnet/api/System.Diagnostics.Process.ProcessName) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3834f-128">In the preceding example, the view is designed to display the [System.Diagnostics.Process.Processname](/dotnet/api/System.Diagnostics.Process.ProcessName) property.</span></span>

<span data-ttu-id="3834f-129">Egy példa egy teljes formázási fájl, amely meghatározza egy egyszerű széles nézet: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-129">For an example of a complete formatting file that defines a simple wide view, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="providing-definitions-for-your-wide-view"></a><span data-ttu-id="3834f-130">Így a széles nézet definíciói</span><span class="sxs-lookup"><span data-stu-id="3834f-130">Providing Definitions for Your Wide View</span></span>

<span data-ttu-id="3834f-131">Széles körű nézetek biztosíthat egy vagy több definíciót alárendelt elemeinek használatával a [WideControl](./widecontrol-element-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="3834f-131">Wide views can provide one or more definitions by using the child elements of the [WideControl](./widecontrol-element-format.md) element.</span></span> <span data-ttu-id="3834f-132">Nézet általában csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="3834f-132">Typically, a view will have only one definition.</span></span> <span data-ttu-id="3834f-133">A következő példában a nézetet biztosít, amelyek értékét jeleníti meg egyetlen meghatározást az [System.Diagnostics.Process.Processname](/dotnet/api/System.Diagnostics.Process.ProcessName) tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3834f-133">In the following example, the view provides a single definition that displays the value of the [System.Diagnostics.Process.Processname](/dotnet/api/System.Diagnostics.Process.ProcessName) property.</span></span> <span data-ttu-id="3834f-134">Egy széles nézet megjelenítheti egy tulajdonság értékét, vagy egy parancsfájl (a példában nem látható) értékét.</span><span class="sxs-lookup"><span data-stu-id="3834f-134">A wide view can display the value of a property or the value of a script (not shown in the example).</span></span>

```xml
<WideControl>
  <AutoSize/>
  <ColumnNumber></ColumnNumber>
  <WideEntries>
    <WideEntry>
      <WideItem>
        <PropertyName>ProcessName</PropertyName>
      </WideItem>
    </WideEntry>
  </WideEntries>
</WideControl>
```

<span data-ttu-id="3834f-135">A következő XML-elemeket adjon meg egy széles nézet definíciói használható:</span><span class="sxs-lookup"><span data-stu-id="3834f-135">The following XML elements can be used to provide definitions for a wide view:</span></span>

- <span data-ttu-id="3834f-136">A [WideControl](./widecontrol-element-format.md) elem, és gyermekelemeinek határozza meg a nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-136">The [WideControl](./widecontrol-element-format.md) element and its child elements define what is displayed in the view.</span></span>

- <span data-ttu-id="3834f-137">A [AutoSize](./autosize-element-for-widecontrol-format.md) elem azt határozza meg, hogy az oszlop méretét és az oszlopok számát módosulnak az adatok mérete alapján.</span><span class="sxs-lookup"><span data-stu-id="3834f-137">The [AutoSize](./autosize-element-for-widecontrol-format.md) element specifies whether the column size and the number of columns are adjusted based on the size of the data.</span></span> <span data-ttu-id="3834f-138">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-138">This element is optional.</span></span>

- <span data-ttu-id="3834f-139">A [ColumnNumber](./columnnumber-element-for-widecontrol-format.md) elem azt határozza meg, a széles nézetben megjelenített oszlopok számát.</span><span class="sxs-lookup"><span data-stu-id="3834f-139">The [ColumnNumber](./columnnumber-element-for-widecontrol-format.md) element specifies the number of columns displayed in the wide view.</span></span> <span data-ttu-id="3834f-140">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-140">This element is optional.</span></span>

- <span data-ttu-id="3834f-141">A [WideEntries](./wideentries-element-for-widecontrol-format.md) elem a nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="3834f-141">The [WideEntries](./wideentries-element-for-widecontrol-format.md) element provides the definitions of the view.</span></span> <span data-ttu-id="3834f-142">A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="3834f-142">In most cases, a view will have only one definition.</span></span> <span data-ttu-id="3834f-143">Ez az elem megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-143">This element is required.</span></span>

- <span data-ttu-id="3834f-144">A [WideEntry](./wideentry-element-for-widecontrol-format.md) elem biztosít a nézet definíciójának.</span><span class="sxs-lookup"><span data-stu-id="3834f-144">The [WideEntry](./wideentry-element-for-widecontrol-format.md) element provides a definition of the view.</span></span> <span data-ttu-id="3834f-145">Legalább egy [WideEntry](./wideentry-element-for-widecontrol-format.md) szükséges; azonban nem adhat hozzá elemek számának nincs maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="3834f-145">At least one [WideEntry](./wideentry-element-for-widecontrol-format.md) is required; however, there is no maximum limit to the number of elements that you can add.</span></span> <span data-ttu-id="3834f-146">A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="3834f-146">In most cases, a view will have only one definition.</span></span>

- <span data-ttu-id="3834f-147">A [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elem azt határozza meg az objektumok, amelyek egy adott definíciója szerint jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-147">The [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) element specifies the objects that are displayed by a specific definition.</span></span> <span data-ttu-id="3834f-148">Ez az elem nem kötelező, és csak a több meghatározása során van szükség [WideEntry](./wideentry-element-for-widecontrol-format.md) elemek, amelyek a különböző objektumok megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="3834f-148">This element is optional and is needed only when you define multiple [WideEntry](./wideentry-element-for-widecontrol-format.md) elements that display different objects.</span></span>

- <span data-ttu-id="3834f-149">A [WideItem](./wideitem-element-for-widecontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="3834f-149">The [WideItem](./wideitem-element-for-widecontrol-format.md) element specifies the data that is displayed by the view.</span></span> <span data-ttu-id="3834f-150">Nézetek más típusú szakembereket széles vezérlőelem megjelenítheti csak egy elemet.</span><span class="sxs-lookup"><span data-stu-id="3834f-150">In contrast to other types of views, a wide control can display only one item.</span></span>

- <span data-ttu-id="3834f-151">A [PropertyName](./propertyname-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="3834f-151">The [PropertyName](./propertyname-element-for-wideitem-for-widecontrol-format.md) element specifies the property whose value is displayed by the view.</span></span> <span data-ttu-id="3834f-152">Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-152">You must specify either a property or a script, but you cannot specify both.</span></span>

- <span data-ttu-id="3834f-153">A [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) eleme megadja a parancsprogramot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="3834f-153">The [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) element specifies the script whose value is displayed by the view.</span></span> <span data-ttu-id="3834f-154">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-154">You must specify either a script or a property, but you cannot specify both.</span></span>

- <span data-ttu-id="3834f-155">A [FormatString](./formatstring-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg olyan minta, amely az adatok megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="3834f-155">The [FormatString](./formatstring-element-for-wideitem-for-widecontrol-format.md) element specifies a pattern that is used to display the data.</span></span> <span data-ttu-id="3834f-156">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-156">This element is optional.</span></span>

<span data-ttu-id="3834f-157">Egy teljes formázási fájl, amely meghatározza egy széles nézet definícióját egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-157">For an example of a complete formatting file that defines a wide view definition, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="defining-the-objects-that-use-the-wide-view"></a><span data-ttu-id="3834f-158">Az objektumok, amelyek a számos nézet definiálása</span><span class="sxs-lookup"><span data-stu-id="3834f-158">Defining the Objects That Use the Wide View</span></span>

<span data-ttu-id="3834f-159">Két módon határozza meg, mely a .NET-objektumokká széles nézet használata.</span><span class="sxs-lookup"><span data-stu-id="3834f-159">There are two ways to define which .NET objects use the wide view.</span></span> <span data-ttu-id="3834f-160">Használhatja a [ViewSelectedBy](./viewselectedby-element-format.md) elem jeleníthető meg úgy a nézetet, vagy a definíciókat objektumok használhatja a [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elem határozza meg, hogy mely objektumok szerint jelennek meg a a nézet adott meghatározása.</span><span class="sxs-lookup"><span data-stu-id="3834f-160">You can use the [ViewSelectedBy](./viewselectedby-element-format.md) element to define the objects that can be displayed by all the definitions of the view, or you can use the [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) element to define which objects are displayed by a specific definition of the view.</span></span> <span data-ttu-id="3834f-161">A legtöbb esetben a nézet csak egyetlen definíciót, rendelkezik, ezért általában által meghatározott objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="3834f-161">In most cases, a view has only one definition, so objects are typically defined by the [ViewSelectedBy](./viewselectedby-element-format.md) element.</span></span>

<span data-ttu-id="3834f-162">Az alábbi példa bemutatja, hogyan használatával széles nézetben megjelenített objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) és [TypeName](./typename-element-for-viewselectedby-format.md) elemeket.</span><span class="sxs-lookup"><span data-stu-id="3834f-162">The following example shows how to define the objects that are displayed by the wide view using the [ViewSelectedBy](./viewselectedby-element-format.md) and [TypeName](./typename-element-for-viewselectedby-format.md) elements.</span></span> <span data-ttu-id="3834f-163">Nem korlátozott számú [TypeName](./typename-element-for-viewselectedby-format.md) elemeket, hogy is megadhat, és a sorrendjük nem lényeges.</span><span class="sxs-lookup"><span data-stu-id="3834f-163">There is no limit to the number of [TypeName](./typename-element-for-viewselectedby-format.md) elements that you can specify, and their order is not significant.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <WideControl>...</WideControl>
</View>
```

<span data-ttu-id="3834f-164">A következő XML-elemeket adja meg az objektumokat, a széles nézet által használt használható:</span><span class="sxs-lookup"><span data-stu-id="3834f-164">The following XML elements can be used to specify the objects that are used by the wide view:</span></span>

- <span data-ttu-id="3834f-165">A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a széles nézetben jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-165">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines which objects are displayed by the wide view.</span></span>

- <span data-ttu-id="3834f-166">A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET, amely szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-166">The [TypeName](./typename-element-for-viewselectedby-format.md) element specifies the .NET that is displayed by the view.</span></span> <span data-ttu-id="3834f-167">A teljes .NET típusú név megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-167">The fully qualified .NET type name is required.</span></span> <span data-ttu-id="3834f-168">Meg kell adnia legalább egy típus vagy állítsa be a nézet a kijelölés, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="3834f-168">You must specify at least one type or selection set for the view, but there is no maximum number of elements that can be specified.</span></span>

<span data-ttu-id="3834f-169">Egy teljes formázási fájl egy példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-169">For an example of a complete formatting file, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

<span data-ttu-id="3834f-170">Az alábbi példában a [ViewSelectedBy](./viewselectedby-element-format.md) és [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elemeket.</span><span class="sxs-lookup"><span data-stu-id="3834f-170">The following example uses the [ViewSelectedBy](./viewselectedby-element-format.md) and [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elements.</span></span> <span data-ttu-id="3834f-171">Használja a kijelölt csoportok használatával több nézetet, például amikor egy széles nézet határozza meg, és a táblázatos nézetre a ugyanazon objektumok megjelenített objektumok kapcsolódó készlete esetében.</span><span class="sxs-lookup"><span data-stu-id="3834f-171">Use selection sets where you have a related set of objects that are displayed using multiple views, such as when you define a wide view and a table view for the same objects.</span></span> <span data-ttu-id="3834f-172">Hozzon létre egy kiválasztási kapcsolatos további információkért lásd: [kijelölt csoportok meghatározása](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-172">For more information about how to create a selection set, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <SelectionSetName>.NET Type Set</SelectionSetName>
  </ViewSelectedBy>
  <WideControl>...</WideControl>
</View>
```

<span data-ttu-id="3834f-173">A következő XML-elemeket adja meg az objektumokat, a széles nézet által használt használható:</span><span class="sxs-lookup"><span data-stu-id="3834f-173">The following XML elements can be used to specify the objects that are used by the wide view:</span></span>

- <span data-ttu-id="3834f-174">A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a széles nézetben jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-174">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines which objects are displayed by the wide view.</span></span>

- <span data-ttu-id="3834f-175">A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elem azt határozza meg a nézetben megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="3834f-175">The [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) element specifies a set of objects that can be displayed by the view.</span></span> <span data-ttu-id="3834f-176">Meg kell adnia legalább egy készlet kiválasztása vagy a nézet típusa, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="3834f-176">You must specify at least one selection set or type for the view, but there is no maximum number of elements that can be specified.</span></span>

<span data-ttu-id="3834f-177">Az alábbi példa bemutatja, hogyan adhat meg az objektumokat, a széles nézet használatával egy adott definíciója szerint jelenik meg a [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="3834f-177">The following example shows how to define the objects displayed by a specific definition of the wide view using the [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) element.</span></span> <span data-ttu-id="3834f-178">Ez az elem használatával, megadhatja az objektum, objektumok kiválasztása csoportja, vagy egy kiválasztási feltétel, amely meghatározza a definíció használatakor .NET nevét.</span><span class="sxs-lookup"><span data-stu-id="3834f-178">Using this element, you can specify the .NET type name of the object, a selection set of objects, or a selection condition that specifies when the definition is used.</span></span> <span data-ttu-id="3834f-179">A kiválasztási feltételek létrehozásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-179">For more information about how to create a selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

```xml
<WideEntry>
  <EntrySelectedBy>
    <TypeName>.NET Type</TypeName>
  </EntrySelectedBy>
</WideEntry>
```

<span data-ttu-id="3834f-180">A következő XML-elemeket adja meg az objektumokat, a széles nézet egy adott definíciója által használt használható:</span><span class="sxs-lookup"><span data-stu-id="3834f-180">The following XML elements can be used to specify the objects that are used by a specific definition of the wide view:</span></span>

- <span data-ttu-id="3834f-181">A [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) elem határozza meg, hogy mely objektumok jelennek meg a definíció szerint.</span><span class="sxs-lookup"><span data-stu-id="3834f-181">The [EntrySelectedBy](./entryselectedby-element-for-wideentry-format.md) element defines which objects are displayed by the definition.</span></span>

- <span data-ttu-id="3834f-182">A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET, a definíció szerint jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-182">The [TypeName](./typename-element-for-viewselectedby-format.md) element specifies the .NET that is displayed by the definition.</span></span> <span data-ttu-id="3834f-183">Ez az elem használatakor a teljes .NET típusú nevének megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-183">When using this element the fully qualified .NET type name is required.</span></span> <span data-ttu-id="3834f-184">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="3834f-184">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span>

- <span data-ttu-id="3834f-185">A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) (nem látható) elemet, adja meg a definíció megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="3834f-185">The [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) element (not shown) specifies a set of objects that can be displayed by this definition.</span></span> <span data-ttu-id="3834f-186">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="3834f-186">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span>

- <span data-ttu-id="3834f-187">A [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md) (nem látható) elemet, adja meg egy feltételt, amely a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="3834f-187">The [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md) element (not shown) specifies a condition that must exist for this definition to be used.</span></span> <span data-ttu-id="3834f-188">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="3834f-188">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span> <span data-ttu-id="3834f-189">További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-189">For more information about defining selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="displaying-groups-of-objects-in-a-wide-view"></a><span data-ttu-id="3834f-190">Az objektumok csoportjaihoz széles nézet megjelenítése</span><span class="sxs-lookup"><span data-stu-id="3834f-190">Displaying Groups of objects in a Wide View</span></span>

<span data-ttu-id="3834f-191">Elkülönítheti az objektumokat, a széles körű képet kaphat csoportok szerint jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-191">You can separate the objects that are displayed by the wide view into groups.</span></span> <span data-ttu-id="3834f-192">Ez nem jelenti azt, hogy Ön meghatározott felhasználói csoporttal, csak a Windows PowerShell elindul egy új csoportot, ha az érték egy adott tulajdonságra vagy egy parancsprogramtípusra.</span><span class="sxs-lookup"><span data-stu-id="3834f-192">This does not mean that you define a group, only that Windows PowerShell starts a new group whenever the value of a specific property or script changes.</span></span> <span data-ttu-id="3834f-193">A következő példában elindul egy új csoportot, amikor az értékét a [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) tulajdonságukat módosítják.</span><span class="sxs-lookup"><span data-stu-id="3834f-193">In the following example, a new group is started whenever the value of the [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) property changes.</span></span>

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

<span data-ttu-id="3834f-194">A következő XML-elemeket segítségével határozhatók meg, amikor egy csoportot:</span><span class="sxs-lookup"><span data-stu-id="3834f-194">The following XML elements are used to define when a group is started:</span></span>

- <span data-ttu-id="3834f-195">A [GroupBy](./groupby-element-for-view-format.md) elem definiálja a tulajdonságot vagy parancsfájlt, amely elindítja az új csoporthoz, és határozza meg, hogyan jelenjen meg a csoport.</span><span class="sxs-lookup"><span data-stu-id="3834f-195">The [GroupBy](./groupby-element-for-view-format.md) element defines the property or script that starts the new group and defines how the group is displayed.</span></span>

- <span data-ttu-id="3834f-196">A [PropertyName](./propertyname-element-for-groupby-format.md) elem azt határozza meg a tulajdonság, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="3834f-196">The [PropertyName](./propertyname-element-for-groupby-format.md) element specifies the property that starts a new group whenever its value changes.</span></span> <span data-ttu-id="3834f-197">Adjon meg egy tulajdonságot vagy a parancsfájl a csoport indítása, de mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-197">You must specify a property or script to start the group, but you cannot specify both.</span></span>

- <span data-ttu-id="3834f-198">A [ScriptBlock](./scriptblock-element-for-groupby-format.md) elem azt határozza meg, a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="3834f-198">The [ScriptBlock](./scriptblock-element-for-groupby-format.md) element specifies the script that starts a new group whenever its value changes.</span></span> <span data-ttu-id="3834f-199">Meg kell adnia egy parancsfájl vagy a csoport indítása tulajdonság azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-199">You must specify a script or property to start the group, but you cannot specify both.</span></span>

- <span data-ttu-id="3834f-200">A [címke](./label-element-for-groupby-format.md) elemet definiál egy címke, amely az egyes csoportok elején jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-200">The [Label](./label-element-for-groupby-format.md) element defines a label that is displayed at the beginning of each group.</span></span> <span data-ttu-id="3834f-201">Ez az elem által meghatározott a szöveg mellett Windows PowerShell, amely az új csoport által aktivált, és hozzáad egy üres sort, előtt és után a felirat értékét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="3834f-201">In addition to the text specified by this element, Windows PowerShell displays the value that triggered the new group and adds a blank line before and after the label.</span></span> <span data-ttu-id="3834f-202">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-202">This element is optional.</span></span>

- <span data-ttu-id="3834f-203">A [CustomControl](./customcontrol-element-for-groupby-format.md) elem határozza meg olyan vezérlő, amely az adatok megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="3834f-203">The [CustomControl](./customcontrol-element-for-groupby-format.md) element defines a control that is used to display the data.</span></span> <span data-ttu-id="3834f-204">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-204">This element is optional.</span></span>

- <span data-ttu-id="3834f-205">A [CustomControlName](./customcontrolname-element-for-groupby-format.md) elem azt határozza meg, egy közös vagy megtekintheti a vezérlő, amely az adatok megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="3834f-205">The [CustomControlName](./customcontrolname-element-for-groupby-format.md) element specifies a common or view control that is used to display the data.</span></span> <span data-ttu-id="3834f-206">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="3834f-206">This element is optional.</span></span>

<span data-ttu-id="3834f-207">Egy teljes formázási fájl, amely meghatározza a csoportok egy példa: [széles nézet (GroupBy)](./wide-view-groupby.md).</span><span class="sxs-lookup"><span data-stu-id="3834f-207">For an example of a complete formatting file that defines groups, see [Wide View (GroupBy)](./wide-view-groupby.md).</span></span>

## <a name="using-format-strings"></a><span data-ttu-id="3834f-208">Formázási karakterláncokat használatával</span><span class="sxs-lookup"><span data-stu-id="3834f-208">Using Format Strings</span></span>

<span data-ttu-id="3834f-209">Egy széles nézet még jobban meghatározhatja, hogyan jelenjen meg az adatok formázási karakterláncokat is hozzáadhatók.</span><span class="sxs-lookup"><span data-stu-id="3834f-209">Formatting strings can be added to a wide view to further define how the data is displayed.</span></span> <span data-ttu-id="3834f-210">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="3834f-210">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<WideItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</WideItem>
```

<span data-ttu-id="3834f-211">A következő XML-elemeket segítségével adjon meg egy Formátumminta:</span><span class="sxs-lookup"><span data-stu-id="3834f-211">The following XML elements can be used to specify a format pattern:</span></span>

- <span data-ttu-id="3834f-212">A [WideItem](./wideitem-element-for-widecontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="3834f-212">The [WideItem](./wideitem-element-for-widecontrol-format.md) element specifies the data that is displayed by the view.</span></span>

- <span data-ttu-id="3834f-213">A [PropertyName](./propertyname-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="3834f-213">The [PropertyName](./propertyname-element-for-wideitem-for-widecontrol-format.md) element specifies the property whose value is displayed by the view.</span></span> <span data-ttu-id="3834f-214">Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-214">You must specify either a property or a script, but you cannot specify both.</span></span>

- <span data-ttu-id="3834f-215">A [FormatString](./formatstring-element-for-wideitem-for-widecontrol-format.md) elem azt határozza meg, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben egy Formátumminta</span><span class="sxs-lookup"><span data-stu-id="3834f-215">The [FormatString](./formatstring-element-for-wideitem-for-widecontrol-format.md) element specifies a format pattern that defines how the property or script value is displayed in the view</span></span>

- <span data-ttu-id="3834f-216">A [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="3834f-216">The [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) element (not shown) specifies the script whose value is displayed by the view.</span></span> <span data-ttu-id="3834f-217">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-217">You must specify either a script or a property, but you cannot specify both.</span></span>

<span data-ttu-id="3834f-218">A következő példában a `ToString` módszert hívja meg a parancsfájl értékének.</span><span class="sxs-lookup"><span data-stu-id="3834f-218">In the following example, the `ToString` method is called to format the value of the script.</span></span> <span data-ttu-id="3834f-219">Parancsprogramok segítségével meghívhatja a bármely metódusát meghívná, egy objektumot.</span><span class="sxs-lookup"><span data-stu-id="3834f-219">Scripts can call any method of an object.</span></span> <span data-ttu-id="3834f-220">Ezért ha egy objektum tartozik egy módszer, például `ToString`, van formázási paramétereket, a parancsfájl segítségével meghívhatja a módszer a parancsfájl kimenete értékének.</span><span class="sxs-lookup"><span data-stu-id="3834f-220">Therefore, if an object has a method, such as `ToString`, that has formatting parameters, the script can call that method to format the output value of the script.</span></span>

```xml
<WideItem>
  <ScriptBlock>
    [String}::Format("(0,10) (1,8)", .LastWriteTime.ToString("d"),
    $_.LastWriteTime.Totring("t"))
  </ScriptBlock>
</WideItem>
```

<span data-ttu-id="3834f-221">A következő XML-elem segítségével hívása a `ToString` módszer:</span><span class="sxs-lookup"><span data-stu-id="3834f-221">The following XML element can be used to calling the `ToString` method:</span></span>

- <span data-ttu-id="3834f-222">A [WideItem](./wideitem-element-for-widecontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="3834f-222">The [WideItem](./wideitem-element-for-widecontrol-format.md) element specifies the data that is displayed by the view.</span></span>

- <span data-ttu-id="3834f-223">A [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="3834f-223">The [ScriptBlock](./scriptblock-element-for-wideitem-for-widecontrol-format.md) element (not shown) specifies the script whose value is displayed by the view.</span></span> <span data-ttu-id="3834f-224">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="3834f-224">You must specify either a script or a property, but you cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="3834f-225">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3834f-225">See Also</span></span>

[<span data-ttu-id="3834f-226">Széles nézet (alapszintű)</span><span class="sxs-lookup"><span data-stu-id="3834f-226">Wide View (Basic)</span></span>](./wide-view-basic.md)

[<span data-ttu-id="3834f-227">Széles nézet (GroupBy)</span><span class="sxs-lookup"><span data-stu-id="3834f-227">Wide View (GroupBy)</span></span>](./wide-view-groupby.md)

[<span data-ttu-id="3834f-228">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="3834f-228">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
