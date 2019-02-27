---
title: CustomControl (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 231e9c6d-09ec-4e68-80ee-0c8f7fe1b9f5
caps.latest.revision: 7
ms.openlocfilehash: 49e2c0cf09dfa55b535effcd431e980daf12fac3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848789"
---
# <a name="selectioncondition-element-for-entryselectedby-for-customcontrol-format"></a><span data-ttu-id="79687-102">A CustomControl elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="79687-102">SelectionCondition Element for EntrySelectedBy for CustomControl (Format)</span></span>

<span data-ttu-id="79687-103">Határozza meg egy feltételt, amely használható vezérlő definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="79687-103">Defines a condition that must exist for a control definition to be used.</span></span> <span data-ttu-id="79687-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="79687-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="79687-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem a CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries CustomControl a nézet (a nézetben (formátum) CustomEntries elemhez CustomEntry CustomControl CustomControl EntrySelectedBy CustomControl nézet (formátum) esetében a nézet (formátum) SelectionCondition elemhez tartozó CustomEntry a nézet (formátum) EntrySelectedBy elemhez tartozó CustomItem eleme formátumban)</span><span class="sxs-lookup"><span data-stu-id="79687-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for CustomControl for View (Format) CustomItem Element for CustomEntry for CustomControl for View (Format) EntrySelectedBy Element for CustomEntry for CustomControl for View (Format) SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="79687-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="79687-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="79687-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="79687-107">Attributes and Elements</span></span>

<span data-ttu-id="79687-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="79687-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="79687-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="79687-109">Attributes</span></span>

<span data-ttu-id="79687-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="79687-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="79687-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="79687-111">Child Elements</span></span>

|<span data-ttu-id="79687-112">Elem</span><span class="sxs-lookup"><span data-stu-id="79687-112">Element</span></span>|<span data-ttu-id="79687-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="79687-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="79687-114">A nézet (formátum) CustomControl SelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="79687-114">PropertyName Element for SelectionCondition for CustomControl for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="79687-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="79687-115">Optional element.</span></span><br /><br /> <span data-ttu-id="79687-116">Megadja a .NET-tulajdonság, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="79687-116">Specifies a .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="79687-117">A nézet (formátum) CustomControl SelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="79687-117">ScriptBlock Element for SelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="79687-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="79687-118">Optional element.</span></span><br /><br /> <span data-ttu-id="79687-119">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="79687-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="79687-120">Egyéni vezérlő nézet (formátum) SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="79687-120">SelectionSetName Element for SelectionCondition for Custom Control for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="79687-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="79687-121">Optional element.</span></span><br /><br /> <span data-ttu-id="79687-122">Megadja a .NET-típusok, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="79687-122">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="79687-123">A nézet (formátum) CustomControl SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="79687-123">TypeName Element for SelectionCondition for CustomControl for View  (Format)</span></span>](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)|<span data-ttu-id="79687-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="79687-124">Optional element.</span></span><br /><br /> <span data-ttu-id="79687-125">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="79687-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="79687-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="79687-126">Parent Elements</span></span>

|<span data-ttu-id="79687-127">Elem</span><span class="sxs-lookup"><span data-stu-id="79687-127">Element</span></span>|<span data-ttu-id="79687-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="79687-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="79687-129">A nézet (formátum) CustomControl CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="79687-129">EntrySelectedBy Element for CustomEntry for CustomControl for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="79687-130">A .NET-típusokat, amelyek a vezérlő definition vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="79687-130">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="79687-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="79687-131">Remarks</span></span>

<span data-ttu-id="79687-132">Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="79687-132">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="79687-133">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="79687-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="79687-134">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="79687-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="79687-135">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="79687-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="79687-136">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="79687-136">See Also</span></span>

[<span data-ttu-id="79687-137">A nézet (formátum) CustomControl SelectionCondition PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="79687-137">PropertyName Element for SelectionCondition for CustomControl for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="79687-138">A nézet (formátum) CustomControl SelectionCondition ScriptBlock eleme</span><span class="sxs-lookup"><span data-stu-id="79687-138">ScriptBlock Element for SelectionCondition for CustomControl for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="79687-139">Egyéni vezérlő nézet (formátum) SelectionCondition SelectionSetName elem.</span><span class="sxs-lookup"><span data-stu-id="79687-139">SelectionSetName Element for SelectionCondition for Custom Control for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="79687-140">A nézet (formátum) CustomControl SelectionCondition TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="79687-140">TypeName Element for SelectionCondition for CustomControl for View  (Format)</span></span>](./typename-element-for-selectioncondition-for-customcontrol-for-view-format.md)

[<span data-ttu-id="79687-141">A nézet (formátum) CustomControl CustomEntry EntrySelectedBy elem.</span><span class="sxs-lookup"><span data-stu-id="79687-141">EntrySelectedBy Element for CustomEntry for CustomControl for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="79687-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="79687-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
