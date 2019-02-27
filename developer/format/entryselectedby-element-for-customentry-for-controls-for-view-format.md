---
title: EntrySelectedBy elemet a vezérlők (formátum) nézet CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b3d80a7d-3797-4c46-ae74-ae5cda79b24f
caps.latest.revision: 8
ms.openlocfilehash: efb20c3f2077547e6eb3cb28240512b444f9c481
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56849286"
---
# <a name="entryselectedby-element-for-customentry-for-controls-for-view-format"></a><span data-ttu-id="1fb6b-102">A Nézet Vezérlők eleméhez tartozó CustomEntry EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="1fb6b-102">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>

<span data-ttu-id="1fb6b-103">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-103">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span> <span data-ttu-id="1fb6b-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="1fb6b-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez</span><span class="sxs-lookup"><span data-stu-id="1fb6b-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="1fb6b-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="1fb6b-106">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="1fb6b-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="1fb6b-107">Attributes and Elements</span></span>

<span data-ttu-id="1fb6b-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-108">The following sections describe attributes, child elements, and parent element of the `EntrySelectedBy` element.</span></span> <span data-ttu-id="1fb6b-109">Meg kell adnia legalább egy típusa, kijelölés set vagy -definíció kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-109">You must specify at least one type, selection set, or selection condition for a definition.</span></span> <span data-ttu-id="1fb6b-110">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-110">There is no maximum limit to the number of child elements that you can use.</span></span>

### <a name="attributes"></a><span data-ttu-id="1fb6b-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="1fb6b-111">Attributes</span></span>

<span data-ttu-id="1fb6b-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="1fb6b-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="1fb6b-113">Child Elements</span></span>

|<span data-ttu-id="1fb6b-114">Elem</span><span class="sxs-lookup"><span data-stu-id="1fb6b-114">Element</span></span>|<span data-ttu-id="1fb6b-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="1fb6b-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1fb6b-116">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-116">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="1fb6b-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-117">Optional element.</span></span><br /><br /> <span data-ttu-id="1fb6b-118">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-118">Defines the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="1fb6b-119">Nézet (formátum) vezérlők EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-119">SelectionSetName Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="1fb6b-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-120">Optional element.</span></span><br /><br /> <span data-ttu-id="1fb6b-121">Ez a definíció, a vezérlő használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-121">Specifies a set of .NET types that use this definition of the control.</span></span>|
|[<span data-ttu-id="1fb6b-122">Nézet (formátum) vezérlők EntrySelectedBy TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-122">TypeName Element for EntrySelectedBy for Controls for View (Format)</span></span>](./typename-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="1fb6b-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-123">Optional element.</span></span><br /><br /> <span data-ttu-id="1fb6b-124">Ez a definíció, a vezérlő használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-124">Specifies a .NET type that uses this definition of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="1fb6b-125">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="1fb6b-125">Parent Elements</span></span>

|<span data-ttu-id="1fb6b-126">Elem</span><span class="sxs-lookup"><span data-stu-id="1fb6b-126">Element</span></span>|<span data-ttu-id="1fb6b-127">Leírás</span><span class="sxs-lookup"><span data-stu-id="1fb6b-127">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="1fb6b-128">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-128">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)|<span data-ttu-id="1fb6b-129">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-129">Provides a definition of the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="1fb6b-130">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="1fb6b-130">Remarks</span></span>

<span data-ttu-id="1fb6b-131">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely léteznie kell a definíciójában használt, például ha egy objektum rendelkezik-e egy adott tulajdonságra vagy ha egy adott tulajdonság értéke, vagy a parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-131">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or when a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="1fb6b-132">További információ a kiválasztási feltételek: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="1fb6b-132">For more information about selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1fb6b-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="1fb6b-133">See Also</span></span>

[<span data-ttu-id="1fb6b-134">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-134">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)

[<span data-ttu-id="1fb6b-135">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="1fb6b-135">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
