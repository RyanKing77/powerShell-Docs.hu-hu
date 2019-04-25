---
title: SelectionCondition CustomControl nézet (formátum) a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7031fa8b-3e2b-4ea8-89cb-95171f467b5a
caps.latest.revision: 6
ms.openlocfilehash: e55d1c5aa533005b258ecbbbf3ed9d55f852eab6
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064560"
---
# <a name="scriptblock-element-for-selectioncondition-for-customcontrol-for-view-format"></a><span data-ttu-id="34d99-102">A Nézet CustomControl eleméhez tartozó SelectionCondition ScriptBlock eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="34d99-102">ScriptBlock Element for SelectionCondition for CustomControl for View (Format)</span></span>

<span data-ttu-id="34d99-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="34d99-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="34d99-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="34d99-104">When this script is evaluated to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="34d99-105">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="34d99-105">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="34d99-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem a CustomControl megtekintése (formátum) CustomEntry elemhez tartozó CustomEntries CustomControl a nézet (a nézetben (formátum) CustomEntries elemhez CustomEntry CustomControl CustomControl SelectionCondition CustomControl nézet (formátum) esetében a nézet (formátum) ScriptBlock elemhez tartozó EntrySelectedBy a nézet (formátum) SelectionCondition elemhez tartozó CustomItem eleme formátumban)</span><span class="sxs-lookup"><span data-stu-id="34d99-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for CustomControl for View (Format) CustomItem Element for CustomEntry for CustomControl for View (Format) SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format) ScriptBlock Element for SelectionCondition for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="34d99-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="34d99-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="34d99-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="34d99-108">Attributes and Elements</span></span>

<span data-ttu-id="34d99-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="34d99-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="34d99-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="34d99-110">Attributes</span></span>

<span data-ttu-id="34d99-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="34d99-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="34d99-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="34d99-112">Child Elements</span></span>

<span data-ttu-id="34d99-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="34d99-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="34d99-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="34d99-114">Parent Elements</span></span>

|<span data-ttu-id="34d99-115">Elem</span><span class="sxs-lookup"><span data-stu-id="34d99-115">Element</span></span>|<span data-ttu-id="34d99-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="34d99-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="34d99-117">A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="34d99-117">SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)|<span data-ttu-id="34d99-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="34d99-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="34d99-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="34d99-119">Text Value</span></span>

<span data-ttu-id="34d99-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="34d99-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="34d99-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="34d99-121">Remarks</span></span>

<span data-ttu-id="34d99-122">A kiválasztási feltétel adjon meg egy legalább egy parancsfájl vagy a tulajdonság nevét értékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="34d99-122">The selection condition must specify a least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="34d99-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="34d99-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="34d99-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="34d99-124">See Also</span></span>

[<span data-ttu-id="34d99-125">A nézet (formátum) CustomControl EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="34d99-125">SelectionCondition Element for EntrySelectedBy for CustomControl for View (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-customcontrol-format.md)

[<span data-ttu-id="34d99-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="34d99-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
