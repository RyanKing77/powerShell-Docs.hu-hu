---
title: A GroupBy (formátum) CustomEntry CustomItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f7c517aa-24f5-41ae-b82d-cb0fac81a245
caps.latest.revision: 7
ms.openlocfilehash: 2d821f5e3bc8d0f81ef8a8a040c6f9bcb1658bee
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56847459"
---
# <a name="customitem-element-for-customentry-for-groupby-format"></a><span data-ttu-id="a7d20-102">A GroupBy CustomEntry elemének CustomItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="a7d20-102">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>

<span data-ttu-id="a7d20-103">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="a7d20-103">Defines what data is displayed by the custom control view and how it is displayed.</span></span> <span data-ttu-id="a7d20-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="a7d20-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="a7d20-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomItem elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez CustomEntry a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="a7d20-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="a7d20-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="a7d20-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <Frame>...</Frame>
  <NewLine/>
  <Text>TextToDisplay</Text>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="a7d20-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="a7d20-107">Attributes and Elements</span></span>

<span data-ttu-id="a7d20-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="a7d20-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="a7d20-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="a7d20-109">Attributes</span></span>

<span data-ttu-id="a7d20-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="a7d20-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="a7d20-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="a7d20-111">Child Elements</span></span>

|<span data-ttu-id="a7d20-112">Elem</span><span class="sxs-lookup"><span data-stu-id="a7d20-112">Element</span></span>|<span data-ttu-id="a7d20-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="a7d20-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a7d20-114">A GroupBy (formátum) CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="a7d20-114">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="a7d20-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="a7d20-115">Optional element.</span></span><br /><br /> <span data-ttu-id="a7d20-116">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="a7d20-116">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="a7d20-117">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="a7d20-117">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="a7d20-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="a7d20-118">Optional element.</span></span><br /><br /> <span data-ttu-id="a7d20-119">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="a7d20-119">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|
|[<span data-ttu-id="a7d20-120">A GroupBy (formátum) CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="a7d20-120">NewLine Element for CustomItem for GroupBy (Format)</span></span>](./newline-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="a7d20-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="a7d20-121">Optional element.</span></span><br /><br /> <span data-ttu-id="a7d20-122">Egy üres sort ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="a7d20-122">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="a7d20-123">Szöveg eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="a7d20-123">Text Element for CustomItem for GroupBy (Format)</span></span>](./text-element-for-customitem-for-groupby-format.md)|<span data-ttu-id="a7d20-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="a7d20-124">Optional element.</span></span><br /><br /> <span data-ttu-id="a7d20-125">Adja meg a rendszer további szöveget a vezérlőelem által megjelenített adatokhoz.</span><span class="sxs-lookup"><span data-stu-id="a7d20-125">Specifies additional text to the data displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="a7d20-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="a7d20-126">Parent Elements</span></span>

|<span data-ttu-id="a7d20-127">Elem</span><span class="sxs-lookup"><span data-stu-id="a7d20-127">Element</span></span>|<span data-ttu-id="a7d20-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="a7d20-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="a7d20-129">A GroupBy (formátum) CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="a7d20-129">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>](./customentry-element-for-customcontrol-for-groupby-format.md)|<span data-ttu-id="a7d20-130">Az egyéni vezérlő nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="a7d20-130">Provides a definition of the custom control view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="a7d20-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="a7d20-131">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="a7d20-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="a7d20-132">See Also</span></span>

[<span data-ttu-id="a7d20-133">A GroupBy (formátum) CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="a7d20-133">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>](./customentry-element-for-customcontrol-for-groupby-format.md)

[<span data-ttu-id="a7d20-134">A GroupBy (formátum) CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="a7d20-134">ExpressionBinding Element for CustomItem for GroupBy (Format)</span></span>](./expressionbinding-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="a7d20-135">Keret eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="a7d20-135">Frame Element for CustomItem for GroupBy (Format)</span></span>](./frame-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="a7d20-136">A GroupBy (formátum) CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="a7d20-136">NewLine Element for CustomItem for GroupBy (Format)</span></span>](./newline-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="a7d20-137">Szöveg eleme CustomItem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="a7d20-137">Text Element for CustomItem for GroupBy (Format)</span></span>](./text-element-for-customitem-for-groupby-format.md)

[<span data-ttu-id="a7d20-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="a7d20-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
