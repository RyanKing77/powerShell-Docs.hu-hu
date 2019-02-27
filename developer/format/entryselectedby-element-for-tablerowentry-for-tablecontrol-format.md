---
title: TableControl (formátum) a TableRowEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49623fcf-1238-4d20-a7ce-238d47d9d565
caps.latest.revision: 15
ms.openlocfilehash: e18564c10898c73128e0a4bc7d077e7c7ffb1c22
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851239"
---
# <a name="entryselectedby-element-for-tablerowentry--for-tablecontrol-format"></a><span data-ttu-id="fab56-102">A TableControl elemhez tartozó TableRowEntry EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="fab56-102">EntrySelectedBy Element for TableRowEntry  for TableControl (Format)</span></span>

<span data-ttu-id="fab56-103">A .NET-típusokat, amelyek a táblázatos nézetre vagy a feltételt, amelyet a definíció használandó léteznie kell a definíció határozza meg.</span><span class="sxs-lookup"><span data-stu-id="fab56-103">Defines the .NET types that use this definition of the table view or the condition that must exist for this definition to be used.</span></span>

<span data-ttu-id="fab56-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="fab56-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="fab56-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="fab56-105">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="fab56-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="fab56-106">Attributes and Elements</span></span>

<span data-ttu-id="fab56-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="fab56-107">The following sections describe attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="fab56-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="fab56-108">Attributes</span></span>

<span data-ttu-id="fab56-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="fab56-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="fab56-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="fab56-110">Child Elements</span></span>

|<span data-ttu-id="fab56-111">Elem</span><span class="sxs-lookup"><span data-stu-id="fab56-111">Element</span></span>|<span data-ttu-id="fab56-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="fab56-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="fab56-113">A TableControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fab56-113">SelectionCondition Element for EntrySelectedBy for TableControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="fab56-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="fab56-114">Optional element.</span></span><br /><br /> <span data-ttu-id="fab56-115">Határozza meg azt a feltételt, amelyet a táblázat nézet definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="fab56-115">Defines the condition that must exist for this table view definition to be used.</span></span>|
|[<span data-ttu-id="fab56-116">A TableControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="fab56-116">SelectionSetName Element for EntrySelectedBy for TableControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="fab56-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="fab56-117">Optional element.</span></span><br /><br /> <span data-ttu-id="fab56-118">.NET-típusokat, amelyek a tábla nézetdefiníció egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="fab56-118">Specifies a set of .NET types that use this table view definition.</span></span>|
|[<span data-ttu-id="fab56-119">EntrySelectedBy TableControl (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="fab56-119">TypeName Element for EntrySelectedBy for TableControl (Format)</span></span>](./typename-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="fab56-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="fab56-120">Optional element.</span></span><br /><br /> <span data-ttu-id="fab56-121">A tábla nézetdefiníció használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="fab56-121">Specifies a .NET type that uses this table view definition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="fab56-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="fab56-122">Parent Elements</span></span>

|<span data-ttu-id="fab56-123">Elem</span><span class="sxs-lookup"><span data-stu-id="fab56-123">Element</span></span>|<span data-ttu-id="fab56-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="fab56-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="fab56-125">TableRowEntry eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="fab56-125">TableRowEntry Element for TableControl (Format)</span></span>](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)|<span data-ttu-id="fab56-126">Határozza meg, amely egy sort a táblában megjelennek az adatok.</span><span class="sxs-lookup"><span data-stu-id="fab56-126">Defines the data that is displayed in a row of the table.</span></span>|

## <a name="remarks"></a><span data-ttu-id="fab56-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="fab56-127">Remarks</span></span>

<span data-ttu-id="fab56-128">Meg kell adnia legalább egy típusa, a kijelölés készlet vagy a kiválasztási feltétel táblázat nézet definícióját.</span><span class="sxs-lookup"><span data-stu-id="fab56-128">You must specify at least one type, selection set, or selection condition for a table view definition.</span></span> <span data-ttu-id="fab56-129">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="fab56-129">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="fab56-130">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="fab56-130">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or that a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="fab56-131">További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="fab56-131">For more information about selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="fab56-132">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="fab56-132">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="fab56-133">Példa</span><span class="sxs-lookup"><span data-stu-id="fab56-133">Example</span></span>

<span data-ttu-id="fab56-134">A következő példa bemutatja egy `TableRowEntry` elem, amellyel a tulajdonságainak megjelenítéséhez a [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objektum.</span><span class="sxs-lookup"><span data-stu-id="fab56-134">The following example shows a `TableRowEntry` element that is used to display the properties of the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object.</span></span>

```xml
<TableRowEntry>
  <EntrySelectedBy>
    <TypeName>System.Diagnostics.Process</TypeName>
  </EntrySelectedBy>
  <TableColumnItems>
    <TableColumnItem>
      <PropertyName>PropertyForFirstColumn</PropertyName>
    </TableColumnItem>
    <TableColumnItem>
      <PropertyName>PropertyForSecondColumn</PropertyName>
    </TableColumnItem>
  </TableColumnItems>
</TableRowEntry>
```

## <a name="see-also"></a><span data-ttu-id="fab56-135">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="fab56-135">See Also</span></span>

[<span data-ttu-id="fab56-136">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="fab56-136">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="fab56-137">A TableControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="fab56-137">SelectionCondition Element for EntrySelectedBy for TableControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="fab56-138">A TableControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="fab56-138">SelectionSetName Element for EntrySelectedBy for TableControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="fab56-139">TableRowEntry eleme TableControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="fab56-139">TableRowEntry Element for TableControl (Format)</span></span>](./tablerowentry-element-for-tablerowentroes-for-tablecontrol-format.md)

[<span data-ttu-id="fab56-140">EntrySelectedBy TableControl (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="fab56-140">TypeName Element for EntrySelectedBy for TableControl (Format)</span></span>](./typename-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="fab56-141">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="fab56-141">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
