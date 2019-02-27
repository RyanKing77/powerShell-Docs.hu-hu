---
title: A GroupBy (formátum) CustomEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a317d482-73cc-4c98-a002-1357fa879cd7
caps.latest.revision: 7
ms.openlocfilehash: cf1a80e845c38d97d71f26eba63c38a550958b79
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851582"
---
# <a name="entryselectedby-element-for-customentry-for-groupby-format"></a><span data-ttu-id="ea776-102">A GroupBy elemhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ea776-102">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>

<span data-ttu-id="ea776-103">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ea776-103">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span> <span data-ttu-id="ea776-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="ea776-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="ea776-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomControl GroupBy (formátum) EntrySelectedBy elemhez tartozó CustomEntry a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="ea776-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ea776-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ea776-106">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ea776-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ea776-107">Attributes and Elements</span></span>

<span data-ttu-id="ea776-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="ea776-108">The following sections describe attributes, child elements, and parent element of the `EntrySelectedBy` element.</span></span> <span data-ttu-id="ea776-109">Meg kell adnia legalább egy típusa, kijelölés set vagy -definíció kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="ea776-109">You must specify at least one type, selection set, or selection condition for a definition.</span></span> <span data-ttu-id="ea776-110">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="ea776-110">There is no maximum limit to the number of child elements that you can use.</span></span>

### <a name="attributes"></a><span data-ttu-id="ea776-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ea776-111">Attributes</span></span>

<span data-ttu-id="ea776-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ea776-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ea776-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ea776-113">Child Elements</span></span>

|<span data-ttu-id="ea776-114">Elem</span><span class="sxs-lookup"><span data-stu-id="ea776-114">Element</span></span>|<span data-ttu-id="ea776-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="ea776-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ea776-116">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-116">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="ea776-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ea776-117">Optional element.</span></span><br /><br /> <span data-ttu-id="ea776-118">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="ea776-118">Defines the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="ea776-119">A GroupBy (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-119">SelectionSetName Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="ea776-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ea776-120">Optional element.</span></span><br /><br /> <span data-ttu-id="ea776-121">Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ea776-121">Specifies a set of .NET types that use this definition of the control.</span></span>|
|[<span data-ttu-id="ea776-122">A GroupBy (formátum) EntrySelectedBy TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-122">TypeName Element for EntrySelectedBy for GroupBy (Format)</span></span>](./typename-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="ea776-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ea776-123">Optional element.</span></span><br /><br /> <span data-ttu-id="ea776-124">Ez a definíció, a vezérlő használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="ea776-124">Specifies a .NET type that uses this definition of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="ea776-125">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ea776-125">Parent Elements</span></span>

|<span data-ttu-id="ea776-126">Elem</span><span class="sxs-lookup"><span data-stu-id="ea776-126">Element</span></span>|<span data-ttu-id="ea776-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="ea776-127">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ea776-128">A GroupBy (formátum) CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-128">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>](./customentry-element-for-customcontrol-for-groupby-format.md)|<span data-ttu-id="ea776-129">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="ea776-129">Provides a definition of the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="ea776-130">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ea776-130">Remarks</span></span>

<span data-ttu-id="ea776-131">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely léteznie kell a definíciójában használt, például ha egy objektum rendelkezik-e egy adott tulajdonságra vagy ha egy adott tulajdonság értéke, vagy a parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="ea776-131">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or when a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="ea776-132">További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ea776-132">For more information about selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ea776-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ea776-133">See Also</span></span>

[<span data-ttu-id="ea776-134">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-134">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="ea776-135">A GroupBy (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-135">SelectionSetName Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="ea776-136">A GroupBy (formátum) EntrySelectedBy TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-136">TypeName Element for EntrySelectedBy for GroupBy (Format)</span></span>](./typename-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="ea776-137">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="ea776-137">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)

[<span data-ttu-id="ea776-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ea776-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
