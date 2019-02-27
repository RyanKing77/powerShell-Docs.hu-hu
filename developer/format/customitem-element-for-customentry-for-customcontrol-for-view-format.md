---
title: A nézet (formátum) CustomControl CustomEntry CustomItem eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98708c1d-6f39-4a76-b454-31153a6ade8c
caps.latest.revision: 12
ms.openlocfilehash: 3c110bd5fe3ef2f790ef136556afa7c29d0b5b29
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846941"
---
# <a name="customitem-element-for-customentry-for-customcontrol-for-view-format"></a><span data-ttu-id="91ee1-102">A Nézet CustomControl eleméhez tartozó CustomEntry CustomItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="91ee1-102">CustomItem Element for CustomEntry for CustomControl for View (Format)</span></span>

<span data-ttu-id="91ee1-103">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="91ee1-103">Defines what data is displayed by the custom control view and how it is displayed.</span></span> <span data-ttu-id="91ee1-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="91ee1-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="91ee1-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="91ee1-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="91ee1-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="91ee1-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <Frame>...</Frame>
  <NewLine/>
  <Text>TextToDisplay</Text>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="91ee1-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="91ee1-107">Attributes and Elements</span></span>

<span data-ttu-id="91ee1-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="91ee1-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="91ee1-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="91ee1-109">Attributes</span></span>

<span data-ttu-id="91ee1-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="91ee1-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="91ee1-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="91ee1-111">Child Elements</span></span>

|<span data-ttu-id="91ee1-112">Elem</span><span class="sxs-lookup"><span data-stu-id="91ee1-112">Element</span></span>|<span data-ttu-id="91ee1-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="91ee1-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="91ee1-114">A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-114">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="91ee1-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="91ee1-115">Optional element.</span></span><br /><br /> <span data-ttu-id="91ee1-116">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="91ee1-116">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="91ee1-117">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-117">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="91ee1-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="91ee1-118">Optional element.</span></span><br /><br /> <span data-ttu-id="91ee1-119">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="91ee1-119">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|
|[<span data-ttu-id="91ee1-120">Egyéni vezérlő nézet (formátum) CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-120">NewLine Element for CustomItem for Custom Control for View (Format)</span></span>](./newline-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="91ee1-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="91ee1-121">Optional element.</span></span><br /><br /> <span data-ttu-id="91ee1-122">Egy üres sort ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="91ee1-122">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="91ee1-123">A nézet (formátum) CustomControl CustomItem szöveg eleme</span><span class="sxs-lookup"><span data-stu-id="91ee1-123">Text Element for CustomItem for CustomControl for View (Format)</span></span>](./text-element-for-customitem-for-customview-for-view-format.md)|<span data-ttu-id="91ee1-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="91ee1-124">Optional element.</span></span><br /><br /> <span data-ttu-id="91ee1-125">Adja meg a rendszer további szöveget a vezérlőelem által megjelenített adatokhoz.</span><span class="sxs-lookup"><span data-stu-id="91ee1-125">Specifies additional text to the data displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="91ee1-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="91ee1-126">Parent Elements</span></span>

|<span data-ttu-id="91ee1-127">Elem</span><span class="sxs-lookup"><span data-stu-id="91ee1-127">Element</span></span>|<span data-ttu-id="91ee1-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="91ee1-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="91ee1-129">A nézet (formátum) CustomControl CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-129">CustomEntry Element for CustomEntries for CustomControl for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|<span data-ttu-id="91ee1-130">Az egyéni vezérlő nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="91ee1-130">Provides a definition of the custom control view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="91ee1-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="91ee1-131">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="91ee1-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="91ee1-132">See Also</span></span>

[<span data-ttu-id="91ee1-133">A nézet (formátum) CustomEntries CustomEntry elem</span><span class="sxs-lookup"><span data-stu-id="91ee1-133">CustomEntry Element for CustomEntries for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[<span data-ttu-id="91ee1-134">A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-134">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="91ee1-135">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-135">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="91ee1-136">A nézet (formátum) CustomControl CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="91ee1-136">NewLine Element for CustomItem for CustomControl for View (Format)</span></span>](./newline-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="91ee1-137">A nézet (formátum) CustomControl CustomItem szöveg eleme</span><span class="sxs-lookup"><span data-stu-id="91ee1-137">Text Element for CustomItem for CustomControl for View (Format)</span></span>](./text-element-for-customitem-for-customview-for-view-format.md)

[<span data-ttu-id="91ee1-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="91ee1-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
