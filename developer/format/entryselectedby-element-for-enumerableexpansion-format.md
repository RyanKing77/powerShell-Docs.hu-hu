---
title: (Formátum) EnumerableExpansion EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3af6aff8-4c2d-4f08-9bb1-e1f3ed3e583e
caps.latest.revision: 11
ms.openlocfilehash: 6a371bdbb85d07730c32931a4a79ee40856ce298
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846521"
---
# <a name="entryselectedby-element-for-enumerableexpansion-format"></a><span data-ttu-id="32ca8-102">Az EnumerableExpansion EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="32ca8-102">EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="32ca8-103">A .NET-típusokat, amelyek a definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="32ca8-103">Defines the .NET types that use this definition or the condition that must exist for this definition to be used.</span></span>

<span data-ttu-id="32ca8-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="32ca8-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="32ca8-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="32ca8-105">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="32ca8-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="32ca8-106">Attributes and Elements</span></span>

<span data-ttu-id="32ca8-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="32ca8-107">The following sections describe attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="32ca8-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="32ca8-108">Attributes</span></span>

<span data-ttu-id="32ca8-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="32ca8-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="32ca8-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="32ca8-110">Child Elements</span></span>

|<span data-ttu-id="32ca8-111">Elem</span><span class="sxs-lookup"><span data-stu-id="32ca8-111">Element</span></span>|<span data-ttu-id="32ca8-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="32ca8-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="32ca8-113">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="32ca8-113">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="32ca8-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="32ca8-114">Optional element.</span></span><br /><br /> <span data-ttu-id="32ca8-115">Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="32ca8-115">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|
|[<span data-ttu-id="32ca8-116">A EnumerableExpansion (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="32ca8-116">SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="32ca8-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="32ca8-117">Optional element.</span></span><br /><br /> <span data-ttu-id="32ca8-118">Ez a definíció, hogyan vannak bontva a gyűjtemény objektumokat használó .NET-típusok egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="32ca8-118">Specifies a set of .NET types that use this definition of how collection objects are expanded.</span></span>|
|[<span data-ttu-id="32ca8-119">EntrySelectedBy EnumerableExpansion (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="32ca8-119">TypeName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="32ca8-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="32ca8-120">Optional element.</span></span><br /><br /> <span data-ttu-id="32ca8-121">Ez a definíció, hogyan vannak bontva a gyűjtemény objektumokat használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="32ca8-121">Specifies a .NET type that uses this definition of how collection objects are expanded.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="32ca8-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="32ca8-122">Parent Elements</span></span>

|<span data-ttu-id="32ca8-123">Elem</span><span class="sxs-lookup"><span data-stu-id="32ca8-123">Element</span></span>|<span data-ttu-id="32ca8-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="32ca8-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="32ca8-125">EnumerableExpansion elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="32ca8-125">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)|<span data-ttu-id="32ca8-126">Határozza meg, hogyan adott .NET gyűjtemény objektumok kibontott nézetben megjelenésekor.</span><span class="sxs-lookup"><span data-stu-id="32ca8-126">Defines how specific .NET collection objects are expanded when they are displayed in a view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="32ca8-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="32ca8-127">Remarks</span></span>

<span data-ttu-id="32ca8-128">Meg kell adnia legalább egy típusa, kijelölés set vagy a definíció bejegyzést kiválasztási feltétel.</span><span class="sxs-lookup"><span data-stu-id="32ca8-128">You must specify at least one type, selection set, or selection condition for a definition entry.</span></span> <span data-ttu-id="32ca8-129">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="32ca8-129">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="32ca8-130">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl kiértékelése `true`.</span><span class="sxs-lookup"><span data-stu-id="32ca8-130">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or that a specific property value or script evaluates to `true`.</span></span> <span data-ttu-id="32ca8-131">További információ a kiválasztási feltételek: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="32ca8-131">For more information about selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="32ca8-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="32ca8-132">See Also</span></span>

[<span data-ttu-id="32ca8-133">Adatok megjelenítése feltételek meghatározása</span><span class="sxs-lookup"><span data-stu-id="32ca8-133">Defining Conditions for Displaying Data</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="32ca8-134">EnumerableExpansion elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="32ca8-134">EnumerableExpansion Element (Format)</span></span>](./enumerableexpansion-element-format.md)

[<span data-ttu-id="32ca8-135">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="32ca8-135">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="32ca8-136">A EnumerableExpansion (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="32ca8-136">SelectionSetName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="32ca8-137">EntrySelectedBy EnumerableExpansion (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="32ca8-137">TypeName Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./typename-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="32ca8-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="32ca8-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
