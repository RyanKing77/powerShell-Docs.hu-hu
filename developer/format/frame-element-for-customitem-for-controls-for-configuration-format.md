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
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065563"
---
# <a name="frame-element-for-customitem-for-controls-for-configuration-format"></a><span data-ttu-id="4f257-102">A Konfiguráció Vezérlők eleméhez tartozó CustomItem Keret eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="4f257-102">Frame Element for CustomItem for Controls for Configuration (Format)</span></span>

<span data-ttu-id="4f257-103">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="4f257-103">Defines how the data is displayed, such as shifting the data to the left or right.</span></span> <span data-ttu-id="4f257-104">Ez az elem szolgál egy közös vezérlőelem a formázási fájlban az összes nézetek által használható meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="4f257-104">This element is used when defining a common control that can be used by all the views in the formatting file.</span></span>

<span data-ttu-id="4f257-105">Konfigurációs elem (formátum) vezérlők elem Configuration (formátum) vezérlőelem elem vezérlők, a vezérlő konfigurációs (formátum) CustomEntries elemhez tartozó CustomControl Configuration (a Configuration (formátum) CustomControl elem Formátum) CustomEntry elemet a vezérlők, a vezérlők, a konfiguráció keret elem CustomItem vezérlők (formátum) konfiguráció esetén a CustomEntry Configuration (formátum) CustomItem elemhez CustomControl</span><span class="sxs-lookup"><span data-stu-id="4f257-105">Configuration Element (Format) Controls Element of Configuration (Format) Control Element for Controls for Configuration (Format) CustomControl Element for Control for Configuration (Format) CustomEntries Element for CustomControl for Configuration (Format) CustomEntry Element for CustomControl for Controls for Configuration (Format) CustomItem Element for CustomEntry for Controls for Configuration Frame Element for CustomItem for Controls for Configuration (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="4f257-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="4f257-106">Syntax</span></span>

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="4f257-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="4f257-107">Attributes and Elements</span></span>

<span data-ttu-id="4f257-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="4f257-108">The following sections describe attributes, child elements, and the parent element of the `Frame` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="4f257-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="4f257-109">Attributes</span></span>

<span data-ttu-id="4f257-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="4f257-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="4f257-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="4f257-111">Child Elements</span></span>

|<span data-ttu-id="4f257-112">Elem</span><span class="sxs-lookup"><span data-stu-id="4f257-112">Element</span></span>|<span data-ttu-id="4f257-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="4f257-113">Description</span></span>|
|-------------|-----------------|
|`CustomItem Element`|<span data-ttu-id="4f257-114">Kötelező elem</span><span class="sxs-lookup"><span data-stu-id="4f257-114">Required Element</span></span>|
|[<span data-ttu-id="4f257-115">Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-115">FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="4f257-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4f257-116">Optional element.</span></span><br /><br /> <span data-ttu-id="4f257-117">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="4f257-117">Specifies how many characters the first line of data is shifted to the left.</span></span>|
|[<span data-ttu-id="4f257-118">Keret (formátum) konfiguráció vezérlők FirstLineIndent elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-118">FirstLineIndent Element for Frame for Controls for Configuration (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="4f257-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4f257-119">Optional element.</span></span><br /><br /> <span data-ttu-id="4f257-120">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="4f257-120">Specifies how many characters the first line of data is shifted to the right.</span></span>|
|[<span data-ttu-id="4f257-121">Keret (formátum) konfiguráció vezérlők LeftIndent elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-121">LeftIndent Element for Frame for Controls for Configuration (Format)</span></span>](./leftindent-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="4f257-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4f257-122">Optional element.</span></span><br /><br /> <span data-ttu-id="4f257-123">Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="4f257-123">Specifies how many characters the data is shifted away from the left margin.</span></span>|
|[<span data-ttu-id="4f257-124">Keret (formátum) konfiguráció vezérlők RightIndent elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-124">RightIndent Element for Frame for Controls for Configuration (Format)</span></span>](./rightindent-element-for-frame-for-controls-for-configuration-format.md)|<span data-ttu-id="4f257-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="4f257-125">Optional element.</span></span><br /><br /> <span data-ttu-id="4f257-126">Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="4f257-126">Specifies how many characters the data is shifted away from the right margin.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="4f257-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="4f257-127">Parent Elements</span></span>

|<span data-ttu-id="4f257-128">Elem</span><span class="sxs-lookup"><span data-stu-id="4f257-128">Element</span></span>|<span data-ttu-id="4f257-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="4f257-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="4f257-130">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-130">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)|<span data-ttu-id="4f257-131">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="4f257-131">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="4f257-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="4f257-132">Remarks</span></span>

<span data-ttu-id="4f257-133">Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md) elemek ugyanazon `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="4f257-133">You cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md) and the [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md) elements in the same `Frame` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="4f257-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="4f257-134">See Also</span></span>

[<span data-ttu-id="4f257-135">Keret (formátum) konfiguráció vezérlők FirstLineHanging elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-135">FirstLineHanging Element for Frame for Controls for Configuration (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="4f257-136">Keret (formátum) konfiguráció vezérlők FirstLineIndent elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-136">FirstLineIndent Element for Frame for Controls for Configuration (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="4f257-137">Keret (formátum) konfiguráció vezérlők LeftIndent elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-137">LeftIndent Element for Frame for Controls for Configuration (Format)</span></span>](./leftindent-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="4f257-138">Keret (formátum) konfiguráció vezérlők RightIndent elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-138">RightIndent Element for Frame for Controls for Configuration (Format)</span></span>](./rightindent-element-for-frame-for-controls-for-configuration-format.md)

[<span data-ttu-id="4f257-139">Konfiguráció vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="4f257-139">CustomItem Element for CustomEntry for Controls for Configuration</span></span>](./customitem-element-for-customentry-for-controls-for-configuration-format.md)

[<span data-ttu-id="4f257-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="4f257-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
