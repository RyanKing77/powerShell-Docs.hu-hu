---
title: SelectionCondition EntrySelectedBy TableControl (formátum) esetében a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e97d56fb-4e35-447a-9282-26f10d0a4609
caps.latest.revision: 11
ms.openlocfilehash: fe65ac95cead7df0069ffdae666fb34b7309fbb6
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847158"
---
# <a name="typename-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format"></a><span data-ttu-id="03c7c-102">Az TableControl EntrySelectedBy eleméhez tartozó SelectionCondition TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="03c7c-102">TypeName Element for SelectionCondition for EntrySelectedBy for TableControl (Format)</span></span>

<span data-ttu-id="03c7c-103">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="03c7c-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="03c7c-104">Ha ez a típus meghatározva, a feltétel nem teljesül, és a táblázatsor szolgál.</span><span class="sxs-lookup"><span data-stu-id="03c7c-104">When this type is present, the condition is met, and the table row is used.</span></span>

<span data-ttu-id="03c7c-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) TableControl elem (formátum) TableRowEntries elem (formátum) TableRowEntry elem (formátum) EntrySelectedBy elem a TableRowEntry (formátum) TableRowEntry (formátum) TypeName elemhez tartozó SelectionCondition EntrySelectedBy TableRowEntry (formátum) esetében a EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="03c7c-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableRowEntries Element (Format) TableRowEntry Element (Format) EntrySelectedBy Element for TableRowEntry (Format) SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format) TypeName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="03c7c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="03c7c-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="03c7c-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="03c7c-107">Attributes and Elements</span></span>

<span data-ttu-id="03c7c-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="03c7c-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="03c7c-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="03c7c-109">Attributes</span></span>

<span data-ttu-id="03c7c-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="03c7c-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="03c7c-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="03c7c-111">Child Elements</span></span>

<span data-ttu-id="03c7c-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="03c7c-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="03c7c-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="03c7c-113">Parent Elements</span></span>

|<span data-ttu-id="03c7c-114">Elem</span><span class="sxs-lookup"><span data-stu-id="03c7c-114">Element</span></span>|<span data-ttu-id="03c7c-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="03c7c-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="03c7c-116">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="03c7c-116">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)|<span data-ttu-id="03c7c-117">Meghatározza a feltétellel, hogy a tábla sor használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="03c7c-117">Defines the condition that must exist for this table row to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="03c7c-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="03c7c-118">Text Value</span></span>

<span data-ttu-id="03c7c-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="03c7c-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="03c7c-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="03c7c-120">Remarks</span></span>

<span data-ttu-id="03c7c-121">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="03c7c-121">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span> <span data-ttu-id="03c7c-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="03c7c-122">For more information about how to use selection conditions, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="03c7c-123">A táblázatos nézetre az összetevőivel kapcsolatos további információkért lásd: [tábla nézetek létrehozásával](./creating-a-table-view.md).</span><span class="sxs-lookup"><span data-stu-id="03c7c-123">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="03c7c-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="03c7c-124">See Also</span></span>

[<span data-ttu-id="03c7c-125">Tábla nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="03c7c-125">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="03c7c-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="03c7c-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="03c7c-127">A TableRowEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="03c7c-127">SelectionCondition Element for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="03c7c-128">A EntrySelectedBy TableRowEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="03c7c-128">SelectionSetName Element for SelectionCondition for EntrySelectedBy for TableRowEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-tablecontrol-format.md)

[<span data-ttu-id="03c7c-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="03c7c-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
