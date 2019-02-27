---
title: CustomItem elemet a vezérlők (formátum) nézet CustomEntry |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 33cb5350-73ef-4b79-a879-0edf051869e4
caps.latest.revision: 7
ms.openlocfilehash: 174ba6a14819f823ec39f72e49a626e781221d8c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56846535"
---
# <a name="customitem-element-for-customentry-for-controls-for-view-format"></a><span data-ttu-id="3cfa0-102">A Nézet Vezérlők eleméhez tartozó CustomEntry CustomItem eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="3cfa0-102">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>

<span data-ttu-id="3cfa0-103">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-103">Defines what data is displayed by the control and how it is displayed.</span></span> <span data-ttu-id="3cfa0-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="3cfa0-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők (formátum) nézet CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="3cfa0-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="3cfa0-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="3cfa0-106">Syntax</span></span>

```xml
<CustomItem>
  <ExpressionBinding>...</ExpressionBinding>
  <NewLine/>
  <Text>TextToDisplay</Text>
  <Frame>...<Frame>
</CustomItem>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="3cfa0-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="3cfa0-107">Attributes and Elements</span></span>

<span data-ttu-id="3cfa0-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `CustomItem` elemet.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-108">The following sections describe attributes, child elements, and the parent element of the `CustomItem` element.</span></span> <span data-ttu-id="3cfa0-109">További információkért lásd a megjegyzések.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-109">For more information, see Remarks.</span></span>

### <a name="attributes"></a><span data-ttu-id="3cfa0-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="3cfa0-110">Attributes</span></span>

<span data-ttu-id="3cfa0-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="3cfa0-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="3cfa0-112">Child Elements</span></span>

|<span data-ttu-id="3cfa0-113">Elem</span><span class="sxs-lookup"><span data-stu-id="3cfa0-113">Element</span></span>|<span data-ttu-id="3cfa0-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cfa0-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3cfa0-115">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-115">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="3cfa0-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-116">Optional element.</span></span><br /><br /> <span data-ttu-id="3cfa0-117">Határozza meg a vezérlő által megjelenített adatokat.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-117">Defines the data that is displayed by the control.</span></span>|
|[<span data-ttu-id="3cfa0-118">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="3cfa0-118">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="3cfa0-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-119">Optional element.</span></span><br /><br /> <span data-ttu-id="3cfa0-120">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-120">Defines how the data is displayed, such as shifting the data to the left or right.</span></span>|
|[<span data-ttu-id="3cfa0-121">Új sor eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="3cfa0-121">NewLine Element for CustomItem for Controls for View (Format)</span></span>](./newline-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="3cfa0-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-122">Optional element.</span></span><br /><br /> <span data-ttu-id="3cfa0-123">Egy üres sort ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-123">Adds a blank line to the display of the control.</span></span>|
|[<span data-ttu-id="3cfa0-124">A vezérlők (formátum) nézet CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="3cfa0-124">Text Element for CustomItem for Controls for View (Format)</span></span>](./text-element-for-customitem-for-controls-for-view-format.md)|<span data-ttu-id="3cfa0-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-125">Optional element.</span></span><br /><br /> <span data-ttu-id="3cfa0-126">Szöveg, például zárójelek vagy zárójelben ad hozzá a vezérlő megjelenését.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-126">Adds text, such as parentheses or brackets, to the display of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="3cfa0-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="3cfa0-127">Parent Elements</span></span>

|<span data-ttu-id="3cfa0-128">Elem</span><span class="sxs-lookup"><span data-stu-id="3cfa0-128">Element</span></span>|<span data-ttu-id="3cfa0-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="3cfa0-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="3cfa0-130">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-130">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)|<span data-ttu-id="3cfa0-131">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-131">Provides a definition of the control.</span></span>|

## <a name="remarks"></a><span data-ttu-id="3cfa0-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="3cfa0-132">Remarks</span></span>

<span data-ttu-id="3cfa0-133">Az alárendelt elemeinek megadásakor a `CustomItem` elem, vegye figyelembe a következőket:</span><span class="sxs-lookup"><span data-stu-id="3cfa0-133">When specifying the child elements of the `CustomItem` element, keep the following in mind:</span></span>

- <span data-ttu-id="3cfa0-134">A gyermekelemek hozzá kell adni a következő sorrendben: `ExpressionBinding`, `NewLine`, `Text`, és `Frame`.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-134">The child elements must be added in the following sequence: `ExpressionBinding`, `NewLine`, `Text`, and `Frame`.</span></span>

- <span data-ttu-id="3cfa0-135">Nincs maximális megadható feladatütemezések száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-135">There is no maximum limit to the number of sequences that you can specify.</span></span>

- <span data-ttu-id="3cfa0-136">Az egyes feladatütemezési nem nincs maximális számának korlátja `ExpressionBinding` elemeket, amelyeket használhat.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-136">In each sequence, there is no maximum limit to the number of `ExpressionBinding` elements that you can use.</span></span>

## <a name="see-also"></a><span data-ttu-id="3cfa0-137">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="3cfa0-137">See Also</span></span>

[<span data-ttu-id="3cfa0-138">Nézet (formátum) vezérlők CustomItem ExpressionBinding elem.</span><span class="sxs-lookup"><span data-stu-id="3cfa0-138">ExpressionBinding Element for CustomItem for Controls for View (Format)</span></span>](./expressionbinding-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="3cfa0-139">Keret eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="3cfa0-139">Frame Element for CustomItem for Controls for View (Format)</span></span>](./frame-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="3cfa0-140">Új sor eleme CustomItem vezérlők nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="3cfa0-140">NewLine Element for CustomItem for Controls for View (Format)</span></span>](./newline-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="3cfa0-141">A vezérlők (formátum) nézet CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="3cfa0-141">Text Element for CustomItem for Controls for View (Format)</span></span>](./text-element-for-customitem-for-controls-for-view-format.md)

[<span data-ttu-id="3cfa0-142">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="3cfa0-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
