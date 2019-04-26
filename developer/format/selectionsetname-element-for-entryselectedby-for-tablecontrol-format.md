---
title: TableControl (formátum) a EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5dd0bd5d-f206-4cc6-a0f8-70700ee2c4b7
caps.latest.revision: 8
ms.openlocfilehash: 819906127e81355c45103ede85ef3608e1c1cfeb
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063921"
---
# <a name="selectionsetname-element-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="0eb2b-102">A TableControl elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0eb2b-102">SelectionSetName Element for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="0eb2b-103">Megadja a .NET készletét típusok használatát a bejegyzés a táblázat nézet.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-103">Specifies a set of .NET types the use this entry of the table view.</span></span> <span data-ttu-id="0eb2b-104">Nincs kijelölt csoportok bejegyzés adható meg száma nincs korlátozva.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-104">There is no limit to the number of selection sets that can be specified for an entry.</span></span>

<span data-ttu-id="0eb2b-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem (formátum) SelectionSetName elem számára EntrySelectedBy a TableRowEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="0eb2b-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element (Format) SelectionSetName Element for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0eb2b-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0eb2b-106">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0eb2b-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0eb2b-107">Attributes and Elements</span></span>

<span data-ttu-id="0eb2b-108">A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemeket.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-108">The following sections describe attributes, child elements, and parent elements.</span></span>

### <a name="attributes"></a><span data-ttu-id="0eb2b-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0eb2b-109">Attributes</span></span>

<span data-ttu-id="0eb2b-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0eb2b-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0eb2b-111">Child Elements</span></span>

<span data-ttu-id="0eb2b-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0eb2b-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0eb2b-113">Parent Elements</span></span>

|<span data-ttu-id="0eb2b-114">Elem</span><span class="sxs-lookup"><span data-stu-id="0eb2b-114">Element</span></span>|<span data-ttu-id="0eb2b-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="0eb2b-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0eb2b-116">EntrySelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0eb2b-116">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="0eb2b-117">A .NET-típusokat, amelyek ezt a bejegyzést, vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-117">Defines the .NET types that use this entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0eb2b-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="0eb2b-118">Text Value</span></span>

<span data-ttu-id="0eb2b-119">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-119">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="0eb2b-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0eb2b-120">Remarks</span></span>

<span data-ttu-id="0eb2b-121">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-121">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="0eb2b-122">Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-122">For example, you might want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="0eb2b-123">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok megjelenítéséhez](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="0eb2b-123">For more information about defining selection sets, see [Defining Sets of objects for a View](./defining-selection-sets.md).</span></span>

<span data-ttu-id="0eb2b-124">Ha megad egy kiválasztása a bejegyzés, típusnév nem adható meg.</span><span class="sxs-lookup"><span data-stu-id="0eb2b-124">If you specify a selection set for an entry, you cannot specify a type name.</span></span> <span data-ttu-id="0eb2b-125">Typ .NET meghatározásával kapcsolatos további információkért lásd: [EntrySelectedBy TableRowEntry (formátum) a TypeName eleme](./typename-element-for-entryselectedby-for-tablecontrol-format.md).</span><span class="sxs-lookup"><span data-stu-id="0eb2b-125">For more information about how to specify a .NET type, see [TypeName Element for EntrySelectedBy for TableRowEntry (Format)](./typename-element-for-entryselectedby-for-tablecontrol-format.md).</span></span>

<span data-ttu-id="0eb2b-126">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="0eb2b-126">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0eb2b-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0eb2b-127">See Also</span></span>

[<span data-ttu-id="0eb2b-128">EntrySelectedBy elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="0eb2b-128">EntrySelectedBy Element (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)

[<span data-ttu-id="0eb2b-129">A nézet csoportjaira meghatározása</span><span class="sxs-lookup"><span data-stu-id="0eb2b-129">Defining Sets of objects for a View</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="0eb2b-130">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="0eb2b-130">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="0eb2b-131">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0eb2b-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
