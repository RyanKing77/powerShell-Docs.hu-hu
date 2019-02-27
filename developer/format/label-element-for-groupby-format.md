---
title: Címke elem a GroupBy (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3351d237-e8c2-4ec5-9500-4eceadb407c2
caps.latest.revision: 11
ms.openlocfilehash: e7158711c60d13c745bbdfab9b1b9fc7d98b34e2
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851288"
---
# <a name="label-element-for-groupby-format"></a><span data-ttu-id="28233-102">A GroupBy Címke eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="28233-102">Label Element for GroupBy (Format)</span></span>

<span data-ttu-id="28233-103">Meghatározza a felirat jelenik meg, ha egy új csoportot észlelt.</span><span class="sxs-lookup"><span data-stu-id="28233-103">Specifies a label that is displayed when a new group is encountered.</span></span>

<span data-ttu-id="28233-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) címke elem a GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="28233-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) Label Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="28233-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="28233-105">Syntax</span></span>

```xml
<Label>DisplayedLabel</Label>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="28233-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="28233-106">Attributes and Elements</span></span>

<span data-ttu-id="28233-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és szülőelemét a `Label` elemet.</span><span class="sxs-lookup"><span data-stu-id="28233-107">The following sections describe the attributes, child elements, and parent element of the `Label` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="28233-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="28233-108">Attributes</span></span>

<span data-ttu-id="28233-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="28233-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="28233-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="28233-110">Child Elements</span></span>

<span data-ttu-id="28233-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="28233-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="28233-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="28233-112">Parent Elements</span></span>

|<span data-ttu-id="28233-113">Elem</span><span class="sxs-lookup"><span data-stu-id="28233-113">Element</span></span>|<span data-ttu-id="28233-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="28233-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="28233-115">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="28233-115">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="28233-116">Határozza meg, hogyan jelenjen meg az objektumok egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="28233-116">Defines how a new group of objects is displayed.</span></span>|

## <a name="text-value"></a><span data-ttu-id="28233-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="28233-117">Text Value</span></span>

<span data-ttu-id="28233-118">Adja meg a szöveg, amelyet minden alkalommal, amikor Windows PowerShell találkozik egy új tulajdonság vagy parancsfájl érték jelenik meg.</span><span class="sxs-lookup"><span data-stu-id="28233-118">Specify the text that is displayed whenever Windows PowerShell encounters a new property or script value.</span></span>

## <a name="remarks"></a><span data-ttu-id="28233-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="28233-119">Remarks</span></span>

<span data-ttu-id="28233-120">Ez az elem által meghatározott a szöveg mellett a Windows PowerShell az új értéket, amely elindítja a csoportot, és hozzáad egy üres sort, előtt és után a csoport jeleníti meg.</span><span class="sxs-lookup"><span data-stu-id="28233-120">In addition to the text specified by this element, Windows PowerShell displays the new value that starts the group, and adds a blank line before and after the group.</span></span>

## <a name="example"></a><span data-ttu-id="28233-121">Példa</span><span class="sxs-lookup"><span data-stu-id="28233-121">Example</span></span>

<span data-ttu-id="28233-122">Az alábbi példa bemutatja egy új csoportot a címkét.</span><span class="sxs-lookup"><span data-stu-id="28233-122">The following example shows the label for a new group.</span></span> <span data-ttu-id="28233-123">A megjelenített címke ehhez hasonlóan néz ki ez: `Service Type: NewValueofProperty`</span><span class="sxs-lookup"><span data-stu-id="28233-123">The displayed label would look similar to this: `Service Type: NewValueofProperty`</span></span>

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

<span data-ttu-id="28233-124">A teljes formázási fájl tartalmazza ezt az elemet egy példa: [széles nézet (GroupBy)](./wide-view-groupby.md).</span><span class="sxs-lookup"><span data-stu-id="28233-124">For an example of a complete formatting file that includes this element, see [Wide View (GroupBy)](./wide-view-groupby.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="28233-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="28233-125">See Also</span></span>

[<span data-ttu-id="28233-126">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="28233-126">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="28233-127">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="28233-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
