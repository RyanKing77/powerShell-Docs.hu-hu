---
title: WideControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b7a9f086-b1ca-4400-9be7-9ec1ec8880f3
caps.latest.revision: 11
ms.openlocfilehash: f20679e3392b99a049c075f24c7712262bab08e1
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62063991"
---
# <a name="selectioncondition-element-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="ab6ce-102">A WideControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ab6ce-102">SelectionCondition Element for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="ab6ce-103">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-103">Defines the condition that must exist for this definition to be used.</span></span> <span data-ttu-id="ab6ce-104">Kiválasztási feltételek széles bejegyzés-definíció adható meg száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-104">There is no limit to the number of selection conditions that can be specified for a wide entry definition.</span></span>

<span data-ttu-id="ab6ce-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára EntrySelectedBy a WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="ab6ce-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ab6ce-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ab6ce-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ab6ce-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ab6ce-107">Attributes and Elements</span></span>

<span data-ttu-id="ab6ce-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span> <span data-ttu-id="ab6ce-109">Meg kell adnia egy `PropertyName` vagy `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-109">You must specify a single `PropertyName` or `ScriptBlock` element.</span></span> <span data-ttu-id="ab6ce-110">A `SelectionSetName` és `TypeName` elemek egyike sem kötelező.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-110">The `SelectionSetName` and `TypeName` elements are optional.</span></span> <span data-ttu-id="ab6ce-111">Mindkét elem kiválaszthat egyet.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-111">You can specify one of either element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ab6ce-112">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ab6ce-112">Attributes</span></span>

<span data-ttu-id="ab6ce-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-113">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ab6ce-114">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ab6ce-114">Child Elements</span></span>

|<span data-ttu-id="ab6ce-115">Elem</span><span class="sxs-lookup"><span data-stu-id="ab6ce-115">Element</span></span>|<span data-ttu-id="ab6ce-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="ab6ce-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ab6ce-117">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-117">PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)|<span data-ttu-id="ab6ce-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-118">Optional element.</span></span><br /><br /> <span data-ttu-id="ab6ce-119">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-119">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="ab6ce-120">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-120">ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="ab6ce-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-121">Optional element.</span></span><br /><br /> <span data-ttu-id="ab6ce-122">Adja meg a parancsprogram-blokkot, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-122">Specifies the script block that triggers the condition.</span></span>|
|[<span data-ttu-id="ab6ce-123">A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="ab6ce-123">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)|<span data-ttu-id="ab6ce-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-124">Optional element.</span></span><br /><br /> <span data-ttu-id="ab6ce-125">Megadja a .NET-típusok, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-125">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="ab6ce-126">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-126">TypeName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="ab6ce-127">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-127">Optional element.</span></span><br /><br /> <span data-ttu-id="ab6ce-128">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-128">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="ab6ce-129">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ab6ce-129">Parent Elements</span></span>

|<span data-ttu-id="ab6ce-130">Elem</span><span class="sxs-lookup"><span data-stu-id="ab6ce-130">Element</span></span>|<span data-ttu-id="ab6ce-131">Leírás</span><span class="sxs-lookup"><span data-stu-id="ab6ce-131">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ab6ce-132">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="ab6ce-132">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)|<span data-ttu-id="ab6ce-133">A .NET-típusokat, amelyek a széles körű bejegyzés vagy a feltétellel, hogy léteznie kell használni a bejegyzés határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-133">Defines the .NET types that use this wide entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="ab6ce-134">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ab6ce-134">Remarks</span></span>

<span data-ttu-id="ab6ce-135">Minden széles bejegyzés rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-135">Each wide entry must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="ab6ce-136">Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="ab6ce-136">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="ab6ce-137">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-137">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="ab6ce-138">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-138">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="ab6ce-139">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ce-139">For more information about how to use selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="ab6ce-140">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="ab6ce-140">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ab6ce-141">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ab6ce-141">See Also</span></span>

[<span data-ttu-id="ab6ce-142">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="ab6ce-142">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="ab6ce-143">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="ab6ce-143">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="ab6ce-144">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="ab6ce-144">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)

[<span data-ttu-id="ab6ce-145">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-145">PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="ab6ce-146">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-146">ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="ab6ce-147">A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="ab6ce-147">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="ab6ce-148">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="ab6ce-148">TypeName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="ab6ce-149">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ab6ce-149">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
