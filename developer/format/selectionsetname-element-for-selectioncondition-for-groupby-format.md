---
title: A GroupBy (formátum) SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b9a4912-d755-42f3-8058-53c0797e28e4
caps.latest.revision: 6
ms.openlocfilehash: 371913eda2b09ff6788494b68738f2ad53ccb115
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063766"
---
# <a name="selectionsetname-element-for-selectioncondition-for-groupby-format"></a><span data-ttu-id="d6446-102">A GroupBy elemhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="d6446-102">SelectionSetName Element for SelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="d6446-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="d6446-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="d6446-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával.</span><span class="sxs-lookup"><span data-stu-id="d6446-104">When any of the types in this set are present, the condition is met, and the object is displayed by using this control.</span></span> <span data-ttu-id="d6446-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="d6446-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="d6446-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) SelectionSetName elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="d6446-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionCondition Element for EntrySelectedBy for GroupBy (Format) SelectionSetName Element for SelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d6446-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d6446-107">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="d6446-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="d6446-108">Attributes and Elements</span></span>

<span data-ttu-id="d6446-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="d6446-109">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="d6446-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d6446-110">Attributes</span></span>

<span data-ttu-id="d6446-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d6446-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d6446-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="d6446-112">Child Elements</span></span>

<span data-ttu-id="d6446-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d6446-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="d6446-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="d6446-114">Parent Elements</span></span>

|<span data-ttu-id="d6446-115">Elem</span><span class="sxs-lookup"><span data-stu-id="d6446-115">Element</span></span>|<span data-ttu-id="d6446-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="d6446-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d6446-117">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="d6446-117">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="d6446-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="d6446-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="d6446-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="d6446-119">Text Value</span></span>

<span data-ttu-id="d6446-120">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="d6446-120">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="d6446-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d6446-121">Remarks</span></span>

<span data-ttu-id="d6446-122">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="d6446-122">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="d6446-123">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="d6446-123">For more information about creating and referencing selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

<span data-ttu-id="d6446-124">Ha ez az elem meg van adva, nem adható meg a [TypeName](./typename-element-for-selectioncondition-for-groupby-format.md) elemet.</span><span class="sxs-lookup"><span data-stu-id="d6446-124">When this element is specified, you cannot specify the [TypeName](./typename-element-for-selectioncondition-for-groupby-format.md) element.</span></span> <span data-ttu-id="d6446-125">További információ a kiválasztási feltételek meghatározása: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="d6446-125">For more information about defining selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d6446-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d6446-126">See Also</span></span>

[<span data-ttu-id="d6446-127">A GroupBy (formátum) SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="d6446-127">TypeName Element for SelectionCondition for GroupBy (Format)</span></span>](./typename-element-for-selectioncondition-for-groupby-format.md)

[<span data-ttu-id="d6446-128">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="d6446-128">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="d6446-129">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="d6446-129">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="d6446-130">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="d6446-130">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="d6446-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="d6446-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
