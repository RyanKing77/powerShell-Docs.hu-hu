---
title: A GroupBy (formátum) SelectionCondition PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d1707317-6c26-4866-bcc1-8924103c9014
caps.latest.revision: 6
ms.openlocfilehash: 7241ea0ea364befa7ad4ab0af4c4209be72214a7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56844841"
---
# <a name="propertyname-element-for-selectioncondition-for-groupby-format"></a><span data-ttu-id="7cba1-102">A GroupBy elemhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="7cba1-102">PropertyName Element for SelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="7cba1-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="7cba1-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="7cba1-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="7cba1-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="7cba1-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="7cba1-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="7cba1-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) PropertyName elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="7cba1-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionCondition Element for EntrySelectedBy for GroupBy (Format) PropertyName Element for SelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="7cba1-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="7cba1-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="7cba1-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="7cba1-108">Attributes and Elements</span></span>

<span data-ttu-id="7cba1-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="7cba1-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="7cba1-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="7cba1-110">Attributes</span></span>

<span data-ttu-id="7cba1-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7cba1-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="7cba1-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="7cba1-112">Child Elements</span></span>

<span data-ttu-id="7cba1-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="7cba1-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="7cba1-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="7cba1-114">Parent Elements</span></span>

|<span data-ttu-id="7cba1-115">Elem</span><span class="sxs-lookup"><span data-stu-id="7cba1-115">Element</span></span>|<span data-ttu-id="7cba1-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="7cba1-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="7cba1-117">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="7cba1-117">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="7cba1-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="7cba1-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="7cba1-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="7cba1-119">Text Value</span></span>

<span data-ttu-id="7cba1-120">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="7cba1-120">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="7cba1-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="7cba1-121">Remarks</span></span>

<span data-ttu-id="7cba1-122">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság nevét, vagy egy parancsfájlt, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="7cba1-122">The selection condition must specify a least one property name or a script, but cannot specify both.</span></span> <span data-ttu-id="7cba1-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="7cba1-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="7cba1-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="7cba1-124">See Also</span></span>

[<span data-ttu-id="7cba1-125">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="7cba1-125">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="7cba1-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="7cba1-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
