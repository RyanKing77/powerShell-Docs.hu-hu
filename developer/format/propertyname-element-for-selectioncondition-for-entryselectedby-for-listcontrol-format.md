---
title: SelectionCondition EntrySelectedBy ListControl (formátum) esetében a PropertyName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71c3f1f6-6fe2-42f1-8260-6974d3871748
caps.latest.revision: 11
ms.openlocfilehash: 7d526372cf80327b3fb9b79b6e83429c57780183
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58059014"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="ff6fb-102">Az ListControl EntrySelectedBy eleméhez tartozó SelectionCondition PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="ff6fb-102">PropertyName Element for SelectionCondition for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="ff6fb-103">Megadja a .NET-tulajdonság, amely elindítja a feltételt.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="ff6fb-104">Ha ez a tulajdonság jelen-e, vagy ha való kiértékelése által `true`, a feltétel nem teljesül, és a regisztrációslista-bejegyzés szolgál.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-104">When this property is present or when it evaluates to `true`, the condition is met, and the list entry is used.</span></span>

<span data-ttu-id="ff6fb-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára A PropertyName elem ListEntry (formátum) a SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a EntrySelectedBy</span><span class="sxs-lookup"><span data-stu-id="ff6fb-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="ff6fb-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="ff6fb-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="ff6fb-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="ff6fb-107">Attributes and Elements</span></span>

<span data-ttu-id="ff6fb-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="ff6fb-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="ff6fb-109">Attributes</span></span>

<span data-ttu-id="ff6fb-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="ff6fb-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="ff6fb-111">Child Elements</span></span>

<span data-ttu-id="ff6fb-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="ff6fb-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="ff6fb-113">Parent Elements</span></span>

|<span data-ttu-id="ff6fb-114">Elem</span><span class="sxs-lookup"><span data-stu-id="ff6fb-114">Element</span></span>|<span data-ttu-id="ff6fb-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="ff6fb-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="ff6fb-116">A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-116">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="ff6fb-117">Meghatározza a feltétellel, hogy a lista bejegyzés használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-117">Defines the condition that must exist for this list entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="ff6fb-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="ff6fb-118">Text Value</span></span>

<span data-ttu-id="ff6fb-119">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="ff6fb-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="ff6fb-120">Remarks</span></span>

<span data-ttu-id="ff6fb-121">A kiválasztási feltételnek legalább egy tulajdonság nevét, vagy parancsprogram-blokkot kell megadnia, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-121">The selection condition must specify at least one property name or a script block, but cannot specify both.</span></span> <span data-ttu-id="ff6fb-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="ff6fb-122">For more information about how to use selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="ff6fb-123">A listanézet egyéb összetevőivel kapcsolatos további információkért lásd: [lista nézet létrehozása](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="ff6fb-123">For more information about other components of a list view, see [Creating List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ff6fb-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="ff6fb-124">See Also</span></span>

[<span data-ttu-id="ff6fb-125">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="ff6fb-125">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="ff6fb-126">Megjelenik feltételeket, amikor adatok meghatározása</span><span class="sxs-lookup"><span data-stu-id="ff6fb-126">Defining Conditions for When Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="ff6fb-127">ListEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="ff6fb-127">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="ff6fb-128">SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a scriptblock kulcsszót elem.</span><span class="sxs-lookup"><span data-stu-id="ff6fb-128">ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="ff6fb-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="ff6fb-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
