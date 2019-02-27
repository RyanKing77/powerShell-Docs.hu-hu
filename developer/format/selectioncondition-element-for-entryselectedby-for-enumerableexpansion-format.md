---
title: EnumerableExpansion (formátum) a EntrySelectedBy SelectionCondition eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8c012115-9241-4851-9015-841eb508faf3
caps.latest.revision: 10
ms.openlocfilehash: d6adf2fa62384d671fd6a07dd185a941daa44cec
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56848411"
---
# <a name="selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="bf54e-102">Az EnumerableExpansion elemhez tartozó EntrySelectedBy SelectionCondition eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="bf54e-102">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="bf54e-103">Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="bf54e-103">Defines the condition that must exist to expand the collection objects of this definition.</span></span>

<span data-ttu-id="bf54e-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="bf54e-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="bf54e-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="bf54e-105">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="bf54e-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="bf54e-106">Attributes and Elements</span></span>

<span data-ttu-id="bf54e-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `SelectionCondition` elemet.</span><span class="sxs-lookup"><span data-stu-id="bf54e-107">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span> <span data-ttu-id="bf54e-108">Meg kell adnia egy `PropertyName` vagy `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="bf54e-108">You must specify a single `PropertyName` or `ScriptBlock` element.</span></span> <span data-ttu-id="bf54e-109">A `SelectionSetName` és `TypeName` elemek egyike sem kötelező.</span><span class="sxs-lookup"><span data-stu-id="bf54e-109">The `SelectionSetName` and `TypeName` elements are optional.</span></span> <span data-ttu-id="bf54e-110">Mindkét elem kiválaszthat egyet.</span><span class="sxs-lookup"><span data-stu-id="bf54e-110">You can specify one of either element.</span></span>

### <a name="attributes"></a><span data-ttu-id="bf54e-111">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="bf54e-111">Attributes</span></span>

<span data-ttu-id="bf54e-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bf54e-112">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="bf54e-113">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="bf54e-113">Child Elements</span></span>

|<span data-ttu-id="bf54e-114">Elem</span><span class="sxs-lookup"><span data-stu-id="bf54e-114">Element</span></span>|<span data-ttu-id="bf54e-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="bf54e-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bf54e-116">SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="bf54e-116">PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="bf54e-117">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="bf54e-117">Optional element.</span></span><br /><br /> <span data-ttu-id="bf54e-118">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="bf54e-118">Specifies the .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="bf54e-119">SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="bf54e-119">ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="bf54e-120">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="bf54e-120">Optional element.</span></span><br /><br /> <span data-ttu-id="bf54e-121">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="bf54e-121">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="bf54e-122">SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span><span class="sxs-lookup"><span data-stu-id="bf54e-122">SelectionSetName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="bf54e-123">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="bf54e-123">Optional element.</span></span><br /><br /> <span data-ttu-id="bf54e-124">Megadja a .NET-típusok, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="bf54e-124">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="bf54e-125">SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a TypeName elem.</span><span class="sxs-lookup"><span data-stu-id="bf54e-125">TypeName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./typename-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="bf54e-126">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="bf54e-126">Optional element.</span></span><br /><br /> <span data-ttu-id="bf54e-127">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="bf54e-127">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="bf54e-128">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="bf54e-128">Parent Elements</span></span>

|<span data-ttu-id="bf54e-129">Elem</span><span class="sxs-lookup"><span data-stu-id="bf54e-129">Element</span></span>|<span data-ttu-id="bf54e-130">Leírás</span><span class="sxs-lookup"><span data-stu-id="bf54e-130">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bf54e-131">EntrySelectedBy eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="bf54e-131">EntrySelectedBy Element for EnumerableExpansion (Format)</span></span>](./entryselectedby-element-for-enumerableexpansion-format.md)|<span data-ttu-id="bf54e-132">Határozza meg, melyik gyűjtemény .NET-objektumokat a definíció szerint bontva.</span><span class="sxs-lookup"><span data-stu-id="bf54e-132">Defines which .NET collection objects are expanded by this definition.</span></span>|

## <a name="remarks"></a><span data-ttu-id="bf54e-133">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="bf54e-133">Remarks</span></span>

<span data-ttu-id="bf54e-134">Minden egyes definíció rendelkeznie kell legalább egy típusnév, kijelölés set vagy meghatározott kiválasztási feltételnek.</span><span class="sxs-lookup"><span data-stu-id="bf54e-134">Each definition must have at least one type name, selection set, or selection condition defined.</span></span>

<span data-ttu-id="bf54e-135">Meghatározásakor kiválasztási feltétel, a következő követelményeknek kell teljesülnie:</span><span class="sxs-lookup"><span data-stu-id="bf54e-135">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="bf54e-136">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="bf54e-136">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="bf54e-137">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="bf54e-137">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="bf54e-138">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételek meghatározása Diplaying adatok](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="bf54e-138">For more information about how to use selection conditions, see [Defining Conditions for Diplaying Data](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="bf54e-139">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="bf54e-139">For more information about other components of a wide view, see [Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="bf54e-140">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bf54e-140">See Also</span></span>

[<span data-ttu-id="bf54e-141">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="bf54e-141">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="bf54e-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="bf54e-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
