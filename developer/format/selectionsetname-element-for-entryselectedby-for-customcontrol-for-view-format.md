---
title: A nézet (formátum) CustomControl EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 859d2335-7fcd-4efd-b1cc-3d171e334c6b
caps.latest.revision: 7
ms.openlocfilehash: f4bf820be88919af43eeaf043b3ed8b9c06e1bf2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846129"
---
# <a name="selectionsetname-element-for-entryselectedby-for-customcontrol-for-view-format"></a><span data-ttu-id="0290f-102">A Nézet CustomControl eleméhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0290f-102">SelectionSetName Element for EntrySelectedBy for CustomControl for View (Format)</span></span>

<span data-ttu-id="0290f-103">Regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0290f-103">Specifies a set of .NET objects for the list entry.</span></span> <span data-ttu-id="0290f-104">Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="0290f-104">There is no limit to the number of selection sets that can be specified for an entry.</span></span>

<span data-ttu-id="0290f-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl számára a nézet (formátum) EntrySelectedBy CustomEntries megtekintése (formátum) CustomEntry elemhez Megtekintése (formátum) SelectionSetName elemhez tartozó EntrySelectedBy CustomEntry (formátum) a CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="0290f-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) EntrySelectedBy Element for CustomEntry for View (Format) SelectionSetName Element for EntrySelectedBy for CustomEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0290f-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0290f-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0290f-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0290f-107">Attributes and Elements</span></span>

<span data-ttu-id="0290f-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="0290f-108">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0290f-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0290f-109">Attributes</span></span>

<span data-ttu-id="0290f-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0290f-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0290f-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0290f-111">Child Elements</span></span>

<span data-ttu-id="0290f-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0290f-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0290f-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0290f-113">Parent Elements</span></span>

|<span data-ttu-id="0290f-114">Elem</span><span class="sxs-lookup"><span data-stu-id="0290f-114">Element</span></span>|<span data-ttu-id="0290f-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="0290f-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0290f-116">A nézet (formátum) CustomEntry EntrySelectedBy elem</span><span class="sxs-lookup"><span data-stu-id="0290f-116">EntrySelectedBy Element for CustomEntry for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="0290f-117">A .NET-típusokat, amelyek egyéni tételhez vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0290f-117">Defines the .NET types that use this custom entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0290f-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="0290f-118">Text Value</span></span>

<span data-ttu-id="0290f-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="0290f-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="0290f-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0290f-120">Remarks</span></span>

<span data-ttu-id="0290f-121">Minden egyes egyéni vezérlőt bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="0290f-121">Each custom control entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="0290f-122">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="0290f-122">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="0290f-123">Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="0290f-123">For example, you might want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="0290f-124">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja a kijelölés](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="0290f-124">For more information about defining selection sets, see [Defining Selection Sets](./defining-selection-sets.md).</span></span>

<span data-ttu-id="0290f-125">Egyéni vezérlő nézet az összetevőivel kapcsolatos további információkért lásd: [egyéni vezérlők létrehozását](./creating-custom-controls.md).</span><span class="sxs-lookup"><span data-stu-id="0290f-125">For more information about the components of a custom control view, see [Creating Custom Controls](./creating-custom-controls.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0290f-126">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0290f-126">See Also</span></span>

[<span data-ttu-id="0290f-127">A nézet (formátum) CustomEntry EntrySelectedBy elem</span><span class="sxs-lookup"><span data-stu-id="0290f-127">EntrySelectedBy Element for CustomEntry for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="0290f-128">Egyéni vezérlő nézetében.</span><span class="sxs-lookup"><span data-stu-id="0290f-128">Custom Control View</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="0290f-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0290f-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
