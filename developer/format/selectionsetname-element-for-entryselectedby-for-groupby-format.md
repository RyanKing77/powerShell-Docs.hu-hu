---
title: A GroupBy (formátum) EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d569c623-2277-49e3-933e-c26262b91cd5
caps.latest.revision: 6
ms.openlocfilehash: 69cd113c444b4e3c5dceabcdfddb439cd1376f6b
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064067"
---
# <a name="selectionsetname-element-for-entryselectedby-for-groupby-format"></a><span data-ttu-id="2a4fa-102">A GroupBy elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="2a4fa-102">SelectionSetName Element for EntrySelectedBy for GroupBy (Format)</span></span>

<span data-ttu-id="2a4fa-103">Regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-103">Specifies a set of .NET objects for the list entry.</span></span> <span data-ttu-id="2a4fa-104">Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-104">There is no limit to the number of selection sets that can be specified for an entry.</span></span> <span data-ttu-id="2a4fa-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="2a4fa-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy GroupBy (formátum) esetében a GroupBy (formátum) SelectionSetName elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="2a4fa-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionSetName Element for EntrySelectedBy for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2a4fa-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2a4fa-107">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2a4fa-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="2a4fa-108">Attributes and Elements</span></span>

<span data-ttu-id="2a4fa-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-109">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2a4fa-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="2a4fa-110">Attributes</span></span>

<span data-ttu-id="2a4fa-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2a4fa-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="2a4fa-112">Child Elements</span></span>

<span data-ttu-id="2a4fa-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="2a4fa-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="2a4fa-114">Parent Elements</span></span>

|<span data-ttu-id="2a4fa-115">Elem</span><span class="sxs-lookup"><span data-stu-id="2a4fa-115">Element</span></span>|<span data-ttu-id="2a4fa-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a4fa-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2a4fa-117">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-117">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="2a4fa-118">A .NET-típusokat, amelyek egyéni tételhez vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-118">Defines the .NET types that use this custom entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="2a4fa-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="2a4fa-119">Text Value</span></span>

<span data-ttu-id="2a4fa-120">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-120">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="2a4fa-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2a4fa-121">Remarks</span></span>

<span data-ttu-id="2a4fa-122">Minden egyes egyéni vezérlőt definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-122">Each custom control definition must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="2a4fa-123">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-123">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="2a4fa-124">Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-124">For example, you may want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="2a4fa-125">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="2a4fa-125">For more information about defining selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

<span data-ttu-id="2a4fa-126">Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="2a4fa-126">For more information about the components of a custom control view, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2a4fa-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2a4fa-127">See Also</span></span>

[<span data-ttu-id="2a4fa-128">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="2a4fa-128">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="2a4fa-129">Egyéni vezérlők létrehozását</span><span class="sxs-lookup"><span data-stu-id="2a4fa-129">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="2a4fa-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="2a4fa-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
