---
title: EntrySelectedBy ListEntry (formátum) esetében a SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eae67e47-6c60-4741-8430-78d2cb6067b1
caps.latest.revision: 10
ms.openlocfilehash: ccfc0b772ad3b2d1979c7c832a5153de870035d7
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075511"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format"></a><span data-ttu-id="e67da-102">Az ListEntry EntrySelectedBy eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e67da-102">SelectionSetName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>

<span data-ttu-id="e67da-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="e67da-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="e67da-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció a listanézet használatával.</span><span class="sxs-lookup"><span data-stu-id="e67da-104">When any of the types in this set are present, the condition is met, and the object is displayed by using this definition of the list view.</span></span>

<span data-ttu-id="e67da-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára EntrySelectedBy ListEntry (formátum) SelectionSetName elemhez tartozó SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a</span><span class="sxs-lookup"><span data-stu-id="e67da-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format) SelectionSetName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e67da-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e67da-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="e67da-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e67da-107">Attributes and Elements</span></span>

<span data-ttu-id="e67da-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="e67da-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e67da-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e67da-109">Attributes</span></span>

<span data-ttu-id="e67da-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e67da-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e67da-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e67da-111">Child Elements</span></span>

<span data-ttu-id="e67da-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e67da-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e67da-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e67da-113">Parent Elements</span></span>

|<span data-ttu-id="e67da-114">Elem</span><span class="sxs-lookup"><span data-stu-id="e67da-114">Element</span></span>|<span data-ttu-id="e67da-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="e67da-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e67da-116">A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e67da-116">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="e67da-117">Határozza meg azt a feltételt, amelyet ez a definíció a listanézet használata léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="e67da-117">Defines the condition that must exist to use this definition of the list view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e67da-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="e67da-118">Text Value</span></span>

<span data-ttu-id="e67da-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="e67da-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="e67da-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e67da-120">Remarks</span></span>

<span data-ttu-id="e67da-121">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="e67da-121">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="e67da-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="e67da-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="e67da-123">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="e67da-123">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="e67da-124">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="e67da-124">For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

<span data-ttu-id="e67da-125">A listanézet egyéb összetevőivel kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="e67da-125">For more information about other components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e67da-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e67da-126">See Also</span></span>

[<span data-ttu-id="e67da-127">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="e67da-127">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="e67da-128">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="e67da-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="e67da-129">A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e67da-129">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="e67da-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e67da-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
