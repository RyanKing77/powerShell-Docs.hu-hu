---
title: EnumerableExpansion (formátum) a EntrySelectedBy SelectionSetName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 936d09f2-2c48-49e8-ab2d-0c8729199a2e
caps.latest.revision: 8
ms.openlocfilehash: 8ba8931ea5e34f610878351396cad42023393ad6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076259"
---
# <a name="selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="b34d5-102">Az EnumerableExpansion elemhez tartozó EntrySelectedBy SelectionSetName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="b34d5-102">SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="b34d5-103">Megadja, hogy ez a definíció szerint bontva .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="b34d5-103">Specifies the set of .NET types that are expanded by this definition.</span></span>

<span data-ttu-id="b34d5-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionSetName elemhez EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="b34d5-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="b34d5-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="b34d5-105">Syntax</span></span>

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="b34d5-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="b34d5-106">Attributes and Elements</span></span>

<span data-ttu-id="b34d5-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionSetName` elemet.</span><span class="sxs-lookup"><span data-stu-id="b34d5-107">The following sections describe attributes, child elements, and the parent element of the `SelectionSetName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="b34d5-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="b34d5-108">Attributes</span></span>

<span data-ttu-id="b34d5-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b34d5-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="b34d5-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="b34d5-110">Child Elements</span></span>

<span data-ttu-id="b34d5-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="b34d5-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="b34d5-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="b34d5-112">Parent Elements</span></span>

|<span data-ttu-id="b34d5-113">Elem</span><span class="sxs-lookup"><span data-stu-id="b34d5-113">Element</span></span>|<span data-ttu-id="b34d5-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="b34d5-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="b34d5-115">EntrySelectedBy eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="b34d5-115">EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>](./entryselectedby-element-for-enumerableexpansion-format.md)|<span data-ttu-id="b34d5-116">Meghatározza a .NET-gyűjtemény objektumok, amelyek a definíció szerint bontva.</span><span class="sxs-lookup"><span data-stu-id="b34d5-116">Defines the .NET collection objects that are expanded by this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="b34d5-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="b34d5-117">Text Value</span></span>

<span data-ttu-id="b34d5-118">Adja meg a kijelölt csoport nevét.</span><span class="sxs-lookup"><span data-stu-id="b34d5-118">Specify the name of the selection set.</span></span>

## <a name="remarks"></a><span data-ttu-id="b34d5-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="b34d5-119">Remarks</span></span>

<span data-ttu-id="b34d5-120">Minden egyes definíciójában meg kell adni, egy vagy több típus nevét, egy kijelölt készlet vagy kiválasztási feltétel.</span><span class="sxs-lookup"><span data-stu-id="b34d5-120">Each definition must specify one or more type names, a selection set, or a selection condition.</span></span>

<span data-ttu-id="b34d5-121">Kijelölt csoportok általában akkor használják, ha meg szeretné több nézetében lévő meghatározott felhasználói csoporttal használt objektumok.</span><span class="sxs-lookup"><span data-stu-id="b34d5-121">Selection sets are typically used when you want to define a group of objects that are used in multiple views.</span></span> <span data-ttu-id="b34d5-122">Például előfordulhat, hogy szeretne létrehozni a táblázatos nézetre, és megjelenítheti a ugyanazt az objektumhalmazt tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="b34d5-122">For example, you might want to create a table view and a list view for the same set of objects.</span></span> <span data-ttu-id="b34d5-123">Kijelölt csoportok meghatározása kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok megjelenítéséhez](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="b34d5-123">For more information about defining selection sets, see [Defining Sets of Objects for a View](./defining-selection-sets.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b34d5-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="b34d5-124">See Also</span></span>

[<span data-ttu-id="b34d5-125">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="b34d5-125">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="b34d5-126">EntrySelectedBy eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="b34d5-126">EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>](./entryselectedby-element-for-enumerableexpansion-format.md)

[<span data-ttu-id="b34d5-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="b34d5-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
