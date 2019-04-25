---
title: ListControl (formátum) a EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cff7763c-5ce0-49c1-a480-1249c9f57a13
caps.latest.revision: 11
ms.openlocfilehash: 7fd431b4b1ddecd3a7358c2bf97f299b97162b34
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62075562"
---
# <a name="selectionsetname-element-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="548a3-102">A ListControl elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="548a3-102">SelectionSetName Element for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="548a3-103">Regisztrációslista-bejegyzés a .NET-objektumokat egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="548a3-103">Specifies a set of .NET objects for the list entry.</span></span> <span data-ttu-id="548a3-104">Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="548a3-104">There is no limit to the number of selection sets that can be specified for an entry.</span></span>

<span data-ttu-id="548a3-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionSetName elem számára EntrySelectedBy a ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="548a3-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionSetName Element for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="548a3-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="548a3-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="548a3-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="548a3-107">Attributes and Elements</span></span>

<span data-ttu-id="548a3-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="548a3-108">The following sections describe attributes, child elements, and parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="548a3-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="548a3-109">Attributes</span></span>

<span data-ttu-id="548a3-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="548a3-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="548a3-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="548a3-111">Child Elements</span></span>

<span data-ttu-id="548a3-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="548a3-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="548a3-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="548a3-113">Parent Elements</span></span>

|<span data-ttu-id="548a3-114">Elem</span><span class="sxs-lookup"><span data-stu-id="548a3-114">Element</span></span>|<span data-ttu-id="548a3-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="548a3-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="548a3-116">EntrySelectedBy eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="548a3-116">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)|<span data-ttu-id="548a3-117">A .NET-típusokat, amelyek a regisztrációslista-bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="548a3-117">Defines the .NET types that use this list entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="548a3-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="548a3-118">Text Value</span></span>

<span data-ttu-id="548a3-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="548a3-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="548a3-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="548a3-120">Remarks</span></span>

<span data-ttu-id="548a3-121">Minden egyes regisztrációslista-bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="548a3-121">Each list entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="548a3-122">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="548a3-122">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="548a3-123">Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="548a3-123">For example, you might want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="548a3-124">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok megjelenítéséhez](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="548a3-124">For more information about defining selection sets, see [Defining Sets of objects for a View](./defining-selection-sets.md).</span></span>

<span data-ttu-id="548a3-125">Megjelenítheti az összetevőivel kapcsolatos további információk: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="548a3-125">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="548a3-126">Példa</span><span class="sxs-lookup"><span data-stu-id="548a3-126">Example</span></span>

<span data-ttu-id="548a3-127">Az alábbi példa bemutatja, hogyan adjon meg egy kiválasztása a lista nézet bejegyzés.</span><span class="sxs-lookup"><span data-stu-id="548a3-127">The following example shows how to specify a selection set for an entry of a list view.</span></span>

```xml
<ListEntry>
  <EntrySelectedBy>
    <SelectionSetName>NameofSelectionSet</SelectionSetName>
  </EntrySelectedBy>
  <ListItems>...</ListItems>
</ListEntry>
```

## <a name="see-also"></a><span data-ttu-id="548a3-128">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="548a3-128">See Also</span></span>

[<span data-ttu-id="548a3-129">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="548a3-129">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="548a3-130">EntrySelectedBy eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="548a3-130">EntrySelectedBy Element for ListEntry (Format)</span></span>](./entryselectedby-element-for-listentry-for-listcontrol-format.md)

[<span data-ttu-id="548a3-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="548a3-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
