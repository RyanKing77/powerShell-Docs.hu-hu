---
title: (Formátum) WideEntry EntrySelectedBy eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e0c98933-b7a5-4205-b811-06c0b0bf8988
caps.latest.revision: 9
ms.openlocfilehash: 54c7c261a23075721cd7bce75e530150dc0e0212
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846094"
---
# <a name="entryselectedby-element-for-wideentry-format"></a><span data-ttu-id="6c52f-102">A WideEntry elem EntrySelectedBy eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="6c52f-102">EntrySelectedBy Element for WideEntry (Format)</span></span>

<span data-ttu-id="6c52f-103">A .NET-típusokat, amelyek a széles nézet vagy a feltételt, amelyet a definíció használandó léteznie kell a definíció határozza meg.</span><span class="sxs-lookup"><span data-stu-id="6c52f-103">Defines the .NET types that use this definition of the wide view or the condition that must exist for this definition to be used.</span></span>

<span data-ttu-id="6c52f-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem a WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="6c52f-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="6c52f-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="6c52f-105">Syntax</span></span>

```xml
<EntrySelectedBy>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <SelectionCondition>...</SelectionCondition>
</EntrySelectedBy>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="6c52f-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="6c52f-106">Attributes and Elements</span></span>

<span data-ttu-id="6c52f-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `EntrySelectedBy` elemet.</span><span class="sxs-lookup"><span data-stu-id="6c52f-107">The following sections describe attributes, child elements, and the parent element of the `EntrySelectedBy` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="6c52f-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="6c52f-108">Attributes</span></span>

<span data-ttu-id="6c52f-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="6c52f-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="6c52f-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="6c52f-110">Child Elements</span></span>

|<span data-ttu-id="6c52f-111">Elem</span><span class="sxs-lookup"><span data-stu-id="6c52f-111">Element</span></span>|<span data-ttu-id="6c52f-112">Leírás</span><span class="sxs-lookup"><span data-stu-id="6c52f-112">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6c52f-113">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="6c52f-113">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="6c52f-114">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="6c52f-114">Optional element.</span></span><br /><br /> <span data-ttu-id="6c52f-115">Határozza meg azt a feltételt, amelyet a széles nézet definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="6c52f-115">Defines the condition that must exist for this wide view definition to be used.</span></span>|
|[<span data-ttu-id="6c52f-116">A WideEntry (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="6c52f-116">SelectionSetName Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="6c52f-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="6c52f-117">Optional element.</span></span><br /><br /> <span data-ttu-id="6c52f-118">.NET-típusokat, amelyek a széles nézet definícióját egy halmazát határozza meg.</span><span class="sxs-lookup"><span data-stu-id="6c52f-118">Specifies a set of .NET types that use this wide view definition.</span></span>|
|[<span data-ttu-id="6c52f-119">EntrySelectedBy WideEntry (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="6c52f-119">TypeName Element for EntrySelectedBy for WideEntry (Format)</span></span>](./typename-element-for-entryselectedby-for-wideentry-format.md)|<span data-ttu-id="6c52f-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="6c52f-120">Optional element.</span></span><br /><br /> <span data-ttu-id="6c52f-121">A széles körű nézetdefiníció használó .NET típust határozzon meg.</span><span class="sxs-lookup"><span data-stu-id="6c52f-121">Specifies a .NET type that uses this wide view definition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="6c52f-122">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="6c52f-122">Parent Elements</span></span>

|<span data-ttu-id="6c52f-123">Elem</span><span class="sxs-lookup"><span data-stu-id="6c52f-123">Element</span></span>|<span data-ttu-id="6c52f-124">Leírás</span><span class="sxs-lookup"><span data-stu-id="6c52f-124">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="6c52f-125">WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6c52f-125">WideEntry Element (Format)</span></span>](./wideentry-element-for-widecontrol-format.md)|<span data-ttu-id="6c52f-126">A széles nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="6c52f-126">Provides a definition of the wide view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="6c52f-127">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="6c52f-127">Remarks</span></span>

<span data-ttu-id="6c52f-128">Meg kell adnia legalább egy típusa, a kijelölés készlet vagy a kiválasztási feltétel széles nézet definícióját.</span><span class="sxs-lookup"><span data-stu-id="6c52f-128">You must specify at least one type, selection set, or selection condition for a wide view definition.</span></span> <span data-ttu-id="6c52f-129">Nincs nem használható gyermekelemek számának maximális korlátot.</span><span class="sxs-lookup"><span data-stu-id="6c52f-129">There is no maximum limit to the number of child elements that you can use.</span></span>

<span data-ttu-id="6c52f-130">Kiválasztási feltételek segítségével határozhatók meg egy feltételt, amely megléte esetén használható, például ha egy objektum rendelkezik-e egy adott tulajdonságra a definíció, vagy egy adott tulajdonság értékét, vagy a parancsfájl érték kiértékelésének eredménye `true`.</span><span class="sxs-lookup"><span data-stu-id="6c52f-130">Selection conditions are used to define a condition that must exist for the definition to be used, such as when an object has a specific property or that a specific property value or script value evaluates to `true`.</span></span> <span data-ttu-id="6c52f-131">További információ a kiválasztási feltételek: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="6c52f-131">For more information about selection conditions, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="6c52f-132">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="6c52f-132">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6c52f-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="6c52f-133">See Also</span></span>

[<span data-ttu-id="6c52f-134">WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="6c52f-134">WideEntry Element (Format)</span></span>](./wideentry-element-for-widecontrol-format.md)

[<span data-ttu-id="6c52f-135">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="6c52f-135">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="6c52f-136">A WideEntry (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="6c52f-136">SelectionSetName Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="6c52f-137">EntrySelectedBy WideEntry (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="6c52f-137">TypeName Element for EntrySelectedBy for WideEntry (Format)</span></span>](./typename-element-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="6c52f-138">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="6c52f-138">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="6c52f-139">Adatok megjelenítése feltételek meghatározása</span><span class="sxs-lookup"><span data-stu-id="6c52f-139">Defining Conditions for Displaying Data</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="6c52f-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="6c52f-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
