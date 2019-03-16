---
title: ListControl (formátum) a ListEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0f7a74e9-764d-46ce-ab8e-8b9314ce1659
caps.latest.revision: 12
ms.openlocfilehash: 442565d25f60ae8e04501f3f9ffba35d486fbc8a
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054935"
---
# <a name="entryselectedby-element-for-listentry-for-listcontrol-format"></a><span data-ttu-id="b68d4-102">A ListControl elemhez tartozó ListEntry EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="b68d4-102">EntrySelectedBy Element for ListEntry for ListControl (Format)</span></span>

<span data-ttu-id="b68d4-103">A .NET-típusokat, amelyek a nézet definíciója vagy a feltétellel, hogy léteznie kell a definíció használandó határoz meg.</span><span class="sxs-lookup"><span data-stu-id="b68d4-103">Defines the .NET types that use this list view definition or the condition that must exist for this definition to be used.</span></span> <span data-ttu-id="b68d4-104">A legtöbb esetben csak egyetlen definíciót lista nézetben van szükség.</span><span class="sxs-lookup"><span data-stu-id="b68d4-104">In most cases only one definition is needed for a list view.</span></span> <span data-ttu-id="b68d4-105">Azonban a listanézet víc definic biztosít, ha azt szeretné használni a ugyanabban listanézetet jelennek meg a különböző objektumok különböző adatok.</span><span class="sxs-lookup"><span data-stu-id="b68d4-105">However, you can provide multiple definitions for the list view if you want to use the same list view to display different data for different objects.</span></span>

<span data-ttu-id="b68d4-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elemhez tartozó ListEntry ListControl (formátum) EntrySelectedBy elemhez tartozó ListEntry a ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b68d4-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntry for ListControl (Format) EntrySelectedBy Element for ListEntry for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b68d4-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b68d4-107">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="b68d4-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="b68d4-108">Attributes and Elements</span></span>

<span data-ttu-id="b68d4-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="b68d4-109">The following sections describe the attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b68d4-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="b68d4-110">Attributes</span></span>

<span data-ttu-id="b68d4-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b68d4-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b68d4-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="b68d4-112">Child Elements</span></span>

|<span data-ttu-id="b68d4-113">Elem</span><span class="sxs-lookup"><span data-stu-id="b68d4-113">Element</span></span>|<span data-ttu-id="b68d4-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="b68d4-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b68d4-115">A ListControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="b68d4-115">SelectionCondition Element for EntrySelectedBy for ListControl  (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="b68d4-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="b68d4-116">Optional element.</span></span><br /><br /> <span data-ttu-id="b68d4-117">Határozza meg azt a feltételt, amelyet a lista nézet definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="b68d4-117">Defines the condition that must exist for this list view definition to be used.</span></span>|
|[<span data-ttu-id="b68d4-118">A ListControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="b68d4-118">SelectionSetName Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="b68d4-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="b68d4-119">Optional element.</span></span><br /><br /> <span data-ttu-id="b68d4-120">.NET-típusokat, amelyek a nézet definíciója egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="b68d4-120">Specifies a set of .NET types that use this list view definition.</span></span>|
|[<span data-ttu-id="b68d4-121">EntrySelectedBy ListControl (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="b68d4-121">TypeName Element for EntrySelectedBy for ListControl (Format)</span></span>](./typename-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="b68d4-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="b68d4-122">Optional element.</span></span><br /><br /> <span data-ttu-id="b68d4-123">A nézet definíciója használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="b68d4-123">Specifies a .NET type that uses this list view definition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="b68d4-124">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="b68d4-124">Parent Elements</span></span>

|<span data-ttu-id="b68d4-125">Elem</span><span class="sxs-lookup"><span data-stu-id="b68d4-125">Element</span></span>|<span data-ttu-id="b68d4-126">Leírás</span><span class="sxs-lookup"><span data-stu-id="b68d4-126">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b68d4-127">ListEntry eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b68d4-127">ListEntry Element for ListControl (Format)</span></span>](./listentry-element-for-listcontrol-format.md)|<span data-ttu-id="b68d4-128">Határozza meg, hogy a lista a sorok jelennek meg.</span><span class="sxs-lookup"><span data-stu-id="b68d4-128">Defines how the rows of the list are displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="b68d4-129">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b68d4-129">Remarks</span></span>

<span data-ttu-id="b68d4-130">Meg kell adnia legalább egy típusa, a kijelölés készlet vagy a kiválasztási feltétel lista nézet definícióját.</span><span class="sxs-lookup"><span data-stu-id="b68d4-130">You must specify at least one type, selection set, or selection condition for a list view definition.</span></span> <span data-ttu-id="b68d4-131">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="b68d4-131">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="b68d4-132">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="b68d4-132">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or that a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="b68d4-133">További információ a kiválasztási feltételek: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="b68d4-133">For more information about selection conditions, see [Defining Conditions for when Data is displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="b68d4-134">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="b68d4-134">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="b68d4-135">Példa</span><span class="sxs-lookup"><span data-stu-id="b68d4-135">Example</span></span>

<span data-ttu-id="b68d4-136">Az alábbi példa bemutatja, hogyan definiálásához az adott nézet használata a .NET-típus neve.</span><span class="sxs-lookup"><span data-stu-id="b68d4-136">The following example shows how to define the objects for a list view using their .NET type name.</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>
    <TypeName>NameofDotNetType</TypeName>>
  </EntrySelectedBy>
</ListEntry>
```

## <a name="see-also"></a><span data-ttu-id="b68d4-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b68d4-137">See Also</span></span>

[<span data-ttu-id="b68d4-138">ListEntry eleme ListControl (formátum)</span><span class="sxs-lookup"><span data-stu-id="b68d4-138">ListEntry Element for ListControl (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="b68d4-139">A ListControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="b68d4-139">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="b68d4-140">A ListControl (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="b68d4-140">SelectionSetName Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="b68d4-141">EntrySelectedBy ListControl (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="b68d4-141">TypeName Element for EntrySelectedBy for ListControl (Format)</span></span>](./typename-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="b68d4-142">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="b68d4-142">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="b68d4-143">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="b68d4-143">Defining Conditions for when Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="b68d4-144">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="b68d4-144">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
