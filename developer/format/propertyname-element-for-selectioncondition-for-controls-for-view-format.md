---
title: PropertyName elemet a vezérlők (formátum) nézet SelectionCondition |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92c4237d-c2b2-4908-82ac-f36070f89d26
caps.latest.revision: 6
ms.openlocfilehash: 79859bed3d762948182e03babf71d4270278bae7
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56845079"
---
# <a name="propertyname-element-for-selectioncondition-for-controls-for-view-format"></a><span data-ttu-id="90193-102">A Nézet Vezérlők eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="90193-102">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>

<span data-ttu-id="90193-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="90193-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="90193-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a bejegyzés szolgál.</span><span class="sxs-lookup"><span data-stu-id="90193-104">When this property is present or when it evaluates to `true`, the condition is met, and the entry is used.</span></span> <span data-ttu-id="90193-105">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="90193-105">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="90193-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő CustomControl vezérlők, a vezérlők, a vezérlők, a vezérlők, a nézet (EntrySelectedBy megtekintése (formátum) SelectionCondition elemhez CustomEntry megtekintése (formátum) EntrySelectedBy elemhez CustomEntries megtekintése (formátum) CustomEntry elemhez Formátum) PropertyName eleme SelectionCondition vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="90193-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format) PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="90193-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="90193-107">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="90193-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="90193-108">Attributes and Elements</span></span>

<span data-ttu-id="90193-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="90193-109">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="90193-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="90193-110">Attributes</span></span>

<span data-ttu-id="90193-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="90193-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="90193-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="90193-112">Child Elements</span></span>

<span data-ttu-id="90193-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="90193-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="90193-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="90193-114">Parent Elements</span></span>

|<span data-ttu-id="90193-115">Elem</span><span class="sxs-lookup"><span data-stu-id="90193-115">Element</span></span>|<span data-ttu-id="90193-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="90193-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="90193-117">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="90193-117">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)|<span data-ttu-id="90193-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="90193-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="90193-119">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="90193-119">Text Value</span></span>

<span data-ttu-id="90193-120">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="90193-120">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="90193-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="90193-121">Remarks</span></span>

<span data-ttu-id="90193-122">A kiválasztási feltétel meg kell adnia legalább egy tulajdonság nevét, vagy egy parancsfájlt, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="90193-122">The selection condition must specify a least one property name or a script, but cannot specify both.</span></span> <span data-ttu-id="90193-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="90193-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="90193-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="90193-124">See Also</span></span>

[<span data-ttu-id="90193-125">Nézet (formátum) vezérlők EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="90193-125">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-controls-for-view-format.md)

[<span data-ttu-id="90193-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="90193-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
