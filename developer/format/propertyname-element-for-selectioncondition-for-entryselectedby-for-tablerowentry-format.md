---
title: SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba3b4d9b-2b8c-4a3a-8887-6c606eb9d490
caps.latest.revision: 10
ms.openlocfilehash: 48011950ed64e78a84292762f2c7779003dc59fd
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62064662"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-tablerowentry-format"></a><span data-ttu-id="f211a-102">Az TableRowEntry EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="f211a-102">PropertyName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>

<span data-ttu-id="f211a-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="f211a-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="f211a-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a táblabejegyzés szolgál.</span><span class="sxs-lookup"><span data-stu-id="f211a-104">When this property is present or when it evaluates to `true`, the condition is met, and the table entry is used.</span></span>

<span data-ttu-id="f211a-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) TableRowEntry (formátum) PropertyName elemhez tartozó SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="f211a-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element for TableRowEntry (Format) SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="f211a-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="f211a-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="f211a-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="f211a-107">Attributes and Elements</span></span>

<span data-ttu-id="f211a-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="f211a-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="f211a-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="f211a-109">Attributes</span></span>

<span data-ttu-id="f211a-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="f211a-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="f211a-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="f211a-111">Child Elements</span></span>

<span data-ttu-id="f211a-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="f211a-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="f211a-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="f211a-113">Parent Elements</span></span>

|<span data-ttu-id="f211a-114">Elem</span><span class="sxs-lookup"><span data-stu-id="f211a-114">Element</span></span>|<span data-ttu-id="f211a-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="f211a-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="f211a-116">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="f211a-116">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="f211a-117">Határozza meg azt a feltételt, amelyet a használandó tábla bejegyzéshez tartozó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="f211a-117">Defines the condition that must exist for this table entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="f211a-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="f211a-118">Text Value</span></span>

<span data-ttu-id="f211a-119">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="f211a-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="f211a-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="f211a-120">Remarks</span></span>

<span data-ttu-id="f211a-121">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="f211a-121">The selection condition must specify at least one property name or a script block, but cannot specify both.</span></span> <span data-ttu-id="f211a-122">Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="f211a-122">For more information about how selection conditions can be used, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="f211a-123">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="f211a-123">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f211a-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="f211a-124">See Also</span></span>

[<span data-ttu-id="f211a-125">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="f211a-125">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="f211a-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="f211a-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="f211a-127">SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="f211a-127">ScriptBlock Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="f211a-128">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="f211a-128">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="f211a-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="f211a-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
