---
title: SelectionCondition EntrySelectedBy WideControl (formátum) esetében a TypeName eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6d6d43fa-c900-4e2f-952d-deccd584236f
caps.latest.revision: 11
ms.openlocfilehash: 6142350e3843a5feddcb5cee8901bbfa607d8d4c
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58055979"
---
# <a name="typename-element-for-selectioncondition-for-entryselectedby-for-widecontrol-format"></a><span data-ttu-id="e520c-102">Az WideControl EntrySelectedBy eleméhez tartozó SelectionCondition TypeName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="e520c-102">TypeName Element for SelectionCondition for EntrySelectedBy for WideControl (Format)</span></span>

<span data-ttu-id="e520c-103">A .NET típusát, amely elindítja a feltételt határozza meg.</span><span class="sxs-lookup"><span data-stu-id="e520c-103">Specifies a .NET type that triggers the condition.</span></span> <span data-ttu-id="e520c-104">Ez a típus meghatározva, a definíciót használ.</span><span class="sxs-lookup"><span data-stu-id="e520c-104">When this type is present, the definition is used.</span></span>

<span data-ttu-id="e520c-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum) EntrySelectedBy elem WideEntry (formátum) SelectionCondition elem számára A TypeName elem WideEntry (formátum) a SelectionCondition EntrySelectedBy WideEntry (formátum) esetében a EntrySelectedBy</span><span class="sxs-lookup"><span data-stu-id="e520c-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format) EntrySelectedBy Element for WideEntry (Format) SelectionCondition Element for EntrySelectedBy for WideEntry (Format) TypeName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e520c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="e520c-106">Syntax</span></span>

```xml
<TypeName>Nameof.NetType</TypeName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="e520c-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="e520c-107">Attributes and Elements</span></span>

<span data-ttu-id="e520c-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `TypeName` elemet.</span><span class="sxs-lookup"><span data-stu-id="e520c-108">The following sections describe attributes, child elements, and the parent element of the `TypeName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="e520c-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="e520c-109">Attributes</span></span>

<span data-ttu-id="e520c-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e520c-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e520c-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="e520c-111">Child Elements</span></span>

<span data-ttu-id="e520c-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="e520c-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e520c-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="e520c-113">Parent Elements</span></span>

|<span data-ttu-id="e520c-114">Elem</span><span class="sxs-lookup"><span data-stu-id="e520c-114">Element</span></span>|<span data-ttu-id="e520c-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="e520c-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e520c-116">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e520c-116">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)|<span data-ttu-id="e520c-117">Határozza meg azt a feltételt, amelyet a használt széles bejegyzéshez tartozó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="e520c-117">Defines the condition that must exist for this wide entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e520c-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="e520c-118">Text Value</span></span>

<span data-ttu-id="e520c-119">Adja meg a teljes nevet, a .NET-típus, például `System.IO.DirectoryInfo`.</span><span class="sxs-lookup"><span data-stu-id="e520c-119">Specify the fully qualified name of the .NET type, such as `System.IO.DirectoryInfo`.</span></span>

## <a name="remarks"></a><span data-ttu-id="e520c-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="e520c-120">Remarks</span></span>

<span data-ttu-id="e520c-121">A kiválasztási feltétel adhatja meg a .NET-típus vagy egyéb állítja be, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="e520c-121">The selection condition can specify a .NET type or a selection set, but cannot specify both.</span></span> <span data-ttu-id="e520c-122">Kiválasztási feltételek használatával kapcsolatos további információkért lásd: [feltételeinek meghatározása mikor jelenik meg adat](./defining-conditions-for-displaying-data.md).</span><span class="sxs-lookup"><span data-stu-id="e520c-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

<span data-ttu-id="e520c-123">Egy széles nézet egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="e520c-123">For more information about other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="e520c-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="e520c-124">See Also</span></span>

[<span data-ttu-id="e520c-125">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="e520c-125">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="e520c-126">Mikor jelenik meg adat feltételeinek meghatározása</span><span class="sxs-lookup"><span data-stu-id="e520c-126">Defining Conditions for When Data Is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="e520c-127">A WideEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="e520c-127">SelectionCondition Element for EntrySelectedBy for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="e520c-128">A EntrySelectedBy WideEntry (formátum) a SelectionCondition SelectionSetName eleme</span><span class="sxs-lookup"><span data-stu-id="e520c-128">SelectionSetName Element for SelectionCondition for EntrySelectedBy for WideEntry (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="e520c-129">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="e520c-129">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
