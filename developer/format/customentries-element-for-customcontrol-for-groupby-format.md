---
title: A GroupBy (formátum) CustomControl CustomEntries eleme |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: af83c0f6-7fdd-4aa0-af12-efc62f632974
caps.latest.revision: 7
ms.openlocfilehash: f073142bf836ae892f161cf8c36ed16c35e311f5
ms.sourcegitcommit: e7445ba8203da304286c591ff513900ad1c244a4
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 04/23/2019
ms.locfileid: "62066539"
---
# <a name="customentries-element-for-customcontrol-for-groupby-format"></a><span data-ttu-id="c607b-102">A GroupBy CustomControl elemének CustomEntries eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="c607b-102">CustomEntries Element for CustomControl for GroupBy (Format)</span></span>

<span data-ttu-id="c607b-103">A definíciók vezérlő biztosít.</span><span class="sxs-lookup"><span data-stu-id="c607b-103">Provides the definitions for the control.</span></span> <span data-ttu-id="c607b-104">Ez az elem szolgál, hogyan jelenjen meg az objektumok egy új csoportot meghatározásakor.</span><span class="sxs-lookup"><span data-stu-id="c607b-104">This element is used when defining how a new group of objects is displayed.</span></span>

<span data-ttu-id="c607b-105">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) CustomControl elem GroupBy (formátum) CustomEntries elemhez tartozó CustomControl a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="c607b-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) CustomControl Element for GroupBy (Format) CustomEntries Element for CustomControl for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="c607b-106">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="c607b-106">Syntax</span></span>

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="c607b-107">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="c607b-107">Attributes and Elements</span></span>

<span data-ttu-id="c607b-108">A következő szakaszok ismertetik az attribútumokat, a gyermekelemek és a szülő elemei a `CustomEntries` elemet.</span><span class="sxs-lookup"><span data-stu-id="c607b-108">The following sections describe attributes, child elements, and parent elements of the `CustomEntries` element.</span></span> <span data-ttu-id="c607b-109">Nincs maximális megadható az alárendelt elemek száma korlátozva van.</span><span class="sxs-lookup"><span data-stu-id="c607b-109">There is no maximum limit to the number of child elements that can be specified.</span></span>

### <a name="attributes"></a><span data-ttu-id="c607b-110">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="c607b-110">Attributes</span></span>

<span data-ttu-id="c607b-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="c607b-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="c607b-112">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="c607b-112">Child Elements</span></span>

|<span data-ttu-id="c607b-113">Elem</span><span class="sxs-lookup"><span data-stu-id="c607b-113">Element</span></span>|<span data-ttu-id="c607b-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="c607b-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c607b-115">A GroupBy (formátum) CustomControl CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="c607b-115">CustomEntry Element for CustomControl for GroupBy (Format)</span></span>](./customentry-element-for-customcontrol-for-groupby-format.md)|<span data-ttu-id="c607b-116">Szükséges eleme.</span><span class="sxs-lookup"><span data-stu-id="c607b-116">Required element.</span></span><br /><br /> <span data-ttu-id="c607b-117">A vezérlőelem egy definíciót tartalmaz.</span><span class="sxs-lookup"><span data-stu-id="c607b-117">Provides a definition of the control.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="c607b-118">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="c607b-118">Parent Elements</span></span>

|<span data-ttu-id="c607b-119">Elem</span><span class="sxs-lookup"><span data-stu-id="c607b-119">Element</span></span>|<span data-ttu-id="c607b-120">Leírás</span><span class="sxs-lookup"><span data-stu-id="c607b-120">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="c607b-121">GroupBy (formátum) CustomControl elem.</span><span class="sxs-lookup"><span data-stu-id="c607b-121">CustomControl Element for GroupBy (Format)</span></span>](./customcontrol-element-for-groupby-format.md)|<span data-ttu-id="c607b-122">Határozza meg az egyéni vezérlő, amely megjeleníti az új csoport.</span><span class="sxs-lookup"><span data-stu-id="c607b-122">Defines the custom control that displays the new group.</span></span>|

## <a name="remarks"></a><span data-ttu-id="c607b-123">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="c607b-123">Remarks</span></span>

<span data-ttu-id="c607b-124">A legtöbb esetben egy vezérlőelem még csak egy definíciót, amely egy megadott `CustomEntry` elemet.</span><span class="sxs-lookup"><span data-stu-id="c607b-124">In most cases, a control has only one definition, which is specified in a single `CustomEntry` element.</span></span> <span data-ttu-id="c607b-125">Azonban úgy is víc definic adja meg, ha ugyanazon vezérlő használata a különböző csoportok megjelenítéséhez.</span><span class="sxs-lookup"><span data-stu-id="c607b-125">However, it is possible to provide multiple definitions if you want to use the same control to display different groups.</span></span> <span data-ttu-id="c607b-126">Ezekben az esetekben definiálhat egy `CustomEntry` elem egy csoportra.</span><span class="sxs-lookup"><span data-stu-id="c607b-126">In those cases, you can define a `CustomEntry` element for a group.</span></span>

## <a name="see-also"></a><span data-ttu-id="c607b-127">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="c607b-127">See Also</span></span>

[<span data-ttu-id="c607b-128">Nézet (formátum) vezérlők CustomEntries CustomEntry elem.</span><span class="sxs-lookup"><span data-stu-id="c607b-128">CustomEntry Element for CustomEntries for Controls for View (Format)</span></span>](./customentry-element-for-customentries-for-controls-for-view-format.md)

[<span data-ttu-id="c607b-129">GroupBy (formátum) CustomControl elem.</span><span class="sxs-lookup"><span data-stu-id="c607b-129">CustomControl Element for GroupBy (Format)</span></span>](./customcontrol-element-for-groupby-format.md)

[<span data-ttu-id="c607b-130">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="c607b-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
