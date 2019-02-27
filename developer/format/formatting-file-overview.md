---
title: Formázás – áttekintés |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe888fee-1fe9-459f-9d62-35732c19a7f8
caps.latest.revision: 13
ms.openlocfilehash: d418cff70c1197aa3c331eed909f49198da139e9
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851918"
---
# <a name="formatting-file-overview"></a><span data-ttu-id="dd6d3-102">Formázási fájl – Áttekintés</span><span class="sxs-lookup"><span data-stu-id="dd6d3-102">Formatting File Overview</span></span>

<span data-ttu-id="dd6d3-103">Parancsok (parancsmagok, függvények és parancsfájlok) által visszaadott objektumaihoz tartozó megjelenítési formátuma formázási fájlok (format.ps1xml) segítségével határozzák meg.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-103">The display format for the objects that are returned by commands (cmdlets, functions, and scripts) are defined by using formatting files (format.ps1xml files).</span></span> <span data-ttu-id="dd6d3-104">Több ilyen fájllal határozza meg azokat az objektumokat által biztosított PowerShell-parancsok, például a visszaadott megjelenítési formátumát a PowerShell által biztosított a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) által visszaadott objektum a `Get-Process` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-104">Several of these files are provided by PowerShell to define the display format for those objects returned by PowerShell-provided commands, such as the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object returned by the `Get-Process` cmdlet.</span></span> <span data-ttu-id="dd6d3-105">Azonban is létrehozhat saját egyéni formázási fájlok felülírja az alapértelmezett megjelenítési formátum, vagy írhat meghatározásához a saját parancsok által visszaadott objektumok megjelenítéséhez egyéni formázási fájlt.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-105">However, you can also create your own custom formatting files to overwrite the default display formats or you can write a custom formatting file to define the display of objects returned by your own commands.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd6d3-106">Formázási fájlokat nem határozzák meg a folyamat visszaadott objektum elemét.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-106">Formatting files do not determine the elements of an object that are returned to the pipeline.</span></span> <span data-ttu-id="dd6d3-107">Visszaadott objektum a folyamat, amikor az objektum összes tagja érhetők el még akkor is, ha némelyike nem jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-107">When an object is returned to the pipeline, all members of that object are available even if some are not displayed.</span></span>

<span data-ttu-id="dd6d3-108">PowerShell a formázási ezeket a fájlokat az adatok segítségével határozza meg, mi jelenjen meg, és a megjelenített adatok formázását.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-108">PowerShell uses the data in these formatting files to determine what is displayed and how the displayed data is formatted.</span></span> <span data-ttu-id="dd6d3-109">A megjelenített adatok az objektum tulajdonságainak és a egy parancsfájl értékét tartalmazhatnak.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-109">The displayed data can include the properties of an object or the value of a script.</span></span> <span data-ttu-id="dd6d3-110">Parancsprogramok akkor használhatók, ha azt szeretné, néhány érték, amely nem érhető el közvetlenül a objektumot, például hozzáadása egy objektum két tulajdonság értékét, és ezután megjelenítése az összeg, az adatok tulajdonságainak megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-110">Scripts are used if you want to display some value that is not available directly from the properties of an object, such as adding the value of two properties of an object and then displaying the sum as a piece of data.</span></span> <span data-ttu-id="dd6d3-111">A megjelenített adatok formázása a megjeleníteni kívánt objektumok nézetek definiálásával történik.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-111">Formatting of the displayed data is done by defining views for the objects that you want to display.</span></span> <span data-ttu-id="dd6d3-112">Megadhatja, hogy egyetlen nézetben minden objektum esetén, meghatározhatja, hogy egyetlen nézetben több objektumon, vagy megadhat több nézetet ugyanahhoz az objektumhoz.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-112">You can define a single view for each object, you can define a single view for multiple objects, or you can define multiple views for the same object.</span></span> <span data-ttu-id="dd6d3-113">Nincs nem definiálható nézetek száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-113">There is no limit to the number of views that you can define.</span></span>

## <a name="common-features-of-formatting-files"></a><span data-ttu-id="dd6d3-114">A formázási fájlok általános szolgáltatások</span><span class="sxs-lookup"><span data-stu-id="dd6d3-114">Common Features of Formatting Files</span></span>

<span data-ttu-id="dd6d3-115">Minden egyes formázási fájl a következő összetevők határozzák meg a fájl minden nézetek között megosztható definiálhatja:</span><span class="sxs-lookup"><span data-stu-id="dd6d3-115">Each formatting file can define the following components that can be shared across all the views defined by the file:</span></span>

- <span data-ttu-id="dd6d3-116">Alapértelmezés szerint a konfigurációs beállítások, például hogy a táblák sorait megjelenített adatok jelennek meg a következő sorban hosszabb, mint az oszlop szélessége adatok esetén.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-116">Default configuration setting, such as whether the data displayed in the rows of tables will be displayed on the next line if the data is longer than the width of the column.</span></span> <span data-ttu-id="dd6d3-117">Ezekkel a beállításokkal kapcsolatos további információkért lásd: [közös konfigurációs beállítások meghatározása](./defining-common-configuration-features.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-117">For more information about these settings, see [Defining Common Configuration Settings](./defining-common-configuration-features.md).</span></span>

- <span data-ttu-id="dd6d3-118">A formázási fájl nézetek által megjelenített objektumok készleteit.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-118">Sets of objects that can be displayed by any of the views of the formatting file.</span></span> <span data-ttu-id="dd6d3-119">További információ ezen készletek (néven *kijelölt csoportok*), lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-119">For more information about these sets (referred to as *selection sets*), see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

- <span data-ttu-id="dd6d3-120">A formázási fájl összes nézetek által használt Gyakori vezérlők.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-120">Common controls that can be used by all the views of the formatting file.</span></span> <span data-ttu-id="dd6d3-121">Vezérlők teszik lehetővé az adatok megjelenítésének lehet finomabb szabályozásra.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-121">Controls give you finer control on how data is displayed.</span></span> <span data-ttu-id="dd6d3-122">Vezérlők kapcsolatos további információkért lásd: [egyéni vezérlők meghatározása](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-122">For more information about controls, see [Defining Custom Controls](./creating-custom-controls.md).</span></span>

## <a name="formatting-views"></a><span data-ttu-id="dd6d3-123">Formázási nézetek</span><span class="sxs-lookup"><span data-stu-id="dd6d3-123">Formatting Views</span></span>

<span data-ttu-id="dd6d3-124">Formázási nézetek objektumokat megjelenítheti egy táblázatos formátumú, listaformátumban, széles és egyéni formátum.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-124">Formatting views can display objects in a table format, list format, wide format, and custom format.</span></span> <span data-ttu-id="dd6d3-125">Minden egyes formázási definíció többségében, a nézet leíró XML-címkék csoportja által leírása.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-125">For the most part, each formatting definition is described by a set of XML tags that describe the view.</span></span> <span data-ttu-id="dd6d3-126">Mindegyik nézetről tartalmaz a nézet nevét az objektumok, amelyek a nézet és az elemek a nézetet, például az oszlopok és sorok információk a táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-126">Each view contains the name of the view, the objects that use the view, and the elements of the view, such as the column and row information for a table view.</span></span>

<span data-ttu-id="dd6d3-127">Táblázat nézet egy objektum vagy egy parancsfájl blokk értéket egy vagy több oszlop tulajdonságait.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-127">Table View Lists the properties of an object or a script block value in one or more columns.</span></span> <span data-ttu-id="dd6d3-128">Minden oszlop egy egyetlen tulajdonságát az objektum vagy egy parancsfájl értéket képvisel.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-128">Each column represents a single property of the object or a script value.</span></span> <span data-ttu-id="dd6d3-129">Definiálhat egy objektumot, vagy a tulajdonságok és parancsfájl-értékek, a tulajdonságok egy részének objektum tulajdonságait megjelenítő táblázat nézet.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-129">You can define a table view that displays all the properties of an object, a subset of the properties of an object, or a combination of properties and script values.</span></span> <span data-ttu-id="dd6d3-130">A táblázat minden egyes sorára jelenti. a visszaadott objektum.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-130">Each row of the table represents a returned object.</span></span> <span data-ttu-id="dd6d3-131">Tábla nézet létrehozásával nagyon hasonlít mikor egy objektum, kanálu a `Format-Table` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-131">Creating a table view is very similar to when you pipe an object to the `Format-Table` cmdlet.</span></span> <span data-ttu-id="dd6d3-132">Ez a nézet kapcsolatos további információkért lásd: [táblázatos nézetre](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-132">For more information about this view, see [Table View](./creating-a-table-view.md).</span></span>

<span data-ttu-id="dd6d3-133">Nézet megjeleníti a tulajdonságok listázásához egy objektum vagy egy parancsfájl egyetlen oszlop értéke.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-133">List View Lists the properties of an object or a script value in a single column.</span></span> <span data-ttu-id="dd6d3-134">A lista minden egyes sorára egy nem kötelező címke vagy tulajdonság vagy parancsfájl értékét a tulajdonság nevét jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-134">Each row of the list displays an optional label or the property name followed by the value of the property or script.</span></span> <span data-ttu-id="dd6d3-135">Lista nézet létrehozásával nagyon hasonlít egy objektum átirányításával a `Format-List` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-135">Creating a list view is very similar to piping an object to the `Format-List` cmdlet.</span></span> <span data-ttu-id="dd6d3-136">Ez a nézet kapcsolatos további információkért lásd: [listanézet](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-136">For more information about this view, see [List View](./creating-a-list-view.md).</span></span>

<span data-ttu-id="dd6d3-137">Széles nézet egy objektum vagy egy parancsfájl értéket egy vagy több oszlop egyetlen tulajdonságát sorolja fel.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-137">Wide View Lists a single property of an object or a script value in one or more columns.</span></span> <span data-ttu-id="dd6d3-138">Nincs címke vagy fejléc ehhez a nézethez.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-138">There is no label or header for this view.</span></span> <span data-ttu-id="dd6d3-139">Széles körű nézetek létrehozásával nagyon hasonlít egy objektum átirányításával a `Format-Wide` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-139">Creating a wide view is very similar to piping an object to the `Format-Wide` cmdlet.</span></span> <span data-ttu-id="dd6d3-140">Ez a nézet kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-140">For more information about this view, see [Wide View](./creating-a-wide-view.md).</span></span>

<span data-ttu-id="dd6d3-141">Egyéni nézet nézetet jelenít meg egy testre szabható objektum tulajdonságai vagy parancsfájl értékek, amelyek nem követi a nézetek, a nézetek és a széles körű nézetek merev struktúráját.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-141">Custom View Displays a customizable view of object properties or script values that does not adhere to the rigid structure of table views, list views, or wide views.</span></span> <span data-ttu-id="dd6d3-142">Meghatározhat egy különálló egyéni nézetet, vagy megadhat egy egyéni nézet, amelyet egy másik nézetre, például egy táblázat vagy lista nézetben.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-142">You can define a stand-alone custom view, or you can define a custom view that is used by another view, such as a table view or list view.</span></span> <span data-ttu-id="dd6d3-143">Egyéni nézet létrehozása nagyon hasonlít egy objektum átirányításával a `Format-Custom` parancsmagot.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-143">Creating a custom view is very similar to piping an object to the `Format-Custom` cmdlet.</span></span> <span data-ttu-id="dd6d3-144">Ez a nézet kapcsolatos további információkért lásd: [egyéni nézet](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="dd6d3-144">For more information about this view, see [Custom View](./creating-custom-controls.md).</span></span>

## <a name="components-of-a-view"></a><span data-ttu-id="dd6d3-145">Nézet összetevői</span><span class="sxs-lookup"><span data-stu-id="dd6d3-145">Components of a View</span></span>

<span data-ttu-id="dd6d3-146">A következő XML-példákat az alapvető XML-összetevők nézet megjelenítése.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-146">The following XML examples show the basic XML components of a view.</span></span> <span data-ttu-id="dd6d3-147">Az egyéni XML-elemeket eltérőek lehetnek attól függően, hogy melyik nézet szeretne létrehozni, de az alapvető összetevők nézetek azonos.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-147">The individual XML elements vary depending on which view you want to create, but the basic components of the views are all the same.</span></span>

<span data-ttu-id="dd6d3-148">Első lépésként mindegyik nézetről tartalmaz egy `Name` elem, amely meghatározza egy felhasználóbarát nevet, amellyel hivatkozni a nézetet.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-148">To start with, each view has a `Name` element that specifies a user friendly name that is used to reference the view.</span></span> <span data-ttu-id="dd6d3-149">egy `ViewSelectedBy` elem, amely meghatározza, mely a .NET-objektumok jelennek meg a nézet által és a egy *vezérlő* elem, amely meghatározza a nézetet.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-149">a `ViewSelectedBy` element that defines which .NET objects are displayed by the view, and a *control* element that defines the view.</span></span>

```xml
<ViewDefinitions>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <ListControl>...</ListControl>
  <View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <WideControl>...</WideControl>
  <View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <CustomControl>...</CustomControl>
  </View>
</ViewDefinitions>

```

<span data-ttu-id="dd6d3-150">A vezérlő elemen belül megadhat egy vagy több *bejegyzés* elemeket.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-150">Within the control element, you can define one or more *entry* elements.</span></span> <span data-ttu-id="dd6d3-151">Ha víc definic használ, meg kell adnia, mely .NET-objektumokká használata minden egyes definíciója.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-151">If you use multiple definitions, you must specify which .NET objects use each definition.</span></span> <span data-ttu-id="dd6d3-152">Általában csak egy bejegyzést, csak egyetlen definíciót, az egyes vezérlőelemek van szükség.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-152">Typically only one entry, with only one definition, is needed for each control.</span></span>

```xml
<ListControl>
  <ListEntries>
    <ListEntry>
      <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
    <ListEntry>
        <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
    <ListEntry>
        <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
  </ListEntries>
</ListControl>

```

<span data-ttu-id="dd6d3-153">A nézetek minden egyes belépési elemen belül adjon meg a *elem* a .NET-tulajdonságok vagy parancsfájlok, amely a nézetben megjelenített meghatározó elemeket.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-153">Within each entry element of a view, you specify the *item* elements that define the .NET properties or scripts that are displayed by that view.</span></span>

```xml

<ListItems>
  <ListItem>...</ListItem>
  <ListItem>...</ListItem>
  <ListItem>...</ListItem>
</ListItems>

```

<span data-ttu-id="dd6d3-154">Ahogyan az előző példák, a formázási fájlt tartalmazhat több nézetet, nézet víc definic is tartalmazhat, és minden egyes tartalmazhat több elem.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-154">As shown in the preceding examples, the formatting file can contain multiple views, a view can contain multiple definitions, and each definition can contain multiple items.</span></span>

## <a name="example-of-a-table-view"></a><span data-ttu-id="dd6d3-155">Példa a táblázatos nézetre</span><span class="sxs-lookup"><span data-stu-id="dd6d3-155">Example of a Table View</span></span>

<span data-ttu-id="dd6d3-156">Az alábbi példa bemutatja a táblázatos nézetre, amely tartalmazza a két oszlopot definiáló XML-címkéket.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-156">The following example shows the XML tags used to define a table view that contains two columns.</span></span> <span data-ttu-id="dd6d3-157">A [ViewDefinitions](./viewdefinitions-element-format.md) elem a tároló eleme a formázási fájlban meghatározott összes nézetben megtekinthetők.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-157">The [ViewDefinitions](./viewdefinitions-element-format.md) element is the container element for all the views defined in the formatting file.</span></span> <span data-ttu-id="dd6d3-158">A [nézet](./view-element-format.md) elem definiálja az adott tábla, list, szélesre vagy egyéni nézet.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-158">The [View](./view-element-format.md) element defines the specific table, list, wide, or custom view.</span></span> <span data-ttu-id="dd6d3-159">Belül [nézet](./view-element-format.md) elem, a [neve](./name-element-for-view-format.md) elem nevét adja meg a nézet a [ViewSelectedBy](./viewselectedby-element-format.md) elem definiálja a megtekintése, valamint a különböző objektumok szabályozhatja az elemeket (például a `TableControl` elem a következő példában látható) határozza meg a nézet típusa.</span><span class="sxs-lookup"><span data-stu-id="dd6d3-159">Within each [View](./view-element-format.md) element, the [Name](./name-element-for-view-format.md) element specifies the name of the view, the [ViewSelectedBy](./viewselectedby-element-format.md) element defines the objects that use the view, and the different control elements (such as the `TableControl` element shown in the following example) define the type of the view.</span></span>

```xml
<ViewDefinitions>
  <View>
    <Name>Name of View</Name>
    <ViewSelectedBy>
      <TypeName>Object to display using this view</TypeName>
      <TypeName>Object to display using this view</TypeName>
    </ViewSelectedBy>
    <TableControl>
      <TableHeaders>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
      </TableHeaders>
      <TableRowEntries>
        <TableRowEntry>
          <TableColumnItems>
            <TableColumnItem>
              <PropertyName>Header for column 1</PropertyName>
            </TableColumnItem>
            <TableColumnItem>
              <PropertyName>Header for column 2</PropertyName>
            </TableColumnItem>
          </TableColumnItems>
        </TableRowEntry>
      </TableRowEntries>
    </TableControl)
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a><span data-ttu-id="dd6d3-160">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="dd6d3-160">See Also</span></span>

[<span data-ttu-id="dd6d3-161">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="dd6d3-161">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="dd6d3-162">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="dd6d3-162">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="dd6d3-163">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="dd6d3-163">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="dd6d3-164">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="dd6d3-164">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="dd6d3-165">Egy PowerShell-formázást és típusok fájl írása</span><span class="sxs-lookup"><span data-stu-id="dd6d3-165">Writing a PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
