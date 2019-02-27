---
title: SelectionCondition EntrySelectedBy WideControl (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ec68309-7826-4643-a521-e29c996663fb
caps.latest.revision: 11
ms.openlocfilehash: 649a978e21e9421a3f3e953261e1d309e23c3f9c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851673"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="2a956-102">Az WideControl EntrySelectedBy eleméhez tartozó SelectionCondition S eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="2a956-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="2a956-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="2a956-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="2a956-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a széles körű bejegyzés definíciót használja.</span><span class="sxs-lookup"><span data-stu-id="2a956-104">When this script is evaluated to `true`, the condition is met, and the wide entry definition is used.</span></span>

<span data-ttu-id="2a956-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára EntrySelectedBy a SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a scriptblock kulcsszót eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="2a956-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) ScriptBlock Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="2a956-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="2a956-106">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="2a956-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="2a956-107">Attributes and Elements</span></span>

<span data-ttu-id="2a956-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="2a956-108">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="2a956-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="2a956-109">Attributes</span></span>

<span data-ttu-id="2a956-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2a956-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="2a956-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="2a956-111">Child Elements</span></span>

<span data-ttu-id="2a956-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="2a956-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="2a956-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="2a956-113">Parent Elements</span></span>

|<span data-ttu-id="2a956-114">Elem</span><span class="sxs-lookup"><span data-stu-id="2a956-114">Element</span></span>|<span data-ttu-id="2a956-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="2a956-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="2a956-116">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="2a956-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="2a956-117">Határozza meg azt a feltételt, amelyet a definíció használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="2a956-117">Defines the condition that must exist for this definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="2a956-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="2a956-118">Text Value</span></span>

<span data-ttu-id="2a956-119">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="2a956-119">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="2a956-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="2a956-120">Remarks</span></span>

<span data-ttu-id="2a956-121">A kiválasztási feltétel kiértékeléséhez, legalább egy parancsfájl vagy a tulajdonság nevét kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="2a956-121">The selection condition must specify at least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="2a956-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="2a956-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="2a956-123">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="2a956-123">For more information about other components of a wide view, see [Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="2a956-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="2a956-124">See Also</span></span>

[<span data-ttu-id="2a956-125">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="2a956-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="2a956-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="2a956-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="2a956-127">SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="2a956-127">PropertyName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="2a956-128">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="2a956-128">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="2a956-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="2a956-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
