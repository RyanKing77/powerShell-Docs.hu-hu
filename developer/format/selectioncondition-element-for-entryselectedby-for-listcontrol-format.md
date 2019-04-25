---
title: ListControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7649d5d0-2b56-49b5-a670-dde46caca343
caps.latest.revision: 11
ms.openlocfilehash: 633204f3b181316761746ea2679910216fb74657
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064101"
---
# <a name="selectioncondition-element-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="ecfa1-102">A ListControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ecfa1-102">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="ecfa1-103">Határozza meg azt a feltételt, amelyet ez a definíció a listanézet használata léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-103">Defines the condition that must exist to use this definition of the list view.</span></span> <span data-ttu-id="ecfa1-104">Kiválasztási feltételek, amelyek egy definíciója adható meg száma nincs korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-104">There is no limit to the number of selection conditions that can be specified for a list definition.</span></span>

<span data-ttu-id="ecfa1-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára EntrySelectedBy a ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="ecfa1-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ecfa1-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ecfa1-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ecfa1-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ecfa1-107">Attributes and Elements</span></span>

<span data-ttu-id="ecfa1-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ecfa1-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ecfa1-109">Attributes</span></span>

<span data-ttu-id="ecfa1-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ecfa1-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ecfa1-111">Child Elements</span></span>

|<span data-ttu-id="ecfa1-112">Elem</span><span class="sxs-lookup"><span data-stu-id="ecfa1-112">Element</span></span>|<span data-ttu-id="ecfa1-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="ecfa1-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ecfa1-114">SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-114">PropertyName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="ecfa1-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-115">Optional element.</span></span><br /><br /> <span data-ttu-id="ecfa1-116">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-116">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="ecfa1-117">SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-117">ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="ecfa1-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-118">Optional element.</span></span><br /><br /> <span data-ttu-id="ecfa1-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="ecfa1-120">A EntrySelectedBy ListEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="ecfa1-120">SelectionSetName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-listentry-format.md)|<span data-ttu-id="ecfa1-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-121">Optional element.</span></span><br /><br /> <span data-ttu-id="ecfa1-122">Megadja azt a feltételt .NET típusú.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-122">Specifies the set of .NET types that trigger the condition.</span></span>|
|[<span data-ttu-id="ecfa1-123">SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-123">TypeName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="ecfa1-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-124">Optional element.</span></span><br /><br /> <span data-ttu-id="ecfa1-125">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="ecfa1-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ecfa1-126">Parent Elements</span></span>

|<span data-ttu-id="ecfa1-127">Elem</span><span class="sxs-lookup"><span data-stu-id="ecfa1-127">Element</span></span>|<span data-ttu-id="ecfa1-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="ecfa1-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ecfa1-129">EntrySelectedBy eleme TableRowEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="ecfa1-129">EntrySelectedBy Element for TableRowEntry (Format)</span></span>](./entryselectedby-element-for-tablerowentry-for-tablecontrol-format.md)|<span data-ttu-id="ecfa1-130">Meghatározza a .NET-típusokat, amelyek a tábla bejegyzés vagy a feltétellel, hogy a bejegyzés használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-130">Defines the .NET types that use this table entry or the condition that must exist for this entry to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="ecfa1-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ecfa1-131">Remarks</span></span>

<span data-ttu-id="ecfa1-132">kiválasztási feltétel definiálása lWhen, az alábbi követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="ecfa1-132">lWhen you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="ecfa1-133">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="ecfa1-134">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="ecfa1-135">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ecfa1-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="ecfa1-136">A listanézet egyéb összetevőivel kapcsolatos további információkért lásd: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="ecfa1-136">For more information about other components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ecfa1-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ecfa1-137">See Also</span></span>

[<span data-ttu-id="ecfa1-138">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="ecfa1-138">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="ecfa1-139">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="ecfa1-139">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="ecfa1-140">ListEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="ecfa1-140">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="ecfa1-141">A ListEntry (formátum) EntrySelectedBy SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-141">SelectionSetName Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="ecfa1-142">EntrySelectedBy ListEntry (formátum) a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="ecfa1-142">TypeName Element for EntrySelectedBy for ListEntry (Format)</span></span>](http://msdn.microsoft.com/en-us/fcd4daa6-f3fd-43f7-a468-03c582d34533)

[<span data-ttu-id="ecfa1-143">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ecfa1-143">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
