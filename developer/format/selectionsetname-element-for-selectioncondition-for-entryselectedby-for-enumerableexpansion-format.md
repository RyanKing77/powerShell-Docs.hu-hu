---
title: EntrySelectedBy EnumerableExpansion (formátum) esetében a SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7b7af0b2-68e6-43c3-adcc-7c58007fced8
caps.latest.revision: 13
ms.openlocfilehash: 6f7c8d9af3c1c2fbda0208148b0088161701fdbe
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850462"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="0a3ff-102">Az EnumerableExpansion EntrySelectedBy eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0a3ff-102">SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="0a3ff-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="0a3ff-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-104">When any of the types in this set are present, the condition is met.</span></span>

<span data-ttu-id="0a3ff-105">Konfigurációs elem DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansions elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a SelectionSetName eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="0a3ff-105">Configuration Element DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansions Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format) SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0a3ff-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0a3ff-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0a3ff-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0a3ff-107">Attributes and Elements</span></span>

<span data-ttu-id="0a3ff-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-108">The following sections describe attributes, child elements, and parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0a3ff-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0a3ff-109">Attributes</span></span>

<span data-ttu-id="0a3ff-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0a3ff-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0a3ff-111">Child Elements</span></span>

<span data-ttu-id="0a3ff-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0a3ff-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0a3ff-113">Parent Elements</span></span>

|<span data-ttu-id="0a3ff-114">Elem</span><span class="sxs-lookup"><span data-stu-id="0a3ff-114">Element</span></span>|<span data-ttu-id="0a3ff-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="0a3ff-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0a3ff-116">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-116">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="0a3ff-117">Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-117">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0a3ff-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="0a3ff-118">Text Value</span></span>

<span data-ttu-id="0a3ff-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="0a3ff-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0a3ff-120">Remarks</span></span>

<span data-ttu-id="0a3ff-121">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-121">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="0a3ff-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="0a3ff-122">For more information about how to use selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="0a3ff-123">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-123">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="0a3ff-124">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="0a3ff-124">For more information about creating and referencing selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0a3ff-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0a3ff-125">See Also</span></span>

[<span data-ttu-id="0a3ff-126">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="0a3ff-126">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="0a3ff-127">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="0a3ff-127">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="0a3ff-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0a3ff-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
