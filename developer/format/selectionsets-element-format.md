---
title: SelectionSets elem (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ebbac73a-1c99-4388-9f47-703cd024dc6d
caps.latest.revision: 18
ms.openlocfilehash: a9356635d60d5f8c5d4dec4ec8b7d0aea2b037dd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063775"
---
# <a name="selectionsets-element-format"></a><span data-ttu-id="d3cb5-102">SelectionSets elem (Formátum)</span><span class="sxs-lookup"><span data-stu-id="d3cb5-102">SelectionSets Element (Format)</span></span>

<span data-ttu-id="d3cb5-103">Határozza meg a gyakori eljárások egyikét a formázási fájl összes nézetek által használható .NET-objektumokat.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-103">Defines the common sets of .NET objects that can be used by all views of the formatting file.</span></span> <span data-ttu-id="d3cb5-104">A nézetek és a formázási fájl vezérlők csak a kijelölt csoport nevét az objektumok teljes készletének hivatkozhat.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-104">The views and controls of the formatting file can reference the complete set of objects by using only the name of the selection set.</span></span>

<span data-ttu-id="d3cb5-105">Konfigurációs elem SelectionSets elem formátuma</span><span class="sxs-lookup"><span data-stu-id="d3cb5-105">Configuration Element SelectionSets Element Format</span></span>

## <a name="syntax"></a><span data-ttu-id="d3cb5-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d3cb5-106">Syntax</span></span>

```xml
<SelectionSets>
  <SelectionSet>...</SelectionSet>
</SelectionSets>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="d3cb5-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="d3cb5-107">Attributes and Elements</span></span>

<span data-ttu-id="d3cb5-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `SelectionSets` elemet.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-108">The following sections describe the attributes, child elements, and parent element of the `SelectionSets` element.</span></span> <span data-ttu-id="d3cb5-109">Minden egyes gyermekelemet határozza meg azon objektumok, amely a készlet neve szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-109">Each child element defines a set of objects that can be referenced by the name of the set.</span></span> <span data-ttu-id="d3cb5-110">Az alárendelt összetevők sorrendje nem lényeges.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-110">The order of the child elements is not significant.</span></span>

### <a name="attributes"></a><span data-ttu-id="d3cb5-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d3cb5-111">Attributes</span></span>

<span data-ttu-id="d3cb5-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d3cb5-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="d3cb5-113">Child Elements</span></span>

|<span data-ttu-id="d3cb5-114">Elem</span><span class="sxs-lookup"><span data-stu-id="d3cb5-114">Element</span></span>|<span data-ttu-id="d3cb5-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="d3cb5-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d3cb5-116">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d3cb5-116">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)|<span data-ttu-id="d3cb5-117">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-117">Required element.</span></span><br /><br /> <span data-ttu-id="d3cb5-118">Meghatároz egy egységes .NET-objektumokat a készlet neve szerint lehet hivatkozni.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-118">Defines a single set of .NET objects that can be referenced by the name of the set.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="d3cb5-119">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="d3cb5-119">Parent Elements</span></span>

|<span data-ttu-id="d3cb5-120">Elem</span><span class="sxs-lookup"><span data-stu-id="d3cb5-120">Element</span></span>|<span data-ttu-id="d3cb5-121">Leírás</span><span class="sxs-lookup"><span data-stu-id="d3cb5-121">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d3cb5-122">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="d3cb5-122">Configuration Element</span></span>](./configuration-element-format.md)|<span data-ttu-id="d3cb5-123">A legfelső szintű elem egy formázási fájl jelöli.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-123">Represents the top-level element of a formatting file.</span></span>|

## <a name="remarks"></a><span data-ttu-id="d3cb5-124">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d3cb5-124">Remarks</span></span>

<span data-ttu-id="d3cb5-125">Kijelölt csoportok is használhatja, ha egyetlen nevet, például az öröklődés kapcsolódó objektumok közül a hivatkozni kívánt kapcsolódó objektumok közül.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-125">You can use selection sets when you have a set of related objects that you want to reference by using a single name, such as a set of objects that are related through inheritance.</span></span> <span data-ttu-id="d3cb5-126">A nézetek meghatározásakor a neve helyett az egyes nézetek összes objektumához ajánlati beállítása a kijelölt objektumok készlete is megadhat.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-126">When defining your views, you can specify the set of objects by using the name of the selection set instead of listing all the objects within each view.</span></span>

<span data-ttu-id="d3cb5-127">Közös kijelölt csoportok neve szerint vannak megadva, a nézetek a formázási fájl vagy a definíciók nézetek meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-127">Common selection sets are specified by their name when defining the views of the formatting file or the definitions of the views.</span></span> <span data-ttu-id="d3cb5-128">Ezekben az esetekben a `SelectionSetName` gyermekeleme a `ViewSelectedBy` és `EntrySelectedBy` elemek szolgáló megadja.</span><span class="sxs-lookup"><span data-stu-id="d3cb5-128">In these cases, the `SelectionSetName` child element of the `ViewSelectedBy` and `EntrySelectedBy` elements specifies the set to be used.</span></span> <span data-ttu-id="d3cb5-129">Kijelölt csoportok kapcsolatos további információkért lásd: [meghatározása beállítja az objektumok](./defining-selection-sets.md).</span><span class="sxs-lookup"><span data-stu-id="d3cb5-129">For more information about selection sets, see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="d3cb5-130">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d3cb5-130">See Also</span></span>

[<span data-ttu-id="d3cb5-131">Konfigurációs elem</span><span class="sxs-lookup"><span data-stu-id="d3cb5-131">Configuration Element</span></span>](./configuration-element-format.md)

[<span data-ttu-id="d3cb5-132">Kijelölt csoportok meghatározása</span><span class="sxs-lookup"><span data-stu-id="d3cb5-132">Defining Selection Sets</span></span>](./defining-selection-sets.md)

[<span data-ttu-id="d3cb5-133">SelectionSet elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="d3cb5-133">SelectionSet Element (Format)</span></span>](./selectionset-element-format.md)

[<span data-ttu-id="d3cb5-134">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="d3cb5-134">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
