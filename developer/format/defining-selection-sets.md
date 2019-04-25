---
title: Kijelölt csoportok meghatározása |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 00dbb5ee-93d4-4914-a082-ef4d8b236b5c
caps.latest.revision: 16
ms.openlocfilehash: 596212f2e64401a751cf3dca0ee7d60b80912c00
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066311"
---
# <a name="defining-selection-sets"></a><span data-ttu-id="48642-102">Kijelölési csoportok definiálása</span><span class="sxs-lookup"><span data-stu-id="48642-102">Defining Selection Sets</span></span>

<span data-ttu-id="48642-103">Nézetek és a vezérlők létrehozásakor hivatkozott objektumok készleteit kijelölt csoportok szerint adhatja meg.</span><span class="sxs-lookup"><span data-stu-id="48642-103">When creating multiple views and controls, you can define sets of objects that are referred to as selection sets.</span></span> <span data-ttu-id="48642-104">Egy kiválasztási beállítása lehetővé teszi, hogy meghatározza az objektumok egy alkalommal megadásukhoz ismételten mindegyik nézetben vagy vezérlő nélkül.</span><span class="sxs-lookup"><span data-stu-id="48642-104">A selection set enables you to define the objects one time, without having to define them repeatedly for each view or control.</span></span> <span data-ttu-id="48642-105">Általában kijelölt csoportok használja egy sor kapcsolódó .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="48642-105">Typically, selection sets are used when you have a set of related .NET objects.</span></span> <span data-ttu-id="48642-106">Ha például a `FileSystem` formázási fájlt (FileSystem.format.ps1xml) határozza meg a rendszer fájltípusokat, amelyek számos nézet kiválasztása készletét.</span><span class="sxs-lookup"><span data-stu-id="48642-106">For example, The `FileSystem` formatting file (FileSystem.format.ps1xml) defines a selection set of the file system types that several views use.</span></span>

## <a name="where-selection-sets-are-defined-and-referenced"></a><span data-ttu-id="48642-107">Kijelölt csoportok amelyeknél definiált és hivatkozott</span><span class="sxs-lookup"><span data-stu-id="48642-107">Where Selection Sets are Defined and Referenced</span></span>

<span data-ttu-id="48642-108">Kijelölt csoportok meghatározhatja a common data, a nézetek és a formázási fájlban meghatározott vezérlők által használható részeként.</span><span class="sxs-lookup"><span data-stu-id="48642-108">You define selection sets as part of the common data that can be used by all the views and controls defined in the formatting file.</span></span> <span data-ttu-id="48642-109">Az alábbi példa bemutatja, hogyan három kijelölési csoportok meghatározására.</span><span class="sxs-lookup"><span data-stu-id="48642-109">The following example shows how to define three selection sets.</span></span>

```xml
<Configuration>
  <SelectionSets>
    <SelectionSet>...</SelectionSet>
    <SelectionSet>...</SelectionSet>
    <SelectionSet>...</SelectionSet>
  </SelectionSets>
</Configuration>
```

<span data-ttu-id="48642-110">A kijelölés hivatkozhat állítja be a következő módon:</span><span class="sxs-lookup"><span data-stu-id="48642-110">You can reference a selection sets in the following ways:</span></span>

- <span data-ttu-id="48642-111">Mindegyik nézetről tartalmaz egy `ViewSelectedBy` elem, amely meghatározza, hogy mely objektumok jelennek meg a nézet használatával.</span><span class="sxs-lookup"><span data-stu-id="48642-111">Each view has a `ViewSelectedBy` element that defines which objects are displayed by using the view.</span></span> <span data-ttu-id="48642-112">A `ViewSelectedBy` elemnek egy `SelectionSetName` gyermekelemet, amely meghatározza a kijelölési beállítása, amely a nézet feltételeit a definíciókat.</span><span class="sxs-lookup"><span data-stu-id="48642-112">The `ViewSelectedBy` element has a `SelectionSetName` child element that specifies the selection set that all the definitions of the view use.</span></span> <span data-ttu-id="48642-113">Nincs kijelölt csoportok nézetben hivatkozási száma korlátozva.</span><span class="sxs-lookup"><span data-stu-id="48642-113">There is no restriction on the number of selection sets that you can reference from a view.</span></span>

- <span data-ttu-id="48642-114">Minden egyes definíciójában nézet vagy -vezérlés a `EntrySelectedBy` elem határozza meg, hogy mely objektumok jelennek meg, hogy a definíció használatával.</span><span class="sxs-lookup"><span data-stu-id="48642-114">In each definition of a view or control, the `EntrySelectedBy` element defines which objects are displayed by using that definition.</span></span> <span data-ttu-id="48642-115">Általában egy nézetet, vagy a vezérlő csak egy definícióval rendelkezik úgy határozzák meg az objektumokat a `ViewSelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="48642-115">Typically a view or control has only one definition so the objects are defined by the `ViewSelectedBy` element.</span></span> <span data-ttu-id="48642-116">A `EntrySelectedBy` elemnek a definíció egy `SelectionSetName` , amely meghatározza a kijelölési set gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="48642-116">The `EntrySelectedBy` element of the definition has a `SelectionSetName` child element that specifies the selection set.</span></span> <span data-ttu-id="48642-117">Ha a kiválasztása a definíciófrissítés számára adja meg, nem adhat meg, további alárendelt elemek a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="48642-117">If you specify the selection set for a definition, you cannot specify any of the other child elements of the `EntrySelectedBy` element.</span></span>

- <span data-ttu-id="48642-118">Minden egyes definíciójában nézet vagy -vezérlés a `SelectionCondition` elem segítségével adja meg a definíció használatakor feltételt.</span><span class="sxs-lookup"><span data-stu-id="48642-118">In each definition of a view or control, the `SelectionCondition` element can be used to specify a condition for when the definition is used.</span></span> <span data-ttu-id="48642-119">A `SelectionCondition` elemnek egy `SelectionSetName` gyermekelemet, amely meghatározza a kijelölési beállítása, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="48642-119">The `SelectionCondition` element has a `SelectionSetName` child element that specifies the selection set that triggers the condition.</span></span> <span data-ttu-id="48642-120">A feltétel akkor aktiválódik, ha a kijelölt csoportban meghatározott objektum jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="48642-120">The condition is triggered when any of the objects defined in the selection set are displayed.</span></span> <span data-ttu-id="48642-121">Ezek a feltételek beállításával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="48642-121">For more information about how to set these conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="selection-set-example"></a><span data-ttu-id="48642-122">Kijelölés példa beállítása</span><span class="sxs-lookup"><span data-stu-id="48642-122">Selection Set Example</span></span>

<span data-ttu-id="48642-123">Az alábbi példa bemutatja egy kiválasztási csoportja, amelyek közvetlenül származik a `FileSystem` Windows PowerShell által biztosított fájl formázását.</span><span class="sxs-lookup"><span data-stu-id="48642-123">The following example shows a selection set that is taken directly from the `FileSystem` formatting file provided by Windows PowerShell.</span></span> <span data-ttu-id="48642-124">Egyéb formázást fájlok Windows PowerShell kapcsolatos további információkért lásd: [Windows PowerShell formázás fájlok](./powershell-formatting-files.md).</span><span class="sxs-lookup"><span data-stu-id="48642-124">For more information about other Windows PowerShell formatting files, see [Windows PowerShell Formatting Files](./powershell-formatting-files.md).</span></span>

```xml
<SelectionSets>
  <SelectionSet>
    <Name>FileSystemTypes</Name>
    <Types>
     <TypeName>System.IO.DirectoryInfo</TypeName>
     <TypeName>System.IO.FileInfo</TypeName>
     <TypeName>Deserialized.System.IO.DirectoryInfo</TypeName>
     <TypeName>Deserialized.System.IO.FileInfo</TypeName>
    </Types>
  </SelectionSet>
</SelectionSets>
```

<span data-ttu-id="48642-125">Az előző kijelölés készletet hivatkozik a `ViewSelectedBy` elem a táblázatos nézetre.</span><span class="sxs-lookup"><span data-stu-id="48642-125">The previous selection set is referenced in the `ViewSelectedBy` element of a table view.</span></span>

```xml
<ViewDefinitions>
  <View>
    <Name>Files</Name>
    <ViewSelectedBy>
      <SelectionSetName>FileSystemTypes</SelectionSetName>
    </ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
</ViewDefinitions>

```

## <a name="xml-elements"></a><span data-ttu-id="48642-126">XML-elemek</span><span class="sxs-lookup"><span data-stu-id="48642-126">XML Elements</span></span>

 <span data-ttu-id="48642-127">Nincs kijelölt csoportok definiálható száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="48642-127">There is no limit to the number of selection sets that you can define.</span></span> <span data-ttu-id="48642-128">A következő XML-elemeket segítségével hozzon létre egy kiválasztási csoportot.</span><span class="sxs-lookup"><span data-stu-id="48642-128">The following XML elements are used to create a selection set.</span></span>

- <span data-ttu-id="48642-129">A [SelectionSets](./selectionsets-element-format.md) elem definiálja a különböző nézetek által hivatkozott .NET-objektumokat és fájl formázási vezérlők.</span><span class="sxs-lookup"><span data-stu-id="48642-129">The [SelectionSets](./selectionsets-element-format.md) element defines the sets of .NET objects that are referenced by the views and controls of the formatting file.</span></span>

- <span data-ttu-id="48642-130">A [SelectionSet](./selectionset-element-format.md) elem egy .NET-objektumokká egyetlen csoportját határozza meg.</span><span class="sxs-lookup"><span data-stu-id="48642-130">The [SelectionSet](./selectionset-element-format.md) element defines a single set of .NET objects.</span></span>

- <span data-ttu-id="48642-131">A [neve](./name-element-for-selectionset-format.md) elem nevét adja meg, amellyel a kijelölt csoport hivatkozhat.</span><span class="sxs-lookup"><span data-stu-id="48642-131">The [Name](./name-element-for-selectionset-format.md) element specifies the name that is used to reference the selection set.</span></span>

- <span data-ttu-id="48642-132">A [típusok](./types-element-for-selectionset-format.md) elem azt határozza meg az objektumok a kijelölt csoport .NET tulajdonságtípusokat.</span><span class="sxs-lookup"><span data-stu-id="48642-132">The [Types](./types-element-for-selectionset-format.md) element specifies the .NET types of the objects of the selection set.</span></span> <span data-ttu-id="48642-133">(Belül fájlok formázást, objektumok vannak megadva .NET típus szerint.)</span><span class="sxs-lookup"><span data-stu-id="48642-133">(Within formatting files, objects are specified by their .NET type.)</span></span>

 <span data-ttu-id="48642-134">A következő XML-elemeket adjon meg egy kijelölést szolgálnak.</span><span class="sxs-lookup"><span data-stu-id="48642-134">The following XML elements are used to specify a selection set.</span></span>

- <span data-ttu-id="48642-135">A következő elem azt határozza meg, a kijelölt állítható be a nézet a definíciók használható:</span><span class="sxs-lookup"><span data-stu-id="48642-135">The following element specifies the selection set to use in all the definitions of the view:</span></span>

    - [<span data-ttu-id="48642-136">SelectionSetName eleme ViewSelectedBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="48642-136">SelectionSetName Element for ViewSelectedBy (Format)</span></span>](./selectionsetname-element-for-viewselectedby-format.md)

    - [<span data-ttu-id="48642-137">A GroupBy (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-137">SelectionSetName Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-groupby-format.md)

- <span data-ttu-id="48642-138">A következő elemeket adja meg a kijelölési készlet egyetlen nézetdefiníció által használt:</span><span class="sxs-lookup"><span data-stu-id="48642-138">The following elements specify the selection set used by a single view definition:</span></span>

    - [<span data-ttu-id="48642-139">A ListControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-139">SelectionSetName Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

    - [<span data-ttu-id="48642-140">A TableControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-140">SelectionSetName Element for EntrySelectedBy for TableControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md)

    - [<span data-ttu-id="48642-141">A WideControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-141">SelectionSetName Element for EntrySelectedBy for WideControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)

    - [<span data-ttu-id="48642-142">A nézet (formátum) CustomControl EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-142">SelectionSetName Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format.md)

- <span data-ttu-id="48642-143">A következő elemeket adjon meg a kijelölési közös által használt és vezérlőelem-definíciók megtekintése:</span><span class="sxs-lookup"><span data-stu-id="48642-143">The following elements specify the selection set used by common and view control definitions:</span></span>

    - [<span data-ttu-id="48642-144">Nézet (formátum) vezérlők EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-144">SelectionSetName Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-controls-for-view-format.md)

    - [<span data-ttu-id="48642-145">Konfiguráció (formátum) vezérlők EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-145">SelectionSetName Element for EntrySelectedBy for Controls for Configuration (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-controls-for-configuration-format.md)

- <span data-ttu-id="48642-146">A következő elemeket adjon meg a kijelölési bontsa ki a objektum meghatározása során használt:</span><span class="sxs-lookup"><span data-stu-id="48642-146">The following elements specify the selection set used when you define which object to expand:</span></span>

    - [<span data-ttu-id="48642-147">A EnumerableExpansion (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-147">SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)

- <span data-ttu-id="48642-148">A következő elemeket adjon meg a kijelölési kiválasztási feltételek által használt.</span><span class="sxs-lookup"><span data-stu-id="48642-148">The following elements specify the selection set used by selection conditions.</span></span>

    - [<span data-ttu-id="48642-149">Konfiguráció (formátum) vezérlők SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-149">SelectionSetName Element for SelectionCondition for Controls for Configuration (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-configuration-format.md)

    - [<span data-ttu-id="48642-150">Nézet (formátum) vezérlők SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-150">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

    - [<span data-ttu-id="48642-151">A nézet (formátum) CustomControl SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-151">SelectionSetName Element for SelectionCondition for CustomControl for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

    - [<span data-ttu-id="48642-152">SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="48642-152">SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

    - [<span data-ttu-id="48642-153">A EntrySelectedBy ListEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="48642-153">SelectionSetName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format.md)

    - [<span data-ttu-id="48642-154">A EntrySelectedBy TableControl (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="48642-154">SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableControl (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

    - [<span data-ttu-id="48642-155">A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="48642-155">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

    - [<span data-ttu-id="48642-156">A GroupBy (formátum) SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="48642-156">SelectionSetName Element for SelectionCondition for GroupBy (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-groupby-format.md)

## <a name="see-also"></a><span data-ttu-id="48642-157">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="48642-157">See Also</span></span>

[<span data-ttu-id="48642-158">SelectionSets</span><span class="sxs-lookup"><span data-stu-id="48642-158">SelectionSets</span></span>](./selectionsets-element-format.md)

[<span data-ttu-id="48642-159">SelectionSet</span><span class="sxs-lookup"><span data-stu-id="48642-159">SelectionSet</span></span>](./selectionset-element-format.md)

[<span data-ttu-id="48642-160">Name (Név)</span><span class="sxs-lookup"><span data-stu-id="48642-160">Name</span></span>](./name-element-for-selectionset-format.md)

[<span data-ttu-id="48642-161">Típusok</span><span class="sxs-lookup"><span data-stu-id="48642-161">Types</span></span>](./types-element-for-selectionset-format.md)

[<span data-ttu-id="48642-162">PowerShell formázás fájlok</span><span class="sxs-lookup"><span data-stu-id="48642-162">PowerShell Formatting Files</span></span>](./powershell-formatting-files.md)

[<span data-ttu-id="48642-163">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="48642-163">Defining Conditions for when Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="48642-164">Egy PowerShell-formázást és típusok fájl írása</span><span class="sxs-lookup"><span data-stu-id="48642-164">Writing a PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
