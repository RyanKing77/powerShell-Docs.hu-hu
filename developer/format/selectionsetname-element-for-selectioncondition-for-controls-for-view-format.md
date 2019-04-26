---
title: SelectionSetName elemet a vezérlők (formátum) nézet SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: daea8c6f-873a-4639-9eee-599642822958
caps.latest.revision: 6
ms.openlocfilehash: 697f2ea284393ebddd77a862c408f27f3d332900
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063887"
---
# <a name="selectionsetname-element-for-selectioncondition-for-controls-for-view-format"></a><span data-ttu-id="729cd-102">A Nézet Vezérlők eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="729cd-102">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>

<span data-ttu-id="729cd-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="729cd-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="729cd-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával.</span><span class="sxs-lookup"><span data-stu-id="729cd-104">When any of the types in this set are present, the condition is met and the object is displayed using this control.</span></span> <span data-ttu-id="729cd-105">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="729cd-105">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="729cd-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum) SelectionSetName eleme SelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="729cd-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format) SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="729cd-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="729cd-107">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="729cd-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="729cd-108">Attributes and Elements</span></span>

<span data-ttu-id="729cd-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="729cd-109">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="729cd-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="729cd-110">Attributes</span></span>

<span data-ttu-id="729cd-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="729cd-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="729cd-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="729cd-112">Child Elements</span></span>

<span data-ttu-id="729cd-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="729cd-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="729cd-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="729cd-114">Parent Elements</span></span>

|<span data-ttu-id="729cd-115">Elem</span><span class="sxs-lookup"><span data-stu-id="729cd-115">Element</span></span>|<span data-ttu-id="729cd-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="729cd-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="729cd-117">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="729cd-117">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="729cd-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="729cd-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="729cd-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="729cd-119">Text Value</span></span>

<span data-ttu-id="729cd-120">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="729cd-120">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="729cd-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="729cd-121">Remarks</span></span>

<span data-ttu-id="729cd-122">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="729cd-122">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="729cd-123">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="729cd-123">For more information about creating and referencing selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

<span data-ttu-id="729cd-124">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="729cd-124">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="729cd-125">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="729cd-125">For more information about how to use selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="729cd-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="729cd-126">See Also</span></span>

[<span data-ttu-id="729cd-127">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="729cd-127">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

[<span data-ttu-id="729cd-128">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="729cd-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="729cd-129">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="729cd-129">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="729cd-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="729cd-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
