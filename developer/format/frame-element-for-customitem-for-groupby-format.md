---
title: Elem keretet CustomItem számára a GroupBy (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab2a5379-299d-4c97-86a2-b639ea890fae
caps.latest.revision: 6
ms.openlocfilehash: 7f9066c0fe0954fadff9dc8f0c35a62c6710f516
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62065597"
---
# <a name="frame-element-for-customitem-for-groupby-format"></a><span data-ttu-id="0d3c5-102">A GroupBy elemhez tartozó CustomItem Keret eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="0d3c5-102">Frame Element for CustomItem for GroupBy (Format)</span></span>

<span data-ttu-id="0d3c5-103">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-103">Defines how the data is displayed, such as shifting the data to the left or right.</span></span> <span data-ttu-id="0d3c5-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="0d3c5-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem a GroupBy (formátum) CustomEntry elemhez tartozó CustomControl GroupBy (formátum) CustomEntries elemhez GroupBy (formátum) CustomItem elem CustomEntry CustomItem GroupBy (formátum) esetében a GroupBy (formátum) keret elemhez tartozó CustomControl</span><span class="sxs-lookup"><span data-stu-id="0d3c5-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format) CustomEntry Element for CustomControl for GroupBy (Format) CustomItem Element for CustomEntry for GroupBy (Format) Frame Element for CustomItem for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="0d3c5-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="0d3c5-106">Syntax</span></span>

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="0d3c5-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="0d3c5-107">Attributes and Elements</span></span>

<span data-ttu-id="0d3c5-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-108">The following sections describe attributes, child elements, and the parent element of the `Frame` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="0d3c5-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="0d3c5-109">Attributes</span></span>

<span data-ttu-id="0d3c5-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="0d3c5-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="0d3c5-111">Child Elements</span></span>

|<span data-ttu-id="0d3c5-112">Elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-112">Element</span></span>|<span data-ttu-id="0d3c5-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="0d3c5-113">Description</span></span>|
|-------------|-----------------|
|`CustomItem Element`|<span data-ttu-id="0d3c5-114">Kötelező elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-114">Required Element</span></span>|
|[<span data-ttu-id="0d3c5-115">GroupBy (formátum)-keret FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-115">FirstLineHanging Element for Frame for GroupBy (Format)</span></span>](./firstlinehanging-element-for-frame-for-groupby-format.md)|<span data-ttu-id="0d3c5-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-116">Optional element.</span></span><br /><br /> <span data-ttu-id="0d3c5-117">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-117">Specifies how many characters the first line of data is shifted to the left.</span></span>|
|[<span data-ttu-id="0d3c5-118">GroupBy (formátum)-keret FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-118">FirstLineIndent Element for Frame for GroupBy (Format)</span></span>](./firstlineindent-element-for-frame-for-groupby-format.md)|<span data-ttu-id="0d3c5-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-119">Optional element.</span></span><br /><br /> <span data-ttu-id="0d3c5-120">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-120">Specifies how many characters the first line of data is shifted to the right.</span></span>|
|[<span data-ttu-id="0d3c5-121">GroupBy (formátum)-keret LeftIndent elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-121">LeftIndent Element for Frame for GroupBy (Format)</span></span>](./leftindent-element-for-frame-for-groupby-format.md)|<span data-ttu-id="0d3c5-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-122">Optional element.</span></span><br /><br /> <span data-ttu-id="0d3c5-123">Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-123">Specifies how many characters the data is shifted away from the left margin.</span></span>|
|<span data-ttu-id="0d3c5-124">[GroupBy (formátum)-keret RightIndent elem](./rightindent-element-for-frame-for-groupby-format.md)RightIndent elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-124">[RightIndent Element for Frame for GroupBy (Format)](./rightindent-element-for-frame-for-groupby-format.md)RightIndent Element</span></span>|<span data-ttu-id="0d3c5-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-125">Optional element.</span></span><br /><br /> <span data-ttu-id="0d3c5-126">Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-126">Specifies how many characters the data is shifted away from the right margin.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="0d3c5-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="0d3c5-127">Parent Elements</span></span>

|<span data-ttu-id="0d3c5-128">Elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-128">Element</span></span>|<span data-ttu-id="0d3c5-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="0d3c5-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="0d3c5-130">A GroupBy (formátum) CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-130">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>](./customitem-element-for-customentry-for-groupby-format.md)|<span data-ttu-id="0d3c5-131">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-131">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="0d3c5-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="0d3c5-132">Remarks</span></span>

<span data-ttu-id="0d3c5-133">Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-groupby-format.md) elemek ugyanazon `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-133">You cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-groupby-format.md) and the [FirstLineIndent](./firstlineindent-element-for-frame-for-groupby-format.md) elements in the same `Frame` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="0d3c5-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="0d3c5-134">See Also</span></span>

[<span data-ttu-id="0d3c5-135">GroupBy (formátum)-keret FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-135">FirstLineHanging Element for Frame for GroupBy (Format)</span></span>](./firstlinehanging-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="0d3c5-136">GroupBy (formátum)-keret FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-136">FirstLineIndent Element for Frame for GroupBy (Format)</span></span>](./firstlineindent-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="0d3c5-137">GroupBy (formátum)-keret LeftIndent elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-137">LeftIndent Element for Frame for GroupBy (Format)</span></span>](./leftindent-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="0d3c5-138">GroupBy (formátum)-keret RightIndent elem</span><span class="sxs-lookup"><span data-stu-id="0d3c5-138">RightIndent Element for Frame for GroupBy (Format)</span></span>](./rightindent-element-for-frame-for-groupby-format.md)

[<span data-ttu-id="0d3c5-139">A GroupBy (formátum) CustomEntry CustomItem elem.</span><span class="sxs-lookup"><span data-stu-id="0d3c5-139">CustomItem Element for CustomEntry for GroupBy (Format)</span></span>](./customitem-element-for-customentry-for-groupby-format.md)

[<span data-ttu-id="0d3c5-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="0d3c5-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
