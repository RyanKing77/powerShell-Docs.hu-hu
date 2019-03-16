---
title: SelectionCondition EntrySelectedBy ListControl (formátum) esetében a scriptblock kulcsszót eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4a1adad7-e864-4892-9d26-a6476a9698d2
caps.latest.revision: 7
ms.openlocfilehash: b65d953169f6daf15fb617ce4d0303cf4cb584ee
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58057773"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a><span data-ttu-id="79cde-102">Az ListControl EntrySelectedBy eleméhez tartozó SelectionCondition S eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="79cde-102">ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListControl (Format)</span></span>

<span data-ttu-id="79cde-103">Megadja a parancsprogramot, amely elindítja a feltétel.</span><span class="sxs-lookup"><span data-stu-id="79cde-103">Specifies the script that triggers the condition.</span></span> <span data-ttu-id="79cde-104">Ha ez a parancsfájl kiértékelése `true`, a feltétel nem teljesül, és a regisztrációslista-bejegyzés szolgál.</span><span class="sxs-lookup"><span data-stu-id="79cde-104">When this script is evaluated to `true`, the condition is met, and the list entry is used.</span></span>

<span data-ttu-id="79cde-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) ListControl elem (formátum) ListEntries elem (formátum) ListEntry elem (formátum) EntrySelectedBy elem ListEntry (formátum) SelectionCondition elem számára EntrySelectedBy a SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a scriptblock kulcsszót eleme ListEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="79cde-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) ListControl Element (Format) ListEntries Element (Format) ListEntry Element (Format) EntrySelectedBy Element for ListEntry (Format) SelectionCondition Element for EntrySelectedBy for ListEntry (Format) ScriptBlock Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="79cde-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="79cde-106">Syntax</span></span>

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="79cde-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="79cde-107">Attributes and Elements</span></span>

<span data-ttu-id="79cde-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `ScriptBlock` elemet.</span><span class="sxs-lookup"><span data-stu-id="79cde-108">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="79cde-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="79cde-109">Attributes</span></span>

<span data-ttu-id="79cde-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="79cde-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="79cde-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="79cde-111">Child Elements</span></span>

<span data-ttu-id="79cde-112">Nincs.</span><span class="sxs-lookup"><span data-stu-id="79cde-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="79cde-113">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="79cde-113">Parent Elements</span></span>

|<span data-ttu-id="79cde-114">Elem</span><span class="sxs-lookup"><span data-stu-id="79cde-114">Element</span></span>|<span data-ttu-id="79cde-115">Leírás</span><span class="sxs-lookup"><span data-stu-id="79cde-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="79cde-116">A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="79cde-116">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|<span data-ttu-id="79cde-117">Meghatározza a feltétellel, hogy a lista bejegyzés használandó léteznie kell.</span><span class="sxs-lookup"><span data-stu-id="79cde-117">Defines the condition that must exist for this list entry to be used.</span></span>|

## <a name="text-value"></a><span data-ttu-id="79cde-118">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="79cde-118">Text Value</span></span>

<span data-ttu-id="79cde-119">Adja meg a parancsfájl, amely ki lesz értékelve.</span><span class="sxs-lookup"><span data-stu-id="79cde-119">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="79cde-120">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="79cde-120">Remarks</span></span>

<span data-ttu-id="79cde-121">A kiválasztási feltétel adjon meg egy legalább egy parancsfájl vagy a tulajdonság nevét értékelése, de nem adható meg egyszerre.</span><span class="sxs-lookup"><span data-stu-id="79cde-121">The selection condition must specify a least one script or property name to evaluate, but cannot specify both.</span></span> <span data-ttu-id="79cde-122">(Hogyan használható a kiválasztási feltételek kapcsolatos további információkért lásd: [definiáló vonatkozó feltételeket, amikor egy nézet bejegyzés vagy az elem](./defining-conditions-for-displaying-data.md).)</span><span class="sxs-lookup"><span data-stu-id="79cde-122">(For more information about how selection conditions can be used, see [Defining Conditions for when a View Entry or Item is Used](./defining-conditions-for-displaying-data.md).)</span></span>

<span data-ttu-id="79cde-123">Megjelenítheti az egyéb összetevőivel kapcsolatos további információk: [listanézet](./creating-a-list-view.md).</span><span class="sxs-lookup"><span data-stu-id="79cde-123">For more information about the other components of a list view, see [List View](./creating-a-list-view.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="79cde-124">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="79cde-124">See Also</span></span>

[<span data-ttu-id="79cde-125">ListEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="79cde-125">ListEntry Element (Format)</span></span>](./listentry-element-for-listcontrol-format.md)

[<span data-ttu-id="79cde-126">SelectionCondition EntrySelectedBy ListEntry (formátum) esetében a PropertyName elem.</span><span class="sxs-lookup"><span data-stu-id="79cde-126">PropertyName Element for SelectionCondition for EntrySelectedBy for ListEntry (Format)</span></span>](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="79cde-127">A ListEntry (formátum) EntrySelectedBy SelectionCondition elem.</span><span class="sxs-lookup"><span data-stu-id="79cde-127">SelectionCondition Element for EntrySelectedBy for ListEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[<span data-ttu-id="79cde-128">Listanézet</span><span class="sxs-lookup"><span data-stu-id="79cde-128">List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="79cde-129">Feltételek meghatározása egy nézet bejegyzés vagy elem használatakor</span><span class="sxs-lookup"><span data-stu-id="79cde-129">Defining Conditions for when a View Entry or Item is Used</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="79cde-130">Egy Windows PowerShell formázás és a fájl típusai</span><span class="sxs-lookup"><span data-stu-id="79cde-130">Writing a Windows PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)
