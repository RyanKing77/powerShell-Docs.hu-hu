---
title: SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4126b799-c43d-4175-8513-6d761c65437e
caps.latest.revision: 9
ms.openlocfilehash: a51d8d22fa8b0c7f303a5e8f37edcc5e57724063
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064373"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="48961-102">Az EnumerableExpansion EntrySelectedBy eleméhez tartozó SelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="48961-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="48961-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="48961-103">Specifies the script that triggers the condition.</span></span>

<span data-ttu-id="48961-104">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="48961-104">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format) ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="48961-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="48961-105">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="48961-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="48961-106">Attributes and Elements</span></span>

<span data-ttu-id="48961-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="48961-107">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="48961-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="48961-108">Attributes</span></span>

<span data-ttu-id="48961-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="48961-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="48961-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="48961-110">Child Elements</span></span>

<span data-ttu-id="48961-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="48961-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="48961-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="48961-112">Parent Elements</span></span>

|<span data-ttu-id="48961-113">Elem</span><span class="sxs-lookup"><span data-stu-id="48961-113">Element</span></span>|<span data-ttu-id="48961-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="48961-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="48961-115">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="48961-115">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="48961-116">Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="48961-116">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="48961-117">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="48961-117">Text Value</span></span>

<span data-ttu-id="48961-118">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="48961-118">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="48961-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="48961-119">Remarks</span></span>

<span data-ttu-id="48961-120">A kiválasztási feltétel kiértékeléséhez, legalább egy parancsfájl vagy a tulajdonság nevét kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="48961-120">The selection condition must specify at least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="48961-121">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="48961-121">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="48961-122">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="48961-122">See Also</span></span>

[<span data-ttu-id="48961-123">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="48961-123">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="48961-124">SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="48961-124">PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="48961-125">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="48961-125">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="48961-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="48961-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
