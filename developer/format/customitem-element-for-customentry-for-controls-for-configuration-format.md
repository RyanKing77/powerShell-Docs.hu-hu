---
title: CustomItem elemet a vezérlők (formátum) konfiguráció CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 73fb11ee-0ebd-477a-ac36-acdfbb32e70d
caps.latest.revision: 7
ms.openlocfilehash: bd0cb69770817ec215ddb1862a43a838baddefcf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066430"
---
# <a name="customitem-element-for-customentry-for-controls-for-configuration-format"></a><span data-ttu-id="5de3e-102">A Konfiguráció Vezérlők eleméhez tartozó CustomEntry CustomItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="5de3e-102">CustomItem Element for CustomEntry for Controls for Configuration (Format)</span></span>

<span data-ttu-id="5de3e-103">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="5de3e-103">Defines what data is displayed by the control and how it is displayed.</span></span> <span data-ttu-id="5de3e-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="5de3e-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="5de3e-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfigurációhoz CustomEntry Configuration (formátum) CustomItem elemhez CustomControl</span><span class="sxs-lookup"><span data-stu-id="5de3e-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration</span></span>

## <a name="syntax"></a><span data-ttu-id="5de3e-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="5de3e-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <NewLine/>
  <Text>TextToDisplay</Text>
  <Frame>...</Frame>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="5de3e-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="5de3e-107">Attributes and Elements</span></span>

<span data-ttu-id="5de3e-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="5de3e-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span> <span data-ttu-id="5de3e-109">További információkért lásd a megjegyzések.</span><span class="sxs-lookup"><span data-stu-id="5de3e-109">For more information, see Remarks.</span></span>

### <a name="attributes"></a><span data-ttu-id="5de3e-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="5de3e-110">Attributes</span></span>

<span data-ttu-id="5de3e-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="5de3e-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="5de3e-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="5de3e-112">Child Elements</span></span>

|<span data-ttu-id="5de3e-113">Elem</span><span class="sxs-lookup"><span data-stu-id="5de3e-113">Element</span></span>|<span data-ttu-id="5de3e-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="5de3e-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5de3e-115">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="5de3e-115">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="5de3e-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="5de3e-116">Optional element.</span></span><br /><br /> <span data-ttu-id="5de3e-117">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="5de3e-117">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="5de3e-118">Keret eleme CustomItem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="5de3e-118">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>](./frame-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="5de3e-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="5de3e-119">Optional element.</span></span><br /><br /> <span data-ttu-id="5de3e-120">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="5de3e-120">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|
|[<span data-ttu-id="5de3e-121">Konfiguráció (formátum) vezérlők CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="5de3e-121">NewLine Element for CustomItem for Controls for Configuration (Format)</span></span>](./newline-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="5de3e-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="5de3e-122">Optional element.</span></span><br /><br /> <span data-ttu-id="5de3e-123">Egy üres sort ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="5de3e-123">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="5de3e-124">A vezérlők (formátum) konfiguráció CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="5de3e-124">Text Element for CustomItem for Controls for Configuration (Format)</span></span>](./text-element-for-customitem-for-controls-for-configuration-format.md)|<span data-ttu-id="5de3e-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="5de3e-125">Optional element.</span></span><br /><br /> <span data-ttu-id="5de3e-126">Szöveg, például zárójelek vagy zárójelben ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="5de3e-126">Adds text, such as parentheses or brackets, to the display of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="5de3e-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="5de3e-127">Parent Elements</span></span>

|<span data-ttu-id="5de3e-128">Elem</span><span class="sxs-lookup"><span data-stu-id="5de3e-128">Element</span></span>|<span data-ttu-id="5de3e-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="5de3e-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="5de3e-130">Konfiguráció (formátum) vezérlők CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="5de3e-130">CustomEntry Element for CustomControl for Controls for Configuration (Format)</span></span>](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|<span data-ttu-id="5de3e-131">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="5de3e-131">Provides a definition of the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="5de3e-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="5de3e-132">Remarks</span></span>

<span data-ttu-id="5de3e-133">Az alárendelt elemeinek megadásakor a `CustomItem` elem, vegye figyelembe a következőket:</span><span class="sxs-lookup"><span data-stu-id="5de3e-133">When specifying the child elements of the `CustomItem` element, keep the following in mind:</span></span>

- <span data-ttu-id="5de3e-134">A gyermekelemek hozzá kell adni a következő sorrendben: `ExpressionBinding`, `NewLine`, `Text`, és `Frame`.</span><span class="sxs-lookup"><span data-stu-id="5de3e-134">The child elements must be added in the following sequence: `ExpressionBinding`, `NewLine`, `Text`, and `Frame`.</span></span>

- <span data-ttu-id="5de3e-135">Nincs maximális megadható feladatütemezések száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="5de3e-135">There is no maximum limit to the number of sequences that you can specify.</span></span>

- <span data-ttu-id="5de3e-136">Az egyes feladatütemezési nem nincs maximális számának korlátja `ExpressionBinding` elemeket, amelyeket használhat.</span><span class="sxs-lookup"><span data-stu-id="5de3e-136">In each sequence, there is no maximum limit to the number of `ExpressionBinding` elements that you can use.</span></span>

## <a name="see-also"></a><span data-ttu-id="5de3e-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="5de3e-137">See Also</span></span>

[<span data-ttu-id="5de3e-138">Konfiguráció (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="5de3e-138">ExpressionBinding Element for CustomItem for Controls for Configuration (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="5de3e-139">Keret eleme CustomItem vezérlők konfiguráció (formátum)</span><span class="sxs-lookup"><span data-stu-id="5de3e-139">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>](./frame-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="5de3e-140">Konfiguráció (formátum) vezérlők CustomItem soremelés elem.</span><span class="sxs-lookup"><span data-stu-id="5de3e-140">NewLine Element for CustomItem for Controls for Configuration (Format)</span></span>](./newline-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="5de3e-141">A vezérlők (formátum) konfiguráció CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="5de3e-141">Text Element for CustomItem for Controls for Configuration (Format)</span></span>](./text-element-for-customitem-for-controls-for-configuration-format.md)

[<span data-ttu-id="5de3e-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="5de3e-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
