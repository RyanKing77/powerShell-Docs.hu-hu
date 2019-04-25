---
title: SelectionCondition EntrySelectedBy TableControl (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2b11fbcf-3426-48ae-9319-2c847969f723
caps.latest.revision: 10
ms.openlocfilehash: 7afc834e68ef332bee1e23da782fb5c5527fcf54
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62076344"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="cc5b5-102">Az TableControl EntrySelectedBy eleméhez tartozó SelectionCondition S eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="cc5b5-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="cc5b5-103">Adja meg a parancsprogram-blokkot, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-103">Specifies the script block that triggers the condition.</span></span> <span data-ttu-id="cc5b5-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a táblabejegyzés szolgál.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-104">When this script is evaluated to `true`, the condition is met, and the table entry is used.</span></span>

<span data-ttu-id="cc5b5-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) TableRowEntry (formátum) ScriptBlock elemhez tartozó SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element for TableRowEntry (Format) SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format) ScriptBlock Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cc5b5-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cc5b5-106">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cc5b5-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="cc5b5-107">Attributes and Elements</span></span>

<span data-ttu-id="cc5b5-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-108">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cc5b5-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="cc5b5-109">Attributes</span></span>

<span data-ttu-id="cc5b5-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cc5b5-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="cc5b5-111">Child Elements</span></span>

<span data-ttu-id="cc5b5-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="cc5b5-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="cc5b5-113">Parent Elements</span></span>

|<span data-ttu-id="cc5b5-114">Elem</span><span class="sxs-lookup"><span data-stu-id="cc5b5-114">Element</span></span>|<span data-ttu-id="cc5b5-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="cc5b5-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cc5b5-116">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-116">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="cc5b5-117">Határozza meg azt a feltételt, amelyet a használandó tábla bejegyzéshez tartozó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-117">Defines the condition that must exist for this table entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="cc5b5-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="cc5b5-118">Text Value</span></span>

<span data-ttu-id="cc5b5-119">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-119">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="cc5b5-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="cc5b5-120">Remarks</span></span>

<span data-ttu-id="cc5b5-121">A kiválasztási feltétel meg kell adnia legalább egy parancsfájl letiltása vagy a tulajdonság nevét, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-121">The selection condition must specify at least one script block or property name, but cannot specify both.</span></span> <span data-ttu-id="cc5b5-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="cc5b5-122">For more information about how to use selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="cc5b5-123">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="cc5b5-123">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cc5b5-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cc5b5-124">See Also</span></span>

[<span data-ttu-id="cc5b5-125">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="cc5b5-125">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="cc5b5-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="cc5b5-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="cc5b5-127">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-127">PropertyName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format.md)

[<span data-ttu-id="cc5b5-128">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cc5b5-128">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="cc5b5-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="cc5b5-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
