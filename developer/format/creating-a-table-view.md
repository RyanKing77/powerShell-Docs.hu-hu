---
title: Tábla nézet létrehozásával |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1f405afb-70b5-4fe0-9986-bc07401d93fd
caps.latest.revision: 23
ms.openlocfilehash: 832527ea4b042812c39934cd7e124201c6dc2ea4
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850658"
---
# <a name="creating-a-table-view"></a><span data-ttu-id="ae556-102">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="ae556-102">Creating a Table View</span></span>

<span data-ttu-id="ae556-103">Táblázatos nézetre egy vagy több oszlop adatait jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-103">A table view displays data in one or more columns.</span></span> <span data-ttu-id="ae556-104">A tábla minden sorára .NET-objektumokat, és a tábla minden oszlopához az objektum vagy egy parancsfájl érték tulajdonsága jelenti.</span><span class="sxs-lookup"><span data-stu-id="ae556-104">Each row in the table represents a .NET object, and each column of the table represents a property of the object or a script value.</span></span> <span data-ttu-id="ae556-105">Definiálhat egy objektumának tulajdonságait, vagy az objektum a tulajdonságok egy részének megjelenítő táblázat nézet.</span><span class="sxs-lookup"><span data-stu-id="ae556-105">You can define a table view that displays all the properties of an object or a subset of the properties of an object.</span></span>

## <a name="a-table-view-display"></a><span data-ttu-id="ae556-106">Egy táblázat nézet megjelenítése</span><span class="sxs-lookup"><span data-stu-id="ae556-106">A Table View Display</span></span>

<span data-ttu-id="ae556-107">Az alábbi példa bemutatja, hogyan jelenítse meg a Windows PowerShell a [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) által visszaadott objektum a [Get-Service](/powershell/module/microsoft.powershell.management/get-service) parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="ae556-107">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller](/dotnet/api/System.ServiceProcess.ServiceController) object that is returned by the [Get-Service](/powershell/module/microsoft.powershell.management/get-service) cmdlet.</span></span> <span data-ttu-id="ae556-108">Az objektum, a Windows PowerShell definiálva van, amely megjeleníti a táblázatos nézetre a `Status` tulajdonság, a `Name` tulajdonság (Ez a tulajdonság egy aliast tulajdonsága nem a `ServiceName` tulajdonság), és a `DisplayName` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="ae556-108">For this object, Windows PowerShell has defined a table view that displays the `Status` property, the `Name` property (this property is an alias property for the `ServiceName` property), and the `DisplayName` property.</span></span> <span data-ttu-id="ae556-109">A tábla minden sorára a parancsmag által visszaadott objektumot jelöl.</span><span class="sxs-lookup"><span data-stu-id="ae556-109">Each row in the table represents an object returned by the cmdlet.</span></span>

```output
Status   Name               DisplayName
------   ----               -----------
Stopped  AJRouter           AllJoyn Router Service
Stopped  ALG                Application Layer Gateway Service
Stopped  AppIDSvc           Application Identity
Running  Appinfo            Application Information
```

## <a name="defining-the-table-view"></a><span data-ttu-id="ae556-110">A táblázat nézet definiálása</span><span class="sxs-lookup"><span data-stu-id="ae556-110">Defining the Table View</span></span>

<span data-ttu-id="ae556-111">A következő XML formátumú bemutatja a táblaséma megtekintése megjelenítése a [System.Serviceprocess.Servicecontroller? Displayproperty = Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objektum.</span><span class="sxs-lookup"><span data-stu-id="ae556-111">The following XML shows the table view schema for displaying the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) object.</span></span> <span data-ttu-id="ae556-112">Meg kell adnia, hogy a tábla nézetben megjeleníteni kívánt minden egyes tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="ae556-112">You must specify each property that you want displayed in the table view.</span></span>

```xml
<View>
  <Name>service</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>
    <TableHeaders>
      <TableColumnHeader>
        <Width>8</Width>
      </TableColumnHeader>
      <TableColumnHeader>
        <Width>18</Width>
      </TableColumnHeader>
      <TableColumnHeader>
        <Width>38</Width>
      </TableColumnHeader>
    </TableHeaders>
    <TableRowEntries>
      <TableRowEntry>
        <TableColumnItems>
          <TableColumnItem>
           <PropertyName>Status</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>Name</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>DisplayName</PropertyName>
          </TableColumnItem>
        </TableColumnItems>
      </TableRowEntry>
    </TableRowEntries>
  </TableControl>
</View>
```

<span data-ttu-id="ae556-113">A következő XML-elemeket a lista nézet meghatározásához használják:</span><span class="sxs-lookup"><span data-stu-id="ae556-113">The following XML elements are used to define a list view:</span></span>

- <span data-ttu-id="ae556-114">A [nézet](./view-element-format.md) elem a szülőelemet, táblázat nézet.</span><span class="sxs-lookup"><span data-stu-id="ae556-114">The [View](./view-element-format.md) element is the parent element of the table view.</span></span> <span data-ttu-id="ae556-115">(Ez az az ugyanazon szülőelem széles, és egyéni nézetekben a listát.)</span><span class="sxs-lookup"><span data-stu-id="ae556-115">(This is the same parent element for the list, wide, and custom control views.)</span></span>

- <span data-ttu-id="ae556-116">A [neve](./name-element-for-view-format.md) elem azt határozza meg a nézet nevét.</span><span class="sxs-lookup"><span data-stu-id="ae556-116">The [Name](./name-element-for-view-format.md) element specifies the name of the view.</span></span> <span data-ttu-id="ae556-117">Ehhez az elemhez kötelező megadni az összes nézetben megtekinthetők.</span><span class="sxs-lookup"><span data-stu-id="ae556-117">This element is required for all views.</span></span>

- <span data-ttu-id="ae556-118">A [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja az objektumok, amelyek a nézetet.</span><span class="sxs-lookup"><span data-stu-id="ae556-118">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines the objects that use the view.</span></span> <span data-ttu-id="ae556-119">Ez az elem megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-119">This element is required.</span></span>

- <span data-ttu-id="ae556-120">A [GroupBy](./groupby-element-for-view-format.md) (ebben a példában nem látható) elem határozza meg, ha az objektumok egy új csoport megjelenik.</span><span class="sxs-lookup"><span data-stu-id="ae556-120">The [GroupBy](./groupby-element-for-view-format.md) element (not shown in this example) defines when a new group of objects is displayed.</span></span> <span data-ttu-id="ae556-121">Egy új csoportot, ha az érték egy adott tulajdonságra vagy parancsfájl el van indítva.</span><span class="sxs-lookup"><span data-stu-id="ae556-121">A new group is started whenever the value of a specific property or script changes.</span></span> <span data-ttu-id="ae556-122">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-122">This element is optional.</span></span>

- <span data-ttu-id="ae556-123">A [vezérlők](./controls-element-for-view-format.md) (ebben a példában nem látható) elem definiálja az egyéni vezérlők a tábla nézet által meghatározott.</span><span class="sxs-lookup"><span data-stu-id="ae556-123">The [Controls](./controls-element-for-view-format.md) element (not shown in this example) defines the custom controls that are defined by the table view.</span></span> <span data-ttu-id="ae556-124">Vezérlők további adja meg, hogyan jelenjen meg az adatokat egy módot biztosít.</span><span class="sxs-lookup"><span data-stu-id="ae556-124">Controls give you a way to further specify how the data is displayed.</span></span> <span data-ttu-id="ae556-125">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-125">This element is optional.</span></span> <span data-ttu-id="ae556-126">Nézet definiálhat a saját egyéni vezérlők, vagy telepítheti a nézeten a formázási fájlban használt Gyakori vezérlők.</span><span class="sxs-lookup"><span data-stu-id="ae556-126">A view can define its own custom controls, or it can use common controls that can be used by any view in the formatting file.</span></span> <span data-ttu-id="ae556-127">Egyéni vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="ae556-127">For more information about custom controls, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

- <span data-ttu-id="ae556-128">A [HideTableHeaders](./hidetableheaders-element-format.md) elem (nem látszik ebben a példában), adja meg, hogy a tábla nem jelenik meg a tábla tetején lévő címkéket.</span><span class="sxs-lookup"><span data-stu-id="ae556-128">The [HideTableHeaders](./hidetableheaders-element-format.md) element (not show in this example) specifies that the table will not show any labels at the top of the table.</span></span> <span data-ttu-id="ae556-129">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-129">This element is optional.</span></span>

- <span data-ttu-id="ae556-130">A [TableControl](./tablecontrol-element-format.md) elem, amely meghatározza a fejlécet és a sor információkat a táblázat.</span><span class="sxs-lookup"><span data-stu-id="ae556-130">The [TableControl](./tablecontrol-element-format.md) element that defines the header and row information of the table.</span></span> <span data-ttu-id="ae556-131">Minden más nézetekhez hasonlóan táblázatos nézetre jeleníthet meg az objektum tulajdonságainak vagy parancsfájlok által létrehozott értékek.</span><span class="sxs-lookup"><span data-stu-id="ae556-131">Similar to all other views, a table view can display the values of object properties or values generated by scripts.</span></span>

## <a name="defining-column-headers"></a><span data-ttu-id="ae556-132">Oszlopfejlécek meghatározása</span><span class="sxs-lookup"><span data-stu-id="ae556-132">Defining Column Headers</span></span>

1. <span data-ttu-id="ae556-133">A [TableHeaders](./tableheaders-element-format.md) elem, és gyermekelemeinek határozza meg a tábla tetején jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-133">The [TableHeaders](./tableheaders-element-format.md) element and its child elements define what is displayed at the top of the table.</span></span>

2. <span data-ttu-id="ae556-134">A [TableColumnHeader](./tablecolumnheader-element-format.md) elem definiálja a tábla egy oszlop tetején jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-134">The [TableColumnHeader](./tablecolumnheader-element-format.md) element defines what is displayed at the top of a column of the table.</span></span> <span data-ttu-id="ae556-135">Adja meg ezeket az elemeket a ahhoz, hogy szeretné-e a fejlécek jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-135">Specify these elements in the order that you want the headers displayed.</span></span>

   <span data-ttu-id="ae556-136">Nem használható ezen elem száma, de száma korlátozott [TableColumnHeader](./tablecolumnheader-element-format.md) elemeit a táblázatos nézetre számának egyenlőnek kell lennie [TableRowEntry](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md) elemeket, amelyeket használhat.</span><span class="sxs-lookup"><span data-stu-id="ae556-136">There is no limit to the number of these element that you can use, but the number of [TableColumnHeader](./tablecolumnheader-element-format.md) elements in your table view must equal the number of [TableRowEntry](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md) elements that you use.</span></span>

3. <span data-ttu-id="ae556-137">A [címke](./label-element-for-tablecolumnheader-for-tablecontrol-format.md) elem azt határozza meg a megjelenített szöveget.</span><span class="sxs-lookup"><span data-stu-id="ae556-137">The [Label](./label-element-for-tablecolumnheader-for-tablecontrol-format.md) element specifies the text that is displayed.</span></span> <span data-ttu-id="ae556-138">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-138">This element is optional.</span></span>

4. <span data-ttu-id="ae556-139">A [szélesség](./width-element-for-tablecolumnheader-for-tablecontrol-format.md) elem azt határozza meg az oszlop szélessége (a karakter).</span><span class="sxs-lookup"><span data-stu-id="ae556-139">The [Width](./width-element-for-tablecolumnheader-for-tablecontrol-format.md) element specifies the width (in characters) of the column.</span></span> <span data-ttu-id="ae556-140">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-140">This element is optional.</span></span>

5. <span data-ttu-id="ae556-141">A [igazítás](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md) elem azt határozza meg, hogyan jelenjen meg a címke.</span><span class="sxs-lookup"><span data-stu-id="ae556-141">The [Alignment](./alignment-element-for-tablecolumnheader-for-tablecontrol-format.md) element specifies how the label is displayed.</span></span> <span data-ttu-id="ae556-142">A címke lehet balra, jobbra, vagy közepén.</span><span class="sxs-lookup"><span data-stu-id="ae556-142">The label can be aligned to the left, to the right, or centered.</span></span> <span data-ttu-id="ae556-143">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-143">This element is optional.</span></span>

## <a name="defining-the-table-rows"></a><span data-ttu-id="ae556-144">A táblázat sorait meghatározása</span><span class="sxs-lookup"><span data-stu-id="ae556-144">Defining the Table Rows</span></span>

<span data-ttu-id="ae556-145">Nézetek biztosíthat egy vagy több adja meg, milyen adatokat a sorokat a tábla jelenik meg, az alárendelt összetevők használatával kapcsolatos definíciókat a [TableRowEntries](./tablerowentries-element-for-tablecontrol-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="ae556-145">Table views can provide one or more definitions that specify what data is displayed in the rows of the table by using the child elements of the [TableRowEntries](./tablerowentries-element-for-tablecontrol-format.md) element.</span></span> <span data-ttu-id="ae556-146">Figyelje meg, hogy a sorokat a tábla több definícióit is megadhat, de a fejlécek, a sorok változatlan marad, függetlenül attól, milyen sor definition használja.</span><span class="sxs-lookup"><span data-stu-id="ae556-146">Notice that you can specify multiple definitions for the rows of the table, but the headers for the rows remains the same, regardless of what row definition is used.</span></span> <span data-ttu-id="ae556-147">Egy tábla általában csak egyetlen definíciót tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="ae556-147">Typically, a table will have only one definition.</span></span>

<span data-ttu-id="ae556-148">A következő példában a nézetet biztosít, amely több tulajdonságának értékét jeleníti meg egyetlen meghatározást az [System.Diagnostics.Process? Displayproperty = Fullname](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="ae556-148">In the following example, the view provides a single definition that displays the values of several properties of the [System.Diagnostics.Process?Displayproperty=Fullname](/dotnet/api/System.Diagnostics.Process) object.</span></span> <span data-ttu-id="ae556-149">Táblázatos nézetre megjelenítheti egy tulajdonság értékét, vagy egy parancsfájl (a példában nem látható) értékét a sorokat.</span><span class="sxs-lookup"><span data-stu-id="ae556-149">A table view can display the value of a property or the value of a script (not shown in the example) in its rows.</span></span>

```xml
<TableRowEntries>
      <TableRowEntry>
        <TableColumnItems>
          <TableColumnItem>
           <PropertyName>Status</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>Name</PropertyName>
          </TableColumnItem>
          <TableColumnItem>
            <PropertyName>DisplayName</PropertyName>
          </TableColumnItem>
        </TableColumnItems>
      </TableRowEntry>
    </TableRowEntries>

```

<span data-ttu-id="ae556-150">A következő XML-elemeket adjon meg egy olyan sor definíciók használható:</span><span class="sxs-lookup"><span data-stu-id="ae556-150">The following XML elements can be used to provide definitions for a row:</span></span>

- <span data-ttu-id="ae556-151">A [TableRowEntries](./tablerowentries-element-for-tablecontrol-format.md) elem és a gyermekelemeinek határozza meg, mi jelenjen meg a tábla sorait.</span><span class="sxs-lookup"><span data-stu-id="ae556-151">The [TableRowEntries](./tablerowentries-element-for-tablecontrol-format.md) element and its child elements define what is displayed in the rows of the table.</span></span>

- <span data-ttu-id="ae556-152">A [TableRowEntry](./listentry-element-for-listcontrol-format.md) elem biztosít a sor meghatározását.</span><span class="sxs-lookup"><span data-stu-id="ae556-152">The [TableRowEntry](./listentry-element-for-listcontrol-format.md) element provides a definition of the row.</span></span> <span data-ttu-id="ae556-153">Legalább egy [TableRowEntry](./listentry-element-for-listcontrol-format.md) szükséges; azonban nem adhat hozzá elemek számának nincs maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="ae556-153">At least one [TableRowEntry](./listentry-element-for-listcontrol-format.md) is required; however, there is no maximum limit to the number of elements that you can add.</span></span> <span data-ttu-id="ae556-154">A legtöbb esetben a nézet csak egyetlen definíciót fog rendelkezni.</span><span class="sxs-lookup"><span data-stu-id="ae556-154">In most cases, a view will have only one definition.</span></span>

- <span data-ttu-id="ae556-155">A [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) elem azt határozza meg az objektumok, amelyek egy adott definíciója szerint jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-155">The [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) element specifies the objects that are displayed by a specific definition.</span></span> <span data-ttu-id="ae556-156">Ez az elem nem kötelező, és csak a több meghatározása során van szükség [TableRowEntry](./listentry-element-for-listcontrol-format.md) elemek, amelyek a különböző objektumok megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="ae556-156">This element is optional and is needed only when you define multiple [TableRowEntry](./listentry-element-for-listcontrol-format.md) elements that display different objects.</span></span>

- <span data-ttu-id="ae556-157">A [burkolása](./wrap-element-for-tablerowentry-for-tablecontrl-format.md) elem azt határozza meg, hogy a következő sorban megjelenik-e a szöveg, amely meghaladja az oszlopok szélességét.</span><span class="sxs-lookup"><span data-stu-id="ae556-157">The [Wrap](./wrap-element-for-tablerowentry-for-tablecontrl-format.md) element specifies that text that exceeds the column width is displayed on the next line.</span></span> <span data-ttu-id="ae556-158">Alapértelmezés szerint a rendszer csonkolja szöveg, amely meghaladja az oszlopok szélességét.</span><span class="sxs-lookup"><span data-stu-id="ae556-158">By default, text that exceeds the column width is truncated.</span></span>

- <span data-ttu-id="ae556-159">A [TableColumnItems](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md) elem definiálja a Tulajdonságok vagy parancsfájlok, melynek értékei jelennek meg a sorban.</span><span class="sxs-lookup"><span data-stu-id="ae556-159">The [TableColumnItems](./tablecolumnitems-element-for-tablerowentry-for-tablecontrol-format.md) element defines the properties or scripts whose values are displayed in the row.</span></span>

- <span data-ttu-id="ae556-160">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlopában.</span><span class="sxs-lookup"><span data-stu-id="ae556-160">The [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) element defines the property or script whose value is displayed in the column of the row.</span></span> <span data-ttu-id="ae556-161">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem megadása kötelező a sor minden oszlophoz.</span><span class="sxs-lookup"><span data-stu-id="ae556-161">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) element is required for each column of the row.</span></span> <span data-ttu-id="ae556-162">Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="ae556-162">The first entry is displayed in first column, the second entry in the second column, and so on.</span></span>

- <span data-ttu-id="ae556-163">A [PropertyName](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="ae556-163">The [PropertyName](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) element specifies the property whose value is displayed in the row.</span></span> <span data-ttu-id="ae556-164">Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="ae556-164">You must specify either a property or a script, but you cannot specify both.</span></span>

- <span data-ttu-id="ae556-165">A [ScriptBlock](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) elem megadja a parancsprogramot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="ae556-165">The [ScriptBlock](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) element specifies the script whose value is displayed in the row.</span></span> <span data-ttu-id="ae556-166">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="ae556-166">You must specify either a script or a property, but you cannot specify both.</span></span>

- <span data-ttu-id="ae556-167">A [FormatString](./label-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát.</span><span class="sxs-lookup"><span data-stu-id="ae556-167">The [FormatString](./label-element-for-listitem-for-listcontrol-format.md) element specifies a format pattern that defines how the property or script value is displayed.</span></span> <span data-ttu-id="ae556-168">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-168">This element is optional.</span></span>

- <span data-ttu-id="ae556-169">A [igazítás](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md) elem azt határozza meg, hogyan jelenjen meg az érték a tulajdonság vagy parancsfájl.</span><span class="sxs-lookup"><span data-stu-id="ae556-169">The [Alignment](./alignment-element-for-tablecolumnitem-for-tablecontrol-format.md) element specifies how the value of the property or script is displayed.</span></span> <span data-ttu-id="ae556-170">Az érték lehet balra, jobbra, vagy közepén.</span><span class="sxs-lookup"><span data-stu-id="ae556-170">The value can be aligned to the left, to the right, or centered.</span></span> <span data-ttu-id="ae556-171">Ez az elem nem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-171">This element is optional.</span></span>

## <a name="defining-the-objects-that-use-the-table-view"></a><span data-ttu-id="ae556-172">Az objektumok, amelyek a táblázatos nézetre meghatározása</span><span class="sxs-lookup"><span data-stu-id="ae556-172">Defining the Objects That Use the Table View</span></span>

<span data-ttu-id="ae556-173">Két módon határozza meg, mely a .NET-objektumok használata a táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="ae556-173">There are two ways to define which .NET objects use the table view.</span></span> <span data-ttu-id="ae556-174">Használhatja a [ViewSelectedBy](./viewselectedby-element-format.md) elem jeleníthető meg úgy a nézetet, vagy a definíciókat objektumok használhatja a [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) elem határozza meg, hogy mely objektumok szerint jelennek meg a a nézet adott meghatározása.</span><span class="sxs-lookup"><span data-stu-id="ae556-174">You can use the [ViewSelectedBy](./viewselectedby-element-format.md) element to define the objects that can be displayed by all the definitions of the view, or you can use the [EntrySelectedBy](./entryselectedby-element-for-listentry-for-listcontrol-format.md) element to define which objects are displayed by a specific definition of the view.</span></span> <span data-ttu-id="ae556-175">A legtöbb esetben a nézet csak egyetlen definíciót, rendelkezik, ezért általában által meghatározott objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="ae556-175">In most cases, a view has only one definition, so objects are typically defined by the [ViewSelectedBy](./viewselectedby-element-format.md) element.</span></span>

<span data-ttu-id="ae556-176">Az alábbi példa bemutatja, hogyan jelennek meg a táblázat nézet használatával objektumok a [ViewSelectedBy](./viewselectedby-element-format.md) és [TypeName](./typename-element-for-viewselectedby-format.md) elemeket.</span><span class="sxs-lookup"><span data-stu-id="ae556-176">The following example shows how to define the objects that are displayed by the table view using the [ViewSelectedBy](./viewselectedby-element-format.md) and [TypeName](./typename-element-for-viewselectedby-format.md) elements.</span></span> <span data-ttu-id="ae556-177">Nem korlátozott számú [TypeName](./typename-element-for-viewselectedby-format.md) elemeket, hogy is megadhat, és a sorrendjük nem lényeges.</span><span class="sxs-lookup"><span data-stu-id="ae556-177">There is no limit to the number of [TypeName](./typename-element-for-viewselectedby-format.md) elements that you can specify, and their order is not significant.</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <TypeName>System.ServiceProcess.ServiceController</TypeName>
  </ViewSelectedBy>
  <TableControl>...</TableControl>
</View>
```

<span data-ttu-id="ae556-178">A következő XML-elemeket adja meg az objektumokat a táblázatos nézetre által használt használható:</span><span class="sxs-lookup"><span data-stu-id="ae556-178">The following XML elements can be used to specify the objects that are used by the table view:</span></span>

- <span data-ttu-id="ae556-179">A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-179">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines which objects are displayed by the list view.</span></span>

- <span data-ttu-id="ae556-180">A [TypeName](./typename-element-for-viewselectedby-format.md) elem azt határozza meg a .NET-objektum, amely szerint a nézet jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-180">The [TypeName](./typename-element-for-viewselectedby-format.md) element specifies the .NET object that is displayed by the view.</span></span> <span data-ttu-id="ae556-181">A teljes .NET típusú név megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-181">The fully qualified .NET type name is required.</span></span> <span data-ttu-id="ae556-182">Meg kell adnia legalább egy típus vagy állítsa be a nézet a kijelölés, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="ae556-182">You must specify at least one type or selection set for the view, but there is no maximum number of elements that can be specified.</span></span>

<span data-ttu-id="ae556-183">Az alábbi példában a [ViewSelectedBy](./viewselectedby-element-format.md) és [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elemeket.</span><span class="sxs-lookup"><span data-stu-id="ae556-183">The following example uses the [ViewSelectedBy](./viewselectedby-element-format.md) and [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elements.</span></span> <span data-ttu-id="ae556-184">Kijelölt csoportok használata több nézetet, például a lista nézetben definiált és a táblázatos nézetre használata ugyanazokat a megjelenített objektumok kapcsolódó készlete esetében.</span><span class="sxs-lookup"><span data-stu-id="ae556-184">Use selection sets where you have a related set of objects that are displayed using multiple views, such as when you define a list view and a table view for the same objects.</span></span> <span data-ttu-id="ae556-185">Hozzon létre egy kiválasztási kapcsolatos további információkért lásd: [kijelölt csoportok meghatározása](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="ae556-185">For more information about how to create a selection set, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

```xml
<View>
  <Name>System.ServiceProcess.ServiceController</Name>
  <ViewSelectedBy>
    <SelectionSetName>.NET Type Set</SelectionSetName>
  </ViewSelectedBy>
  <TableControl>...</TableControl>
</View>
```

<span data-ttu-id="ae556-186">A következő XML-elemeket adja meg az objektumokat a listanézet által használt használható:</span><span class="sxs-lookup"><span data-stu-id="ae556-186">The following XML elements can be used to specify the objects that are used by the list view:</span></span>

- <span data-ttu-id="ae556-187">A [ViewSelectedBy](./viewselectedby-element-format.md) elem határozza meg, hogy mely objektumok szerint a listanézetet jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-187">The [ViewSelectedBy](./viewselectedby-element-format.md) element defines which objects are displayed by the list view.</span></span>

- <span data-ttu-id="ae556-188">A [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) elem azt határozza meg a nézetben megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="ae556-188">The [SelectionSetName](./selectionsetname-element-for-viewselectedby-format.md) element specifies a set of objects that can be displayed by the view.</span></span> <span data-ttu-id="ae556-189">Meg kell adnia legalább egy készlet kiválasztása vagy a nézet típusa, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="ae556-189">You must specify at least one selection set or type for the view, but there is no maximum number of elements that can be specified.</span></span>

<span data-ttu-id="ae556-190">Az alábbi példa bemutatja, hogyan adhat meg a táblázat nézet használatával egy adott definíciója szerint jelenik meg az objektumok a [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="ae556-190">The following example shows how to define the objects displayed by a specific definition of the table view using the [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) element.</span></span> <span data-ttu-id="ae556-191">Ez az elem használatával, megadhatja az objektum, objektumok kiválasztása csoportja, vagy egy kiválasztási feltétel, amely meghatározza a definíció használatakor .NET nevét.</span><span class="sxs-lookup"><span data-stu-id="ae556-191">Using this element, you can specify the .NET type name of the object, a selection set of objects, or a selection condition that specifies when the definition is used.</span></span> <span data-ttu-id="ae556-192">A kiválasztási feltételek létrehozásával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ae556-192">For more information about how to create a selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ae556-193">A táblázatos nézetre víc definic létrehozásakor különböző oszlopfejlécek nem adható meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-193">When creating multiple definitions of the table view you cannot specify different column headers.</span></span> <span data-ttu-id="ae556-194">Megadhatja, hogy csak a sorokat a tábla, például, hogy mely objektumok jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-194">You can specify only what is displayed in the rows of the table, such as what objects are displayed.</span></span>

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <TypeName>.NET Type</TypeName>
  </EntrySelectedBy>
</TableRowEntry>
```

<span data-ttu-id="ae556-195">A következő XML-elemeket adja meg az objektumokat a listanézet adott definíciójának által használt használható:</span><span class="sxs-lookup"><span data-stu-id="ae556-195">The following XML elements can be used to specify the objects that are used by a specific definition of the list view:</span></span>

- <span data-ttu-id="ae556-196">A [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) elem határozza meg, hogy mely objektumok jelennek meg a definíció szerint.</span><span class="sxs-lookup"><span data-stu-id="ae556-196">The [EntrySelectedBy](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md) element defines which objects are displayed by the definition.</span></span>

- <span data-ttu-id="ae556-197">A [TypeName](./typename-element-for-entryselectedby-for-listcontrol-format.md) elem azt határozza meg a .NET-objektum, amely a definíció szerint jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="ae556-197">The [TypeName](./typename-element-for-entryselectedby-for-listcontrol-format.md) element specifies the .NET object that is displayed by the definition.</span></span> <span data-ttu-id="ae556-198">Ez az elem használatakor a teljes .NET típusú név megadása kötelező.</span><span class="sxs-lookup"><span data-stu-id="ae556-198">When using this element, the fully qualified .NET type name is required.</span></span> <span data-ttu-id="ae556-199">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="ae556-199">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span>

- <span data-ttu-id="ae556-200">A [SelectionSetName](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg a definíció megjelenített objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="ae556-200">The [SelectionSetName](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md) element (not shown) specifies a set of objects that can be displayed by this definition.</span></span> <span data-ttu-id="ae556-201">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="ae556-201">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span>

- <span data-ttu-id="ae556-202">A [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) (nem látható) elemet, adja meg egy feltételt, amely a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="ae556-202">The [SelectionCondition](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md) element (not shown) specifies a condition that must exist for this definition to be used.</span></span> <span data-ttu-id="ae556-203">Meg kell adnia legalább egy típus, kijelölés set vagy kijelölés feltételt a definíciójában, de nincs nem adható meg elemek maximális számát.</span><span class="sxs-lookup"><span data-stu-id="ae556-203">You must specify at least one type, selection set, or selection condition for the definition, but there is no maximum number of elements that can be specified.</span></span> <span data-ttu-id="ae556-204">További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ae556-204">For more information about defining selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="using-format-strings"></a><span data-ttu-id="ae556-205">Formázási karakterláncokat használatával</span><span class="sxs-lookup"><span data-stu-id="ae556-205">Using Format Strings</span></span>

<span data-ttu-id="ae556-206">A nézet még jobban meghatározhatja, hogyan jelenjen meg az adatok formázási karakterláncokat is hozzáadhatók.</span><span class="sxs-lookup"><span data-stu-id="ae556-206">Formatting strings can be added to a view to further define how the data is displayed.</span></span> <span data-ttu-id="ae556-207">Az alábbi példa bemutatja, hogyan definiáljon értékét formázási karakterláncot a `StartTime` tulajdonság.</span><span class="sxs-lookup"><span data-stu-id="ae556-207">The following example shows how to define a formatting string for the value of the `StartTime` property.</span></span>

```xml
<TableColumnItem>
  <PropertyName>StartTime</PropertyName>
  <FormatString>{0:MMM} (0:DD) (0:HH):(0:MM)</FormatString>
</TableColumnItem>
```

<span data-ttu-id="ae556-208">A következő XML-elemeket segítségével adjon meg egy Formátumminta:</span><span class="sxs-lookup"><span data-stu-id="ae556-208">The following XML elements can be used to specify a format pattern:</span></span>

- <span data-ttu-id="ae556-209">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlopában.</span><span class="sxs-lookup"><span data-stu-id="ae556-209">The [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) element defines the property or script whose value is displayed in the column of the row.</span></span> <span data-ttu-id="ae556-210">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem megadása kötelező a sor minden oszlophoz.</span><span class="sxs-lookup"><span data-stu-id="ae556-210">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) element is required for each column of the row.</span></span> <span data-ttu-id="ae556-211">Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="ae556-211">The first entry is displayed in first column, the second entry in the second column, and so on.</span></span>

- <span data-ttu-id="ae556-212">A [PropertyName](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) elem azt határozza meg a tulajdonságot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="ae556-212">The [PropertyName](./propertyname-element-for-tablecolumnitem-for-tablecontrol-format.md) element specifies the property whose value is displayed in the row.</span></span> <span data-ttu-id="ae556-213">Adjon meg egy tulajdonságot vagy a parancsfájl azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="ae556-213">You must specify either a property or a script, but you cannot specify both.</span></span>

- <span data-ttu-id="ae556-214">A [FormatString](./label-element-for-listitem-for-listcontrol-format.md) elem azt határozza meg, amely meghatározza, hogyan jelenjen meg a tulajdonság vagy parancsfájl érték formátuma mintát.</span><span class="sxs-lookup"><span data-stu-id="ae556-214">The [FormatString](./label-element-for-listitem-for-listcontrol-format.md) element specifies a format pattern that defines how the property or script value is displayed.</span></span>

<span data-ttu-id="ae556-215">A következő példában a `ToString` módszert hívja meg a parancsfájl értékének.</span><span class="sxs-lookup"><span data-stu-id="ae556-215">In the following example, the `ToString` method is called to format the value of the script.</span></span> <span data-ttu-id="ae556-216">Parancsprogramok segítségével meghívhatja a bármely metódusát meghívná, egy objektumot.</span><span class="sxs-lookup"><span data-stu-id="ae556-216">Scripts can call any method of an object.</span></span> <span data-ttu-id="ae556-217">Ezért ha egy objektum tartozik egy módszer, például `ToString`, van formázási paramétereket, a parancsfájl segítségével meghívhatja a módszer a parancsfájl kimenete értékének.</span><span class="sxs-lookup"><span data-stu-id="ae556-217">Therefore, if an object has a method, such as `ToString`, that has formatting parameters, the script can call that method to format the output value of the script.</span></span>

```xml
<ListItem>
  <ScriptBlock>
    [String]::Format("(0,10) (1,8)", .LastWriteTime.ToString("d"),
    $_.LastWriteTime.Totring("t"))
  </ScriptBlock>
</ListItem>
```

<span data-ttu-id="ae556-218">A következő XML-elem segítségével hívása a `ToString` módszer:</span><span class="sxs-lookup"><span data-stu-id="ae556-218">The following XML element can be used to calling the `ToString` method:</span></span>

- <span data-ttu-id="ae556-219">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem definiálja a tulajdonságot, vagy a parancsfájl, amelynek értéke megjelenik a sor oszlopában.</span><span class="sxs-lookup"><span data-stu-id="ae556-219">The [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) element defines the property or script whose value is displayed in the column of the row.</span></span> <span data-ttu-id="ae556-220">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) elem megadása kötelező a sor minden oszlophoz.</span><span class="sxs-lookup"><span data-stu-id="ae556-220">A [TableColumnItem](./tablecolumnitem-element-for-tablecolumnitems-for-tablecontrol-format.md) element is required for each column of the row.</span></span> <span data-ttu-id="ae556-221">Az első bejegyzés jelenik meg az első oszlopban a második bejegyzés a második oszlopban, és így tovább.</span><span class="sxs-lookup"><span data-stu-id="ae556-221">The first entry is displayed in first column, the second entry in the second column, and so on.</span></span>

- <span data-ttu-id="ae556-222">A [ScriptBlock](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) elem megadja a parancsprogramot, amelynek értéke megjelenik a sorban.</span><span class="sxs-lookup"><span data-stu-id="ae556-222">The [ScriptBlock](./scriptblock-element-for-tablecolumnitem-for-tablecontrol-format.md) element specifies the script whose value is displayed in the row.</span></span> <span data-ttu-id="ae556-223">Meg kell adnia egy parancsfájl vagy a tulajdonságot azonban mindkettő megadására nincs lehetőség.</span><span class="sxs-lookup"><span data-stu-id="ae556-223">You must specify either a script or a property, but you cannot specify both.</span></span>

## <a name="see-also"></a><span data-ttu-id="ae556-224">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ae556-224">See Also</span></span>

[<span data-ttu-id="ae556-225">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ae556-225">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
