---
title: (Formátum) WideControl WideEntry eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 014763cb-7716-4931-899c-8375b5d7a3dd
caps.latest.revision: 15
ms.openlocfilehash: d1d13b5c3436871053353814293d9163ea13c7fb
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847179"
---
# <a name="wideentry-element-for-widecontrol-format"></a><span data-ttu-id="af372-102">A WideControl WideEntry eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-102">WideEntry Element for WideControl (Format)</span></span>

<span data-ttu-id="af372-103">A széles nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="af372-103">Provides a definition of the wide view.</span></span>

<span data-ttu-id="af372-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum) WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format) WideEntry Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="af372-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="af372-105">Syntax</span></span>

```xml
<WideEntry>
  <EntrySelectedBy>...</EntrySelectedBy>
  <WideItem>...</WideItem>
</WideEntry>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="af372-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="af372-106">Attributes and Elements</span></span>

<span data-ttu-id="af372-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `WideEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="af372-107">The following sections describe the attributes, child elements, and the parent element of the `WideEntry` element.</span></span> <span data-ttu-id="af372-108">Meg kell adnia egy `WideItem` gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="af372-108">You must specify a single `WideItem` child element.</span></span>

### <a name="attributes"></a><span data-ttu-id="af372-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="af372-109">Attributes</span></span>

<span data-ttu-id="af372-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="af372-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="af372-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="af372-111">Child Elements</span></span>

|<span data-ttu-id="af372-112">Elem</span><span class="sxs-lookup"><span data-stu-id="af372-112">Element</span></span>|<span data-ttu-id="af372-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="af372-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="af372-114">EntrySelectedBy eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-114">EntrySelectedBy Element for WideEntry (Format)</span></span>](./entryselectedby-element-for-wideentry-format.md)|<span data-ttu-id="af372-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="af372-115">Optional element.</span></span><br /><br /> <span data-ttu-id="af372-116">A .NET-típusokat, amelyek a széles körű bejegyzés definíció vagy a feltétellel, hogy léteznie kell a definíció használandó határozza meg.</span><span class="sxs-lookup"><span data-stu-id="af372-116">Defines the .NET types that use this wide entry definition or the condition that must exist for this definition to be used.</span></span>|
|[<span data-ttu-id="af372-117">WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-117">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)|<span data-ttu-id="af372-118">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="af372-118">Required element.</span></span><br /><br /> <span data-ttu-id="af372-119">Határozza meg, tulajdonság vagy parancsfájl, amelynek értéke megjelenik.</span><span class="sxs-lookup"><span data-stu-id="af372-119">Defines the property or script whose value is displayed.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="af372-120">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="af372-120">Parent Elements</span></span>

|<span data-ttu-id="af372-121">Elem</span><span class="sxs-lookup"><span data-stu-id="af372-121">Element</span></span>|<span data-ttu-id="af372-122">Leírás</span><span class="sxs-lookup"><span data-stu-id="af372-122">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="af372-123">WideEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-123">WideEntries Element (Format)</span></span>](./wideentries-element-for-widecontrol-format.md)|<span data-ttu-id="af372-124">A széles nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="af372-124">Provides the definitions of the wide view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="af372-125">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="af372-125">Remarks</span></span>

<span data-ttu-id="af372-126">A széles nézet olyan egyetlen tulajdonság értékét vagy az egyes objektumok parancsfájlérték megjelenítő lista formájában.</span><span class="sxs-lookup"><span data-stu-id="af372-126">A wide view is a list format that displays a single property value or script value for each object.</span></span> <span data-ttu-id="af372-127">Ellentétben más típusú nézetek minden egyes nézet definíciójában csak egy elem elem is megadhat.</span><span class="sxs-lookup"><span data-stu-id="af372-127">Unlike other types of views, you can specify only one item element for each view definition.</span></span> <span data-ttu-id="af372-128">Egy széles nézet az egyéb összetevőivel kapcsolatos további információkért lásd: [széles nézet létrehozásával](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="af372-128">For more information about the other components of a wide view, see [Creating a Wide View](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="af372-129">Példa</span><span class="sxs-lookup"><span data-stu-id="af372-129">Example</span></span>

<span data-ttu-id="af372-130">A következő példa bemutatja egy `WideEntry` elem, amely meghatározza egy `WideItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="af372-130">The following example shows a `WideEntry` element that defines a single `WideItem` element.</span></span> <span data-ttu-id="af372-131">A `WideItem` elem definiálja a tulajdonságot, amelynek értéke megjelenik a nézetben.</span><span class="sxs-lookup"><span data-stu-id="af372-131">The `WideItem` element defines the property whose value is displayed in the view.</span></span>

```xml
<WideEntries>
  <WideEntry>
    <WideItem>
      <PropertyName>ProcessName</PropertyName>
    </WideItem>
  </WideEntry>
</WideEntries>

```

<span data-ttu-id="af372-132">Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="af372-132">For a complete example of a wide view, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="af372-133">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="af372-133">See Also</span></span>

[<span data-ttu-id="af372-134">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="af372-134">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="af372-135">SelectionCondition eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-135">SelectionCondition Element for WideEntry (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="af372-136">SelectionSetName eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-136">SelectionSetName Element for WideEntry (Format)</span></span>](./selectionsetname-element-for-entryselectedby-for-widecontrol-format.md)

[<span data-ttu-id="af372-137">TypeName eleme WideEntry (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-137">TypeName Element for WideEntry (Format)</span></span>](./typename-element-for-entryselectedby-for-wideentry-format.md)

[<span data-ttu-id="af372-138">WideEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-138">WideEntries Element (Format)</span></span>](./wideentries-element-for-widecontrol-format.md)

[<span data-ttu-id="af372-139">WideItem elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="af372-139">WideItem Element (Format)</span></span>](./wideitem-element-for-widecontrol-format.md)

[<span data-ttu-id="af372-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="af372-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
