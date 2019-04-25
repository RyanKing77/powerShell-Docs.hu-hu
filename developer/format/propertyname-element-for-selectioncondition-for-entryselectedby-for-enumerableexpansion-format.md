---
title: SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ae11924-0072-451e-bf70-c5ffb25dccc0
caps.latest.revision: 13
ms.openlocfilehash: 0c20512e660c8d2b61d063dbd7078b55b23efeb8
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064951"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="8cf7e-102">Az EnumerableExpansion EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="8cf7e-102">PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="8cf7e-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="8cf7e-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span>

<span data-ttu-id="8cf7e-105">Konfigurációs elem (formátum) DefaultSettings elem (formátum) EnumerableExpansions elem (formátum) EnumerableExpansion elem (formátum) EntrySelectedBy elem esetében a EntrySelectedBy EnumerableExpansion (formátum) SelectionCondition elemhez SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a PropertyName eleme EnumerableExpansion (formátum)</span><span class="sxs-lookup"><span data-stu-id="8cf7e-105">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="8cf7e-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="8cf7e-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="8cf7e-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="8cf7e-107">Attributes and Elements</span></span>

<span data-ttu-id="8cf7e-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="8cf7e-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="8cf7e-109">Attributes</span></span>

<span data-ttu-id="8cf7e-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="8cf7e-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="8cf7e-111">Child Elements</span></span>

<span data-ttu-id="8cf7e-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="8cf7e-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="8cf7e-113">Parent Elements</span></span>

|<span data-ttu-id="8cf7e-114">Elem</span><span class="sxs-lookup"><span data-stu-id="8cf7e-114">Element</span></span>|<span data-ttu-id="8cf7e-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="8cf7e-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8cf7e-116">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-116">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="8cf7e-117">Határozza meg azt a feltételt, amelyet a bontsa ki a gyűjtemény objektumokat, ez a definíció léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-117">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="8cf7e-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="8cf7e-118">Text Value</span></span>

<span data-ttu-id="8cf7e-119">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="8cf7e-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="8cf7e-120">Remarks</span></span>

<span data-ttu-id="8cf7e-121">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság neve vagy a parancsfájl kiértékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-121">The selection condition must specify at least one property name or a script to evaluate, but cannot specify both.</span></span> <span data-ttu-id="8cf7e-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="8cf7e-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8cf7e-123">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="8cf7e-123">See Also</span></span>

[<span data-ttu-id="8cf7e-124">Megjelenik feltételeket, amikor adatok meghatározása</span><span class="sxs-lookup"><span data-stu-id="8cf7e-124">Defining Conditions for When Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="8cf7e-125">SelectionCondition EntrySelectedBy EnumerableExpansion (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-125">ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="8cf7e-126">A EnumerableExpansion (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="8cf7e-126">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="8cf7e-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="8cf7e-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
