---
title: EntrySelectedBy WideEntry (formátum) esetében a SelectionCondition SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a13a429c-a31b-4e29-828c-c0c0917b5415
caps.latest.revision: 11
ms.openlocfilehash: baea89e4b259611dfa45b6bcf94fa0bf2df6b9de
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845499"
---
# <a name="selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format"></a><span data-ttu-id="85042-102">Az WideEntry EntrySelectedBy eleméhez tartozó SelectionCondition SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="85042-102">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

<span data-ttu-id="85042-103">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="85042-103">Specifies the set of .NET types that trigger the condition.</span></span> <span data-ttu-id="85042-104">Az ebben a készletben típusok találhatók, ha a feltétel nem teljesül, és az objektum megjelenik ez a definíció, a széles nézet használatával.</span><span class="sxs-lookup"><span data-stu-id="85042-104">When any of the types in this set are present, the condition is met, and the object is displayed by using this definition of the wide view.</span></span>

<span data-ttu-id="85042-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára EntrySelectedBy WideEntry (formátum) SelectionSetName elemhez tartozó SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a</span><span class="sxs-lookup"><span data-stu-id="85042-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="85042-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="85042-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="85042-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="85042-107">Attributes and Elements</span></span>

<span data-ttu-id="85042-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="85042-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="85042-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="85042-109">Attributes</span></span>

<span data-ttu-id="85042-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="85042-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="85042-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="85042-111">Child Elements</span></span>

<span data-ttu-id="85042-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="85042-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="85042-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="85042-113">Parent Elements</span></span>

|<span data-ttu-id="85042-114">Elem</span><span class="sxs-lookup"><span data-stu-id="85042-114">Element</span></span>|<span data-ttu-id="85042-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="85042-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="85042-116">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="85042-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="85042-117">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="85042-117">Defines the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="85042-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="85042-118">Text Value</span></span>

<span data-ttu-id="85042-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="85042-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="85042-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="85042-120">Remarks</span></span>

<span data-ttu-id="85042-121">A kiválasztási feltétel egy kijelölés set vagy a .NET-típus is megadhat, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="85042-121">The selection condition can specify a selection set or .NET type, but cannot specify both.</span></span> <span data-ttu-id="85042-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="85042-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="85042-123">Kijelölés sets csoportjai közös nézeten, amely meghatározza a formázási fájl által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="85042-123">Selection sets are common groups of .NET objects that can be used by any view that the formatting file defines.</span></span> <span data-ttu-id="85042-124">Létrehozásával és a kijelölt csoportok hivatkozó kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="85042-124">For more information about creating and referencing selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

<span data-ttu-id="85042-125">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="85042-125">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="85042-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="85042-126">See Also</span></span>

[<span data-ttu-id="85042-127">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="85042-127">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="85042-128">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="85042-128">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="85042-129">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="85042-129">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="85042-130">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="85042-130">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="85042-131">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="85042-131">TypeName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="85042-132">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="85042-132">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
