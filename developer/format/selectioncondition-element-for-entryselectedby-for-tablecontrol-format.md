---
title: TableControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 912f3e63-e4d5-41ce-8710-6dfd8c885dc2
caps.latest.revision: 12
ms.openlocfilehash: 2faca6021dc26878869bdd2d35bc4ffc64d0fe7b
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850476"
---
# <a name="selectioncondition-element-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="28123-102">A TableControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="28123-102">SelectionCondition Element for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="28123-103">Határozza meg azt a feltételt, amelyet ez a táblázat nézet definícióját használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="28123-103">Defines the condition that must exist to use for this definition of the table view.</span></span> <span data-ttu-id="28123-104">Kiválasztási feltételek, amelyek a tábla definíciója adható meg száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="28123-104">There is no limit to the number of selection conditions that can be specified for a table definition.</span></span>

<span data-ttu-id="28123-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="28123-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element for TableRowEntry (Format) SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="28123-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="28123-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="28123-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="28123-107">Attributes and Elements</span></span>

<span data-ttu-id="28123-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a szülőelemet SelectionCondition prvku.</span><span class="sxs-lookup"><span data-stu-id="28123-108">The following sections describe attributes, child elements, and the parent element of the SelectionCondition element.</span></span>

### <a name="attributes"></a><span data-ttu-id="28123-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="28123-109">Attributes</span></span>

<span data-ttu-id="28123-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="28123-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="28123-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="28123-111">Child Elements</span></span>

|<span data-ttu-id="28123-112">Elem</span><span class="sxs-lookup"><span data-stu-id="28123-112">Element</span></span>|<span data-ttu-id="28123-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="28123-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="28123-114">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="28123-114">PropertyName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md)|<span data-ttu-id="28123-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="28123-115">Optional element.</span></span><br /><br /> <span data-ttu-id="28123-116">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="28123-116">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="28123-117">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="28123-117">ScriptBlock Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="28123-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="28123-118">Optional element.</span></span><br /><br /> <span data-ttu-id="28123-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="28123-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="28123-120">A EntrySelectedBy TableRowEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="28123-120">SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="28123-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="28123-121">Optional element.</span></span><br /><br /> <span data-ttu-id="28123-122">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="28123-122">Specifies the set of .NET types that trigger the condition.</span></span>|
|[<span data-ttu-id="28123-123">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="28123-123">TypeName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="28123-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="28123-124">Optional element.</span></span><br /><br /> <span data-ttu-id="28123-125">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="28123-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="28123-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="28123-126">Parent Elements</span></span>

|<span data-ttu-id="28123-127">Elem</span><span class="sxs-lookup"><span data-stu-id="28123-127">Element</span></span>|<span data-ttu-id="28123-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="28123-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="28123-129">EntrySelectedBy eleme TableRowEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="28123-129">EntrySelectedBy Element for TableRowEntry (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="28123-130">Meghatározza a .NET-típusokat, amelyek a tábla bejegyzés vagy a feltétellel, hogy a bejegyzés használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="28123-130">Defines the .NET types that use this table entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="28123-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="28123-131">Remarks</span></span>

<span data-ttu-id="28123-132">Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="28123-132">Each list entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="28123-133">Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="28123-133">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="28123-134">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="28123-134">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="28123-135">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="28123-135">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="28123-136">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="28123-136">For more information about how to use selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="28123-137">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="28123-137">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="28123-138">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="28123-138">See Also</span></span>

[<span data-ttu-id="28123-139">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="28123-139">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="28123-140">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="28123-140">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="28123-141">EntrySelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="28123-141">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="28123-142">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="28123-142">PropertyName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md)

[<span data-ttu-id="28123-143">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="28123-143">ScriptBlock Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="28123-144">A EntrySelectedBy TableRowEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="28123-144">SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="28123-145">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="28123-145">TypeName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="28123-146">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="28123-146">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
