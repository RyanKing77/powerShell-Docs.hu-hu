---
title: Keretet elem számára CustomItem vezérlők (formátum) nézet |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a5729091-78a9-4bc1-abac-210bc20c6dbe
caps.latest.revision: 7
ms.openlocfilehash: f93dc20a9c5f87c14605578062b1e60f5a3d25cf
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065716"
---
# <a name="frame-element-for-customitem-for-controls-for-view-format"></a><span data-ttu-id="86c7c-102">A Nézet Vezérlők eleméhez tartozó CustomItem Keret eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="86c7c-102">Frame Element for CustomItem for Controls for View (Format)</span></span>

<span data-ttu-id="86c7c-103">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="86c7c-103">Defines how the data is displayed, such as shifting the data to the left or right.</span></span> <span data-ttu-id="86c7c-104">Ez az elem szolgál a nézet által használható vezérlők meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="86c7c-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="86c7c-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem vezérlők elem (formátum) vezérlőelem elem vezérlők, a nézet (formátum) CustomControl elem megtekintése (formátum) CustomEntries elemet a vezérlők a vezérlő A nézet (formátum) CustomEntry elem CustomEntries vezérlők, a vezérlők, a vezérlők (formátum) nézet CustomItem megtekintése (formátum) keret elemhez CustomEntry megtekintése (formátum) CustomItem elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="86c7c-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) CustomItem Element for CustomEntry for Controls for View (Format) Frame Element for CustomItem for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="86c7c-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="86c7c-106">Syntax</span></span>

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="86c7c-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="86c7c-107">Attributes and Elements</span></span>

<span data-ttu-id="86c7c-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="86c7c-108">The following sections describe attributes, child elements, and the parent element of the `Frame` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="86c7c-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="86c7c-109">Attributes</span></span>

<span data-ttu-id="86c7c-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="86c7c-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="86c7c-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="86c7c-111">Child Elements</span></span>

|<span data-ttu-id="86c7c-112">Elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-112">Element</span></span>|<span data-ttu-id="86c7c-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="86c7c-113">Description</span></span>|
|-------------|-----------------|
|`CustomItem Element`|<span data-ttu-id="86c7c-114">Kötelező elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-114">Required Element</span></span>|
|[<span data-ttu-id="86c7c-115">Keret (formátum) nézet vezérlők FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-115">FirstLineHanging Element of Frame of Controls of View (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-view-format.md)|<span data-ttu-id="86c7c-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="86c7c-116">Optional element.</span></span><br /><br /> <span data-ttu-id="86c7c-117">Itt adhatja meg az első sor a bal oldali úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="86c7c-117">Specifies how many characters the first line is shifted to the left.</span></span>|
|[<span data-ttu-id="86c7c-118">Keret (formátum) nézet vezérlők FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-118">FirstLineIndent Element of Frame of Controls of View (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-view-format.md)|<span data-ttu-id="86c7c-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="86c7c-119">Optional element.</span></span><br /><br /> <span data-ttu-id="86c7c-120">Itt adhatja meg az első sor jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="86c7c-120">Specifies how many characters the first line is shifted to the right.</span></span>|
|[<span data-ttu-id="86c7c-121">Keret (formátum) nézet vezérlők LeftIndent elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-121">LeftIndent Element of Frame of Controls of View (Format)</span></span>](./leftindent-element-for-frame-for-controls-for-view-format.md)|<span data-ttu-id="86c7c-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="86c7c-122">Optional element.</span></span><br /><br /> <span data-ttu-id="86c7c-123">Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="86c7c-123">Specifies how many characters the data is shifted away from the left margin.</span></span>|
|[<span data-ttu-id="86c7c-124">Keret (formátum) nézet vezérlők RightIndent elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-124">RightIndent Element of Frame of Controls of View (Format)</span></span>](./rightindent-element-for-frame-for-controls-for-view-format.md)|<span data-ttu-id="86c7c-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="86c7c-125">Optional element.</span></span><br /><br /> <span data-ttu-id="86c7c-126">Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="86c7c-126">Specifies how many characters the data is shifted away from the right margin.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="86c7c-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="86c7c-127">Parent Elements</span></span>

|<span data-ttu-id="86c7c-128">Elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-128">Element</span></span>|<span data-ttu-id="86c7c-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="86c7c-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="86c7c-130">Nézet (formátum) vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="86c7c-130">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>](./customitem-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="86c7c-131">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="86c7c-131">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="86c7c-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="86c7c-132">Remarks</span></span>

<span data-ttu-id="86c7c-133">Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md) elemek ugyanazon `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="86c7c-133">You cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-controls-for-view-format.md) and the [FirstLineIndent](./firstlineindent-element-for-frame-for-controls-for-view-format.md) elements in the same `Frame` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="86c7c-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="86c7c-134">See Also</span></span>

[<span data-ttu-id="86c7c-135">Keret (formátum) nézet vezérlők FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-135">FirstLineHanging Element of Frame of Controls of View (Format)</span></span>](./firstlinehanging-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="86c7c-136">Keret (formátum) nézet vezérlők FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-136">FirstLineIndent Element of Frame of Controls of View (Format)</span></span>](./firstlineindent-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="86c7c-137">Keret (formátum) nézet vezérlők LeftIndent elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-137">LeftIndent Element of Frame of Controls of View (Format)</span></span>](./leftindent-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="86c7c-138">Keret (formátum) nézet vezérlők RightIndent elem</span><span class="sxs-lookup"><span data-stu-id="86c7c-138">RightIndent Element of Frame of Controls of View (Format)</span></span>](./rightindent-element-for-frame-for-controls-for-view-format.md)

[<span data-ttu-id="86c7c-139">Nézet (formátum) vezérlők CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="86c7c-139">CustomItem Element for CustomEntry for Controls for View (Format)</span></span>](./customitem-element-for-customentry-for-controls-for-view-format.md)

[<span data-ttu-id="86c7c-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="86c7c-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
