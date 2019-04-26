---
title: Lista nézet létrehozásával |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8c7a40ca-1786-46f0-bab5-6ce229daa7ee
caps.latest.revision: 14
ms.openlocfilehash: 25d24063501196d44e0f806a55bb699c82f771ce
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066855"
---
# <a name="creating-a-list-view"></a><span data-ttu-id="4d761-102">Listanézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="4d761-102">Creating a List View</span></span>

<span data-ttu-id="4d761-103">A listanézet csak egy oszlop (sorrendben) adatokat jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-103">A list view displays data in a single column (in sequential order).</span></span> <span data-ttu-id="4d761-104">A listán megjelenített adatok lehetnek, a .NET-tulajdonság értéke, vagy egy parancsfájl értékét.</span><span class="sxs-lookup"><span data-stu-id="4d761-104">The data displayed in the list can be the value of a .NET property or the value of a script.</span></span>

## <a name="a-list-view-display"></a><span data-ttu-id="4d761-105">A lista nézet megjelenítése</span><span class="sxs-lookup"><span data-stu-id="4d761-105">A List View Display</span></span>

<span data-ttu-id="4d761-106">A következő kimenetet jeleníti meg, hogyan jeleníti meg a Windows PowerShell tulajdonságainak [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektumok a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="4d761-106">The following output shows how Windows PowerShell displays the properties of [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects that are returned by the [Get-Service](/powershell/module/microsoft.powershell.management/get-service) cmdlet.</span></span> <span data-ttu-id="4d761-107">Ebben a példában három objektumot adott vissza, az előző objektum különíteni egy üres sor minden objektumot.</span><span class="sxs-lookup"><span data-stu-id="4d761-107">In this example, three objects were returned, with each object separated from the preceding object by a blank line.</span></span>

```powershell
Get-Service | format-list
```

```output
Name                : AEADIFilters
DisplayName         : Andrea ADI Filters Service
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess

Name                : AeLookupSvc
DisplayName         : Application Experience
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32ShareProcess

Name                : AgereModemAudio
DisplayName         : Agere Modem Call Progress Audio
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess
...
```

## <a name="defining-the-list-view"></a><span data-ttu-id="4d761-108">A lista nézet definiálása</span><span class="sxs-lookup"><span data-stu-id="4d761-108">Defining the List View</span></span>

<span data-ttu-id="4d761-109">A következő XML formátumú jeleníti meg a lista nézet séma számos tulajdonságainak megjelenítése a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="4d761-109">The following XML shows the list view schema for displaying several properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span> <span data-ttu-id="4d761-110">Meg kell adnia, hogy a nézetben megjeleníteni kívánt minden egyes tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4d761-110">You must specify each property that you want displayed in the list view.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>
          <ListItem>
            <PropertyName>Name</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>DisplayName</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>Status</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>ServiceType</PropertyName>
          </ListItem>
        </ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>
</View>
```

<span data-ttu-id="4d761-111">A következő XML-elemeket a lista nézet meghatározásához használják:</span><span class="sxs-lookup"><span data-stu-id="4d761-111">The following XML elements are used to define a list view:</span></span>

- <span data-ttu-id="4d761-112">A [nézet](./view-element-format.md) elem a lista nézet a szülőelemet.</span><span class="sxs-lookup"><span data-stu-id="4d761-112">The [View](./view-element-format.md) element is the parent element of the list view.</span></span> <span data-ttu-id="4d761-113">(Ez a táblához, széles és az egyéni vezérlő nézetek az ugyanazon szülőelem.)</span><span class="sxs-lookup"><span data-stu-id="4d761-113">(This is the same parent element for the table, wide, and custom control views.)</span></span>

- <span data-ttu-id="4d761-114">A [neve](./name-element-for-view-format.md) elem azt határozza meg a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="4d761-114">The [Name](./name-element-for-view-format.md) element specifies the name of the view.</span></span> <span data-ttu-id="4d761-115">Ehhez az elemhez kötelező megadni az összes nézetben megtekinthetők.</span><span class="sxs-lookup"><span data-stu-id="4d761-115">This element is required for all views.</span></span>

- <span data-ttu-id="4d761-116">A [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja az objektumok, amelyek a nézetet.</span><span class="sxs-lookup"><span data-stu-id="4d761-116">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines the objects that use the view.</span></span> <span data-ttu-id="4d761-117">Ez az elem megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-117">This element is required.</span></span>

- <span data-ttu-id="4d761-118">A [GroupBy](./groupby-element-for-view-format.md) elem határozza meg, ha az objektumok egy új csoport megjelenik.</span><span class="sxs-lookup"><span data-stu-id="4d761-118">The [GroupBy](./groupby-element-for-view-format.md) element defines when a new group of objects is displayed.</span></span> <span data-ttu-id="4d761-119">Egy új csoportot, ha az érték egy adott tulajdonságra vagy parancsfájl el van indítva.</span><span class="sxs-lookup"><span data-stu-id="4d761-119">A new group is started whenever the value of a specific property or script changes.</span></span> <span data-ttu-id="4d761-120">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-120">This element is optional.</span></span>

- <span data-ttu-id="4d761-121">A [vezérlők](./controls-element-for-view-format.md) elem definiálja az egyéni vezérlők, a lista nézet által meghatározott.</span><span class="sxs-lookup"><span data-stu-id="4d761-121">The [Controls](./controls-element-for-view-format.md) element defines the custom controls that are defined by the list view.</span></span> <span data-ttu-id="4d761-122">Vezérlők további adja meg, hogyan jelenjen meg az adatokat egy módot biztosít.</span><span class="sxs-lookup"><span data-stu-id="4d761-122">Controls give you a way to further specify how the data is displayed.</span></span> <span data-ttu-id="4d761-123">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-123">This element is optional.</span></span> <span data-ttu-id="4d761-124">Nézet definiálhat a saját egyéni vezérlők, vagy telepítheti a nézeten a formázási fájlban használt Gyakori vezérlők.</span><span class="sxs-lookup"><span data-stu-id="4d761-124">A view can define its own custom controls, or it can use common controls that can be used by any view in the formatting file.</span></span> <span data-ttu-id="4d761-125">Egyéni vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-125">For more information about custom controls, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

- <span data-ttu-id="4d761-126">A [ListControl](./listcontrol-element-format.md) elem definiálja a nézetben jelenik meg, és hogyan van formázva.</span><span class="sxs-lookup"><span data-stu-id="4d761-126">The [ListControl](./listcontrol-element-format.md) element defines what is displayed in the view and how it is formatted.</span></span> <span data-ttu-id="4d761-127">Minden más nézetekhez hasonlóan, a listanézet jeleníthet meg az objektum tulajdonságainak vagy szkript által létrehozott értékek.</span><span class="sxs-lookup"><span data-stu-id="4d761-127">Similar to all other views, a list view can display the values of object properties or values generated by script.</span></span>

<span data-ttu-id="4d761-128">Egy példa egy teljes formázási fájl, amely meghatározza egy egyszerű lista nézet: [listanézet (alapszintű)](./list-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-128">For an example of a complete formatting file that defines a simple list view, see [List View (Basic)](./list-view-basic.md).</span></span>

## <a name="providing-definitions-for-your-list-view"></a><span data-ttu-id="4d761-129">Így a lista nézet definíciói</span><span class="sxs-lookup"><span data-stu-id="4d761-129">Providing Definitions for Your List View</span></span>

<span data-ttu-id="4d761-130">Listanézetek biztosíthat egy vagy több definíciót alárendelt elemeinek használatával a [ListControl](./listcontrol-element-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="4d761-130">List views can provide one or more definitions by using the child elements of the [ListControl](./listcontrol-element-format.md) element.</span></span> <span data-ttu-id="4d761-131">Nézet általában csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="4d761-131">Typically, a view will have only one definition.</span></span> <span data-ttu-id="4d761-132">A következő példában a nézetet biztosít egy egyetlen definíciót, amely számos tulajdonságát megjeleníti a [System.Diagnostics.Process? Displayproperty = Fullname](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="4d761-132">In the following example, the view provides a single definition that displays several properties of the [System.Diagnostics.Process?Displayproperty=Fullname](/dotnet/api/System.Diagnostics.Process) object.</span></span> <span data-ttu-id="4d761-133">A listanézet megjelenítheti egy tulajdonság értékét, vagy egy parancsfájl (a példában nem látható) értékét.</span><span class="sxs-lookup"><span data-stu-id="4d761-133">A list view can display the value of a property or the value of a script (not shown in the example).</span></span>

```xml
<ListControl>
    <ListEntries>
      <ListEntry>
        <ListItems>
          <ListItem>
            <PropertyName>Name</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>DisplayName</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>Status</PropertyName>
          </ListItem>
          <ListItem>
            <PropertyName>ServiceType</PropertyName>
          </ListItem>
        </ListItems>
      </ListEntry>
    </ListEntries>
  </ListControl>

```

<span data-ttu-id="4d761-134">A következő XML-elemeket adja meg az adott nézet definíciói használható:</span><span class="sxs-lookup"><span data-stu-id="4d761-134">The following XML elements can be used to provide definitions for a list view:</span></span>

- <span data-ttu-id="4d761-135">A [ListControl](./listcontrol-element-format.md) elem, és gyermekelemeinek határozza meg a nézetben jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-135">The [ListControl](./listcontrol-element-format.md) element and its child elements define what is displayed in the view.</span></span>

- <span data-ttu-id="4d761-136">A [ListEntries](./listentries-element-for-listcontrol-format.md) elem a nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="4d761-136">The [ListEntries](./listentries-element-for-listcontrol-format.md) element provides the definitions of the view.</span></span> <span data-ttu-id="4d761-137">A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="4d761-137">In most cases, a view will have only one definition.</span></span> <span data-ttu-id="4d761-138">Ez az elem megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-138">This element is required.</span></span>

- <span data-ttu-id="4d761-139">A [ListEntry](./listentry-element-for-listcontrol-format.md) elem biztosít a nézet definíciójának.</span><span class="sxs-lookup"><span data-stu-id="4d761-139">The [ListEntry](./listentry-element-for-listcontrol-format.md) element provides a definition of the view.</span></span> <span data-ttu-id="4d761-140">Legalább egy [ListEntry](./listentry-element-for-listcontrol-format.md) szükséges; azonban nem adhat hozzá elemek számának nincs maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="4d761-140">At least one [ListEntry](./listentry-element-for-listcontrol-format.md) is required; however, there is no maximum limit to the number of elements that you can add.</span></span> <span data-ttu-id="4d761-141">A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="4d761-141">In most cases, a view will have only one definition.</span></span>

- <span data-ttu-id="4d761-142">A [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem azt határozza meg az objektumok, amelyek egy adott definíciója szerint jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-142">The [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) element specifies the objects that are displayed by a specific definition.</span></span> <span data-ttu-id="4d761-143">Ez az elem nem kötelező, és csak a több meghatározása során van szükség [ListEntry](./listentry-element-for-listcontrol-format.md) elemek, amelyek a különböző objektumok megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="4d761-143">This element is optional and is needed only when you define multiple [ListEntry](./listentry-element-for-listcontrol-format.md) elements that display different objects.</span></span>

- <span data-ttu-id="4d761-144">A [ListItems elemek](./listitems-element-for-listentry-for-listcontrol-format.md) elem azt határozza meg, a tulajdonságok és a parancsfájlok, melynek értékei jelennek meg a listanézet sorait.</span><span class="sxs-lookup"><span data-stu-id="4d761-144">The [ListItems](./listitems-element-for-listentry-for-listcontrol-format.md) element specifies the properties and scripts whose values are displayed in the rows of the list view.</span></span>

- <span data-ttu-id="4d761-145">A [ListItem](./listitems-element-for-listentry-for-listcontrol-format.md) elem azt határozza meg, egy tulajdonságot vagy parancsfájl, amelynek értéke megjelenik a lista nézet sorban.</span><span class="sxs-lookup"><span data-stu-id="4d761-145">The [ListItem](./listitems-element-for-listentry-for-listcontrol-format.md) element specifies a property or script whose value is displayed in a row of the list view.</span></span> <span data-ttu-id="4d761-146">A listanézet adjon meg legalább egy tulajdonságot vagy parancsfájlt.</span><span class="sxs-lookup"><span data-stu-id="4d761-146">A list view must specify at least one property or script.</span></span> <span data-ttu-id="4d761-147">Nincs maximális megadható sorok száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="4d761-147">There is no maximum limit to the number of rows that can be specified.</span></span>

- <span data-ttu-id="4d761-148">A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="4d761-148">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element specifies the property whose value is displayed in the row.</span></span> <span data-ttu-id="4d761-149">Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-149">You must specify either a property or a script, but you cannot specify both.</span></span>

- <span data-ttu-id="4d761-150">A [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elem megadja a parancsprogramot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="4d761-150">The [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) element specifies the script whose value is displayed in the row.</span></span> <span data-ttu-id="4d761-151">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-151">You must specify either a script or a property, but you cannot specify both.</span></span>

- <span data-ttu-id="4d761-152">A [címke](./label-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg a címke bal oldalán a tulajdonság, vagy parancsprogram érték sorában megjelenik.</span><span class="sxs-lookup"><span data-stu-id="4d761-152">The [Label](./label-element-for-listitem-for-listcontrol-format.md) element specifies the label that is displayed to the left of the property or script value in the row.</span></span> <span data-ttu-id="4d761-153">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-153">This element is optional.</span></span> <span data-ttu-id="4d761-154">Ha nincs megadva címke, a tulajdonság, vagy a parancsfájl neve jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-154">If a label is not specified, the name of the property or the script is displayed.</span></span> <span data-ttu-id="4d761-155">Egy teljes példa: [listanézet (címkék)](./list-view-labels.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-155">For a complete example, see [List View (Labels)](./list-view-labels.md).</span></span>

- <span data-ttu-id="4d761-156">A [ItemSelectionCondition](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg egy feltételt, amely a megjeleníteni kívánt sor léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="4d761-156">The [ItemSelectionCondition](./itemselectioncondition-element-for-listitem-for-listcontrol-format.md) element specifies a condition that must exist for the row to be displayed.</span></span> <span data-ttu-id="4d761-157">A listanézet feltételek hozzáadásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-157">For more information about adding conditions to the list view, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span> <span data-ttu-id="4d761-158">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-158">This element is optional.</span></span>

- <span data-ttu-id="4d761-159">A [FormatString](./formatstring-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg, amellyel meg az értéket a tulajdonság vagy parancsfájl mintát.</span><span class="sxs-lookup"><span data-stu-id="4d761-159">The [FormatString](./formatstring-element-for-listitem-for-listcontrol-format.md) element specifies a pattern that is used to display the value of the property or script.</span></span> <span data-ttu-id="4d761-160">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-160">This element is optional.</span></span>

<span data-ttu-id="4d761-161">Egy példa egy teljes formázási fájl, amely meghatározza egy egyszerű lista nézet: [listanézet (alapszintű)](./list-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-161">For an example of a complete formatting file that defines a simple list view, see [List View (Basic)](./list-view-basic.md).</span></span>

## <a name="defining-the-objects-that-use-the-list-view"></a><span data-ttu-id="4d761-162">Az objektumok, amelyek a lista nézet definiálása</span><span class="sxs-lookup"><span data-stu-id="4d761-162">Defining the Objects That Use the List View</span></span>

<span data-ttu-id="4d761-163">Két módon határozza meg, melyik .NET-objektumokat a listanézetet használja.</span><span class="sxs-lookup"><span data-stu-id="4d761-163">There are two ways to define which .NET objects use the list view.</span></span> <span data-ttu-id="4d761-164">Használhatja a [ViewSelectedBy](./viewselectedby-element-format.md) elem jeleníthető meg úgy a nézetet, vagy a definíciókat objektumok használhatja a [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem határozza meg, hogy mely objektumok szerint jelennek meg a a nézet adott meghatározása.</span><span class="sxs-lookup"><span data-stu-id="4d761-164">You can use the [ViewSelectedBy](./viewselectedby-element-format.md) element to define the objects that can be displayed by all the definitions of the view, or you can use the [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) element to define which objects are displayed by a specific definition of the view.</span></span> <span data-ttu-id="4d761-165">A legtöbb esetben a nézet csak egyetlen definíciót, rendelkezik, ezért általában által meghatározott objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="4d761-165">In most cases, a view has only one definition, so objects are typically defined by the [ViewSelectedBy](./viewselectedby-element-format.md) element.</span></span>

<span data-ttu-id="4d761-166">Az alábbi példa bemutatja, hogyan jelennek meg a lista nézet használatával objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) és [TypeName](./typename-element-for-viewselectedby-format.md) elemeket.</span><span class="sxs-lookup"><span data-stu-id="4d761-166">The following example shows how to define the objects that are displayed by the list view using the [ViewSelectedBy](./viewselectedby-element-format.md) and [TypeName](./typename-element-for-viewselectedby-format.md) elements.</span></span> <span data-ttu-id="4d761-167">Nem korlátozott számú [TypeName](./typename-element-for-viewselectedby-format.md) elemeket, hogy is megadhat, és a sorrendjük nem lényeges.</span><span class="sxs-lookup"><span data-stu-id="4d761-167">There is no limit to the number of [TypeName](./typename-element-for-viewselectedby-format.md) elements that you can specify, and their order is not significant.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

<span data-ttu-id="4d761-168">A következő XML-elemeket adja meg az objektumokat a listanézet által használt használható:</span><span class="sxs-lookup"><span data-stu-id="4d761-168">The following XML elements can be used to specify the objects that are used by the list view:</span></span>

- <span data-ttu-id="4d761-169">A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-169">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines which objects are displayed by the list view.</span></span>

- <span data-ttu-id="4d761-170">A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET-objektum, amely szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-170">The [TypeName](./typename-element-for-viewselectedby-format.md) element specifies the .NET object that is displayed by the view.</span></span> <span data-ttu-id="4d761-171">A teljes .NET típusú név megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-171">The fully qualified .NET type name is required.</span></span> <span data-ttu-id="4d761-172">Meg kell adnia legalább egy típus vagy állítsa be a nézet a kijelölés, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="4d761-172">You must specify at least one type or selection set for the view, but there is no maximum number of elements that can be specified.</span></span>

<span data-ttu-id="4d761-173">Egy teljes formázási fájl egy példa: [listanézet (alapszintű)](./list-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-173">For an example of a complete formatting file, see [List View (Basic)](./list-view-basic.md).</span></span>

<span data-ttu-id="4d761-174">Az alábbi példában a [ViewSelectedBy](./viewselectedby-element-format.md) és [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elemeket.</span><span class="sxs-lookup"><span data-stu-id="4d761-174">The following example uses the [ViewSelectedBy](./viewselectedby-element-format.md) and [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elements.</span></span> <span data-ttu-id="4d761-175">Kijelölt csoportok használata több nézetet, például a lista nézetben definiált és a táblázatos nézetre használata ugyanazokat a megjelenített objektumok kapcsolódó készlete esetében.</span><span class="sxs-lookup"><span data-stu-id="4d761-175">Use selection sets where you have a related set of objects that are displayed using multiple views, such as when you define a list view and a table view for the same objects.</span></span> <span data-ttu-id="4d761-176">Hozzon létre egy kiválasztási kapcsolatos további információkért lásd: [kijelölt csoportok meghatározása](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-176">For more information about how to create a selection set, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <SelectionSetName>.NET Type Set</SelectionSetName>
  </ViewSelectedBy>
  <ListControl>...</ListControl>
</View>
```

<span data-ttu-id="4d761-177">A következő XML-elemeket adja meg az objektumokat a listanézet által használt használható:</span><span class="sxs-lookup"><span data-stu-id="4d761-177">The following XML elements can be used to specify the objects that are used by the list view:</span></span>

- <span data-ttu-id="4d761-178">A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-178">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines which objects are displayed by the list view.</span></span>

- <span data-ttu-id="4d761-179">A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elem azt határozza meg a nézetben megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="4d761-179">The [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) element specifies a set of objects that can be displayed by the view.</span></span> <span data-ttu-id="4d761-180">Meg kell adnia legalább egy készlet kiválasztása vagy a nézet típusa, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="4d761-180">You must specify at least one selection set or type for the view, but there is no maximum number of elements that can be specified.</span></span>

<span data-ttu-id="4d761-181">Az alábbi példa bemutatja, hogyan adhat meg az objektumok egy adott lista nézet használatával definíciója szerint jelenik meg a [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="4d761-181">The following example shows how to define the objects displayed by a specific definition of the list view using the [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) element.</span></span> <span data-ttu-id="4d761-182">Ez az elem használatával, megadhatja az objektum, objektumok kiválasztása csoportja, vagy egy kiválasztási feltétel, amely meghatározza a definíció használatakor .NET nevét.</span><span class="sxs-lookup"><span data-stu-id="4d761-182">Using this element, you can specify the .NET type name of the object, a selection set of objects, or a selection condition that specifies when the definition is used.</span></span> <span data-ttu-id="4d761-183">A kiválasztási feltételek létrehozásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-183">For more information about how to create a selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>.NET Type</TypeName>
  </EntrySelectedBy>
</ListEntry>
```

<span data-ttu-id="4d761-184">A következő XML-elemeket adja meg az objektumokat a listanézet adott definíciójának által használt használható:</span><span class="sxs-lookup"><span data-stu-id="4d761-184">The following XML elements can be used to specify the objects that are used by a specific definition of the list view:</span></span>

- <span data-ttu-id="4d761-185">A [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem határozza meg, hogy mely objektumok jelennek meg a definíció szerint.</span><span class="sxs-lookup"><span data-stu-id="4d761-185">The [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) element defines which objects are displayed by the definition.</span></span>

- <span data-ttu-id="4d761-186">A [TypeName](./typename-element-for-entryselectedby-for-listcontrol-format.md) elem azt határozza meg a .NET-objektum, amely a definíció szerint jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-186">The [TypeName](./typename-element-for-entryselectedby-for-listcontrol-format.md) element specifies the .NET object that is displayed by the definition.</span></span> <span data-ttu-id="4d761-187">Ez az elem használatakor a teljes .NET típusú név megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-187">When using this element, the fully qualified .NET type name is required.</span></span> <span data-ttu-id="4d761-188">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="4d761-188">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span>

- <span data-ttu-id="4d761-189">A [SelectionSetName](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg a definíció megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="4d761-189">The [SelectionSetName](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) element (not shown) specifies a set of objects that can be displayed by this definition.</span></span> <span data-ttu-id="4d761-190">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="4d761-190">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span>

- <span data-ttu-id="4d761-191">A [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg egy feltételt, amely a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="4d761-191">The [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) element (not shown) specifies a condition that must exist for this definition to be used.</span></span> <span data-ttu-id="4d761-192">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="4d761-192">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span> <span data-ttu-id="4d761-193">További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-193">For more information about defining selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="displaying-groups-of-objects-in-a-list-view"></a><span data-ttu-id="4d761-194">Lista nézetben a csoportok objektumok megjelenítése</span><span class="sxs-lookup"><span data-stu-id="4d761-194">Displaying Groups of Objects in a List View</span></span>

<span data-ttu-id="4d761-195">Elkülönítheti az objektumokat, amely szerint a lista nézet csoportokba jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-195">You can separate the objects that are displayed by the list view into groups.</span></span> <span data-ttu-id="4d761-196">Ez nem jelenti azt, hogy Ön meghatározott felhasználói csoporttal, csak a Windows PowerShell elindul egy új csoportot, ha az érték egy adott tulajdonságra vagy egy parancsprogramtípusra.</span><span class="sxs-lookup"><span data-stu-id="4d761-196">This does not mean that you define a group, only that Windows PowerShell starts a new group whenever the value of a specific property or script changes.</span></span> <span data-ttu-id="4d761-197">A következő példában elindul egy új csoportot, amikor az értékét a [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) tulajdonságukat módosítják.</span><span class="sxs-lookup"><span data-stu-id="4d761-197">In the following example, a new group is started whenever the value of the [System.Serviceprocess.Servicecontroller.Servicetype](/dotnet/api/System.ServiceProcess.ServiceController.ServiceType) property changes.</span></span>

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

<span data-ttu-id="4d761-198">A következő XML-elemeket segítségével határozhatók meg, amikor egy csoportot:</span><span class="sxs-lookup"><span data-stu-id="4d761-198">The following XML elements are used to define when a group is started:</span></span>

- <span data-ttu-id="4d761-199">A [GroupBy](./groupby-element-for-view-format.md) elem definiálja a tulajdonságot vagy parancsfájlt, amely elindítja az új csoporthoz, és határozza meg, hogyan jelenjen meg a csoport.</span><span class="sxs-lookup"><span data-stu-id="4d761-199">The [GroupBy](./groupby-element-for-view-format.md) element defines the property or script that starts the new group and defines how the group is displayed.</span></span>

- <span data-ttu-id="4d761-200">A [PropertyName](./propertyname-element-for-groupby-format.md) elem azt határozza meg a tulajdonság, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="4d761-200">The [PropertyName](./propertyname-element-for-groupby-format.md) element specifies the property that starts a new group whenever its value changes.</span></span> <span data-ttu-id="4d761-201">Adjon meg egy tulajdonságot vagy a parancsfájl a csoport indítása, de mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-201">You must specify a property or script to start the group, but you cannot specify both.</span></span>

- <span data-ttu-id="4d761-202">A [ScriptBlock](./scriptblock-element-for-groupby-format.md) elem azt határozza meg, a parancsfájl, amely elindítja egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="4d761-202">The [ScriptBlock](./scriptblock-element-for-groupby-format.md) element specifies the script that starts a new group whenever its value changes.</span></span> <span data-ttu-id="4d761-203">Meg kell adnia egy parancsfájl vagy a csoport indítása tulajdonság azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-203">You must specify a script or property to start the group, but you cannot specify both.</span></span>

- <span data-ttu-id="4d761-204">A [címke](./label-element-for-groupby-format.md) elemet definiál egy címke, amely az egyes csoportok elején jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-204">The [Label](./label-element-for-groupby-format.md) element defines a label that is displayed at the beginning of each group.</span></span> <span data-ttu-id="4d761-205">Ez az elem által meghatározott a szöveg mellett Windows PowerShell, amely az új csoport által aktivált, és hozzáad egy üres sort, előtt és után a felirat értékét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="4d761-205">In addition to the text specified by this element, Windows PowerShell displays the value that triggered the new group and adds a blank line before and after the label.</span></span> <span data-ttu-id="4d761-206">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-206">This element is optional.</span></span>

- <span data-ttu-id="4d761-207">A [CustomControl](./customcontrol-element-for-groupby-format.md) elem határozza meg olyan vezérlő, amely az adatok megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="4d761-207">The [CustomControl](./customcontrol-element-for-groupby-format.md) element defines a control that is used to display the data.</span></span> <span data-ttu-id="4d761-208">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-208">This element is optional.</span></span>

- <span data-ttu-id="4d761-209">A [CustomControlName](./customcontrolname-element-for-groupby-format.md) elem azt határozza meg, egy közös vagy megtekintheti a vezérlő, amely az adatok megjelenítésére szolgál.</span><span class="sxs-lookup"><span data-stu-id="4d761-209">The [CustomControlName](./customcontrolname-element-for-groupby-format.md) element specifies a common or view control that is used to display the data.</span></span> <span data-ttu-id="4d761-210">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="4d761-210">This element is optional.</span></span>

<span data-ttu-id="4d761-211">Egy teljes formázási fájl, amely meghatározza a csoportok egy példa: [listanézet (GroupBy)](./list-view-groupby.md).</span><span class="sxs-lookup"><span data-stu-id="4d761-211">For an example of a complete formatting file that defines groups, see [List View (GroupBy)](./list-view-groupby.md).</span></span>

## <a name="using-format-strings"></a><span data-ttu-id="4d761-212">Formázási karakterláncokat használatával</span><span class="sxs-lookup"><span data-stu-id="4d761-212">Using Format Strings</span></span>

<span data-ttu-id="4d761-213">A nézet még jobban meghatározhatja, hogyan jelenjen meg az adatok formázási karakterláncokat is hozzáadhatók.</span><span class="sxs-lookup"><span data-stu-id="4d761-213">Formatting strings can be added to a view to further define how the data is displayed.</span></span> <span data-ttu-id="4d761-214">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="4d761-214">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<ListItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</ListItem>
```

<span data-ttu-id="4d761-215">A következő XML-elemeket segítségével adjon meg egy Formátumminta:</span><span class="sxs-lookup"><span data-stu-id="4d761-215">The following XML elements can be used to specify a format pattern:</span></span>

- <span data-ttu-id="4d761-216">A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="4d761-216">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element specifies the data that is displayed by the view.</span></span>

- <span data-ttu-id="4d761-217">A [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="4d761-217">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element specifies the property whose value is displayed by the view.</span></span> <span data-ttu-id="4d761-218">Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-218">You must specify either a property or a script, but you cannot specify both.</span></span>

- <span data-ttu-id="4d761-219">A [FormatString](./formatstring-element-for-listitem-for-listcontrol-format.md) elem meghatározza formátumú mintát, amely meghatározza, hogy a tulajdonság vagy parancsfájl érték hogyan jelenjen meg a nézetben.</span><span class="sxs-lookup"><span data-stu-id="4d761-219">The [FormatString](./formatstring-element-for-listitem-for-listcontrol-format.md) element specifies a format pattern that defines how the property or script value is displayed in the view.</span></span>

- <span data-ttu-id="4d761-220">A [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="4d761-220">The [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) element (not shown) specifies the script whose value is displayed by the view.</span></span> <span data-ttu-id="4d761-221">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-221">You must specify either a script or a property, but you cannot specify both.</span></span>

<span data-ttu-id="4d761-222">A következő példában a `ToString` módszert hívja meg a parancsfájl értékének.</span><span class="sxs-lookup"><span data-stu-id="4d761-222">In the following example, the `ToString` method is called to format the value of the script.</span></span> <span data-ttu-id="4d761-223">Parancsprogramok segítségével meghívhatja a bármely metódusát meghívná, egy objektumot.</span><span class="sxs-lookup"><span data-stu-id="4d761-223">Scripts can call any method of an object.</span></span> <span data-ttu-id="4d761-224">Ezért ha egy objektum tartozik egy módszer, például `ToString`, van formázási paramétereket, a parancsfájl segítségével meghívhatja a módszer a parancsfájl kimenete értékének.</span><span class="sxs-lookup"><span data-stu-id="4d761-224">Therefore, if an object has a method, such as `ToString`, that has formatting parameters, the script can call that method to format the output value of the script.</span></span>

```xml
<ListItem>
  <ScriptBlock>
    [String}::Format("(0,10) (1,8)", .LastWriteTime.ToString("d"),
    $_.LastWriteTime.Totring("t"))
  </ScriptBlock>
</ListItem>
```

<span data-ttu-id="4d761-225">A következő XML-elem segítségével hívása a `ToString` módszer:</span><span class="sxs-lookup"><span data-stu-id="4d761-225">The following XML element can be used to calling the `ToString` method:</span></span>

- <span data-ttu-id="4d761-226">A [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) elem azt határozza meg a nézet által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="4d761-226">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element specifies the data that is displayed by the view.</span></span>

- <span data-ttu-id="4d761-227">A [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) elem (nem látható) megadja a parancsprogramot, amelynek értéke megjelenik a nézet által.</span><span class="sxs-lookup"><span data-stu-id="4d761-227">The [ScriptBlock](./scriptblock-element-for-listitem-for-listcontrol-format.md) element (not shown) specifies the script whose value is displayed by the view.</span></span> <span data-ttu-id="4d761-228">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="4d761-228">You must specify either a script or a property, but you cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="4d761-229">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4d761-229">See Also</span></span>

[<span data-ttu-id="4d761-230">Egy Windows PowerShell-parancsmag írása</span><span class="sxs-lookup"><span data-stu-id="4d761-230">Writing a Windows PowerShell Cmdlet</span></span>](../cmdlet/writing-a-windows-powershell-cmdlet.md)
