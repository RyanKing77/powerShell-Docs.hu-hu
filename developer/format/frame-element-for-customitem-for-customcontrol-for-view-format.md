---
title: Keretet elem számára CustomItem CustomControl a nézet (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1a13100-41a4-4847-9f07-458c85783505
caps.latest.revision: 6
ms.openlocfilehash: 925ef86e61801f5a66f89dd25e0756f00dd35155
ms.sourcegitcommit: caac7d098a448232304c9d6728e7340ec7517a71
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 03/16/2019
ms.locfileid: "58054781"
---
# <a name="frame-element-for-customitem-for-customcontrol-for-view-format"></a><span data-ttu-id="65b83-102">A Nézet CustomControl eleméhez tartozó CustomItem Keret eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="65b83-102">Frame Element for CustomItem for CustomControl for View (Format)</span></span>

<span data-ttu-id="65b83-103">Határozza meg, hogyan egy jelennek meg, például az adatok pótlása jobbra vagy balra.</span><span class="sxs-lookup"><span data-stu-id="65b83-103">Defines how the data is displayed, such as shifting the data to the left or right.</span></span> <span data-ttu-id="65b83-104">Ehhez az elemhez használt egyéni vezérlő nézet definiálása.</span><span class="sxs-lookup"><span data-stu-id="65b83-104">This element is used when defining a custom control view.</span></span>

<span data-ttu-id="65b83-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézet elem (formátum) CustomControl elem (formátum) CustomEntries eleme CustomControl megtekintése (formátum) CustomEntry elem megtekintése (formátum) CustomItem elemhez tartozó CustomEntries számára CustomEntry CustomItem CustomControl nézet (formátum) esetében a CustomControlView (formátum) keret elemhez</span><span class="sxs-lookup"><span data-stu-id="65b83-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) CustomControl Element (Format) CustomEntries Element for CustomControl for View (Format) CustomEntry Element for CustomEntries for View (Format) CustomItem Element for CustomEntry for CustomControlView (Format) Frame Element for CustomItem for CustomControl for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="65b83-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="65b83-106">Syntax</span></span>

```xml
<Frame>
  <LeftIndent>NumberOfCharactersToShift</LeftIndent>
  <RightIndent>NumberOfCharactersToShift</RightIndent>
  <FirstLineHanging>NumberOfCharactersToShift</FirstLineHanging>
  <FirstLineIndent>NumberOfCharactersToShift</FirstLineIndent>
  <CustomItem>...</CustomItem>
</Frame>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="65b83-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="65b83-107">Attributes and Elements</span></span>

<span data-ttu-id="65b83-108">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="65b83-108">The following sections describe attributes, child elements, and the parent element of the `Frame` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="65b83-109">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="65b83-109">Attributes</span></span>

<span data-ttu-id="65b83-110">Nincs.</span><span class="sxs-lookup"><span data-stu-id="65b83-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="65b83-111">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="65b83-111">Child Elements</span></span>

|<span data-ttu-id="65b83-112">Elem</span><span class="sxs-lookup"><span data-stu-id="65b83-112">Element</span></span>|<span data-ttu-id="65b83-113">Leírás</span><span class="sxs-lookup"><span data-stu-id="65b83-113">Description</span></span>|
|-------------|-----------------|
|`CustomItem Element`|<span data-ttu-id="65b83-114">Kötelező elem</span><span class="sxs-lookup"><span data-stu-id="65b83-114">Required Element</span></span>|
|[<span data-ttu-id="65b83-115">FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="65b83-115">FirstLineHanging Element</span></span>](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="65b83-116">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="65b83-116">Optional element.</span></span><br /><br /> <span data-ttu-id="65b83-117">Megadja a bal oldali adatok első sora úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="65b83-117">Specifies how many characters the first line of data is shifted to the left.</span></span>|
|[<span data-ttu-id="65b83-118">FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="65b83-118">FirstLineIndent Element</span></span>](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="65b83-119">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="65b83-119">Optional element.</span></span><br /><br /> <span data-ttu-id="65b83-120">Megadja az adatok első sorának jobb úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="65b83-120">Specifies how many characters the first line of data is shifted to the right.</span></span>|
|[<span data-ttu-id="65b83-121">LeftIndent elem</span><span class="sxs-lookup"><span data-stu-id="65b83-121">LeftIndent Element</span></span>](./leftindent-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="65b83-122">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="65b83-122">Optional element.</span></span><br /><br /> <span data-ttu-id="65b83-123">Itt adhatja meg az adatokat erről a bal oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="65b83-123">Specifies how many characters the data is shifted away from the left margin.</span></span>|
|[<span data-ttu-id="65b83-124">RightIndent elem</span><span class="sxs-lookup"><span data-stu-id="65b83-124">RightIndent Element</span></span>](./rightindent-element-for-frame-for-customcontrol-for-view-format.md)|<span data-ttu-id="65b83-125">Nem kötelező eleme.</span><span class="sxs-lookup"><span data-stu-id="65b83-125">Optional element.</span></span><br /><br /> <span data-ttu-id="65b83-126">Itt adhatja meg az adatokat erről a jobb oldali margó úgy, hogy hány karakter.</span><span class="sxs-lookup"><span data-stu-id="65b83-126">Specifies how many characters the data is shifted away from the right margin.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="65b83-127">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="65b83-127">Parent Elements</span></span>

|<span data-ttu-id="65b83-128">Elem</span><span class="sxs-lookup"><span data-stu-id="65b83-128">Element</span></span>|<span data-ttu-id="65b83-129">Leírás</span><span class="sxs-lookup"><span data-stu-id="65b83-129">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="65b83-130">A nézet (formátum) CustomEntry CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="65b83-130">CustomItem Element for CustomEntry for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)|<span data-ttu-id="65b83-131">Határozza meg a vezérlő által megjelenített adatokat, és hogyan jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="65b83-131">Defines what data is displayed by the control and how it is displayed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="65b83-132">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="65b83-132">Remarks</span></span>

<span data-ttu-id="65b83-133">Nem adható meg a [FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) és a [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) elemek ugyanazon `Frame` elemet.</span><span class="sxs-lookup"><span data-stu-id="65b83-133">You cannot specify the [FirstLineHanging](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md) and the [FirstLineIndent](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md) elements in the same `Frame` element.</span></span>

## <a name="see-also"></a><span data-ttu-id="65b83-134">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="65b83-134">See Also</span></span>

[<span data-ttu-id="65b83-135">FirstLineHanging elem</span><span class="sxs-lookup"><span data-stu-id="65b83-135">FirstLineHanging Element</span></span>](./firstlinehanging-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="65b83-136">FirstLineIndent elem</span><span class="sxs-lookup"><span data-stu-id="65b83-136">FirstLineIndent Element</span></span>](./firstlineindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="65b83-137">LeftIndent elem</span><span class="sxs-lookup"><span data-stu-id="65b83-137">LeftIndent Element</span></span>](./leftindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="65b83-138">RightIndent elem</span><span class="sxs-lookup"><span data-stu-id="65b83-138">RightIndent Element</span></span>](./rightindent-element-for-frame-for-customcontrol-for-view-format.md)

[<span data-ttu-id="65b83-139">A nézet (formátum) CustomEntry CustomItem elem</span><span class="sxs-lookup"><span data-stu-id="65b83-139">CustomItem Element for CustomEntry for View (Format)</span></span>](./customitem-element-for-customentry-for-customcontrol-for-view-format.md)

[<span data-ttu-id="65b83-140">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="65b83-140">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
