---
title: A PropertyName elemet a GroupBy (formátum) |} A Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ddcecc46-ac75-43fa-b03a-802a68524ec3
caps.latest.revision: 10
ms.openlocfilehash: da6ac5abe7acbbee8f57b3e81529664f81800b86
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: hu-HU
ms.lasthandoff: 02/03/2019
ms.locfileid: "56851897"
---
# <a name="propertyname-element-for-groupby-format"></a><span data-ttu-id="393a4-102">A GroupBy PropertyName eleme (Formátum)</span><span class="sxs-lookup"><span data-stu-id="393a4-102">PropertyName Element for GroupBy (Format)</span></span>

<span data-ttu-id="393a4-103">Megadja a .NET-tulajdonságot, amely elindít egy új csoportot, amikor annak értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="393a4-103">Specifies the .NET property that starts a new group whenever its value changes.</span></span>

<span data-ttu-id="393a4-104">Konfigurációs elem (formátum) ViewDefinitions elem (formátum) nézetben (formátum) elem GroupBy elem megtekintése (formátum) PropertyName elemhez tartozó GroupBy (formátum)</span><span class="sxs-lookup"><span data-stu-id="393a4-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) PropertyName Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="393a4-105">Szintaxis</span><span class="sxs-lookup"><span data-stu-id="393a4-105">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="393a4-106">Attribútumok és elemek</span><span class="sxs-lookup"><span data-stu-id="393a4-106">Attributes and Elements</span></span>

<span data-ttu-id="393a4-107">A következő szakaszok ismertetik az attribútumokat, gyermekelemek és a fölérendelt eleme a `PropertyName` elemet.</span><span class="sxs-lookup"><span data-stu-id="393a4-107">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="393a4-108">Attribútumok</span><span class="sxs-lookup"><span data-stu-id="393a4-108">Attributes</span></span>

<span data-ttu-id="393a4-109">Nincs.</span><span class="sxs-lookup"><span data-stu-id="393a4-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="393a4-110">Gyermekelemek</span><span class="sxs-lookup"><span data-stu-id="393a4-110">Child Elements</span></span>

<span data-ttu-id="393a4-111">Nincs.</span><span class="sxs-lookup"><span data-stu-id="393a4-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="393a4-112">Szülőelemek</span><span class="sxs-lookup"><span data-stu-id="393a4-112">Parent Elements</span></span>

|<span data-ttu-id="393a4-113">Elem</span><span class="sxs-lookup"><span data-stu-id="393a4-113">Element</span></span>|<span data-ttu-id="393a4-114">Leírás</span><span class="sxs-lookup"><span data-stu-id="393a4-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="393a4-115">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="393a4-115">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="393a4-116">Határozza meg, hogyan jelenjen meg a .NET-objektumokká csoportja.</span><span class="sxs-lookup"><span data-stu-id="393a4-116">Defines how a group of .NET objects is displayed.</span></span>|

## <a name="text-value"></a><span data-ttu-id="393a4-117">Szöveges érték</span><span class="sxs-lookup"><span data-stu-id="393a4-117">Text Value</span></span>

<span data-ttu-id="393a4-118">Adja meg a .NET-tulajdonság neve.</span><span class="sxs-lookup"><span data-stu-id="393a4-118">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="393a4-119">Megjegyzés</span><span class="sxs-lookup"><span data-stu-id="393a4-119">Remarks</span></span>

<span data-ttu-id="393a4-120">Windows PowerShell elindul egy új csoportot, ha a ennek a tulajdonságnak az értéke módosul.</span><span class="sxs-lookup"><span data-stu-id="393a4-120">Windows PowerShell starts a new group whenever the value of this property changes.</span></span>

<span data-ttu-id="393a4-121">Ha ez az elem meg van adva, nem adható meg a [ScriptBlock](./scriptblock-element-for-groupby-format.md) elem elindítani egy új csoportot.</span><span class="sxs-lookup"><span data-stu-id="393a4-121">When this element is specified, you cannot specify the [ScriptBlock](./scriptblock-element-for-groupby-format.md) element to start a new group.</span></span>

## <a name="example"></a><span data-ttu-id="393a4-122">Példa</span><span class="sxs-lookup"><span data-stu-id="393a4-122">Example</span></span>

<span data-ttu-id="393a4-123">Az alábbi példa bemutatja, hogyan indítható egy új csoportot, ha egy tulajdonság értékét módosítja.</span><span class="sxs-lookup"><span data-stu-id="393a4-123">The following example shows how to start a new group when the value of a property changes.</span></span>

```xml
<GroupBy>
  <Label>Service Type</Label>
  <PropertyName>ServiceType</PropertyName>
</GroupBy>

```

<span data-ttu-id="393a4-124">A teljes formázási fájl tartalmazza ezt az elemet egy példa: [széles nézet (GroupBy)](./wide-view-groupby.md).</span><span class="sxs-lookup"><span data-stu-id="393a4-124">For an example of a complete formatting file that includes this element, see [Wide View (GroupBy)](./wide-view-groupby.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="393a4-125">Lásd még:</span><span class="sxs-lookup"><span data-stu-id="393a4-125">See Also</span></span>

[<span data-ttu-id="393a4-126">GroupBy elem nézet (formátum)</span><span class="sxs-lookup"><span data-stu-id="393a4-126">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="393a4-127">GroupBy (formátum) a scriptblock kulcsszót elem</span><span class="sxs-lookup"><span data-stu-id="393a4-127">ScriptBlock Element for GroupBy (Format)</span></span>](./scriptblock-element-for-groupby-format.md)

[<span data-ttu-id="393a4-128">A fájl formázása PowerShell írása</span><span class="sxs-lookup"><span data-stu-id="393a4-128">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)
