---
title: EntrySelectedBy TableControl (formátum) esetében a SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17ae4d6b-dc95-4a1d-8e32-31ff084a951f
caps.latest.revision: 10
ms.openlocfilehash: edb163f2b0b5129bd741677dce882888d9bbfd89
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851904"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="97895-102">Az TableControl EntrySelectedBy eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="97895-102">SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="97895-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="97895-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="97895-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció, a táblázat nézet használatával.</span><span class="sxs-lookup"><span data-stu-id="97895-104">When any of the types in this set are present, the condition is met, and the object is displayed by using this definition of the table view.</span></span>

<span data-ttu-id="97895-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) TableRowEntry (formátum) SelectionSetName elemhez tartozó SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="97895-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element for TableRowEntry (Format) SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format) SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="97895-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="97895-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="97895-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="97895-107">Attributes and Elements</span></span>

<span data-ttu-id="97895-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="97895-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="97895-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="97895-109">Attributes</span></span>

<span data-ttu-id="97895-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="97895-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="97895-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="97895-111">Child Elements</span></span>

<span data-ttu-id="97895-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="97895-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="97895-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="97895-113">Parent Elements</span></span>

|<span data-ttu-id="97895-114">Elem</span><span class="sxs-lookup"><span data-stu-id="97895-114">Element</span></span>|<span data-ttu-id="97895-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="97895-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="97895-116">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="97895-116">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="97895-117">Határozza meg azt a feltételt, amelyet ez a táblázat nézet definícióját használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="97895-117">Defines the condition that must exist to use for this definition of the table view.</span></span>|

## <a name="text-value"></a><span data-ttu-id="97895-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="97895-118">Text Value</span></span>

<span data-ttu-id="97895-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="97895-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="97895-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="97895-120">Remarks</span></span>

<span data-ttu-id="97895-121">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="97895-121">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="97895-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="97895-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="97895-123">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="97895-123">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="97895-124">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="97895-124">For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

<span data-ttu-id="97895-125">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="97895-125">For more information about other components of a wide view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="97895-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="97895-126">See Also</span></span>

[<span data-ttu-id="97895-127">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="97895-127">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="97895-128">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="97895-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="97895-129">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="97895-129">TypeName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="97895-130">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="97895-130">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="97895-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="97895-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
