---
title: A nézet (formátum) CustomControl SelectionCondition PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fc48a417-2083-46d4-ac38-16c12e65b6b9
caps.latest.revision: 7
ms.openlocfilehash: e08037d5d051d3be51e90193c7e87cc2e738f78a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56850287"
---
# <a name="propertyname-element-for-selectioncondition-for-customcontrol-for-view-format"></a><span data-ttu-id="0d218-102">A Nézet CustomControl eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0d218-102">PropertyName Element for SelectionCondition for CustomControl for View (Format)</span></span>

<span data-ttu-id="0d218-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="0d218-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="0d218-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="0d218-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="0d218-105">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="0d218-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="0d218-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem a CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries CustomControl a nézet (a nézetben (formátum) CustomEntries elemhez CustomEntry CustomControl CustomControl a számára a nézet (formátum) PropertyName CustomControl EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez tartozó CustomEntry a nézet (formátum) EntrySelectedBy elemhez tartozó CustomItem eleme formátumban) A nézet (formátum) CustomControl SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="0d218-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for CustomControl for View (Format) CustomItem Element for CustomEntry for CustomControl for View (Format) EntrySelectedBy Element for CustomEntry for CustomControl for View (Format) SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format) PropertyName Element for SelectionCondition for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0d218-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0d218-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0d218-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0d218-108">Attributes and Elements</span></span>

<span data-ttu-id="0d218-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="0d218-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0d218-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0d218-110">Attributes</span></span>

<span data-ttu-id="0d218-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0d218-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0d218-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0d218-112">Child Elements</span></span>

<span data-ttu-id="0d218-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0d218-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="0d218-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0d218-114">Parent Elements</span></span>

|<span data-ttu-id="0d218-115">Elem</span><span class="sxs-lookup"><span data-stu-id="0d218-115">Element</span></span>|<span data-ttu-id="0d218-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="0d218-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0d218-117">A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="0d218-117">SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)|<span data-ttu-id="0d218-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="0d218-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="0d218-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="0d218-119">Text Value</span></span>

<span data-ttu-id="0d218-120">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="0d218-120">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="0d218-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0d218-121">Remarks</span></span>

<span data-ttu-id="0d218-122">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság nevét, vagy egy parancsfájlt, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="0d218-122">The selection condition must specify a least one property name or a script, but cannot specify both.</span></span> <span data-ttu-id="0d218-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="0d218-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0d218-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0d218-124">See Also</span></span>

[<span data-ttu-id="0d218-125">A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="0d218-125">SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

[<span data-ttu-id="0d218-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0d218-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
