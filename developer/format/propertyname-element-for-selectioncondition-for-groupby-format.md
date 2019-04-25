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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064815"
---
# <a name="propertyname-element-for-selectioncondition-for-groupby-format"></a><span data-ttu-id="e5b5c-102">A GroupBy elemhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e5b5c-102">PropertyName Element for SelectionCondition for GroupBy (Format)</span></span>

<span data-ttu-id="e5b5c-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="e5b5c-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="e5b5c-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="e5b5c-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) PropertyName elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="e5b5c-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionCondition Element for EntrySelectedBy for GroupBy (Format) PropertyName Element for SelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e5b5c-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e5b5c-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="e5b5c-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e5b5c-108">Attributes and Elements</span></span>

<span data-ttu-id="e5b5c-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e5b5c-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e5b5c-110">Attributes</span></span>

<span data-ttu-id="e5b5c-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e5b5c-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e5b5c-112">Child Elements</span></span>

<span data-ttu-id="e5b5c-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e5b5c-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e5b5c-114">Parent Elements</span></span>

|<span data-ttu-id="e5b5c-115">Elem</span><span class="sxs-lookup"><span data-stu-id="e5b5c-115">Element</span></span>|<span data-ttu-id="e5b5c-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="e5b5c-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e5b5c-117">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-117">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="e5b5c-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e5b5c-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="e5b5c-119">Text Value</span></span>

<span data-ttu-id="e5b5c-120">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-120">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="e5b5c-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e5b5c-121">Remarks</span></span>

<span data-ttu-id="e5b5c-122">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság nevét, vagy egy parancsfájlt, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-122">The selection condition must specify a least one property name or a script, but cannot specify both.</span></span> <span data-ttu-id="e5b5c-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="e5b5c-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e5b5c-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e5b5c-124">See Also</span></span>

[<span data-ttu-id="e5b5c-125">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e5b5c-125">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="e5b5c-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e5b5c-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
