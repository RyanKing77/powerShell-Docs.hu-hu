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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066413"
---
# <a name="customitem-element-for-customentry-for-customcontrol-for-view-format"></a><span data-ttu-id="9ad83-102">A Nézet CustomControl eleméhez tartozó CustomEntry CustomItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="9ad83-102">CustomItem Element for CustomEntry for CustomControl for View (Format)</span></span>

<span data-ttu-id="9ad83-103">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="9ad83-103">Defines what data is displayed by the custom control view and how it is displayed.</span></span> <span data-ttu-id="9ad83-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="9ad83-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="9ad83-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="9ad83-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="9ad83-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="9ad83-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <Frame>...</Frame>
  <NewLine/>
  <Text>TextToDisplay</Text>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="9ad83-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="9ad83-107">Attributes and Elements</span></span>

<span data-ttu-id="9ad83-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="9ad83-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="9ad83-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="9ad83-109">Attributes</span></span>

<span data-ttu-id="9ad83-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="9ad83-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="9ad83-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="9ad83-111">Child Elements</span></span>

|<span data-ttu-id="9ad83-112">Elem</span><span class="sxs-lookup"><span data-stu-id="9ad83-112">Element</span></span>|<span data-ttu-id="9ad83-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="9ad83-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="9ad83-114">A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-114">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="9ad83-115">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9ad83-115">Optional element.</span></span><br /><br /> <span data-ttu-id="9ad83-116">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="9ad83-116">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="9ad83-117">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-117">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="9ad83-118">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9ad83-118">Optional element.</span></span><br /><br /> <span data-ttu-id="9ad83-119">Határozza meg az egyéni vezérlőt a nézetben megjelenített adatok, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="9ad83-119">Defines what data is displayed by the custom control view and how it is displayed.</span></span>|
|[<span data-ttu-id="9ad83-120">Egyéni vezérlő nézet (formátum) CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-120">NewLine Element for CustomItem for Custom Control for View (Format)</span></span>](./newline-element-for-customitem-for-customcontrol-for-view-format.md)|<span data-ttu-id="9ad83-121">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9ad83-121">Optional element.</span></span><br /><br /> <span data-ttu-id="9ad83-122">Egy üres sort ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="9ad83-122">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="9ad83-123">A nézet (formátum) CustomControl CustomItem szöveg eleme</span><span class="sxs-lookup"><span data-stu-id="9ad83-123">Text Element for CustomItem for CustomControl for View (Format)</span></span>](./text-element-for-customitem-for-customview-for-view-format.md)|<span data-ttu-id="9ad83-124">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="9ad83-124">Optional element.</span></span><br /><br /> <span data-ttu-id="9ad83-125">Adja meg a rendszer további szöveget a vezérlőelem által megjelenített adatokhoz.</span><span class="sxs-lookup"><span data-stu-id="9ad83-125">Specifies additional text to the data displayed by the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="9ad83-126">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="9ad83-126">Parent Elements</span></span>

|<span data-ttu-id="9ad83-127">Elem</span><span class="sxs-lookup"><span data-stu-id="9ad83-127">Element</span></span>|<span data-ttu-id="9ad83-128">Leírás</span><span class="sxs-lookup"><span data-stu-id="9ad83-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="9ad83-129">A nézet (formátum) CustomControl CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-129">CustomEntry Element for CustomEntries for CustomControl for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)|<span data-ttu-id="9ad83-130">Az egyéni vezérlő nézet definíciójának biztosít.</span><span class="sxs-lookup"><span data-stu-id="9ad83-130">Provides a definition of the custom control view.</span></span>|

## <a name="remarks"></a><span data-ttu-id="9ad83-131">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="9ad83-131">Remarks</span></span>

## <a name="see-also"></a><span data-ttu-id="9ad83-132">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="9ad83-132">See Also</span></span>

[<span data-ttu-id="9ad83-133">A nézet (formátum) CustomEntries CustomEntry elem</span><span class="sxs-lookup"><span data-stu-id="9ad83-133">CustomEntry Element for CustomEntries for View (Format)</span></span>](./customentry-element-for-customentries-for-customcontrol-for-view-format.md)

[<span data-ttu-id="9ad83-134">A nézet (formátum) CustomControl CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-134">ExpressionBinding Element for CustomItem for CustomControl for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="9ad83-135">A nézet (formátum) CustomControl CustomItem keret elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-135">Frame Element for CustomItem for CustomControl for View (Format)</span></span>](./frame-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="9ad83-136">A nézet (formátum) CustomControl CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="9ad83-136">NewLine Element for CustomItem for CustomControl for View (Format)</span></span>](./newline-element-for-customitem-for-customcontrol-for-view-format.md)

[<span data-ttu-id="9ad83-137">A nézet (formátum) CustomControl CustomItem szöveg eleme</span><span class="sxs-lookup"><span data-stu-id="9ad83-137">Text Element for CustomItem for CustomControl for View (Format)</span></span>](./text-element-for-customitem-for-customview-for-view-format.md)

[<span data-ttu-id="9ad83-138">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="9ad83-138">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
