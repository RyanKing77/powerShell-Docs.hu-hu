---
title: SelectionCondition elemet a vezérlők (formátum) nézet EntrySelectedBy |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2623407e-fa10-4d27-a804-204f6d50ef22
caps.latest.revision: 6
ms.openlocfilehash: ea15e647a9dd7a7064718a0c536c4a3178d62d95
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064231"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-view-format"></a><span data-ttu-id="e8793-102">A Nézet Vezérlők eleméhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e8793-102">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>

<span data-ttu-id="e8793-103">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="e8793-103">Defines a condition that must exist for the control definition to be used.</span></span> <span data-ttu-id="e8793-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="e8793-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="e8793-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum)</span><span class="sxs-lookup"><span data-stu-id="e8793-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e8793-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e8793-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="e8793-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e8793-107">Attributes and Elements</span></span>

<span data-ttu-id="e8793-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="e8793-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e8793-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e8793-109">Attributes</span></span>

<span data-ttu-id="e8793-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e8793-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e8793-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e8793-111">Child Elements</span></span>

|<span data-ttu-id="e8793-112">Elem</span><span class="sxs-lookup"><span data-stu-id="e8793-112">Element</span></span>|<span data-ttu-id="e8793-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="e8793-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e8793-114">A PropertyName eleme SelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="e8793-114">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="e8793-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="e8793-115">Optional element.</span></span><br /><br /> <span data-ttu-id="e8793-116">Megadja a .NET-tulajdonság, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="e8793-116">Specifies a .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="e8793-117">Nézet (formátum) vezérlők SelectionCondition ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-117">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="e8793-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="e8793-118">Optional element.</span></span><br /><br /> <span data-ttu-id="e8793-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="e8793-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="e8793-120">Nézet (formátum) vezérlők SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-120">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="e8793-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="e8793-121">Optional element.</span></span><br /><br /> <span data-ttu-id="e8793-122">Megadja a .NET-típusok, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="e8793-122">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="e8793-123">Nézet (formátum) vezérlők SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-123">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="e8793-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="e8793-124">Optional element.</span></span><br /><br /> <span data-ttu-id="e8793-125">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e8793-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="e8793-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e8793-126">Parent Elements</span></span>

|<span data-ttu-id="e8793-127">Elem</span><span class="sxs-lookup"><span data-stu-id="e8793-127">Element</span></span>|<span data-ttu-id="e8793-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="e8793-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e8793-129">Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-129">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="e8793-130">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e8793-130">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="e8793-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e8793-131">Remarks</span></span>

<span data-ttu-id="e8793-132">Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="e8793-132">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="e8793-133">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="e8793-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="e8793-134">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="e8793-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="e8793-135">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="e8793-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e8793-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e8793-136">See Also</span></span>

[<span data-ttu-id="e8793-137">A PropertyName eleme SelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="e8793-137">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="e8793-138">Nézet (formátum) vezérlők SelectionCondition ScriptBlock elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-138">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="e8793-139">Nézet (formátum) vezérlők SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-139">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="e8793-140">Nézet (formátum) vezérlők SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-140">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="e8793-141">Nézet (formátum) vezérlők CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="e8793-141">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)

[<span data-ttu-id="e8793-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e8793-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
