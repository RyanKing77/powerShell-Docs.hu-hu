---
title: A GroupBy (formátum) EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6dc2093a-dc54-42c4-ada3-c8d089ba1e8e
caps.latest.revision: 6
ms.openlocfilehash: a6738a7c4c934b2d6a16695a711f7c6c80afdd2d
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846227"
---
# <a name="selectioncondition-element-for-entryselectedby-for-groupby-format"></a><span data-ttu-id="0754a-102">A GroupBy elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0754a-102">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>

<span data-ttu-id="0754a-103">Határozza meg egy feltételt, amely használható vezérlő definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="0754a-103">Defines a condition that must exist for a control definition to be used.</span></span> <span data-ttu-id="0754a-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="0754a-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="0754a-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy GroupBy (formátum) esetében a GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="0754a-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0754a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0754a-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0754a-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0754a-107">Attributes and Elements</span></span>

<span data-ttu-id="0754a-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="0754a-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0754a-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0754a-109">Attributes</span></span>

<span data-ttu-id="0754a-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0754a-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0754a-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0754a-111">Child Elements</span></span>

|<span data-ttu-id="0754a-112">Elem</span><span class="sxs-lookup"><span data-stu-id="0754a-112">Element</span></span>|<span data-ttu-id="0754a-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="0754a-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0754a-114">A GroupBy (formátum) SelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-114">PropertyName Element for SelectionCondition for GroupBy (Format)</span></span>](./propertyname-element-for-selectioncondition-for-groupby-format.md)|<span data-ttu-id="0754a-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0754a-115">Optional element.</span></span><br /><br /> <span data-ttu-id="0754a-116">Megadja a .NET-tulajdonság, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="0754a-116">Specifies a .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="0754a-117">SelectionCondition GroupBy (formátum) a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-117">ScriptBlock Element for SelectionCondition for GroupBy (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="0754a-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0754a-118">Optional element.</span></span><br /><br /> <span data-ttu-id="0754a-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="0754a-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="0754a-120">A GroupBy (formátum) SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-120">SelectionSetName Element for SelectionCondition for GroupBy (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-groupby-format.md)|<span data-ttu-id="0754a-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0754a-121">Optional element.</span></span><br /><br /> <span data-ttu-id="0754a-122">Megadja a .NET-típusok, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="0754a-122">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="0754a-123">A GroupBy (formátum) SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-123">TypeName Element for SelectionCondition for GroupBy  (Format)</span></span>](./typename-element-for-selectioncondition-for-groupby-format.md)|<span data-ttu-id="0754a-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0754a-124">Optional element.</span></span><br /><br /> <span data-ttu-id="0754a-125">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0754a-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0754a-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0754a-126">Parent Elements</span></span>

|<span data-ttu-id="0754a-127">Elem</span><span class="sxs-lookup"><span data-stu-id="0754a-127">Element</span></span>|<span data-ttu-id="0754a-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="0754a-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0754a-129">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-129">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="0754a-130">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="0754a-130">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0754a-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0754a-131">Remarks</span></span>

<span data-ttu-id="0754a-132">Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="0754a-132">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="0754a-133">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="0754a-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="0754a-134">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="0754a-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="0754a-135">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="0754a-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0754a-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0754a-136">See Also</span></span>

[<span data-ttu-id="0754a-137">A nézet (formátum) CustomControl SelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-137">PropertyName Element for SelectionCondition for CustomControl for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="0754a-138">A nézet (formátum) CustomControl SelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="0754a-138">ScriptBlock Element for SelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="0754a-139">Egyéni vezérlő nézet (formátum) SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-139">SelectionSetName Element for SelectionCondition for Custom Control for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="0754a-140">A GroupBy (formátum) SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-140">TypeName Element for SelectionCondition for GroupBy  (Format)</span></span>](./typename-element-for-selectioncondition-for-groupby-format.md)

[<span data-ttu-id="0754a-141">A GroupBy (formátum) CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="0754a-141">EntrySelectedBy Element for CustomEntry for GroupBy (Format)</span></span>](./entryselectedby-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="0754a-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0754a-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
