---
title: (Formátum) WideControl WideEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0c4bff45-0960-4b3a-95e7-47f2cee03ac5
caps.latest.revision: 12
ms.openlocfilehash: 083f3c8df8136858e32778ed231943ef983e47aa
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62083688"
---
# <a name="wideentries-element-for-widecontrol-format"></a><span data-ttu-id="bbc4d-102">A WideControl WideEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="bbc4d-102">WideEntries Element for WideControl (Format)</span></span>

<span data-ttu-id="bbc4d-103">A széles nézet a definíciókat tartalmazza.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-103">Provides the definitions of the wide view.</span></span> <span data-ttu-id="bbc4d-104">A széles nézet meg kell adnia egy vagy több definíciót.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-104">The wide view must specify one or more definitions.</span></span>

<span data-ttu-id="bbc4d-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem WideControl elem (formátum) WideEntries elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bbc4d-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) WideControl Element (Format) WideEntries Element (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="bbc4d-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="bbc4d-106">Syntax</span></span>

```xml
<WideEntries>
  <WideEntry>...</WideEntry>
</WideEntries>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="bbc4d-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="bbc4d-107">Attributes and Elements</span></span>

<span data-ttu-id="bbc4d-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `WideEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-108">The following sections describe the attributes, child elements, and parent element of the `WideEntries` element.</span></span> <span data-ttu-id="bbc4d-109">Meg kell adni legalább egy gyermekelemet.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-109">At least one child element must be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="bbc4d-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="bbc4d-110">Attributes</span></span>

<span data-ttu-id="bbc4d-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="bbc4d-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="bbc4d-112">Child Elements</span></span>

|<span data-ttu-id="bbc4d-113">Elem</span><span class="sxs-lookup"><span data-stu-id="bbc4d-113">Element</span></span>|<span data-ttu-id="bbc4d-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="bbc4d-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bbc4d-115">WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bbc4d-115">WideEntry Element (Format)</span></span>](./wideentry-element-for-widecontrol-format.md)|<span data-ttu-id="bbc4d-116">A széles nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-116">Provides a definition of the wide view.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="bbc4d-117">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="bbc4d-117">Parent Elements</span></span>

|<span data-ttu-id="bbc4d-118">Elem</span><span class="sxs-lookup"><span data-stu-id="bbc4d-118">Element</span></span>|<span data-ttu-id="bbc4d-119">Leírás</span><span class="sxs-lookup"><span data-stu-id="bbc4d-119">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="bbc4d-120">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bbc4d-120">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)|<span data-ttu-id="bbc4d-121">A wide (egyetlen érték) határozza meg a Nézet formátuma.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-121">Defines a wide (single value) list format for the view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="bbc4d-122">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="bbc4d-122">Remarks</span></span>

<span data-ttu-id="bbc4d-123">A széles nézet olyan egyetlen tulajdonság értékét vagy az egyes objektumok parancsfájlérték megjelenítő lista formájában.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-123">A wide view is a list format that displays a single property value or script value for each object.</span></span> <span data-ttu-id="bbc4d-124">Egy széles nézet az összetevőivel kapcsolatos további információkért lásd: [széles nézet összetevők](./creating-a-wide-view.md).</span><span class="sxs-lookup"><span data-stu-id="bbc4d-124">For more information about the components of a wide view, see [Wide View Components](./creating-a-wide-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="bbc4d-125">Példa</span><span class="sxs-lookup"><span data-stu-id="bbc4d-125">Example</span></span>

<span data-ttu-id="bbc4d-126">A következő példa bemutatja egy `WideEntries` elem, amely meghatározza egy `WideEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-126">The following example shows a `WideEntries` element that defines a single `WideEntry` element.</span></span> <span data-ttu-id="bbc4d-127">A `WideEntry` elem tartalmazza egyetlen `WideItem` elem, amely meghatározza, milyen tulajdonság, vagy parancsprogram érték jelenik meg a nézetben.</span><span class="sxs-lookup"><span data-stu-id="bbc4d-127">The `WideEntry` element contains a single `WideItem` element that defines what property or script value is displayed in the view.</span></span>

```xml
<WideControl>
  <WideEntries>
    <WideEntry>
      <WideItem>...</WideItem>
    <WideEntry>
  </WideEntries>
</WideControl>
```

<span data-ttu-id="bbc4d-128">Egy széles nézet egy teljes példa: [széles nézet (alapszintű)](./wide-view-basic.md).</span><span class="sxs-lookup"><span data-stu-id="bbc4d-128">For a complete example of a wide view, see [Wide View (Basic)](./wide-view-basic.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="bbc4d-129">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="bbc4d-129">See Also</span></span>

[<span data-ttu-id="bbc4d-130">Egy széles nézet létrehozása</span><span class="sxs-lookup"><span data-stu-id="bbc4d-130">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="bbc4d-131">WideControl elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bbc4d-131">WideControl Element (Format)</span></span>](./widecontrol-element-format.md)

[<span data-ttu-id="bbc4d-132">WideEntry elem (formátum)</span><span class="sxs-lookup"><span data-stu-id="bbc4d-132">WideEntry Element (Format)</span></span>](./wideentry-element-for-widecontrol-format.md)

[<span data-ttu-id="bbc4d-133">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="bbc4d-133">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
