---
title: A nézet (formátum) CustomControl SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a52b05a9-762e-4f1c-ad57-9d1710149722
caps.latest.revision: 10
ms.openlocfilehash: 25d46665ca5df3ddf49af5718d513b84c77988c8
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851547"
---
# <a name="selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format"></a><span data-ttu-id="3042a-102">A Nézet CustomControl eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="3042a-102">SelectionSetName Element for SelectionCondition for CustomControl for View (Format)</span></span>

<span data-ttu-id="3042a-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="3042a-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="3042a-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik a vezérlőelem használatával.</span><span class="sxs-lookup"><span data-stu-id="3042a-104">When any of the types in this set are present, the condition is met and the object is displayed using this control.</span></span> <span data-ttu-id="3042a-105">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="3042a-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="3042a-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Elem a CustomEntry nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="3042a-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) EntrySelectedBy Element for CustomEntry for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="3042a-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3042a-107">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="3042a-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="3042a-108">Attributes and Elements</span></span>

<span data-ttu-id="3042a-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="3042a-109">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="3042a-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="3042a-110">Attributes</span></span>

<span data-ttu-id="3042a-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3042a-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="3042a-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="3042a-112">Child Elements</span></span>

<span data-ttu-id="3042a-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3042a-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="3042a-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="3042a-114">Parent Elements</span></span>

|<span data-ttu-id="3042a-115">Elem</span><span class="sxs-lookup"><span data-stu-id="3042a-115">Element</span></span>|<span data-ttu-id="3042a-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="3042a-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3042a-117">A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="3042a-117">SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)|<span data-ttu-id="3042a-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="3042a-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="3042a-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="3042a-119">Text Value</span></span>

<span data-ttu-id="3042a-120">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="3042a-120">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="3042a-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3042a-121">Remarks</span></span>

<span data-ttu-id="3042a-122">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="3042a-122">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="3042a-123">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="3042a-123">For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

<span data-ttu-id="3042a-124">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="3042a-124">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="3042a-125">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="3042a-125">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3042a-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3042a-126">See Also</span></span>

[<span data-ttu-id="3042a-127">A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="3042a-127">SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

[<span data-ttu-id="3042a-128">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="3042a-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="3042a-129">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="3042a-129">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="3042a-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="3042a-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
