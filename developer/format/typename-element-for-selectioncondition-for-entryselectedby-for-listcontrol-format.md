---
title: SelectionCondition EntrySelectedBy ListControl (formátum) esetében a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bd025a3a-3780-40db-a068-873e7df38015
caps.latest.revision: 9
ms.openlocfilehash: 2b76b040b39088cc9c3b9d6890c38df3c533b39f
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083858"
---
# <a name="typename-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="cf759-102">Az ListControl EntrySelectedBy eleméhez tartozó SelectionCondition TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="cf759-102">TypeName Element for SelectionCondition for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="cf759-103">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="cf759-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="cf759-104">Ez a típus meghatározva, a regisztrációslista-bejegyzés használ.</span><span class="sxs-lookup"><span data-stu-id="cf759-104">When this type is present, the list entry is used.</span></span>

<span data-ttu-id="cf759-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem ListControl elem (formátum) ListEntries elem ListControl (formátum) ListEntry elemhez tartozó ListEntries ListControl (formátum) EntrySelectedBy elemhez tartozó ListEntry EntrySelectedBy SelectionCondition EntrySelectedBy ListControl (formátum) esetében a vonatkozó ListControl (formátum) TypeName elemhez tartozó ListControl (formátum) SelectionCondition elemhez</span><span class="sxs-lookup"><span data-stu-id="cf759-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element for ListControl (Format) ListEntry Element for ListEntries for ListControl (Format) EntrySelectedBy Element for ListEntry for ListControl (Format) SelectionCondition Element for EntrySelectedBy for ListControl (Format) TypeName Element for SelectionCondition for EntrySelectedBy for ListControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cf759-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="cf759-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cf759-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="cf759-107">Attributes and Elements</span></span>

<span data-ttu-id="cf759-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="cf759-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cf759-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="cf759-109">Attributes</span></span>

<span data-ttu-id="cf759-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cf759-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cf759-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="cf759-111">Child Elements</span></span>

<span data-ttu-id="cf759-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="cf759-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="cf759-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="cf759-113">Parent Elements</span></span>

|<span data-ttu-id="cf759-114">Elem</span><span class="sxs-lookup"><span data-stu-id="cf759-114">Element</span></span>|<span data-ttu-id="cf759-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="cf759-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cf759-116">A ListControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cf759-116">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="cf759-117">Meghatározza a feltétellel, hogy a lista bejegyzés használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="cf759-117">Defines the condition that must exist for this list entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="cf759-118">A szöveges érték</span><span class="sxs-lookup"><span data-stu-id="cf759-118">Text Value</span></span>

<span data-ttu-id="cf759-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="cf759-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="cf759-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="cf759-120">Remarks</span></span>

<span data-ttu-id="cf759-121">A kiválasztási feltétel adhat meg minden olyan .NET-típusok száma vagy a kiválasztási állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="cf759-121">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span> <span data-ttu-id="cf759-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="cf759-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="cf759-123">További információ más olyan listanézetet összetevőinek: [lista nézet létrehozásával](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="cf759-123">For more information about other the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cf759-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="cf759-124">See Also</span></span>

[<span data-ttu-id="cf759-125">Lista nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="cf759-125">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="cf759-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="cf759-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="cf759-127">A ListControl (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="cf759-127">SelectionCondition Element for EntrySelectedBy for ListControl (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="cf759-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="cf759-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
