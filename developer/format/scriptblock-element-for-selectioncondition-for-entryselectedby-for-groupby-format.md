---
title: SelectionCondition EntrySelectedBy GroupBy (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e01344bd-ad69-4789-8e9f-2e79880c3a33
caps.latest.revision: 6
ms.openlocfilehash: cb79fb942111cee89c6b2abba75de4c494082b7e
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064341"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-groupby-format"></a><span data-ttu-id="90a75-102">Az GroupBy EntrySelectedBy eleméhez tartozó SelectionCondition S eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="90a75-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for GroupBy (Format)</span></span>

<span data-ttu-id="90a75-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="90a75-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="90a75-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a definíció szolgál.</span><span class="sxs-lookup"><span data-stu-id="90a75-104">When this script is evaluated to `true`, the condition is met, and the definition is used.</span></span> <span data-ttu-id="90a75-105">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="90a75-105">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="90a75-106">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) EntrySelectedBy elem CustomEntry EntrySelectedBy SelectionCondition GroupBy (formátum) esetében a GroupBy (formátum) ScriptBlock elemhez tartozó GroupBy (formátum) SelectionCondition elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="90a75-106">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) EntrySelectedBy Element for CustomEntry for GroupBy (Format) SelectionCondition Element for EntrySelectedBy for GroupBy (Format) ScriptBlock Element for SelectionCondition for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="90a75-107">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="90a75-107">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="90a75-108">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="90a75-108">Attributes and Elements</span></span>

<span data-ttu-id="90a75-109">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="90a75-109">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="90a75-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="90a75-110">Attributes</span></span>

<span data-ttu-id="90a75-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="90a75-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="90a75-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="90a75-112">Child Elements</span></span>

<span data-ttu-id="90a75-113">Nincs.</span><span class="sxs-lookup"><span data-stu-id="90a75-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="90a75-114">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="90a75-114">Parent Elements</span></span>

|<span data-ttu-id="90a75-115">Elem</span><span class="sxs-lookup"><span data-stu-id="90a75-115">Element</span></span>|<span data-ttu-id="90a75-116">Leírás</span><span class="sxs-lookup"><span data-stu-id="90a75-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="90a75-117">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="90a75-117">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)|<span data-ttu-id="90a75-118">Határozza meg egy feltételt, amely a vezérlőelem definíciójában használt léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="90a75-118">Defines a condition that must exist for the control definition to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="90a75-119">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="90a75-119">Text Value</span></span>

<span data-ttu-id="90a75-120">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="90a75-120">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="90a75-121">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="90a75-121">Remarks</span></span>

<span data-ttu-id="90a75-122">A kiválasztási feltétel adjon meg egy legalább egy parancsfájl vagy a tulajdonság nevét értékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="90a75-122">The selection condition must specify a least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="90a75-123">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [feltételek meghatározása az adatok megjelenítése](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="90a75-123">For more information about how selection conditions can be used, see [Defining Conditions for Displaying Data](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="90a75-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="90a75-124">See Also</span></span>

[<span data-ttu-id="90a75-125">A GroupBy (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="90a75-125">SelectionCondition Element for EntrySelectedBy for GroupBy (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-groupby-format.md)

[<span data-ttu-id="90a75-126">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="90a75-126">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
