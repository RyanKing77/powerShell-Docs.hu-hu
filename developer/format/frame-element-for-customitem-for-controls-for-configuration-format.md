---
title: Keretet elem számára CustomItem vezérlők (formátum) a konfigurációhoz |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d879c8ce-679d-4622-bc43-c207f6413871
caps.latest.revision: 9
ms.openlocfilehash: b11b154a94daccead57bdfb5e579e1de2c190c09
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851694"
---
# <a name="frame-element-for-customitem-for-controls-for-configuration-format"></a><span data-ttu-id="d76b5-102">A Konfiguráció Vezérlők eleméhez tartozó CustomItem Keret eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="d76b5-102">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>

<span data-ttu-id="d76b5-103">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="d76b5-103">Defines how the data is displayed, such as shifting the data to the left or right.</span></span> <span data-ttu-id="d76b5-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="d76b5-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="d76b5-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció keret elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl</span><span class="sxs-lookup"><span data-stu-id="d76b5-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration Frame Element for CustomItem for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="d76b5-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="d76b5-106">Syntax</span></span>

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="d76b5-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="d76b5-107">Attributes and Elements</span></span>

<span data-ttu-id="d76b5-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="d76b5-108">The following sections describe attributes, child elements, and the parent element of the `Frame` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="d76b5-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="d76b5-109">Attributes</span></span>

<span data-ttu-id="d76b5-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="d76b5-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="d76b5-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="d76b5-111">Child Elements</span></span>

|<span data-ttu-id="d76b5-112">Elem</span><span class="sxs-lookup"><span data-stu-id="d76b5-112">Element</span></span>|<span data-ttu-id="d76b5-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="d76b5-113">Description</span></span>|
|-------------|-----------------|
|`CustomItem Element`|<span data-ttu-id="d76b5-114">Kötelező elem</span><span class="sxs-lookup"><span data-stu-id="d76b5-114">Required Element</span></span>|
|[<span data-ttu-id="d76b5-115">Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-115">FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="d76b5-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d76b5-116">Optional element.</span></span><br /><br /> <span data-ttu-id="d76b5-117">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="d76b5-117">Specifies how many characters the first line of data is shifted to the left.</span></span>|
|[<span data-ttu-id="d76b5-118">Keret (formátum) konfiguráció vezérlők FirstLineIndent elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-118">FirstLineIndent Element for Frame for Controls for Configuration (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="d76b5-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d76b5-119">Optional element.</span></span><br /><br /> <span data-ttu-id="d76b5-120">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="d76b5-120">Specifies how many characters the first line of data is shifted to the right.</span></span>|
|[<span data-ttu-id="d76b5-121">Keret (formátum) konfiguráció vezérlők LeftIndent elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-121">LeftIndent Element for Frame for Controls for Configuration (Format)</span></span>](./leftindent-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="d76b5-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d76b5-122">Optional element.</span></span><br /><br /> <span data-ttu-id="d76b5-123">Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="d76b5-123">Specifies how many characters the data is shifted away from the left margin.</span></span>|
|[<span data-ttu-id="d76b5-124">Keret (formátum) konfiguráció vezérlők RightIndent elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-124">RightIndent Element for Frame for Controls for Configuration (Format)</span></span>](./rightindent-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="d76b5-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="d76b5-125">Optional element.</span></span><br /><br /> <span data-ttu-id="d76b5-126">Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="d76b5-126">Specifies how many characters the data is shifted away from the right margin.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="d76b5-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="d76b5-127">Parent Elements</span></span>

|<span data-ttu-id="d76b5-128">Elem</span><span class="sxs-lookup"><span data-stu-id="d76b5-128">Element</span></span>|<span data-ttu-id="d76b5-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="d76b5-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="d76b5-130">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-130">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="d76b5-131">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="d76b5-131">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="d76b5-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="d76b5-132">Remarks</span></span>

<span data-ttu-id="d76b5-133">Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md) elemek ugyanazon `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="d76b5-133">You cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) and the [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md) elements in the same `Frame` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="d76b5-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="d76b5-134">See Also</span></span>

[<span data-ttu-id="d76b5-135">Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-135">FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="d76b5-136">Keret (formátum) konfiguráció vezérlők FirstLineIndent elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-136">FirstLineIndent Element for Frame for Controls for Configuration (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="d76b5-137">Keret (formátum) konfiguráció vezérlők LeftIndent elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-137">LeftIndent Element for Frame for Controls for Configuration (Format)</span></span>](./leftindent-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="d76b5-138">Keret (formátum) konfiguráció vezérlők RightIndent elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-138">RightIndent Element for Frame for Controls for Configuration (Format)</span></span>](./rightindent-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="d76b5-139">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="d76b5-139">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="d76b5-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="d76b5-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
